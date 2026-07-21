# WINDSURF CONFIGURATION REBUILD META-PROMPT

## ROLE

Act as a Senior Windsurf Configuration Architect, GitHub Copilot
Customization Specialist, Security Engineer, and Repository Migration Lead.

Your task is to completely rebuild the repository's Windsurf configuration
from the existing GitHub Copilot configuration.

This is not a blind filename copy.

Perform a semantic migration that preserves every useful capability from
GitHub Copilot while translating it into Windsurf-native Rules, Skills,
Workflows, and AGENTS.md instructions.

The repository must continue supporting both:

1. GitHub Copilot
2. Windsurf Cascade

The existing `.github/` configuration is the source of truth for the
migration and must remain unchanged.

---

# PRIMARY OBJECTIVE

Inspect all GitHub Copilot customization files and create a new professional
Windsurf configuration that provides equivalent capabilities.

Migrate all relevant:

- agents
- instructions
- prompts
- workflows
- standards
- checklists
- templates
- domain expertise
- architecture guidance
- testing guidance
- security guidance
- compliance guidance
- implementation processes
- Git and GitHub processes
- runbook processes
- business-analysis processes
- QA processes
- infrastructure processes
- CyberArk-related safe guidance
- SQL guidance
- documentation guidance

The final Windsurf architecture must use:

- `.windsurfrules`
- root `AGENTS.md`
- `.windsurf/rules/*.md`
- `.windsurf/skills/<skill-name>/SKILL.md`
- `.windsurf/workflows/*.md`

Do not create nested `AGENTS.md` files under `src/` during this migration.

The current `src/` architecture is temporary and will be redesigned later.

---

# DESTRUCTIVE-CHANGE AUTHORIZATION

The user has explicitly authorized replacing the current `.windsurf/`
configuration.

You may:

- delete existing files inside `.windsurf/`
- delete obsolete directories inside `.windsurf/`
- recreate `.windsurf/` from scratch
- replace the root `.windsurfrules`
- replace or create the root `AGENTS.md`

You must not:

- delete `.github/`
- modify `.github/`
- rename `.github/`
- delete application source code
- modify files under `src/`
- modify tests
- modify deployment code
- modify project dependencies
- modify CI/CD files unless they are inside `.windsurf/`
- expose credentials or secrets

Before deletion, record the existing `.windsurf/` file inventory in the
migration report.

If Git is available, verify that the repository is under version control
before deleting the old `.windsurf/` configuration.

Do not create a Git commit unless explicitly requested.

---

# SOURCE LOCATIONS

Inspect all relevant repository content, especially:

