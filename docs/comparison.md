# Side-by-side comparison: Cursor, Claude Code, Devin

How three coding-agent system prompts are structured, based on community-extracted copies.
See [Sources & method](../README.md#sources--method) for what that means and its limits.

| Prompt | File in source repo | Size |
|---|---|---|
| Cursor Agent Prompt 2.0 | `Cursor Prompts/Agent Prompt 2.0.txt` | ~40 KB |
| Claude Code 2.0 | `Anthropic/Claude Code 2.0.txt` | ~58 KB |
| Devin | `Devin AI/Prompt.txt` | ~35 KB |

## 1. Same skeleton, different emphasis

All three prompts contain the same building blocks, named differently:

| Block | Cursor | Claude Code | Devin |
|---|---|---|---|
| Identity & role | Very short | Short | Longer, stresses capability |
| Communication & tone | `<communication>` | "Tone and style" + many examples | "When to Communicate" |
| Tool-calling rules | `<tool_calling>`, 9 numbered rules | "Tool usage policy" | "Command Reference" |
| Context gathering | `<maximize_context_understanding>` | "Doing tasks" | Planning mode |
| Code-change rules | `<making_code_changes>` | Edit tool + "Code References" | "Coding Best Practices" |
| Task tracking | `todo_write` | `TodoWrite` | `suggest_plan` |
| Safety & security | Little explicit guidance | Defensive-security rules | "Data Security" |
| Tool definitions | Separate JSON schema | Inline, very detailed | XML-style commands |

**Observation:** behavioral instructions are a minority of each prompt. Most of the text defines
tools and explains how to use each one. In these prompts, the quality of the tool descriptions seems
to matter more than the "You are…" paragraph. *(This is an interpretation, not a measured result.)*

## 2. Where they differ

| Topic | Cursor | Claude Code | Devin |
|---|---|---|---|
| Initiative | High: executes a plan without waiting | Balanced: answers "how" questions before acting | Governed by mode (planning / standard) |
| Answer length | Normal | Very short (CLI interface) | Reports only when needed |
| Git commits | Not specified | Only when the user explicitly asks | Follows the plan |
| Revealing instructions | Not specified | Not specified | Explicit rule never to reveal them |
| `<example>` blocks | 14 | 22 | 0 |

## 3. Takeaway

The prompts agree on the fundamentals (tool rules, context first, verification) and differ mainly on
**initiative** and **verbosity**. Those two settings are product decisions, not universal best
practice. Choose them deliberately for your interface and users (see
[pattern 05](../patterns/05-questions-vs-requests.md)).
