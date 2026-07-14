### Create the base directories.

```bash
mkdir -p \
  .github/{agents,instructions,prompts,skills,hooks/scripts,workflows,ISSUE_TEMPLATE} \
  docs/{architecture,releases/2026,guides,decisions} \
  research/{official,community,raw,normalized} \
  templates/{agents,hooks,instructions,prompts,skills,release-notes} \
  automation/{collectors,parsers,analyzers,reporters} \
  config \
  data/{snapshots,state,reports} \
  tests/{unit,integration,fixtures} \
  scripts
```


###  Add governance documents.

```bash
README.md
SECURITY.md
CONTRIBUTING.md
.github/CODEOWNERS
.github/PULL_REQUEST_TEMPLATE.md
```