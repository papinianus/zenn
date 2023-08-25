---
title: 'PostgreSQL 16 beta 3 で新しく Pleasanter を起動してみた'
emoji: '🌊'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: [postgresql, Pleasanter]
published: true
---

## まとめ

- PostgreSQL 15 対応の Pleasanter はそのまま PostgreSQL 16 に適用できそう
  - 16 での変更点[^1]を考えると目立った恩恵はないかも。
- PostgreSQL 15 対応より前の仕様と違ってて、ちょっとはまった

### PostgreSQL 15 対応以前との違い

[プリザンターの直近のバージョンアップ情報](https://pleasanter.org/manual/release-notes-core)[^2]によると 1.3.44 で PostgreSQL 15 対応したのでそれ以前と動作が違う。

> 7/28 リリース情報(ver.1.3.44.0)
> ・PostgreSQL15 対応。

結論として "Implem.Pleasanter" のデータベースの所有者が postgres ではなくなること、および "Implem.Pleasanter" のデータベースが既に存在する場合には Pleasanter が利用するロールを作成しなくなった点で、それ以前までの手順に慣れたユーザが操作すると思わぬはまりかたをする状況にある。

- "Implem.Pleasanter" のデータベースの作成と "pg_trgm" 拡張機能のインストールは CodeDefiner がやってくれる
  - その影響で ↑ のデータベースの所有者が "Implem.Pleasanter_Owner" になる
  - 多分 PostgreSQL 15 で public スキーマがデフォルトで PUBLIC に対して CREATE, USAGE を付与しなくなった[^3]ことをプログラム的に解決したと想像される
  - 14 以前の手順では postgres ユーザで、データベースの作成と拡張機能のインストールを実施する必要があった[^4]
    - postgresql-contrib のパッケージを OS にインストールしてなかったときのエラーの出方が気になる
- 一方で "Implem.Pleasanter" のデータベースが存在すると、"Implem.Pleasanter_Owner" や ""Implem.Pleasanter_User" を作成しなくなった
  - 個人的には docker のイニシャライズスクリプトでデータベースを作成するようにしており、CodeDefiner 実行時にパスワードが違うというエラーになった。[^5]

### 余談：ダッシュボードについて

ダッシュボードのクイックアクセスパーツのレイアウトで横方向と、縦方向が一貫性がない印象。

- 縦方向は
  - パーツを横に伸ばすと、項目も横に伸びる
  - 縦横どちらにパーツを狭めても回り込みは起こらず、縦スクロールが出る
- 横方向は
  - パーツを縦に伸ばしても変化なし(項目は縦に伸びない)
  - 縦に伸ばした場合は回り込みは起こらないが、横に伸ばした場合、回り込みがおき、かつ縦スクロールが出る。横方向のレイアウトなのに横スクロールが出ることがない。

横方向は、カンバン表示のように縦方向に長くして、縦には項目それ自体のエリアが伸び、横方向にスクロール可能にしないと、縦方向と辻褄があってないのではないだろうか。

![dashboard](/images/dc6baaeee75576.gif)

[^1]:
    https://www.postgresql.org/docs/16/release-16.html#RELEASE-16-CHANGES
    https://www.sraoss.co.jp/tech-blog/pgsql/pg16report/
    一般的な性能改善がなされている部分はあたりそうだが、新機能的なところで刺さるものはなさそう。
    例えば pg_dump で lz4/zstd の圧縮が有効になったので、バックアップを多世代とってるなら嬉しいかも。
    その他 Pleasater では、ウィンドウ関数とかパラレルクエリとかは使ってなさそうだし、ユースケース的にロジカルレプリケーションとかもしなさそう。双方向レプリケーションでマルチマスターとかできるけど Pleasnter で何も考えずにやっちゃうと id が衝突しそうで怖い。

[^2]:
    2023/8/25 現在。場合によっては過去の情報に移動するかもしれない。
    https://pleasanter.org/manual/release-notes-core-history

[^3]: https://dev.classmethod.jp/articles/postgresql-15-revoke-create-on-public-schema/
[^4]: https://pleasanter.org/manual/faq-postgresql-14-intall-pleasanter-for-linux
[^5]:
    このとき[PostgreSQL 15 対応マニュアル](https://pleasanter.org/manual/getting-started-pleasanter-ubuntu)を見返して気付いたが、[ココ](https://pleasanter.org/manual/getting-started-pleasanter-ubuntu#:~:text=UID%3Dpostgres%3BPWD%3D-,%3C%E8%A8%AD%E5%AE%9A%E3%81%97%E3%81%9F%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%3E,-%22%2C%0A%20%20%20%20%22OwnerConnectionString)で Rds.json に postgres に設定したパスワードを指定せよ、とあるが、このマニュアルの手順では psql でのログインがないので、パスワードに何を書くかが同定されていない。
    cf. [14 まででの対応手順ではログインしている](https://pleasanter.org/manual/faq-postgresql-14-intall-pleasanter-for-linux#:~:text=PostgreSQL%E7%AE%A1%E7%90%86%E7%94%A8,COPY%20CODE)
