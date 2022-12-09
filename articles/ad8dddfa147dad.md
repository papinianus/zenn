---
title: 'Pleasanter x Google 連携:スプレッドシートからデータを書き込む(新規作成・更新編)'
emoji: '🍊'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['googlespreadsheet', 'pleasanter']
published: true
---

- [2022 個人アドベントカレンダー](https://qiita.com/advent-calendar/2022/papinianus) の記事です。

## ゴール

- Google SpreadSheet で編集した内容を Pleasanter に適用する
  - 以下の 2 つを前提としています。
  - [読み取りの記事](https://zenn.dev/ulpianus/articles/0c75008f5fa87d)
  - [削除編](https://zenn.dev/ulpianus/articles/aa0717ed01b749)
    - 特に、「コード.gs」は削除編と同じです。

## コード

- 「削除編」で記載した「コード.gs」の `main` 関数で、既存データが読み込まれている前提です
  - ヘッダ列を妥当にするために必要
- ResultId がある列に対しての編集は更新、ResultId が空白である列に対しての編集は新規作成として処理します。
  - ID がない列にはコピペをする前提です。複数回書き込んでしまうと、その数だけレコードが書き込まれます。

```javascript
const onEdit = (e) => {
  if (e.authMode.toString() === 'LIMITED') return;
  const sheet = e.range.getSheet();
  const data = sheet.getDataRange().getValues();
  const header = data[0];
  const idColName = header.includes('ResultId') ? 'ResultId' : 'IssueId';
  const idCol = header.findIndex((e) => e === idColName);
  const colNums = range(e.range.getColumn() - 1, e.range.getWidth());
  if (!colNums.includes(idCol)) {
    colNums.push(idCol);
  }
  const rowNums = range(e.range.getRow() - 1, e.range.getHeight());
  if (!rowNums.includes(0)) {
    rowNums.push(0);
  }
  const edited = data
    .filter((_, i) => rowNums.includes(i))
    .map((r) => r.filter((_, i) => colNums.includes(i)));
  handler(edited, idColName);
};
const handler = (data, idColName) => {
  const idCol = data[0].findIndex((e) => e === idColName);
  handleDelete(filterDelete(data, idCol));
  handleCreate(buildData(filterCreate(data, idCol)));
  handleUpdate(buildData(filterUpdate(data, idCol)));
};
const needsHash = (str) =>
  /^(Class|Num|Description|Date|Check)[A-Z0-9]+$/.test(str);
const matchHash = (str) =>
  /^(Class|Num|Description|Date|Check)[A-Z0-9]+$/.exec(str);
const assignTo = (obj, key, value) => {
  if (!needsHash(key)) return { ...obj, [key]: value };
  const varType = matchHash(key)[1];
  const sub = { [key]: value };
  const bundleKey = `${varType}Hash`;
  return { ...obj, [bundleKey]: { ...obj[bundleKey], ...sub } };
};
const buildData = (data) => {
  const header = data[0];
  return data
    .slice(1)
    .map((e) => e.reduce((a, c, i) => assignTo(a, header[i], c), {}));
};
const filterDelete = (data, idCol) => {
  const idxDel = data[0].findIndex((e) => e === '削除');
  if (idxDel === -1) return [];
  return data.slice(1).map((e) => e[idCol]);
};
const filterCreate = (data, idCol) => {
  const idxDel = data[0].findIndex((e) => e === '削除');
  return data.filter((e, i) =>
    i === 0
      ? e
      : (e[idCol] === '' || Number(e[idCol]) < 1) &&
        (idxDel === -1 || e[idxDel] === ''),
  );
};
const filterUpdate = (data, idCol) => {
  const idxDel = data[0].findIndex((e) => e === '削除');
  return data.filter((e, i) =>
    i === 0
      ? e
      : e[idCol] !== '' &&
        Number(e[idCol]) > 0 &&
        (idxDel === -1 || e[idxDel] === ''),
  );
};
const handleDelete = (ids) => {
  ids.forEach((e) => post(host, 'records', 'delete', e));
};
const handleUpdate = (objs) => {
  objs.forEach((e) => post(host, 'records', 'update', e['ResultId'], e));
};
const handleCreate = (objs) => {
  objs.forEach((e) => post(host, 'records', 'create', siteId, e));
};
const range = (start, len) => Array.from({ length: len }, (_, i) => start + i);
```

## Google SpreadSheet 連携を作ってみて考えたこと

### 必要性

個人的には Pleasanter を使う上では、テーブルに機能を増築していくのではなく API 連携をして繋ぎ込むことが良いと考えています。

しかし"脱 Excel"を掲げる Pleasanter において SpreadSheet と連携をするのは適切でないと感じました。

具体的には、

- 実用できるものにするハードルが高い
  - マスタ(組織、グループ、ユーザ)と連携させないと、事実上入力ができない
    - CSV インポートでは表示名からコード値を埋めてくれる
  - サイトパッケージを取得して、データ型や選択肢を再構成しないと、正しいデータが作れない
    - 数値、日付、分類の選択肢が思ったようにならない可能性あり
- SpreadSheet でなれけばできないことに乏しい
  - Excel ライクな SpreadSheet の画面は UI として優秀ではあるものの UI としての使い勝手はむしろ Pleasanter 自身の改善で対応して欲しい
    - そもそも多量のデータ入力をすること自体を考え直したほうがいい側面も
  - 強いて言えば、セル関数は依然として SpreadSheet に優位性があるかも
    - 計算式やプロセス機能で何とかなるかもしれない。

### Pleasanter API の取り回しの難しさ

- 必須や範囲のチェックをしない
  - 無効化しているデータ項目への書き込みや、必須条件を満たさない書き込みが受け入れられてしまう。
  - 例えば ResultId だけを Update したとしても「更新しました」と応答する
- エラーの対応のしにくさ
  - 特権ユーザ以外ではシステム上でログを見る方法がないが、見たとしても JSON に対して「不正なデータ」であるときの具体的な不備が見えない

ただ、システムとして画面から入力することに主眼を置いていると捉えているので、改善されればよいが欠点とは思いません。

## さいごに

- システム連携をすることで解決できる課題が何かを考える
  - SpreadSheet に連携したいと言われたら、掘り下げるべき
- できれば Pleasanter から連携しに行く(連携を受けるのではなく)

といったことを意識したい。
