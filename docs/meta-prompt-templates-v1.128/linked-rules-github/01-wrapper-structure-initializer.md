# Wrapper Structure Initializer

## Position in pipeline

```text
Step 1 of 3 — Wrapper Structure Initializer   ◄── you are here
Step 2 of 3 — Universal Meta-Prompt Builder       (02-universal-meta-prompt-builder.md)
Step 3 of 3 — Build-Linking Compiler              (03-build-linking-compiler.md)
```

This file always runs **first**. Its only job is to guarantee that the base
`.github` skeleton and root governance files exist before any agent,
instruction, prompt, skill, hook, or workflow is generated.

- **Input:** the current repository state (may be empty, partially set up, or already initialized).
- **Output:** the base directory structure and governance files listed below.
- **Hands off to:** [`02-universal-meta-prompt-builder.md`](./02-universal-meta-prompt-builder.md), which performs discovery again at a deeper level (per-file, per-component) and then generates the requested capability package. Step 2 assumes this step has already run, but it must not fail silently if a directory is still missing — it should re-run the relevant check from this file before proceeding.
- **Does not** create agents, instructions, prompts, skills, hooks, or workflow implementation files. That responsibility belongs entirely to Step 2. This file creates structure only.

Source of this file: adapted from `main-meta-prompts/create-repo-structure.md`, kept behaviorally identical, with pipeline framing added.

---

## Role

You are a senior GitHub repository configuration engineer.

## Task

Initialize the base `.github` folder structure for this repository.

This task creates only:

- the required directories
- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/CODEOWNERS`
- `.github/dependabot.yml`
- `.github/copilot-instructions.md`
- `AGENTS.md` at the repository root

Do not create implementation files inside the customization directories.

---

## Objective

Create the following structure:

```text
AGENTS.md
.github/
├── workflows/
├── agents/
├── instructions/
├── prompts/
├── skills/
├── hooks/
│   └── scripts/
├── ISSUE_TEMPLATE/
├── PULL_REQUEST_TEMPLATE.md
├── CODEOWNERS
├── dependabot.yml
└── copilot-instructions.md
```

`AGENTS.md` lives at the repository root, alongside the `.github` folder, not inside it. VS Code automatically detects a root-level `AGENTS.md` file and applies its instructions to all chat requests in the workspace, provided the `chat.useAgentsMdFile` setting is enabled (default). This makes it the right place for a single, agent-agnostic set of instructions recognized by GitHub Copilot and other AI coding agents that support the `AGENTS.md` convention.

The directories must be prepared for future implementation, but their Copilot customization files must not be generated during this task.

---

## Mandatory restrictions

Do not create:

- workflow YAML files inside `.github/workflows/`
- `*.agent.md` files inside `.github/agents/`
- `*.instructions.md` files inside `.github/instructions/`
- `*.prompt.md` files inside `.github/prompts/`
- skill directories or `SKILL.md` files inside `.github/skills/`
- `hooks.json` or executable scripts inside `.github/hooks/`
- issue-template YAML or Markdown files inside `.github/ISSUE_TEMPLATE/`
- sample agents, prompts, instructions, hooks, skills, or workflows
- placeholder implementation content
- files outside `.github/`, except the single root-level `AGENTS.md` file explicitly required by this task
- nested or subfolder `AGENTS.md` files (these are only created by a separate, explicitly requested monorepo task)
- duplicate files when an existing file is already present

Do not modify application source code, tests, configuration, or documentation outside `.github/`.

---

## Existing repository protection

Before creating or modifying anything:

1. Inspect the existing `.github` directory.
2. Identify existing folders and files.
3. Do not overwrite existing files without reviewing them.
4. Preserve valid existing configuration.
5. If one of the required files already exists:
   - review its current content;
   - retain useful repository-specific configuration;
   - add only missing sections;
   - report what was preserved and what was changed.
6. Do not remove existing workflows, agents, skills, prompts, instructions, hooks, or issue templates.

Use minimal and targeted changes.

---

## Empty-directory handling

Git does not track empty directories.

To preserve the empty directory structure in Git, create a `.gitkeep` file only in directories that would otherwise be empty:

- `.github/workflows/.gitkeep`
- `.github/agents/.gitkeep`
- `.github/instructions/.gitkeep`
- `.github/prompts/.gitkeep`
- `.github/skills/.gitkeep`
- `.github/hooks/scripts/.gitkeep`
- `.github/ISSUE_TEMPLATE/.gitkeep`

A `.gitkeep` file must contain only:

```text
Reserved for future repository configuration.
```

Do not create `.gitkeep` when the directory already contains files.

`.gitkeep` is the only file permitted inside the empty customization directories during this task.

---

## File requirements

### 1. `.github/PULL_REQUEST_TEMPLATE.md`

Create a reusable pull request template with these sections:

- `## Summary`
  - `<!-- Clearly explain what this pull request changes and why. -->`
