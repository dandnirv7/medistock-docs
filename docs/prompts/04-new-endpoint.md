# 04 — New Endpoint Prompt

**Use**: When the task needs an endpoint that is **not yet** in `docs/api_contract.md`.

**Why this exists**: `AGENTS.md` says the API contract is single source of truth. New endpoints = contract must be updated **first**, then code.

---

```
The endpoint <METHOD> <PATH> is needed because <reason>.
It is NOT in docs/api_contract.md.

Per /AGENTS.md, the API contract is single source of truth. Therefore:
1. First, draft the contract (request body, response, status codes, error
   cases) as if it were a new section in docs/api_contract.md.
2. Show me the draft and STOP. Do not implement until I confirm.
3. After my confirmation: update docs/api_contract.md, then implement the
   backend module, then add the mobile repository method that calls it.
```

## Notes

- The "STOP after draft" step is critical. It enforces the **doc-first** rule
  from `AGENTS.md`.
- If the user agrees verbally that the endpoint already exists in the contract
  but is missing in code, switch to template `02-vertical-slice.md` instead
  and skip the contract-draft step.
