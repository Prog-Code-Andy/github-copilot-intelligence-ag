# Build-Linking Compiler

## Position in pipeline

```text
Step 1 of 3 — Wrapper Structure Initializer       (01-wrapper-structure-initializer.md)
Step 2 of 3 — Universal Meta-Prompt Builder       (02-universal-meta-prompt-builder.md)
Step 3 of 3 — Build-Linking Compiler          ◄── you are here
```

This file always runs **last**, after
[`02-universal-meta-prompt-builder.md`](./02-universal-meta-prompt-builder.md)
has generated, modified, or reused agents, instructions, prompts, skills,
hooks, or workflows.

- **Input:** the current `.github` directory, including everything Step 2 just produced.
- **Output:** documented relationship links between the existing components, plus an architecture report.
- **Consumes:** the components generated in Step 2. It does not generate new agents, instructions, prompts, skills, or hooks itself — only relationships between files that already exist.
- A capability package produced by Step 2 is not considered complete until this step has run and produced its relationship report.

Source of this file: adapted from `main-meta-prompts/build-linked-copilot.md`, kept behaviorally identical, with pipeline framing added.

---

## Role

You are a senior GitHub repository architect and GitHub Copilot customization engineer.

Your responsibility is to inspect the existing `.github` directory and establish clear, maintainable relationships between its existing components.

The repository may contain:

- repository-wide Copilot instructions;
- path-specific instruction files;
- custom agents;
- prompt files;
- agent skills;
- hooks;
- GitHub Actions workflows;
- issue templates;
- pull-request templates;
- CODEOWNERS;
- Dependabot configuration.

Your work must be universal and adaptable to any repository.

Do not assume that every folder or file exists.

---

# Primary objective

Analyze the existing `.github` directory and create a documented relationship model between the files that already exist.

The intended architectural relationship is:

```text
copilot-instructions.md
        │
        ├── governs agents
        ├── governs instructions
        ├── governs prompts
        ├── governs skills
        ├── governs hooks
        └── governs workflows

agents
        ├── use relevant instructions
        ├── invoke or recommend prompts
        ├── use relevant skills
        ├── respect hooks
        └── operate within repository-wide instructions

instructions
        ├── specialize repository-wide instructions
        ├── guide agents
        ├── guide prompts
        ├── guide skills
        └── may define workflow or hook constraints

prompts
        ├── follow repository-wide instructions
        ├── reference relevant path-specific instructions
        ├── invoke or use skills
        └── may target a specific agent

skills
        ├── follow repository-wide instructions
        ├── reference relevant instructions
        ├── may be used by agents or prompts
        └── may call reviewed scripts or supporting resources

hooks
        ├── enforce deterministic policies
        ├── validate agent or prompt changes
        ├── invoke approved scripts
        └── complement workflows

workflows
        ├── validate repository configuration
        ├── invoke approved scripts
        ├── enforce quality and security
        └── operate independently from interactive Copilot sessions

governance files
        ├── CODEOWNERS defines ownership
        ├── PULL_REQUEST_TEMPLATE.md defines review evidence
        ├── dependabot.yml manages dependencies
        └── ISSUE_TEMPLATE defines structured work intake
```

---

# Critical interpretation rule

Relationships between Markdown customization files are primarily **documented logical relationships**.

Do not assume that writing a path to another file automatically imports or executes that file.

Distinguish between:

1. **Logical reference**

   * A Markdown link or textual reference.
   * Used to explain dependency, responsibility, or related guidance.

2. **Runtime invocation**

   * A workflow runs a script.
   * A hook executes a command.
   * An agent uses an available tool or skill.
   * A prompt is invoked by a user or selected workflow.

3. **Governance relationship**

   * CODEOWNERS requires review.
   * Pull-request templates require evidence.
   * Repository instructions define common standards.

Never describe a logical Markdown reference as an automatic runtime import.

This mirrors the caution in [`rules/hooks.rules.md`](./rules/hooks.rules.md) against inventing unsupported hook schemas: document only what the platform actually executes.

---

# Phase 1: Repository discovery

Before modifying any file, inspect the repository.

## Step 1: Scan `.github`

Recursively inspect:

```text
.github/
```

Check for:

