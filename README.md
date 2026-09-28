# AI Agent Prompt Patterns

12 reusable design patterns for coding-agent system prompts, drawn from a side-by-side reading of
the Cursor, Claude Code and Devin prompts, with a fill-in template for writing your own.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
&nbsp;·&nbsp; [Tiếng Việt](README.vi.md)

## What this is

A study of **how** production coding agents are instructed, reduced to patterns you can apply to
your own agents, skills or custom GPTs. Each pattern has:

- the **pattern** in one paragraph
- **evidence**: where it appears in the source prompts, down to the line
- **why it helps**, **how to apply it**, and an **anti-pattern** to avoid

## What this is not

- **Not a copy of any prompt.** Every pattern is written in our own words. Nothing is reproduced
  verbatim beyond a few identifiers such as tag and tool names.
- **Not official documentation.** The source prompts were extracted by the community, not published
  by the vendors (see [Known limitations](#known-limitations)).
- **Not benchmarked.** "Why it helps" is reasoning, not a measured result.

## Patterns

### Tool use
| # | Pattern | Seen in |
|---|---|---|
| 01 | [Situational tool rules](patterns/01-situational-tool-rules.md): one numbered rule per concrete situation | Cursor |
| 02 | [When *not* to use a tool](patterns/02-when-not-to-use.md): every tool names its better alternative | Claude Code, Devin |
| 03 | [Batch independent calls](patterns/03-parallel-independent-calls.md): parallelize what does not depend on each other | Claude Code, Devin |

### Context & planning
| # | Pattern | Seen in |
|---|---|---|
| 04 | [Search before asking](patterns/04-search-before-asking.md): ask only for what cannot be discovered | Cursor |
| 05 | [Questions vs requests](patterns/05-questions-vs-requests.md): answer questions, act on requests | Cursor, Claude Code |
| 06 | [Planning and execution modes](patterns/06-planning-and-execution-modes.md): gather everything before executing | Devin |
| 07 | [Verify state before acting](patterns/07-verify-state-before-acting.md): re-read after failures, check dependencies | Cursor, Devin |

### Verification & repair
| # | Pattern | Seen in |
|---|---|---|
| 08 | [Reflection at decision points](patterns/08-think-at-decision-points.md): a mandatory gate before "done" | Devin |
| 09 | [Bounded self-repair](patterns/09-bounded-self-repair.md): max 3 fix attempts, then stop | Cursor, Devin |
| 10 | [Never edit tests to pass](patterns/10-never-edit-tests-to-pass.md): acceptance criteria are not negotiable | Devin |

### Behavior
| # | Pattern | Seen in |
|---|---|---|
| 11 | [Accuracy over agreement](patterns/11-accuracy-over-agreement.md): evidence beats validation | Claude Code |
| 12 | [Teach by example](patterns/12-teach-by-example.md): examples for style, rules for constraints | Claude Code |

## Also in this repo

- [**Side-by-side comparison**](docs/comparison.md): how the three prompts are structured and where they differ
- [**Prompt framework template**](templates/prompt-framework.md): a 10-part skeleton linked to the patterns above

## How to use

1. Skim the pattern tables and pick the ones your agent is missing.
2. Copy [`templates/prompt-framework.md`](templates/prompt-framework.md) and fill in each section.
3. Check your draft against the anti-pattern at the end of each pattern file.

## Sources & method

| | |
|---|---|
| Source | [`x1xhlol/system-prompts-and-models-of-ai-tools`](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools) (GPL-3.0) |
| Snapshot | commit `1e4203a`, 2026-08-11 |
| Files read | `Cursor Prompts/Agent Prompt 2.0.txt`, `Anthropic/Claude Code 2.0.txt`, `Devin AI/Prompt.txt` |
| Method | Read in full; every claim checked against the file and cited by line number |

Every pattern is marked **`OBSERVED`**: the behavior appears in the extracted prompt text at that
snapshot. None is marked `VERIFIED`. No pattern was tested against the live products.

## Known limitations

- **Unofficial sources.** The prompts are community extractions. They may be outdated, incomplete or
  inaccurate, and the vendors have not confirmed them.
- **Point-in-time.** The products change their prompts; line numbers refer to the snapshot above.
- **Three agents only.** Patterns seen in one prompt may not generalize. The *Seen in* column shows
  how widely each pattern was observed.
- **No benchmarks.** This repo does not measure whether a pattern improves agent quality.

## Contributing

New patterns, corrections and evidence from other agents are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE) for the analysis and template in this repo. The source prompts belong to their
respective owners and are **not** included here.
