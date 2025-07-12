---
title: "tmux"
date: "2025-07-12"
tags: [terminal,tmux]
aliases: []
draft: false
---

# Overview

tmux は主に Pane分割・コピーモードを利用する。セッション管理は積極的には利用しない。

macOS 前提。また、 vim を使う前提でのキーバインディング。

- [dotfiles/.config/tmux/tmux.conf](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.config/tmux/tmux.conf)

# Settings

## Prefix Key

prefix key を `Ctrl+g` に変更する。デフォルトは `Ctrl+b` 。

```tmux title="~/.config/tmux/tmux.conf"
unbind C-b
set -g prefix C-g
bind C-g send-prefix
```

## Reload Command

`tmux.conf` を編集して設定をリロードする場合、以下のコマンドを実行する必要がある。

```bash
tmux source-file ~/.config/tmux/tmux.conf
```

これをすばやくするために、 `<prefix> r` に割り当てる。

```tmux title="~/.config/tmux/tmux.conf"
unbind r
bind r source-file "~/.config/tmux/tmux.conf" \; display "Reloaded tmux conf"
```

## Key Bindings

縦・横の Pane 分割方法にそれぞれ 2 種類のキーバインドを割り当てている：

- 半分に分割
- 表示の 20% サイズで分割

Make コマンドやテストの実行など、補助的に実行したいときは 20% サイズで分割する使い分けをしている。

オプションの `-c '#{pane_current_path}'` は、カレントディレクトリを引き継ぐための設定。
オプションなしで分割すると、毎回ホームディレクトリに戻ってしまうため指定する。

```tmux title="~/.config/tmux/tmux.conf"
bind / split-window -h -c '#{pane_current_path}'
bind ? split-window -p 20 -h -c '#{pane_current_path}'
bind - split-window -v -c '#{pane_current_path}'
bind _ split-window -p 20 -v -c '#{pane_current_path}'
```

画面移動は vim の キーバインド に揃える。


```tmux title="~/.config/tmux/tmux.conf"
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
```

微妙に幅を広げたい時があるので、 `H`, `J`, `K`, `L` でそれぞれサイズ調整できるようにする。

```tmux title="~/.config/tmux/tmux.conf"
bind J resize-pane -D 5
bind K resize-pane -U 5
bind H resize-pane -L 5
bind L resize-pane -R 5
```

## Copy Mode

```tmux title="~/.config/tmux/tmux.conf"
setw -g mode-keys vi            # コピーモードでのキーバインドを vim 風にする
set -s copy-command 'pbcopy'    # コピーモードでコピーした内容をmacOSのクリップボードに送る

bind-key -T copy-mode-vi v      send -X begin-selection
bind-key -T copy-mode-vi C-v    send -X rectangle-toggle
bind-key -T copy-mode-vi y      send -X copy-selection
```

こうすることで、以下のように操作が可能：

1. `<prefix> [` でコピーモード
2. `v` で vim のビジュアルモード風に選択
3. `y` でクリップボードにコピー
4. `Enter` でコピーモード終了

## Color Scheme

[[PermanentNotes/wezterm|WezTerm]] を使用しているので、xterm-256color を指定する。

```tmux title="~/.config/tmux/tmux.conf"
set -g default-terminal "xterm-256color"
```

Color scheme として catppuccin を使用しているので [公式のおすすめ設定](https://github.com/catppuccin/tmux?tab=readme-ov-file#recommended-default-configuration) と同じ設定を適用する。

```tmux
run ~/.config/tmux/plugins/catppuccin/tmux/catppuccin.tmux

# Make the status line pretty and add some modules
set -g status-right-length 100
set -g status-left-length 100
set -g status-left ""
set -g status-right "#{E:@catppuccin_status_application}"
set -agF status-right "#{E:@catppuccin_status_cpu}"
set -ag status-right "#{E:@catppuccin_status_session}"
set -ag status-right "#{E:@catppuccin_status_uptime}"
set -agF status-right "#{E:@catppuccin_status_battery}"

run ~/.config/tmux/plugins/tmux-cpu/cpu.tmux
run ~/.config/tmux/plugins/tmux-battery/battery.tmux
```

## Others

tmux セッション内での default shell を zsh に指定する。

```tmux title="~/.config/tmux/tmux.conf"
set -g default-shell /bin/zsh   # デフォルトシェルを指定する
set -g mouse on                 # マウス操作を有効化する
set -g set-titles on            # ウィンドウタイトルを変更できるようにする
set -s escape-time 50           # Escape キー入力から別のキー入力を受け付けるまでの時間
```

# Appendix