- `.github/agents/`
- `.github/instructions/`
- `.github/prompts/`
- `.github/workflows/`
- `.github/copilot-instructions.md`
- `.github/CODEOWNERS`
- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/README*`
- project-level README files
- project documentation referenced by Copilot files

Also inspect the existing:

- `.windsurf/`
- `.windsurfrules`
- `AGENTS.md`

Use the existing Windsurf configuration only as historical input.

Do not assume that the current Windsurf implementation is correct.

---

# TARGET ARCHITECTURE

Create this target structure, adapting names to the actual capabilities
found in `.github/`:

project-root/
├── .github/
│   └── preserve completely unchanged
│
├── .windsurfrules
├── AGENTS.md
│
└── .windsurf/
    ├── README.md
    ├── MIGRATION-MAP.md
    ├── VALIDATION-REPORT.md
    │
    ├── rules/
    │   ├── project-core.md
    │   ├── architecture.md
    │   ├── coding-standards.md
    │   ├── code-writing.md
    │   ├── configuration.md
    │   ├── error-handling.md
    │   ├── security-compliance.md
    │   ├── testing-strategy.md
    │   ├── documentation.md
    │   └── additional domain-specific rules as required
    │
    ├── skills/
    │   ├── architecture-analysis/
    │   │   ├── SKILL.md
    │   │   ├── process.md
    │   │   ├── checklist.md
    │   │   └── output-template.md
    │   │
    │   ├── architecture-review/
    │   ├── business-analysis/
    │   ├── code-review/
    │   ├── code-writer/
    │   ├── compliance-audit/
    │   ├── confluence/
    │   ├── cyberark/
    │   ├── github-commit/
    │   ├── implementation/
    │   ├── knowledge-base/
    │   ├── linux-infrastructure/
    │   ├── qa-analysis/
    │   ├── runbook/
    │   ├── sql-analysis/
    │   ├── tdd-design/
    │   └── additional skills derived from Copilot agents
    │
    └── workflows/
        ├── architecture-analysis.md
        ├── architecture-review.md
        ├── architecture-solution-design.md
        ├── business-analysis.md
        ├── code-review.md
        ├── code-writer.md
        ├── compliance-audit.md
        ├── github-commit.md
        ├── implementation.md
        ├── knowledge-base.md
        ├── linux-check-development.md
        ├── linux-infrastructure-audit.md
        ├── linux-ssh-debug.md
        ├── qa-analysis.md
        ├── runbook.md
        ├── sql-analysis.md
        ├── tdd-design.md
        └── additional workflows derived from Copilot prompts

Do not create empty placeholder directories.

Create only capabilities supported by source material or clearly required
to route migrated content.

---

# WINDSURF COMPONENT MODEL

Use the following separation strictly.

## 1. `.windsurfrules`

Create `.windsurfrules` as a concise legacy compatibility file.

It must contain only critical, repository-wide constraints such as:

- repository purpose
- mandatory security behavior
- prohibition against secrets
- instruction to preserve `.github/`
- minimal change discipline
- requirement to follow root `AGENTS.md`
- references to `.windsurf/rules/`, `.windsurf/skills/`, and
  `.windsurf/workflows/`

Do not copy every detailed rule into `.windsurfrules`.

Do not duplicate entire rule files.

Target approximately 50–120 lines maximum unless the source architecture
demonstrably requires more.

Clearly state that detailed canonical instructions live under:

- `.windsurf/rules/`
- `.windsurf/skills/`
- `.windsurf/workflows/`

---

## 2. Root `AGENTS.md`

Create exactly one root `AGENTS.md` during this migration.

The root file is project-wide operating guidance for Cascade.

It must contain:

- repository mission
- repository navigation procedure
- source-of-truth hierarchy
- rules, skills, and workflows routing
- change discipline
- security requirements
- testing expectations
- documentation expectations
- agent-role routing model
- skill-selection instructions
- workflow-selection instructions
- collaboration and handoff behavior
- uncertainty and escalation behavior
- prohibition against editing unrelated files
- statement that nested `AGENTS.md` files are intentionally deferred

Do not add YAML frontmatter to `AGENTS.md`.

Do not turn `AGENTS.md` into a copy of every Copilot agent.

Do not duplicate complete skill content in `AGENTS.md`.

Instead, build a routing table such as:

| Task type | Primary skill | Workflow |
|---|---|---|
| Architecture analysis | `@architecture-analysis` | `/architecture-analysis` |
| Code review | `@code-review` | `/code-review` |
| Git commit preparation | `@github-commit` | `/github-commit` |
| Runbook creation | `@runbook` | `/runbook` |

The table must be generated from the actual migrated capabilities.

Use repository-relative references where useful.

Example:

- Skill: `.windsurf/skills/code-review/SKILL.md`
- Workflow: `.windsurf/workflows/code-review.md`
- Rule: `.windsurf/rules/coding-standards.md`

Do not claim that these Markdown links technically register skills.
They are navigation and routing guidance.

---

## 3. Windsurf Rules

Use `.windsurf/rules/*.md` for persistent behavioral guidance and
constraints.

Examples:

- coding standards
- architecture constraints
- security requirements
- compliance requirements
- testing standards
- error-handling rules
- documentation standards
- configuration conventions
- file-specific rules
- language-specific conventions

Every rule must begin with valid YAML frontmatter.

Use one of these activation strategies:

### Always-on rule

Use for short, critical requirements that must apply to every interaction.

Example:

---
trigger: always_on
---

### Glob rule

Use for instructions that apply only to particular paths or file types.

Example:

---
trigger: glob
globs:
  - "**/*.py"
  - "tests/**/*.py"
---

Use the exact frontmatter syntax supported by the installed Windsurf
version. If the repository or Windsurf UI shows a different accepted shape,
use the documented local syntax rather than inventing one.

### Model-decision rule

Use for specialized guidance Cascade should load only when relevant.

Example intent:

---
trigger: model_decision
description: Apply when reviewing application architecture or proposing
structural changes.
---

### Manual rule

Use only where explicit user activation is preferable.

Do not mark every rule `always_on`.

Keep always-on context small.

