# GitHub Issue ソース

## 1. GitHub issue一覧の取得

`gh`コマンドで`fleeting note`ラベルがついたissueを取得します：

```bash
gh issue list --label "fleeting note" --state open --json number,title,body,labels
```

引数でリポジトリが指定された場合は`--repo`オプションを使用：
```bash
gh issue list --repo owner/repo --label "fleeting note" --state open --json number,title,body,labels
```

## 2. 取得したissueの確認

取得したissueの一覧を表示し、処理対象を確認します：
- issue番号
- タイトル
- 本文プレビュー（最初の100文字程度）
- ラベル一覧

複数のissueがある場合は、処理する順序を確認します。

## 3. 各issueの処理

各issueについて以下を実行：

### 3.1 issue内容の提示

現在処理中のissueの詳細を表示：
- **Issue #[番号]**: [タイトル]
- **本文**: [全文]
- **ラベル**: [ラベル一覧]

### 3.2 メインプロセスへ

issue内容を思考内容として、メインプロセス（@.claude/commands/flt.md）の「6段階対話プロトコル」に進みます。

## 4. issue完了処理

Fleeting Note作成完了後：

### 4.1 issueへのコメント

作成したnote pathを含むコメントをissueに投稿：
```bash
gh issue comment [issue番号] --body "Fleeting Note作成完了: [note path]"
```

### 4.2 issueのクローズ

```bash
gh issue close [issue番号]
```

## 5. 次のissueへ

複数issueがある場合、手順3に戻り次のissueを処理します。

## 6. 全体完了報告

すべてのissue処理完了後：
- 作成されたFleeting Noteのリスト
- クローズしたissue番号のリスト

を報告します。
