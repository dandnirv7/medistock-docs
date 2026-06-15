# 02 — Vertical Slice Prompt (main template)

**Use**: Once per slice. Slice 0–10 are defined in `docs/folder_structure.md`.

**Order within a slice**: DB schema first → API endpoint(s) → Flutter feature scaffold. Do all three before moving to the next slice.

---

## Standard Slice (Slices 1–10)

```
Implement Slice <N> — <Name> (see docs/folder_structure.md section "Slice <N>").

Vertical slice order: DB schema first → API endpoint(s) → Flutter feature
scaffold. Do all three before moving to the next slice.

Read carefully first:
- /docs/prd.md section <X.Y> for the feature spec
- /docs/api_contract.md for endpoint contracts (request, response, status,
  error format)
- /docs/database_schema_mvp.md for table/column definitions
- /docs/folder_structure.md section "Slice <N> — <Name>" for the file layout
  to produce

Constraints (from /AGENTS.md):
- No new dependencies beyond what's already in pubspec.yaml / package.json.
- Use the modules-based NestJS layout and feature-based Flutter layout from
  docs/folder_structure.md.
- Use Prisma for DB. Use class-validator DTOs. Use Dio + GetX on mobile.
- Do NOT reference docs/database_schema_full.md (post-MVP).
- Do NOT add tests beyond unit tests on controllers/services.
- Do NOT commit, push, or create branches.

Deliverables for this slice:
1. Prisma migration or schema change (if any).
2. Backend module: controller, service, module, DTOs, basic unit test.
3. Flutter feature folder: bindings, controller, views, models, repository,
   plus route registration in app_pages.dart.
4. Brief summary of what was changed and what to verify manually.

After implementation, list:
- Files created
- Files modified
- New env vars / config needed
- Manual test steps
```

## Slice 0 — Foundation (override)

```
Slice 0 — Foundation deliverables:
1. Prisma schema reflecting docs/database_schema_mvp.md.
2. NestJS bootstrap: global ValidationPipe, global response interceptor
   (matching docs/api_contract.md response format), global exception filter
   (matching error format), CORS for Flutter, prefix /api/v1.
3. Flutter app bootstrap: GetMaterialApp, app theme (per ui/ mockups),
   app_routes.dart, app_pages.dart (empty list OK), initial_binding.dart,
   api_client.dart with Dio + JWT interceptor reading from
   flutter_secure_storage.
4. One health endpoint GET /health returning { status: "ok" } so we can
   verify the wiring.
```
