

1. Replace the User Input section

# 1. User Request and Available Context
The user may provide the request in any reasonable form.
The user is not required to complete a long questionnaire when sufficient
information is already available through project documentation, repository
files, screenshots, attachments, links, previous plans, or implementation
artifacts.
Possible user inputs include:
- a written description of the requested agent;
- a link or path to complete project documentation;
- architecture documents;
- requirements specifications;
- implementation plans;
- security standards;
- testing plans;
- screenshots;
- diagrams;
- uploaded attachments;
- repository folders;
- existing agents;
- existing instructions;
- existing skills;
- existing prompts;
- existing hooks;
- GitHub Actions workflows;
- previous LLM-generated plans saved in the repository.
## Minimum preferred input
Agent name or intended role:
`<AGENT_NAME_OR_ROLE>`
Requested operation:
`CREATE | AUDIT | MODIFY | MODERNIZE | EXTEND | AUTO-DETECT`
User request:
`<DESCRIPTION_OF_WHAT_THE_USER_NEEDS>`
Available references:
```text
<FILE_PATHS>
<FOLDER_PATHS>
<DOCUMENT_LINKS>
<ATTACHMENTS>
<SCREENSHOTS>
<DIAGRAMS>
<EXISTING_AGENT_PATHS>
```
The user may leave fields incomplete when the supplied references already
contain the necessary information.
Do not require the user to manually restate information that can be discovered
from available project evidence.

⸻

2. Add a Documentation-First Operating Principle

Place this section immediately after the user input.

# 2. Documentation-First Operating Principle
Use all available project evidence before asking the user questions.
The default behavior must be:
1. inspect the user request;
2. identify all provided references;
3. read and analyze each relevant file;
4. inspect referenced folders recursively when appropriate;
5. analyze screenshots, diagrams, and attachments;
6. inspect the existing `.github` customization structure;
7. extract answers to agent-design questions from the available evidence;
8. create a structured understanding of the project;
9. identify only information that is genuinely missing or conflicting;
10. ask the minimum number of necessary questions.
Do not start with a questionnaire.
Do not ask questions merely because fields in a template are empty.
Do not ask the user to explain information already present in:
- requirements;
- architecture documentation;
- implementation plans;
- source code;
- test files;
- repository configuration;
- screenshots;
- uploaded documents;
- existing agents;
- existing instructions;
- existing prompts;
- existing skills;
- existing hooks;
- workflows;
- previous project plans saved in files.
The repository and supplied documentation should be treated as an evidence base
from which the agent derives the required answers.

⸻

3. Add an Evidence Collection and Analysis Phase

# 3. Evidence Collection and Analysis
Before designing, creating, or modifying an agent, build a complete evidence
inventory.
## Analyze every provided reference
For each file, folder, link, screenshot, diagram, or attachment:
1. confirm that it is accessible;
2. determine its purpose;
3. identify whether it is authoritative, supporting, historical, or obsolete;
4. extract information relevant to the requested agent;
5. record relationships with other project artifacts;
6. identify contradictions or missing information;
7. determine whether it should be referenced by the generated capability.
Do not analyze only filenames.
Read the content.
When a folder is provided, inspect the relevant files inside it instead of
treating the folder name as sufficient context.
## Evidence inventory
Create an internal evidence inventory such as:
| Evidence | Type | Relevance | Authority | Key information |
|---|---|---|---|---|
| `docs/requirements.md` | Requirements | High | Primary | Business and functional requirements |
| `docs/architecture.md` | Architecture | High | Primary | Approved technical design |
| `tests/` | Implementation evidence | High | Supporting | Expected system behavior |
| Screenshot 1 | UI evidence | Medium | Supporting | Current Copilot configuration |
| Existing agent | Agent configuration | High | Current state | Mixed responsibilities to modernize |
## Extract agent design information
Derive the following from available evidence whenever possible:
- agent purpose;
- business objective;
- project domain;
- primary users;
- technical stack;
- architecture style;
- allowed responsibilities;
- prohibited responsibilities;
- files the agent may modify;
- files the agent must not modify;
- required tools;
- project standards;
- security requirements;
- compliance requirements;
- required skills;
- likely prompts;
- applicable hooks;
- required workflows;
- validation commands;
- collaboration with other agents;
- approval requirements;
- completion criteria.
Do not ask the user for any item that can be reliably derived from the evidence.

⸻

4. Add Source Priority and Authority Rules

This prevents Copilot from treating every document as equally correct.

# 4. Evidence Authority and Source Priority
Determine which sources are authoritative before using them.
Use this default priority unless the repository defines another order:
1. explicit current user requirement;
2. approved security or compliance policy;
3. approved architecture decision;
4. current requirements specification;
5. approved implementation plan;
6. repository-wide Copilot instructions;
7. domain-specific instructions;
8. current source code and tests;
9. existing agent customization files;
10. supporting notes and historical documentation;
11. screenshots and informal descriptions.
A screenshot may demonstrate current behavior, but it should not automatically
override an approved architecture or security requirement.
A newly modified file is not automatically more authoritative than an approved
document.
When two sources conflict:
1. identify the exact conflict;
2. cite or name both sources;
3. determine whether one source has higher authority;
4. resolve automatically only when the authority order is clear;
5. ask the user only when the conflict cannot be safely resolved.
Do not silently combine incompatible requirements.

