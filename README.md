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

## Repository Structure

See [docs/REPOSITORY-STRUCTURE.md](docs/REPOSITORY-STRUCTURE.md) for the full tracked tree
and file-by-file breakdown.

The short version:
- `core/` runs the backend and API
- `apps/command-deck/` is the main dashboard UI
- `apps/mission-room/` is the alternate mission-style UI
- `lib/` keeps legacy entrypoints working
- `docs/` holds architecture notes, screenshots, and repo docs
- `scripts/` holds startup, verification, and release helpers
- `tests/` covers the backend and topic logic

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
