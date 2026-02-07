---
name: dev-workflow
description: 開発時の作業ワークフロー。コードの変更、ブランチ作成、コミットなど開発作業を行う際に使用する。GitHub Flowに従った開発フローを提供する。
---

# 開発ワークフロー

GitHub Flowに従った開発ワークフロー。

## 作業開始前

1. `main` ブランチの最新変更を `rebase` で取り込む（マージコミットを作らない）

```bash
git fetch origin
git rebase origin/main
```

1. 作業用ブランチを作成する（新規ブランチの場合）

```bash
git switch -c feature/<機能名>
```

- ブランチ名は `feature/機能名` とする
- 機能名は英語のケバブケースで記述する（例: `feature/add-user-auth`）

## 作業中

- こまめにコミットする
- コミットメッセージは1行で簡潔に書く
- 不要なファイル（`.env`、ビルド成果物など）をコミットに含めない

## 作業完了後（PR前）

1. `main` の最新変更を `rebase` で取り込む

```bash
git fetch origin
git rebase origin/main
```

1. コミットを整理する（不要な修正コミットは squash する）

```bash
git rebase -i origin/main
```

1. リモートにプッシュする

```bash
git push -u origin HEAD
```

1. PRを作成する（`.claude/skills/pr-creator/SKILL.md` を参照）
