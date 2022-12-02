---
title: 'モンティホール問題について'
emoji: '🍊'
type: 'idea' # tech: 技術記事 / idea: アイデア
topics: ['MontyHallproblem']
published: false
---

## これは何

モンティホール問題について

- [ぼくは「モンティ・ホール問題」がよくわからない。](https://cruel.hatenablog.com/entry/2022/10/30/214634)

なお、ここであげるデータは[エクセル](https://github.com/papinianus/zenn/blob/main/blobs/monty.xlsx)にまとめた。
こういうときエクセルは依然として非常に有用。

## 「二人がモンティ・ホール問題をやったらどうなるだろう？」あるいは、ハギーワギーの苦悩について

### ハギーワギーが苦悩する状況

まず、次の表を得る。
この表では、「そのまま」つまり最初の選択を変更しなかった場合と「変更」つまり選択を変更した場合とで、それぞれ勝つ事象(TRUE である事象)は均等である。
これが、ハギーワギーの苦悩のもと。

- α 三等分シート

| 正解 | 選択 | モンティ | 変更先 | 可能 | そのまま | 変更  |
| ---- | ---- | -------- | ------ | ---- | -------- | ----- |
| A    | A    | B        | C      | TRUE | TRUE     | FALSE |
| A    | A    | C        | B      | TRUE | TRUE     | FALSE |
| A    | B    | C        | A      | TRUE | FALSE    | TRUE  |
| A    | C    | B        | A      | TRUE | FALSE    | TRUE  |
| B    | A    | C        | B      | TRUE | FALSE    | TRUE  |
| B    | B    | A        | C      | TRUE | TRUE     | FALSE |
| B    | B    | C        | A      | TRUE | TRUE     | FALSE |
| B    | C    | A        | B      | TRUE | FALSE    | TRUE  |
| C    | A    | B        | C      | TRUE | FALSE    | TRUE  |
| C    | B    | A        | C      | TRUE | FALSE    | TRUE  |
| C    | C    | A        | B      | TRUE | TRUE     | FALSE |
| C    | C    | B        | A      | TRUE | TRUE     | FALSE |

#### ハギーワギーが想定する全ての事象

ところで、前記の表の「可能」は、ゲームが可能、つまり成立する場合をフィルタしたもので、正解、選択、モンティ、変更先の全てを列挙すると、次の表となる。
なお「変更先」を設けずに考えることも可能だと思うが、後の検討をやりやすくすることと、実際の TV Show においても、番組製作側が正解を設定する(車とヤギを置く)→ 参加者が選択する → モンティがドアを開ける → 変更する、の流れを履むのに適合的であること、変更しない/した場合をエクセルで表現しやすいこと、といった観点から、変更先を選択の一種とし、かつ変更が妥当であるか、を列として表現した。

- α 想定可能な全てシート

| 正解 | 選択 | モンティ | 変更先 | モンティが正解をあけた | モンティが選択をあけた | 変更してない | モンティに変更 | 可能  | そのまま | 変更  |
| ---- | ---- | -------- | ------ | ---------------------- | ---------------------- | ------------ | -------------- | ----- | -------- | ----- |
| A    | A    | A        | A      | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| A    | A    | A        | B      | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| A    | A    | A        | C      | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| A    | A    | B        | A      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| A    | A    | B        | B      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| A    | A    | B        | C      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| A    | A    | C        | A      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| A    | A    | C        | B      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| A    | A    | C        | C      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| A    | B    | A        | A      | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| A    | B    | A        | B      | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | B    | A        | C      | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | B    | B        | A      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| A    | B    | B        | B      | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| A    | B    | B        | C      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | B    | C        | A      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| A    | B    | C        | B      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | B    | C        | C      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| A    | C    | A        | A      | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| A    | C    | A        | B      | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | C    | A        | C      | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | C    | B        | A      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| A    | C    | B        | B      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| A    | C    | B        | C      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | C    | C        | A      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| A    | C    | C        | B      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | C    | C        | C      | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| B    | A    | A        | A      | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| B    | A    | A        | B      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| B    | A    | A        | C      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | A    | B        | A      | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | A    | B        | B      | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| B    | A    | B        | C      | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | A    | C        | A      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | A    | C        | B      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| B    | A    | C        | C      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| B    | B    | A        | A      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| B    | B    | A        | B      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| B    | B    | A        | C      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| B    | B    | B        | A      | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| B    | B    | B        | B      | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| B    | B    | B        | C      | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| B    | B    | C        | A      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| B    | B    | C        | B      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| B    | B    | C        | C      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| B    | C    | A        | A      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| B    | C    | A        | B      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| B    | C    | A        | C      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | C    | B        | A      | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | C    | B        | B      | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| B    | C    | B        | C      | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | C    | C        | A      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | C    | C        | B      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| B    | C    | C        | C      | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | A    | A        | A      | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | A    | A        | B      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | A    | A        | C      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| C    | A    | B        | A      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | A    | B        | B      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| C    | A    | B        | C      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| C    | A    | C        | A      | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | A    | C        | B      | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | A    | C        | C      | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| C    | B    | A        | A      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| C    | B    | A        | B      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | B    | A        | C      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| C    | B    | B        | A      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | B    | B        | B      | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | B    | B        | C      | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| C    | B    | C        | A      | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | B    | C        | B      | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | B    | C        | C      | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| C    | C    | A        | A      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| C    | C    | A        | B      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| C    | C    | A        | C      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| C    | C    | B        | A      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| C    | C    | B        | B      | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| C    | C    | B        | C      | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| C    | C    | C        | A      | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| C    | C    | C        | B      | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| C    | C    | C        | C      | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |

#### ハギーワギーが苦悩する場合の全事象に確率を振る

前記において、確率は均等なわけだから、全てを 1/3 で選択するとこうなる。

- α 想定可能な全てが均等シート

| 正解 | 正解の選択確率 | 選択 | 同一の正解における選択の選択確率 | モンティ | 同一の正解および選択の組に対するモンティの選択確率 | 変更先 | 同一の正解および選択およびモンティの選択の組に対する変更先の選択確率 | 各自事象の起こる確率 | モンティが正解をあけた | モンティが選択をあけた | 変更してない | モンティに変更 | 可能  | そのまま | 変更  |
| ---- | -------------- | ---- | -------------------------------- | -------- | -------------------------------------------------- | ------ | -------------------------------------------------------------------- | -------------------- | ---------------------- | ---------------------- | ------------ | -------------- | ----- | -------- | ----- |
| A    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| A    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| B    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| C    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| C    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| C    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | A      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | B      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | C        | 0.333333333                                        | C      | 0.333333333                                                          | 0.012345679          | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |

#### ハギーワギーが苦悩する状況は全事象ではない

従って、ハギーワギーが苦悩する状況は 0.01234568 の 12 倍であり 0.14814816 程度。全事象の 1 には程遠い。
(消えた事象がどこにいったかは後述)

#### モンティホール問題におけるゲームが成立する場合の選択確率

現実に、番組を成り立たせる、あるいはモンティホール問題を問題たらしめるためには、正解の決定 → 初回選択 → モンティの開示 → 変更のステップにおいて、特にモンティの開示と、変更には選択に制約がかかり、それぞれ 1/3 ではあり得ない。

実際に選択される可能性は次のようになる。

- α ゲームが成立する確率シート

| 正解 | 正解の選択確率 | 選択 | 同一の正解における選択の選択確率 | モンティ | 同一の正解および選択の組に対するモンティの選択確率 | 変更先 | 同一の正解および選択およびモンティの選択の組に対する変更先の選択確率 | 1           | モンティが正解をあけた | モンティが選択をあけた | 変更してない | モンティに変更 | 可能  | そのまま | 変更  |
| ---- | -------------- | ---- | -------------------------------- | -------- | -------------------------------------------------- | ------ | -------------------------------------------------------------------- | ----------- | ---------------------- | ---------------------- | ------------ | -------------- | ----- | -------- | ----- |
| A    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| A    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.5                                                | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.5                                                | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.5                                                | C      | 1                                                                    | 0.055555556 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.5                                                | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.5                                                | B      | 1                                                                    | 0.055555556 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.5                                                | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | A        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | B    | 0.333333333                      | A        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | A        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | A      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | B      | 0                                                                    | 0           | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | C      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 1                                                  | A      | 1                                                                    | 0.111111111 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 1                                                  | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 1                                                  | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | A        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | C    | 0.333333333                      | A        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | A        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 1                                                  | A      | 1                                                                    | 0.111111111 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 1                                                  | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 1                                                  | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | A      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| A    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | B      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| A    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | C      | 0                                                                    | 0           | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | A      | 0                                                                    | 0           | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | B      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | C      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | B        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | B        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | A    | 0.333333333                      | B        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 1                                                  | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 1                                                  | B      | 1                                                                    | 0.111111111 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 1                                                  | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.5                                                | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.5                                                | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.5                                                | C      | 1                                                                    | 0.055555556 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| B    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.5                                                | A      | 1                                                                    | 0.055555556 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.5                                                | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.5                                                | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 1                                                  | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 1                                                  | B      | 1                                                                    | 0.111111111 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 1                                                  | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | B        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | B        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | C    | 0.333333333                      | B        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | A      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| B    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | B      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| B    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | C      | 0                                                                    | 0           | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | A      | 0                                                                    | 0           | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | B      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | A        | 0                                                  | C      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 1                                                  | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 1                                                  | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 1                                                  | C      | 1                                                                    | 0.111111111 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| C    | 0.333333333    | A    | 0.333333333                      | C        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | C        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | A    | 0.333333333                      | C        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 1                                                  | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 1                                                  | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 1                                                  | C      | 1                                                                    | 0.111111111 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | FALSE    | TRUE  |
| C    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | A      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | B      | 0                                                                    | 0           | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | B        | 0                                                  | C      | 0                                                                    | 0           | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | B    | 0.333333333                      | C        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | C        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| C    | 0.333333333    | B    | 0.333333333                      | C        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.5                                                | A      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.5                                                | B      | 1                                                                    | 0.055555556 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.5                                                | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.5                                                | A      | 1                                                                    | 0.055555556 | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE  | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.5                                                | B      | 0                                                                    | 0           | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.5                                                | C      | 0                                                                    | 0           | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| C    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | A      | 0                                                                    | 0           | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | B      | 0                                                                    | 0           | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| C    | 0.333333333    | C    | 0.333333333                      | C        | 0                                                  | C      | 0                                                                    | 0           | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |

#### モンティホール問題の確率

従ってこの表から次の表を得る

- α ゲームが成立するときの変更の有無による勝率シート

| 正解 | 正解の選択確率 | 選択 | 同一の正解における選択の選択確率 | モンティ | 同一の正解および選択の組に対するモンティの選択確率 | 変更先 | 同一の正解および選択およびモンティの選択の組に対する変更先の選択確率 | 起こる事象の確率 | モンティが正解をあけた | モンティが選択をあけた | 変更してない | モンティに変更 | 可能 | そのまま | 変更  | そのままの勝率 | 変更の勝率  |
| ---- | -------------- | ---- | -------------------------------- | -------- | -------------------------------------------------- | ------ | -------------------------------------------------------------------- | ---------------- | ---------------------- | ---------------------- | ------------ | -------------- | ---- | -------- | ----- | -------------- | ----------- |
| A    | 0.333333333    | A    | 0.333333333                      | B        | 0.5                                                | C      | 1                                                                    | 0.055555556      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | TRUE     | FALSE | 0.055555556    | 0           |
| A    | 0.333333333    | A    | 0.333333333                      | C        | 0.5                                                | B      | 1                                                                    | 0.055555556      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | TRUE     | FALSE | 0.055555556    | 0           |
| A    | 0.333333333    | B    | 0.333333333                      | C        | 1                                                  | A      | 1                                                                    | 0.111111111      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | FALSE    | TRUE  | 0              | 0.111111111 |
| A    | 0.333333333    | C    | 0.333333333                      | B        | 1                                                  | A      | 1                                                                    | 0.111111111      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | FALSE    | TRUE  | 0              | 0.111111111 |
| B    | 0.333333333    | A    | 0.333333333                      | C        | 1                                                  | B      | 1                                                                    | 0.111111111      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | FALSE    | TRUE  | 0              | 0.111111111 |
| B    | 0.333333333    | B    | 0.333333333                      | A        | 0.5                                                | C      | 1                                                                    | 0.055555556      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | TRUE     | FALSE | 0.055555556    | 0           |
| B    | 0.333333333    | B    | 0.333333333                      | C        | 0.5                                                | A      | 1                                                                    | 0.055555556      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | TRUE     | FALSE | 0.055555556    | 0           |
| B    | 0.333333333    | C    | 0.333333333                      | A        | 1                                                  | B      | 1                                                                    | 0.111111111      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | FALSE    | TRUE  | 0              | 0.111111111 |
| C    | 0.333333333    | A    | 0.333333333                      | B        | 1                                                  | C      | 1                                                                    | 0.111111111      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | FALSE    | TRUE  | 0              | 0.111111111 |
| C    | 0.333333333    | B    | 0.333333333                      | A        | 1                                                  | C      | 1                                                                    | 0.111111111      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | FALSE    | TRUE  | 0              | 0.111111111 |
| C    | 0.333333333    | C    | 0.333333333                      | A        | 0.5                                                | B      | 1                                                                    | 0.055555556      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | TRUE     | FALSE | 0.055555556    | 0           |
| C    | 0.333333333    | C    | 0.333333333                      | B        | 0.5                                                | A      | 1                                                                    | 0.055555556      | FALSE                  | FALSE                  | FALSE        | FALSE          | TRUE | TRUE     | FALSE | 0.055555556    | 0           |

### 求める確率

上記を集計すると

- α ゲームが成立するときの変更の有無による勝率シート、表下部

| 変更しない場合の勝率 | 変更した場合の勝率 |
| -------------------- | ------------------ |
| 0.333333333          | 0.666666667        |

## 「逆にドアを減らそう。ドアが 2 つしかなかったとしよう。」

右と左、L と R のドアがあるとする。

### 想定可能な事象

として、次の表を得る。

- β 想定可能な全てが均等シート

| 正解 | 正解の選択確率 | 選択 | 同一の正解に対する選択の選択確率 | モンティ | 同一の正解、選択の組に対するモンティの選択確率 | 変更 | 同一の正解、選択、モンティの選択の組に対する変更の選択確率 | 各事象の確率 | モンティが正解をあけた | モンティが選択をあけた | 変更してない | モンティに変更 | 可能  | そのまま | 変更  |
| ---- | -------------- | ---- | -------------------------------- | -------- | ---------------------------------------------- | ---- | ---------------------------------------------------------- | ------------ | ---------------------- | ---------------------- | ------------ | -------------- | ----- | -------- | ----- |
| L    | 0.5            | L    | 0.5                              | L        | 0.5                                            | L    | 0.5                                                        | 0.0625       | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| L    | 0.5            | L    | 0.5                              | L        | 0.5                                            | R    | 0.5                                                        | 0.0625       | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| L    | 0.5            | L    | 0.5                              | R        | 0.5                                            | L    | 0.5                                                        | 0.0625       | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| L    | 0.5            | L    | 0.5                              | R        | 0.5                                            | R    | 0.5                                                        | 0.0625       | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| L    | 0.5            | R    | 0.5                              | L        | 0.5                                            | L    | 0.5                                                        | 0.0625       | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| L    | 0.5            | R    | 0.5                              | L        | 0.5                                            | R    | 0.5                                                        | 0.0625       | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| L    | 0.5            | R    | 0.5                              | R        | 0.5                                            | L    | 0.5                                                        | 0.0625       | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| L    | 0.5            | R    | 0.5                              | R        | 0.5                                            | R    | 0.5                                                        | 0.0625       | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | L        | 0.5                                            | L    | 0.5                                                        | 0.0625       | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | L        | 0.5                                            | R    | 0.5                                                        | 0.0625       | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| R    | 0.5            | L    | 0.5                              | R        | 0.5                                            | L    | 0.5                                                        | 0.0625       | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | R        | 0.5                                            | R    | 0.5                                                        | 0.0625       | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| R    | 0.5            | R    | 0.5                              | L        | 0.5                                            | L    | 0.5                                                        | 0.0625       | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| R    | 0.5            | R    | 0.5                              | L        | 0.5                                            | R    | 0.5                                                        | 0.0625       | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| R    | 0.5            | R    | 0.5                              | R        | 0.5                                            | L    | 0.5                                                        | 0.0625       | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| R    | 0.5            | R    | 0.5                              | R        | 0.5                                            | R    | 0.5                                                        | 0.0625       | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |

### ゲームが成立する確率

は、ゼロだ。

- β ゲームを成立させる確率シート

| 正解 | 正解の選択確率 | 選択 | 同一の正解に対する選択の選択確率 | モンティ | 同一の正解、選択の組に対するモンティの選択確率 | 変更 | 同一の正解、選択、モンティの選択の組に対する変更の選択確率 | 各事象の確率 | モンティが正解をあけた | モンティが選択をあけた | 変更してない | モンティに変更 | 可能  | そのまま | 変更  |
| ---- | -------------- | ---- | -------------------------------- | -------- | ---------------------------------------------- | ---- | ---------------------------------------------------------- | ------------ | ---------------------- | ---------------------- | ------------ | -------------- | ----- | -------- | ----- |
| L    | 0.5            | L    | 0.5                              | L        | 0                                              | L    | 0.5                                                        | 0            | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |
| L    | 0.5            | L    | 0.5                              | L        | 0                                              | R    | 0.5                                                        | 0            | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| L    | 0.5            | L    | 0.5                              | R        | 0.5                                            | L    | 0                                                          | 0            | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| L    | 0.5            | L    | 0.5                              | R        | 0.5                                            | R    | 0                                                          | 0            | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| L    | 0.5            | R    | 0.5                              | L        | 0.5                                            | L    | 0                                                          | 0            | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| L    | 0.5            | R    | 0.5                              | L        | 0.5                                            | R    | 0                                                          | 0            | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| L    | 0.5            | R    | 0.5                              | R        | 0                                              | L    | 0.5                                                        | 0            | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| L    | 0.5            | R    | 0.5                              | R        | 0                                              | R    | 0.5                                                        | 0            | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | L        | 0                                              | L    | 0.5                                                        | 0            | FALSE                  | TRUE                   | TRUE         | TRUE           | FALSE | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | L        | 0                                              | R    | 0.5                                                        | 0            | FALSE                  | TRUE                   | FALSE        | FALSE          | FALSE | FALSE    | TRUE  |
| R    | 0.5            | L    | 0.5                              | R        | 0                                              | L    | 0.5                                                        | 0            | TRUE                   | FALSE                  | TRUE         | FALSE          | FALSE | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | R        | 0                                              | R    | 0.5                                                        | 0            | TRUE                   | FALSE                  | FALSE        | TRUE           | FALSE | FALSE    | TRUE  |
| R    | 0.5            | R    | 0.5                              | L        | 0.5                                            | L    | 0                                                          | 0            | FALSE                  | FALSE                  | FALSE        | TRUE           | FALSE | TRUE     | FALSE |
| R    | 0.5            | R    | 0.5                              | L        | 0.5                                            | R    | 0                                                          | 0            | FALSE                  | FALSE                  | TRUE         | FALSE          | FALSE | TRUE     | TRUE  |
| R    | 0.5            | R    | 0.5                              | R        | 0                                              | L    | 0.5                                                        | 0            | TRUE                   | TRUE                   | FALSE        | FALSE          | FALSE | TRUE     | FALSE |
| R    | 0.5            | R    | 0.5                              | R        | 0                                              | R    | 0.5                                                        | 0            | TRUE                   | TRUE                   | TRUE         | TRUE           | FALSE | TRUE     | TRUE  |

### つまり。

確かに 2 つしかドアがないときに「ぼく」が正解を選択し、モンティが外れのドアを開けた場合に、ぼくは変更しないことで 100 % の勝率だ。

> これを強調するため、逆にドアを減らそう。ドアが 2 つしかなかったとしよう。ぼくが片方を選んだ。当選確率は 1/2 だ。司会者は残り 1 つを開け、それが外れだということを示した。さて、ぼくが選んだドアの当選確率は？
> 当然ながら、100％だ。

ただ、このときボクは変更することはそもそもできないし、さらにはボクが外れを選択したときモンティには開けられるドアがない。
その想定はゲームをゲームとして成り立たせていない。ゲームを破壊している。

### 従って

モンティホール問題を、問題たらしめているのは、番組を成立させようとするモンティのエンターテイナーシップであり、さらに言えばゲームをゲームとして愉しむ参加者のコラボレーションである。

もし、モンティが番組やゲームのルールを度外視して、正解のドアを開けたり、参加者が選択したドアを開けたりしはじめたり、あるいは参加者が無法にもモンティが開けたドアに変更したり、変更をしていないのに変更したと言い張ったりするとすれば、確かに変更してもしなくても確率は同じであり得る。

しかし、現実には Let's Make A Deal ではそのようなことは起こらなかったし、だからこそ Marilyn が回答する価値があったのだと思う。

## 均等な確率では消えた確率

しかし、山形浩生さんが悪意をもってゲームを破綻させる例を挙げたのでないとすれば、どう考えれば 2 つのドアの場合を考察できるだろうか。
それは、可能世界を含んで確率を考えれば想定できる。

### 可能世界を想定した場合の確率

正解が決定されることと、参加者が選択することは独立に決定できる事柄である。
これに対し、モンティは、正解でも、参加者が選んだのでもないドアを選ばなければならない。このうちより強い要請は正解を開けてはならない。であろう。(原理的に正解でも参加者が選んだのでもないドアを選ぶことにすると、行動できない詰みになるのを回避するため最低限正解は選べない、と仮定する)
また、参加者も変更というからには自身の初回選択とは別の選択をすることが強く要請される。

- γ 可能的ゲーム

| 正解 | 正解の選択確率 | 選択 | 同一の正解に対する選択の選択確率 | モンティ | 同一の正解、選択の組に対するモンティの選択確率 | 変更 | 同一の正解、選択、モンティの選択の組に対する変更の選択確率 | 各事象の確率 | そのまま | 変更  |
| ---- | -------------- | ---- | -------------------------------- | -------- | ---------------------------------------------- | ---- | ---------------------------------------------------------- | ------------ | -------- | ----- |
| L    | 0.5            | L    | 0.5                              | L        | 0                                              | L    | 0                                                          | 0            | TRUE     | TRUE  |
| L    | 0.5            | L    | 0.5                              | L        | 0                                              | R    | 1                                                          | 0            | TRUE     | FALSE |
| L    | 0.5            | L    | 0.5                              | R        | 1                                              | L    | 0                                                          | 0            | TRUE     | TRUE  |
| L    | 0.5            | L    | 0.5                              | R        | 1                                              | R    | 1                                                          | 0.25         | TRUE     | FALSE |
| L    | 0.5            | R    | 0.5                              | L        | 0                                              | L    | 0                                                          | 0            | FALSE    | TRUE  |
| L    | 0.5            | R    | 0.5                              | L        | 0                                              | R    | 0                                                          | 0            | FALSE    | FALSE |
| L    | 0.5            | R    | 0.5                              | R        | 1                                              | L    | 1                                                          | 0.25         | FALSE    | TRUE  |
| L    | 0.5            | R    | 0.5                              | R        | 1                                              | R    | 0                                                          | 0            | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | L        | 1                                              | L    | 0                                                          | 0            | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | L        | 1                                              | R    | 1                                                          | 0.25         | FALSE    | TRUE  |
| R    | 0.5            | L    | 0.5                              | R        | 0                                              | L    | 0.5                                                        | 0            | FALSE    | FALSE |
| R    | 0.5            | L    | 0.5                              | R        | 0                                              | R    | 0.5                                                        | 0            | FALSE    | TRUE  |
| R    | 0.5            | R    | 0.5                              | L        | 1                                              | L    | 1                                                          | 0.25         | TRUE     | FALSE |
| R    | 0.5            | R    | 0.5                              | L        | 1                                              | R    | 0                                                          | 0            | TRUE     | TRUE  |
| R    | 0.5            | R    | 0.5                              | R        | 0                                              | L    | 0                                                          | 0            | TRUE     | FALSE |
| R    | 0.5            | R    | 0.5                              | R        | 0                                              | R    | 0                                                          | 0            | TRUE     | TRUE  |

### 可能的ゲームにおける確率

このとき、「モンティは正解でも参加者が選んだのでもないドアを開けた」、つまり「モンティの行動の時点でゲームのルールが破られなかった」可能世界に限定すると、変更しない場合の勝率は 100 % となる(上記の 4 および 13 行目の事象のみとなり、いずれも変更しないことで当選する)。

しかし、このときゲームは続行不能であり、参加者は、自身の選択でもない、モンティが開けてもいないドアに変更する余地が残されていない。

逆に、モンティホールの問題で着目する「変更が有利となる」可能世界を限定的に取り挙げると、変更した場合の勝率が 100 % となる(上記の 7 および 10 行目の事象となり、いずれも変更することで当選する)。

しかし、このときモンティは初回選択が外れであると示しており、ゲームとして最早成り立っていない。

これらのいずれの事態も、ルールが破綻しているものとして平等に評価すれば、モンティが積極的に答えを教えないし、参加者も変更権を行使しながら同じドアに変更したとは言わないとすれば、変更するもしないも同じ確率と言える。

そしてまさに、モンティがドアを開けて、ルールの破綻が決定的となるまでには、同じ可能性として存在しており、なるほど

> でもそんなはずがあるか？ シュレーディンガーのネコじゃあるまいし。

のとおり、可能世界において、平等に存在すると見られる。

### モンティホール問題を均等だとする世界観

もし、正解の設定、参加者の選択、モンティの開示を独立に決定した全ての多世界が同等に存在すると仮定して、「モンティが正解をあけちゃった」「モンティが参加者が選んだドアを開けちゃった」という世界も平等に存在を認めて俯瞰的に取り扱ったうえで、その可能世界の中からゲームが成立した世界をピックアップして、変更した場合、しなかった場合を取捨すれば、変更してもしなくても確率は等しくなり得る。

そうして、選ばれずに不成立で流れた世界に、消えた 86 % くらいの余事象が存在する。

## 「なぜ問題の言い方を変えただけで話が変わるの？」

> あるいは問題の設定を変えてみよう。
> 「選んだカードを変えますか？」という問題ではなく「最初の選択をご破算にして、どっちか選びなおしてください」という問題設定にしよう。そうなったら、どっちかのドアの後ろに賞品があって、それは等確率だから、どっちを選んでも確率は 1/2 だ。それが、最初にぼくが選んだドアか、そうでないか、というのはまったく問題にならない。そうだよね？ (上にあげた Wikipedia ページにもそう書いてある)。

[wikipedia をナナメ読みしてもどこを指すのか分からなかった](https://en.wikipedia.org/wiki/Monty_Hall_problem#Other_host_behaviors)が、言い方それ自体の問題ではない。その言い方によってモンティの知識や行動が左右され得ることに問題があり、それがゲームを成立させる局面をどの程度絞るかあるいは絞らないかに影響すると考えられる。

## 最後に/「選ぶという「想い」で世界は変わるの？」

選ぶことによっては変わらないが、認識によっては変化し得る。という立場を私は取る。ただこれとハギーワギーの苦悩は関係がない。

ハギーワギーやあるいはテレビ番組視聴者は、自分が選んだと思ったドアが外れとして開けられてしまうこと、あるいはそのことをモンティはドアを開けるときに考慮しないこと、がボクとの決定的な立場の非対称性として存在する。

偶然、ボクとハギーワギーが別のドアを選択し、さらにモンティがこのいずれでもないドアを開けた可能世界ばかりを拾ってくれば、相互に確率は同等になるかもしれない、それくらいの補正があってはじめてハギーワギーはボクと同じ立場に立てる。

> 両者が頭の中でたまたまちがうことを考えただけで、両者にとって同じ物理世界の確率分布がちがうの

ではなく、モンティにとってのゲームの相手は唯一ボクであって、そのことをハギーワギー自身認めており、

> ハギーワギーくんは最初、B のドアを選んでいた。もちろん、場合によっては司会者が B のドアを「ハズレでした」と開けてしまう場合もある

と受容している。ハギーワギーが選んだドアを開けることはあっても、ボクが選んだドアをハズレと開けることはないことにおいてモンティのプロフェッショナリティを信頼しているとさえ言える。

競技クイズの文脈で言えばハギーワギーは解答権を得ていない。
ボタンを付けよう。そうすれば「想い」で世界を変えられる主人公になれるかもしれない。
