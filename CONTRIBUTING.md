# Contributing

Thanks for helping improve this collection. Three kinds of contribution are useful:

1. **A correction:** a pattern misdescribes its source, a line reference is wrong, or a source has changed.
2. **New evidence:** the same pattern appears in another agent's prompt (Windsurf, Kiro, Cline…).
3. **A new pattern:** a recurring design choice not covered yet.

## Rules for every pattern

- **Cite evidence.** Name the source file and the line numbers, plus the snapshot (commit or date).
  No evidence, no pattern.
- **Paraphrase; do not copy.** Describe the behavior in your own words. Quote at most a tag or tool
  name, never whole instructions.
- **Mark the status honestly.** Use `OBSERVED` (appears in the source text). Use `VERIFIED` only if
  you tested the behavior and describe how.
- **Separate fact from interpretation.** "Why it helps" is reasoning. Do not present it as a
  measured result.
- **No sensitive data.** No API keys, personal data or private URLs in examples.

## File format

Copy an existing file in [`patterns/`](patterns/) and keep its sections:

```text
# NN · Title
**Group:** … · **Status:** `OBSERVED` · **Seen in:** …
## Pattern
## Evidence
## Why it helps
## How to apply
## Anti-pattern
```

Then add a row to the matching table in [README.md](README.md).

## Process

Open an issue with the **New pattern / correction** template first, or send a pull request directly
for small fixes.
