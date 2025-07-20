---
description: "Source Note (文献情報の本体) を作成する"
---

## 基本原則

**情報記録原則**: ユーザが提供した文献情報のみを記載し、解釈・推測は一切追加しない。

## 厳格な禁止事項

**絶対禁止**:
- **推測による情報記載**: 公式API以外からの情報や憶測での補完は完全禁止
- **不要項目の追加**: ページ数、価格、在庫状況、レビュー等の不要な情報は記載しない
- **偽情報の防止**: 必ずGoogle Books API、youtube-mcp等の公式ツールで情報を検証
- **解釈の追加**: ユーザーが言及していない内容や評価を勝手に追加しない

**許可される行為**:
- 公式APIから取得した正確な情報のみの記載
- ユーザーが明示的に提供した情報の構造化

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

**情報取得プロトコル**

**書籍情報取得（Google Books API）**
書籍情報取得には `httpie` の `http` コマンドを使用してください。

```bash
# タイトル検索
http GET https://www.googleapis.com/books/v1/volumes q==intitle:書籍名 maxResults==3

# 著者検索
http GET https://www.googleapis.com/books/v1/volumes q==inauthor:著者名 maxResults==3

# ISBN検索（10桁・13桁両対応）
http GET https://www.googleapis.com/books/v1/volumes q==isbn:ISBN番号 maxResults==3

# タイトルと著者の両方を指定して検索
http GET https://www.googleapis.com/books/v1/volumes q==intitle:書籍名+inauthor:著者名 maxResults==3
```

**注意： q=="intitle:書籍名" のように `"` をつけないでください。**

**YouTube動画情報取得**
```bash
# 動画情報と字幕の取得
mcp__youtube-mcp__download_youtube_url(url)
```

**重要**: 推測による情報記載は厳禁。必ず公式APIから正確な情報を取得すること。

### 2. Source Note作成

**2.1 既存タグ取得・Note作成**
```
mcp__zk-mcp__get_tags()
mcp__zk-mcp__create_note(
  title: "正確な文献タイトル", # YouTube動画は動画タイトルと完全一致
  directory: "SourceNotes"
)
```

**2.2 内容・フロントマター更新**

**⚠️ 重要**: ファイル編集前に必ず `Read` ツールでファイル内容を確認すること。Claude Codeの安全機能により、既存ファイルを変更する前にRead必須。

```
# 必須: ファイル内容確認
Read(file_path: "SourceNotes/ファイル名.md")

# その後、編集実行
Edit(
  - body:
    - 概要セクション: 文献要約
    - 目次・構成セクション: 章立て情報
    - Literature Notesセクション: 後で追加予定（空）
  - tags: 既存タグ優先
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
