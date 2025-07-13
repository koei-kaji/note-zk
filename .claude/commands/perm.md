---
description: "Fleeting Note から Permanent Note を作成する"
---

## Capabilities

- `mcp__zk-mcp__get_note_paths`: 条件に基づいてNoteを検索し、パスとタイトル情報を取得する
- `mcp__zk-mcp__get_note`: 指定したパスのNote内容を読み取る
- `mcp__zk-mcp__get_linking_notes`: 指定したNoteとリンク関係にあるNoteを検索・取得する
- `mcp__zk-mcp__get_tags`: 使用されているtagの一覧を取得する
- `mcp__zk-mcp__create_note`: 新しい Note を作成する
- `Edit`: noteの内容を編集する

## Your task

複数のFleeting Noteの内容を整理・統合し、完全な思考のアウトプットとしてPermanent Noteに情報・知識を記録する。

1. 対象となるFleeting Noteを特定・取得する
2. Fleeting Noteの内容を分析・理解する
3. 内容を統合・洗練してPermanent Noteを作成する
4. 関連Noteとのリンク関係を構築する
5. 元のFleeting Noteの処理を提案する

### 1. 対象となるFleeting Noteを特定・取得する

ユーザから統合したいFleeting Noteの情報を受け取る方法：
- 具体的なNote名やIDの指定
- キーワードやタグによる検索条件の提供
- テーマや分野に基づく関連Note群の特定

`mcp__zk-mcp__get_note_paths`を使用してFleeting Noteディレクトリから対象ノートを検索し、
必要に応じて`mcp__zk-mcp__get_note`で内容を確認してください。

### 2. Fleeting Noteの内容を分析・理解する

取得したFleeting Noteについて：
- 各ノートの核心的なアイデアや概念を抽出
- ノート間の共通点・関連性・相違点を分析
- 論理的な構造や流れを整理
- 不足している情報や発展可能な部分を特定

### 3. 内容を統合・洗練してPermanent Noteを作成する

`mcp__zk-mcp__get_tags`で既存タグを取得後、以下の手順でPermanent Noteを作成：

#### 3.1 Permanent Note作成

`mcp__zk-mcp__create_note`を使用：
- title: 統合されたアイデアを表現する明確で検索しやすいタイトル。
- directory: `PermanentNotes`

** Fleeting Note は後続ステップで削除を検討するため、参考情報として FleetingNotes のリンク記載は不要です。**

**重要**: ユーザが発言した内容のみを記載し、あなたの解釈や考察は一切追加しないでください。元のFleeting Noteの内容を統合・洗練する際も、ユーザの思考そのものを整理するのみに留めてください。

#### 3.2 内容の構築

統合された内容を以下の構造で整理：
- **概要**: 主要な概念やアイデアの要約
- **詳細**: 論理的に構造化された本文
- **考察**: より深い洞察や含意
- **関連事項**: 他のテーマや概念との関連性
- **参考**: 元となったFleeting Noteへの参照

#### 3.3 フロントマターの設定

- **tags**: 既存タグを優先使用し、必要に応じて新規作成（3つまで）
- **aliases**: 検索性向上のため、 title の別名（英語）を付与、1つのみ
- **draft**: false（完成されたPermanent Noteのため）

### 4. 関連Noteとのリンク関係を構築する

`mcp__zk-mcp__get_linking_notes`を使用して：
- 作成したPermanent Noteに関連する既存のNoteを特定
- 適切なWikiスタイルリンク（`[[ファイルパス|表示名]]`）を追加
- 双方向のリンク関係を確認・構築

### 5. 元のFleeting Noteの処理を提案する

Permanent Note作成後の元Fleeting Noteについて：
- 統合済みのFleeting Noteの削除を提案
- 部分的に使用されたFleeting Noteの残存部分の処理方針
- Structure Noteでの整理が必要な場合の提案
