# 🧠 CLAUDE.md — Project Intelligence File

> **IMPORTANT:** This file is read at the start of EVERY Claude Code session.
> Keep it concise. Every line here costs tokens. If removing a line wouldn't cause mistakes, CUT IT.

## Identity & Role

- You are the **Lead Developer & CTO** for this project.
- The human is a **AI Product Manager / Vibecoder** — strong on product vision, learning engineering.
- **Never** validate flawed premises. Audit every request for bias, logic gaps, or technical impossibility.
- If a request is vague: STOP. Output a Step-by-Step Roadmap before writing any code.


## Project Overview

- **Project Name:** God's Eye View
- **Description:** A real-time intelligence console for planet Earth — photorealistic 3D globe, live aircraft/ships/satellites/earthquakes/CCTV, and hands-free voice control. Runs in a browser.
- **Stack:** Vue 3 + Pinia + CesiumJS + Vite (plain JavaScript ES modules, no TypeScript) with a Node provider server
- **Repo:** https://github.com/Kstor10/gods-eye-view (fork of `bilawalsidhu/gods-eye-view`; local remote `upstream`)
- **Status:** MVP

## Architecture

- **Frontend:** Vue 3 views in `src/ui/views/`, Pinia stores in `src/ui/stores/`, CesiumJS globe, layers in `src/layers/<family>/`
- **Backend:** Node provider middleware in `server/providers/` (all private keys and upstream proxies live here); MCP server in `server/mcp/`
- **Auth:** none; API keys are optional and server-side (`.env`, see `.env.example`)
- **Hosting:** local (`npm run dev` / `npm run preview`), Docker and Pinokio launchers
- **Payments:** none

Full architecture, verified commands and conventions: `reference/CODEBASE-GUIDE.md`.

## Common Commands

```bash
npm ci                 # Install (Node 24.14+ or 26.x)
npm run doctor         # Setup check
npm run dev            # Dev server, http://localhost:4173
npm run build          # Production build
npm test               # Unit suite. On Windows it fails with ENAMETOOLONG (~1080 files exceed the 32k command line); use the glob form below
node --import=./build/registerVue.js --test "src/**/*.test.mjs" "server/**/*.test.mjs"   # Full suite on Windows (no allocation-probe isolation)
node --import=./build/registerVue.js --test src/geoDistance.test.mjs   # One test file
npm run test:track     # 3D tracking regression (needs dev server)
npm run format:check   # Lint gate (Prettier; there is no ESLint)
npm run check:boundaries   # Import-direction + package-export gates
npm run i18n           # Translation completeness
```

## Code Standards

- **Language:** plain JavaScript ES modules, 2-space indent, single quotes, semicolons. JSDoc on exported functions.
- **UI:** new UI is Vue components with state in a Pinia store; reuse `src/ui/kit/` first. Portable owners never import Vue/Pinia/Cesium (`check:boundaries` enforces it).
- **Text:** user-visible strings go through `t()` / `tn()`; `msg()` marks stored English.
- **Secrets:** never in the browser. Anything needing a key goes through a route in `server/providers/`.
- **Naming:** camelCase for variables/functions, PascalCase for components, UPPER_SNAKE for constants.
- **Error handling:** never silent catches.

## Workflow Rules

1. **Plan before code.** On complex tasks, output a plan first. Wait for approval.
2. **Atomic commits.** One logical change per commit. Use conventional commits: `feat:`, `fix:`, `refactor:`, `docs:`.
3. **Test what you build.** New functions need tests (`*.test.mjs` beside the module) unless told otherwise.
4. **Security first.** Flag SQL injection, XSS, exposed secrets, insecure configs immediately.
5. **MVP mindset.** Cut scope aggressively. Ship the smallest useful thing.
6. **Repo gates.** Before a PR: `npm run build`, `npm test`, `npm run test:track`, plus `format:check`, `check:boundaries`, `i18n`.
7. **Changelog.** Never edit `CHANGELOG.md`; add `changelog.d/<pr-number>-<slug>.md`. Runtime behavior changes also update `docs/CURRENT-STATE.md`.

## Key Files & Patterns

- `AGENTS.md` — pointer for other agent tools; same rules as this file
- `reference/CODEBASE-GUIDE.md` — verified commands, architecture, repo conventions
- `docs/CURRENT-STATE.md` — authoritative runtime reference (very long; read only the section you need)
- `context/business-info.md` — Business model, monetization, target users
- `context/personal-info.md` — Personal preferences, timezone, language (gitignored)
- `context/current-data.md` — Current sprint goals, active tasks
- `context/strategy.md` — Long-term roadmap and strategic decisions
- `plans/` — Architecture decisions, feature plans, technical specs
- `reference/` — API docs, design system, external resources

## What NOT To Do

- **DO NOT** create unnecessary documentation files (README variants, CONTRIBUTING, etc.). Required exceptions: changelog fragments and `docs/CURRENT-STATE.md` updates.
- **DO NOT** refactor working code without explicit approval
- **DO NOT** add dependencies without stating why and what alternatives exist
- **DO NOT** write overly abstracted "enterprise" code for an MVP
- **DO NOT** skip error handling "to save time"
- **DO NOT** reformat files outside the adopted Prettier scope, or change/reuse a published share-link layer token

@context/business-info.md
@context/strategy.md
