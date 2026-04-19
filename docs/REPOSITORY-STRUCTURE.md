# Repository Structure

This is the tracked GitHub tree for `mission-control-oss`. It excludes local-only
artifacts such as `.git/`, `node_modules/`, logs, and generated runtime state.

## Top Level

- `.gitignore` - excludes local config, runtime files, and generated artifacts.
- `AGENTS.md` - workspace instructions for agents operating in this repo.
- `CODE_OF_CONDUCT.md` - contributor behavior policy.
- `CONTRIBUTING.md` - contribution and workflow notes.
- `LICENSE` - MIT license.
- `Makefile` - convenience targets for local workflows.
- `Makefile.local.example` - sample local Makefile overrides.
- `README.md` - primary project overview.
- `README.zh-CN.md` - Chinese project overview.
- `SKILL.md` - repo-specific skill entrypoint.
- `package.json` / `package-lock.json` - Node package metadata and lockfile.
- `eslint.config.mjs` - ESLint configuration.

## Full Tree

```text
mission-control-oss/
├── AGENTS.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── Makefile
├── Makefile.local.example
├── README.md
├── README.zh-CN.md
├── SKILL.md
├── .gitignore
├── package.json
├── package-lock.json
├── eslint.config.mjs
├── apps/
│   ├── command-deck/
│   │   ├── favicon.svg
│   │   ├── index.html
│   │   ├── jobs.html
│   │   ├── css/
│   │   │   └── dashboard.css
│   │   ├── data/
│   │   │   ├── AGENTS.md
│   │   │   ├── operators.json.example
│   │   │   └── privacy-settings.json.example
│   │   ├── js/
│   │   │   ├── api.js
│   │   │   ├── app.js
│   │   │   ├── bala-office.js
│   │   │   ├── i18n.js
│   │   │   ├── lib/
│   │   │   │   └── morphdom.min.js
│   │   │   ├── sidebar.js
│   │   │   ├── store.js
│   │   │   └── utils.js
│   │   ├── locales/
│   │   │   ├── en.json
│   │   │   └── zh-CN.json
│   │   └── partials/
│   │       └── sidebar.html
│   └── mission-room/
│       ├── app.js
│       ├── index.html
│       └── style.css
├── config/
│   └── dashboard.example.json
├── core/
│   ├── config.js
│   ├── jobs.js
│   ├── linear-sync.js
│   ├── server.js
│   └── topic-classifier.js
├── docs/
│   ├── README.md
│   ├── REPOSITORY-STRUCTURE.md
│   ├── api/
│   │   └── .gitkeep
│   ├── architecture/
│   │   ├── .gitkeep
│   │   └── OVERVIEW.md
│   ├── guides/
│   │   └── .gitkeep
│   └── screenshots/
│       ├── cerebro-panel.png
│       ├── cost-modal.png
│       ├── costs-panel.png
│       ├── cron-panel.png
│       ├── dashboard-full.png
│       ├── hero.png
│       ├── memory-panel.png
│       ├── operator-modal.png
│       ├── operators-panel.png
│       ├── privacy-modal.png
│       ├── session-detail.png
│       └── sessions-panel.png
├── lib/
│   ├── config.js
│   ├── jobs.js
│   ├── linear-sync.js
│   ├── server.js
│   └── topic-classifier.js
├── scripts/
│   ├── dashboard-loop.sh
│   ├── pre-commit
│   ├── release.sh
│   ├── run-server.sh
│   ├── setup.sh
│   ├── start.sh
│   ├── stop.sh
│   ├── tmux-dashboard.sh
│   ├── verify.sh
│   └── checks/
│       ├── README.md
│       ├── no-secrets.sh
│       ├── no-user-data.sh
│       └── version-sync.sh
└── tests/
    ├── config.test.js
    ├── jobs.test.js
    ├── server.test.js
    └── topic-classifier.test.js
```

## What Each Area Does

- `core/` runs the dashboard backend, API routes, SSE updates, and runtime helpers.
- `apps/command-deck/` is the primary browser UI for the Mission Control deck.
- `apps/mission-room/` is a separate mission-style surface with its own frontend bundle.
- `lib/` keeps old entrypoints working for legacy scripts and imports.
- `config/` stores sample config for local installs.
- `docs/` contains architecture notes, screenshots, and repo documentation.
- `scripts/` holds startup, verification, release, and safety helpers.
- `tests/` contains the Node test suite for config, jobs, server, and topic logic.

## Generated Or Local-Only Files

These are intentionally not tracked in Git:

- `node_modules/`
- runtime logs such as `command-center.log`
- local secret/config overlays that match `.gitignore`

