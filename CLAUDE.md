# Claude Code 向け指示

このリポジトリは Cloudflare Workers 上で動作する Moltbot (AI エージェント) のカスタマイズ版。

## プロジェクト概要

- Cloudflare Sandbox コンテナで Moltbot を実行
- Cloudflare Access で認証
- R2 で永続化（オプション）
- Telegram/Discord/Slack 連携可能

## 重要な知識

`knowledge/` ディレクトリに以下のドキュメントあり：

- `setup-lessons.md` - セットアップ時の教訓・トラブルシューティング
- `user-roi-framework.md` - ユーザーのタスク評価基準
- `roadmap.md` - 今後の拡張計画
- `model-config.md` - モデル設定のカスタマイズ内容

## カスタマイズ済み内容

1. **デフォルトモデルを Haiku に変更** - コスト最適化のため
2. **ROI ベースのタスク管理** を計画中

## コマンド

```bash
npm run deploy      # ビルド＆デプロイ
npm test           # テスト実行
npm run typecheck  # 型チェック
```

## シークレット管理

```bash
npx wrangler secret put <NAME>
npx wrangler secret delete <NAME>
npx wrangler secret list
```

## 注意点

- ローカル開発 (`npm run dev`) は動作しない（HTML インポートの問題）
- Apple Silicon では Colima + Rosetta 2 が必要
- `CF_ACCESS_TEAM_DOMAIN` はフルドメイン形式で指定

## Linear 連携

ユーザーの Linear:
- チーム: Ebiyy
- プロジェクト: Portfolio Budgeting, ショーケース, qiita-posts

タスク管理の自動化を計画中。詳細は `knowledge/roadmap.md` 参照。
