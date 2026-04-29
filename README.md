# github-template

新規 GitHub リポジトリ作成時に共通利用する `.github` 設定一式の Template Repository。

## 使い方

### Web UI から

GitHub のリポジトリ画面右上 **`Use this template`** ボタンから新リポジトリを生成する。

### CLI から

```sh
gh repo create <new-repo-name> --template Ryo-Ohshima/github-template --private
```

## 含まれるファイル

| パス | 用途 |
|---|---|
| `.github/PULL_REQUEST_TEMPLATE.md` | PR テンプレート（What / Why / Refs + コミット規約プレフィックス選択） |
| `.github/ISSUE_TEMPLATE/bug_report.md` | バグ報告テンプレート（日本語） |
| `.github/ISSUE_TEMPLATE/feature_request.md` | 機能要望テンプレート（日本語） |
| `.github/ISSUE_TEMPLATE/config.yml` | blank issue を無効化しテンプレ選択を強制 |
| `.github/CODEOWNERS` | PR レビュー自動割り当て（初期値 `@Ryo-Ohshima`） |
| `.github/release.yml` | リリースノート自動カテゴリ分類（コミット規約整合） |
| `.github/dependabot.yml` | npm + github-actions 週次自動更新 |
| `.github/workflows/claude.yml` | `@claude` メンションで Claude Code を起動 |
| `.github/workflows/stale.yml` | 30 日無活動 Issue/PR を自動クローズ |
| `.github/workflows/ci.yml.example` | Node.js 用 CI 雛形（リネーム+調整して使用） |

## 新リポ生成後にやること

- [ ] **`CODEOWNERS`** のユーザー名を必要に応じて変更
- [ ] **`ci.yml.example`** を `ci.yml` にリネームし、プロジェクトのスクリプト構成に合わせて調整。Node.js 以外のスタックなら丸ごと置き換え
- [ ] **`claude.yml`** を使う場合は Repository Secret に `CLAUDE_CODE_OAUTH_TOKEN` を設定
- [ ] **`dependabot.yml`** で該当しないエコシステムのブロックを削除（例: TS リポなら github-actions のみ残す）
- [ ] **`release.yml`** のラベルが PR ラベル運用と整合しているか確認

## 設計方針

- スタック非依存で汎用的なものに限定（CI 本体は雛形のみ）
- 規約は [`claude-code/rules/git-guideline.md`](https://github.com/Ryo-Ohshima/claude-code) のコミットプレフィックスと整合
- すべてのテンプレ・メッセージは日本語
