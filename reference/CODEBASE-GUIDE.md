# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

Requires Node 24.14+ (or 26.x); `package.json` enforces it. Run `npm ci` for installs.

```bash
npm run doctor            # setup policy check; reports which optional keys are configured
npm run dev               # Vite dev server on http://localhost:4173 (keys optional)
npm run build             # production bundle; also the release gate
npm run preview           # serves the built app plus local /api providers
npm test                  # unit suite (all src/**/*.test.mjs and server/**/*.test.mjs); on Windows it fails with ENAMETOOLONG (1080 file paths = 38k chars > 32k limit), use: node --import=./build/registerVue.js --test "src/**/*.test.mjs" "server/**/*.test.mjs"
npm run test:track        # 3D tracking regression; needs the dev server running
npm run test:perf         # timing budgets (GEV_PERF_BUDGETS=1); not part of npm test
npm run format:check      # Prettier check on the adopted scope; this is the lint gate (no ESLint)
npm run format            # apply formatting
npm run check:boundaries  # import-direction and package-export gates
npm run i18n              # translation catalog completeness
npm run layer-token:check -- --base-ref origin/main   # published share-token ledger
```

Running one test file (the unit runner is a thin wrapper around `node --test`):

```bash
node --import=./build/registerVue.js --test src/geoDistance.test.mjs
node --import=./build/registerVue.js --test --test-name-pattern="haversine" src/geoDistance.test.mjs
```

Use the `--import=./build/registerVue.js` flag for any test that imports Vue single-file components or the UI. Plain `node --test` works for pure modules (`node --test src/geoDistance.test.mjs` also passes).

Feature gates are headless browser scripts in `scripts/qa-*.mjs`. Each needs a running dev server and usually a specific provider or fixture. Read the header of the script before running it; `CONTRIBUTING.md` and `docs/CURRENT-STATE.md` say which gate covers which feature. Only `qa:street-level:fixtures` runs in CI.

Before a PR, the contributor baseline is `npm run build`, `npm test`, and `npm run test:track` (dev server up), plus the gate for the area changed, `format:check`, `check:boundaries` and `i18n` when relevant.

## Architecture

**Shape.** A browser app (Vue 3 + Pinia for UI, CesiumJS for the globe, Vite for builds) backed by a Node server (`server/`) that holds all private API keys and proxies every upstream feed. The browser only ever receives the Google Maps browser key and ephemeral voice tokens. Anything that needs a secret goes through a route under `server/providers/`.

**Composition, not discovery.** `src/main.js` reads browser config and starts `src/standalone/application.js`. That selects four constructors (`createScene`, `createControls`, `createData`, `createTools`) and hands them to the framework-free `createApplication` in `src/application/` (see `docs/APPLICATION.md`). Each constructor returns a component and registers `defer(cleanup)` for what it owns. Teardown runs in the reverse order: tools, controls, data, scene. The app is a single page-scoped instance; the package exports exist so consumers can compose the same pieces, not to run multiple viewers.

**Layers.** Each data layer lives in `src/layers/<family>/` and is split by owner: `source.js` (acquisition), `records.js` / `ingestion.js` (plain record state, portable), and the Cesium renderer/controller. Sources and records must not import Cesium or DOM code; `check:boundaries` enforces this for the listed portable graphs. Layers are instantiated in `src/app/layers/` and `src/app/constructCatalog.js`, registered in the catalog (`src/app/catalog.js`), and their state is controlled through `src/data/lifecycle.js`. Some layers keep older `src/data/<layer>.js` compatibility facades; new code goes in the owning family directory, not the facade.

**Shareable state.** Share links encode layer state using immutable tokens in `LAYER_STATE_REGISTRY` (`src/data/layerState.js`) and the reservation ledger `src/data/layerStateTokenReservations.json`. Never change or reuse a published token. Use `npm run layer-token:next -- <layer-id>` to allocate. Data Library entries have a separate ledger in `src/library/ledger.json`.

**Server providers.** `server/providers/*.js` each export a route factory with its own process-scoped cache. `server/providers/local.js` composes them into the dev/preview middleware in the order `server/standalone/vite.config.js` expects. `server/standalone/key-setup.js` owns Provider Settings and writes the root `.env`; it is development-only. Server-side routes reject request parameters that override upstream endpoints; add endpoints in the factory config, never from the query string.

**UI.** Views are Vue components in `src/ui/views/` and feature components beside their owner (`src/ui/rail/`, `src/ui/weather/`). Owners publish plain view objects to Pinia stores in `src/ui/stores/` and receive user actions through handlers connected to those stores. Portable owners must not import Vue or Pinia. Controls come from `src/ui/kit/`; prefer extending a kit component over writing a one-off. `docs/UI-OWNERSHIP.md` lists which owner handles what, and `docs/VUE-MIGRATION.md` lists the surfaces that still use imperative DOM on purpose.

**Tools and voice.** `src/tools/` defines the tool catalog once (`defineTool`), with query and action kinds. The same catalog is exposed through MCP (`server/mcp/`, `npm run mcp`) and function calling for voice (`src/voice/`). Voice actions are defined in `src/voice/actionSchemas.js` and executed in `src/voice/gevActions.js`; keep the descriptions in `server/providers/openai/tools.js` in sync with them. See `docs/TOOLS.md`.

**Data Library.** Regional and niche sources that do not need JavaScript are JSON manifests under `src/library/` (`docs/DATA-LIBRARY.md`). `npm run library:check` validates them; `npm run library:docs` regenerates their section of `DATA_SOURCES.md`.

**Map sources and cameras.** `src/maps/` holds the basemap registry with factories and fallback policy; `src/layers/cctv/` and `server/providers/cctv/` pair a camera pack's catalog with a server-registered frame proxy. The proxy only fetches URLs it registered, never client-supplied ones. Packs are enabled and sized by `CCTV_*` environment variables (see `.env.example`).

## Conventions that are not obvious from the code

- **Authoritative runtime reference:** `docs/CURRENT-STATE.md` (~8500 lines). A behavior change updates it in the same PR. Read the relevant section before changing a feature.
- **Changelog:** do not edit `CHANGELOG.md`. Add `changelog.d/<pr-number>-<slug>.md` (see `changelog.d/README.md`).
- **Text:** user-visible text goes through `t()` / `tn()` in code and templates, English is the key, and `msg()` marks English that is stored and translated later. Static page markup uses `data-i18n*` attributes. Run `npm run i18n` after adding strings.
- **No Cesium text labels.** New world labels use the world-overlay host.
- **Formatting:** 2-space indent, single quotes, semicolons. Keep mechanical formatting in its own commit.
- **Data sources:** update `DATA_SOURCES.md` with license and attribution, and register credits in `src/data/dataCredits.js`. Do not commit data you cannot redistribute; fetch it at runtime.
- **Allocation probes** (`src/data/focusAllocations.test.mjs`, `src/overlays/worldOverlayAllocation.test.mjs`) only run on Node 24 or 26 and are skipped with a warning elsewhere. `GEV_REQUIRE_ALLOCATION_GATE=1` makes that a failure.
- **Upstream fork.** This checkout is a fork of `bilawalsidhu/gods-eye-view` (remote `upstream`). Its `origin` remote is `Kstor10/gods-eye-view`.