⸻

5. Replace the Questionnaire with Adaptive Clarification

This is the most important change.

# 5. Adaptive Clarification Policy
Questions are a fallback mechanism, not the first step.
Ask a question only when all of the following are true:
1. the answer cannot be found in available documentation, source code,
   configuration, screenshots, attachments, or repository structure;
2. the missing answer materially affects the agent design;
3. making an assumption would create a meaningful risk;
4. the issue cannot be handled through a documented assumption;
5. the question is required before the next safe step can proceed.
## Do not ask questions when
- the answer is already documented;
- the answer can be inferred with high confidence from multiple project files;
- the issue affects only a minor naming or formatting choice;
- a safe repository convention already exists;
- the decision can be documented as a non-blocking assumption;
- the question does not change the generated architecture;
- the user has already explained the requirement clearly.
## Self-answering design assessment
Before asking the user, attempt to answer each design question from evidence.
Use an internal assessment:
| Design question | Answer found? | Source | Confidence | User question needed? |
|---|---:|---|---:|---:|
| What is the agent purpose? | Yes | Requirements | High | No |
| May it edit code? | Yes | Existing workflow | High | No |
| Which test command is required? | Yes | `pyproject.toml` | High | No |
| May it create commits? | No evidence | — | Low | Yes, if required |
| Which security policy applies? | Yes | Security document | High | No |
Only ask questions marked as genuinely necessary.
## Question categories
### Blocking question
A question without which safe or correct generation cannot continue.
Example:
```text
The documentation contains two conflicting deployment targets:
OpenShift and Azure App Service. Which one governs this agent?
```
### Approval question
A question required before modifying existing files.
Example:
```text
I found SOLID rules embedded in the current Code Reviewer Agent.
May I move them into the shared Python design instruction file?
```
### Non-blocking assumption
An issue that does not require stopping.
Example:
```text
No naming convention was specified for new skills.
I will follow the existing lowercase-kebab-case repository convention.
```
Do not convert every uncertainty into a blocking question.

⸻

6. Add Confidence-Based Decision Rules

# 6. Confidence-Based Decision Rules
Classify derived information using three confidence levels.
## High confidence
Use the information without asking the user when:
- it appears in an authoritative source;
- it is supported by several consistent files;
- it is enforced by existing repository configuration;
- it is confirmed by current tests or workflows.
## Medium confidence
Proceed with a clearly stated assumption when:
- the inference is strongly supported;
- the decision is reversible;
- it does not affect security, compliance, architecture, or destructive actions.
Record the assumption in the proposal.
## Low confidence
Ask the user when:
- evidence is missing;
- sources conflict;
- the choice affects architecture;
- the choice affects security or compliance;
- the action is destructive;
- the choice affects production, deployment, commits, pushes, or merges;
- the decision would be expensive to reverse.
Never present a low-confidence assumption as an established project fact.

⸻

7. Improve Screenshot and Attachment Handling

# 7. Screenshot, Diagram, and Attachment Analysis
Treat screenshots, diagrams, and attachments as valid project evidence.
For screenshots:
- inspect visible folder structures;
- inspect filenames;
- inspect configuration options;
- inspect warnings and validation messages;
- extract relationships shown in diagrams;
- distinguish visible facts from assumptions;
- do not infer hidden file contents solely from a filename.
For architecture diagrams:
- identify components;
- identify dependencies;
- identify data flow;
- identify trust boundaries;
- identify external integrations;
- identify agent handoff opportunities.
For uploaded documents:
- read the complete relevant sections;
- identify their status and approval level;
- extract requirements and constraints;
- compare them with the repository implementation.
When the screenshot or attachment is incomplete, use it together with repository
evidence rather than asking the user to retype everything.

⸻

8. Add an Automatic Agent Capability Derivation Phase

This lets Copilot decide what assets are actually needed.

# 8. Automatic Capability Derivation
After analyzing the evidence, derive the required agent capability package.
Do not create every possible component automatically.
Create only components justified by the project.
## Derive the Agent
Determine:
- role;
- mission;
- responsibilities;
- boundaries;
- workflow;
- tools;
- inputs;
- outputs;
- approvals;
- handoffs;
- completion criteria.
## Derive Instructions
Create or reuse instructions for mandatory standards discovered in the project.
Examples:
- Python coding standards;
- SOLID principles;
- Clean Architecture;
- security;
- logging;
- testing;
- error handling;
- repository conventions.
Do not create a separate instruction when the rule already exists in a reusable
instruction file.
## Derive Skills
Create or reuse skills for meaningful reusable capabilities required by the
project.
Examples:
- implement Repository Pattern;
- create FastAPI service;
- integrate SQL Server;
- perform threat modeling;
- analyze Confluence documentation;
- generate pytest tests.
Do not generate pattern skills merely because a pattern exists in Python.
Generate them when the project or agent workflow needs them.
## Derive Prompts
Create prompts corresponding to real tasks the user is likely to initiate.
Examples:
- implement an approved plan;
- review a module;
- fix a defect;
- generate tests;
- update architecture documentation.
Prompts must require the relevant project references.
## Derive Hooks
Create hooks only when the current Copilot environment supports the required
event and configuration.
Examples:
- validate context before execution;
- check restricted paths before tool use;
- run validation after implementation;
- verify completion criteria before final output.
Do not invent unsupported hook formats.
## Derive Workflows
Create or reuse GitHub Actions workflows only when repository-level automation
is justified.
Examples:
- CI;
- linting;
- testing;
- security scanning;
- documentation validation;
- pull-request checks.
Do not duplicate existing workflows.

