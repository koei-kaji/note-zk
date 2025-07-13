---
description: "Literature Note (章・セクション別の詳細ノート) を作成する"
---

## Capabilities

- `mcp__zk-mcp__get_note_paths`: 条件に基づいてNoteを検索し、パスとタイトル情報を取得する
- `mcp__zk-mcp__get_note`: 指定したパスのNote内容を読み取る
- `mcp__zk-mcp__get_linking_notes`: 指定したNoteとリンク関係にあるNoteを検索・取得する
- `mcp__zk-mcp__get_tags`: 使用されているtagの一覧を取得する
- `mcp__zk-mcp__create_note`: 新しい Note を作成する
- `Edit`: noteの内容を編集する

## Your task

Root Literature Noteに関連する章・セクション別のLiterature Noteを作成し、詳細なアイデアや知識を記録する。

1. Root Literature Noteを特定・確認する
2. ユーザの思考・アウトプットを明確化し、正確な情報を残す
3. 現在のtag一覧を取得する
4. Literature Noteを作成する
5. Noteの内容を更新する
6. Noteのfrontmatterを更新する
7. Root Literature Noteとの相互リンクを構築する

### 1. Root Literature Noteを特定・確認する

以下の方法でRoot Literature Noteを特定してください：

- ユーザから直接Root Literature Noteの指定を受ける
- `mcp__zk-mcp__get_note_paths`でStructureNotesディレクトリから文献ノートを検索
- 該当するRoot Literature Noteが見つからない場合は、先にRoot Literature Note作成を提案

`mcp__zk-mcp__get_note`でRoot Literature Noteの内容を確認し、以下の情報を把握：
- 文献の基本情報
- 目次・構成
- 既存のLiterature Noteリンク

### 2. ユーザの思考・アウトプットを明確化し、正確な情報を残す

ユーザの思考・アウトプットを整理し、明確にする手伝いをしてください。
内容が曖昧な場合は、追加の質問を行って具体的で思慮深い内容に発展させてください。
質問がある場合は、次のステップに移らずにユーザの回答を必ず待ってください。

### 3. 現在のtag一覧を取得する

`mcp__zk-mcp__get_tags`を使用し、現在のtag一覧を取得してください。
Root Literature Noteのtagも参考にして、一貫性のあるtagging戦略を採用してください。

### 4. Literature Noteを作成

`mcp__zk-mcp__create_note`を使用してノートを作成してください：

- title: [章・セクション名を含む適切なタイトル]
- directory: `LiteratureNotes`

### 5. Noteの内容を更新する

`mcp__zk-mcp__get_note`でノート内容を取得後、`Edit`ツールで内容を更新してください：

- Root Literature Noteセクションにwikiリンクを追加（`[[ファイルパス|表示名]]`形式）
- 章・セクション情報を詳細に記載
- 内容・要約セクションに章の要約を記述
- 重要な概念・アイデアセクションに主要概念を整理
- 引用・メモセクションに重要な引用や参考情報を記載

**重要**: ユーザが発言した内容のみを記載し、あなたの解釈や考察は一切追加しないでください。

### 6. Noteのfrontmatterを更新する

章・Root Note情報に基づいてfrontmatterを更新してください：

- **tags**: Root Literature Noteと整合性のあるタグを選択（3つまで）
- **title**: 章・セクション名を含む適切なタイトルに調整
- **extra**フィールド:
  - `chapter`: 章・セクション名
  - `page`: ページ番号や範囲

### 7. Root Literature Noteとの相互リンクを構築する

Literature Note作成完了後：

1. Root Literature Noteの「関連Literature Notes」セクションに新しいLiterature Noteへのリンクを追加（`[[ファイルパス|表示名]]`形式）
2. 必要に応じて他の関連Literature Noteとの横断的リンクも構築
3. リンク構築完了の確認をユーザに報告
