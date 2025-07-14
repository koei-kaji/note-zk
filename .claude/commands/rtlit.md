---
description: "Root Literature Note (文献情報の本体) を作成する"
---

## Capabilities

- `mcp__zk-mcp__get_tags`: 使用されているtagの一覧を取得する
- `mcp__zk-mcp__create_note`: 新しい Note を作成する
- `Edit`: noteの内容を編集する
- `WebSearch`: ネット検索で文献情報を補完する

## Your task

文献の基本情報を整理し、Root Literature Note（Structure Note）として記録する。この後、章別のLiterature Noteを作成する際の参照元として機能する。

1. 文献の基本情報を収集・整理する
2. 現在のtag一覧を取得する
3. Root Literature Noteを作成する
4. Noteの内容を更新する
5. Noteのfrontmatterを更新する
6. 後続のLiterature Note作成の提案

### 1. 文献の基本情報を収集・整理する

以下の情報を収集・整理してください：
- **文献タイトル**: 正確なタイトル
- **著者**: 著者名（複数の場合は配列で）
- **種別**: Book/Video/Blog/Reference など
- **出版社・媒体**: 出版社名や媒体名
- **出版日**: YYYY-MM-DD形式
- **URL**: オンライン資料の場合
- **進捗状況**: TODO/IN PROGRESS/DONE/PENDING/REJECT
- **評価**: 1-5の評価（任意）
- **概要**: 文献の概要
- **目次・構成**: 章立てや構成情報

情報が不足している場合は、`WebSearch`ツールを使用して文献情報を検索・補完してください。
情報は出版社やAmazonなどの公式といえるサイトから取得してください。

### 2. 現在のtag一覧を取得する

`mcp__zk-mcp__get_tags`を使用し、現在のtag一覧を取得してください。
後続ステップでのtag選択時に既存tagを優先使用するためです。

### 3. Root Literature Noteを作成

`mcp__zk-mcp__create_note`を使用してノートを作成してください：

- title: [正確な文献タイトル]（YouTube動画の場合は動画タイトルと全く同じにする）
- directory: `StructureNotes/Literature`

### 4. Noteの内容を更新する

`mcp__zk-mcp__get_note`でノート内容を取得後、`Edit`ツールで内容を更新してください：

- 概要セクションに文献の要約を記載
- 目次・構成セクションに章立て情報を記載
- Literature Notesセクションは後で追加予定として空にしておく

**重要**: ユーザが提供した文献情報のみを記載し、あなたの解釈や推測は一切追加しないでください。

### 5. Noteのfrontmatterを更新する

文献情報に基づいてfrontmatterを更新してください：

- **tags**: 既存tagsから適切なものを選択、または新規作成（3つまで）
- **title**: 正確な文献タイトルに調整（YouTube動画の場合は動画タイトルと全く同じにする）
- **extra**フィールド:
  - `type`: 文献種別
  - `publication`: 出版社・媒体
  - `published_at`: 出版日
  - `authors`: 著者配列
  - `url`: URL（該当する場合）
  - `progress`: `TODO`
