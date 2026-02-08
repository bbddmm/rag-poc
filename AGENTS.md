# AGENTS.md

このリポジトリでAIエージェントが作業する際のガイドラインを定義する。

## 開発ワークフロー

GitHub Flowに従って開発を行う。詳細は各スキルを参照。

## スキル一覧

| スキル        | 説明                                       |
| ------------- | ------------------------------------------ |
| dev-workflow  | 開発時の作業ワークフロー                   |
| pr-creator    | PRテンプレートに沿ったPR作成               |
| code-review   | コードレビュー（共通観点 + レイヤー固有）  |
| add-package   | npmパッケージの追加・管理                   |
| skill-creator | スキルの作成・更新ガイド                   |

## プロジェクト概要

Amplify + Bedrockを使用した簡易チャットアプリ。必要に応じてWeb検索して応答する。

## 全体構成

- **monorepo**: Turborepo + pnpm
- **認証**: Cognito（自前実装、Hosted UI不使用）
- **AI**: Bedrock（Web検索もBedrockの機能を使用）

## ディレクトリ構成

```text
apps/
  frontend/     — Next.js
  backend/      — Hono (Lambdalith構成)
  infra/        — SST
packages/
  models/       — ElectroDB エンティティ定義等の共有コード
```

各アプリの詳細は `apps/*/AGENTS.md` を参照。

## 技術スタック一覧

| レイヤー       | 主な技術                                                   |
| -------------- | ---------------------------------------------------------- |
| フロントエンド | Next.js (App Router), shadcn/ui, TanStack Query, Zustand   |
| バックエンド   | Hono (Lambdalith), ElectroDB, tsyringe                     |
| インフラ       | SST v3 (Ion), DynamoDB, Cognito, Lambda + API Gateway      |
| API通信        | Hono RPC（型共有、通信上はREST）                           |

## 開発ツール

| 項目                 | 選定                                                           |
| -------------------- | -------------------------------------------------------------- |
| パッケージマネージャ | pnpm                                                           |
| ランタイム管理       | mise, aqua                                                     |
| Linter               | oxlint                                                         |
| Formatter            | oxfmt                                                          |
| 型チェック           | tsgo（デコレータ非対応のため、必要に応じてtscにフォールバック） |
| Git hooks            | lefthook                                                       |
| CI/CD                | GitHub Actions                                                 |
