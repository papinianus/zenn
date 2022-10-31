---
title: 'macOS で急に node が実行できなくなったので volta を入れ直した'
emoji: '🍊'
type: 'tech'
topics:
  - 'nodejs'
  - 'volta'
published: true
---

## 直しかた

```zsh
brew uninstall volta
brew cleanup
rm -rf ~/.volta
brew install volta
volta install@latest
```

## 原因

`~/.volta` の node の symlink が `/opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim` を指していたが、実際は `/opt/homebrew/Cellar/volta/1.1.0/bin/volta-shim` にあった。

```sh
❯ ~/.volta/bin/
❯ ll
total 0
lrwxr-xr-x  1 papinianus  staff    47B  8  6 15:58 node -> /opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim
lrwxr-xr-x  1 papinianus  staff    47B  8  6 15:58 npm -> /opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim
lrwxr-xr-x  1 papinianus  staff    47B  8  6 15:58 npx -> /opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim
lrwxr-xr-x  1 papinianus  staff    47B  8  6 16:04 pnpm -> /opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim
lrwxr-xr-x  1 papinianus  staff    47B  8  6 16:04 pnpx -> /opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim
lrwxr-xr-x  1 papinianus  staff    47B  8  6 15:58 yarn -> /opt/homebrew/Cellar/volta/1.0.8/bin/volta-shim
```

- volta を homebrew でアンインストールしただけでは homedir から .volta が消えず改善しなかった。
  - ので、ディレクトリを削除して対応

## 調べたときにみた情報

- Node.js が突然壊れた話（env: node: No such file or directory）
  https://abillyz.com/watanabe/studies/246
  → 時期的には遠くないが、nodenv なので微妙。ただ入れ直し、でいけてたのでその方向で考える参考とした。