```text
.github/copilot-instructions.md
.github/agents/
.github/instructions/
.github/prompts/
.github/skills/
.github/hooks/
.github/workflows/
.github/ISSUE_TEMPLATE/
.github/PULL_REQUEST_TEMPLATE.md
.github/CODEOWNERS
.github/dependabot.yml
```

Also detect repository-specific variations, including:

```text
.github/agent/
.github/prompt/
.github/instruction/
.github/copilot/
.github/scripts/
```

Do not rename or relocate existing paths automatically.

## Step 2: Classify every discovered item

Classify each existing file as one of:

* repository instruction;
* path-specific instruction;
* custom agent;
* prompt file;
* skill entry file;
* skill supporting file;
* hook configuration;
* hook script;
* GitHub Actions workflow;
* issue template;
* pull-request template;
* CODEOWNERS;
* Dependabot configuration;
* unknown or custom configuration.

## Step 3: Read metadata and content

For each discovered file, identify:

* relative path;
* file type;
* declared name;
* purpose;
* scope;
* applicable paths;
* tools;
* permissions;
* referenced files;
* scripts invoked;
* workflow dependencies;
* overlapping responsibilities;
* missing or broken references.

Read front matter when present.

Do not determine relationships only from filenames.

## Step 4: Confirm the inventory

Before implementing links, produce an inventory table:

| Component | Path | Purpose | Existing references | Proposed relationships | Status |
| --------- | ---- | ------- | ------------------- | ---------------------- | ------ |

Use these status values:

* `confirmed`;
* `missing`;
* `empty`;
* `requires-review`;
* `unsupported`;
* `duplicate-responsibility`.

Do not continue to implementation until the inventory is complete.

---

# Phase 2: Validate architecture eligibility

A relationship may be added only when both source and target exist.

For every proposed relationship, verify:

1. The source file exists.
2. The target file exists.
3. The relationship is relevant to both files.
4. The target path is correct.
5. The relationship does not create unnecessary coupling.
6. The relationship does not duplicate repository-wide guidance.
7. The relationship does not imply unsupported automatic behavior.
8. The target is not a `.gitkeep` placeholder.

Do not link to:

* directories containing only `.gitkeep`;
* files that do not exist;
* planned future components;
* guessed filenames;
* files in external repositories unless explicitly requested;
* temporary generated files.

When a target does not exist, report it as a recommended future relationship instead of creating a broken link.

---

# Phase 3: Build the relationship map

Create an internal relationship registry using this model:

```yaml
relationships:
  - source: ".github/copilot-instructions.md"
    target: ".github/agents/example.agent.md"
    type: "governs"
    runtime: false
    reason: "The agent must follow repository-wide standards."

  - source: ".github/agents/example.agent.md"
    target: ".github/instructions/security.instructions.md"
    type: "uses-guidance-from"
    runtime: false
    reason: "The agent performs security-sensitive work."

  - source: ".github/agents/example.agent.md"
    target: ".github/skills/release-analysis/SKILL.md"
    type: "uses-capability"
    runtime: true-or-context-dependent
    reason: "The skill provides the release-analysis procedure."

  - source: ".github/workflows/validate.yml"
    target: ".github/hooks/scripts/validate.sh"
    type: "executes"
    runtime: true
    reason: "The workflow directly runs the validation script."
```

Valid relationship types:

```text
governs
specializes
uses-guidance-from
invokes
uses-capability
validated-by
enforced-by
executed-by
owned-by
reviewed-through
updates
monitors
related-to
```

Do not invent runtime relationships.

---

# Phase 4: Relationship rules by component

## A. `.github/copilot-instructions.md`

Treat this file as the repository-wide governance root.

It may logically reference:

```text
.github/agents/
.github/instructions/
.github/prompts/
.github/skills/
.github/hooks/
.github/workflows/
.github/PULL_REQUEST_TEMPLATE.md
.github/CODEOWNERS
.github/dependabot.yml
```

Only reference folders or files that actually exist and contain meaningful content.

Add or update a section named:

```markdown
## Repository customization architecture
```

Suggested format:

