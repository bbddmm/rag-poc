# Infra AGENTS.md

## 技術スタック

| 項目 | 選定 | 備考 |
| -------- | ---- | ---- |
| IaC | SST v3 (Ion) | Pulumi/Terraformベース、CDKより記述量少 |
| CI/CD | GitHub Actions | lint, deploy |

## 設計方針

- **SST v3**: `link` で権限自動付与、`sst dev` でライブデバッグが可能
- **transform**: 低レベルの設定変更が必要な場合は `transform` を使用して対応する
- **差分確認**: スナップショットテストは行わない。デプロイ前に `sst diff` で差分を確認する
- **state管理**: SSTのstate管理は自前（S3）

## デプロイ先構成

| リソース | サービス |
| -------- | ---- |
| フロントエンド | Amplify Hosting |
| API | Lambda + API Gateway |
| DB | DynamoDB |
| 認証 | Cognito |
