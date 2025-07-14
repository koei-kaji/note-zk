---
description: "Root Literature Note (文献情報の本体) を作成する"
---

## 基本原則

**情報記録原則**: ユーザが提供した文献情報のみを記載し、解釈・推測は一切追加しない。

## ワークフロー

### 1. 文献基本情報収集・整理

**必要情報**
- 文献タイトル（正確なタイトル）
- 著者（複数の場合は配列）
- 種別（Book/Video/Blog/Reference）
- 出版社・媒体
- 出版日（YYYY-MM-DD形式）
- URL（該当する場合）
- 概要
- 目次・構成

**情報補完**
```
WebSearch() # 情報不足時、公式サイト（出版社・Amazon等）から取得
```

### 2. Root Literature Note作成

**2.1 既存タグ取得・Note作成**
```
mcp__zk-mcp__get_tags()
mcp__zk-mcp__create_note(
  title: "正確な文献タイトル", # YouTube動画は動画タイトルと完全一致
  directory: "StructureNotes/Literature"
)
```

**2.2 内容・フロントマター更新**
```
Edit(
  - body: 
    - 概要セクション: 文献要約
    - 目次・構成セクション: 章立て情報
    - Literature Notesセクション: 後で追加予定（空）
  - tags: 既存タグ優先、新規作成は3つまで
  - extra:
    - type: 文献種別
    - publication: 出版社・媒体
    - published_at: 出版日
    - authors: 著者配列
    - url: URL（該当時）
    - progress: "TODO"
    - evaluation: "" # 1-5評価（空で作成）
  - draft: false
)
```

### 3. 後続Literature Note作成の提案

章別Literature Note作成の案内を提供。
