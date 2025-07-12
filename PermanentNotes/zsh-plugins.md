---
title: "zsh plugins"
date: "2025-07-12"
tags: [terminal,zsh,sheldon]
aliases: []
draft: false
---

# Overview

zsh の plugin manager として [sheldon](https://github.com/rossmacarthur/sheldon) を使用する。
以前は oh-my-zsh を使用していたが、 sheldon の方が設定・管理がシンプルになるため移行。

- [dotfiles/.zshrc](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.zshrc)
- [dotfiles/.config/zsh/plugins.zsh](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.config/zsh/plugins.zsh)
- [dotfiles/.config/sheldon/plugins.toml](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.config/sheldon/plugins.toml)

# Installing sheldon

```zsh
brew install sheldon
```

sheldon の設定は `$XDG_CONFIG_HOME/sheldon/plugins.toml` に記載する。
設定は dotfiles に集約したいため、 `~/.zshenv` で `$XDG_CONFIG_HOME` に `~/.config` を指定する。

```zsh title="~/.zshenv"
export XDG_CONFIG_HOME="$HOME/.config"
```

`sheldon init` を実行する。

```zsh
sheldon init --shell zsh
```

sheldon でインストールした plugin を読み込むため、`~/.zshrc` に追記する。

```zsh title="~/.zshrc"
eval "$(sheldon source)"
```

# Installing plugins

```zsh title="~/.config/sheldon/plugins.toml"
[plugins]

[plugins.zsh-autosuggestions]
github = "zsh-users/zsh-autosuggestions"

[plugins.powerlevel10k]
github = "romkatv/powerlevel10k"

[plugins.zsh-syntax-highlighting]
github = "zsh-users/zsh-syntax-highlighting"

[plugins.zsh-bat]
github = "fdellwing/zsh-bat"

[plugins.zsh-you-should-use]
github = "MichaelAquilina/zsh-you-should-use"
```

- **zsh-autosuggestions**: コマンドを入力する際に、過去のコマンド履歴から候補を自動提案してくれる
- **powerlevel10k**: 高度にカスタマイズ可能な zsh のプロンプトテーマ
- **zsh-syntax-highlighting**: コマンドラインに入力したコマンドの構文をリアルタイムでハイライト表示
- **zsh-bat**: `bat`コマンド（catの代替）をZshで使いやすくするラッパー
- **zsh-you-should-use**: エイリアスを設定しているのに使っていない場合に通知してくれるプラグイン
