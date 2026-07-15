# Agents — Vendor Rules

## Purpose

Authoritative technical specification for `.agent.md` custom agent files,
sourced from official VS Code / GitHub Copilot documentation
(`temp-files-skills/custom-agents-v1.128.md`). This file is consulted by
[`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)
(section "Generate or Modernize the Agent") before creating or modifying any
`.github/agents/*.agent.md` file. It defines the binding format; the builder
defines the workflow around when and why to create one.

---

## What a custom agent is

Custom agents provide a tailored chat configuration: a bundle of
instructions, tools, and model settings applied whenever that agent is
selected. Unlike the built-in general-purpose agents, a custom agent lets a
user (or a subagent invocation) switch to a specific, repeatable
configuration instead of manually assembling tools and instructions each
time.

- Defined in a `.agent.md` Markdown file.
- Can live in the workspace (shared with collaborators via the repo) or in
  the user profile (reused across workspaces, personal only).
- Reusable in background agents and cloud agents — the same specialized
  configuration can run autonomously, not just interactively.

## File location

```text
.github/agents/<agent-name>.agent.md
```

Workspace-scoped agents belong here so they are shared through source
control. User-profile agents live outside the repository and are out of
scope for repository-generated capability packages.

## Frontmatter fields (documented)

| Field | Required | Default | Description |
|---|---|---|---|
| `name` | Recommended | filename-derived | Identifier used to select the agent. |
| `tools` | No | inherited | Tools available to the agent. Apply least privilege. |
| `model` | No | inherited from session | The model this agent (or subagent invocation) should use. |
| `user-invocable` | No | `true` | Controls whether the agent appears in the agents dropdown in chat. Set to `false` to make an agent reachable only as a subagent. |
| `disable-model-invocation` | No | `false` | Prevents the agent from being selected automatically as a subagent by other agents. Set to `true` when an agent must only be triggered explicitly by a user. |
| `agents` (Experimental) | No | `*` (all) | Restricts which custom agents this agent may use as subagents. Accepts a list of agent names, `*` for all, or `[]` to disallow any subagent use. |
| `infer` | No | — | **Deprecated.** Use `user-invocable` and `disable-model-invocation` instead. |

## Subagent invocation model

- By default, a subagent inherits the parent agent's model and tools.
- A custom agent used as a subagent can override the inherited model, tools,
  and instructions via its own frontmatter.
- The parent agent can also request a specific model when invoking a
  subagent.
- To run a custom agent as a subagent, the parent simply instructs the AI to
  use that named agent for the subtask (for example: "Run the Research agent
  as a subagent to research X").

## Restricting subagents (Experimental)

- Without restriction, every custom agent that does not set
  `disable-model-invocation: true` is eligible to be auto-selected as a
  subagent — if multiple agents have similar names/descriptions, the wrong
  one can be picked.
- Use the `agents` frontmatter property on the **parent** agent to constrain
  this: a list of allowed agent names, `*` (default, all allowed), or `[]`
  (no subagent use at all).
- Explicitly listing an agent in a parent's `agents` array overrides that
  agent's own `disable-model-invocation: true` — this is the supported
  mechanism for "protected except for one specific coordinator" agents (for
  example, a TDD orchestrator that may only ever call Red/Green/Refactor
  agents, never a generic coding agent).

## Common pitfalls (from vendor documentation)

- Do not use the deprecated `infer` property in newly generated agents;
  always use `user-invocable` + `disable-model-invocation`.
- Do not assume an agent is hidden from autonomous subagent selection just
  because it is hidden from the dropdown (`user-invocable: false` only
  affects the dropdown; use `disable-model-invocation: true` to also block
  subagent auto-selection).
- When several agents have overlapping names or descriptions, prefer
  explicit `agents` restriction lists on coordinator/orchestrator agents
  over relying on the model to disambiguate.

## Checklist for the builder

Before finalizing a generated `.agent.md` file, confirm:

- [ ] File is located at `.github/agents/<agent-name>.agent.md`.
- [ ] `name` is set and matches the intended selector.
- [ ] `tools` reflects least privilege (see Security Controls in
      [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)).
- [ ] `user-invocable` / `disable-model-invocation` are set deliberately, not
      left to defaults when the agent is subagent-only or user-only.
- [ ] `infer` is not used.
- [ ] If this agent orchestrates other agents as subagents, the `agents`
      restriction list is set explicitly rather than left at `*` when
      ambiguity risk exists.
- [ ] The body stays concise: identity, mission, responsibilities, workflow,
      approval gates — not a dumping ground for standards (those belong in
      [`instructions.rules.md`](./instructions.rules.md)) or procedures
      (those belong in [`skills.rules.md`](./skills.rules.md)).

## Consumed by

- [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md) — "Generate or Modernize the Agent" and "Capability Classification" sections.
- [`../03-build-linking-compiler.md`](../03-build-linking-compiler.md) — "Relationship rules by component / B. Custom agents".
