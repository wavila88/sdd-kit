---
name: create-tasks
description: Use when a spec.md exists in .sdd/specs/ and the developer wants the implementation broken into phases, or when tasks.md is missing for a spec.
argument-hint: "[optional: spec folder, defaults to the most recent one]"
---

# Create the tasks

Turn `spec.md` into `tasks.md`: a list of phases. Each phase is one small, vertical slice of behavior that is built with TDD and approved by the developer before the next one starts.

## Steps

1. **Pick the spec.** The folder given as argument, otherwise the highest-numbered folder in `.sdd/specs/`. If it has no `spec.md`, ask the developer to run `/sdd:specify` first.
2. **Read** `spec.md` and `.sdd/project.md` (test command, test location, architecture).
3. **Cut the phases.**
   - One phase = one behavior the user can observe, tested end to end at the level the project uses (unit, integration or e2e, whatever project.md shows).
   - Happy paths first, then sad paths. Group sad paths only when they share the same code.
   - A phase is small enough to review in one sitting. A simple spec usually has 1-2 phases.
   - Never split by layer ("phase 1: model, phase 2: UI"); every phase cuts through all the layers it needs.
4. **Write `tasks.md`** next to `spec.md` with the template. Reference the spec IDs (`HP-1`, `SP-2`); do not copy the spec text.
5. **Finish** with the number of phases and suggest `/sdd:implement` to build Phase 1.

## Template

```markdown
# Tasks: <Title>
Spec: ./spec.md
Test command: `<from project.md>`

## Phase 1 — <behavior in a few words> (covers HP-1)
Test: <test file and what it asserts, one line>
Manual check: <what the developer opens and does, one line>

- [ ] 1.1 Failing test — result: ________
- [ ] 1.2 Implementation — files: ________
- [ ] 1.3 Passing test — result: ________
- [ ] 1.4 Developer approval

## Phase 2 — <behavior> (covers SP-1)
...
```

The blanks are filled in by `/sdd:implement` while it works.