Each rule must have:

- clear purpose
- clear scope
- enforceable instructions
- prohibited behaviors
- validation expectations
- references to applicable skills when useful

Do not place long operational procedures in Rules.

Move procedures to Skills or Workflows.

---

## 4. Windsurf Skills

Use `.windsurf/skills/<skill-name>/SKILL.md` for reusable expertise,
multi-step procedures, and supporting resources.

Each skill must be placed in its own directory.

Each skill directory must contain exactly one canonical file named:

`SKILL.md`

The filename must use uppercase `SKILL.md`.

Every `SKILL.md` must start with YAML frontmatter:

---
name: lowercase-hyphenated-name
description: Explain precisely what the skill does and when Cascade should
use it.
---

Skill names must use only:

- lowercase letters
- numbers
- hyphens

The `description` must be semantically specific because Cascade uses the
name and description to determine when the skill is relevant.

Each `SKILL.md` should contain:

1. Purpose
2. When to use
3. When not to use
4. Required inputs
5. Relevant rules
6. Primary procedure
7. Decision points
8. Validation
9. Expected output
10. Failure handling
11. Supporting files
12. Safety boundaries

Supporting files may include:

- `process.md`
- `checklist.md`
- `templates.md`
- `examples.md`
- `references.md`
- `output-template.md`
- safe helper scripts
- schemas
- configuration templates without secrets

Use progressive disclosure:

- keep `SKILL.md` focused
- move large references into supporting files
- reference supporting files from `SKILL.md`
- avoid duplicating the same content across skills

Do not create a skill that only contains a one-line prompt.

Do not place organization secrets in skills.

Do not copy credentials, host passwords, tokens, CyberArk secret values,
private keys, or production connection strings.

---

## 5. Windsurf Workflows

Use `.windsurf/workflows/*.md` for explicit repeatable commands invoked by
the user with slash commands.

Examples:

- `/code-review`
- `/github-commit`
- `/architecture-analysis`
- `/runbook`

Workflow filenames must be lowercase and hyphenated.

Every workflow must contain:

1. Workflow name
2. Purpose
3. Invocation example
4. Required inputs
5. Optional inputs
6. Relevant rules
7. Relevant skills
8. Ordered execution steps
9. Safety gates
10. Validation steps
11. Stop conditions
12. Final response format

Workflows may explicitly instruct Cascade to apply a skill.

Use references such as:

- Apply `@code-review`
- Follow `.windsurf/skills/code-review/SKILL.md`
- Enforce `.windsurf/rules/coding-standards.md`

Do not assume the Markdown reference itself performs registration.

The skill is discovered through its `SKILL.md` metadata. The workflow
instruction provides explicit routing.

A workflow must inspect the repository before making changes.

A workflow must stop when:

- required information is missing
- requested work risks exposing secrets
- the requested scope is ambiguous and unsafe
- validation cannot be performed
- the operation would modify prohibited paths
- a destructive action was not authorized

Do not bury permanent coding standards only inside workflows.

Canonical standards belong in Rules.

---

# COPILOT-TO-WINDSURF CLASSIFICATION

Classify every source artifact by meaning.

## Copilot agent

A Copilot agent may contain:

- persona
- expertise
- rules
- process
- output format
- tool behavior
- collaboration rules

Do not copy a Copilot agent into a fake Windsurf agent file.

Split it as needed:

- persistent constraints → Rule
- expertise and procedure → Skill
- reusable invocation sequence → Workflow
- project-wide routing → root `AGENTS.md`
- template → Skill supporting file

One Copilot agent may produce multiple Windsurf artifacts.

Example:

`.github/agents/github-committer.agent.md`

May become:

- `.windsurf/skills/github-commit/SKILL.md`
- `.windsurf/skills/github-commit/commit-conventions.md`
- `.windsurf/skills/github-commit/checklist.md`
- `.windsurf/workflows/github-commit.md`
- an entry in root `AGENTS.md`

## Copilot instruction

Classify as:

- global constraint → always-on Rule
- language/path-specific standard → glob Rule
- specialized contextual guidance → model-decision Rule
- multi-step procedure → Skill
- checklist → Skill supporting file
- mixed content → split across multiple artifacts

## Copilot prompt

Classify as:

- repeatable user-invoked operation → Workflow
- reusable procedural expertise → Skill
- output template → Skill supporting file
- permanent behavior → Rule

