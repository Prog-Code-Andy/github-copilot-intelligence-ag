# Instructions — Vendor Rules

## Purpose

Authoritative technical specification for repository instruction files,
sourced from official VS Code / GitHub Copilot documentation
(`temp-files-skills/instructions-v1.128.md`). This file is consulted by
[`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)
(section "Generate or Reuse Instructions") before creating or modifying any
repository or path-specific instruction file.

---

## Two categories of instructions

VS Code supports two categories. If multiple instruction files exist, VS
Code combines and adds them all to the chat context — no specific
combination order is guaranteed, so avoid contradictory rules across files.

### 1. Always-on instructions

Automatically included in **every** chat request. Use for project-wide
coding standards, architecture decisions, and conventions that apply to all
code.

| Mechanism | Location | Scope | Notes |
|---|---|---|---|
| `.github/copilot-instructions.md` | Workspace root `.github/` | Whole workspace | Auto-detected by VS Code; GitHub-Copilot specific. |
| `AGENTS.md` | Workspace root (or subfolders, experimental) | Whole workspace (or subfolder, experimental) | Agent-agnostic; useful across multiple AI coding tools. Root-level requires `chat.useAgentsMdFile` (default on). Nested per-folder requires the experimental `chat.useNestedAgentsMdFiles` setting. |
| Organization-level instructions | Defined at the GitHub organization level | All repos in the org | Shared across multiple workspaces/repositories. |
| `CLAUDE.md` | Workspace root, `.claude/`, or user home | Whole workspace | Compatibility with Claude Code and other Claude-based tools. |

**Guidance:** start with a single `.github/copilot-instructions.md` for
project-wide standards. Use `AGENTS.md` when multiple AI agents need to share
one instruction set. Do not duplicate the same rule across both — update it
in one place and cross-reference from the other.

### 2. File-based instructions (`.instructions.md`)

Applied conditionally when the file(s) the agent is working on match a glob
pattern, or when the instruction's description semantically matches the
current task. Use for language-specific conventions, framework patterns, or
rules scoped to part of the codebase.

Location:

```text
.github/instructions/<name>.instructions.md
```

Can be organized into subfolders for clarity, for example:

```text
.github/instructions/
  frontend/
    react.instructions.md
    accessibility.instructions.md
  backend/
    api-design.instructions.md
  testing/
    unit-tests.instructions.md
```

#### Frontmatter fields

| Field | Required | Description |
|---|---|---|
| `name` | No | Display name shown in the UI. Defaults to the file name. |
| `description` | No | Short description shown on hover in the Chat view. |
| `applyTo` | No | Glob pattern defining which files trigger automatic application, relative to the workspace root. Use `**` to apply to all files. If omitted, the instructions are not applied automatically but can still be added manually to a chat request. |

Example:

```markdown
---
name: 'Python Standards'
description: 'Coding conventions for Python files'
applyTo: '**/*.py'
---
# Python coding standards
- Follow the PEP 8 style guide.
- Use type hints for all function signatures.
- Write docstrings for public functions.
- Use 4 spaces for indentation.
```

## Selecting the right mechanism

| Use case | Mechanism |
|---|---|
| Coding style, naming, tech-stack, architecture, security, docs standards applying to the whole repo | `.github/copilot-instructions.md` |
| Sharing one rule set across multiple AI agents/tools | `AGENTS.md` |
| Frontend vs. backend conventions in a monorepo | Multiple `.instructions.md` with different `applyTo` |
| Language-specific rules in a polyglot repo | `.instructions.md` per language |
| Framework-specific rules for specific modules | `.instructions.md` scoped via `applyTo` |
| Rules only for tests or documentation | `.instructions.md` scoped via `applyTo` |

## Relevant settings

- `chat.useAgentsMdFile` — enables/disables root-level `AGENTS.md` detection (default: enabled).
- `chat.useNestedAgentsMdFiles` — experimental; enables recursive discovery of subfolder `AGENTS.md` files.

## Generating instructions automatically

VS Code can analyze a workspace and generate always-on instructions
matching existing coding practices: it discovers existing conventions
(`copilot-instructions.md`, `AGENTS.md`), analyzes project structure/coding
patterns, then generates tailored workspace instructions. When the universal
meta-prompt builder is asked to "generate instructions from the existing
codebase," this is the underlying mechanism it is emulating — so it should
follow the same order: discover existing conventions first, analyze the
project, generate only what's missing or requested.

## Checklist for the builder

- [ ] Repository-wide rule → `.github/copilot-instructions.md`, not an
      `.instructions.md` file.
- [ ] Rule scoped to specific files/folders/languages → `.instructions.md`
      with a correct `applyTo` glob.
- [ ] Multi-agent-agnostic shared ruleset → `AGENTS.md`, not duplicated into
      `copilot-instructions.md`.
- [ ] No nested `AGENTS.md` created unless the task explicitly requires it
      and `chat.useNestedAgentsMdFiles` is acknowledged as experimental.
- [ ] `.instructions.md` frontmatter includes a meaningful `description` (used
      for semantic matching when `applyTo` is absent or task-based).
- [ ] No contradictory rules introduced across multiple always-on files
      (VS Code merges them with no guaranteed order).

## Consumed by

- [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md) — "Generate or Reuse Instructions" and "Capability Classification" sections.
- [`../01-wrapper-structure-initializer.md`](../01-wrapper-structure-initializer.md) — creates the initial `.github/copilot-instructions.md` and root `AGENTS.md`.
- [`../03-build-linking-compiler.md`](../03-build-linking-compiler.md) — "Relationship rules by component / C. Path-specific instructions".