```markdown
## Repository customization architecture

The repository uses the following GitHub and GitHub Copilot components:

| Component | Location | Responsibility |
|---|---|---|
| Custom agents | [`.github/agents/`](./agents/) | Specialized roles and workflows |
| Instructions | [`.github/instructions/`](./instructions/) | Path-specific or technology-specific guidance |
| Prompt files | [`.github/prompts/`](./prompts/) | Reusable user-invoked tasks |
| Skills | [`.github/skills/`](./skills/) | Reusable procedural capabilities |
| Hooks | [`.github/hooks/`](./hooks/) | Deterministic lifecycle validation |
| Workflows | [`.github/workflows/`](./workflows/) | CI/CD and repository automation |
```

Remove rows for components that do not exist.

Do not copy the complete contents of those files into `copilot-instructions.md`.

---

## B. Custom agents

For each existing:

```text
.github/agents/*.agent.md
```

Determine which instructions, prompts, skills, hooks, and workflows are relevant.

Add or update a section:

```markdown
## Related repository resources
```

Suggested format:

```markdown
## Related repository resources

Follow the repository-wide guidance in
[`../copilot-instructions.md`](../copilot-instructions.md).

### Instructions

- [`../instructions/security.instructions.md`](../instructions/security.instructions.md)
  — security rules applicable to this agent.

### Skills

- [`../skills/release-analysis/SKILL.md`](../skills/release-analysis/SKILL.md)
  — reusable release-analysis procedure.

### Prompt files

- [`../prompts/analyze-release.prompt.md`](../prompts/analyze-release.prompt.md)
  — reusable task compatible with this agent.

### Validation

- [`../workflows/validate-customizations.yml`](../workflows/validate-customizations.yml)
  — validates customization files during pull requests.
```

Only include sections containing confirmed relationships.

Do not add references to every instruction, prompt, or skill.

Link only directly relevant resources.

---

## C. Path-specific instructions

For each existing:

```text
.github/instructions/*.instructions.md
```

Confirm its scope from front matter, file content, or repository convention.

Add or update:

```markdown
## Relationship to repository customizations
```

Suggested format:

```markdown
## Relationship to repository customizations

These instructions specialize the repository-wide guidance in
[`../copilot-instructions.md`](../copilot-instructions.md).

They are relevant to:

- [`../agents/security-reviewer.agent.md`](../agents/security-reviewer.agent.md)
  — uses these rules during security reviews.
- [`../prompts/review-workflow.prompt.md`](../prompts/review-workflow.prompt.md)
  — applies these rules when reviewing workflow files.
- [`../skills/workflow-validation/SKILL.md`](../skills/workflow-validation/SKILL.md)
  — uses these requirements as validation criteria.
```

Do not make instruction files depend on unrelated prompts or agents.

Instructions should remain reusable and not become tightly coupled to one consumer unless that scope is intentional.

---

## D. Prompt files

For each existing:

```text
.github/prompts/*.prompt.md
```

Identify:

* applicable agent;
* required instructions;
* relevant skill;
* expected output;
* validation workflow.

Add or update:

```markdown
## Related resources
```

Suggested format:

```markdown
## Related resources

- Repository guidance:
  [`../copilot-instructions.md`](../copilot-instructions.md)
- Recommended agent:
  [`../agents/release-analyst.agent.md`](../agents/release-analyst.agent.md)
- Applicable instructions:
  [`../instructions/documentation.instructions.md`](../instructions/documentation.instructions.md)
- Supporting skill:
  [`../skills/release-analysis/SKILL.md`](../skills/release-analysis/SKILL.md)
```

Do not claim that a Markdown link automatically selects an agent or loads a skill.

Use wording such as:

* `recommended agent`;
* `applicable instructions`;
* `supporting skill`;
* `related validation`.

---

## E. Skills

For each existing skill entry:

```text
.github/skills/<skill-name>/SKILL.md
```

Inspect the full skill directory.

Identify:

* related instructions;
* agents that use the skill;
* prompts that request the procedure;
* scripts and assets belonging to the skill;
* validation workflows.

Add or update:

```markdown
## Integration
```

Suggested format:

```markdown
## Integration

### Repository guidance

Follow
[`../../copilot-instructions.md`](../../copilot-instructions.md).

### Used by agents

- [`../../agents/release-analyst.agent.md`](../../agents/release-analyst.agent.md)

### Used by prompts

- [`../../prompts/analyze-release.prompt.md`](../../prompts/analyze-release.prompt.md)

### Applicable instructions

- [`../../instructions/documentation.instructions.md`](../../instructions/documentation.instructions.md)

### Supporting resources

- [`scripts/normalize_release.py`](scripts/normalize_release.py)
- [`references/classification-rules.md`](references/classification-rules.md)
```

