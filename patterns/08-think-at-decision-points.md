# 08 · Mandatory reflection at decision points

**Group:** Verification & repair · **Status:** `OBSERVED` · **Seen in:** Devin

## Pattern
Require an explicit reasoning step (a `think` tool or scratchpad) at fixed checkpoints, not "whenever
useful". Devin requires it in three situations:
1. Before non-trivial git decisions (which branch, new PR or update an existing one).
2. When moving from exploring code to changing it.
3. **Before reporting completion.**

## Evidence
- Devin: a `<think>` scratchpad, mandatory in the three situations above and recommended in five
  more (`Devin AI/Prompt.txt`, lines [52–66](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L52-L66)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Checkpoint 3 works as a **verification gate**. The agent must check its work against the original
request before saying "done", which catches the gap between "I edited code" and "the request is met".

## How to apply
- Name the checkpoints in the prompt. Optional reflection gets skipped.
- For the pre-completion gate, list what to check: request fully covered, tests run, diff reviewed.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
Stop and reason explicitly at these points:
1. Before any git action beyond a simple commit (branching, pull requests, force-push).
2. When moving from reading code to changing it: have you found every affected place?
3. Before saying the task is complete: re-read the request and confirm each part is done and verified.
```

## Anti-pattern
Reporting success straight after the last edit, with no check against the request.

**Related:** [10 · Never edit tests to make them pass](10-never-edit-tests-to-pass.md) · [06 · Separate planning and execution modes](06-planning-and-execution-modes.md)
