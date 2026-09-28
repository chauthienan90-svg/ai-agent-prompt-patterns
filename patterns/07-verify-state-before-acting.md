# 07 · Verify state before acting

**Group:** Context & planning · **Status:** `OBSERVED` · **Seen in:** Cursor, Devin

## Pattern
Never act on an assumed state:
- If an edit fails, **re-read the file** before retrying. Someone may have changed it.
- Never assume a library is available. **Check the project's dependency files** first.

## Evidence
- Cursor Agent Prompt 2.0: after a failed edit, read the file again because the user may have edited it
  (line [536](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L536)).
- Devin: never assume a library is available, even a well-known one; check that the codebase already
  uses it (`Devin AI/Prompt.txt`, line [21](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L21)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Most agent failures in real repositories come from stale context: an old view of a file, or a
dependency that "should" exist. One cheap read avoids an expensive wrong edit.

## How to apply
- On any failed write: re-read, then retry once.
- Before importing a package: check `package.json`, `requirements.txt`, `go.mod` or the equivalent.
- Treat anything not observed in this session as an assumption.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
Never act on an assumed state.
- After a failed edit, re-read the file before retrying.
- Before using a library, confirm it is listed in the project's dependency file.
- Treat anything you have not observed in this session as an assumption.
```

## Anti-pattern
Retrying the same failed edit with the same stale content.

**Related:** [04 · Search before asking](04-search-before-asking.md) · [09 · Bounded self-repair](09-bounded-self-repair.md)
