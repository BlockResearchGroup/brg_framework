# Theory

One folder per method. This is the only place where theory is written by hand.
The skills and the MCP server read from here.

| Folder | Method | Used by |
| --- | --- | --- |
| `fd/` | Force density | `compas_fd` |
| `dr/` | Dynamic relaxation | `compas_dr` |
| `tna/` | Thrust network analysis | `compas_tna` |
| `tno/` | Thrust network optimisation | `compas_tno` |
| `dem/` | Discrete element models | `compas_dem` |
| `ags/` | Algebraic graph statics | `compas_ags` |

## Files in each folder

| File | Content |
| --- | --- |
| `index.md` | What the method is, when to use it, assumptions, limits |
| `formulation.md` | Equations, each with a stable id |
| `glossary.md` | Terms |
| `references.md` | Papers and books |
| `teaching/` | Exercises, notebooks, slides |

## Page header

Each page starts with:

```text
---
id: fd/index
summary: One sentence that says what this page answers.
packages: [compas_fd]
---
```

The force density pages already exist in `server/src/brg_mcp/fd/`. Move them here when the server is changed to read from this folder.
