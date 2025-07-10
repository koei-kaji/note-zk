# note-zk

[zk](https://github.com/zk-org/zk)ツールを使用したZettelkastenノートシステムです。

## 概要

このリポジトリは相互接続されたノートのコレクションを管理するためのZettelkastenシステムです。ノートは以下のカテゴリに分類されます：

- **FleetingNotes/**: 思いついたアイデアや一時的なメモ
- **PermanentNotes/**: 洗練された永続的な知識
- **StructureNotes/**: トピックを整理するための構造的なノート
- **LiteratureNotes/**: 読書や参考資料からの学び

## セットアップ

### 前提条件

- [zk](https://github.com/zk-org/zk)がインストールされている
- Neovim（エディタとして設定済み）
- fzf（対話的な検索用）
- bat（プレビュー用）
- yq（参考文献生成用）

### 使用方法

#### ノートの作成

```bash
# フリーティングノート（思いついたアイデア）
zk flt "アイデアのタイトル"

# パーマネントノート（洗練された知識）
zk perm "知識のタイトル"

# ストラクチャノート（整理用）
zk str "構造のタイトル"

# 文献ノート（読書記録）
zk lit "文献のタイトル"
```

#### ノートの管理

```bash
# ノートを検索・編集
zk ls

# 最近のノートを編集
zk recent

# 最後に変更したノートを編集
zk editlast

# 内容で検索
zk list --match "検索語句"
```

#### カテゴリ別の操作

```bash
# 各カテゴリのノートを一覧表示
zk ls-flt    # フリーティングノート
zk ls-perm   # パーマネントノート
zk ls-str    # ストラクチャノート
zk ls-lit    # 文献ノート
```

#### その他の便利な機能

```bash
# 変更をGitにコミット・プッシュ
zk git-push

# 文献ノートから引用を生成
zk cit

# ランダムなノートを表示
zk lucky
```

## ノート構造

### 基本的なフロントマター

```yaml
---
title: "ノートタイトル"
date: "2024-01-01"
tags: []
aliases: []
draft: true
---
```

### 文献ノートの追加メタデータ

```yaml
---
# 基本情報に加えて
extra:
  type: "Book"              # Book, Video, Blog, Reference
  publication: "出版社名"
  published_at: "2024-01-01"
  authors: ["著者名"]
  url: "https://example.com"
  evaluation: "4"           # 1-5の評価
---
```

## 設定

システムは`.zk/config.toml`で設定されており、以下の特徴があります：

- 日本語対応
- カスタムファイル名パターン
- Wikiスタイルのリンク
- LSPサポート（デッドリンク検出）
- 各ノートタイプ用のテンプレート
