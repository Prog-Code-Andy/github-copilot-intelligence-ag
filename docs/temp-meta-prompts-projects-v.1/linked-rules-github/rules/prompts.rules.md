# Prompts — Vendor Rules

## Purpose

Authoritative technical specification for `.prompt.md` reusable prompt
files, sourced from official VS Code / GitHub Copilot documentation
(`temp-files-skills/prompts-v1.128.md`). This file is consulted by
[`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)
(section "Generate or Reuse Prompts") before creating or modifying any
`.github/prompts/*.prompt.md` file.

---

## File format

Prompt files are Markdown files with the `.prompt.md` extension and an
optional YAML frontmatter header.

Location:

```text
.github/prompts/<name>.prompt.md
```

## Frontmatter fields

| Field | Required | Description |
|---|---|---|
| `description` | No | A short description of the prompt. |
| `name` | No | The name used after typing `/` in chat. Defaults to the file name if omitted. |
| `argument-hint` | No | Hint text shown in the chat input field to guide users on how to interact with the prompt. |
| `agent` | No | The agent used to run the prompt: `ask`, `agent`, `plan`, or the name of a custom agent. Defaults to the currently selected agent. If `tools` is specified without `agent`, the default becomes `agent`. |
| `model` | No | The language model used when running the prompt. Defaults to the currently selected model in the model picker. |
| `tools` | No | A list of tool or toolset names available for this prompt. Can include built-in tools, toolsets, MCP tools, or extension-contributed tools. Use `<server name>/*` to include all tools of an MCP server. If a listed tool is unavailable when the prompt runs, it is silently ignored. |

## Body content rules

- The body is the prompt text in Markdown.
- Reference other workspace files using Markdown links with **relative
  paths**, correct relative to the prompt file's location.
- Reference agent tools in the body using the `#tool:<tool-name>` syntax
  (for example, `#tool:browser`).
- Existing prompt files can be edited through the Agent Customizations
  editor in VS Code, not only as raw Markdown.

## Authoring checklist (vendor-recommended steps)

1. Author the body using Markdown formatting.
2. Fill in the frontmatter to configure `description`, `agent`, `tools`, and
   other settings relevant to this prompt.
3. Add clear, step-by-step instructions in the body.

## Checklist for the builder

- [ ] File is located at `.github/prompts/<name>.prompt.md`.
- [ ] `description` is present and explains the reusable task.
- [ ] `agent` is set explicitly when the prompt should run under a specific
      custom agent (see [`agents.rules.md`](./agents.rules.md)), rather than
      relying on "whatever agent happens to be selected".
- [ ] `tools` lists only what the prompt genuinely needs (least privilege) —
      note that unavailable tools are silently ignored, not an error, so
      don't rely on a missing tool to fail loudly.
- [ ] Required project references (requirements, architecture, plans,
      security docs) are linked with correct relative Markdown paths, not
      hard-coded absolute paths.
- [ ] Any `#tool:<tool-name>` reference in the body corresponds to a tool
      actually declared in `tools` or available by default.
- [ ] The prompt states its approval rules for irreversible or destructive
      actions (matching the Security Controls in
      [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md)).

## Consumed by

- [`../02-universal-meta-prompt-builder.md`](../02-universal-meta-prompt-builder.md) — "Generate or Reuse Prompts" and "Capability Classification" sections.
- [`../03-build-linking-compiler.md`](../03-build-linking-compiler.md) — "Relationship rules by component / D. Prompt files".