Only list files that exist.

Do not move shared scripts into a skill unless the repository already defines that ownership.

---

## F. Hooks

Inspect:

```text
.github/hooks/
```

Identify:

* hook configuration files;
* lifecycle event;
* script invoked;
* validation or policy purpose;
* related agent, instruction, skill, or workflow.

For hook documentation or configuration files, add or maintain a clearly documented mapping:

```markdown
## Hook relationships

| Hook | Script | Enforces | Also used by |
|---|---|---|---|
| Post-edit validation | `scripts/validate-files.sh` | Repository instructions | `validate-customizations.yml` |
```

Only claim execution where the hook configuration directly invokes the script.

Do not describe a hook as a GitHub Actions workflow.

Hooks and workflows are separate automation mechanisms. See
[`rules/hooks.rules.md`](./rules/hooks.rules.md) for the authoritative hook
configuration schema before documenting any hook relationship.

---

## G. GitHub Actions workflows

For each:

```text
.github/workflows/*.yml
.github/workflows/*.yaml
```

Inspect actual steps and referenced paths.

Document relationships through YAML comments only when useful and non-disruptive.

Example:

```yaml
# Validates:
# - .github/copilot-instructions.md
# - .github/agents/**/*.agent.md
# - .github/instructions/**/*.instructions.md
# - .github/prompts/**/*.prompt.md
# - .github/skills/**/SKILL.md
```

Do not add comments that claim validation which the workflow does not perform.

When the workflow executes a script, verify the path and record the relationship as:

```text
workflow → executes → script
```

When a workflow validates files, record:

```text
workflow → validates → component
```

---

## H. `PULL_REQUEST_TEMPLATE.md`

Update only when necessary.

The pull-request template may reference categories rather than every file.

It should request confirmation for changes involving:

```text
copilot-instructions
agents
instructions
prompts
skills
hooks
workflows
security permissions
```

Example section:

```markdown
## GitHub customization impact

- [ ] Repository-wide Copilot instructions changed
- [ ] Path-specific instructions changed
- [ ] Custom agent changed
- [ ] Prompt file changed
- [ ] Skill changed
- [ ] Hook or executable script changed
- [ ] GitHub Actions workflow changed
- [ ] Tool, secret, or permission scope changed
- [ ] Related references were validated
```

Do not place detailed architecture documentation inside the PR template.

---

## I. `CODEOWNERS`

Inspect existing ownership rules.

Confirm that sensitive paths have an owner where appropriate:

```text
/.github/copilot-instructions.md
/.github/agents/
/.github/instructions/
/.github/prompts/
/.github/skills/
/.github/hooks/
/.github/workflows/
/.github/CODEOWNERS
/.github/dependabot.yml
```

Do not invent usernames or teams.

If ownership is missing and no valid owner is known, report the missing rule rather than adding a fake identity.

---

## J. `dependabot.yml`

Dependabot normally has a dependency-management relationship with:

```text
.github/workflows/
```

and any detected package ecosystems.

Do not add Markdown links inside `dependabot.yml`.

Document this relationship in the architecture report instead.

Do not change update ecosystems unless required by the task.

---

## K. Issue templates

For existing files under:

```text
.github/ISSUE_TEMPLATE/
```

Identify whether they create work for:

* agents;
* instructions;
* prompts;
* skills;
* hooks;
* workflows;
* release research;
* security review.

Issue templates may include fields such as:

```text
Affected component
Existing file
Proposed relationship
Authoritative source
Security impact
Validation criteria
```

Do not create issue templates when none exist unless explicitly requested.

---

# Phase 5: Prevent harmful relationships

Do not create circular procedural dependencies such as:

```text
agent requires prompt
prompt requires agent
```

unless the relationship is explicitly intentional and documented as optional.

Avoid patterns such as:

```text
every agent → every instruction
every prompt → every skill
every skill → every agent
```

Prefer the smallest useful graph.

A healthy relationship model is:

```text
repository instruction
        ↓
specialized instruction
        ↓
agent or prompt
        ↓
skill
        ↓
script or resource
        ↓
validation workflow
```

