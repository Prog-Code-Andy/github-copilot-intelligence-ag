Takeaway: A good enterprise GitHub Copilot customization separates Agents (who), Instructions (rules), Skills (expertise), and Prompts (reusable tasks). This keeps everything modular and easy to maintain.

Recommended folder structure

.github/
│
├── agents/
├── instructions/
├── skills/
├── prompts/
├── hooks/
└── workflows/      (GitHub Actions)

⸻

1. agents/

Each file defines a specialized AI persona.

agents/
│
├── architect.agent.md
├── developer.agent.md
├── reviewer.agent.md
├── qa.agent.md
├── cyberark.agent.md
└── documentation.agent.md

File	Purpose
architect.agent.md	Enterprise solution architecture
developer.agent.md	Feature implementation
reviewer.agent.md	PR and code reviews
qa.agent.md	Testing and validation
cyberark.agent.md	CyberArk/PAM specialist
documentation.agent.md	Documentation generation

⸻

2. instructions/

Always-loaded project rules.

instructions/
│
├── copilot-instructions.md
├── architecture.md
├── python.md
├── sql.md
├── security.md
├── logging.md
├── testing.md
└── naming.md

File	Purpose
copilot-instructions.md	Global project rules
architecture.md	Clean Architecture standards
python.md	Python coding conventions
sql.md	SQL standards
security.md	Security requirements
logging.md	Logging policy
testing.md	Unit/integration testing rules
naming.md	Naming conventions

⸻

3. skills/

Each folder contains one reusable capability.

skills/
│
├── architecture/
├── cyberark/
├── sql-review/
├── github-pr/
├── security-review/
├── qa-analysis/
├── runbook/
├── documentation/
└── code-review/

Folder	Purpose
architecture	System design workflows
cyberark	CyberArk expertise
sql-review	SQL optimization
github-pr	PR creation and review
security-review	Security analysis
qa-analysis	Test analysis
runbook	Operational procedures
documentation	Documentation generation
code-review	General code reviews

⸻

Example Skill

skills/
└── code-review/
    │
    ├── SKILL.md
    ├── review-checklist.md
    ├── coding-standards.md
    ├── security-checklist.md
    ├── output-template.md
    └── examples.md

File	Purpose
SKILL.md	Skill entry point and description
review-checklist.md	Review steps
coding-standards.md	Coding guidelines
security-checklist.md	Security checks
output-template.md	Standard review format
examples.md	Example reviews

⸻

4. prompts/

Reusable prompt templates.

prompts/
│
├── create-pr.prompt.md
├── generate-tests.prompt.md
├── create-runbook.prompt.md
├── explain-code.prompt.md
├── refactor.prompt.md
├── create-diagram.prompt.md
└── optimize-sql.prompt.md

File	Purpose
create-pr.prompt.md	Generate PR descriptions
generate-tests.prompt.md	Create unit tests
create-runbook.prompt.md	Generate operational runbooks
explain-code.prompt.md	Explain source code
refactor.prompt.md	Refactor code
create-diagram.prompt.md	Generate architecture diagrams
optimize-sql.prompt.md	SQL optimization

⸻

5. hooks/

Automatic workflows triggered by events.

hooks/
│
├── pre-commit.md
├── post-commit.md
├── pre-pr.md
├── post-pr.md
└── release.md

File	Purpose
pre-commit.md	Checks before commit
post-commit.md	Actions after commit
pre-pr.md	Validate before PR
post-pr.md	Actions after merge
release.md	Release workflow

⸻

6. workflows/

GitHub Actions.

workflows/
│
├── ci.yml
├── cd.yml
├── security.yml
├── release.yml
└── dependency-scan.yml

File	Purpose
ci.yml	Continuous Integration
cd.yml	Deployment
security.yml	Security scanning
release.yml	Releases
dependency-scan.yml	Dependency scanning

⸻

Overall relationship

.github/
│
├── agents/          ← WHO performs the task
│
├── instructions/    ← Global project rules
│
├── skills/          ← HOW to perform a specialized task
│
├── prompts/         ← Reusable user requests
│
├── hooks/           ← Automatic actions
│
└── workflows/       ← GitHub Actions automation

Recommendation for your enterprise projects

Given your CyberArk and enterprise architecture work, I would organize the repository around these core Skills:

* Architecture
* CyberArk
* Python
* SQL Review
* Security Review
* GitHub PR
* QA Analysis
* Runbooks
* Documentation

This structure is scalable and allows multiple agents (Architect, Developer, Reviewer, QA) to reuse the same Skills while sharing common Instructions.