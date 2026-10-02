# Baby Feelings 紹介ホームページ

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](LICENSE)

AIで赤ちゃんの泣き声を分析し、感情を推測するアプリ「Baby Feelings」の紹介サイトです。

## 公開URL

| サイト | URL |
|--------|-----|
| 紹介ホームページ | https://baby-feelings.github.io/ |
| アプリ本体 | https://baby-feelings.web.app/ |

## 技術スタック

| 技術 | 用途 |
|------|------|
| Jekyll 3.10.0 | 静的サイト生成 |
| GitHub Pages | ホスティング・自動デプロイ |
| Tailwind CSS (CDN) | スタイリング |
| Liquid | テンプレートエンジン |
| Google Analytics | アクセス解析 |
| Google Forms | お問い合わせフォーム |
| jekyll-sitemap | sitemap.xml の自動生成 |
| Dependabot | 依存関係の自動更新（週次） |

## ディレクトリ構成

```
baby-feelings.github.io/
├── .github/dependabot.yml   # 依存関係の自動更新設定
├── .semgrepignore           # Semgrep 誤検知の除外設定
├── _config.yml              # Jekyll 設定
├── _layouts/default.html    # ベースレイアウト
├── _includes/               # 共通パーツ（header, footer, head 等）
├── assets/
│   ├── css/style.css        # カスタムCSS
│   ├── images/              # 画像ファイル
│   └── js/main.js           # JavaScript
├── index.html               # トップページ
├── privacy.html             # プライバシーポリシー
├── terms.html               # 利用規約
├── contact.html             # お問い合わせ
├── site.webmanifest         # PWA マニフェスト（favicon・アイコン類とセット）
├── Gemfile / Gemfile.lock   # Ruby 依存関係
├── CLAUDE.md                # AI開発ガイドライン
└── .claude/skills/          # プロジェクト固有スキル（スキルマップ・セキュリティチェック等）
```

## ローカル開発

```bash
# 依存関係をインストール
bundle install

# 開発サーバーを起動
bundle exec jekyll serve

# → http://localhost:4000 でプレビュー
```

## ページ構成

- **トップページ** (`index.html`) — ヒーロー、課題提起、製品紹介、特徴、使い方、ユーザーの声、CTA
- **プライバシーポリシー** (`privacy.html`)
- **利用規約** (`terms.html`)
- **お問い合わせ** (`contact.html`) — Google Forms 埋め込み

## 開発フロー

1. `<prefix>/short-description` ブランチを作成（プレフィックスはコミットメッセージ規約に準拠）
2. 変更をコミット（[コミットメッセージ規約](CLAUDE.md#コミットメッセージ規約)に従う）
3. Pull Request を作成
4. レビュー・CI 通過後に `main` へマージ
5. GitHub Pages に自動デプロイ

## ライセンス

[GNU Affero General Public License v3.0（AGPL-3.0）](LICENSE)

AGPL-3.0 は、コードを改変してネットワーク経由で提供する場合（サーバー型サービスとしての利用を含む）も、改変後のソースコードを利用者に公開する義務を課す強めのコピーレフトライセンスです。無断でコードをコピーして非公開の競合サービスとして運営することを防ぐ目的で選択しています。個人利用・学習目的の閲覧・フォークは自由ですが、本コードを基にしたサービスを公開する場合はソースコードの公開が必要です。商用利用や別ライセンスでの利用を希望する場合は個別にご相談ください。
