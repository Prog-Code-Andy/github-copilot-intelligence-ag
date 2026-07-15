# Skills — Vendor Rules & Deep-Dive Generation Procedure

## Purpose

This file has two parts:

- **Part 1 — Vendor specification** (binding): the authoritative
  `SKILL.md` / Agent Skills format, sourced from official documentation
  (`temp-files-skills/skills-v1.128.md`).
- **Part 2 — Deep-dive generation procedure** (practical workflow): a
  merged, phase-based procedure for generating a complete `skills/`
  directory at scale, adapted from
  `architecture-github/generate-gitHub-copilot-skills-architecture.md`.

Both parts are consulted by
[`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)
(section "Generate or Reuse Skills") whenever a skill needs to be created,
reused, or a whole `skills/` directory needs to be scaffolded. **Part 1
governs what is technically valid; Part 2 governs how to run the generation
workflow efficiently. Where Part 2's descriptive suggestions (e.g. extra
Metadata fields) go beyond what Part 1 says VS Code actually parses, Part 1
wins — see the reconciliation note at the end of Part 2.**

---

# Part 1 — Vendor specification (binding)

## What agent skills are

Agent skills are structured bundles of instructions, scripts, and
supporting resources that package everything needed to perform a task into
a reusable system, instead of relying on one-off prompts. GitHub Copilot
automatically loads relevant skills to execute specialized workflows. They
are also designed as an open, cross-environment standard (not VS Code
specific).

A skill typically includes: a description of what it does, rules for how it
should behave, and references to related workflows or dependencies.

## Skills vs. custom instructions

| Feature | Agent Skills | Custom Instructions |
|---|---|---|
| Purpose | Teach specialized capabilities and workflows | Define coding standards and guidelines |
| Portability | Works across VS Code, Copilot CLI, and Copilot cloud agent | VS Code and GitHub.com only |
| Content | Instructions, scripts, examples, and resources | Instructions only |
| Scope | Task-specific, loaded on demand | Always applied (or via glob patterns) |
| Standard | Open standard (agentskills.io) | VS Code-specific |

Use skills when you need reusable, cross-tool capabilities that may bundle
scripts/examples/resources. Use `.instructions.md` (see
[`instructions.rules.md`](./instructions.rules.md)) for always-applied
coding standards.

## File layout

```text
my-skill/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
├── assets/           # Optional: templates, resources
└── ...               # Any additional files or directories
```

Repository location:

```text
.github/skills/<skill-name>/SKILL.md
```

## `SKILL.md` frontmatter fields

| Field | Required | Description |
|---|---|---|
| `name` | **Yes** | Unique identifier. Only lowercase letters, numbers, and hyphens. No slashes, colons, dots, or namespace prefixes. **Must match the parent directory name.** Max 64 characters. Invalid characters cause the skill to **silently fail to load**. |
| `description` | **Yes** | What the skill does and when to use it. Be specific about capabilities and use cases — this drives automatic discovery. Max 1024 characters. |
| `argument-hint` | No | Hint text shown in chat input when invoked as a slash command (e.g. `[test file] [options]`). |
| `user-invocable` | No | Defaults to `true`. Controls whether the skill appears as a slash command in the chat menu. Set `false` to hide it from the `/` menu while still allowing automatic loading. |
| `disable-model-invocation` | No | Defaults to `false`. Set `true` to require manual invocation via the `/` slash command only (agent cannot auto-load it). |
| `context` (Experimental) | No | Defaults to `inline` (instructions added to the parent agent's context). Set to `fork` to run the skill in a dedicated subagent context — only the final result returns to the parent. |

**Critical naming pitfall:** when a skill is distributed through a plugin,
the plugin name is automatically used as a command prefix (e.g.
`/my-plugin:test-runner`). **Do not manually add namespace prefixes to
`name`.** Prefixes like `myorg/skillname` or `myorg:skillname` cause the
skill to **silently fail to load** — there is no error message, it just
doesn't appear.

## Progressive disclosure (three-stage loading)

1. **Discovery** — at startup, only `name` and `description` are loaded into
   context for every available skill (cheap, always-on awareness).
2. **Activation** — when a task matches a skill's description (or the user
   types `/skill-name`), the full `SKILL.md` body is loaded into context.
3. **Execution** — as the agent follows the instructions, it loads
   additional referenced files (scripts, templates, references) only when
   the instructions actually reference them. Unreferenced files in the
   skill directory are never loaded.

This is why many skills can be installed without consuming context —
context cost scales with what's actually relevant to the current task, not
with the total number of skills present.

Skills that opt into `context: fork` follow the same discovery step, but
their instructions and any files they read load into a separate subagent
context; only the final result returns to the parent agent.

## Registering a skill for an extension (if applicable)

If a skill is distributed through a VS Code extension, add the
`chatSkills` contribution point in the extension's `package.json`, with
`path` pointing to the corresponding `SKILL.md`. Not applicable to plain
workspace-level `.github/skills/` folders.

---

# Part 2 — Deep-dive generation procedure

Use this procedure when the universal meta-prompt builder's task is
specifically "scaffold a full `skills/` directory" (as opposed to adding one
narrowly-scoped skill). It complements, and does not replace, the
Capability Classification and Reuse-First rules in
[`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md).

