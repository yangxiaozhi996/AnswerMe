# Repository Guidelines

## Project Structure & Module Organization
`koishi.yml` is the canonical map of server, console, adapter, and development plugins—keep group identifiers stable when editing. Runtime state stays under `data/` (`koishi.db`, `logs/`, `telemetry.json`) and translations under `locales/`. Plugin source lives in `external/*/src` or `packages/*/src`, created via `yarn new`/`yarn setup` and wired through `tsconfig.json` path aliases. Deployment scripts sit in `docker/` and `.github/workflows/`; update them whenever build paths or entry commands change.

## Build, Test, and Development Commands
- `yarn setup` – hydrate Koishi upstream dependencies and populate `external/`.
- `yarn dev` – start Koishi with HMR for iterative plugin coding.
- `yarn build` – run the Yakumo pipeline (`tsc`, `esbuild`, client bundling) for release artifacts.
- `yarn start` – boot the compiled bot for staging or production verification.
- `yarn clean | yarn dep | yarn bump` – reset caches, upgrade dependencies, and create version bumps before publishing.
- `yarn new <name>` – scaffold a `koishi-plugin-<name>` package with the expected boilerplate.

## Coding Style & Naming Conventions
`.editorconfig` enforces UTF-8, LF endings, and two-space indentation for TypeScript, YAML, and shell files. Stick to ES modules, async/await, camelCase functions, PascalCase classes, and kebab-case package names (`koishi-plugin-answer-me`). Align locale keys with command ids (`locales/en.yml` → `answer.me.description`) and guard optional plugin blocks in `koishi.yml` with the same `$if env.KOISHI_AGENT` checks used elsewhere.

## Testing Guidelines
There is no Jest/Vitest harness yet, so validate behavior through `yarn dev`, Koishi Console interactions, and adapter smoke tests while tailing `data/logs/*.log`. For scripted coverage, co-locate minimal integration specs (`external/foo/src/foo.spec.ts`) that spin up a mock `Context`; gate them with `NODE_ENV=test` and avoid shipping them in production bundles. Document manual scenarios (commands exercised, adapters touched, expected replies) inside every PR until broader automation lands.

## Commit & Pull Request Guidelines
Use Conventional Commit prefixes (`feat:`, `fix:`, `chore:`) so `yakumo version` can infer releases. PRs should enumerate the plugins or config sections touched, summarize schema/locale updates, reference related issues, and attach console screenshots or log excerpts for UI-facing work. Always run `yarn build` (plus any adapter-specific checks) before requesting review, and call out Docker or workflow updates explicitly.

## Security & Configuration Tips
Store secrets in `.env` and reference them from `koishi.yml`; never hardcode adapter tokens. Keep sensitive artifacts inside `data/`, which remains gitignored. When editing Docker assets, specify whether you tested `docker/Dockerfile` or `Dockerfile.lite`, and document required `KOISHI_AGENT` values so downstream agents load only the intended plugins.