Do not create `.windsurf/prompts/`.

Windsurf workflows replace reusable explicit prompt commands in this
architecture.

## Copilot workflow

Convert to:

- Windsurf Workflow
- related Skill when reusable expertise or supporting files are required
- related Rule when permanent constraints are embedded

## Copilot template

Move to the relevant skill directory.

Examples:

- PR review template → code-review skill
- runbook template → runbook skill
- architecture decision template → architecture skill
- QA report template → QA skill

---

# CAPABILITY MIGRATION REQUIREMENT

Every source agent, instruction, prompt, and workflow must be accounted for.

Create a migration table containing:

| Source file | Source type | Responsibilities | Target rule | Target skill | Target workflow | Status |
|---|---|---|---|---|---|---|

No source file may be silently skipped.

Allowed statuses:

- Migrated
- Split across targets
- Consolidated as duplicate
- Preserved only in Copilot
- Obsolete
- Requires user decision

Any file marked obsolete or preserved only in Copilot must include a clear
reason.

---

# DEDUPLICATION RULES

Before creating files, analyze duplication across all Copilot content.

Identify common repeated material, including:

- coding standards
- security restrictions
- output formats
- Git conventions
- testing requirements
- architecture principles
- documentation requirements
- no-secret rules
- environment handling
- validation requirements

Assign one canonical destination to each reusable instruction.

Examples:

- universal secret handling → `security-compliance.md`
- Python conventions → Python glob Rule
- Git commit procedure → `github-commit` Skill
- commit execution command → `github-commit` Workflow
- review output template → code-review Skill supporting file

Reference canonical files instead of duplicating full paragraphs.

Avoid circular references.

---

# AGENT-TO-SKILL ROUTING MODEL

Windsurf does not require a separate agent-registration file.

Implement logical role routing in root `AGENTS.md`.

For each migrated Copilot agent, define:

- role name
- mission
- primary skill
- optional supporting skills
- primary workflow
- applicable rules
- boundaries
- expected output
- handoff conditions

Use a section similar to:

## Role Routing

### Architecture Role

Mission:
Analyze and design system architecture without modifying implementation
until explicitly authorized.

Primary skill:
`@architecture-analysis`

Supporting skills:
`@business-analysis`
`@compliance-audit`

Primary workflow:
`/architecture-analysis`

Applicable rules:
- `.windsurf/rules/architecture.md`
- `.windsurf/rules/security-compliance.md`

Handoff:
After approval, hand off implementation to `@implementation`.

Generate this routing from actual source agents.

Do not pretend that these roles are separate persistent running agents.

They are behavioral roles and routing conventions for Cascade.

---

# SOURCE-OF-TRUTH PRECEDENCE

Document this hierarchy in root `AGENTS.md` and `.windsurf/README.md`:

1. User's current explicit request
2. Security and organizational restrictions
3. Root `AGENTS.md`
4. Applicable `.windsurf/rules/*.md`
5. Explicitly invoked workflow
6. Applicable skill
7. Repository documentation
8. Existing implementation patterns

When instructions conflict:

- choose the safer interpretation
- report the conflict
- do not silently ignore security rules
- do not invent missing requirements
- request clarification only when implementation cannot safely proceed

Do not claim this hierarchy overrides Windsurf's internal platform-level
instruction precedence. It is the repository's intended operating policy.

---

# SECURITY AND CONFIDENTIALITY

Never copy or generate:

- passwords
- access tokens
- API keys
- SSH private keys
- certificate private keys
- vault secret values
- CyberArk secret values
- production credentials
- confidential connection strings
- personal data
- internal secrets

Safe content may include:

- environment-variable names
- placeholder values
- generic server-role names
- secret retrieval interfaces
- safe CyberArk workflow descriptions
- redacted examples

Use placeholders such as:

- `${SECRET_NAME}`
- `${CYBERARK_ACCOUNT}`
- `<REDACTED>`
- `<ENVIRONMENT_HOST>`

Do not inspect ignored secret files.

Do not weaken `.gitignore`, `.copilotignore`, or other security controls.

Do not place sensitive information in:

- Rules
- Skills
- Workflows
- AGENTS.md
- `.windsurfrules`
- migration reports

---

# MIGRATION EXECUTION

Execute the migration in the following order.

## Phase 1 — Repository discovery

