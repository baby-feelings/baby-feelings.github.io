# あなたの役割と開発方針

## 役割
あなたは、プロのプロダクトマネージャー兼プログラマーです。  
これから、**Baby Feelings 紹介ホームページの開発**を行います。

## (重要)最初にやること
```bash
# code-review-graph (https://github.com/tirth8205/code-review-graph)を使える状態にする。
code-review-graph build

# グラフの更新(ビルド後、実行し、グラフの更新を監視するため)
code-review-graph watch
```

## プロジェクト概要

| 項目 | 内容 |
|------|------|
| **プロダクト名** | Baby Feelings |
| **概要** | AIで赤ちゃんの泣き声を分析し、感情を推測するアプリの紹介サイト |
| **公開URL** | https://baby-feelings.github.io/ |
| **アプリ本体URL** | https://baby-feelings.web.app/ |
| **ホスティング** | GitHub Pages |
| **静的サイト生成** | Jekyll 3.10.0（github-pages プラグイン） |
| **CSS** | Tailwind CSS（CDN） |
| **Google Analytics** | G-6BTCQ4XQZ3 |

## ディレクトリ構成

```
baby-feelings.github.io/
├── .github/
│   └── dependabot.yml    # 依存関係の自動更新設定（bundler, weekly）
├── _config.yml          # Jekyll 設定ファイル
├── _layouts/
│   └── default.html     # ベースレイアウト
├── _includes/
│   ├── head.html        # <head> タグ（meta, CSS）
│   ├── header.html      # ナビゲーションヘッダー
│   ├── footer.html      # フッター
│   └── smartphone-frame.html  # スマホフレームコンポーネント
├── assets/
│   ├── css/style.css    # カスタムCSS
│   ├── images/          # 画像ファイル
│   └── js/main.js       # JavaScript
├── index.html           # トップページ
├── privacy.html         # プライバシーポリシー
├── terms.html           # 利用規約
├── contact.html         # お問い合わせ（Google Forms 埋め込み）
├── Gemfile              # Ruby 依存関係
├── SKILL.md             # 必要スキル・技術スタック一覧
└── _site/               # ビルド出力（自動生成・Git管理外推奨）
```

## 開発方針（設計原則）
以下の原則に則って設計・実装を行います。

- SOLID 原則
- DRY 原則（Don't Repeat Yourself）
- KISS 原則（Keep It Simple, Stupid）
- YAGNI（You Aren't Gonna Need It）
- 高凝集・低結合（High Cohesion, Low Coupling）
- Separation of Concerns（関心の分離）
- Principle of Least Astonishment（最小驚愕の原則）
- Fail Fast（早めに失敗させる）
- Convention over Configuration（設定より規約）
- Continuous Improvement（継続的改善）

## コーディングルール
- コード内には、処理が分かるようにコメントを記載してください。
- テスト用コードも作成してください。
- HTML は Jekyll テンプレート構文（Liquid）を使用してください。
- CSS は Tailwind CSS のユーティリティクラスを優先的に使用してください。

## CI/CD

現状の構成:

- **依存関係の自動更新**: Dependabot（`.github/dependabot.yml`）が bundler の依存を週次でチェックし、自動でPRを作成
- **デプロイ**: GitHub Pages（legacy build）が `main` ブランチへのプッシュを検知し自動ビルド・公開（Actions ワークフローは未使用）
- **自動テスト・静的解析**: GitHub Actions は未導入。導入する場合は以下のフローを想定

  - Pull Request 作成
  - 自動テスト・静的解析
  - レビュー
  - Merge
  - GitHub Pages への自動デプロイ

## リファクタリング方針
### リファクタリングの基本方針
- 元の機能・仕様を変更してはいけません。
- 外部から見える振る舞い（画面・リンク・レイアウト）は変えないでください。
- 内部構造・設計・可読性・保守性を改善してください。

## 開発手順

```bash
# 1. ブランチを作成（命名規約はコミットメッセージ規約のプレフィックスに準拠）
git checkout -b <prefix>/short-description

# 2. コードを変更・コミット
git add <files>
git commit -m "feat: 機能の説明"

# 3. プッシュして PR を作成
git push -u origin <prefix>/short-description
# → GitHub 上で Pull Request を作成

# 4. レビュー通過後 main へマージ → GitHub Pages に自動デプロイ
```

## ローカル開発

```bash
# Jekyll サーバーを起動
bundle install
bundle exec jekyll serve

# → http://localhost:4000 でプレビュー
```

## コミットメッセージ規約

| プレフィックス | 用途 |
|--------------|------|
| `feat:` | 新機能 |
| `fix:` | バグ修正 |
| `docs:` | ドキュメント |
| `refactor:` | リファクタリング |
| `test:` | テスト追加・修正 |
| `chore:` | ビルド・設定変更 |

---

## セキュリティ情報の活用（必須）

> **重要:** 開発・実装・レビューのあらゆる場面で、以下の手順に従い「サイバー攻撃情報 API」から最新の脅威情報を取得し、開発に活かすこと。

### サイバー攻撃情報 API について

