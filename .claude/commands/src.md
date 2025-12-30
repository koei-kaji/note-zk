---
description: "Source Note (文献情報の本体) を作成する"
allowed-tools: mcp__zk-mcp__*, mcp__youtube-mcp__*, Bash(http GET:*), Read, Edit, TodoWrite
argument-hint: [文献タイトル] [URL]
---

## 情報記録原則

**絶対禁止**:
- 推測による情報記載（公式API以外からの情報や憶測での補完は完全禁止）
- 不要項目の追加（ページ数、価格、在庫状況、レビュー等）
- 偽情報の防止（必ずGoogle Books API、youtube-mcp等の公式ツールで情報を検証）
- 解釈の追加（ユーザーが言及していない内容や評価を勝手に追加しない）

**許可される行為**:
- 公式APIから取得した正確な情報のみの記載
- ユーザーが明示的に提供した情報の構造化

## 1. 文献基本情報の確認

引数が提供された場合は`$ARGUMENTS`を解析します。
提供されていない場合は、ユーザーと対話して以下を確認：

- 文献タイトル（正確なタイトル）
- 著者情報
- 種別（Book/Video/Blog/Reference）
- URL（該当する場合）

## 2. 情報取得計画の提示

文献種別に応じた情報取得方法を提示し、y/nで確認を取ります：

### 書籍情報（Google Books API使用）
- タイトル検索: `http GET https://www.googleapis.com/books/v1/volumes q==intitle:書籍名 maxResults==3`
- 著者検索: `http GET https://www.googleapis.com/books/v1/volumes q==inauthor:著者名 maxResults==3`
- ISBN検索: `http GET https://www.googleapis.com/books/v1/volumes q==isbn:ISBN番号 maxResults==3`
- 組み合わせ検索: `http GET https://www.googleapis.com/books/v1/volumes q==intitle:書籍名+inauthor:著者名 maxResults==3`

### YouTube動画情報
- `mcp__youtube-mcp__download_youtube_url`で動画情報と字幕を取得

## 3. 文献情報取得・検証

確認が取れたら公式APIから情報を取得：

1. 適切なAPIを使用して文献情報を取得
2. 取得した情報の正確性を確認
3. 必要情報を整理：
   - 正確な文献タイトル
   - 著者（複数の場合は配列）
   - 出版社・媒体
   - 出版日（YYYY-MM-DD形式）
   - URL（該当時）
   - 概要・要約
   - 目次・構成情報

## 4. Source Note作成・編集

情報取得後、以下を実行：

1. `mcp__zk-mcp__get_tags`で既存タグを取得
2. `mcp__zk-mcp__create_note`でSourceNotesディレクトリにノート作成（タイトルは正確な文献タイトル）
3. `Read`ツールでファイル内容を確認
4. `Edit`ツールで以下を更新：
   - body: 概要セクション（文献要約）、目次・構成セクション（章立て情報）、Literature Notesセクション（空で作成、後で追加予定）
   - tags: 分野タグ中心（既存タグ優先）
   - extra: type（文献種別）、publication（出版社・媒体）、published_at（出版日）、authors（著者配列）、url（該当時）、progress（"TODO"）、evaluation（空で作成）
   - draft: false

## 5. 後続作業の提案

Source Note作成完了後、以下を提案：
- 章別Literature Note作成の案内
- 関連するPermanent Noteとのリンク構築
- Structure Noteでの整理

## 6. 完了報告

作成されたSource Noteの内容と後続作業の提案をユーザーに報告します。
