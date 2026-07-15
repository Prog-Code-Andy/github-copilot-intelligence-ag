# Hooks — Vendor Rules & Deep-Dive Planning Procedure

## Purpose

This file has two parts:

- **Part 1 — Vendor specification** (binding): the authoritative hook
  configuration format, sourced from official documentation
  (`temp-files-skills/hooks-v1.128.md`).
- **Part 2 — Deep-dive planning procedure** (design layer): a merged
  procedure for planning a complete set of hooks, adapted from
  `architecture-github/generate-gitHub-copilot-hooks-architecture.md`.

Both parts are consulted by
[`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)
(section "Generate or Reuse Hooks"). **Part 1 is the only source of truth
for what is executable. Part 2 is a planning aid; it must never be used to
invent a hook schema or event name that Part 1 does not support** — see the
Reconciliation note below. This mirrors the "Do not invent unsupported hook
event names or schemas" rule already stated in
[`../03-build-linking-compiler.md`](../03-build-linking-compiler.md).

---

# Part 1 — Vendor specification (binding)

## Why hooks exist

Hooks provide **deterministic, code-driven automation**. Unlike
instructions or prompts, which guide agent behavior probabilistically,
hooks execute real code at specific lifecycle points with guaranteed
outcomes. Common use cases:

- **Enforce security policies** — block dangerous commands (e.g. `rm -rf`,
  `DROP TABLE`) before they execute, regardless of how the agent was
  prompted.
- **Automate code quality** — run formatters, linters, or tests
  automatically after file modifications.
- **Create audit trails** — log every tool invocation, command execution,
  or file change for compliance and debugging.
- **Inject context** — add project-specific information, API keys, or
  environment details to help the agent make better decisions.
- **Control approvals** — automatically approve safe operations while
  requiring confirmation for sensitive ones.

## File format and location

Hooks are defined in JSON files, for example:

```text
.github/hooks/format.json
```

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write ."
      }
    ]
  }
}
```

VS Code automatically loads hook files it finds — no separate registration
step is required. Verify execution using the **Developer: Show Agent Debug
Logs** command.

## How hooks work

A hook has three parts:

1. **An event** that determines when the hook runs (a lifecycle event, such
   as `PostToolUse` — the point after the agent uses a tool, e.g. an edit).
2. **A command** that VS Code runs when the event fires.
3. **Optional JSON input/output** on stdin/stdout that lets the command
   read event details and influence the agent (for example, to block a
   tool call).

Basic hooks (like the quick-start example) ignore stdin and just run a
fixed command. Advanced hooks read the JSON event payload from stdin to
make decisions, and can write a JSON object to stdout to pass context back
to the agent or control what happens next.

**Only lifecycle events that VS Code actually documents/supports are
valid.** `PostToolUse` is confirmed by the vendor example. Do not assume
additional event names exist without confirming them against current VS
Code documentation before relying on them.

## What hooks are not

- Hooks are **not** Git hooks (`.git/hooks/*`) and are **not** GitHub
  Actions workflows. They are a distinct, editor/agent-session-scoped
  automation mechanism.
- Hook events fire based on the **agent's tool-use/session lifecycle**
  inside the editor (e.g. before/after a tool call), **not** on raw GitHub
  repository events such as "pull request opened", "branch pushed", or
  "issue created". Those repository-level events belong to
  `.github/workflows/*.yml` (GitHub Actions), which run server-side on
  GitHub's infrastructure independent of any open editor session — see the
  "Generate or Reuse GitHub Actions Workflows" section of
  [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md).

---

# Part 2 — Deep-dive planning procedure

Use this procedure when the task is "design a comprehensive set of hooks
for this repository", to think through coverage systematically before
writing the real JSON. It complements, and does not replace, Part 1.

Role framing: act as a senior repository architect extending an existing
`.github` AI architecture with a production-ready `hooks/` directory,
without modifying existing Agents, Skills, Instructions, Prompts, or
`copilot-instructions.md`. Hooks are **event orchestrators**: they load the
correct skills, activate the correct agents, and reference the correct
instructions/prompts, but never implement business logic themselves.

## Phase 1 — Repository discovery

Scan `.github` and verify `agents/`, `skills/`, `instructions/`, `prompts/`,
and `copilot-instructions.md` exist. If any required component is missing,
**stop** and report which are unavailable before generating hooks (reuse the
universal builder's discovery result if already performed this session; if
the skeleton itself is missing, defer to
[`../01-wrapper-structure-initializer.md`](../01-wrapper-structure-initializer.md)).

## Phase 2 — Analyze existing architecture

Read every agent (responsibilities, workflows), skill (reusable
capabilities, activation conditions), instruction (standards, conventions,
compliance rules), prompt (reusable workflows), and
`copilot-instructions.md` (root configuration).

## Phase 3 — Candidate trigger discovery

Brainstorm candidate triggers, then **classify each one against Part 1**
before treating it as a real hook:

| Candidate trigger | Valid as a Copilot hook event? | Correct mechanism |
|---|---|---|
| A tool call just completed (e.g. a file was edited) | Yes — matches `PostToolUse` | `.github/hooks/*.json` |
| A tool is about to run (e.g. before a shell command) | Plausible if VS Code documents a corresponding pre-event; confirm before use | `.github/hooks/*.json` (confirm event name first) |
| A specific file type was just modified by the agent | Yes, if expressed as a `PostToolUse` hook that filters by path in its stdin payload, not as a fabricated `file-modified` event name | `.github/hooks/*.json` |
| Branch created/switched/synced | No — this is a local Git/editor event, not a documented Copilot hook event | Out of scope for hooks; consider editor/Git tooling, not Copilot hooks |
| Pull request opened/updated/reviewed, issue created/closed, release started/completed | No — these are GitHub repository events | `.github/workflows/*.yml` (GitHub Actions) |
| Repository/workspace opened or indexed | Not confirmed as a documented hook event | Do not implement until confirmed against current vendor docs |

Do not carry over the original architecture generator's full list of ~28
"repository lifecycle events" (branch switched, PR opened, issue created,
release completed, etc.) as if they were native hook events — most of them
are GitHub repository events and belong to GitHub Actions workflows
instead. Only the subset that genuinely corresponds to an in-editor
tool-use lifecycle moment (confirmed against Part 1) may become a real
hook.

## Phase 4 — Generate the hooks folder

```text
.github/
  hooks/
    README.md
    format.json
    security-guardrail.json
    ...
```

Prefer one JSON file per concern (or a small number of well-named files),
each containing one or more entries under the appropriate event key inside
`"hooks"`. There is no vendor requirement for a "one directory per hook"
layout — that pattern is a planning convenience, not an execution
requirement.

## Phase 5 — Design note per hook (planning only, not executable)

Before writing the JSON, capture a short design note (in the hooks
`README.md`, a PR description, or scratch notes — not a file VS Code
executes) covering:

- **Purpose** — why this hook exists, business/engineering objective.
- **Trigger** — the confirmed real event (Part 1), e.g. `PostToolUse`.
- **Activation conditions** — when it should/shouldn't fire (e.g. filter by
  file path from the stdin payload).