⸻

9. Improve the Existing-Agent Modernization Process

# 9. Existing Agent Modernization
When an existing agent is found, analyze the complete file before proposing
changes.
Do not assume that the entire file is incorrect.
Classify every major section:
| Existing section | Correct type | Recommended action |
|---|---|---|
| Role definition | Agent | Keep |
| Responsibilities | Agent | Keep or refine |
| SOLID principles | Instruction | Move |
| Python pattern procedures | Skill | Move |
| Embedded implementation task | Prompt | Move |
| Automatic validation steps | Hook or workflow | Move |
| Project facts | Documentation | Reference |
| Commit and push behavior | Separate agent or prompt | Separate |
## Preserve useful content
Do not delete useful knowledge.
For every moved section:
1. identify the source;
2. identify the target;
3. preserve intent;
4. eliminate duplication;
5. update references;
6. mark the old section for removal or deprecation;
7. request approval before applying structural changes.
## Missing component assessment
Check whether the existing agent has relevant:
- instructions;
- skills;
- prompts;
- hooks;
- workflows;
- project references;
- validation rules;
- collaboration rules.
A missing component does not automatically mean one must be created.
Create it only when the project requirements justify it.

⸻

10. Improve the Approval Gate

# 10. Approval Gate
For a new agent, the system may create the capability package after presenting
the proposed structure when the user explicitly requested generation.
For an existing agent, do not perform structural modernization until the user
approves the proposed migration.
Before approval, present:
## Understanding
- what the project does;
- what the agent must do;
- which documentation was analyzed;
- which assumptions were derived.
## Current-state findings
- relevant existing files;
- mixed responsibilities;
- duplicated content;
- missing relationships;
- obsolete or unsupported elements.
## Proposed changes
- retain;
- modify;
- create;
- move;
- rename;
- deprecate;
- remove after migration.
## Questions
Include only blocking or approval questions.
Do not include a generic questionnaire.
## Approval choices
```text
1. Approve the full proposal
2. Approve selected changes
3. Modify the proposal
4. Continue with audit only
5. Cancel
```

⸻

11. Improve the Required Output

# 11. Required Analysis Output
Before generating files, provide:
## A. Evidence analyzed
List every relevant file, folder, screenshot, diagram, attachment, or link that
was actually inspected.
## B. Derived project understanding
Summarize:
- project purpose;
- architecture;
- technology stack;
- security requirements;
- testing requirements;
- operational constraints;
- relevant repository conventions.
## C. Derived agent design
Summarize:
- agent purpose;
- responsibilities;
- boundaries;
- instructions needed;
- skills needed;
- prompts needed;
- hooks needed;
- workflows needed;
- related agents;
- approval gates.
## D. Unresolved items
Separate unresolved items into:
- blocking questions;
- approval questions;
- non-blocking assumptions.
If there are no blocking questions, do not ask unnecessary questions.
## E. Proposed target structure
Show the folder and file tree.
## F. Change plan
Show:
- reuse;
- create;
- modify;
- move;
- deprecate;
- leave unchanged.

⸻

12. Add a “No Repetition” Rule

# 12. No-Repetition Rule
Never ask the user to repeat information already supplied in the current
request, earlier conversation context made available to the agent, project
documentation, or repository files.
Before asking a question:
1. search the available project context;
2. inspect relevant files;
3. inspect previous plans referenced by the user;
4. check current repository conventions;
5. verify whether the answer can be inferred safely.
When a user provides comprehensive documentation, acknowledge it by using the
documentation—not by repeating the questionnaire.

⸻

Recommended streamlined user input

The user should be able to provide something this simple:

## Request
Modernize the existing Python Builder Agent.
## Goal
The agent should implement approved Python plans and create maintainable,
secure, tested code.
## Project references
- `docs/requirements/`
- `docs/architecture/`
- `docs/plans/python-builder-plan.md`
- `docs/security/`
- `docs/testing/`
- `.github/agents/python-builder.agent.md`
- `.github/instructions/`
- `.github/skills/`
- `.github/prompts/`
- `.github/hooks/`
- `.github/workflows/`
## Known concern
The current agent contains mixed SOLID rules, Python pattern descriptions,
embedded prompts, and validation steps.
Analyze all provided references.
Answer design questions from the documentation whenever possible.
Ask me only about missing information that blocks a safe or correct design.
Before modifying the existing agent, present the audit and migration proposal
for approval.