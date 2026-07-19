# AGENTS.md

Guidance for AI agents and contributors working in this repo.

## What this is

`whenkit` — a tiny (~90 LOC), **dependency-free** duration/relative-time library published to npm as **ESM + CJS + `.d.ts`**. Public API: `parseDuration`, `formatDuration`, `humanize`, `toUnit`. Keep the surface small and the bundle zero-dep.

## Stack & commands

- **Runtime:** [Bun](https://bun.sh) for all dev tasks (never npm/node).
- **Bundler:** tsdown → `dist/` (esm, cjs, d.ts).
- **Tests:** `bun test`.

```bash
bun install
bun test           # must stay green
bun run build      # tsdown → dist/
```

## Layout

| Path      | Responsibility                                   |
| --------- | ------------------------------------------------ |
| `src/`    | Library source; the only public entry is index.  |
| `tests/`  | `bun test` specs — one per exported function.     |
| `dist/`   | Build output (git-ignored, published to npm).     |

## Conventions

- **Zero runtime dependencies** — non-negotiable. New deps must be dev-only.
- Fully typed; every export ships accurate `.d.ts`. No `any` in public signatures.
- `sideEffects: false` — keep the module tree-shakeable (no top-level side effects).
- `parseDuration` throws on invalid input; preserve that contract.
- Update the README API table whenever a signature changes; add a test first.

## Definition of done

`bun test` green, `bun run build` produces esm+cjs+d.ts, README API table matches code.
