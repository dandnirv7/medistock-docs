# `docs/` — MediStock Documentation

> Single source of truth for product and technical decisions.
> Read in this order when starting any task.

## File Index

| # | File | Purpose | When to read |
|---|------|---------|--------------|
| 1 | `prd.md` | Product Requirements: features, flows, problem statement, scope of MVP demo | Always — first thing on any task |
| 2 | `api_contract.md` | REST API contracts: base URL, endpoints, request/response schemas, status codes, error format | When creating/modifying endpoints or mobile HTTP layer |
| 3 | `database_schema_mvp.md` | PostgreSQL schema for the MVP: tables, columns, relationships, indexes, seeds | When creating/modifying DB, ORM, entities, or migrations |
| 4 | `folder_structure.md` | Backend (NestJS, modules-based) and mobile (Flutter, feature-based with GetX) folder layouts | When adding new files/modules to know where they go |
| - | `database_schema_full.md` | Full future schema (Batch, PO, Sales, Stock Opname, Audit Trail, etc.) | **Not in scope for MVP.** Reference only when planning the post-MVP phase. |
| 5 | `prompts/` | Reusable prompt templates for coding sessions (repo init, vertical slice, quick fix, new endpoint, validation, handoff) | At session start, and before/after each slice |

## Authority Order

When two documents conflict, follow this order (higher wins):

1. `prd.md` — product truth
2. `api_contract.md` — interface truth
3. `database_schema_mvp.md` — persistence truth
4. `folder_structure.md` — organization truth

> `prompts/` is workflow tooling; it does not participate in authority
> resolution. It references the docs above and is updated independently.

## Conventions for Docs in This Folder

- Do not delete or rename files here without confirmation.
- Keep contents in the original language (mixed ID/EN) — do not re-translate.
- If a code change requires contradicting a doc, update the doc **first**, then the code.
