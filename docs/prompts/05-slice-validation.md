# 05 — Slice Validation Prompt

**Use**: After a slice is finished, before moving to the next. Read-only audit.

---

```
Audit Slice <N> — <Name> against docs/folder_structure.md.

Check:
- Backend: controller, service, module, DTOs, basic unit test all exist
  in the right path.
- Mobile: bindings, controller, views, models, repository all exist under
  lib/features/<name>/.
- API request/response match docs/api_contract.md exactly (status codes,
  error format, field names).
- DB queries match docs/database_schema_mvp.md exactly (table names,
  column names, enums).
- No files outside the documented layout for this slice.

Output:
- ✅ what's complete
- ❌ what's missing or wrong (with file:line)
- ⚠️ risks or things to double-check
- DO NOT FIX. Just report.
```

## Notes

- This is a **read-only** audit. The agent must not fix anything, only report.
- Run this before moving to the next slice. Cheap insurance against
  accumulated drift.
- If the output is "all ✅", the next prompt to send is `02-vertical-slice.md`
  for slice N+1.
