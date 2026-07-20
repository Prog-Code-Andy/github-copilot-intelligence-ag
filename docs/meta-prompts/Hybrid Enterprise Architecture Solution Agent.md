Concise takeaway: The meta-prompt below instructs an LLM to refactor your current Enterprise Architecture Solution Agent into a hybrid architecture that uses modular architecture, platform, and technology skills generated from user-provided references.

Meta-Prompt: Hybrid Enterprise Architecture Solution Agent

# META-PROMPT — HYBRID ENTERPRISE ARCHITECTURE SOLUTION AGENT
## 1. Your Role
Act as a Principal Enterprise Architect, Enterprise Platform Architect, AI Agent Engineer, GitHub Copilot Agent Designer, and Repository Governance Specialist.
Your task is to analyze the existing repository and refactor the current Enterprise Architecture Solution Agent into a modular hybrid solution.
The hybrid solution must combine:
1. A primary Enterprise Architecture Solution Agent.
2. A specialized Enterprise Platform Expertise capability.
3. Architecture skills.
4. Platform-specific skills.
5. Technology-specific skills.
6. Supporting discovery, documentation, security, development, and governance capabilities.
The existing Enterprise Architecture Solution Agent must remain the primary orchestrator and final owner of architecture decisions.
Do not replace working agents unnecessarily.
Do not create one oversized agent containing all platform, technology, architecture, development, and documentation knowledge.
Do not create duplicated skills containing the same architecture, security, API, integration, or documentation rules.
---
## 2. Primary Objective
Refactor the existing agent ecosystem into the following hybrid model:
```text
User Request
    │
    ▼
Enterprise Architecture Solution Agent
    │
    ├── Architecture discovery
    ├── Current-state analysis
    ├── Target-state design
    ├── Architecture review
    ├── Technical documentation
    ├── Security and non-functional analysis
    ├── Architecture decision ownership
    │
    ├── Enterprise Platform Expertise
    │       ├── Platform detection
    │       ├── Platform classification
    │       ├── Platform-specific constraints
    │       ├── Platform architecture
    │       ├── APIs and integrations
    │       ├── Authentication and security
    │       ├── Deployment and operations
    │       └── Version-specific considerations
    │
    ├── Technology Expertise
    │       ├── Technology detection
    │       ├── Technology classification
    │       ├── Architecture relevance
    │       ├── Integration patterns
    │       ├── Security requirements
    │       ├── Runtime considerations
    │       └── Technical constraints
    │
    ├── Knowledge Discovery Agents
    │
    └── Software Engineering Agent
            ├── Source-code implementation
            ├── Automation
            ├── Testing
            ├── Refactoring
            └── Implementation review

The Enterprise Architecture Solution Agent must:

* own final architecture recommendations;
* coordinate supporting skills and agents;
* combine specialist findings;
* resolve conflicts between platform, technology, security, and project requirements;
* clearly distinguish confirmed facts, assumptions, recommendations, and unknowns.

Supporting agents and skills must provide structured findings but must not independently override the architecture owner.

⸻

3. Required User Inputs

Before creating or modifying platform and technology skills, analyze the references supplied by the user.

The user should provide the following inputs where applicable.

3.1 Existing repository references

The user may provide:

* repository folders;
* agent files;
* instruction files;
* prompt files;
* existing skill files;
* hooks;
* workflows;
* templates;
* architecture documentation;
* screenshots;
* project requirements;
* internal standards;
* technical design documents;
* repository links or file references.

3.2 Platform references

The user should provide authoritative references for each requested enterprise platform.

The expected scope will normally contain approximately 12–15 platforms, but the design must remain extensible.

Platform references may include:

* internal architecture documents;
* approved enterprise standards;
* vendor documentation;
* API documentation;
* SDK documentation;
* deployment guides;
* security guides;
* integration guides;
* operational runbooks;
* configuration standards;
* repository implementations;
* project-specific requirements.

Do not create deep platform skills based only on a platform name.

When references are missing:

1. Identify the missing information.
2. Mark the proposed skill as incomplete or provisional.
3. Ask for the required reference.
4. Do not invent enterprise-specific configuration.
5. Do not present assumed platform behaviour as confirmed fact.

3.3 Technology inventory

The user should provide a file that identifies the technologies used or expected to be used by the solution.

The technology inventory may be provided as:

* Markdown;
* YAML;
* JSON;
* CSV;
* spreadsheet;
* architecture document;
* technical design document;
* dependency manifest;
* repository configuration;
* multiple supporting files.

The inventory should include, where available:

technologies:
  - name: "<technology-name>"
    category: "<technology-category>"
    purpose: "<project-purpose>"
    components:
      - "<component-or-service>"
    version: "<version-or-unknown>"
    environment:
      - "<environment>"
    status: "<approved|proposed|legacy|deprecated|unknown>"
    integration_role: "<integration-purpose>"
    security_relevance: "<security-context>"
    source_reference: "<authoritative-reference>"

Do not create technology skills for technologies that are unrelated to the project.

Do not assume that every dependency requires a separate skill.

⸻

4. Mandatory Discovery Phase

Before generating or modifying repository files, inspect the current agent ecosystem.

Analyze:

* .github/agents/;
* .github/skills/;
* .github/instructions/;
* .github/prompts/;
* .github/hooks/;
* .github/workflows/;
* repository governance files;
* referenced project documents;
* platform references;
* technology inventory;
* supporting architecture and implementation files.

Identify:

1. Existing agents and their responsibilities.
2. Existing skills and their actual content.
3. Files containing mixed responsibilities.
4. Architecture skills stored directly under the root skill folder.
5. Technology knowledge mixed into architecture skills.
6. Platform knowledge embedded inside generic architecture instructions.
7. Development instructions mixed with architecture responsibilities.
8. Duplicate or conflicting skills.
9. Broken or obsolete references.
10. Oversized agent files.
11. Missing responsibility boundaries.
12. Missing platform or technology expertise.
13. Unused or outdated files.
14. Existing content that should be preserved.

Do not classify files using filenames alone.

Read and classify files according to their actual content and responsibility.

⸻

5. Required Planning Gate

Before modifying repository files, produce a structured implementation plan containing:

1. Current-state architecture.
2. Identified problems.
3. Proposed hybrid agent design.
4. Proposed folder structure.
5. Platform classification.
6. Technology classification.
7. Existing skills to preserve.
8. Existing skills to move.
9. Existing skills to split.
10. Existing skills to merge.
11. Existing skills to retire.
12. New skills to create.
13. Agent references to update.
14. Prompt and instruction references to update.
15. Risks and compatibility concerns.
16. Validation strategy.
17. Migration sequence.

Do not modify repository files until the user approves the plan, unless the user explicitly requests immediate implementation.

⸻

6. Target Repository Structure

Refactor the repository toward the following logical structure:

.github/
├── agents/
│   ├── enterprise-architecture-solution.agent.md
│   ├── enterprise-platform-specialist.agent.md
│   ├── software-engineer.agent.md
│   └── supporting-agents/
│
├── skills/
│   ├── architecture/
│   │   ├── discovery/
│   │   ├── current-state-analysis/
│   │   ├── target-state-design/
│   │   ├── solution-architecture/
│   │   ├── integration-architecture/
│   │   ├── security-architecture/
│   │   ├── data-architecture/
│   │   ├── infrastructure-architecture/
│   │   ├── application-architecture/
│   │   ├── technical-design/
│   │   ├── architecture-review/
│   │   ├── non-functional-requirements/
│   │   ├── architecture-decisions/
│   │   ├── diagrams/
│   │   └── documentation/
│   │
│   ├── platforms/
│   │   ├── <platform-domain>/
│   │   │   └── <platform-name>/
│   │   └── shared-platform-capabilities/
│   │
│   ├── technology/
│   │   ├── programming-languages/
│   │   ├── scripting/
│   │   ├── frameworks/
│   │   ├── api-and-protocols/
│   │   ├── authentication-and-authorization/
│   │   ├── databases/
│   │   ├── messaging/
│   │   ├── containers-and-runtime/
│   │   ├── infrastructure-as-code/
│   │   ├── operating-systems/
│   │   ├── testing/
│   │   ├── observability/
│   │   ├── security-technologies/
│   │   └── shared-technology-capabilities/
│   │
│   ├── development/
│   │   ├── implementation-workflows/
│   │   ├── code-quality/
│   │   ├── code-review/
│   │   ├── refactoring/
│   │   └── test-automation/
│   │
│   ├── security/
│   ├── documentation/
│   ├── discovery/
│   ├── governance/
│   └── shared/
│
├── instructions/
│   ├── architecture/
│   ├── platforms/
│   ├── technology/
│   ├── development/
│   ├── security/
│   ├── governance/
│   └── repository/
│
├── prompts/
│   ├── architecture/
│   ├── platforms/
│   ├── technology/
│   ├── implementation/
│   ├── documentation/
│   └── review/
│
├── hooks/
│
└── workflows/

This is a logical target, not a requirement to generate every possible empty folder.

Create only folders that contain required artifacts.

⸻

7. Architecture Skill Migration

All architecture-related skills currently stored directly under .github/skills/ must be evaluated and moved into appropriate subfolders under:

.github/skills/architecture/

Architecture-related content includes:

* architecture discovery;
* project context analysis;
* current-state assessment;
* target-state design;
* architecture review;
* solution architecture;
* technical design;
* integration design;
* security architecture;
* data architecture;
* infrastructure architecture;
* application architecture;
* architecture diagrams;
* non-functional requirements;
* architecture decision records;
* HLD, LLD, TDD, ADR, and related documentation.

For each existing architecture skill:

1. Analyze its responsibility.
2. Select the correct architecture subfolder.
3. Move the skill when it contains one clear responsibility.
4. Split the skill when it combines multiple responsibilities.
5. Preserve valuable content.
6. Remove duplicated instructions.
7. Update every agent, prompt, instruction, workflow, and documentation reference.
8. Verify that the previous path is no longer used.
9. Document the migration.

Do not leave architecture skills unclassified directly under .github/skills/.

⸻

8. Platform Expertise Design

Platform-specific expertise must be stored under:

.github/skills/platforms/

Create a separate platform skill only when the platform requires distinct knowledge such as:

* product architecture;
* product components;
* administration model;
* governance model;
* APIs;
* authentication;
* authorization;
* deployment;
* integration;
* security controls;
* operational lifecycle;
* monitoring;
* recovery;
* compatibility;
* version-specific behaviour.

8.1 Platform categorization

Analyze the user-provided platform list and references.

Group platforms into appropriate enterprise domains.

Do not impose categories that are unsupported by the supplied references.

Example category pattern:

skills/platforms/
└── <enterprise-domain>/
    └── <normalized-platform-name>/
        └── SKILL.md

Use normalized, stable, lowercase folder names.

8.2 Platform skill generation workflow

For every requested platform:

1. Confirm that the user supplied a platform reference.
2. Identify the platform’s enterprise domain.
3. Analyze its architecture and components.
4. Identify how it is used in the project.
5. Identify supported integration mechanisms.
6. Identify APIs, SDKs, events, connectors, or protocols.
7. Identify authentication and authorization models.
8. Identify security requirements.
9. Identify deployment and runtime requirements.
10. Identify operational requirements.
11. Identify availability and recovery considerations.
12. Identify version-specific constraints.
13. Identify known unknowns.
14. Compare the platform with existing skills.
15. Reuse shared capabilities where possible.
16. Create a focused platform skill.
17. Link the skill to the Enterprise Platform Specialist.
18. Record authoritative references.

Do not copy general architecture instructions into every platform skill.

Do not copy general API, security, documentation, or troubleshooting workflows into every platform skill.

Reference reusable shared skills instead.

⸻

9. Technology Expertise Design

Technology-specific expertise must be stored under:

.github/skills/technology/

Technology skills describe technical building blocks used to design, implement, integrate, secure, deploy, test, and operate the solution.

Technology expertise may include:

* programming languages;
* scripting languages;
* frameworks;
* libraries;
* SDKs;
* APIs;
* protocols;
* authentication standards;
* database technologies;
* messaging technologies;
* runtimes;
* container technologies;
* infrastructure-as-code technologies;
* operating-system capabilities;
* testing technologies;
* observability technologies;
* security technologies;
* build and packaging technologies.

9.1 Technology skill generation workflow

For each technology identified in the user-provided technology inventory:

1. Confirm that it is used or proposed for the project.
2. Identify its purpose.
3. Identify associated components.
4. Identify its approved, proposed, legacy, deprecated, or unknown status.
5. Identify applicable versions.
6. Determine whether it requires distinct reusable expertise.
7. Determine whether an equivalent skill already exists.
8. Reuse or enhance an existing skill where appropriate.
9. Create a new technology skill only when justified.
10. Place it in the correct technology subfolder.
11. Link it to relevant architecture and engineering workflows.
12. Record the reference source.
13. Identify uncertainties and missing information.

Do not create one skill for every package, dependency, or minor library.

Create a skill when the technology materially affects:

* architecture;
* integration;
* security;
* deployment;
* scalability;
* maintainability;
* testing;
* availability;
* observability;
* project standards.

⸻

10. Platform Versus Technology Classification

Before creating any skill, classify the subject correctly.

Use:

.github/skills/platforms/

when the subject is an enterprise product, managed service, operational product suite, or vendor platform with its own:

* product architecture;
* administration model;
* governance model;
* deployment model;
* operational lifecycle;
* security controls;
* APIs;
* product-specific components.

Use:

.github/skills/technology/

when the subject is a technical building block such as:

* language;
* framework;
* protocol;
* library;
* SDK;
* runtime;
* database technology;
* messaging technology;
* operating-system capability;
* testing technology;
* observability standard.

When a subject could qualify as both:

1. Select one primary skill location.
2. Keep platform administration and governance in the platform skill.
3. Keep implementation-level technical guidance in a technology skill only when independently reusable.
4. Link related skills.
5. Do not duplicate the same content in both locations.
6. Document the classification decision.

⸻

11. Required Skill Structure

Every generated skill must use a consistent structure.

---
name: <normalized-skill-name>
description: <what the skill provides and when it should be used>
---
# Purpose
Explain the responsibility of the skill.
# Applicability
Define when the agent should load the skill.
# Exclusions
Define what is outside the skill's responsibility.
# Core Concepts
Describe the concepts the agent must understand.
# Project Context
Explain how the platform or technology is used in the current project.
# Architecture Relevance
Explain its impact on:
- system boundaries;
- dependencies;
- integration;
- security;
- availability;
- scalability;
- performance;
- maintainability;
- observability;
- deployment;
- recovery.
# Components
Describe relevant platform or technology components.
# Integration Patterns
Describe supported project-relevant integration patterns.
# Security Requirements
Cover:
- authentication;
- authorization;
- least privilege;
- encryption;
- secret management;
- input validation;
- audit logging;
- dependency security;
- sensitive-data handling.
# Operational Requirements
Cover:
- configuration;
- deployment;
- monitoring;
- logging;
- supportability;
- failure handling;
- recovery;
- compatibility.
# Constraints and Risks
Document confirmed limitations and project risks.
# Version Considerations
Separate stable concepts from version-specific behaviour.
# Interaction with Other Skills
Reference related architecture, platform, technology, development, security, or documentation skills.
# Authoritative References
List the user-provided references used to create or validate the skill.
# Assumptions
List assumptions explicitly.
# Unknowns
List missing information requiring confirmation.

⸻

12. Hybrid Routing Logic

The Enterprise Architecture Solution Agent must use the following workflow:

Receive user request
        │
        ▼
Identify architecture objective
        │
        ▼
Inspect available project context
        │
        ▼
Detect required platforms
        │
        ▼
Detect required technologies
        │
        ▼
Select relevant architecture skills
        │
        ├── Load relevant platform skills
        ├── Load relevant technology skills
        ├── Load security skills
        ├── Load discovery skills
        └── Load documentation skills
        │
        ▼
Collect structured specialist findings
        │
        ▼
Resolve constraints and trade-offs
        │
        ▼
Produce final architecture result

For every request, the agent must:

1. Identify the architecture task.
2. Identify explicitly mentioned platforms.
3. Identify implied platforms only when supported by project evidence.
4. Identify relevant technologies.
5. Compare technologies with the approved technology inventory.
6. Load only relevant skills.
7. Avoid loading the complete platform and technology catalog.
8. Identify missing platform references.
9. Identify technologies missing from the inventory.
10. Distinguish facts, assumptions, recommendations, and unknowns.
11. Resolve conflicting platform and technology constraints.
12. Retain ownership of the final architecture decision.

⸻

13. Enterprise Platform Specialist Responsibilities

Create or enhance the Enterprise Platform Specialist Agent.

The Platform Specialist must:

* detect platforms in the request;
* classify platforms by domain;
* locate corresponding platform skills;
* analyze vendor-specific and product-specific requirements;
* validate supported integration methods;
* identify authentication and authorization requirements;
* identify product constraints;
* identify deployment and operational requirements;
* identify compatibility and version concerns;
* identify missing references;
* return structured findings to the Architecture Agent.

The Platform Specialist must not:

* own the final architecture;
* independently approve technology choices;
* invent enterprise standards;
* write implementation code unless explicitly delegated;
* replace the Software Engineering Agent;
* embed detailed expertise for all platforms inside its agent file;
* load unrelated platform skills.

Its output should use this structure:

# Platform Findings
## Platforms Detected
## Relevant Skills Loaded
## Confirmed Capabilities
## Integration Options
## Security Requirements
## Deployment and Operational Constraints
## Compatibility and Version Considerations
## Risks
## Assumptions
## Unknowns
## Recommendations to the Architecture Agent
## Sources

⸻

14. Enterprise Architecture Agent Responsibilities

The Enterprise Architecture Solution Agent remains responsible for:

* requirements interpretation;
* architecture discovery;
* current-state analysis;
* target-state design;
* system boundaries;
* integration architecture;
* security architecture;
* data flows;
* non-functional requirements;
* technology trade-offs;
* architecture decisions;
* HLD, LLD, TDD, and ADR generation;
* diagram generation;
* architecture review;
* final recommendations.

The agent must use specialist findings as input, not as unreviewed final decisions.

⸻

15. Software Engineering Agent Boundary

The Software Engineering Agent remains responsible for:

* implementation code;
* automation scripts;
* API clients;
* unit tests;
* integration tests;
* code quality;
* refactoring;
* error handling;
* logging implementation;
* dependency management;
* implementation-specific design patterns.

Do not move general coding instructions into architecture or platform skills.

Architecture and technology skills may define constraints that implementation must follow, but they must not duplicate the complete software engineering workflow.

⸻

16. Reference and Evidence Rules

Use user-provided references as the primary source for project-specific platform and technology behaviour.

For every platform or technology skill:

* record the originating references;
* distinguish internal standards from external documentation;
* distinguish version-independent guidance from version-specific guidance;
* identify conflicting references;
* prefer current approved project documentation;
* identify deprecated content;
* mark unsupported assumptions;
* never include credentials, secrets, tokens, certificates, or sensitive production configuration.

Do not hardcode reference links into generic reusable templates.

Do not create recommendations solely from a reference title or filename.

Analyze the actual content before using it.

⸻

17. Security and Governance Requirements

Apply the following requirements throughout the refactoring:

* least-privilege access;
* secure secret management;
* no secrets in prompts, agents, skills, examples, or repositories;
* secure API authentication;
* input and output validation;
* dependency security;
* auditability;
* traceable architecture decisions;
* controlled production access;
* separation of duties;
* environment isolation;
* protected branches;
* pull-request review;
* CODEOWNERS protection for agent and skill files;
* secret scanning;
* dependency scanning;
* code scanning where applicable;
* version-controlled changes;
* authoritative reference tracking.

Generated content must not expose:

* passwords;
* private keys;
* certificates;
* tokens;
* internal credentials;
* production endpoints;
* restricted configuration values.

⸻

18. Migration Rules

For every existing skill, select one action:

* preserve;
* move;
* rename;
* split;
* merge;
* enhance;
* replace;
* retire.

Generate a migration table:

Current file	Current responsibility	Problem	Target location	Action	References to update

When moving or splitting skills:

1. Preserve valuable content.
2. Remove duplication.
3. Maintain clear responsibility boundaries.
4. Update agent references.
5. Update prompt references.
6. Update instruction references.
7. Update workflow references.
8. Update documentation references.
9. Check relative paths.
10. Verify that obsolete paths are removed.
11. Avoid breaking existing invocation workflows.

⸻

19. Required Deliverables

Produce the following deliverables.

Phase 1 — Analysis and plan

1. Current-state summary.
2. Current agent architecture diagram.
3. Existing skill inventory.
4. Skill responsibility classification.
5. Platform inventory.
6. Technology inventory.
7. Gap analysis.
8. Duplicate and mixed-concern analysis.
9. Proposed hybrid agent architecture.
10. Proposed folder structure.
11. Migration map.
12. Files to create, move, split, merge, preserve, or retire.
13. Risks and assumptions.
14. Approval request.

Phase 2 — Implementation after approval

1. Refactored Enterprise Architecture Solution Agent.
2. Enterprise Platform Specialist Agent.
3. Reorganized architecture skills under:
    .github/skills/architecture/
4. Platform skills under:
    .github/skills/platforms/
5. Technology skills under:
    .github/skills/technology/
6. Updated supporting skills.
7. Updated instructions.
8. Updated prompts.
9. Updated internal references.
10. Platform and technology classification report.
11. Final repository tree.
12. Validation report.

⸻

20. Validation Requirements

After implementation, validate that:

* the Enterprise Architecture Solution Agent remains the final architecture owner;
* platform knowledge is not embedded directly into the main architecture agent;
* platform skills are stored under skills/platforms/;
* technology skills are stored under skills/technology/;
* architecture skills are stored under skills/architecture/;
* no architecture skills remain incorrectly mixed at the root of skills/;
* no platform or technology content is unnecessarily duplicated;
* mixed skills have been split appropriately;
* all referenced paths exist;
* no obsolete paths remain;
* agents invoke only relevant skills;
* all 12–15 requested platforms are accounted for;
* platform skills are supported by user-provided references;
* relevant technologies from the inventory are accounted for;
* unsupported or missing technologies are identified;
* security boundaries are preserved;
* no sensitive information has been introduced;
* existing valid workflows remain functional.

Generate a validation table:

Validation check	Status	Evidence	Required correction

Use these statuses:

* Passed
* Passed with warning
* Failed
* Not validated
* Requires user input

⸻

21. Decision Rules

Follow these decision rules:

1. Preserve working content unless refactoring provides a clear benefit.
2. Prefer focused skills over oversized multi-purpose skills.
3. Prefer reusable capabilities over duplicated platform instructions.
4. Create platform skills only from supplied references.
5. Create technology skills only when project relevance is established.
6. Do not create a separate skill for every dependency.
7. Do not place all expertise in the main agent file.
8. Do not let specialist agents own final architecture decisions.
9. Do not modify files before approval unless explicitly authorized.
10. Do not silently delete existing files.
11. Do not invent missing enterprise standards.
12. Ask targeted questions only when missing information blocks correct implementation.
13. Do not repeat questions already answered by supplied references.
14. Use explicit assumptions when implementation can safely continue.
15. Keep the design extensible beyond the initial platform inventory.

⸻

22. Output Format

Use the following response structure.

Executive Summary

Current-State Assessment

Existing Agent Architecture

<ASCII architecture diagram>

Existing Skill Classification

Platform Inventory

Technology Inventory

Problems Identified

Proposed Hybrid Architecture

<ASCII target architecture diagram>

Proposed Repository Structure

<folder tree>

Proposed Skill Migration

Current file	Target location	Action	Reason

New Skills Required

Architecture Skills

Platform Skills

Technology Skills

Shared Skills

Agent Responsibility Matrix

Responsibility	Architecture Agent	Platform Specialist	Software Engineer	Supporting Agent

Files to Create or Modify

Security and Governance Review

Risks, Assumptions, and Unknowns

Implementation Sequence

Approval Required

End the planning phase by clearly asking the user to approve, reject, or modify the proposed plan.

Do not begin implementation until approval is received, unless immediate implementation was explicitly requested.

# Actionable workflow
1. Attach or reference the current `.github` agent ecosystem.
2. Provide the platform reference files for the approximately 12–15 platforms.
3. Provide the technology inventory file.
4. Run the meta-prompt in planning mode.
5. Review the proposed folder structure and migration map.
6. Approve implementation only after confirming the classifications.
# Best practices
Keep agent identity small, store reusable expertise in categorized skills, and load only the platform and technology knowledge relevant to the current request. Protect `.github/agents/`, `.github/skills/`, `.github/instructions/`, and `.github/prompts/` with `CODEOWNERS` and pull-request approval.
# Pitfalls
Avoid generating skills from names alone, creating one skill for every dependency, duplicating the same subject under both `platforms/` and `technology/`, or allowing the Platform Specialist to become a second competing architecture owner.
# Guided Link
**[Next: Create the platform-reference and technology-inventory templates]**
