---
name: add-package
description: npmパッケージの追加・管理。パッケージを追加する際に使用する。dependencies/devDependenciesの適切な振り分け、最新バージョンの確認、ライセンスチェック、pnpm monorepoでのワークスペース指定を行う。
---

# パッケージ追加

pnpm monorepo環境でのパッケージ追加手順。

## 手順

### 1. ライセンス確認

パッケージ追加前に必ずライセンスを確認する。

```bash
npm info <package-name> license
```

**許可するライセンス**: MIT, Apache-2.0, ISC, BSD-2-Clause, BSD-3-Clause, 0BSD, CC0-1.0, Unlicense

上記以外のライセンスの場合はユーザに確認を取る。

### 2. dependencies / devDependencies の判断

| 分類 | 対象 | 例 |
|------|------|-----|
| dependencies | ランタイムで必要 | react, hono, electrodb |
| devDependencies | ビルド・テスト・lint・型定義 | vitest, @types/*, typescript |

迷ったら dependencies に入れる。

### 3. インストール先の判断

| 対象 | コマンド |
|------|---------|
| 特定ワークスペース | `pnpm -F <workspace> add <pkg>` |
| 特定ワークスペース (dev) | `pnpm -F <workspace> add -D <pkg>` |
| ルート (dev only) | `pnpm add -Dw <pkg>` |

- ワークスペース名は package.json の `name` フィールドの値を使う
- ルートには devDependencies のみ追加する（ビルドツール、lint等）
- バージョン指定なしで最新を入れる（pnpm addのデフォルト動作）

### 4. ESLintプラグインをjsPluginで追加する場合

oxlintが対応していないESLintプラグインは、oxlintのjsPlugin機能で導入する。

```bash
pnpm add -Dw eslint-plugin-<name>
```

`.oxlintrc.json` に追加:

```json
{
  "plugins": {
    "jsPlugins": ["eslint-plugin-<name>"]
  }
}
```

### 5. 複数パッケージの一括追加

```bash
pnpm -F frontend add react react-dom next
pnpm -F frontend add -D @types/react @types/react-dom vitest
```