- **Command** — the exact command VS Code will run.
- **Inputs consumed** — which stdin JSON fields the command reads, if any.
- **Outputs produced** — what, if anything, is written to stdout and how it
  influences the agent (e.g. blocking a tool call).
- **Related skills/agents/instructions/prompts** — if the command's
  behavior depends on repository conventions, name them for traceability.
- **Validation** — how to confirm the hook fired (e.g. Developer: Show
  Agent Debug Logs) and what a successful run looks like.

This design note is documentation to aid humans reviewing the change. **The
actual executable artifact is the JSON file conforming to Part 1** — do not
substitute a Markdown "HOOK.md" for the real JSON hook definition.

## Phase 6 — Dependency rules

```text
Confirmed hook event (Part 1)
        ↓
copilot-instructions.md
        ↓
Relevant instructions
        ↓
Relevant skills
        ↓
Relevant agents
        ↓
Relevant prompts
        ↓
Repository files
```

Never skip levels; load only the minimum required context; never reference
unrelated files.

## Phase 7 — Cross references

Each hook's design note should document: related skills, related agents,
related instructions, related prompts, related repository files, produced
outputs, and consumed inputs.

## Phase 8 — `hooks/README.md`

Cover: purpose of hooks, difference between hooks and skills, difference
between hooks and agents, difference between hooks and GitHub Actions
workflows (critical — see Part 1 "What hooks are not"), lifecycle,
architecture, execution flow, naming conventions, how hooks invoke
skills/activate agents, how to add new hooks, best practices.

