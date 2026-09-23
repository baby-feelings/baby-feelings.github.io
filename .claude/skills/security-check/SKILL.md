---
name: security-check
description: 開発・実装・レビュー前にCISA KEVカタログの脆弱性情報を確認する手順
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

### 他プロジェクトへの転記方法

このスキルファイルをそのまま他プロジェクトの `.claude/skills/security-check/SKILL.md` にコピーすることで、
どのプロジェクトでも同じセキュリティ情報の活用フローを強制できます。
API キーは各プロジェクトの環境変数 `CYBERATTACK_API_KEY` にセットしてください。
