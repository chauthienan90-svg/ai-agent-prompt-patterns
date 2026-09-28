# 02 · Tool descriptions say when *not* to use them

**Group:** Tool use · **Status:** `OBSERVED` · **Seen in:** Claude Code, Devin

## Pattern
Each tool description includes a **"do not use when"** line pointing to the better alternative,
not only a "use when" line.

## Evidence
- Claude Code 2.0: the shell tool says not to use it for reading, editing or searching files and
  names the dedicated tools instead (`Anthropic/Claude Code 2.0.txt`, lines [162](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L162), [199](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L199)).
- Devin: the shell must never be used to view, create or edit files; editor commands are used instead
  (`Devin AI/Prompt.txt`, line [105](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L105)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
When two tools overlap (a shell can do almost anything), the model picks the more general one unless
told otherwise. The negative line removes the overlap.

## How to apply
For every tool, answer three questions in its description:
1. What is it for?
2. When should it be used?
3. **When should it not be used, and what should be used instead?**

See the tool schema example (section 10) in [`templates/prompt-framework.md`](../templates/prompt-framework.md).

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
shell: run builds, tests, git and package managers.
  Use when: the task needs a terminal command.
  Do NOT use when: reading, searching or editing files. Use read_file, search and edit_file instead.
```

## Anti-pattern
A general-purpose tool (shell, HTTP client, SQL) with no stated limits. It will absorb work that
specialized, safer tools were built for.

**Related:** [01 · Situational tool rules](01-situational-tool-rules.md) · [03 · Batch independent calls](03-parallel-independent-calls.md)
