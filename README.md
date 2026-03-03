# Mission Control Deck

English | [简体中文](README.zh-CN.md)

A real-time operations cockpit for OpenClaw workspaces.

This repository is a clean open-source variant focused on:
- observability for sessions, cost, vitals, jobs, and memory
- profile-aware runtime behavior
- no bundled secrets or user-private data

## Why This Layout Is Different

The project is intentionally organized as a multi-surface workspace:
- `core/` is the runtime control plane
- `apps/command-deck/` is the main dashboard web app
- `apps/mission-room/` is a separate mission-style UI surface
- `lib/` remains as compatibility shims for older commands and imports

## Folder Structure

```text
mission-control-oss/
├── core/                      # Runtime control plane (Node backend)
│   ├── server.js              # Main HTTP server + API
│   ├── config.js              # Config and workspace detection
│   ├── jobs.js                # Jobs API bridge
│   ├── linear-sync.js         # Optional Linear sync
│   └── topic-classifier.js    # Topic intelligence
├── apps/
│   ├── command-deck/          # Primary dashboard (served by core/server.js)
│   │   ├── index.html
│   │   ├── jobs.html
│   │   ├── css/
│   │   ├── js/
│   │   ├── locales/
│   │   ├── partials/
│   │   └── data/
│   └── mission-room/          # Mission-control style standalone surface
│       ├── index.html
│       ├── app.js
│       └── style.css
├── lib/                       # Backward-compatibility wrappers
├── config/                    # Example/local config files
├── scripts/                   # Start/stop/check/release helpers
├── docs/                      # Screenshots + architecture notes
└── tests/                     # Node test suite
```

## Quick Start

```bash
npm ci
npm test
npm start
```

Default URL: `http://localhost:3333`

Equivalent direct run:

```bash
node core/server.js
```

## Legacy Compatibility

The repo keeps `lib/*` wrappers so older automation still works:

```bash
node lib/server.js
```

## Common Commands

```bash
npm start                  # run dashboard server
npm run dev                # watch mode
npm test                   # test suite
npm run lint               # lint core + wrappers + tests
./scripts/start.sh         # managed startup helper
./scripts/stop.sh          # stop helper
```

## Configuration

Key environment variables:

- `PORT` (default `3333`)
- `OPENCLAW_PROFILE`
- `OPENCLAW_WORKSPACE`
- `DASHBOARD_AUTH_MODE` (`none`, `token`, `tailscale`, `cloudflare`, `allowlist`)
- `DASHBOARD_TOKEN` (required when auth mode = `token`)

Example:

```bash
DASHBOARD_AUTH_MODE=tailscale node core/server.js
```

## API Surface

Primary endpoints:

- `GET /api/health`
- `GET /api/state`
- `GET /api/sessions`
- `GET /api/vitals`
- `GET /api/llm-usage`
- `GET /api/cron`
- `GET /api/events` (SSE)

## Security Posture

- local-first runtime (no mandatory external telemetry)
- secret scanning check in `scripts/checks/no-secrets.sh`
- user-data guard in `scripts/checks/no-user-data.sh`
- local/private files excluded via `.gitignore`

## License

MIT — see [LICENSE](LICENSE).
