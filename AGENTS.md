# AGENTS.md

Guidance for people and agents editing this repository.

## What this repository is

Content, not a library. No package imports it.

| Folder | Content | Edited by hand |
| --- | --- | --- |
| `theory/` | Method theory, one folder per method | yes |
| `catalog/` | Packages and the method table | yes, for now |
| `skills/` | Skills that combine several packages, such as `brg-methods`. Package skills here are drafts to move | yes |
| `server/` | The MCP server | yes |
| `evals/` | Tasks to measure tokens, time and correctness | yes |

## Rules

1. Write each thing once. Theory lives only in `theory/`.
2. A skill never copies a function signature. It tells the agent to read the installed package.
3. Skill names are lowercase with hyphens and equal the folder name: `compas-fd`.
4. Every code example is a file that runs. Say which package version it was run with.
5. Do not rename a heading in `theory/*/formulation.md` once something links to it.
6. Short sentences, plain words.

## Adding a package

1. Add a row to `catalog/packages.toml` and to `catalog/methods.md`.
2. Add `theory/<method>/` with the four pages and `teaching/`.
3. Add `skills/<package-name>/SKILL.md` in the package repository, not here. Copy an existing draft and change it.
4. Add a row to the table in `skills/brg-methods/SKILL.md`.
5. Install the package and run every import the skill names.

## Checks

```bash
cd server
uv sync --extra dev
uv run ruff check .
uv run pytest -q
```
