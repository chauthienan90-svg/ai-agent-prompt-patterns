# 03 · Batch independent calls

**Group:** Tool use · **Status:** `OBSERVED` · **Seen in:** Claude Code, Devin

## Pattern
When several tool calls do not depend on each other, issue them **in the same turn** instead of
one after another.

## Evidence
- Claude Code 2.0: batch independent tool calls in a single response; independent shell commands go
  in one message (`Anthropic/Claude Code 2.0.txt`, lines [160–161](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L160-L161), [232](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Anthropic/Claude%20Code%202.0.txt#L232)).
- Devin: output multiple search commands at once for parallel search (`Devin AI/Prompt.txt`, line [216](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L216)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Each turn costs a model round-trip. Batching reading and searching cuts latency and cost without
changing the result.

## How to apply
- In the prompt, state the rule and its condition: *independent* calls only.
- In a workflow engine, mark steps as `independent` so they can be scheduled together.
- Keep dependent steps sequential. A call that needs the output of another must wait for it.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
When you need several pieces of information that do not depend on each other,
request them in the same turn (for example, read three files at once).
If one call needs the result of another, run them in order.
```

## Anti-pattern
Batching calls that depend on each other, for example editing a file in the same batch as the read
that was supposed to decide the edit.

**Related:** [01 · Situational tool rules](01-situational-tool-rules.md) · [06 · Separate planning and execution modes](06-planning-and-execution-modes.md)
