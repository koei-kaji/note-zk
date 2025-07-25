---
description: "Literature Note (章・セクション別の詳細ノート) を作成する"
---

## 基本原則

**情報記録原則**: ユーザが発言した内容のみを体系的・構造的に記載し、解釈・考察・感想は一切追加しない。

**文章記述原則**: 極端に箇条書きを採用しない。箇条書きが多すぎると意見やアイデアが丸め込まれ、思考の流れや論理的なつながりが失われる。ユーザの思考を自然な文章形式で記録し、必要最小限の箇条書きのみ使用する。

## ワークフロー

### 1. Source Note特定・確認

**1.1 Source Note特定**
- ユーザ指定のSource Note
- 検索による特定：`mcp__zk-mcp__get_note_paths(include_str="SourceNotes")`
- 未存在時：Source Note作成を提案

**1.2 Source Note内容確認**
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

**⚠️ 重要**: ファイル編集前に必ず `Read` ツールでファイル内容を確認すること。Claude Codeの安全機能により、既存ファイルを変更する前にRead必須。

```
# 必須: ファイル内容確認
Read(file_path: "LiteratureNotes/ファイル名.md")

# その後、編集実行
Edit(
  - body:
    - Source Noteへのwikiリンク: [[ファイルパス|表示名]]
    - 章・セクション情報詳細
    - 内容・要約（ユーザの思考のみ記載）
  - tags: 概念タグ・人名タグ中心
  - extra:
    - chapter: 章・セクション名
    - page: ページ番号・範囲
  - draft: false
)
```

### 3.3 LiteratureNotes特化タグガイドライン

**タグ選択方針**（Source Notesで分野タグ管理済みのため、以下に特化）:
- **専門領域タグ**: `pragmatics`, `phonetics`, `syntax`, `morphology`
- **具体的概念タグ**: `information-structure`, `bics-calp`, `interdependence-hypothesis`
- **研究者タグ**: `jim-cummins`, `stephen-krashen`, `chomsky`

**命名規則**:
- 概念: 正式英語名のkebab-case (`information-structure`)
- 理論: 一般的略語優先（`bics`, `calp`）
- 研究者: `firstname-lastname` (`jim-cummins`)

**タグ抽出のポイント**:
- 章・セクションで言及される主要概念を特定
- 引用・参照される研究者をタグ化
- 抽象的すぎるタグ（`education`, `language`）は避ける

### 4. 相互リンク構築

**4.1 Source Noteへのリンク追加**
```
Read(Source Note path) # 編集前の必須確認
Edit(Source Note) # Literature Notesセクションに新ノートリンク追加
```

**4.2 横断的リンク構築**
```
mcp__zk-mcp__get_linking_notes(path) # 関連Literature Note特定
Read(file_path) # 編集前の必須確認
Edit() # 必要に応じて横断的リンク追加
```

**4.3 完了報告**
リンク構築完了をユーザに報告