Bidirectional documentation links are permitted for discoverability, but runtime responsibility must remain directional.

Example:

```text
Agent documentation:
"This agent uses the release-analysis skill."

Skill documentation:
"This skill is used by the release-analyst agent."
```

This is a documentation relationship, not two runtime invocations.

---

# Phase 6: Generate the architecture report

Create or update an architecture report only when an appropriate documentation location already exists.

Preferred paths:

```text
docs/architecture/github-customization-map.md
docs/github-customization-map.md
.github/ARCHITECTURE.md
```

Selection order:

1. Use an existing architecture documentation folder.
2. Use an existing `.github/ARCHITECTURE.md`.
3. When no documentation location exists, propose the file but do not create it unless the task permits files outside `.github`.
4. When restricted to `.github`, use `.github/ARCHITECTURE.md`.

The report should contain:

```markdown
# GitHub Customization Architecture

## Component inventory

| Type | File | Responsibility | Status |
|---|---|---|---|

## Relationship matrix

| Source | Relationship | Target | Runtime | Reason |
|---|---|---|---|---|

## Dependency flow

```text
copilot-instructions.md
    ├── instructions
    │   ├── agents
    │   ├── prompts
    │   └── skills
    ├── hooks
    └── workflows
```

## Missing relationships

List files that should probably be related but require human confirmation.

## Broken references

List references whose target does not exist.

## Duplicated responsibilities

List files that repeat the same rules.

## Security-sensitive relationships

List:

* executable hooks;
* scripts;
* workflow permissions;
* MCP or tool access;
* external dependencies;
* secret usage.

## Validation results

Record checks actually performed.

```

---

# Phase 7: Implementation rules

After the discovery and relationship plan is approved:

1. Modify only files with confirmed relationships.
2. Use relative Markdown links.
3. Preserve existing front matter.
4. Preserve required file schemas.
5. Avoid changing behavior while adding documentation links.
6. Do not alter tool permissions unless explicitly requested.
7. Do not rename files.
8. Do not create missing agents, prompts, skills, instructions, hooks, or workflows.
9. Do not remove `.gitkeep` files unless a real file is added to that directory.
10. Do not commit or push unless explicitly instructed.

---

# Relative-link examples

From:

```text
.github/copilot-instructions.md
```

to an agent:

```markdown
[Release analyst agent](./agents/release-analyst.agent.md)
```

From:

```text
.github/agents/release-analyst.agent.md
```

to repository instructions:

```markdown
[Repository-wide instructions](../copilot-instructions.md)
```

From an agent to an instruction:

```markdown
[Documentation instructions](../instructions/documentation.instructions.md)
```

From an agent to a skill:

```markdown
[Release-analysis skill](../skills/release-analysis/SKILL.md)
```

From a prompt to an agent:

```markdown
[Recommended agent](../agents/release-analyst.agent.md)
```

From a skill to repository instructions:

```markdown
[Repository-wide instructions](../../copilot-instructions.md)
```

From a skill to an agent:

```markdown
[Release analyst agent](../../agents/release-analyst.agent.md)
```

Always calculate the relative path from the source file.

---

# Validation requirements

Perform all applicable checks.

## File validation

* Confirm every linked target exists.
* Confirm path capitalization matches exactly.
* Confirm links use the correct relative depth.
* Confirm no link targets `.gitkeep`.
* Confirm no unsupported file was created.
* Confirm front matter remains valid.
* Confirm Markdown headings are not duplicated.

## Relationship validation

* Confirm each relationship has a documented reason.
* Confirm runtime relationships are supported by configuration or code.
* Confirm logical links are not described as automatic imports.
* Confirm no unnecessary all-to-all linking was added.
* Confirm no circular mandatory workflow was introduced.
* Confirm repository-wide rules were not copied into every file.

## Security validation

* Confirm no secrets were introduced.
* Confirm no external code is executed.
* Confirm hooks and scripts are clearly identified.
* Confirm workflow permissions were not expanded.
* Confirm CODEOWNERS entries were not invented.
* Confirm sensitive files remain reviewable.

## Git validation

Review:

```bash
git status --short
git diff --check
git diff -- .github
```

Run repository-specific validation commands when available.

Do not claim a command passed unless it was executed.

---

# Required Plan-mode output

Before making changes, return:

## 1. Existing inventory

