# Agent Guidelines

MediStock — Flutter Android pharmacy inventory MVP demo with a NestJS backend and PostgreSQL.

Detailed project docs live in [docs/](docs/) and [docs/README.md](docs/README.md) — reference them via links rather than duplicating here.

## Tech Stack

- **Flutter (Dart)** — Mobile app, Android-first target. State management via GetX.
- **Dio** — HTTP client for the Flutter app.
- **flutter_secure_storage** — Token and credential storage on device.
- **NestJS 11 (TypeScript)** — Backend framework, modules-based, vertical-slice per feature.
- **Prisma** — ORM for PostgreSQL (planned per `docs/folder_structure.md`).
- **Passport + JWT** — Authentication (per NestJS starter deps).
- **PostgreSQL** — Primary database.
- **pnpm** — Backend package manager.
- **Jest** — Backend unit and e2e tests.

## Common Commands

### Backend (`medistock-api/`)

- `pnpm install` — install dependencies
- `pnpm run start:dev` — run NestJS in watch mode
- `pnpm run build` — production build
- `pnpm run lint` — ESLint with auto-fix
- `pnpm run format` — Prettier write
- `pnpm run test` — Jest unit tests
- `pnpm run test:e2e` — Jest e2e tests

### Mobile (`medistock_mobile/`)

- `flutter pub get` — fetch Dart packages
- `flutter run` — run app on connected device/emulator
- `flutter test` — run widget and unit tests
- `flutter analyze` — static analysis
- `flutter build apk` — build Android APK

## Pre-Commit Verification

Before every commit, verify code quality on changed files:

```sh
# Backend
cd medistock-api
pnpm run lint
pnpm run test

# Mobile
cd ../medistock_mobile
flutter analyze
flutter test
```

Never commit code that fails these checks.

## Source-of-Truth Docs

The repo is **spec-driven**. Before starting work, read the relevant doc(s) in `docs/`:

- [PRD](docs/prd.md) — features, flows, MVP scope.
- [API Contract](docs/api_contract.md) — REST endpoints, request/response, error format.
- [DB Schema (MVP)](docs/database_schema_mvp.md) — tables and columns for the MVP.
- [DB Schema (Full)](docs/database_schema_full.md) — post-MVP reference only. **Not in scope for MVP.**
- [Folder Structure](docs/folder_structure.md) — backend and mobile layout.
- [UI Mockups](ui/) — visual references for screens.

### Authority order when docs conflict

1. `prd.md` — product truth
2. `api_contract.md` — interface truth
3. `database_schema_mvp.md` — persistence truth
4. `folder_structure.md` — organization truth

### Import size warning

`prd.md` (~1170 lines) and `folder_structure.md` (~1160 lines) are intentionally **not** `@import`-ed to avoid bloating the context window on every conversation. Read them on demand.

## Code Style & Common Patterns

- **Backend**: follow NestJS modules-based layout from `docs/folder_structure.md` (one module per domain feature: `auth/`, `users/`, `categories/`, `suppliers/`, `medicines/`, `stock-movements/`, `dashboard/`). Use `class-validator` DTOs at every endpoint. Use Prisma for DB access.
- **Mobile**: follow Flutter feature-based layout from `docs/folder_structure.md` (`lib/features/<feature>/{controllers,views,bindings,models}/`). Use GetX for state, routing, and DI. Use Dio with a shared `ApiClient` under `lib/core/network/`.
- **Errors**: API error response format must match `docs/api_contract.md`.
- **Lint/Format**: rely on the default tool configs already in each sub-project — do not invent new style rules.

## File Organization

```
MediStock/
├── AGENTS.md              # this file
├── CLAUDE.md              # Claude Code pointer to AGENTS.md
├── docs/                  # single source of truth (PRD, API, schema, structure)
├── ui/                    # UI mockups (PNG)
├── medistock_mobile/      # Flutter app
│   ├── lib/
│   │   ├── app/           # routes, bindings, root widget
│   │   ├── core/          # constants, network, storage, theme, utils, widgets
│   │   ├── data/          # models, repositories
│   │   └── features/      # one folder per feature (controllers, views, bindings, models)
│   └── test/
└── medistock-api/         # NestJS backend
    ├── prisma/            # schema.prisma, seed.ts
    ├── src/
    │   ├── main.ts
    │   ├── app.module.ts
    │   ├── common/        # decorators, filters, guards, interceptors, pipes, dto
    │   ├── config/        # app.config, jwt.config
    │   ├── database/      # prisma.module, prisma.service
    │   └── <feature>/     # one module per domain (auth, users, categories, …)
    └── test/
```

## Workflow

- **Scope**: MVP demo per `docs/prd.md`. Refuse work that falls outside MVP unless the user updates the PRD first.
- **Vertical slice**: implement one feature end-to-end (DB → API → mobile screen) before moving to the next.
- **Doc-first**: if a code change requires contradicting a doc, update the doc first, then the code.
- **No new deps**: do not add dependencies, libraries, or services beyond what is listed in `docs/`.
- **No commits without explicit user request.**

## Gotchas

- `lib/main.dart` and `lib/test/widget_test.dart` are still Flutter default boilerplate — do not use the counter app as a reference; follow `docs/folder_structure.md` instead.
- `src/app.module.ts` is bare NestJS starter — feature modules do not exist yet.
- `medistock-mobile/README.md` and `medistock-api/README.md` are template boilerplate; replace with project-specific docs only when a sub-project is actually being developed.
- `database_schema_full.md` is **not** MVP scope — referencing it as authority is a scope violation.
- Platform folders (`ios/`, `macos/`, `windows/`, `linux/`, `web/` in the Flutter project) are default `flutter create` scaffolding — leave them as-is unless explicitly asked.

## Further Documentation

- [Docs index](docs/README.md)
- [PRD](docs/prd.md)
- [API Contract](docs/api_contract.md)
- [DB Schema (MVP)](docs/database_schema_mvp.md)
- [Folder Structure](docs/folder_structure.md)
- [Prompt library](docs/prompts/README.md) — reusable session templates (repo init, vertical slice, quick fix, new endpoint, validation, handoff)
- [UI mockups](ui/)