- `## Change type`
  - `- [ ] Documentation`
  - `- [ ] GitHub Copilot customization`
  - `- [ ] Agent`
  - `- [ ] Instruction`
  - `- [ ] Prompt`
  - `- [ ] Skill`
  - `- [ ] Hook`
  - `- [ ] GitHub Actions workflow`
  - `- [ ] Automation`
  - `- [ ] Security`
  - `- [ ] Bug fix`
  - `- [ ] Maintenance`
- `## Related issue`
  - `<!-- Example: Closes #123 -->`
- `## Changes made`
  - `<!-- List the important changes included in this pull request. -->`
- `## Validation performed`
  - `- [ ] Files were reviewed locally`
  - `- [ ] Markdown, YAML, or JSON syntax was validated`
  - `- [ ] No secrets or sensitive information were added`
  - `- [ ] Relevant tests or validation commands passed`
  - `- [ ] Documentation was updated if necessary`
- `## GitHub Copilot impact`
  - `- [ ] No Copilot customization impact`
  - `- [ ] Repository instructions changed`
  - `- [ ] Agent behavior changed`
  - `- [ ] Prompt behavior changed`
  - `- [ ] Skill behavior changed`
  - `- [ ] Hook behavior changed`
  - `- [ ] Tool or permission scope changed`
- `## Security review`
  - `- [ ] No credentials, tokens, certificates, or private URLs are included`
  - `- [ ] Workflow permissions follow least privilege`
  - `- [ ] External actions or dependencies are trusted and pinned appropriately`
  - `- [ ] Scripts do not execute untrusted external content`
  - `- [ ] Changes do not expose enterprise or repository-sensitive information`
- `## Screenshots or evidence`
  - `<!-- Add screenshots, logs, generated reports, or other validation evidence when relevant. -->`
- `## Reviewer notes`
  - `<!-- Highlight important decisions, risks, limitations, or follow-up work. -->`

Keep the language professional and suitable for documentation, automation, and GitHub Copilot customization work.

---

### 2. `.github/CODEOWNERS`

Create a conservative starter configuration.

Use a clearly marked placeholder rather than inventing usernames or teams:

```text
# Replace @repository-owner with the correct GitHub user or team.
# Team example: @organization/platform-engineering
* @repository-owner
# GitHub governance and automation
/.github/ @repository-owner
# Sensitive GitHub configuration
/.github/workflows/ @repository-owner
/.github/hooks/ @repository-owner
/.github/CODEOWNERS @repository-owner
/.github/dependabot.yml @repository-owner
# GitHub Copilot customizations
/.github/agents/ @repository-owner
/.github/instructions/ @repository-owner
/.github/prompts/ @repository-owner
/.github/skills/ @repository-owner
/.github/copilot-instructions.md @repository-owner
```

Requirements:

- Do not invent an organization, team, or username.
- Include a comment explaining that the placeholder must be replaced.
- Apply explicit ownership to workflows, hooks, Copilot customizations, and governance files.
- Keep the configuration easy to update later.

---

### 3. `.github/dependabot.yml`

Create a valid Dependabot configuration.

Initially configure GitHub Actions dependency updates:

```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "monday"
      time: "09:00"
      timezone: "America/Toronto"
    open-pull-requests-limit: 5
    labels:
      - "dependencies"
      - "github-actions"
    commit-message:
      prefix: "chore"
      include: "scope"
```

Before adding another package ecosystem:

1. Inspect the repository.
2. Add an ecosystem only when its manifest already exists.
3. Examples:
   - `pip` for `requirements.txt`, `pyproject.toml`, or `Pipfile`
   - `npm` for `package.json`
   - `docker` for supported Docker manifests
   - `maven` for `pom.xml`
   - `gradle` for Gradle build files
