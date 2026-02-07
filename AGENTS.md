# AGENTS.md

このリポジトリでAIエージェントが作業する際のガイドラインを定義する。

## 開発ワークフロー

GitHub Flowに従って開発を行う。

### 基本ルール

- 作業開始前に `main` ブランチの最新変更を `rebase` で取り込む（マージコミットを作らない）
- ブランチ名は `feature/機能名` とする
- コミットメッセージは日本語で1行で簡潔に書く
- コミットメッセージは[Conventional Commits](https://www.conventionalcommits.org/)の形式に従う
  - 形式: `<type>: <description>`
  - 主なtype: `feat`(新機能), `fix`(バグ修正), `docs`(ドキュメント), `refactor`(リファクタリング), `test`(テスト), `chore`(雑務)
- PR前にコミットを整理する（不要な修正コミットは squash する）
- PRは `.github/pull_request_template.md` に沿って作成する
- 作業が完了したらPR作成まで行う

## スキル一覧

| スキル | 説明 |
| -------- | ---- |
| dev-workflow | 開発時の作業ワークフロー |
| pr-creator | PRテンプレートに沿ったPR作成 |
| skill-creator | スキルの作成・更新ガイド |
