---
description: "Fleeting Note から Permanent Note を作成する"
allowed-tools: mcp__zk-mcp__*, Read, Edit, TodoWrite
argument-hint: [Fleeting Note] [統合内容]
---

## 情報記録原則

**情報記録原則**: ユーザが発言した内容のみを体系的・構造的に記載し、解釈・考察・感想は一切追加しない。

## 1. 対象Fleeting Note特定・取得

引数が提供された場合は`$ARGUMENTS`を解析します。
提供されていない場合は、ユーザーと対話して以下を確認：

### 1.1 検索条件確認
- 具体的なNote名/ID指定
- キーワード・タグによる検索条件
- テーマ・分野による関連Note群特定

### 1.2 Note検索・内容確認
`mcp__zk-mcp__get_notes`で条件に応じて検索し、`mcp__zk-mcp__get_note_content`で必要に応じて内容確認

## 2. Fleeting Note分析

対象となるFleeting Noteを分析し、以下を整理：
- 各ノートの核心アイデア・概念を抽出
- ノート間の共通点・関連性・相違点を分析
- 論理的構造・流れを整理
- 不足情報・発展可能部分を特定

## 3. 作業計画の提示と確認

Permanent Note作成の具体的な計画を提示し、y/nで確認を取ります：

- 統合するFleeting Noteの範囲
- 新しいPermanent Noteのタイトル
- 統合内容の構造・流れ
- 使用するタグ・エイリアス
- 元Fleeting Noteの処理方針

## 4. Permanent Note作成・統合

確認が取れたら以下を実行：

### 4.1 既存タグ取得・Note作成

**ファイル命名規則**:
- Permanent Noteのファイル名は**kebab-case（ハイフン区切り小文字）の英語名**を使用する
- 例: `macos-ime-keyboard-shortcut-troubleshooting.md`
- frontmatterの`title`フィールドには日本語タイトルを記載

**手順**:
1. `mcp__zk-mcp__get_tags`で既存タグを取得
2. `mcp__zk-mcp__create_note`でPermanentNotesディレクトリにノート作成
   - `title`パラメータにはkebab-caseの英語ファイル名を指定

### 4.2 内容統合・フロントマター更新
1. `Read`ツールでファイル内容を確認
2. `Edit`ツールで以下を更新：
   - body: 統合された内容（ユーザーの思考のみ記載）
   - tags: 既存タグ優先、新規作成は3つまで
   - aliases: 検索性向上のため英語別名を1つ
   - draft: false

**注意**: Fleeting Noteのリンクは記載しない（後続ステップで削除検討のため）

## 5. 関連Noteリンク構築

必要に応じて以下を実行：
1. `mcp__zk-mcp__get_linked_by_notes`と`mcp__zk-mcp__get_link_to_notes`で関連Note特定
2. `Read`でファイル確認後、`Edit`でWikiスタイルリンク `[[ファイルパス|表示名]]` 追加

## 6. 元Fleeting Note処理提案

以下の提案をユーザーに提示：
- 統合済みFleeting Noteの削除提案
- 部分使用Noteの残存部分処理方針
- Structure Note整理の必要性提案

## 7. 完了報告

作成されたPermanent Noteの内容、リンク構築状況、およびFleeting Note処理提案をユーザーに報告します。
