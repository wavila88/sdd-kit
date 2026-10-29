---
name: scan
description: Use when installing SDD in a repository, when .sdd/project.md does not exist, or when the developer asks to refresh the project standards after the architecture, stack or test setup changed.
argument-hint: "[optional: areas to focus on]"
---

# Scan the project

Produce `.sdd/project.md`: the short, evidence-based summary of how this repository is built. The other SDD skills read it instead of re-scanning, and the developer reviews code against it.

## Steps

1. **Read existing standards first.** `CLAUDE.md`, `AGENTS.md`, `README*`, `CONTRIBUTING*`, `docs/`, `.editorconfig`, linter and formatter configs. What the team already wrote wins over anything you infer.
2. **Detect the stack.** Manifests (`*.csproj`, `*.sln`, `package.json`, `requirements*.txt`, `pyproject.toml`, `go.mod`, ...): language, framework, main libraries, versions.
3. **Detect the architecture.** Folder and project layout, 2-3 representative files per layer. Name the pattern only when the evidence supports it (for example Clean Architecture: `Core/`, `Inbound/`, `Outbound/`, Core has no references to the outer layers). Write the dependency rules you can see.
4. **Detect conventions.** Naming, error handling, logging, dependency injection, how a typical feature is wired. Take them from real code, not from habit.
5. **Frontend (if any).** Styling approach (CSS files, Tailwind, design tokens, component library), where shared components live.
6. **Tests.** Frameworks, where tests live, kinds (unit, integration, e2e), naming, and the exact **command to run them**. If you cannot find the command, write `not detected` and ask; TDD depends on it.
7. **Run the app.** Command and URL used for manual checks.
8. **Write `.sdd/project.md`** with the template below. If the file exists, update it and keep the developer's manual edits.
9. **Show the developer a 5-line summary** plus everything under "Not detected / questions", and ask them to correct it. Apply their corrections to the file.

## Rules

- Every statement cites its source in parentheses: `(← src/Core/Core.csproj)`. No source, no statement.
- Anything you could not confirm goes under "Not detected / questions". Never fill a gap with a guess.
- Keep it under ~60 lines. It is a reference card, not documentation.
- Do not change any code.

## Template

```markdown
# Project: <name>
Sources read: <files>
Last scan: <YYYY-MM-DD>

## Stack
- <language / framework / version> (← <file>)

## Architecture
- Pattern: <name> (← <evidence>)
- Layers: <folder> → <what goes there>
- Dependency rules: <rule> (← <evidence>)

## Conventions
- <convention> (← <example file>)

## Frontend
- <styling approach, shared components> (← <file>)   | or: N/A

## Tests
- Frameworks: <...> (← <file>)
- Location and naming: <...>
- Command: `<command>`

## Run the app
- `<command>` → <url>

## Not detected / questions
- <item>
```
