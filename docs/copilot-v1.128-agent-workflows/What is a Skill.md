Takeaway: Yes—GitHub Copilot Skills in VS Code 1.128 are conceptually very similar to Windsurf Skills, but Microsoft’s implementation is more integrated with the GitHub Copilot agent ecosystem (Agents, Instructions, Prompts, Hooks, and Skills working together).

Your screenshots are actually showing the direction GitHub is moving toward. Since you’ve already built custom AI agents for CyberArk and enterprise architecture, this feature will probably become one of the most valuable additions for your workflow.

⸻

What is a Skill?

Think of a Skill as teaching Copilot how to perform one specific job.

Instead of writing the same prompt every time:

“Review this code using security best practices…”

you create a Code Review Skill once.

Then any agent can reuse it.

You
 │
 │ "Review this PR"
 ▼
Agent
 │
 ▼
Code Review Skill
 │
 ├── checklist
 ├── output format
 ├── security rules
 ├── coding standards
 └── review workflow

⸻

Before VS Code 1.128

Previously you mostly had:

copilot-instructions.md

which contained things like

* coding style
* architecture rules
* naming conventions

Everything lived in one big instruction file.

⸻

After 1.128

GitHub splits responsibilities.

Agent
   │
   ├── Instructions
   ├── Skills
   ├── Prompts
   ├── Hooks
   └── Tools

Every part has one responsibility.

⸻

What each one does

1. Agent

The personality.

Example

Senior Software Architect
OR
CyberArk Engineer
OR
Python Developer

It decides

* how to think
* how to answer
* what tools to use

⸻

2. Instructions

Global rules.

Example

Always use Clean Architecture.
Always add logging.
Never use print().
Follow PEP8.
Use dependency injection.

These apply everywhere.

⸻

3. Skills ⭐

Reusable workflows.

Example

Security Review

contains

Review checklist
OWASP checks
Secrets scan
Dependency validation
Output template

Another example

SQL Optimization

contains

Index analysis
Execution plan
Performance checklist
Deadlock detection
Output template

Instead of writing this every day…

…the agent simply loads the skill.

⸻

4. Prompt

A reusable question.

Example

Generate Unit Tests
Explain this code
Create Architecture Diagram
Generate README

⸻

5. Hook

Automatic action.

Example

Every time you commit

↓

Run

lint
tests
format
security scan

without asking.

⸻

Is it the same as Windsurf?

Conceptually: yes.

Here’s a comparison:

Windsurf	GitHub Copilot 1.128
Rules	Instructions
Skills	Skills
Cascade	Agent
Memories	Context/Instructions
Workflows	Hooks
Prompt Library	Prompts

Very similar ideas.

⸻

Your Windsurf example

I noticed this structure:

.windsurf
skills
code-review
SKILL.md
review-checklist.md
review-output-template.md

That is actually a very good design.

code-review/
    SKILL.md
    review-checklist.md
    output-template.md

This is almost exactly how GitHub envisions Skills.

⸻

Example Skill

Imagine

skills
cyberark-platform

Inside

SKILL.md
platforms.md
vault-rules.md
CPM.md
PSM.md
PVWA.md
EVD.md

Whenever you ask

Explain why this CPM failed

the agent automatically loads everything.

No huge prompt required.

⸻

Another example

skills
sql-review

Contains

index-guide.md
performance-checklist.md
naming.md
security.md
output-template.md

Now you simply ask

Review this stored procedure

instead of writing

Review this SQL
Use performance
Check indexes
Check transactions
Check locking
Check SQL injection
...

⸻

This is exactly what you have already been building

Over the last few months you’ve created specialized resources such as:

* CyberArk knowledge
* SQL review logic
* GitHub commit assistant
* Architecture planning
* QA analysis
* Runbooks

Those map naturally to Skills.

For example:

skills/
    cyberark/
    sql-review/
    architecture/
    qa-analysis/
    github-commit/
    documentation/
    security-review/

Each skill encapsulates expertise for a specific task, while your agent chooses when to use it.

⸻

How I would organize your enterprise project

.github/
    instructions/
        copilot-instructions.md
        python.md
        architecture.md
    skills/
        cyberark/
        architecture/
        sql-review/
        github-pr/
        qa-analysis/
        runbook/
        documentation/
        security-review/
    prompts/
        create-pr.prompt.md
        generate-tests.prompt.md
        create-runbook.prompt.md
    agents/
        architect.agent.md
        developer.agent.md
        reviewer.agent.md

This separates:

* Instructions → always-on rules.
* Skills → reusable expertise and workflows.
* Prompts → reusable tasks.
* Agents → specialized AI personas.

⸻

Best practices

* Keep each Skill focused on one domain or workflow.
* Put checklists, templates, and reference documents inside the Skill folder.
* Keep global coding standards in Instructions, not in every Skill.
* Design Skills so multiple agents (Developer, Reviewer, Architect) can reuse them.

⸻

Common pitfalls

* ❌ Making one giant “everything” Skill. Smaller, focused Skills are easier for the agent to select and maintain.
* ❌ Duplicating the same rules across every Skill. Put shared rules in Instructions.
* ❌ Using a Skill as an agent. A Skill provides capabilities; the Agent decides when to use them.

My recommendation for you

Based on all of our previous conversations about your enterprise CyberArk projects, GitHub Copilot, and architecture work, I would gradually migrate your current Windsurf organization into the GitHub Copilot structure. The concepts are close enough that most of your existing Skills can be adapted rather than rewritten.

Once GitHub fully stabilizes this feature, you’ll have a single ecosystem where your custom Architect, Developer, QA, Security, and CyberArk agents can all share the same reusable Skills.

Next, I can show you how to convert your existing .windsurf/skills folder into the new .github/skills format recommended for VS Code 1.128, with a complete enterprise folder structure and examples for your CyberArk and architecture agents.