1. Confirm the repository root.
2. List all `.github/` customization files.
3. List all existing `.windsurf/` files.
4. Detect existing `.windsurfrules`.
5. Detect existing root `AGENTS.md`.
6. Identify referenced documentation.
7. Identify potential sensitive content without reproducing it.
8. Identify duplicate instructions.
9. Identify missing referenced files.
10. Build the initial migration matrix.

Do not edit application code.

## Phase 2 — Backup awareness

Before replacing `.windsurf/`:

1. Confirm that Git tracks or can recover the current files.
2. Record the current `.windsurf/` inventory in the migration report.
3. Report uncommitted changes affecting:
   - `.windsurf/`
   - `.windsurfrules`
   - `AGENTS.md`

The user has already authorized replacing these paths.

Do not block the migration solely because these files exist.

Do stop if deleting them would also delete application code or files
outside the approved configuration paths.

## Phase 3 — Remove current Windsurf configuration

Remove:

- all contents under `.windsurf/`
- the existing `.windsurfrules`, if present
- the existing root `AGENTS.md`, if present

Only remove these exact approved configuration paths.

Do not use broad recursive deletion patterns that could target another
directory.

Verify the resolved paths before deleting.

## Phase 4 — Build Rules

1. Create `.windsurf/rules/`.
2. Consolidate Copilot instructions into modular Rules.
3. Select appropriate activation modes.
4. Keep always-on Rules concise.
5. Add file globs only when supported by source scope.
6. Add descriptions for contextual Rules.
7. Remove duplicated procedures.
8. Reference Skills where appropriate.

## Phase 5 — Build Skills

For every reusable Copilot agent capability:

1. Create a lowercase-hyphenated skill directory.
2. Create canonical `SKILL.md`.
3. Add precise name and description frontmatter.
4. Extract procedural knowledge.
5. Add checklists, templates, examples, or references as supporting files.
6. Add failure handling and validation.
7. Reference canonical Rules.
8. Avoid duplication.

## Phase 6 — Build Workflows

For every reusable Copilot prompt or workflow:

1. Create a lowercase-hyphenated Workflow file.
2. Define invocation and inputs.
3. Reference applicable Rules.
4. Route to relevant Skills.
5. Preserve source intent.
6. Add repository inspection steps.
7. Add safety gates.
8. Add validation.
9. Define the output format.
10. Add stop conditions.

## Phase 7 — Build root `AGENTS.md`

Create root `AGENTS.md` with:

- project-wide operating instructions
- Windsurf component navigation
- capability routing table
- migrated role definitions
- agent-to-skill routing
- workflow routing
- collaboration and handoff behavior
- security and compliance expectations
- change discipline
- test expectations
- documentation expectations
- explicit statement that nested `AGENTS.md` files are deferred

Do not create `src/**/AGENTS.md`.

## Phase 8 — Build `.windsurfrules`

Create a concise legacy compatibility file.

It must:

- summarize critical always-on constraints
- direct Cascade to root `AGENTS.md`
- identify `.windsurf/rules/` as canonical detailed Rules
- identify `.windsurf/skills/` as reusable capabilities
- identify `.windsurf/workflows/` as slash-command procedures
- prohibit secret exposure
- prohibit unauthorized application changes
- preserve `.github/`

Do not duplicate the full contents of root `AGENTS.md`.

## Phase 9 — Documentation

Create `.windsurf/README.md`.

Explain:

- why both `.github/` and `.windsurf/` exist
- how GitHub Copilot and Windsurf coexist
- Rules versus Skills versus Workflows versus `AGENTS.md`
- purpose of `.windsurfrules`
- how Skills are automatically selected
- how to explicitly invoke a Skill with `@skill-name`
- how to invoke a Workflow with `/workflow-name`
- how root `AGENTS.md` routes capabilities
- why nested `AGENTS.md` files are deferred
- how nested `AGENTS.md` files can be added after `src/` redesign
- naming conventions
- frontmatter requirements
- maintenance rules
- process for adding a new capability

Create `.windsurf/MIGRATION-MAP.md`.

Include:

- original file inventory
- target mapping
- consolidation decisions
- duplicate-content decisions
- obsolete-content decisions
- unresolved issues
- security redactions
- files intentionally not migrated

Create `.windsurf/VALIDATION-REPORT.md`.

Include the results of every validation check.

---

# VALIDATION REQUIREMENTS

After implementation, perform all checks below.

