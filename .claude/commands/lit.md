---
description: "Literature Note (章・セクション別の詳細ノート) を作成する"
allowed-tools: mcp__zk-mcp__*, Read, Edit, TodoWrite
argument-hint: [Source Note] [章・セクション] [内容]
---

## 情報記録原則

**情報記録原則**: ユーザが発言した内容のみを体系的・構造的に記載し、解釈・考察・感想は一切追加しない。

**文章記述原則**: 極端に箇条書きを採用せず、思考の流れや論理的なつながりを自然な文章形式で記録。

## 1. 入力情報の確認

引数が提供された場合は`$ARGUMENTS`を解析します。
提供されていない場合は、ユーザーと対話して以下を確認：

- 対象のSource Note
- 章・セクション情報
- 記録したい内容・思考

## 2. Source Note特定・確認

以下の手順でSource Noteを特定・確認：

1. ユーザー指定のSource Noteまたは検索による特定
2. `mcp__zk-mcp__get_notes`でSourceNotesディレクトリ内を検索
3. 未存在時はSource Note作成を提案
4. `mcp__zk-mcp__get_note_content`でSource Noteの文献基本情報・目次・既存リンクを把握

## 3. 思考内容の明確化

ユーザーの思考・アウトプットを整理し、明確化します。内容が曖昧な場合は追加質問を行い、具体的で思慮深い内容に発展させます。

**重要**: 質問がある場合は次ステップに移らず、ユーザーの回答を必ず待ちます。

## 4. 作業計画の提示と確認

Literature Note作成の具体的な計画を提示し、y/nで確認を取ります：

- ノートタイトル（章・セクション名を含む）
- Source Noteへのリンク方法
- 記載内容（ユーザーの思考のみ）
- 使用する概念タグ・人名タグ
- 章・セクション情報（extraフィールド）

## 5. Literature Note作成・編集

確認が取れたら以下を実行：

1. `mcp__zk-mcp__get_tags`で既存タグを取得
2. `mcp__zk-mcp__create_note`でLiteratureNotesディレクトリにノート作成
3. `Read`ツールでファイル内容を確認
4. `Edit`ツールで以下を更新：
   - body: Source Noteへのwikiリンク `[[ファイルパス|表示名]]`、章・セクション情報詳細、内容・要約（ユーザーの思考のみ記載）
   - tags: 概念タグ・人名タグ中心（LiteratureNotes特化ガイドライン適用）
   - extra: chapter（章・セクション名）、page（ページ番号・範囲）
   - draft: false

## 6. LiteratureNotes特化タグガイドライン

Source Notesで分野タグ管理済みのため、以下に特化：

**タグ選択方針**:
- **専門領域タグ**: `pragmatics`, `phonetics`, `syntax`, `morphology`
- **具体的概念タグ**: `information-structure`, `bics-calp`, `interdependence-hypothesis`
- **研究者タグ**: `jim-cummins`, `stephen-krashen`, `chomsky`

**命名規則**:
- 概念: 正式英語名のkebab-case (`information-structure`)
- 理論: 一般的略語優先（`bics`, `calp`）
- 研究者: `firstname-lastname` (`jim-cummins`)

## 7. 相互リンク構築

必要に応じて以下を実行：

1. Source Noteへのリンク追加: `Read`でSource Note確認後、`Edit`でLiterature Notesセクションに新ノートリンク追加
2. 横断的リンク構築: `mcp__zk-mcp__get_linked_by_notes`と`mcp__zk-mcp__get_link_to_notes`で関連Literature Note特定後、必要に応じて横断的リンク追加

## 8. 完了報告

作成されたLiterature Noteの内容とリンク構築状況をユーザーに報告します。
