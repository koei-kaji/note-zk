# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

このリポジトリは[zk](https://github.com/zk-org/zk)ツールを使用したZettelkastenノートシステムです。タイプ別に整理された相互接続されたノートのコレクションを管理します：

- **FleetingNotes/**: タイムスタンプベースのファイル名を持つ一時的なノート (`flt-{id}-{timestamp}.md`)
- **PermanentNotes/**: 洗練された永続的なノート (`perm-{id}-{timestamp}.md`)
- **StructureNotes/**: スラッグベースのファイル名を使用した組織的なノート (`{slug-title}.md`)
- **LiteratureNotes/**: メタデータを持つ文献ノート (`lit-{id}-{timestamp}.md`)

## アーキテクチャ

システムは`.zk/config.toml`のzk設定を中心に構築されています：

- **ノートテンプレート**: `.zk/templates/`にメタデータ用のフロントマター付きで配置
- **グループ**: 異なるノートタイプには独自のファイル名パターンとテンプレート
- **言語**: 日本語(`ja`)用に設定、カスタムスラッグ対応
- **リンク**: Wikiスタイルのリンク(`[[note-title]]`)を使用
- **データベース**: インデックスと検索用のSQLiteデータベース`.zk/notebook.db`

## Claude Code での操作方法

Claude Code環境では、zkコマンドの代わりにMCP (Model Context Protocol) zk-mcpツールを使用してノートを管理します。

### ノート作成

```
# ノートの作成
mcp__zk-mcp__create_note を使用
- title: ノートタイトル
- directory: 作成先ディレクトリ（オプション）
```

### ノート管理・検索

```
# ノートの検索・一覧取得
mcp__zk-mcp__get_note_paths を使用
- include_str: 内容やファイル名に含む文字列でフィルタ
- exclude_str: 除外する文字列
- include_tags: 含めるタグ
- exclude_tags: 除外するタグ

# ノート内容の読み取り
mcp__zk-mcp__get_note を使用
- path: ノートファイルのパス

# リンク関係の分析
mcp__zk-mcp__get_linking_notes を使用
- path: 対象ノートのパス
- 戻り値: リンク先、被リンク、関連ノート

# タグの取得
mcp__zk-mcp__get_tags を使用
- 全てのタグの一覧を取得
```

## Claude Code でのノート操作ガイダンス

### 基本的な使用方針

- **ノート作成**: `mcp__zk-mcp__create_note`を使用し、適切なディレクトリとタイトルを指定
- **ノート検索**: `mcp__zk-mcp__get_note_paths`で条件に合うノートを検索
- **内容確認**: `mcp__zk-mcp__get_note`で特定のノートの内容を読み取り
- **関連分析**: `mcp__zk-mcp__get_linking_notes`でノート間の関係を把握

### 検索とフィルタリング

- **文字列検索**: `include_str`で内容やファイル名に含む文字列を指定
- **タグ検索**: `include_tags`で特定のタグを持つノートを検索
- **除外検索**: `exclude_str`や`exclude_tags`で不要なノートを除外
- **演算子**: `AND`/`OR`で複数条件の組み合わせ方を指定

### 日本語ノート管理のポイント

- **スラッグ**: 日本語タイトルは自動的にスラッグ化される
- **タグ**: 日本語タグも適切に処理される
- **検索**: 日本語の内容検索も正常に動作する

## 設定

### Claude Code環境

- **MCP連携**: zkツールがMCP経由で利用可能
- **ノート管理**: 全てのノート操作はMCPツールを通じて実行
- **検索機能**: 高度な検索・フィルタリング機能を提供

## ノート構造

デフォルトノートには以下のフロントマターが含まれます：
- `title`: ノートタイトル
- `date`: 作成日 (YYYY-MM-DD)
- `tags`: タグの配列
- `aliases`: 別名の配列
- `draft`: ドラフトステータス（真偽値）

文献ノートには追加のメタデータが含まれます：
- `type`: 書籍/動画/ブログ/参考資料
- `publication`: 出版物名
- `published_at`: 出版日
- `authors`: 著者名の配列
- `url`: ソースURL
- `evaluation`: 評価（1-5）
