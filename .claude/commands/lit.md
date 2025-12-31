---
description: "Literature Note (章・セクション別の詳細ノート) を作成する"
allowed-tools: mcp__zk-mcp__*, Read, Edit
argument-hint: [Source Note] [章・セクション情報]
---

## コマンドの使い方

```
/lit [Source Note] [章・セクション情報]
```

**例**:
```
/lit SourceNotes/AI_Voice_Agents_Automation_with_Vapi_ElevenLabs_n8n_and_MCP.md Section2, Lecture11: Which Platforms Exist for Voice Agents?
```

このコマンドは、Literature Noteの構造のみを作成します。内容は後でユーザーが記載します。

## 1. 引数の解析

`$ARGUMENTS`から以下を抽出：
- Source Note のパス
- 章・セクション情報（Section番号、Lecture番号、タイトルなど）

引数が不足している場合は、ユーザーに確認します。

## 2. Source Note確認

`mcp__zk-mcp__get_note_content`でSource Noteの基本情報を取得：
- 文献タイトル
- 目次・構成
- 既存のLiterature Notesリンク

## 3. 作業計画の提示と確認

Literature Note作成の具体的な計画を提示し、y/nで確認を取ります：

- ノートタイトル（章・セクション名を含む）
- Source Noteへのリンク方法
- 基本タグ（ai, voice-agentsなど）
- 章・セクション情報（extraフィールド）
- 内容は「[後で記載]」

## 4. Literature Note作成・編集

確認が取れたら以下を実行：

1. `mcp__zk-mcp__get_tags`で既存タグを取得
2. `mcp__zk-mcp__create_note`で path=`LiteratureNotes`でノートを作成
3. `Read`ツールでファイル内容を確認
4. `Edit`ツールで以下を更新：
   - title: 章・セクション情報を含むタイトル
   - body: Source Noteへのwikiリンク `[[ファイルパス|表示名]]`、章・セクション情報、内容欄は「[後で記載]」
   - tags: 基本タグのみ（ai, voice-agentsなど、内容に応じて推測可能な最小限のタグ）
   - extra: chapter（章・セクション名）、page（時間や範囲）
   - draft: false

## 5. Source Noteリンク追加

Source Noteの該当セクションの下に、新しいLiterature Noteへのリンクを追加：

```markdown
## セクション2: Technology Fundamentals & How Voice Agents Work (47分)
音声エージェントの基礎技術と動作原理

- [[LiteratureNotes/lit-xxx.md|Lecture 8: タイトル]]
- [[LiteratureNotes/lit-yyy.md|Lecture 9: タイトル]]
```

## 6. 完了報告

作成されたLiterature Noteのパスと、次のステップ（内容記載と`/refine`コマンド使用）をユーザーに報告します。
