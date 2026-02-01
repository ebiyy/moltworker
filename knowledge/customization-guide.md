# Customization Guide

## moltworker vs openclaw

| カスタマイズ | 場所 | フォーク |
|-------------|------|----------|
| スキル追加 | `skills/` | moltworker |
| モデル設定 | `moltbot.json.template` | moltworker |
| ツール追加 | `Dockerfile` | moltworker |
| システムプロンプト変更 | openclaw本体 | **openclaw推奨** |
| AIプロバイダー追加 | openclaw本体 | **openclaw推奨** |
| チャンネル実装変更 | openclaw本体 | **openclaw推奨** |
| メモリ戦略変更 | openclaw本体 | **openclaw推奨** |

## 方針

- **moltworker**: 軽いカスタマイズのみ（skills, config, Dockerfile）
- **openclaw**: 深いカスタマイズが必要な場合

## 理由

moltworkerはOpenClawをnpmパッケージ（`clawdbot`）として使用。
本体を改造するとnpmバージョンアップ時に競合が発生する。

深いカスタマイズが必要になったら：
1. ebiyy/openclawを改造
2. Dockerfileを `npm install -g github:ebiyy/openclaw` に変更
3. ビルド・デプロイ

## フォーク一覧

- [ebiyy/moltworker](https://github.com/ebiyy/moltworker) - Workers層（軽いカスタマイズ）
- [ebiyy/openclaw](https://github.com/ebiyy/openclaw) - 本体（深いカスタマイズ用、現在は追跡のみ）