4. Do not guess which package manager the repository uses.
5. Do not add unsupported or unused ecosystems.

For each detected ecosystem:

- use weekly scheduling;
- use the America/Toronto timezone;
- limit open pull requests;
- apply relevant dependency labels;
- use a conventional `chore` commit-message prefix.

The resulting YAML must be syntactically valid.

---

### 4. `.github/copilot-instructions.md`

Create repository-wide GitHub Copilot instructions with the following content and principles:

# GitHub Copilot Repository Instructions

## Repository purpose

This repository tracks and evaluates GitHub Copilot and development-environment changes.
It maintains reviewed documentation, automation, and reusable customization patterns for:

- custom agents;
- repository and path-specific instructions;
- prompt files;
- agent skills;
- hooks;
- MCP integrations;
- GitHub Actions;
- development-environment configuration;
- secure AI-assisted development workflows.

## General operating rules

1. Inspect the repository before proposing changes.
2. Reuse existing patterns before creating new structures.
3. Make minimal and focused changes.
4. Do not create unrelated files.
5. Do not duplicate guidance across agents, instructions, prompts, skills, or hooks.
6. Clearly distinguish verified facts from recommendations or assumptions.
7. Preserve existing repository-specific configuration unless a change is necessary.
8. Do not modify the protected `main` branch directly.
9. Use a dedicated branch and pull request for meaningful changes.
10. Include validation evidence with implementation changes.

## Source priority

When researching GitHub Copilot functionality, use this priority:

1. Official GitHub documentation.
2. Official GitHub Changelog announcements.
3. Official Visual Studio Code release notes.
4. Official GitHub or Microsoft repositories.
5. Approved community repositories.
6. Other community sources for discovery only.

Do not present community examples as official GitHub functionality.
Record source URLs, publication dates, product surfaces, and release status when documenting external changes.

## Product-surface validation

Do not assume a capability is available everywhere.
Identify the applicable surface:

- Visual Studio Code;
- GitHub.com;
- GitHub Copilot coding agent;
- GitHub Copilot CLI;
- JetBrains IDEs;
- Visual Studio;
- GitHub Mobile;
- enterprise-managed environments.

Identify the release status:

- experimental;
- preview;
- public preview;
- generally available;
- deprecated;
- retired.

Do not classify preview functionality as production-ready without an explicit review.

## Customization selection rules

Use the appropriate customization type:

- `.github/copilot-instructions.md` for repository-wide rules;
- `.github/instructions/*.instructions.md` for path-specific or technology-specific rules;
- `.github/prompts/*.prompt.md` for reusable user-invoked tasks;
- `.github/agents/*.agent.md` for specialized roles and end-to-end workflows;
- `.github/skills/` for reusable procedural capabilities with supporting resources;
- `.github/hooks/` for deterministic lifecycle commands and policy enforcement;
- `.github/workflows/` for repository automation and CI/CD.

Do not place all behavior into one large custom agent.
Prefer small, composable, clearly owned customizations.

## File-creation policy

Do not create agents, skills, prompts, instructions, hooks, workflows, or issue templates unless the current task explicitly requires them.
When creating a new customization:

1. Explain why that customization type is appropriate.
2. Check whether an existing file can be reused.
3. Define its responsibility and boundaries.
4. Avoid hard-coded repository paths when discovery is possible.
5. Add validation criteria.
6. Document required tools and permissions.
7. Include security considerations.

## Security requirements

1. Never commit passwords, tokens, API keys, certificates, private keys, cookies, or connection strings.
2. Never include sensitive enterprise URLs, infrastructure names, or internal identifiers in public examples.
3. Use GitHub Secrets or approved secret-management systems.
4. Apply least-privilege permissions to workflows, agents, MCP servers, and tools.
5. Treat hooks and skill scripts as executable code requiring review.
6. Do not execute code from an untrusted external repository.
7. Review external actions and dependencies before adoption.
8. Pin security-sensitive dependencies and GitHub Actions where required by repository policy.
9. Validate generated shell commands before execution.
10. Do not expose private source code or confidential information in prompts.

## Git and pull-request rules

Use descriptive branch names:

