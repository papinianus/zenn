---
title: 'GitHub の README としてレンダーされるファイル名'
emoji: '🍊'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['github']
published: true
---

# 調べたこと

- `/^readme(\..+)*$/i` なファイル名の README が展開されていそう
- レンダリングでサポートされている markup 書式は[こちら](https://github.com/github/markup)

## 実際に確認したこと

この[レポジトリ](https://github.com/papinianus/ofreadme)で確認しています。

### md でファイル名を確認

ファイル内容が表示されたパターン

- README.md
- ReadMe.md
- Readme.md
- readMe.md
- readme.md

ファイル内容が表示されなかったパターン

- READ_ME.md
- read_me.md
- read-me.md

### 大文字小文字について

- 大文字小文字は無視されている
  - OS によって、大文字小文字を区別しないパターンがあるのを考慮していそう
- 記号おを含めると読みこまれない
  - 1 フレーズとして書く必要がある

### 拡張子の確認

ファイル内容が表示されたパターン

- readme
- readme.txt
- readme.mp4 (内容はテキスト)
- readme.jpg (内容はテキスト)

ファイル内容が表示されなかったパターン

- readme.
- readmenone
- readme.png (画像)

### 拡張子について

- 拡張子がない、もしくは拡張子がある場合、内容は表示されそう
  - レンダリングはされない(レンダリングルールがない)が、内容は表示される
- file コマンド相当で内容のチェックをしていそう
- readme の後に余計な文字があると表示されなさそう

## そもそもなんで大文字なの

[StackExchange](https://softwareengineering.stackexchange.com/questions/301691/readme-txt-vs-readme-txt/301708#301708)をみると、アスキーソートされたときに CAPITAL が先に出てくるので、REDAME とか LICENSE とかを大文字にして上に表示させているよう。

## まとめ

README(全部大文字)じゃないとだめ、みたいな会話が社内であって、個人的に `Readme.md` を使ってたりしたので、ないわー、と思ったので調べてみた。

結論としては ↓ が妥当だと思っている。
https://github.com/sindresorhus/ama/issues/197#issuecomment-126047560

> Aesthetics. It looks better lowercased. And there's no longer any practical reason to uppercase it.
