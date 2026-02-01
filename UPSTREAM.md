# Upstream Sync

This is a fork of [cloudflare/moltworker](https://github.com/cloudflare/moltworker).

## Remotes

| Remote | Repository | Purpose |
|--------|------------|---------|
| origin | ebiyy/moltworker | Your fork (push here) |
| upstream | cloudflare/moltworker | Original repo (pull from here) |

## Sync Commands

```bash
# Fetch and rebase upstream changes
git fetch upstream
git rebase upstream/main
git push origin main
```

## Related Fork

- [ebiyy/openclaw](https://github.com/ebiyy/openclaw) - OpenClaw core (upstream: openclaw/openclaw)

moltworker uses OpenClaw as an npm dependency (`clawdbot`). To use your own OpenClaw fork, modify the Dockerfile.
