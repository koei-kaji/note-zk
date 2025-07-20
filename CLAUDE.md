# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリで作業する際のガイダンスを提供します。

## プロジェクト概要

[zk](https://github.com/zk-org/zk)ツールを使用したZettelkastenノートシステムです。タイプ別に整理された相互接続されたノートのコレクションを管理します。

### ノートタイプとディレクトリ構造

- **FleetingNotes/**: 一時的な思考やアイデア (`flt-{timestamp}-{id}.md`)
- **PermanentNotes/**: 洗練された永続的な知識 (`{title}.md`)
- **StructureNotes/**: 組織的・概念的なノート (`{title}.md`)
- **SourceNotes/**: 文献の基本情報 (`{title}.md`)
- **LiteratureNotes/**: 章・セクション別の詳細ノート (`lit-{timestamp}-{id}.md`)

## ノート作成の実装

### 基本的なワークフロー

1. **Fleeting Note**: アイデアや思考の一時的記録 → [.claude/commands/flt.md]
2. **Permanent Note**: Fleeting Noteを統合・洗練 → [.claude/commands/perm.md]
3. **Source Note**: 文献の基本情報記録 → [.claude/commands/rtlit.md]
4. **Literature Note**: 章別の詳細ノート → [.claude/commands/lit.md]
5. **検索・関連分析**: ノート間の関係把握 → [.claude/commands/find.md]

### MCP ツールによるノート操作

```
# ノート作成
mcp__zk-mcp__create_note(title, directory)

# ノート検索・一覧
mcp__zk-mcp__get_note_paths(include_str, include_tags, exclude_str, exclude_tags)

# ノート内容読み取り
mcp__zk-mcp__get_note(path)

# リンク関係分析
mcp__zk-mcp__get_linking_notes(path)

# タグ一覧取得
mcp__zk-mcp__get_tags()
```

## ノート構造とテンプレート

### 共通フロントマター
```yaml
title: "ノートタイトル"
date: "YYYY-MM-DD"
tags: []
aliases: []
draft: true/false
```

### Source Note 専用フィールド
```yaml
extra:
  type: "Book/Video/Blog/Reference"
  publication: "出版社・媒体"
  published_at: "YYYY-MM-DD"
  authors: ["著者名"]
  url: "URL"
  progress: "TODO/IN PROGRESS/DONE/PENDING/REJECT"
  evaluation: "1-5"
```

### Literature Note 専用フィールド
```yaml
extra:
  chapter: "章・セクション情報"
  page: "ページ番号"
```

## 重要なガイドライン

### リンク記載方法
- **Wikiスタイル**: `[[ファイルパス|表示名]]` の形式を使用
- **例**: `[[LiteratureNotes/文献名-章名.md|章名]]`
- **Source参照**: `[[SourceNotes/文献名.md|文献名]]`

### タグとエイリアス

#### 基本原則
- **言語**: 英語のみ
- **形式**: kebab-case (`jim-cummins`, `information-structure`)
- **一意性確保**: 新規タグ前に `mcp__zk-mcp__get_tags()` で既存確認必須

#### タグカテゴリ（概念分類）
- **分野タグ**: `linguistics`, `education`, `sla`
- **専門領域タグ**: `pragmatics`, `phonetics`, `syntax`
- **概念タグ**: `information-structure`, `bics-calp`, `interdependence-hypothesis`
- **人名タグ**: `jim-cummins`, `stephen-krashen`, `chomsky`

#### ノートタイプ別タグ方針
- **Source Notes**: 分野タグ中心（`sla`, `education`, `linguistics`）
- **Literature Notes**: 概念タグ・人名タグ中心
- **Permanent Notes**: 概念タグ中心
- **Fleeting Notes**: 自由度高め

#### 命名規則
- **概念**: 正式英語名のkebab-case (`information-structure`)
- **理論**: 一般的略語優先（`bics`, `calp`, `sla`）
- **研究者**: `firstname-lastname` (`jim-cummins`)

#### エイリアス
- **Permanent Noteのみ**: 検索性向上のため、英語の別名を1つ付与

## 2層構造の文献管理

### Source Note（SourceNotes/）
文献の基本情報・概要・目次を管理する中心的なノート

### Literature Note（LiteratureNotes/）
章・セクション別の詳細内容を記録し、Source Noteにリンク
