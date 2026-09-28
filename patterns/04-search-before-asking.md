# 04 · Search before asking

**Group:** Context & planning · **Status:** `OBSERVED` · **Seen in:** Cursor

## Pattern
If the agent can get the information with its own tools, it does that **instead of asking the user**.
It asks only for what it cannot find: missing credentials or permissions, or a choice that belongs
to the user.

## Evidence
- Cursor Agent Prompt 2.0: prefer tool calls over asking the user when the information is obtainable
  (line [531](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L531)); bias towards not asking if the answer can be found (line [551](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L551)); do not guess file contents,
  read them (line [534](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Cursor%20Prompts/Agent%20Prompt%202.0.txt#L534)).
- Contrast, Devin: if information cannot be found, the task seems unclear, or context or credentials
  are missing, the agent should ask the user and not be shy about it (`Devin AI/Prompt.txt`,
  line [43](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L43)).
  Both agree on *what* to ask about; Cursor leans harder towards not asking.

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Every question costs the user a context switch. Answers the agent finds itself are also more accurate
than the user's memory of the code.

## How to apply
Split "unknowns" into two lists in the prompt:
- **Discoverable:** file contents, configuration, versions, existing conventions → look it up.
- **Only the user knows:** intent, preferences, secrets, trade-off decisions → ask.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
Before asking the user anything, check whether your tools can answer it
(files, configuration, git history, dependency lists).
Ask only for intent, preferences, credentials, or a choice you cannot make yourself.
```

## Anti-pattern
"Which file handles authentication?" when a search would answer it in one call.

**Related:** [07 · Verify state before acting](07-verify-state-before-acting.md) · [05 · Distinguish questions from requests](05-questions-vs-requests.md)