Role framing: act as a senior repository architect extending an existing
`.github` AI architecture by creating a production-ready `skills/`
directory. Do not modify existing Agents, Instructions, Prompts, or
`copilot-instructions.md` — only add new Skills that integrate with what
already exists. Skills represent reusable **capabilities**; Agents represent
decision-making **personas**. Never mix these responsibilities.

## Phase 1 — Repository discovery

Before generating any skill, scan `.github` and validate the existence of
`agents/`, `instructions/`, `prompts/`, and `copilot-instructions.md`. If any
required component is missing, **stop** and report which components are
unavailable — do not generate skills until validation succeeds. (This
mirrors the Mandatory Discovery Phase in the universal builder; do not
duplicate the scan, reuse its result if already performed in this session.)

## Phase 2 — Analyze existing architecture

Read every existing agent (responsibilities, workflows, reusable
capabilities, domain, dependencies), every instruction (standards,
conventions, compliance rules), every prompt (reusable workflows,
implementation/review/testing patterns), and `copilot-instructions.md` as
the global entry point.

## Phase 3 — Skill identification

Extract **reusable capabilities**, not agent names. Do not create a skill by
copying an agent's name 1:1. Example candidate capabilities: architecture
analysis, documentation update, knowledge-base synchronization, code
review, git commit preparation, language-specific clean architecture (e.g.
Python), SQL development/review, QA validation, security analysis,
compliance audit, runbook generation, release management, configuration
validation, dependency analysis, testing, repository analysis, Markdown
documentation, GitHub workflow authoring, issue analysis, pull-request
review.

Apply the Reuse-First Rule from the universal builder: create a skill only
when the capability is genuinely reusable, contains a meaningful multi-step
workflow, and benefits from bundled examples/templates/scripts — not for a
one-line coding rule (that belongs in an instruction file instead).

## Phase 4 — Generate the skills folder

```text
.github/
  skills/
    README.md
    architecture-analysis/
      SKILL.md
    code-review/
      SKILL.md
    documentation-update/
      SKILL.md
    ...
```

One directory per skill; `SKILL.md` is the entry point in each.

## Phase 5 — `SKILL.md` body template

Beyond the required frontmatter (Part 1), structure the body as:

```markdown
---
name: <skill-name>
description: <what it does and when to use it>
---

# Purpose
Business objective, engineering objective, expected outcome.

# Activation
When should this skill be used? Which repository events or tasks trigger
it? Which agent(s) normally invoke it? Can multiple agents invoke it?

# Inputs
E.g. current repository, current branch, changed files, current issue/PR,
architecture documents, runbooks, source files, configuration.

# Outputs
E.g. updated documentation, generated report, implementation plan,
architecture review, QA report, compliance report, commit message.

# Workflow
Numbered steps, e.g.: Analyze → Validate → Load applicable instructions →
Perform task → Validate output → Return result.

# Dependencies
Reference existing project files: copilot-instructions.md, instructions/,
prompts/, agents/ — only those actually relevant.

# Related instructions
List each instruction file used and why.

# Related prompts
List each prompt that can trigger this skill and why.

# Related agents
List each agent capable of invoking this skill and why.

# Best practices
Professional guidance specific to this capability.

# Validation checklist
- [ ] Standards followed
- [ ] Security reviewed
- [ ] Documentation updated
- [ ] Tests generated (if applicable)
- [ ] Dependencies checked
```

