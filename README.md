# Baby Feelings 紹介ホームページ

AIで赤ちゃんの泣き声を分析し、感情を推測するアプリ「Baby Feelings」の紹介サイトです。

## 公開URL

| サイト | URL |
|--------|-----|
| 紹介ホームページ | https://baby-feelings.github.io/ |
| アプリ本体 | https://baby-feelings.web.app/ |

## 技術スタック

| 技術 | 用途 |
|------|------|
| Jekyll 3.9.5 | 静的サイト生成 |
| GitHub Pages | ホスティング・自動デプロイ |
| Tailwind CSS (CDN) | スタイリング |
| Liquid | テンプレートエンジン |
| Google Analytics | アクセス解析 |
| Google Forms | お問い合わせフォーム |

## ディレクトリ構成

```
baby-feelings.github.io/
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
├── Gemfile                  # Ruby 依存関係
└── CLAUDE.md                # AI開発ガイドライン
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

1. `feature/*` ブランチを作成
2. 変更をコミット（[コミットメッセージ規約](CLAUDE.md#コミットメッセージ規約)に従う）
3. Pull Request を作成
4. レビュー・CI 通過後に `main` へマージ
5. GitHub Pages に自動デプロイ

## ライセンス

All Rights Reserved. &copy; Baby Feelings.
