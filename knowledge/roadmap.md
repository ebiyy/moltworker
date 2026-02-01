# Moltworker 拡張ロードマップ

## 現在のステータス

- [x] Cloudflare Workers Paid プラン
- [x] 基本デプロイ完了
- [x] Cloudflare Access 認証設定
- [x] デバイスペアリング完了
- [x] Haiku モデルに変更（コスト最適化）
- [ ] R2 永続ストレージ（後回し）

## 次のステップ

### Phase 1: Telegram 連携

1. **BotFather で Bot 作成**
   - https://t.me/botfather
   - `/newbot` でボット作成
   - Bot Token を取得

2. **Moltworker に設定**
   ```bash
   npx wrangler secret put TELEGRAM_BOT_TOKEN
   npm run deploy
   ```

3. **ペアリング**
   - Bot に DM を送る
   - `/_admin/` でデバイス承認

### Phase 2: Linear タスク管理 Skill 作成

1. **Linear API トークン取得**
   - https://linear.app/settings/api
   - Personal API Key を作成

2. **Skill ファイル作成**
   - `/root/clawd/skills/linear-task-manager.md`
   - インタビューフローを定義
   - ROI ラベル自動付与ロジック

3. **Skill 内容**
   ```markdown
   # Linear Task Manager

   ## トリガー
   「タスク追加」「新しいタスク」等のキーワード

   ## インタビューフロー
   1. タスク内容を聞く
   2. 納期を確認
   3. 学習要素を確認
   4. 転用可能性を確認
   5. 見積もり時間を確認

   ## 自動ラベル付け
   - 回答に基づいてラベルを決定
   - Linear API でタスク作成
   ```

### Phase 3: 定期ブリーフィング

1. **cron 設定追加** (wrangler.jsonc)
   ```json
   "triggers": {
     "crons": ["0 8 * * *"]  // 毎朝8時
   }
   ```

2. **ブリーフィング内容**
   - 今日の期限タスク
   - 今週の予定
   - 未完了タスク数

### Phase 4: R2 永続化（必要に応じて）

会話履歴・ペアリング情報を永続化したくなったら設定。

```bash
npx wrangler secret put R2_ACCESS_KEY_ID
npx wrangler secret put R2_SECRET_ACCESS_KEY
npx wrangler secret put CF_ACCOUNT_ID
npm run deploy
```

## 使い分け方針

| 用途 | ツール | モデル |
|------|--------|--------|
| 開発・創造的作業 | Claude Code | Opus/Sonnet (Max) |
| タスク追加・管理 | Moltworker + Telegram | Haiku |
| 定期レポート | Moltworker cron | Haiku |

## 参考リンク

- [Moltworker README](../README.md)
- [Moltbot 公式](https://molt.bot/)
- [Linear API Docs](https://developers.linear.app/)