- `docs/<scope>-<purpose>`
- `feat/<scope>-<purpose>`
- `fix/<scope>-<purpose>`
- `research/<scope>-<purpose>`
- `automation/<scope>-<purpose>`

Use conventional, focused commit messages where practical:

- `docs: document Copilot release changes`
- `feat: add release-analysis agent`
- `automation: add scheduled update monitor`
- `fix: prevent duplicate release reports`

Before proposing a pull request:

1. Review the diff.
2. Validate changed Markdown, YAML, JSON, scripts, or code.
3. Confirm no secrets are present.
4. Confirm unrelated files were not changed.
5. Document tests and validation.
6. Identify security or compatibility risks.

## Automation rules

Automation should follow this lifecycle:

```text
Collect → Normalize → Compare → Report → Human review → Pull request → Approval
```

Scheduled monitoring may generate:

- normalized records;
- reports;
- issues;
- draft pull requests.

It must not silently approve its own output or merge directly into the protected default branch.

Use deterministic collection and validation before AI-assisted analysis.

Prevent duplicate reports by storing state such as:

- source identifiers;
- release versions;
- commit SHAs;
- publication timestamps;
- content hashes.

## Documentation standards

Documentation must include, when relevant:

- purpose;
- authoritative sources;
- applicable product surface;
- release status;
- architecture or workflow;
- exact implementation steps;
- security considerations;
- validation steps;
- limitations;
- rollback or removal guidance.

Use clear headings, short paragraphs, tables, examples, and diagrams where they improve understanding.

Do not copy large sections of external documentation. Summarize and cite the authoritative source.

## Relationship to AGENTS.md

This repository also maintains a root-level `AGENTS.md` file. `AGENTS.md` holds the concise, agent-agnostic rules that should apply regardless of which AI coding agent is used. `.github/copilot-instructions.md` holds the extended, GitHub Copilot-specific detail.

Do not duplicate the full content of one file into the other. When a rule changes, update it in exactly one place and reference it from the other if needed.

## Validation requirements

After making changes:

1. Review the generated file tree.
2. Validate Markdown structure.
3. Validate YAML and JSON syntax.
4. Check shell scripts for safe quoting and error handling.
5. Run available tests or repository validation scripts.
6. Check for accidentally committed secrets.
7. Report:
   - files created;
   - files modified;
   - files intentionally not created;
   - validations performed;
   - unresolved warnings.

## Current initialization boundary

The initial repository setup creates only:

- base `.github` directories;
- `.github/PULL_REQUEST_TEMPLATE.md`;
- `.github/CODEOWNERS`;
- `.github/dependabot.yml`;
- `.github/copilot-instructions.md`;
- root-level `AGENTS.md`;
- `.gitkeep` files required to preserve otherwise-empty directories.

Do not generate agents, instructions, prompts, skills, hooks, workflows, issue templates, or nested `AGENTS.md` files until a separate task explicitly requests them.

---

### 5. `AGENTS.md` (repository root)

