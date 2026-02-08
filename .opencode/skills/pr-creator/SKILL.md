---
name: pr-creator
description: PRテンプレートに沿ったPR作成。PRの作成やPRの説明文を書く際に使用する。`.github/pull_request_template.md` の形式に従ってPRを作成する。
---

# PR作成

`.github/pull_request_template.md` に沿ってPRを作成する。

## 手順

### 1. 事前チェック

ブランチ名が `feature/<機能名>` の命名規則に従っているか確認する。

```bash
git branch --show-current
```

命名規則に従っていない場合は `git branch -m feature/<適切な名前>` でリネームする。

### 2. mainの最新を取り込む

```bash
git fetch origin
git rebase origin/main
```

コンフリクトが発生した場合は自分で解消する。解消後 `git rebase --continue` で続行する。

### 3. コミットログの確認・整理

```bash
git log --oneline origin/main..HEAD
```

以下を確認し、問題があれば `git rebase -i origin/main` で整理する。

- **不要なマージコミットが含まれていないこと** — マージコミットがある場合は rebase で除去する
- **レビュアーが読みやすい粒度であること** — 「fix typo」「wip」等の修正コミットは関連コミットにsquashする
- **各コミットが論理的にまとまった変更であること** — 1コミットに無関係な変更が混在していないか確認する
- **コミットメッセージが1行で簡潔に書かれていること** — 長すぎる場合はrewordで修正する

### 4. リモートにpush

```bash
git push -u origin HEAD
```

### 5. 変更内容を確認する

```bash
git log --oneline origin/main..HEAD
git diff origin/main...HEAD
```

### 6. PRテンプレートに沿ってPRを作成する

1. PRテンプレート（`.github/pull_request_template.md`）を読み込む
1. テンプレートの各セクションを埋める
1. PRタイトルはConventional Commits形式で記述する（例: `feat: ユーザ認証機能の追加`）
1. `gh pr create` でPRを作成する

### 7. PR作成後の確認

PR作成後、コンフリクトが発生していないか確認する。

```bash
gh pr view --json mergeStateStatus --jq '.mergeStateStatus'
```

`DIRTY` の場合はコンフリクトが発生している。`git fetch origin && git rebase origin/main` で解消し、force pushする。

## テンプレートの記述ガイド

### 概要

- このPRで何を変更したか1〜2文で簡潔に記述する

### 変更内容

- 具体的な変更点を箇条書きで記述する
- ファイル単位ではなく、論理的な変更単位でまとめる

### 関連Issue

- 関連するIssueがあれば `closes #xxx` の形式でリンクする

### 確認事項

- チェックリストの各項目を確認し、該当するものにチェックを入れる

### レビュワーへの補足

- 設計判断の背景や、特に確認してほしいポイントがあれば記述する

## PR作成コマンド例

```bash
gh pr create --title "feat: PRタイトル" --body "$(cat <<'EOF'
## 概要

変更の概要をここに記述

## 変更内容

- 変更点1
- 変更点2

## 関連Issue

closes #xxx

## 確認事項

- [x] ローカルで動作確認済み
- [x] 不要なファイルがコミットに含まれていない
- [x] 既存機能への影響を確認済み

## レビュワーへの補足

補足事項があればここに記述
EOF
)"
```
