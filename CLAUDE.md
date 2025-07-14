# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリで作業する際のガイダンスを提供します。

## プロジェクト概要

[zk](https://github.com/zk-org/zk)ツールを使用したZettelkastenノートシステムです。タイプ別に整理された相互接続されたノートのコレクションを管理します。

### ノートタイプとディレクトリ構造

- **FleetingNotes/**: 一時的な思考やアイデア (`flt-{id}-{timestamp}.md`)
- **PermanentNotes/**: 洗練された永続的な知識 (`{title}.md`)  
- **StructureNotes/**: 組織的・概念的なノート (`{title}.md`)
- **StructureNotes/Literature/**: 文献の基本情報 (`{title}.md`)
- **LiteratureNotes/**: 章・セクション別の詳細ノート (`{title}.md`)

## ノート作成の実装

### 基本的なワークフロー

1. **Fleeting Note**: アイデアや思考の一時的記録 → [.claude/commands/flt.md]
2. **Permanent Note**: Fleeting Noteを統合・洗練 → [.claude/commands/perm.md]
3. **Root Literature Note**: 文献の基本情報記録 → [.claude/commands/rtlit.md]
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

### Root Literature Note 専用フィールド
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

### 情報記録の原則
- **ユーザ入力のみ記載**: ユーザが発言した内容のみを体系的・構造的に記載
- **解釈・考察禁止**: ユーザが発言していない解釈、考察、感想は一切追加しない
- **事実のみ記録**: 解釈ではなく、ユーザの考えや発言そのものを記録

### リンク記載方法
- **Wikiスタイル**: `[[ファイルパス|表示名]]` の形式を使用
- **例**: `[[LiteratureNotes/文献名-章名.md|章名]]`
- **Root参照**: `[[StructureNotes/Literature/文献名.md|文献名]]`

### タグとエイリアス
- **既存タグ優先**: `mcp__zk-mcp__get_tags()`で取得した既存タグを優先使用
- **タグ上限**: 1ノートあたり最大3つまで
- **エイリアス**: 検索性向上のため、英語の別名を1つ付与（Permanent Noteのみ）

## 2層構造の文献管理

### Root Literature Note（StructureNotes/Literature/）
文献の基本情報・概要・目次を管理する中心的なノート

### Literature Note（LiteratureNotes/）
章・セクション別の詳細内容を記録し、Root Literature Noteにリンク