Create a root-level `AGENTS.md` file, following the [VS Code AGENTS.md convention](https://code.visualstudio.com/docs/agent-customization/custom-instructions#_use-an-agentsmd-file).

Requirements:

- Place the file at the repository root, never inside `.github/`.
- Keep it agent-agnostic: write rules that any AI coding agent supporting `AGENTS.md` can follow, not only GitHub Copilot.
- Keep it concise. Do not duplicate the full `.github/copilot-instructions.md` content; summarize the shared rules and cross-reference the detailed file for Copilot-specific guidance.
- Include, at minimum:
  - `# AGENTS.md`
  - `## Repository purpose` — one or two sentences, consistent with `.github/copilot-instructions.md`.
  - `## General rules` — the essential subset: inspect before changing, make minimal focused changes, do not duplicate guidance, preserve existing configuration, do not modify `main` directly, use a branch and pull request.
  - `## Security rules` — never commit secrets, use least-privilege permissions, review external actions and scripts before use.
  - `## Git and pull-request conventions` — the same branch-naming and commit-message conventions used in `.github/copilot-instructions.md`.
  - `## Where to find more` — a pointer to `.github/copilot-instructions.md` for repository-wide Copilot instructions, `.github/instructions/` for path-specific rules, `.github/prompts/` for reusable tasks, `.github/agents/` for specialized agents, and `.github/skills/` for procedural capabilities.
- Do not create nested or subfolder `AGENTS.md` files during this task. Nested `AGENTS.md` files (for monorepo-style, folder-specific instructions) require the experimental `chat.useNestedAgentsMdFiles` setting and must only be added through a separate, explicitly requested task.
- Mention, as a follow-up note (not a file to create), that `AGENTS.md` support depends on the `chat.useAgentsMdFile` setting being enabled in VS Code (enabled by default).

---

## Execution workflow

Follow these steps:

1. Inspect the repository root.
2. Inspect the existing `.github` folder, when present.
3. Check whether a root-level `AGENTS.md` already exists; if it does, review and preserve its content instead of overwriting it.
4. Create only missing required directories.
5. Add `.gitkeep` only to directories that would otherwise remain empty.
6. Create or carefully update:
   - `.github/PULL_REQUEST_TEMPLATE.md`;
   - `.github/CODEOWNERS`;
   - `.github/dependabot.yml`;
   - `.github/copilot-instructions.md`;
   - `AGENTS.md` at the repository root.
7. Validate:
   - directory structure;
   - Markdown;
   - YAML syntax;
   - CODEOWNERS paths;
   - absence of secrets;
   - absence of unintended files;
   - no unintended duplication between `AGENTS.md` and `.github/copilot-instructions.md`.
8. Review the final Git diff.
9. Do not commit or push unless explicitly instructed.

---

## Required final response

Return a concise implementation report using this format:

```markdown
## `.github` initialization completed
### Directories created
- `.github/workflows/`
- `.github/agents/`
- `.github/instructions/`
- `.github/prompts/`
- `.github/skills/`
- `.github/hooks/scripts/`
- `.github/ISSUE_TEMPLATE/`
### Governance files created or updated
- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/CODEOWNERS`
- `.github/dependabot.yml`
- `.github/copilot-instructions.md`
- `AGENTS.md`
### Placeholder files
List any `.gitkeep` files added to preserve empty directories.
### Existing content preserved
List existing files that were reviewed and left unchanged.
### Validation
- [ ] Folder structure verified
- [ ] Markdown reviewed
- [ ] Dependabot YAML validated
- [ ] CODEOWNERS paths reviewed
- [ ] No secrets detected
- [ ] No agent, skill, prompt, instruction, hook, workflow, or issue-template implementation files created
- [ ] No unintended duplication between `AGENTS.md` and `.github/copilot-instructions.md`
### Follow-up required
- Replace `@repository-owner` in `.github/CODEOWNERS`.
- Confirm the `chat.useAgentsMdFile` setting is enabled if `AGENTS.md` instructions are not being picked up.
- Add implementation files only through separate reviewed tasks.
```

Do not claim that validation passed unless it was actually performed.

Expected result

```text
AGENTS.md
.github/
├── workflows/
│   └── .gitkeep
├── agents/
│   └── .gitkeep
├── instructions/
│   └── .gitkeep
├── prompts/
│   └── .gitkeep
├── skills/
│   └── .gitkeep
├── hooks/
│   └── scripts/
│       └── .gitkeep
├── ISSUE_TEMPLATE/
│   └── .gitkeep
├── PULL_REQUEST_TEMPLATE.md
├── CODEOWNERS
├── dependabot.yml
└── copilot-instructions.md
```

Best practices

Use this prompt in Plan mode first, so Copilot inspects the existing repository before creating files. Then run it in Agent mode after reviewing the plan.

The `.gitkeep` files are necessary because Git does not store empty directories. They do not implement agents, skills, hooks, workflows, or prompts; they only preserve the planned structure.

`AGENTS.md` is recognized by VS Code out of the box (`chat.useAgentsMdFile`) and is intended to hold the single, agent-agnostic rule set shared across AI coding agents. Nested `AGENTS.md` files per subfolder are an experimental, opt-in capability (`chat.useNestedAgentsMdFiles`) and are out of scope for this initial setup task.

---

## Next step

Once this structure exists (or is confirmed already present), proceed to
[`02-universal-meta-prompt-builder.md`](./02-universal-meta-prompt-builder.md)
to generate the requested agent, instructions, prompts, skills, or hooks.
