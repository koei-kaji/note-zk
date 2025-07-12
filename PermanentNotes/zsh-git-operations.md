---
title: "zsh git operations"
date: "2025-07-12"
tags: [terminal,zsh,git]
aliases: [zsh-git]
draft: false
---

# Overview

git 操作を便利にするための設定。

- [dotfiles/.zshrc](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.zshrc)
- [dotfiles/.config/zsh/aliases.zsh](https://github.com/koei-kaji/dotfiles/blob/ed9a134dec91748de136f20f8f8daab12473cc9f/.config/zsh/aliases.zsh)

# Preparation

## Installing Dependencies

ghq, fzf, bat を使うのでインストール。

```zsh
brew install ghq
brew install fzf
brew install bat
```

## Creating Files

`~/.config/zsh/options.zsh` を作成し、 `~/.zshrc` で読み込む。

```zsh
mkdir ~/.config/zsh
touch ~/.config/zsh/aliases.zsh
```

```zsh title="~/.zshrc"
source ~/.config/zsh/aliases.zsh
```

# Settings

```zsh title="~/.config/zsh/aliases.zsh"
alias gget='ghq get'
alias gcd='cd $(ghq root)/$(_ghq-fzf)'
alias gvi='cd $(ghq root)/$(_ghq-fzf) && vim .'
alias gcode='cd $(ghq root)/$(_ghq-fzf) && code .'
alias ghb="open \$(_ghq-fzf | awk '{print \"https://\"\$1}')"

function _ghq-fzf() {
  local src=$(ghq list | fzf --preview "bat --color=always --style=header,grid --line-range :80 $(ghq root)/{}/README.*")
  if [ -n "$src" ]; then
      echo $src
  fi
}

function ghmo() {
    local repo=$(_ghq-fzf)

    case "$repo" in
      *github*)
        open $(echo $repo | awk '{print "https://"$1"/pulls"}')
        ;;
      *gitlab*)
        open $(echo $repo | awk '{print "https://"$1"/-/merge_requests"}')
        ;;
      *)
        echo "No match"
        ;;
    esac
}
function ghmm() {
    local repo=$(_ghq-fzf)

    case "$repo" in
      *github*)
        open $(echo $repo | awk '{print "https://"$1"/pulls?q=is:pr+is:closed"}')
        ;;
      *gitlab*)
        open $(echo $repo | awk '{print "https://"$1"/-/merge_requests?scope=all&sort=merged_at_desc&state=merged"}')
        ;;
      *)
        echo "No match"
        ;;
    esac
}
```

- `gget`: リポジトリを ghq 管理下で clone する
- `gcd`: fzf で リポジトリを検索・選択して移動
- `gvi`: fzf で リポジトリを検索・選択して vim で開く
- `gcode`: fzf で リポジトリを検索・選択して VSCode で開く
- `ghb`: fzf で リポジトリを検索・選択して ブラウザで開く
- `ghmo`: fzf で リポジトリを検索・選択してオープン状態のPull Request or Merge Request をブラウザで開く
- `ghmm`: fzf で リポジトリを検索・選択してマージ済みのPull Request or Merge Request をブラウザで開く