米 CISA の KEV（Known Exploited Vulnerabilities）カタログを毎日収集し、配信する社内 API です。  
実際に悪用が確認された脆弱性のみを収録しているため、**今すぐ対処すべきリスク**を正確に把握できます。

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `https://cyberattack-info-api.onrender.com` |
| **認証** | `X-API-KEY` ヘッダー（値は `.env.production` の `API_KEY` を参照） |
| **ドキュメント** | `https://cyberattack-info-api.onrender.com/docs` |
| **更新頻度** | 毎日 JST 04:00 自動取得 |

### 開発前に必ず実施すること

**1. 直近 30 日の新規脅威を確認する**

```powershell
# PowerShell
$key = $env:CYBERATTACK_API_KEY  # 環境変数から取得
Invoke-RestMethod `
  -Uri "https://cyberattack-info-api.onrender.com/api/vulnerabilities/recent?days=30" `
  -Headers @{ "X-API-KEY" = $key }
```

```bash
# bash / CI
curl -s -H "X-API-KEY: $CYBERATTACK_API_KEY" \
  "https://cyberattack-info-api.onrender.com/api/vulnerabilities/recent?days=30"
```

**2. 使用ライブラリ・製品に関連する脆弱性を検索する**

```powershell
# 例: 本プロジェクトで使用している技術スタックの脆弱性を確認
foreach ($keyword in @("Jekyll", "Ruby", "JavaScript", "nginx")) {
    $result = Invoke-RestMethod `
      -Uri "https://cyberattack-info-api.onrender.com/api/vulnerabilities?search=$keyword&per_page=5" `
      -Headers @{ "X-API-KEY" = $env:CYBERATTACK_API_KEY }
    Write-Host "$keyword : $($result.total) 件"
}
```

```bash
# bash
for keyword in Jekyll Ruby JavaScript nginx; do
  count=$(curl -s -H "X-API-KEY: $CYBERATTACK_API_KEY" \
    "https://cyberattack-info-api.onrender.com/api/vulnerabilities?search=$keyword&per_page=1" \
    | python -c "import sys,json; print(json.load(sys.stdin)['total'])")
  echo "$keyword: $count 件"
done
```

### 取得した情報の開発への活かし方

取得した脆弱性情報を以下の観点で開発に反映してください。

| 観点 | 具体的なアクション |
|------|-----------------|
| **依存ライブラリ** | 脆弱なバージョンを使っていないか確認し、`Gemfile` を更新する |
| **実装パターン** | 脆弱性の種別（XSS・インジェクション等）から、同様のパターンが自分のコードにないか検査する |
| **テスト追加** | 該当する攻撃ベクトルに対するセキュリティテストを追加する |
| **コードレビュー** | PR レビュー時に、直近の CVE と照合してセキュリティ観点のコメントを付ける |
| **ドキュメント** | 対応した脆弱性と対策内容をコミットメッセージ・PR 説明に記載する |

### 他プロジェクトの CLAUDE.md への転記方法

このセクション（「セキュリティ情報の活用（必須）」）をそのまま他プロジェクトの `CLAUDE.md` にコピーすることで、  
どのプロジェクトでも同じセキュリティ情報の活用フローを強制できます。  
API キーは各プロジェクトの環境変数 `CYBERATTACK_API_KEY` にセットしてください。

---

<!-- code-review-graph MCP tools -->
## MCP Tools: code-review-graph

**IMPORTANT: This project has a knowledge graph. ALWAYS use the
code-review-graph MCP tools BEFORE using Grep/Glob/Read to explore
the codebase.** The graph is faster, cheaper (fewer tokens), and gives
you structural context (callers, dependents, test coverage) that file
scanning cannot.

### When to use graph tools FIRST

- **Exploring code**: `semantic_search_nodes_tool` or `query_graph_tool` instead of Grep
- **Understanding impact**: `get_impact_radius_tool` instead of manually tracing imports
- **Code review**: `detect_changes_tool` + `get_review_context_tool` instead of reading entire files
- **Finding relationships**: `query_graph_tool` with callers_of/callees_of/imports_of/tests_for
- **Architecture questions**: `get_architecture_overview_tool` + `list_communities_tool`

Fall back to Grep/Glob/Read **only** when the graph doesn't cover what you need.

### Key Tools

| Tool | Use when |
| ------ | ---------- |
| `detect_changes_tool` | Reviewing code changes — gives risk-scored analysis |
| `get_review_context_tool` | Need source snippets for review — token-efficient |
| `get_impact_radius_tool` | Understanding blast radius of a change |
| `get_affected_flows_tool` | Finding which execution paths are impacted |
| `query_graph_tool` | Tracing callers, callees, imports, tests, dependencies |
| `semantic_search_nodes_tool` | Finding functions/classes by name or keyword |
| `get_architecture_overview_tool` | Understanding high-level codebase structure |
| `refactor_tool` | Planning renames, finding dead code |

### Workflow

1. The graph auto-updates on file changes (via hooks).
2. Use `detect_changes_tool` for code review.
3. Use `get_affected_flows_tool` to understand impact.
4. Use `query_graph_tool` pattern="tests_for" to check coverage.
