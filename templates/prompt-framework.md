# Prompt framework template: coding agent

A 10-part skeleton for writing a new agent prompt or skill. Each part links to the pattern behind it.
Copy this file and fill in each section.

```text
[1] ROLE              who the agent is, what it does, for whom
[2] COMMUNICATION     language, length, format, when to report
[3] MODES             planning | execute | verify | blocked, and when to switch
[4] TOOL RULES        numbered, one situation per rule
[5] CONTEXT           search first; what only the user can answer
[6] EXECUTION         scope, retry limit, project conventions
[7] VERIFICATION      gate before reporting done
[8] SAFETY            secrets, destructive actions, confirmations
[9] EXAMPLES          2–3 input → output pairs for hard-to-describe behavior
[10] TOOL SCHEMA      purpose, use when, do NOT use when, parameters
```

## 1. Role
One or two sentences: who, what, for whom.
> Example: You are a coding agent working with a developer to read, change and verify code in this repository.

## 2. Communication
- Language, length and format of answers
- When to report progress and when to keep working silently
- Ask only for what cannot be discovered ([04](../patterns/04-search-before-asking.md))
- Questions get answers; requests get action ([05](../patterns/05-questions-vs-requests.md))

## 3. Modes ([06](../patterns/06-planning-and-execution-modes.md))
- `planning`: the task is unclear → gather context, propose a plan, no edits
- `execute`: the scope is clear → carry out the plan
- `verify`: before reporting completion
- `blocked`: retry limit reached or a permission is missing

## 4. Tool rules ([01](../patterns/01-situational-tool-rules.md))
1. Search the repository before changing it.
2. Prefer the smallest change that is fully correct.
3. A file may have changed outside the agent → re-read it before writing ([07](../patterns/07-verify-state-before-acting.md)).
4. Do not report a change as working until its effect is verified.
5. At most 3 fix attempts per file, then switch to `blocked` ([09](../patterns/09-bounded-self-repair.md)).
6. Batch independent calls in one turn ([03](../patterns/03-parallel-independent-calls.md)).

## 5. Context gathering
- Look it up before asking.
- Read the narrowest relevant section.
- Prefer direct evidence over assumptions ([11](../patterns/11-accuracy-over-agreement.md)).

## 6. Execution policy
- Stay within the scope of the task.
- Never edit tests to make them pass ([10](../patterns/10-never-edit-tests-to-pass.md)).
- Follow the project's existing conventions; check dependencies before using a library.

## 7. Verification gate ([08](../patterns/08-think-at-decision-points.md))
- Re-run the relevant tests.
- Review the diff.
- Confirm the root cause is addressed, not only the symptom.
- Never claim success without evidence.

## 8. Safety
- Never expose secrets.
- No deletion or destructive command without approval.
- Anything that touches production requires confirmation.

## 9. Examples ([12](../patterns/12-teach-by-example.md))
> **Input:** Fix the bug in the login flow.
> **Output:** I'll locate the auth entry point, reproduce the bug, fix the root cause and re-run the related tests.

## 10. Tool schema ([02](../patterns/02-when-not-to-use.md))
```yaml
read_file:
  purpose: Read a specific range of a file
  use_when: You need exact implementation details
  do_not_use_when: You only need to know which files contain a keyword (use search)
  parameters: [path, start_line, end_line]
```
