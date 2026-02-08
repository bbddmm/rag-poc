# Backend AGENTS.md

## 技術スタック

| 項目 | 選定 | 備考 |
| -------- | ---- | ---- |
| フレームワーク | Hono | Hono RPCでフロントと型共有 |
| ホスティング | Lambda + API Gateway | Lambdalith構成（1つのLambdaで全ルート処理） |
| API形式 | REST | Hono RPCは通信上はREST |
| ストリーミング | API Gateway SSE | SSE用Lambdaを分けるかは別途検討中 |
| DB | DynamoDB | 無料枠大、運用ゼロ |
| ORM | ElectroDB | DynamoDB専用、型推論強い、Collection機能で擬似リレーション |
| DI | tsyringe | Microsoft製、デコレータベース |
| テスト | Vitest | |

## 設計方針

- **Lambdalith構成**: 1つのLambdaで全ルートを処理する。Honoがルーティングを担当する。コールドスタート頻度が減り、開発体験が良い
- **Hono RPC**: フロントエンドと型を共有する。contractパッケージやts-restは不要。サーバーのルート定義がそのまま型定義になる
- **ElectroDB**: エンティティ定義とキー設計がAPI側に集約される。Collection機能で同じPKのエンティティを1クエリで取得できる（擬似JOIN）
- **SSE**: API GatewayのREST APIレスポンスストリーミングを利用する。SSE用Lambdaを別に分けるかは検討中

## DI方針

- **tsyringe** を使用する（Microsoft製、デコレータベースのDIコンテナ）
- **@hono/tsyringe** でHonoとの連携を行う
- デコレータを使用するため、tsgoではなくtscでコンパイルが必要な場合がある

## テスト方針

- テストフレームワークはVitestを使用する
- **Hono testClient()** を使用して型安全にAPIテストを行う
- `app.request()` または `testClient()` でリクエストを送信する。HTTPサーバーの起動は不要（supertestも不要）
