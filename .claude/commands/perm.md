---
description: "Fleeting Note から Permanent Note を作成する"
---

## 基本原則

**情報記録原則**: ユーザが発言した内容のみを体系的・構造的に記載し、解釈・考察・感想は一切追加しない。

## ワークフロー

### 1. 対象Fleeting Note特定・取得

**1.1 検索条件確認**
- 具体的なNote名/ID指定
- キーワード・タグによる検索条件
- テーマ・分野による関連Note群特定

**1.2 Note検索・内容確認**
```
mcp__zk-mcp__get_note_paths(include_str, include_tags, ...)
mcp__zk-mcp__get_note(path) # 必要に応じて内容確認
```

### 2. Fleeting Note分析

- 各ノートの核心アイデア・概念を抽出
- ノート間の共通点・関連性・相違点を分析
- 論理的構造・流れを整理
- 不足情報・発展可能部分を特定

### 3. Permanent Note作成・統合

**3.1 既存タグ取得・Note作成**
```
mcp__zk-mcp__get_tags()
mcp__zk-mcp__create_note(
  title: "統合されたアイデアを表現する明確なタイトル",
  directory: "PermanentNotes"
)
```

**3.2 内容統合・フロントマター更新**
```
Edit(
  - body: 統合された内容（ユーザの思考のみ記載）
  - tags: 既存タグ優先、新規作成は3つまで
  - aliases: ["英語別名"] # 検索性向上のため1つ
  - draft: false
)
```

**注意**: Fleeting Noteのリンク記載は不要（後続ステップで削除検討のため）

### 4. 関連Noteリンク構築

```
mcp__zk-mcp__get_linking_notes(path) # 関連Note特定
Edit() # Wikiスタイルリンク [[ファイルパス|表示名]] 追加
```

### 5. 元Fleeting Note処理提案

- 統合済みFleeting Noteの削除提案
- 部分使用Noteの残存部分処理方針
- Structure Note整理の必要性提案
