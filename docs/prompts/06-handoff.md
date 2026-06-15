# 06 — Handoff Prompt

**Use**: At the end of a session, when context will be lost (session end, swap
to another agent, resume later). Captures state so the next session can pick
up cleanly.

---

```
Context handoff for MediStock.

Read first: /AGENTS.md, /docs/README.md.

Current slice: <N> — <Name> (<status: in_progress | done>).
What's done: <list>.
What's in progress: <list>.
What's next: <next slice>.

Specific quirks/decisions made in this session that aren't in the docs:
- <e.g., chose to use dto validation pipe globally at main.ts>
- <e.g., added custom claim to JWT payload: pharmacy_id>

Open questions for the user:
- <list>

Continue from <specific next action>.
```

## Notes

- "Quirks/decisions" is the most valuable section. The docs are the
  spec, but the *decisions* made during a session (workarounds, naming
  choices, library quirks) are not. Capture them.
- "Continue from" should be a single concrete next action, not a list.
