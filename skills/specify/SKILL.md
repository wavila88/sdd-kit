---
name: specify
description: Use when the developer describes a change, feature or bug fix they want to build and there is no spec for it yet in .sdd/specs/.
argument-hint: "[simple|complex] <description of the change>"
---

# Specify a change

Turn the developer's description into a short `spec.md`: what must happen when things go right (happy path) and when they go wrong (sad paths). No technical design; that comes from `.sdd/project.md` during implementation.

## Steps

1. **Require the project scan.** If `.sdd/project.md` does not exist, stop and ask the developer to run `/sdd:scan` first.
2. **Read** `.sdd/project.md` and the code areas the description touches, so the spec uses the project's real names (pages, endpoints, entities).
3. **Choose the size.** If the developer wrote `simple` or `complex` first, use it. Otherwise:
   - **simple**: one or two behaviors, a few files, no new entity, API, dependency or architectural piece.
   - **complex**: anything else.
   Tell the developer which size you chose and why, in one line.
4. **Create the folder** `.sdd/specs/NNN-short-name/`, where `NNN` is the next three-digit number after the highest one present (start at `001`).
5. **Write `spec.md`** with the template. Write it in English.
6. **Questions.** Ask only what blocks the spec, at most 3, and write the answers into the spec. For anything else, choose a reasonable default and state it.
7. **Finish** with the path of the spec and suggest `/sdd:create-tasks` as the next step.

## Size limits

| | simple | complex |
|---|---|---|
| Length | ~15 lines | ~50 lines |
| Happy paths | 1-2 | as many as there are distinct user goals |
| Sad paths | only the ones a user can realistically hit | same, plus integration failures |
| Extra section | — | "Touches": the layers or components involved, by name from project.md |

Each path is one line: given, when, then. Sad paths cover what matters (invalid input, empty result, service down), not every theoretical edge case.

## Template

```markdown
# <Title>
Size: <simple|complex> — <one-line reason>

## Goal
<one or two sentences: what the user can do and why>

## Happy path
- HP-1: Given <context>, when <action>, then <observable result>.

## Sad paths
- SP-1: Given <context>, when <action>, then <observable result>.

## Out of scope
- <what this change explicitly does not do>

## Touches            (complex only)
- <layer/component from project.md>

## Decisions and open questions
- <default chosen or answer received>
```
