# Prompt Library — MediStock

> Reusable prompt templates for coding sessions on this repo.
> Copy-paste, fill in the angle brackets, send to your agent.

All templates follow the **C4 pattern**:
**C**ontext (state) → **C**ontract (link to docs) → **C**onstraints (guard rules) → **C**ommand (action).

## Templates

| # | File | When to use |
|---|------|-------------|
| 1 | [`01-repo-init.md`](01-repo-init.md) | Once, at the start of a new session/repo onboarding. |
| 2 | [`02-vertical-slice.md`](02-vertical-slice.md) | **Main template.** Once per slice (Slices 0–10 from `docs/folder_structure.md`). |
| 3 | [`03-quick-fix.md`](03-quick-fix.md) | Small bug or typo fix. |
| 4 | [`04-new-endpoint.md`](04-new-endpoint.md) | Endpoint that is not yet in `docs/api_contract.md`. |
| 5 | [`05-slice-validation.md`](05-slice-validation.md) | Audit a finished slice before moving on. |
| 6 | [`06-handoff.md`](06-handoff.md) | End-of-session handoff to a future session or another agent. |

## Workflow

```
[1. repo-init] → [2. slice 0] → [2. slice 1] → ... → [2. slice 10]
                       ↓                ↓                ↓
                  [3. quick-fix]    [5. validation]  [6. handoff]
                                          ↓
                                  [4. new-endpoint] (any time, if needed)
```

## Anti-Patterns

These prompt styles will get rejected or steered back to scope. Do not use:

- "Build the whole app" — too broad, agent will exit MVP.
- "Refactor this for cleanliness" with no concrete target.
- "Add 100% test coverage" — out of scope per `AGENTS.md`.
- "Setup production Docker" — out of scope.
- "Add i18n / push notifications" — out of scope.
- "Use the full database schema" — `database_schema_full.md` is post-MVP.

If a feature request matches an anti-pattern, break it down into a slice from `docs/folder_structure.md` first, or refuse and ask the user to update the PRD.