| Type | Existing paths | Count | Status |
| ---- | -------------- | ----: | ------ |

## 2. Confirmed relationships

| Source | Relationship | Target | Reason |
| ------ | ------------ | ------ | ------ |

## 3. Proposed file modifications

| File | Proposed change | Behavioral impact |
| ---- | --------------- | ----------------- |

## 4. Missing components

List folders that are:

* absent;
* empty;
* `.gitkeep` only;
* missing expected entry files.

Do not propose links to them as existing components.

## 5. Risks and ambiguities

List:

* unclear ownership;
* duplicated instructions;
* broken links;
* unsupported runtime assumptions;
* security-sensitive scripts;
* unknown file formats.

## 6. Approval boundary

End the plan with:

> No files have been changed. Approve this plan before relationship links are applied.

---

# Required implementation report

After approved implementation, return:

## `.github` relationship linking completed

### Files inspected

List all relevant files inspected.

### Files modified

| File | Relationship added or corrected |
| ---- | ------------------------------- |

### Confirmed architecture

```text
Show the final relationship flow.
```

### Broken or unresolved relationships

List links that were not created and explain why.

### Files intentionally not created

Confirm that missing agents, prompts, skills, instructions, hooks, workflows, and issue templates were not generated.

### Validation performed

* [ ] Every target path exists
* [ ] Relative links validated
* [ ] Markdown structure reviewed
* [ ] Front matter preserved
* [ ] Runtime claims verified
* [ ] No secrets introduced
* [ ] No workflow permissions expanded
* [ ] Git diff reviewed

Do not mark an item complete unless it was actually validated.

---

# Recommended relationship architecture

The most maintainable model is not “every file references every other file.” It is a layered architecture:

```text
┌──────────────────────────────────────────────┐
│ .github/copilot-instructions.md              │
│ Repository-wide standards                   │
└──────────────────────┬───────────────────────┘
                       │ governs
              ┌────────┴────────┐
              ▼                 ▼
┌───────────────────────┐  ┌───────────────────────┐
│ instructions/         │  │ Governance            │
│ Scoped guidance       │  │ CODEOWNERS / PR       │
└───────────┬───────────┘  └───────────────────────┘
            │ guides
      ┌─────┴───────────────┐
      ▼                     ▼
┌───────────────┐    ┌───────────────┐
│ agents/       │    │ prompts/      │
│ Orchestration │    │ Reusable task │
└───────┬───────┘    └───────┬───────┘
        │ uses                 │ uses
        └──────────┬───────────┘
                   ▼
          ┌─────────────────┐
          │ skills/         │
          │ Procedures and  │
          │ supporting data │
          └────────┬────────┘
                   │ may use
                   ▼
          ┌─────────────────┐
          │ hooks/scripts   │
          │ Deterministic   │
          │ execution       │
          └────────┬────────┘
                   │ validated by
                   ▼
          ┌─────────────────┐
          │ workflows/      │
          │ CI and security │
          └─────────────────┘
```

# Example of a correct relationship

Assume the repository contains:

```text
.github/
├── copilot-instructions.md
├── agents/
│   └── release-analyst.agent.md
├── instructions/
│   └── documentation.instructions.md
├── prompts/
│   └── analyze-release.prompt.md
└── skills/
    └── release-analysis/
        └── SKILL.md
```

The links would be:

```text
copilot-instructions.md
    ├── documents agents/
    ├── documents instructions/
    ├── documents prompts/
    └── documents skills/

release-analyst.agent.md
    ├── follows copilot-instructions.md
    ├── uses documentation.instructions.md
    ├── supports analyze-release.prompt.md
    └── uses release-analysis/SKILL.md

analyze-release.prompt.md
    ├── follows copilot-instructions.md
    ├── recommends release-analyst.agent.md
    ├── applies documentation.instructions.md
    └── uses release-analysis/SKILL.md

release-analysis/SKILL.md
    ├── follows copilot-instructions.md
    ├── is used by release-analyst.agent.md
    └── supports analyze-release.prompt.md
```

---

## Pipeline complete

Once this step's implementation report has been produced and approved, the
capability package generated by [`02-universal-meta-prompt-builder.md`](./02-universal-meta-prompt-builder.md)
is considered fully built and linked. There is no further step in this
pipeline.