## Phase 9 — Architecture diagram

```text
Confirmed agent-lifecycle event (e.g. PostToolUse)
        │
        ▼
copilot-instructions.md
        │
        ▼
     Instructions
        │
        ▼
        Skills
        │
        ▼
        Agents
        │
        ▼
       Prompts
        │
        ▼
 Repository Changes
```

## Phase 10 — Naming convention

Lowercase, kebab-case filenames (e.g. `security-guardrail.json`,
`post-edit-format.json`). Avoid spaces and unestablished abbreviations.

## Phase 11 — Quality standards

Every hook should be: reusable, event-driven (using a confirmed real
event), lightweight, independent, well documented, cross-referenced, easy to
extend, enterprise-ready, and strictly an orchestrator — never containing
business logic itself (the invoked command/skill/agent does the real work).

## Output requirements

Generate only new files inside `.github/hooks/`. Do not regenerate existing
agents, skills, instructions, or prompts. Do not modify
`copilot-instructions.md` as part of this procedure — that belongs to
[`../03-build-linking-compiler.md`](../03-build-linking-compiler.md).

## Reconciliation note (Part 1 vs. Part 2)

The original architecture generator's "Recommended Enterprise Hooks" list
(branch created/switched/synced, PR opened/updated/reviewed, issue
created/assigned/closed, release started/completed, repository
opened/indexed, etc.) describes **GitHub repository and editor-session
events, most of which are not documented Copilot hook events**. Treat that
list as raw material for **GitHub Actions workflow triggers**
(`on: pull_request`, `on: issues`, `on: push`, etc. — see "Generate or Reuse
GitHub Actions Workflows" in the universal builder) rather than as Copilot
hook events. Only bring an item from that list into `.github/hooks/*.json`
if it can be honestly expressed using a real, confirmed hook event from
Part 1 (currently: `PostToolUse`, and any other event VS Code documentation
confirms at build time).

## Checklist for the builder

- [ ] Every hook event name used is confirmed against current VS Code hook
      documentation — none are invented.
- [ ] The executable artifact is a valid `.github/hooks/*.json` file
      matching Part 1's `{ "hooks": { "<Event>": [ { "type": "command",
      "command": "..." } ] } }` shape.
- [ ] Any Markdown design note is clearly non-executable planning content,
      not presented as the hook itself.
- [ ] Repository-level events (PR, issue, branch, release) were routed to
      GitHub Actions workflows, not fabricated as hook events.
- [ ] The command invoked is reviewed for security (no destructive
      commands run unreviewed; matches Security Controls in
      [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)).
- [ ] Hook execution was validated via Developer: Show Agent Debug Logs (or
      equivalent) before being reported as working.

## Consumed by

- [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md) — "Generate or Reuse Hooks" and "Capability Classification" sections.
- [`../03-build-linking-compiler.md`](../03-build-linking-compiler.md) — "Relationship rules by component / F. Hooks".
