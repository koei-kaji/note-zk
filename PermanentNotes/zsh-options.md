---
title: "zsh options"
date: "2025-07-12"
tags: [terminal,zsh]
aliases: [zsh-options]
draft: false
---

# Overview

zsh で追加設定するオプションをまとめる。

- [dotfiles/.zshrc](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.zshrc)
- [dotfiles/.config/zsh/options.zsh](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.config/zsh/options.zsh)

# Preparation

`~/.config/zsh/options.zsh` を作成し、 `~/.zshrc` で読み込む。

```zsh
mkdir ~/.config/zsh
touch ~/.config/zsh/options.zsh
```


```zsh title="~/.zshrc"
source ~/.config/zsh/options.zsh
```

# Settings

## Directory Operations

```zsh title="~/.config/zsh/options.zsh"
setopt auto_pushd pushd_ignore_dups auto_cd
```

- `auto_pushd`: ディレクトリ変更時に自動的に `pushd` コマンドを使い、ディレクトリ履歴を保存する
- `pushd_ignore_dups`: 同じディレクトリが `pushd` スタックに重複して追加されることを防ぐ
- `auto_cd`: コマンドとして認識されない文字列を入力した場合、ディレクトリパスとして解釈してそこに移動する

## Command History

```zsh title="~/.config/zsh/options.zsh"
setopt hist_ignore_dups share_history inc_append_history
```

- `hist_ignore_dups`: 連続して同じコマンドを実行した場合、履歴に1つだけ保存する
- `share_history`: 異なるセッション間でもコマンド履歴を共有する
- `inc_append_history`: コマンド実行後すぐに履歴ファイルに書き込む

## Menu Completion

```zsh title="~/.config/zsh/options.zsh"
setopt noautomenu nomenucomplete
```

- `noautomenu`: 自動メニュー補完機能を無効化する
- `nomenucomplete`: メニュー補完を無効化する

## Vi Mode

```zsh title="~/.config/zsh/options.zsh"
set -o vi
bindkey "jj" vi-cmd-mode
```

- `set -o vi`: シェルのキーバインドをViモードに設定する
- `bindkey "jj" vi-cmd-mode`: 挿入モードで「jj」というキーシーケンスを入力するとコマンドモードに切り替わるショートカットを設定する
