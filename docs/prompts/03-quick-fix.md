# 03 — Quick Fix Prompt

**Use**: Small bug, typo, or one-file change. No refactor, no scope expansion.

---

```
Read /AGENTS.md first. Then:

Bug: <describe the symptom — what you see vs. what you expect>.
Repro: <steps to reproduce>.
Relevant docs: <point to the doc that defines correct behavior, e.g.
docs/api_contract.md section 5.1>.

Fix only the bug. Do not refactor surrounding code. Do not add comments
explaining the fix. Do not commit.
```
