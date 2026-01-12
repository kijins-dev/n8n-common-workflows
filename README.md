# n8n-common-workflows

n8nワークフロー自動化プロジェクトの共通基盤

## 概要

このリポジトリは、複数のn8nワークフローで共有する以下の機能を管理する：

- **エラー通知**: 全ワークフロー共通のエラーハンドリング
- **重複処理防止**: 冪等性を確保するための状態管理
- **実行ログ**: 標準化されたログ記録

## 関連プロジェクト

| プロジェクト | リポジトリ | 説明 |
|-------------|-----------|------|
| Chatworkログ自動化 | [obsidian_summary_chatwork](https://github.com/kijins-dev/obsidian_summary_chatwork) | Chatworkメッセージの日次要約 |
| Tactiq議事録自動化 | [obsidian_summary](https://github.com/kijins-dev/obsidian_summary) | 会議文字起こしの議事録化 |

## ディレクトリ構成

```
n8n-common-workflows/
├── workflows/
│   ├── error_notification.json    # エラー通知ワークフロー
│   └── ...
├── prompts/
│   ├── base_prompt.md             # 共通プロンプト
│   ├── chatwork_summary.md        # Chatwork用
│   └── meeting_summary.md         # 会議用
├── config/
│   └── room_config_template.csv   # ルーム設定テンプレート
└── docs/
    └── setup.md                   # セットアップ手順
```

## 実装予定

### Phase 1: 安定化（今週）
- [ ] エラー通知ワークフロー
- [ ] 重複処理防止（Tactiq）
- [ ] 価値検証フォーム

### Phase 2: 評価（来週）
- [ ] 品質検証の仕組み
- [ ] 実行ログ標準化

## 技術構成

| 役割 | ツール |
|------|--------|
| ワークフロー実行 | n8n（クラウド版） |
| 要約生成 | Claude API |
| ナレッジ保存 | Obsidian（Local REST API + ngrok） |
| データアーカイブ | Google Sheets |

## 更新履歴

| 日付 | 内容 |
|------|------|
| 2026-01-12 | リポジトリ作成 |
