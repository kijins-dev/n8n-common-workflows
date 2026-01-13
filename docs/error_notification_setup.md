# エラー通知ワークフロー セットアップ手順

## 概要

n8nのError Triggerを使用し、インスタンス内の全ワークフローのエラーをChatworkマイチャットに通知します。

## 前提条件

- n8nクラウド版（michi-gaeru.app.n8n.cloud）
- Chatwork APIトークン
- マイチャットのroom_id: `202698767`

## セットアップ手順

### 1. ワークフローのインポート

1. n8nにアクセス
2. Create new workflow
3. メニュー → Import from JSON
4. `workflows/error_notification.json` の内容を貼り付け

### 2. 認証情報の設定

`Send to Chatwork` ノードで：

1. ノードをダブルクリック
2. Credential to connect with で既存のChatwork認証を選択

**既存の認証がない場合：**

1. Create New Credential → Header Auth
2. Name: `X-ChatWorkToken`
3. Value: あなたのChatwork APIトークン

### 3. 有効化

1. 右上の「Inactive」トグルをクリックして「Active」にする
2. 保存

## 動作確認

Error Triggerは手動テストできないため、以下の方法で確認：

### 方法1: テスト用ワークフローでエラーを起こす

1. 新規ワークフローを作成
2. Manual Trigger + Code ノードを追加
3. Codeノードに以下を記述：

```javascript
throw new Error('テストエラー');
```

4. 実行してマイチャットに通知が届くか確認

### 方法2: 既存ワークフローで意図的にエラー

- HTTP Requestノードで存在しないURLを指定
- 一時的に必須パラメータを削除

## 通知内容

Chatworkに以下の形式で通知されます：

```
[info][title](devil) ワークフローエラー発生[/title]
■ ワークフロー: Chatwork Daily Summary
■ 失敗ノード: HTTP Request
■ エラー内容: Request failed with status code 401
■ 実行ID: abc123
■ 発生時刻: 2026-01-13 15:30:45 (JST)
■ 詳細確認: https://michi-gaeru.app.n8n.cloud/workflow/xxx/executions/abc123
[/info]
```

## 注意事項

| 項目 | 説明 |
|------|------|
| Error Trigger自体のエラー | 無限ループ防止のため通知されない（n8n仕様） |
| 対象範囲 | インスタンス内の全アクティブワークフロー |
| 既存ワークフローへの影響 | なし（変更不要） |

## トラブルシューティング

### 通知が届かない場合

1. ワークフローがActiveか確認
2. Chatwork APIトークンが有効か確認
3. room_idが正しいか確認
4. n8nの実行履歴でError Notificationワークフローの実行状況を確認

## 更新履歴

| 日付 | 内容 |
|------|------|
| 2026-01-13 | 初版作成 |
