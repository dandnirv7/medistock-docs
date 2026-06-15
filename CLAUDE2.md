# CLAUDE.md — MediStock

> Compact mirror for Claude Code / agents that read this file first.
> Primary source: `AGENTS.md` at the repo root. Open that for the full rules.

## Pointers

- Full scope guard → `AGENTS.md`
- Features & product flow → `docs/prd.md`
- API endpoint contracts → `docs/api_contract.md`
- MVP database schema → `docs/database_schema_mvp.md`
- Folder structure & architecture style → `docs/folder_structure.md`
- Mockups & UI assets → `ui/`
- Docs index → `docs/README.md`

## Stack (Quick)

- Mobile: Flutter (Android-first) + GetX, feature-based
- Backend: NestJS (TypeScript), modules-based
- Database: PostgreSQL

## Core Rules

1. Treat `docs/*.md` as the single source of truth.
2. Do not add dependencies / endpoints / tables beyond what is documented there.
3. Refuse work that falls in **Out-of-Scope** (see `AGENTS.md` section 3).
4. Communication: Indonesian. Code & identifiers: English.

> Full details: open `AGENTS.md`.
