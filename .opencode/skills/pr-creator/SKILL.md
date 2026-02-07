---
name: pr-creator
description: PRテンプレートに沿ったPR作成。PRの作成やPRの説明文を書く際に使用する。`.github/pull_request_template.md` の形式に従ってPRを作成する。
---

# PR作成

`.github/pull_request_template.md` に沿ってPRを作成する。

## 手順

1. 変更内容を確認する

```bash
git log --oneline origin/main..HEAD
git diff origin/main...HEAD
```

1. PRテンプレート（`.github/pull_request_template.md`）を読み込む
1. テンプレートの各セクションを埋める
1. `gh pr create` でPRを作成する

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
gh pr create --title "PRタイトル" --body "$(cat <<'EOF'
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
