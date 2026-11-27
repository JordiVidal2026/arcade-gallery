# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Arcade Vault: a platform to play games online and compete for the highest score (see `README.md`, written in Spanish). The project follows a spec-driven workflow (`/spec` and `/spec-impl` skills, from `Klerith/fernando-skills`, installed with `npx skills@latest add Klerith/fernando-skills`). The codebase is still the fresh Create Next App scaffold (`app/page.tsx`, `app/layout.tsx`); no game or gallery features exist yet.

- No test runner is configured.
## Skills
Usa siempre /fronted-design para diseñar la interfaz de usuario


## Next.js version warning

This uses Next.js 16.4.6 with React 19.3 — newer than typical training data, with breaking changes. `AGENTS.md` requires reading the relevant guide in `node_modules/next/dist/docs/` (`01-app`, `02-pages`, `03-architecture`, `04-community`) before writing Next.js code, and heeding deprecation notices.

## Architecture notes

- App Router only (`app/`). Path alias `@/*` maps to the repo root.
- `next.config.ts` enables `cacheComponents: true` and `partialPrefetching: true`, which change caching/rendering semantics (e.g. dynamic data access must be handled per the Cache Components docs). Check the docs before writing data-fetching code.
- Tailwind CSS v4 is wired through Turbopack, not PostCSS: `next.config.ts` has a `turbopack.rules` entry running `@tailwindcss/turbopack` on `*.css`, and there is no `postcss.config`. Styles are configured in `app/globals.css` via `@import "tailwindcss"` and `@theme inline` (no `tailwind.config`).
- `app/layout.tsx` types props with the globally generated `LayoutProps<"/">` helper (no import needed) and loads Geist fonts via `next/font/google`. Light/dark theme comes from CSS variables in `globals.css` using `prefers-color-scheme`.
