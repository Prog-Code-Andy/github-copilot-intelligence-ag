# Linked Meta-Prompt Bundle

This folder is the consolidated, executable bundle for generating GitHub
Copilot agent capability packages (agent + instructions + skills + prompts
+ hooks + workflows) in a professional, non-duplicated, standards-compliant
way. It replaces four previously isolated meta-prompts with one linked
pipeline, plus five vendor-sourced rule files.

`Linked Relations.png` (already in this folder) illustrates the target
relationship model this bundle produces inside a repository's `.github/`
directory once it has been run end to end.

---

## Execution pipeline

```text
00-README.md                                (you are here — read first)
        │
        ▼
01-wrapper-structure-initializer.md          Step 1/3 — scaffold .github/
        │
        ▼
02-universal-meta-prompt-builder.md          Step 2/3 — generate the
        │                                    capability package, consulting
        │                                    rules/*.rules.md for each
        │                                    component type as needed
        ▼
03-build-linking-compiler.md                 Step 3/3 — link everything
                                              generated in Step 2 and
                                              produce the architecture report
```

Load order (progressive disclosure, mirroring how VS Code loads skills —
see [`rules/skills.rules.md`](./rules/skills.rules.md)):

1. **Always read first:** this README, to know where you are in the
   pipeline.
2. **Read next, based on stage:** whichever of `01-`, `02-`, or `03-` is
   relevant. `01-` only needs to run once per repository (or whenever the
   `.github` skeleton is incomplete); `02-` runs for every agent-generation
   task; `03-` runs once at the end of every `02-` session.
3. **Read on demand, only when generating that specific component type:**
   the matching file under [`rules/`](./rules/). `02-` explicitly points to
   the right one at the moment it is needed — do not preload all five.

---

## Files in this bundle

| File | Role | Derived from |
|---|---|---|
| [`00-README.md`](./00-README.md) | Bundle index and pipeline map | New — synthesized for this bundle |
| [`01-wrapper-structure-initializer.md`](./01-wrapper-structure-initializer.md) | Step 1/3 — scaffolds the base `.github` skeleton and root governance files | `main-meta-prompts/create-repo-structure.md` |
| [`02-universal-meta-prompt-builder.md`](./02-universal-meta-prompt-builder.md) | Step 2/3 — the core orchestrator: discovery, evidence, clarification policy, capability classification, generation procedures, security, validation | Merge of `main-meta-prompts/universal-meta-promp-builder-v1.md` and `main-meta-prompts/universal-meta-promp-builder-v2.md` |
| [`03-build-linking-compiler.md`](./03-build-linking-compiler.md) | Step 3/3 — links generated components together and produces the architecture report | `main-meta-prompts/build-linked-copilot.md` |
| [`rules/agents.rules.md`](./rules/agents.rules.md) | Binding `.agent.md` format: frontmatter, subagent behavior, restriction rules | `temp-files-skills/custom-agents-v1.128.md` |
| [`rules/instructions.rules.md`](./rules/instructions.rules.md) | Binding instruction mechanisms: `copilot-instructions.md`, `AGENTS.md`, `.instructions.md` | `temp-files-skills/instructions-v1.128.md` |
| [`rules/prompts.rules.md`](./rules/prompts.rules.md) | Binding `.prompt.md` format: frontmatter, tool references | `temp-files-skills/prompts-v1.128.md` |
| [`rules/skills.rules.md`](./rules/skills.rules.md) | Binding `SKILL.md` format + deep-dive procedure for scaffolding a full `skills/` directory | `temp-files-skills/skills-v1.128.md` + `architecture-github/generate-gitHub-copilot-skills-architecture.md` |
| [`rules/hooks.rules.md`](./rules/hooks.rules.md) | Binding hook JSON format + deep-dive planning procedure, with an explicit correction separating real hook events from GitHub Actions triggers | `temp-files-skills/hooks-v1.128.md` + `architecture-github/generate-gitHub-copilot-hooks-architecture.md` |

All source files listed above remain untouched in their original locations
— this bundle is an additive, reorganized synthesis, not a replacement of
the originals.

---

## Why this structure

- **Separation of concerns**, applied to the meta-prompts themselves: the
  bundle practices exactly what `02-universal-meta-prompt-builder.md`
  preaches — a concise orchestrator, standards kept in dedicated rule
  files, and a distinct linking phase, instead of one giant file.
- **Vendor-accurate by construction:** every `rules/*.rules.md` file is
  traceable to an official VS Code / GitHub Copilot documentation source,
  so the builder cannot silently invent a schema (frontmatter field, hook
  event, naming rule) that doesn't actually exist.
- **One corrected inconsistency worth noting:** the original
  `generate-gitHub-copilot-hooks-architecture.md` treated repository-level
  events (PR opened, branch pushed, issue created) as if they were
  Copilot hook events. `rules/hooks.rules.md` corrects this — those events
  belong to GitHub Actions workflows, not `.github/hooks/*.json`.

## How to use this bundle

Point an agent at `02-universal-meta-prompt-builder.md` with a request such
as "create a Python builder agent" or "audit the existing security reviewer
agent". It will:

1. Confirm (or trigger) `01-wrapper-structure-initializer.md` if the
   `.github` skeleton is missing.
2. Run its own discovery, evidence-authority, and clarification steps.
3. Generate/modernize the requested agent and its supporting instructions,
   skills, prompts, and hooks — consulting the relevant `rules/*.rules.md`
   file for each.
4. Hand off to `03-build-linking-compiler.md` to link everything and
   produce the final architecture report.

No file in this bundle should be run in isolation as a substitute for the
full pipeline; each step assumes the previous one has run.
