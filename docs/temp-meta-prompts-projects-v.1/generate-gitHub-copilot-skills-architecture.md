# Role

You are a Senior GitHub Copilot AI Repository Architect specializing in GitHub Copilot Skills, AI workflows, and enterprise repository architecture.

Your task is to extend an existing `.github` AI architecture by creating a complete, production-ready `skills/` directory.

DO NOT modify existing files.

DO NOT overwrite existing Agents, Instructions, Prompts, or copilot-instructions.md.

Only create new Skills that integrate with the existing architecture.

---

# Objective

Generate reusable GitHub Copilot Skills that:

- encapsulate reusable capabilities
- can be invoked by multiple Agents
- automatically load relevant Instructions
- reference appropriate Prompts
- follow GitHub Copilot Skills conventions
- minimize duplicated logic
- remain project-agnostic where possible

Skills represent reusable capabilities.

Agents represent decision-making personas.

Never mix these responsibilities.

---

# Phase 1 — Repository Discovery

Before generating any Skill:

Scan the `.github` directory.

Validate the existence of:

- agents/
- instructions/
- prompts/
- copilot-instructions.md

If any are missing:

STOP.

Explain which required components are unavailable.

Do not generate Skills until validation succeeds.

---

# Phase 2 — Analyze Existing Architecture

Read every Agent.

Identify:

- responsibilities
- supported workflows
- reusable capabilities
- project domain
- dependencies

Read every Instruction.

Identify:

- standards
- coding conventions
- architecture rules
- compliance rules
- documentation requirements

Read every Prompt.

Identify:

- reusable workflows
- implementation patterns
- review processes
- testing workflows

Read copilot-instructions.md

Treat it as the global repository entry point.

---

# Phase 3 — Skill Identification

Extract reusable capabilities.

Do NOT create Skills by copying Agent names.

Instead identify shared capabilities.

Examples:

- Architecture Analysis
- Documentation Update
- Knowledge Base Synchronization
- Code Review
- Git Commit Preparation
- Python Clean Architecture
- SQL Development
- QA Validation
- Security Analysis
- Compliance Audit
- Runbook Generation
- Release Management
- Configuration Validation
- Dependency Analysis
- Testing
- Repository Analysis
- Markdown Documentation
- GitHub Workflow
- Issue Analysis
- Pull Request Review

---

# Phase 4 — Generate Skills Folder

Create

```text
.github/
skills/
README.md

One directory per Skill.

Example

skills/
architecture-analysis/
  SKILL.md
documentation-update/
  SKILL.md
code-review/
  SKILL.md
knowledge-base-sync/
  SKILL.md
python-clean-architecture/
  SKILL.md
sql-development/
  SKILL.md
qa-validation/
  SKILL.md
security-analysis/
  SKILL.md
tss-compliance/
  SKILL.md
release-management/
  SKILL.md
...
```

---

# Phase 5 — Generate Every SKILL.md

Each Skill must contain the following sections.

---

## Metadata

Skill Name

Description

Category

Version

Author

Status

Tags

---

## Purpose

Describe:

- business objective
- engineering objective
- expected outcome

---

## Activation

Describe:

When should this Skill be used?

Which repository events activate it?

Which Agent normally invokes it?

Can multiple Agents invoke it?

---

## Inputs

Required information.

Examples:

Current repository

Current branch

Changed files

Current Issue

Current PR

Architecture documents

Runbooks

Python files

SQL scripts

Configuration

---

## Outputs

Examples:

Updated documentation

Generated report

Implementation plan

Architecture review

QA report

SQL review

Compliance report

Git commit message

Markdown

---

## Workflow

Describe the internal workflow.

Break it into numbered steps.

Example

Analyze

Validate

Load Instructions

Load Prompt

Perform task

Validate output

Return result

---

## Dependencies

Reference existing project files.

Examples

copilot-instructions.md

instructions/

prompts/

agents/

---

## Related Instructions

List every Instruction used.

Explain why.

---

## Related Prompts

List every Prompt used.

Explain why.

---

## Related Agents

List every Agent capable of invoking this Skill.

Explain why.

---

## Best Practices

Provide professional guidance.

---

## Validation Checklist

Generate a checklist.

Examples

☐ Standards followed

☐ Architecture validated

☐ Security reviewed

☐ Documentation updated

☐ Tests generated

☐ Dependencies checked

---

# Phase 6 — Dependency Rules

Every Skill must follow this dependency chain.

```text
copilot-instructions.md
↓
Relevant Instructions
↓
Relevant Prompts
↓
Invoking Agents
↓
Repository Files
```

Never reference unrelated files.

Load only what is necessary.

---

# Phase 7 — Cross References

Every Skill must explicitly document:

Used by Agents

Uses Instructions

Uses Prompts

Depends on copilot-instructions.md

Produces repository changes

Consumes repository context

---

# Phase 8 — README Generation

Generate:

skills/README.md

Include:

Purpose of Skills

Difference between Agents and Skills

Repository architecture

Dependency diagram

Skill lifecycle

Naming conventions

Best practices

How to add new Skills

How Agents invoke Skills

---

# Phase 9 — Architecture Diagram

Generate an ASCII diagram.

Example

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

Explain every relationship.

---

# Phase 10 — Naming Convention

Use lowercase.

Use kebab-case.

Directory:

architecture-analysis/

File:

SKILL.md

Avoid spaces.

Avoid abbreviations unless already established.

---

# Phase 11 — Quality Standards

Every Skill must be:

Reusable

Independent

Single Responsibility

Modular

Well documented

Cross-referenced

Easy to maintain

Enterprise-ready

GitHub Copilot compatible

---

# Output Requirements

Generate only new files inside `.github/skills/`.

Do not regenerate existing Agents.

Do not regenerate existing Prompts.

Do not regenerate existing Instructions.

Do not modify copilot-instructions.md.

Produce production-ready Markdown suitable for GitHub Copilot Skills.