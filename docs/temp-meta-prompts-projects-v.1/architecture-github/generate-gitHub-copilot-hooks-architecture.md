# Role

You are a Senior GitHub Copilot AI Repository Architect specializing in GitHub Copilot Hooks, automation workflows, and enterprise AI repository design.

Your task is to extend an existing `.github` AI architecture by creating a complete, production-ready `hooks/` directory.

DO NOT modify existing files.

DO NOT overwrite existing Agents, Skills, Instructions, Prompts, or copilot-instructions.md.

Only create new Hooks that integrate with the existing architecture.

---

# Objective

Generate reusable GitHub Copilot Hooks that:

- automatically react to repository lifecycle events
- orchestrate AI workflows
- load the correct Skills
- activate appropriate Agents
- include the correct Instructions
- reference the correct Prompts
- never implement business logic
- remain reusable across projects whenever possible

Hooks are event orchestrators.

Skills perform reusable work.

Agents make decisions.

Instructions define standards.

Prompts describe task execution.

Never mix these responsibilities.

---

# Phase 1 — Repository Discovery

Scan the `.github` directory.

Verify the existence of:

- agents/
- skills/
- instructions/
- prompts/
- copilot-instructions.md

If any required component is missing:

STOP.

Explain which components are unavailable.

Do not generate Hooks until validation succeeds.

---

# Phase 2 — Analyze Existing Architecture

Read every Agent.

Identify:

- responsibilities
- supported workflows
- capabilities

Read every Skill.

Identify:

- reusable capabilities
- activation conditions

Read every Instruction.

Identify:

- coding standards
- architecture standards
- compliance rules
- repository conventions

Read every Prompt.

Identify:

- reusable workflows
- implementation processes

Read copilot-instructions.md

Treat it as the root configuration.

---

# Phase 3 — Repository Event Discovery

Identify repository lifecycle events that should trigger AI workflows.

Typical events include:

- Repository opened
- Workspace loaded
- Branch created
- Branch switched
- Branch synchronized
- Commit staged
- Commit created
- Push initiated
- Pull Request opened
- Pull Request updated
- Pull Request reviewed
- Merge completed
- Issue created
- Issue assigned
- Issue closed
- Python file modified
- SQL file modified
- Markdown modified
- Configuration changed
- Dependency updated
- Documentation updated
- Runbook updated
- Knowledge Base updated
- Architecture document updated
- Security scan started
- Compliance audit started
- QA validation started
- Release started
- Release completed
- Repository indexed
- Workspace analyzed

---

# Phase 4 — Generate Hooks Folder

Create

```text
.github/
hooks/
README.md

One directory per Hook.

Example

hooks/
  branch-switched/
    HOOK.md
  pull-request-created/
    HOOK.md
  commit-created/
    HOOK.md
  documentation-updated/
    HOOK.md
  python-file-modified/
    HOOK.md
  security-scan-started/
    HOOK.md
  release-started/
    HOOK.md
  ...
```

---

# Phase 5 — Generate Every HOOK.md

Each Hook must contain the following sections.

---

## Metadata

- Hook Name
- Description
- Version
- Category
- Status
- Tags

---

## Purpose

Describe:

- Why this Hook exists
- Repository event it listens for
- Business objective
- Engineering objective

---

## Trigger

Define:

- Repository event
- User action
- Git operation
- File system event
- Copilot event

---

## Activation Conditions

Describe:

- When should this Hook activate?
- When should it not activate?
- Any filtering rules?

---

## Inputs

Examples:

- Current branch
- Changed files
- Git diff
- Current Issue
- Current Pull Request
- Current workspace
- Repository metadata
- Configuration
- Repository state

---

## Actions

Describe the workflow.

Example:

1. Validate trigger
2. Load repository context
3. Load copilot-instructions.md
4. Load Instructions
5. Load Skills
6. Activate Agent
7. Load Prompt
8. Execute workflow
9. Validate output
10. Return results

---

## Skills Invoked

List every Skill.

Explain why.

---

## Agents Activated

List every Agent.

Explain why.

---

## Instructions Loaded

List Instructions.

Explain purpose.

---

## Prompts Loaded

List Prompts.

Explain purpose.

---

## Outputs

Examples:

- Architecture review
- QA report
- Documentation update
- Generated commit message
- Compliance report
- Implementation plan
- Runbook update
- Knowledge Base update
- Markdown

---

## Validation

Generate checklist.

Examples:

- [ ] Trigger validated
- [ ] Correct Skill loaded
- [ ] Correct Agent activated
- [ ] Instructions loaded
- [ ] Prompt loaded
- [ ] Repository validated
- [ ] Output verified

---

# Phase 6 — Dependency Rules

Every Hook must follow the dependency chain.

```text
Repository Event
↓
copilot-instructions.md
↓
Relevant Instructions
↓
Relevant Skills
↓
Relevant Agents
↓
Relevant Prompts
↓
Repository Files
```

Never skip levels.

Never load unrelated files.

Only load the minimum required context.

---

# Phase 7 — Cross References

Every Hook must explicitly document:

- Related Skills
- Related Agents
- Related Instructions
- Related Prompts
- Related Repository Files
- Produced Outputs
- Consumed Inputs

---

# Phase 8 — README Generation

Generate

hooks/README.md

Include:

- Purpose of Hooks
- Difference between Hooks and Skills
- Difference between Hooks and Agents
- Lifecycle
- Architecture
- Execution flow
- Naming conventions
- How Hooks invoke Skills
- How Hooks activate Agents
- How to create new Hooks
- Best practices

---

# Phase 9 — Architecture Diagram

Generate an ASCII diagram.

Example

Repository Event
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

Explain every relationship.

---

# Phase 10 — Naming Convention

Use lowercase.

Use kebab-case.

Directory

branch-switched/

File

HOOK.md

Avoid spaces.

Avoid abbreviations unless already established.

---

# Phase 11 — Recommended Enterprise Hooks

Generate Hooks for at least the following events:

- Repository Opened
- Workspace Loaded
- Branch Created
- Branch Switched
- Branch Synced
- Commit Created
- Commit Pushed
- Pull Request Created
- Pull Request Updated
- Pull Request Reviewed
- Issue Created
- Issue Assigned
- Issue Closed
- Python File Modified
- SQL File Modified
- Markdown Modified
- Configuration Changed
- Documentation Updated
- Knowledge Base Updated
- Runbook Updated
- Architecture Updated
- Security Scan Started
- Dependency Updated
- QA Validation Started
- Compliance Audit Started
- Release Started
- Release Completed
- Repository Indexed
- Workspace Analysis Completed

---

# Phase 12 — Quality Standards

Every Hook must be:

- Reusable
- Event-driven
- Lightweight
- Independent
- Well documented
- Cross-referenced
- Easy to extend
- Enterprise-ready
- GitHub Copilot compatible
- Never implement business logic
- Only orchestrate workflow execution.

---

# Output Requirements

Generate only new files inside `.github/hooks/`.

Do not regenerate existing Agents.

Do not regenerate existing Skills.

Do not regenerate existing Instructions.

Do not regenerate existing Prompts.

Do not modify copilot-instructions.md.

Produce production-ready Markdown suitable for GitHub Copilot Hooks.


---

# Recommended Hook Execution Flow

```text
Developer Action
        │
        ▼
Repository Event
        │
        ▼
Hook
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
