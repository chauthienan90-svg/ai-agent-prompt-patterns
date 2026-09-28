# 09 · Bounded self-repair

**Group:** Verification & repair · **Status:** `OBSERVED` · **Seen in:** Cursor, Devin

## Pattern
Cap the number of automatic fix attempts. After the limit, stop and hand the decision to the user.

## Evidence
- Cursor Agent Prompt 2.0: do not loop more than 3 times fixing linter errors on the same file; on the
  third attempt, stop and ask the user (line [562](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L562)).
- Devin: when iterating to get CI to pass, ask the user for help if CI still fails after the third attempt
  (`Devin AI/Prompt.txt`, line [402](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L402)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Without a cap, a model can repeat the same failing fix indefinitely, burning time and tokens and
sometimes making the code worse with each pass.

## How to apply
- Define `max_retries` per problem (per file or per error), not per session.
- On reaching it, switch to a `blocked` state and report: what was tried, what failed, what is needed.
- Forbid guessing: if the fix is not clear, stop earlier.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
If the same error on the same file survives 3 fix attempts, stop.
Report what you tried, what failed, and what you need from the user.
Do not guess at a fix you do not understand.
```

## Anti-pattern
"Keep trying until the tests pass."

**Related:** [08 · Mandatory reflection at decision points](08-think-at-decision-points.md) · [07 · Verify state before acting](07-verify-state-before-acting.md)
