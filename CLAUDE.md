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

コードベース探索・レビュー・デバッグ・リファクタリングの具体的な手順は
`.claude/skills/` 配下の各スキル（`explore-codebase`, `review-changes`,
`debug-issue`, `refactor-safely`）を参照してください。開発・実装・レビュー前の
セキュリティチェックは `.claude/skills/security-check/SKILL.md`、必要スキル・
技術スタックの一覧は `.claude/skills/project-overview/SKILL.md` を参照してください。

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
├── .claude/skills/       # プロジェクト固有スキル（セキュリティチェック等）
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
