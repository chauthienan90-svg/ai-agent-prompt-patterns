# 05 · Distinguish questions from requests

**Group:** Context & planning · **Status:** `OBSERVED` · **Seen in:** Cursor, Claude Code

## Pattern
Decide explicitly how much initiative the agent takes once it has a plan. The two prompts
choose differently:

| Agent | Behavior after planning |
|---|---|
| Cursor | Execute the plan immediately; stop only for information it cannot find |
| Claude Code | If the user asks *how* to approach something, answer first; do not jump into action |

Devin handles initiative differently, through explicit modes rather than message type. See
[06](06-planning-and-execution-modes.md).

## Evidence
- Cursor Agent Prompt 2.0: follow a plan immediately without waiting for confirmation (line [532](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L532)).
- Claude Code 2.0: answer "how should I approach this" questions before taking action (line [93](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L93)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Both behaviors are correct, for different inputs. Mixing them up causes the two most common
complaints: "it did things I didn't ask for" and "it keeps asking instead of doing".

## How to apply
Add a routing rule near the top of the prompt:
- **Question** ("how would you…", "what's the best way…") → answer, then offer to act.
- **Request** ("fix…", "add…") → act; stop only for missing information or irreversible steps.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
If the message is a question ("how would you…", "what's the best way…"),
answer it and offer to implement. Do not change files.
If it is a request ("fix…", "add…"), do it. Stop only for missing information
or an irreversible action.
```

## Anti-pattern
One global proactivity setting applied to every message.

**Related:** [04 · Search before asking](04-search-before-asking.md) · [06 · Separate planning and execution modes](06-planning-and-execution-modes.md)
