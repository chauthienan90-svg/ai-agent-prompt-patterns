# 01 · Situational tool rules

**Group:** Tool use · **Status:** `OBSERVED` · **Seen in:** Cursor

## Pattern
Write tool-calling rules as a short numbered list where **each rule handles one concrete situation**
(a tool that no longer exists, an edit that failed, uncertainty about file contents), not as general
advice like "use tools carefully".

## Evidence
- Cursor Agent Prompt 2.0: a `<tool_calling>` block with 9 numbered rules, each tied to one situation
  (`Cursor Prompts/Agent Prompt 2.0.txt`, lines [526–537](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L526-L537)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
A model can match a numbered, situation-specific rule to what is happening right now. A vague rule
gives it nothing to match, so it gets ignored exactly when it matters.

## How to apply
- One rule = one trigger + one required behavior.
- Write rules for the failure modes you have actually seen, not ones you imagine.
- Keep the list short. If it grows past ~10, split it by tool.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
Tool rules:
1. If a tool you want to call is not in your tool list, do not call it; use an available one.
2. If an edit fails, re-read the file before trying again.
3. If you are unsure what a file contains, read it; never guess.
4. If a command could change data outside this repository, ask first.
```

## Anti-pattern
> "Be careful when using tools and make sure you use them correctly."

No trigger, no behavior. It cannot be followed or checked.

**Related:** [02 · Tool descriptions say when *not* to use them](02-when-not-to-use.md) · [07 · Verify state before acting](07-verify-state-before-acting.md)