> Note: descriptive body headings like "Purpose", "Activation", "Best
> Practices" are plain Markdown content, not parsed frontmatter. Only the
> fields in Part 1's frontmatter table are read by the tool itself.

## Phase 6 — Dependency rules

```text
copilot-instructions.md
        ↓
Relevant instructions
        ↓
Relevant prompts
        ↓
Invoking agents
        ↓
Repository files
```

Never reference unrelated files; load only what is necessary (consistent
with progressive disclosure in Part 1).

## Phase 7 — Cross references

Every skill should explicitly document: which agents use it, which
instructions/prompts it uses, its dependency on `copilot-instructions.md`,
what repository changes it produces, and what repository context it
consumes.

## Phase 8 — `skills/README.md`

Generate one README covering: purpose of skills, difference between agents
and skills, repository architecture, dependency diagram, skill lifecycle,
naming conventions, best practices, how to add new skills, how agents
invoke skills.

## Phase 9 — Architecture diagram

```text
copilot-instructions.md
            │
            ▼
     Instructions
            │
            ▼
        Prompts
            │
            ▼
         Skills
            ▲
            │
         Agents
```

## Phase 10 — Naming convention

Lowercase, kebab-case directory names (e.g. `architecture-analysis/`), entry
file always named `SKILL.md`. Avoid spaces and unestablished abbreviations.
**This must match the `name` frontmatter field exactly (Part 1 requirement)
— the directory name and the `name` field are the same string.**

## Phase 11 — Quality standards

Every skill should be reusable, independent, single-responsibility,
modular, well documented, cross-referenced, easy to maintain,
enterprise-ready, and GitHub Copilot compatible.

## Output requirements

Generate only new files inside `.github/skills/`. Do not regenerate
existing agents, prompts, or instructions. Do not modify
`copilot-instructions.md` as part of this procedure — that belongs to the
build-linking step ([`../03-build-linking-compiler.md`](../03-build-linking-compiler.md)).

## Reconciliation note (Part 1 vs. Part 2)

Part 2's "Metadata" style suggestions (Category, Version, Author, Status,
Tags) from the original architecture generator are **optional descriptive
body content at most**, not parsed frontmatter. Only `name`, `description`,
`argument-hint`, `user-invocable`, `disable-model-invocation`, and `context`
are real frontmatter fields (Part 1). Do not present invented fields as if
VS Code reads them — doing so would silently produce a non-functional
skill, exactly the kind of pitfall Part 1 warns about.

## Checklist for the builder

- [ ] Directory name and `name` frontmatter field match exactly, lowercase
      + hyphens only, ≤ 64 characters, no namespace prefix.
- [ ] `description` is specific enough to drive automatic discovery, ≤ 1024
      characters.
- [ ] Only real frontmatter fields are used (Part 1 table); any extra
      "metadata" is plain body content, not claimed as parsed.
- [ ] Referenced scripts/templates/references actually exist in the skill
      directory before being referenced.
- [ ] `agents/`, `instructions/`, `prompts/`, `copilot-instructions.md`
      exist before generating (Phase 1); if not, defer to
      [`../01-wrapper-structure-initializer.md`](../01-wrapper-structure-initializer.md).
- [ ] Skill was created because it's a reusable, multi-step capability — not
      a one-line rule that belongs in an instruction file.

## Consumed by

- [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md) — "Generate or Reuse Skills" and "Capability Classification" sections.
- [`../03-build-linking-compiler.md`](../03-build-linking-compiler.md) — "Relationship rules by component / E. Skills".
