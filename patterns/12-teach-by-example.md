# 12 · Teach behavior by example

**Group:** Behavior · **Status:** `OBSERVED` · **Seen in:** Claude Code

## Pattern
For behavior that is hard to describe in rules, such as answer length, tone or when to stop, give
**2–3 input → output examples** instead of more rules.

## Evidence
- Claude Code 2.0 contains 22 `<example>` blocks (`Anthropic/Claude Code 2.0.txt`), showing exactly how short an answer should be (lines [44–62](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L44-L62)).
- For comparison: Cursor Agent Prompt 2.0 has 14 `<example>` blocks and the Devin prompt has none.

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
"Be concise" means different things to different readers. An example of a one-line answer leaves no
room for interpretation.

## How to apply
- Use examples for style and judgment; use rules for hard constraints.
- Show contrast: one good response and, where useful, one to avoid.
- Keep examples short and realistic. The model copies their length as well as their content.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
Keep answers short. Examples:
user: which command lists the files here?
assistant: ls
user: does parse_user() handle a null input?
assistant: No. Line 42 reads user.name without a null check.
```

## Anti-pattern
Ten lines of rules about brevity followed by a long example answer. The example wins.

**Related:** [05 · Distinguish questions from requests](05-questions-vs-requests.md) · [11 · Accuracy over agreement](11-accuracy-over-agreement.md)
