# Frontend AGENTS.md

## 技術スタック

| 項目 | 選定 | 備考 |
| -------- | ---- | ---- |
| フレームワーク | Next.js (App Router) | `"use client"` 中心のCSR |
| バンドラー | Turbopack | Next.js標準 |
| ホスティング | Amplify Hosting | SSR対応 |
| API通信 | Hono RPC | サーバーコードが型定義を兼ねる |
| サーバー状態管理 | TanStack Query | Hono RPCと併用 |
| クライアント状態管理 | Zustand | サイドバー開閉、モーダル等 |
| UIライブラリ | shadcn/ui | Radix UI + Tailwind CSS。コンポーネントのソースコードを自プロジェクトにコピーする方式 |
| Storybook | 使用 | UIコンポーネント中心 |
| テスト | Vitest | |
| 最適化 | React Compiler | `experimental.reactCompiler: true` で有効化 |

## ディレクトリ構成（Package by Feature）

```text
src/
├── features/
│   ├── auth/
│   │   ├── components/         — LoginForm, SignupForm等
│   │   ├── hooks/              — useAuth, useSignup
│   │   └── pages/              — LoginPage, SignupPage
│   ├── chat/
│   │   ├── components/         — MessageList, MessageInput, RoomCard
│   │   ├── hooks/              — useMessages, useRooms
│   │   └── pages/              — ChatPage, RoomListPage
│   └── settings/
│       ├── components/         — ProfileForm
│       ├── hooks/              — useUserSettings
│       └── pages/              — SettingsPage
├── components/
│   └── ui/                     — shadcn/uiコンポーネント (Button, Dialog等)
├── lib/                        — 共通ユーティリティ、APIクライアント
└── app/                        — Next.js App Router (ルーティングのみ、薄く保つ)
```

## 設計方針

- App Routerは `"use client"` 中心で使用する。サーバーコンポーネントは必要最小限
- `app/` ディレクトリはルーティング専用で薄く保つ。ビジネスロジックやUIは `features/` に配置する
- 機能単位（feature）でコンポーネント・hooks・ページをまとめる（Package by Feature）
- shadcn/uiのコンポーネントは `components/ui/` に配置する（npmパッケージではなくソースコードをコピーする方式）
- Hono RPCでバックエンドと型を共有する（ts-restやcontractパッケージは不要）

## 画面構成

### 認証系（自前実装）

| 画面 | パス |
| -------- | ---- |
| ログイン | `/login` |
| サインアップ | `/signup` |
| メール確認 | `/verify` |
| パスワードリセット | `/reset-password` |

### メイン系

| 画面 | パス |
| -------- | ---- |
| チャットルーム一覧 | `/` |
| チャット | `/chats/:chatId` |

### 設定系

| 画面 | パス |
| -------- | ---- |
| ユーザ設定 | `/settings` |

## Storybook方針

- UIコンポーネント（`components/ui/`、`features/*/components/`）を中心にStoriesを作成する
- ページコンポーネント（`features/*/pages/`）やモックが複雑になるものは除外する

## テスト方針

- テストフレームワークはVitestを使用する
- コンポーネントのユニットテスト・hookのテストを中心に記述する
