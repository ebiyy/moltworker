# Moltworker セットアップ経験

## 環境情報

- macOS (Apple Silicon)
- Docker: Colima
- Cloudflare Workers Paid プラン

## セットアップで学んだこと

### 1. Docker Buildx が必要

Cloudflare Sandbox は AMD64 イメージが必要。Apple Silicon では buildx + Rosetta 2 が必須。

```bash
# buildx インストール
brew install docker-buildx

# ~/.docker/config.json に追加
{
  "cliPluginsExtraDirs": [
    "/opt/homebrew/lib/docker/cli-plugins"
  ]
}

# Colima を Rosetta 2 有効で再起動
colima stop && colima start --vz-rosetta --arch aarch64 --vm-type vz
```

### 2. CF_ACCESS_TEAM_DOMAIN はフルドメイン

❌ `myteam`
✅ `myteam.cloudflareaccess.com`

types.ts のコメントに記載あり：
```typescript
CF_ACCESS_TEAM_DOMAIN?: string; // e.g., 'myteam.cloudflareaccess.com'
```

### 3. Cloudflare Access ポリシー設定

Workers & Pages で Access を有効にしただけでは不十分。
Zero Trust Dashboard → Access → Applications でポリシー追加が必要：

- Include: Emails → 自分のメールアドレス

### 4. デバイスペアリング必須

初回アクセス時は `/_admin/` でデバイス承認が必要。
"Pairing required" エラーが出たら管理画面で Approve する。

### 5. コールドスタートは遅い

Sandbox コンテナ初回起動は 1-2 分かかる。
"Waiting for gateway..." が表示されたら待つ。

## 必須シークレット

```bash
npx wrangler secret put ANTHROPIC_API_KEY
npx wrangler secret put MOLTBOT_GATEWAY_TOKEN
npx wrangler secret put CF_ACCESS_TEAM_DOMAIN  # フルドメイン！
npx wrangler secret put CF_ACCESS_AUD
```

## オプションシークレット

```bash
# R2 永続化
npx wrangler secret put R2_ACCESS_KEY_ID
npx wrangler secret put R2_SECRET_ACCESS_KEY
npx wrangler secret put CF_ACCOUNT_ID

# Telegram
npx wrangler secret put TELEGRAM_BOT_TOKEN

# Browser Rendering
npx wrangler secret put CDP_SECRET
npx wrangler secret put WORKER_URL
```

## デプロイコマンド

```bash
npm run deploy
```

ローカル開発 (`npm run dev`) は HTML インポートの問題で動作しない。
