---
title: 'Pleasanter をカレンダーに連携させる'
emoji: '🍊'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['pleasanter']
published: true
---

[2022 個人アドベントカレンダー](https://qiita.com/advent-calendar/2022/papinianus) の記事です。

再度、期日に間に合わなかった…

## やりたいこと

- Pleeasanter のカレンダー機能は表示としての一覧性こそあるが、時間ベースの表示やイベント前のアラームなどができないので、既存のカレンダーに連携して補ってもらう

## 方針

カレンダー情報を例えば Google Apps Script のウェブアプリケーションに Post したり、何らかの API に Post してもいいが、投げ先ごとに用意しないといけない。

という手間を惜しむため、iCalendar 形式の添付ファイルをメールで送る。

メリットとして、受け手が複数いて、それぞれ Google カレンダーと OutLook を使っているような場合であっても 1 機能で両方に対応できる。

## 実装

### スクリプト

- 期限付きテーブルの
- 開始と終了をカレンダーの始期、終期とする
- タイトルを件名(メールとカレンダー両方の)に
- 内容を本文に
- 分類 A を To にする

スクリプトの出力先としては「編集」を想定

```javascript
const buildIcs = (title, start, end) => `BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//Pleasanter//Via script//EN
BEGIN:VEVENT
DTSTART:${start.toISOString().replaceAll(/[-:.]/g, '')}
DTEND:${end.toISOString().replaceAll(/[-:.]/g, '')}
SUMMARY:${title}
END:VEVENT
END:VCALENDAR
`;
const mailMessage = (to, title, body, start, end) => ({
  To: to,
  Title: title,
  Body: body,
  Attachments: [
    {
      Name: 'calender.ics',
      ContentType: 'text/calendar ',
      BASE64: btoa(buildIcs(title, new Date(start), new Date(end))),
    },
  ],
});
const sendCal = () => {
  const data = mailMessage(
    $p.getControl('ClassA').val(),
    $p.getControl('Title').val(),
    $p.getControl('Body').val(),
    $p.getControl('開始').val(),
    $p.getControl('完了').val(),
  );
  $.ajax({
    url: $p.apiSendMailUrl($p.id()),
    type: 'post',
    async: false,
    cache: false,
    data: JSON.stringify(data),
    contentType: 'application/json',
    dataType: 'json',
  })
    .done(() => {
      console.log('sent');
    })
    .fail((jqXHR, textStatus, errorThrown) => {
      alert(`mail send error ${errorThrown}`);
    });
};
```

なお、メール送信 API は動的宛先に対応していない。[^1]
今回は時間の都合もあり省略したが、最近のバージョンではメールアドレスは API 取得できるので、担当者のメールアドレスを取得する改修は可能と見込まれる。

### プロセス

- アクション種別を"無し"
- OnClick を "sendCal()"

にしたボタンを置き、これで送信する

## おわりに

- カレンダー連携は考えていたんだけれども Google Apps Script で doPost で受けるのは自己剽窃である以上におもしろくないので、使ったことがないメール送信 API を使ってみた。
- 動的宛先に対応してないのが、想定外だったので、この辺機能拡張されると良いなと思った(というか実装時の対応漏れじゃね?)

[^1]:
    メール送信 API のエントリポイントは ↓
    https://github.com/Implem/Implem.Pleasanter/blob/main/Implem.Pleasanter/Controllers/OutgoingMailsController.cs#L50-L61
    ↓ のあたりでバリデータが降りていって
    https://github.com/Implem/Implem.Pleasanter/blob/02d84f957b783608c2f38943bc7722c6e2c28ae2/Implem.Pleasanter/Models/OutgoingMails/OutgoingMailUtilities.cs#L671
    https://github.com/Implem/Implem.Pleasanter/blob/02d84f957b783608c2f38943bc7722c6e2c28ae2/Implem.Pleasanter/Models/OutgoingMails/OutgoingMailValidators.cs#L48
    https://github.com/Implem/Implem.Pleasanter/blob/02d84f957b783608c2f38943bc7722c6e2c28ae2/Implem.Pleasanter/Models/MailAddresses/MailAddressValidators.cs#L26
    https://github.com/Implem/Implem.Pleasanter/blob/02d84f957b783608c2f38943bc7722c6e2c28ae2/Implem.Pleasanter/Libraries/Mails/Addresses.cs#L131
    実態としては ↓ で検証
    https://github.com/Implem/Implem.Pleasanter/blob/02d84f957b783608c2f38943bc7722c6e2c28ae2/Implem.Pleasanter/Libraries/Mails/Addresses.cs#L13
    なので、To に指定した値がそれ自体として `System.Net.Mail.MailAddress` で FormatException にならないかたちである必要がある。
