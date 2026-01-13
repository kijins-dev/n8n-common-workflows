# エラー通知ワークフロー セットアップ手順

## 概要

n8nのError Triggerを使用し、インスタンス内の全ワークフローのエラーをChatworkに通知する。

## 仕組み

- Error Triggerはn8nインスタンス全体のエラーを自動でキャッチ
- 既存ワークフローの変更は一切不要
- 有効化するだけで全ワークフローが監視対象になる

## 前提条件

- n8nクラウド版（michi-gaeru.app.n8n.cloud）
- Chatwork APIトークン（Header Auth設定済み）
- 通知先room_id: `252085376`（botとの個別チャット）

## セットアップ手順

### 1. ワークフローのインポート

1. n8nにアクセス
2. Workflows → Import from File
3. `workflows/error_notification.json` を選択

### 2. 認証情報の設定

「Chatwork Send」ノードで既存のChatwork APIクレデンシャルを選択

### 3. 有効化

右上のトグルをONにする

## 動作確認方法

既存ワークフローで意図的にエラーを起こす（例：HTTPノードのURLを壊す）

## 通知内容

```
[info][title]n8n エラー通知[/title]
発生時刻: 2026/1/13 15:45:21
ワークフロー: Example Workflow
失敗ノード: HTTP Request
エラー内容: 401 Unauthorized

実行ログ: https://michi-gaeru.app.n8n.cloud/workflow/.../executions/...
[/info]
```

## 注意事項

| 項目 | 説明 |
|------|------|
| 正常終了時 | 通知されない（エラー時のみ） |
| Error Trigger自体のエラー | 無限ループ防止のため通知されない |
| 対象範囲 | インスタンス内の全アクティブワークフロー |

## トラブルシューティング

### 通知が届かない場合

1. ワークフローがActiveか確認
2. Chatwork APIトークンが有効か確認
3. room_idが正しいか確認
4. n8nの実行履歴でエラー通知ワークフローの状況を確認

## 更新履歴

| 日付 | 内容 |
|------|------|
| 2026-01-13 | 動作確認完了、room_idを252085376に変更 |
| 2026-01-13 | 初版作成 |
