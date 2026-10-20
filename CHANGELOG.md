# Changelog

## 0.1.0-beta
First public-ready beta.

- Hosts manager with a marked block, backups, read-back check and rollback.
- Loopback proxy with mirror origin, offline mode, detail-level cap, live statistics.
- Resumable, verified chunk mirror with scope (campaign / everything / custom packages), detail level (standard, high, ultra), bandwidth cap, daily quota,
  waiting out lost connections, `plan`, `verify --all`, `prune`.
- Control window: session start/stop, Texture pack tab, cache tools, doctor, per-launch session reports, logs.
- Polite client behaviour: User-Agent naming the tool, back-off on HTTP 429/503 (honours Retry-After), 4 connections and 50 requests/s by default, edge address
  from public DNS.
- Bulk-download notice that must be accepted once per version (GUI dialog, or `--accept-notice` on the command line).
- 89 tests that run without the game.
