---
name: implement
description: Use when a tasks.md exists in .sdd/specs/ and the developer wants to build the next phase, continue an interrupted phase, or apply review feedback on the current phase.
argument-hint: "[optional: spec folder, defaults to the most recent one]"
---

# Implement one phase

Build exactly ONE phase of `tasks.md` with TDD, then work with the developer as a pair until they approve it.

**One run = one phase.** After the developer approves, stop. The next phase starts only when the developer runs `/sdd:implement` again.

## Find where to resume

1. Read `.sdd/project.md`, `spec.md` and `tasks.md` of the spec folder (argument, or the highest-numbered one).
2. The current phase is the first one with an unchecked box. Resume at its first unchecked step; the boxes are the only state, so trust them over memory.
3. If every box is checked, report that the spec is complete and stop.

## The four steps

**1. Failing test.** Write only the test for this phase, following the test conventions in project.md. Run the test command. It must fail.
- Fill in the result with the failure line, e.g. `FAILED: clear-button not found`. Check the box.
- If it passes, stop: the test does not exercise new behavior. Show the developer and agree on how to fix the test.

**2. Implementation.** Write the minimum code that makes the test pass, following the architecture, conventions and styles in project.md. Do not touch the test. Fill in the files changed. Check the box.

**3. Passing test.** Run the test command. Fill in the result. Check the box only if it passes.
- If it fails, fix the implementation, not the test. Change the test only if the developer agrees it is wrong.

**4. Developer approval.** Present, then STOP and wait:
- Files changed and a short summary of the diff.
- Self-review against project.md: architecture and dependency rules, conventions, and for frontend changes, consistency with the existing styles. Name anything that deviates.
- The manual check steps from the phase.
- Ask: "¿Apruebas la fase o qué cambiamos?" (in the developer's language).

## Pair-programming loop

The developer replies with feedback ("move the button down", "use the IRepository interface", "inject it through the constructor"):
1. Apply it.
2. Run the test command again; it must still pass.
3. Present again as in step 4 and wait.

Repeat until the developer explicitly approves ("ok", "aprobado", "quedó bien"). Only then check box 4, suggest a commit for the phase, and stop.

## Red flags — stop and follow the steps

| Thought | Reality |
|---|---|
| "The next phase is tiny, I'll do it too." | One run = one phase. Stop after approval. |
| "Tests pass, so I'll mark the approval." | Box 4 is the developer's. Only their explicit OK checks it. |
| "I'll write the code and the test together." | Test first, run it, see it fail. Then code. |
| "I'll adjust the test so it passes." | Fix the code. The test changes only with the developer's agreement. |
| "The feedback is small, no need to re-run the test." | Every change re-runs the test before presenting again. |
