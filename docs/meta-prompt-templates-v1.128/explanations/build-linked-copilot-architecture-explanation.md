## Concise takeaway

Use the meta-prompt below to **inspect the existing `.github` directory first**, build an inventory of actual Copilot customization files, and then add only valid, minimal, bidirectional documentation links between agents, instructions, prompts, skills, hooks, workflows, and governance files.

# Universal meta-prompt: Link `.github` architecture components

Copy this prompt into GitHub Copilot **Plan mode** first.

---

## Best practices

Keep `copilot-instructions.md` focused on global standards. It should provide a map to other components, but it should not duplicate their complete content.

Agents should reference only the instructions and skills needed for their responsibilities. Prompts should remain usable independently when possible, and skills should contain reusable procedures rather than agent-specific personality.

Use links for discoverability and human maintenance. Use actual tool configuration, workflow steps, or hook configuration for runtime execution.

## Pitfalls

Do not assume that linking an instruction file inside an agent Markdown file automatically loads it. GitHub Copilot behavior depends on the supported customization mechanism and current product surface; the link itself primarily documents the relationship.

Do not create links to empty folders containing only `.gitkeep`. Do not invent missing agent or skill filenames. Do not create a highly coupled graph in which one small file change requires updates to every customization file.

### Guided Links

**[Apply in Plan mode]** → inventory and relationship proposal · **[Apply after approval]** → add validated links and architecture documentation · **[Next phase]** → create a workflow that automatically checks for broken `.github` references
