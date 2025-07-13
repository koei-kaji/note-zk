---
description: "Note を検索し、情報を取得する"
---

## Capabilities

- `mcp__zk-mcp__get_note_paths`: 条件に基づいてNoteを検索し、パスとタイトル情報を取得する
- `mcp__zk-mcp__get_note`: 指定したパスのNote内容を読み取る
- `mcp__zk-mcp__get_linking_notes`: 指定したNoteとリンク関係にあるNoteを検索・取得する
- `mcp__zk-mcp__get_tags`: 使用されているタグの一覧を取得する

## Your task

ユーザの検索要求に基づいて適切なNoteを検索し、情報を提供してください。

### 1. 検索条件の理解と最適化

ユーザの入力から検索意図を理解し、以下の方法で検索条件を設定：

- **文字列検索**: `include_str`でキーワード、タイトル、内容による検索
- **タグ検索**: `include_tags`で特定のタグを持つNoteを検索
- **除外検索**: `exclude_str`や`exclude_tags`で不要なNoteを除外
- **組み合わせ検索**: `AND`/`OR`演算子で複数条件を組み合わせ

### 2. 検索実行

`mcp__zk-mcp__get_note_paths`を使用してNote一覧を取得。
必要に応じて`mcp__zk-mcp__get_note`で具体的な内容を確認。

### 3. 関連Note の探索

検索結果のNoteについて、`mcp__zk-mcp__get_linking_notes`を使用して：
- リンク先のNote（link_to）
- 被リンクのNote（linked_by）
- 関連Note（related）

の情報も提供。

### 4. 結果の整理と提示

検索結果を以下の形式で整理：
- 該当Note数
- Note一覧（タイトル、パス、簡潔な説明）
- 必要に応じてNote内容の抜粋
- 関連Noteの情報

### 5. 検索結果の効果的な活用

検索結果をユーザが効果的に活用できるよう以下を提案：
- **関連性の高いNote群の発見**: 複数のNoteに共通するテーマやパターンの特定
- **知識のギャップの特定**: 検索結果から不足している情報や観点の指摘
- **次のアクション提案**: 検索結果に基づく新規Note作成やリンク構築の提案
- **関連検索の提案**: より深い探索のための追加キーワードやタグの提案
