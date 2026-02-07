# AGENTS.md

このリポジトリでAIエージェントが作業する際のガイドラインを定義する。

## 開発ワークフロー

GitHub Flowに従って開発を行う。詳細は `.claude/skills/dev-workflow/SKILL.md` を参照。

### 基本ルール

- 作業開始前に `main` ブランチの最新変更を `rebase` で取り込む（マージコミットを作らない）
- ブランチ名は `feature/機能名` とする
- コミットメッセージは日本語で1行で簡潔に書く
- コミットメッセージの末尾に `Co-Authored-By: opencode <noreply@opencode.ai>` を追加する
- PR前にコミットを整理する（不要な修正コミットは squash する）
- エージェントはコミットまで行い、push・PR作成は行わない
- PR作成はvibe-kanbanのUIから行う

## スキル一覧

| スキル | 説明 | パス |
| -------- | ---- | ---- |
| dev-workflow | 開発時の作業ワークフロー | `.claude/skills/dev-workflow/` |
| pr-creator | PRテンプレートに沿ったPR作成 | `.claude/skills/pr-creator/` |
| skill-creator | スキルの作成・更新ガイド | `.claude/skills/skill-creator/` |
