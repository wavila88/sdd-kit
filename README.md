# sdd-kit

Lightweight spec-driven development for Claude Code. Minimal documentation and developer control at every phase.

- **Few words:** a short spec (happy paths and sad paths) and a list of phases. Nothing else.
- **TDD per phase:** every phase starts with a failing test and ends with the test green.
- **Pair programming:** when a phase is done, Claude stops. You review the code and the manual check, give feedback ("move the button down", "use that interface") and Claude applies it until you say it looks good.

## Flow

| Command | When | Result |
|---|---|---|
| `/sdd:scan` | Once, when installing in a repo (or when the project changes) | `.sdd/project.md`: stack, architecture, conventions and test command, each fact with its source file |
| `/sdd:specify <description>` | For each change | `.sdd/specs/NNN-name/spec.md` (simple ~15 lines, complex ~50) |
| `/sdd:create-tasks` | After the spec | `tasks.md` with vertical phases |
| `/sdd:implement` | Once per phase | Builds **one** phase and waits for your approval |

Each phase in `tasks.md`:

```markdown
## Phase 1 — Clear the field after a search (covers HP-1)
- [ ] 1.1 Failing test — result: ________
- [ ] 1.2 Implementation — files: ________
- [ ] 1.3 Passing test — result: ________
- [ ] 1.4 Developer approval
```

Claude checks 1.1-1.3. Box 1.4 is only checked with your explicit approval. The boxes are the state: if you close the editor, `/sdd:implement` resumes where it left off.

## Installation

As a plugin, in the project where you want to use it:

```
/plugin marketplace add wavila88/sdd-kit
/plugin install sdd@sdd-kit
```

Then run `/sdd:scan` and review `.sdd/project.md`.

## Structure in your project

```
.sdd/
├── project.md
└── specs/
    └── 001-clear-search/
        ├── spec.md
        └── tasks.md
```
