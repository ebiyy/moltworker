# モデル設定カスタマイズ

## 変更内容

デフォルトモデルを Opus から **Haiku** に変更済み。

### 変更ファイル

1. `moltbot.json.template`
2. `start-moltbot.sh`

### コスト比較

| モデル | 入力 | 出力 | Opus比 |
|--------|------|------|--------|
| Opus | $15/M tokens | $75/M tokens | 1x |
| Sonnet | $3/M tokens | $15/M tokens | 5x安い |
| **Haiku** | **$0.25/M tokens** | **$1.25/M tokens** | **60x安い** |

### 用途別推奨

- **Haiku**: 定型タスク、インタビュー、通知
- **Sonnet**: 中程度の推論が必要な場合
- **Opus**: 複雑な分析、創造的作業

## 変更箇所詳細

### moltbot.json.template

```json
{
  "agents": {
    "defaults": {
      "workspace": "/root/clawd",
      "model": {
        "primary": "anthropic/claude-haiku-4-5"
      }
    }
  }
}
```

### start-moltbot.sh

Line 262 (AI Gateway 使用時):
```javascript
config.agents.defaults.model.primary = 'anthropic/claude-haiku-4-5-20251001';
```

Line 265 (直接 Anthropic 使用時):
```javascript
config.agents.defaults.model.primary = 'anthropic/claude-haiku-4-5';
```

## モデル切り替え方法

一時的に高性能モデルを使いたい場合、チャットで指示可能：
- 「Sonnet を使って分析して」
- 「Opus で詳細に考えて」

または、`start-moltbot.sh` の該当行を変更して再デプロイ。
