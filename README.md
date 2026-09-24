# Dashy — Static Live Mirror

A static snapshot of [Lissy93/dashy](https://github.com/Lissy93/dashy) (MIT license, see
[`LICENSE`](./LICENSE)), built for hosting on GitHub Pages. No servers required — just
a static web host.

**Live demo:** https://coattails-droid.github.io/dashy-live/

## Provenance

- **Source:** https://github.com/Lissy93/dashy
- **Upstream commit:** `e51a3268378c227928f1bbdb6146f62ceaa31759` ("Bump version to 4.7.7", 2026-09-22)
- **Build command:** `VITE_APP_CONFIG_PATH=/dashy-live/conf.yml npx vite build --base=/dashy-live/`
- **Build date:** 2026-09-24
- **Config:** the default/sample `user-data/conf.yml` from upstream, baked into this
  build as `conf.yml` (copied to the site root by the build).
- **Fallbacks:** `404.html` is a byte-copy of `index.html`, so GitHub Pages serves the
  app on deep links (the app uses history-mode routing).

This repo contains **only build output** — no build tooling, no `node_modules`. To
rebuild, clone the upstream repo at the commit above and run the build command.

## What works — and what doesn't

Dashy is designed to run with its companion Node.js server (`server.js`), which
exposes status-check, auth, config-management, backup and proxy endpoints. This
static mirror has no server, so everything server-dependent is degraded or inert:

- ❌ **Live status indicators** — the "checking status" widgets call
  `/status-check`, which does not exist statically. (Some status checks made
  directly from the browser may still work.)
- ❌ **Auth / user accounts** — no login, no user management.
- ❌ **In-UI config editor write-back** — the editor can change settings in memory,
  but changes cannot be saved to the server (no `/config-manager` endpoint).
  `conf.yml` here is fixed at build time.
- ❌ **Cloud backup & restore** — requires server-side storage.
- ❌ **Server-side widgets** — system info, ping check, and anything routed through
  the server's CORS proxy.
- ❌ **Service worker offline mode** — the bundled PWA service worker's navigation
  fallback targets the domain root, not this subpath; offline support is unreliable.
- ✅ **Core dashboard** — sections, items, search, themes, icon packs, client-side
  widgets (clocks, RSS feeds fetched client-side, etc.) all work from the baked-in
  `conf.yml`.

## License

Dashy © Lissy93 — MIT License, reproduced in [`LICENSE`](./LICENSE).
