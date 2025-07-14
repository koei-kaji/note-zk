---
description: "Literature Note (章・セクション別の詳細ノート) を作成する"
---

## 基本原則

**情報記録原則**: ユーザが発言した内容のみを体系的・構造的に記載し、解釈・考察・感想は一切追加しない。

## ワークフロー

### 1. Root Literature Note特定・確認

**1.1 Root Note特定**
- ユーザ指定のRoot Literature Note
- 検索による特定：`mcp__zk-mcp__get_note_paths(include_str="StructureNotes/Literature")`
- 未存在時：Root Literature Note作成を提案

**1.2 Root Note内容確認**
```
mcp__zk-mcp__get_note(path) # 文献基本情報・目次・既存リンクを把握
```

### 2. 思考内容の明確化

ユーザの思考・アウトプットを整理し、明確にする。内容が曖昧な場合は追加質問を行い、具体的で思慮深い内容に発展させる。

**重要**: 質問がある場合は次ステップに移らず、ユーザの回答を必ず待つ。

### 3. Literature Note作成

**3.1 既存タグ取得・Note作成**
```
mcp__zk-mcp__get_tags()
mcp__zk-mcp__create_note(
  title: "章・セクション名を含む適切なタイトル",
  directory: "LiteratureNotes"
)
```

**3.2 内容・フロントマター更新**
```
Edit(
  - body:
    - Root Literature Noteへのwikiリンク: [[ファイルパス|表示名]]
    - 章・セクション情報詳細
    - 内容・要約（ユーザの思考のみ記載）
  - tags: Root Noteと整合性のあるタグ（3つまで）
  - extra:
    - chapter: 章・セクション名
    - page: ページ番号・範囲
  - draft: false
)
```

### 4. 相互リンク構築

**4.1 Root Literature Noteへのリンク追加**
```
Edit(Root Literature Note) # Literature Notesセクションに新ノートリンク追加
```

**4.2 横断的リンク構築**
```
mcp__zk-mcp__get_linking_notes(path) # 関連Literature Note特定
Edit() # 必要に応じて横断的リンク追加
```

**4.3 完了報告**
リンク構築完了をユーザに報告
