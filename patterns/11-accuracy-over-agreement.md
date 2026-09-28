# 11 · Accuracy over agreement

**Group:** Behavior · **Status:** `OBSERVED` · **Seen in:** Claude Code

## Pattern
Put technical accuracy ahead of agreeing with the user. When unsure, investigate first, then answer.
No praise or validation for its own sake.

## Evidence
- Claude Code 2.0: a "Professional objectivity" section that ranks technical accuracy and truthfulness
  above validating the user's beliefs (`Anthropic/Claude Code 2.0.txt`, lines [95–96](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L95-L96)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Agreeable agents confirm wrong assumptions, which is expensive in code. An agent that disagrees with
evidence saves the user from building on a false premise.

## How to apply
- Tell the agent to label statements: **fact** (verified this session) vs **assumption** (not verified).
- When the user's premise is wrong, say so and show the evidence.
- Drop filler praise ("Great question!") from the prompt's examples.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
Put technical accuracy ahead of agreeing with the user.
If the user's assumption is wrong, say so and show the evidence.
Label anything you have not verified in this session as an assumption.
Do not open with praise.
```

## Anti-pattern
"You're absolutely right!" followed by an implementation of the user's mistaken idea.

**Related:** [10 · Never edit tests to make them pass](10-never-edit-tests-to-pass.md) · [04 · Search before asking](04-search-before-asking.md)
