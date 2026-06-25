# Baby Feelings 紹介ホームページ — スキルマップ

本プロジェクトの開発に必要な技術スキルとナレッジをまとめます。

## 必須スキル

### 1. フロントエンド

| スキル | レベル | 用途 |
|--------|--------|------|
| HTML5 | 基本 | ページ構造・セマンティックマークアップ |
| CSS3 / Tailwind CSS | 基本〜中級 | レスポンシブデザイン・ユーティリティクラス設計 |
| JavaScript (ES6+) | 基本 | モバイルメニュー・スクロールアニメーション・インタラクション |

### 2. 静的サイト生成

| スキル | レベル | 用途 |
|--------|--------|------|
| Jekyll | 基本〜中級 | サイトビルド・設定管理 |
| Liquid テンプレート | 基本 | レイアウト・パーシャルの記述 |
| YAML | 基本 | `_config.yml` の設定・Front Matter |

### 3. インフラ・デプロイ

| スキル | レベル | 用途 |
|--------|--------|------|
| GitHub Pages | 基本 | ホスティング・自動デプロイ |
| Git / GitHub | 基本〜中級 | バージョン管理・ブランチ運用・PR レビュー |
| GitHub Actions | 基本 | CI/CD パイプライン |

### 4. SEO・アクセス解析

| スキル | レベル | 用途 |
|--------|--------|------|
| Google Analytics (GA4) | 基本 | アクセス解析・コンバージョン計測 |
| SEO 基礎 | 基本 | メタタグ・OGP・サイトマップ（jekyll-sitemap） |
| Google Search Console | 基本 | 検索パフォーマンス・インデックス管理 |

## 推奨スキル

| スキル | 用途 |
|--------|------|
| Ruby (Bundler) | Gemfile 管理・Jekyll プラグイン開発 |
| PWA (Web App Manifest) | モバイル対応・ホーム画面追加 |
| アクセシビリティ (WCAG) | alt 属性・コントラスト比・キーボード操作 |
| パフォーマンス最適化 | 画像圧縮・Lazy Loading・Core Web Vitals |

## 外部サービス連携

| サービス | 用途 | 設定場所 |
|----------|------|----------|
| Google Forms | お問い合わせフォーム | `contact.html` 内の iframe |
| Google Analytics (GA4) | アクセス解析 | `_config.yml` の `google_analytics` |
| Firebase Hosting | アプリ本体ホスティング | `https://baby-feelings.web.app/` |
| CISA KEV API | セキュリティ脆弱性情報 | `CLAUDE.md` 参照 |

## 開発環境

| ツール | バージョン | 備考 |
|--------|-----------|------|
| Ruby | Gemfile に準拠 | Jekyll 実行環境 |
| Jekyll | 3.9.5 | `github-pages` gem に含まれる |
| Bundler | 最新推奨 | `bundle install` で依存解決 |
| Git | 最新推奨 | バージョン管理 |
| Node.js | 不要 | Tailwind CSS は CDN 利用のため不要 |
