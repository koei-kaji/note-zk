## プロジェクト概要

[zk](https://github.com/zk-org/zk)ツールを使用したZettelkastenノートシステムです。

### ノートタイプとディレクトリ構造

- **FleetingNotes/**: 一時的な思考やアイデア (`flt-{timestamp}-{id}.md`)
- **PermanentNotes/**: 洗練された永続的な知識 (`{title}.md`)
- **StructureNotes/**: 組織的・概念的なノート (`{title}.md`)
- **SourceNotes/**: 文献の基本情報 (`{title}.md`)
- **LiteratureNotes/**: 章・セクション別の詳細ノート (`lit-{timestamp}-{id}.md`)

### ファイル命名規則

**重要**: ファイルシステムで使用できない特殊文字の扱い

- **禁止文字**: `/` (スラッシュ), `:` (コロン), `"` (ダブルクオーテーション), `*` (アスタリスク), `?` (クエスチョンマーク), `<` `>` (不等号), `|` (パイプ)
- **置き換え規則**: 禁止文字はアンダースコア (`_`) で置き換える
- **適用対象**: ファイル名として使用されるタイトル（PermanentNotes、StructureNotes、SourceNotes）
- **フロントマターのtitleフィールド**: 元の正式タイトル（特殊文字を含む）をそのまま記載

**例**:
- 正式タイトル: `"AI Voice Agents: Automation with Vapi, ElevenLabs, n8n & MCP"`
- ファイル名: `AI_Voice_Agents_Automation_with_Vapi_ElevenLabs_n8n_and_MCP.md`
- frontmatter title: `"AI Voice Agents: Automation with Vapi, ElevenLabs, n8n & MCP"`

**MCP使用時の注意**:
- `mcp__zk-mcp__create_note`の`path`パラメータはディレクトリパスを指定
- `title`パラメータにはファイル名として使用される文字列（特殊文字をアンダースコアに置き換えたもの）を指定
- ノート作成後、`Edit`ツールでfrontmatterの`title`フィールドを正式タイトルに修正

## ノート構造

### フロントマター

```yaml
title: "ノートタイトル"
date: "YYYY-MM-DD"
tags: []           # kebab-case英語タグ
aliases: []        # Permanent Noteのみ
draft: false
```

### Source Note専用フィールド
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

### Literature Note専用フィールド
```yaml
extra:
  chapter: "章・セクション情報"
  page: "ページ番号"
```

## タグシステム

### 基本原則
- **言語**: 英語のみ
- **形式**: kebab-case (`jim-cummins`, `information-structure`)
- **一意性**: 新規タグ作成前の既存確認必須

### カテゴリ別タグ戦略

#### 分野タグ (Source Notes中心)
- `linguistics`, `education`, `sla`

#### 概念タグ (Literature/Permanent Notes中心)
- `information-structure`, `bics-calp`, `interdependence-hypothesis`

#### 研究者タグ (Literature Notes中心)
- `jim-cummins`, `stephen-krashen`, `chomsky`

### 命名規則
- **概念**: 正式英語名のkebab-case
- **理論**: 一般的略語優先（`bics`, `calp`）
- **研究者**: `firstname-lastname`

## リンクシステム

### Wikiスタイルリンク
```
[[ファイルパス|表示名]]
```

### 典型的リンクパターン
```
[[LiteratureNotes/文献名-章名.md|章名]]
[[SourceNotes/文献名.md|文献名]]
[[PermanentNotes/概念名.md|概念名]]
```
## 重要な運用原則

### 情報記録原則
- ユーザー発言内容のみを記載
- 推測・解釈・考察の追加禁止
- 事実に基づく構造化のみ実施

### 品質保証原則
- API連携による情報の正確性確保
- 一貫したフォーマットの維持
- 定期的なシステム整合性チェック

### 効率化原則
- 適切なツール選択による作業最適化
- Sub-AgentsとCommandsの使い分け
- 自動化可能な処理の積極活用
