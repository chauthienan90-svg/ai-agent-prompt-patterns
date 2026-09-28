# 06 · Separate planning and execution modes

**Group:** Context & planning · **Status:** `OBSERVED` · **Seen in:** Devin

## Pattern
Run the agent in explicit modes. In the Devin prompt:
- **Planning:** gather all the information needed for the task (search, read, inspect). A
  planning-only command signals that enough information has been gathered for a complete plan.
- **Standard:** the plan's current and next steps are shown to the agent, which acts on them and
  follows the plan's requirements.

Making planning **read-only** is our recommendation (see *How to apply*), not something the source
prompt states.

## Evidence
- Devin: the agent is always in one of the two modes, and **the user tells it which** before each
  next action, so mode selection comes from outside the agent (`Devin AI/Prompt.txt`, line [41](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L41)).
- Devin: mode "planning" is for gathering all needed information (`Devin AI/Prompt.txt`, line [42](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L42));
  mode "standard" follows the plan steps (line [45](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L45)); a planning-only command marks the plan as ready
  (line [383](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/1e4203a7d88873c1b37ab2d1c07074fea498c274/Devin%20AI/Prompt.txt#L383)).

*Source: community-extracted, unofficial prompts from [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/tree/1e4203a7d88873c1b37ab2d1c07074fea498c274) at commit `1e4203a` (2026-08-11). Line links point to that snapshot.*

## Why it helps
Mixing exploration and editing leads to edits made on half the picture. A mode boundary forces the
agent to finish understanding before it changes anything.

## How to apply
- Store `mode` as explicit state (`planning` → `execute` → `verify` → `blocked`).
- Allow only read-only tools in `planning`.
- Define the exit condition: all affected locations found and a plan written.

## Drop-in snippet
An original wording you can paste into your own prompt and adapt:

```text
You work in two modes.
PLANNING: read and search only. Find every place that must change, then write a plan.
EXECUTE: carry out the approved plan step by step.
Never edit a file while in PLANNING.
```

## Anti-pattern
Editing the first file found while still searching for the rest.

**Related:** [05 · Distinguish questions from requests](05-questions-vs-requests.md) · [08 · Mandatory reflection at decision points](08-think-at-decision-points.md)