## Structural validation

Verify:

- `.github/` still exists
- `.github/` content was not modified
- `.windsurfrules` exists
- root `AGENTS.md` exists
- `.windsurf/rules/` exists
- `.windsurf/skills/` exists
- `.windsurf/workflows/` exists
- every skill directory contains `SKILL.md`
- no skill uses lowercase `skill.md`
- no empty capability directories exist
- no nested `AGENTS.md` files were created under `src/`

## Rules validation

Verify:

- every Rule has valid frontmatter
- every Rule has an intentional trigger
- always-on context is concise
- globs match real repository paths
- no procedures are unnecessarily duplicated
- no conflicting Rules exist
- no unsupported trigger type was invented

## Skills validation

Verify:

- every skill name is lowercase and hyphenated
- every `SKILL.md` has `name`
- every `SKILL.md` has `description`
- descriptions explain when the skill is applicable
- supporting-file references resolve
- each skill has clear boundaries
- each skill defines validation
- each skill defines expected output
- no secret values exist

## Workflow validation

Verify:

- workflow filenames are lowercase and hyphenated
- every workflow can be invoked as a slash command
- each workflow references valid Rules and Skills
- each workflow defines required inputs
- each workflow defines ordered steps
- each workflow defines validation
- each workflow defines stop conditions
- no workflow claims unsupported automatic execution

## Routing validation

Verify:

- every migrated Copilot agent has a corresponding role entry
- every role points to an existing Skill, Workflow, or Rule
- all `@skill-name` references match actual skill names
- all `/workflow-name` references match actual workflow filenames
- no circular handoffs exist
- no role is assigned overlapping ownership without explanation

## Migration coverage

Verify:

- every Copilot agent was analyzed
- every Copilot instruction was analyzed
- every Copilot prompt was analyzed
- every Copilot workflow was analyzed
- every source file appears in `MIGRATION-MAP.md`
- skipped files include reasons
- duplicate files include canonical destinations
- no capability was silently lost

## Security validation

Search generated Windsurf configuration for:

- passwords
- tokens
- private keys
- API keys
- secret values
- production credentials
- confidential endpoints

Do not print detected sensitive values.

If suspicious content is detected:

1. redact it
2. report the affected filename
3. explain the category of risk
4. do not reproduce the value

## Scope validation

Verify that no files outside these approved paths were modified:

- `.windsurf/**`
- `.windsurfrules`
- `AGENTS.md`

The migration reports are included under `.windsurf/**`.

If another path was changed accidentally, revert that change.

---

# FINAL RESPONSE FORMAT

When finished, respond with:

## 1. Migration summary

State:

- number of Copilot agents analyzed
- number of instructions analyzed
- number of prompts analyzed
- number of workflows analyzed
- number of Windsurf Rules created
- number of Windsurf Skills created
- number of Windsurf Workflows created

## 2. Created architecture

Display the complete new Windsurf tree.

## 3. Capability mapping

Summarize major Copilot-to-Windsurf mappings.

## 4. Deleted Windsurf files

List only the paths removed from the previous `.windsurf/` configuration.

## 5. Preserved files

Confirm that `.github/` was not modified.

## 6. Validation results

Show pass, warning, or failure for:

- structure
- Rules
- Skills
- Workflows
- routing
- migration coverage
- security
- scope

## 7. Warnings

List:

- unresolved mappings
- ambiguous source instructions
- broken source references
- intentionally deferred nested `AGENTS.md` files
- any content that requires human review

## 8. Suggested test commands

Provide Windsurf commands to test, for example:

- `/architecture-analysis`
- `/code-review`
- `/github-commit`
- `/runbook`

Also provide one direct Skill test using:

- `@skill-name`

Do not create a Git commit.

Do not modify application code.

Do not modify `.github/`.

---

# FINAL QUALITY STANDARD

The resulting Windsurf configuration must:

- preserve the intent of the Copilot architecture
- use current Windsurf-native structures
- keep `.github/` functional for Copilot
- provide equivalent reusable capabilities in Windsurf
- avoid blind one-to-one copying
- avoid duplicate knowledge
- use precise Skill descriptions
- use safe Rules activation
- provide clear workflow slash commands
- provide logical agent-to-skill routing
- remain maintainable as the source architecture changes
- avoid creating nested `AGENTS.md` files prematurely
- contain no secrets
- make no application-code changes
