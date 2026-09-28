# 10 · Never edit tests to make them pass

**Group:** Verification & repair · **Status:** `OBSERVED` · **Seen in:** Devin

## Pattern
When tests fail, assume the bug is in the code under test, not in the test. Change a test only when
the task explicitly asks for it.

## Evidence
- Devin: never modify tests while struggling to pass them unless the task asks for it; first consider
  that the root cause is in the code being tested (`Devin AI/Prompt.txt`, line [14](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L14)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Tests are the success criteria. An agent allowed to edit them can always "pass" by weakening them,
and the report looks green while the bug remains.

## How to apply
- State the rule in the prompt and in the verification checklist.
- Generalize it: **never change the acceptance criteria to meet them.** This covers linters, type
  checks and CI configuration too.
- If a test really is wrong, the agent reports that and asks rather than editing it silently.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
When a test fails, assume the bug is in the code under test.
Do not modify, skip or weaken tests, linters or CI checks to make them pass
unless the task explicitly asks for it. If a test looks wrong, say so and ask.
```

## Anti-pattern
Deleting an assertion, adding `skip`, or loosening a threshold to turn CI green.

**Related:** [08 · Mandatory reflection at decision points](08-think-at-decision-points.md) · [11 · Accuracy over agreement](11-accuracy-over-agreement.md)
