# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリで作業する際のガイダンスを提供します。

## プロジェクト概要

[zk](https://github.com/zk-org/zk)ツールを使用したZettelkastenノートシステムです。Sub-AgentsとSlash Commandsを活用した効率的なノート管理システムを提供します。

### ノートタイプとディレクトリ構造

- **FleetingNotes/**: 一時的な思考やアイデア (`flt-{timestamp}-{id}.md`)
- **PermanentNotes/**: 洗練された永続的な知識 (`{title}.md`)
- **StructureNotes/**: 組織的・概念的なノート (`{title}.md`)
- **SourceNotes/**: 文献の基本情報 (`{title}.md`)
- **LiteratureNotes/**: 章・セクション別の詳細ノート (`lit-{timestamp}-{id}.md`)

## Sub-Agents システム

### 利用可能なSub-Agents

#### 1. zk-note-manager
**用途**: 総合的なノート管理と品質保証
- ノート作成・編集・検索の統合管理
- システム整合性の維持と品質管理
- 複数ノートタイプの横断的操作

**使用場面**:
- 複雑なノート操作や一括管理
- システム全体の整合性確認
- 品質管理とバリデーション

#### 2. literature-researcher
**用途**: 学術文献研究とAPI連携
- Google Books API連携による正確な文献情報取得
- YouTube動画の字幕・メタデータ処理
- Source/Literature Note作成の自動化

**使用場面**:
- 新しい文献のSource Note作成
- API連携が必要な情報取得
- 学術的厳密性が要求される作業

#### 3. knowledge-synthesizer
**用途**: 知識統合と構造化
- 複数Fleeting NoteからPermanent Note作成
- 概念間関係の分析と統合
- Structure Note設計と作成

**使用場面**:
- 散在する思考の統合
- 複雑な概念の体系化
- 知識領域の構造設計

#### 4. tag-organizer
**用途**: タグ管理と分類最適化
- kebab-case英語タグの一貫性維持
- ノートタイプ別タグ戦略の適用
- タグ階層とカテゴリの最適化

**使用場面**:
- タグシステムの整理・最適化
- 新規タグの検証と作成
- 分類体系の見直し

#### 5. link-builder
**用途**: ノート間リンク構築と最適化
- ノート間関係の分析と可視化
- 戦略的リンク構築
- ナレッジネットワークの最適化

**使用場面**:
- 関連ノートの発見と接続
- ナビゲーション改善
- 知識ネットワークの構造化

### Sub-Agents呼び出し方法

```
@zk-note-manager [タスク内容]
@literature-researcher [文献情報・URL]
@knowledge-synthesizer [統合対象の説明]
@tag-organizer [タグ関連作業]
@link-builder [リンク構築作業]
```

## Slash Commands システム

### 基本的なWorkflow Commands

- `/flt [タイトル] [思考内容]` - Fleeting Note作成
- `/perm [Fleeting Note] [統合内容]` - Permanent Note作成
- `/src [文献タイトル] [URL]` - Source Note作成
- `/lit [Source Note] [章・セクション] [内容]` - Literature Note作成
- `/find [検索キーワード] [タグ]` - ノート検索
- `/edit [ファイルパス] [追記内容]` - 既存ノート編集

## 効果的な使い分け指針

### タスクの複雑さによる使い分け

#### 単純作業 → Slash Commands
- 単一ノートの作成・編集
- 決まったフォーマットでの情報記録
- 標準的なワークフローの実行

#### 複雑作業 → Sub-Agents
- 複数ノートの関係性分析
- API連携を伴う情報取得
- システム全体の最適化作業

### 専門性による使い分け

#### 文献研究
1. **新規文献**: `/src` または `@literature-researcher`
2. **章別詳細**: `/lit` または `@literature-researcher`
3. **関連分析**: `@knowledge-synthesizer`

#### 思考整理
1. **アイデア記録**: `/flt`
2. **思考統合**: `/perm` または `@knowledge-synthesizer`
3. **構造化**: `@knowledge-synthesizer`

#### システム管理
1. **品質管理**: `@zk-note-manager`
2. **タグ整理**: `@tag-organizer`
3. **リンク構築**: `@link-builder`

## ノート構造ガイドライン

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

## 推奨ワークフロー

### 1. 日常的な思考記録
```
/flt [思考タイトル] [内容] → 定期的統合 → @knowledge-synthesizer
```

### 2. 文献研究プロセス
```
@literature-researcher [文献情報] → /lit [章別内容] → @link-builder
```

### 3. 知識体系化
```
@knowledge-synthesizer [統合対象] → @tag-organizer [分類] → @link-builder [関係構築]
```

### 4. システムメンテナンス
```
@zk-note-manager [品質管理] → @tag-organizer [タグ整理] → @link-builder [リンク最適化]
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