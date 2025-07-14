---
description: "Note を検索し、情報を取得する"
---

## ワークフロー

### 1. 検索条件最適化

ユーザ入力から検索意図を理解し、条件を設定：

- **文字列検索**: `include_str`（キーワード・タイトル・内容）
- **タグ検索**: `include_tags`（特定タグ）
- **除外検索**: `exclude_str`・`exclude_tags`（不要Note除外）
- **組み合わせ検索**: `AND`/`OR`演算子

### 2. 検索実行・関連Note探索

```
mcp__zk-mcp__get_note_paths(include_str, include_tags, exclude_str, exclude_tags)
mcp__zk-mcp__get_note(path) # 必要に応じて内容確認
mcp__zk-mcp__get_linking_notes(path) # リンク関係（link_to, linked_by, related）
```

### 3. 結果整理・提示

- 該当Note数
- Note一覧（タイトル、パス、簡潔な説明）
- Note内容抜粋（必要時）
- 関連Note情報

### 4. 活用提案

- **関連Note群発見**: 共通テーマ・パターン特定
- **知識ギャップ特定**: 不足情報・観点の指摘
- **次アクション提案**: 新規Note作成・リンク構築
- **関連検索提案**: 追加キーワード・タグの提案
