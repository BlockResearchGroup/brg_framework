---
name: brg-methods
description: Chooses the right Block Research Group COMPAS package for a structural design task (form finding of nets and membranes, funicular vaults, masonry assessment, discrete element models, graphic statics) and points to its repository and docs. Use when the user describes a structural form finding or masonry problem, names a BRG package, or asks which BRG or COMPAS package to use.
license: MIT
metadata:
  catalog: "2026-11-13"
---

# Which BRG package

Pick the package from the table. Then let the package do the work. Do not solve the problem by hand.

| The user wants | Method | Package | Repository | Docs |
| --- | --- | --- | --- | --- |
| Shape of a cable net, membrane or hanging network from force densities | Force density | `compas_fd` | https://github.com/BlockResearchGroup/compas_fd | https://blockresearchgroup.github.io/compas_fd |
| The same with material stiffness, initial lengths or large displacements | Dynamic relaxation | `compas_dr` | https://github.com/BlockResearchGroup/compas_dr | https://blockresearchgroup.github.io/compas_dr |
| A compression-only vault under vertical loads, with form and force diagrams | Thrust network analysis | `compas_tna` | https://github.com/BlockResearchGroup/compas_tna | https://blockresearchgroup.github.io/compas_tna |
| Is a masonry vault safe: minimum or maximum thrust, minimum thickness | Thrust network optimisation | `compas_tno` | https://github.com/BlockResearchGroup/compas_tno | https://blockresearchgroup.github.io/compas_tno |
| A masonry structure as separate blocks with contacts | Discrete element model | `compas_dem` | https://github.com/BlockResearchGroup/compas_dem | https://blockresearchgroup.github.io/compas_dem |
| Form and force diagrams of a 2D truss or funicular structure, or its load path | Algebraic graph statics | `compas_ags` | https://github.com/BlockResearchGroup/compas_ags | https://blockresearchgroup.github.io/compas_ags/latest |

## Then

1. If two rows fit, ask one short question to choose. If no row fits, say so.
2. Check that the package is installed: `python -c "import <package>; print(<package>.__version__)"`.
   If it is missing: `pip install <package>`. If Python or COMPAS itself is missing, follow https://compas.dev first.
3. If the package ships its own skill or an `AGENTS.md`, follow it.
4. If not, read the package: its README, `docs/examples/`, `tests/`, and `help()` on the installed names. Trust the installed version over anything you remember.
5. Use the package's own examples as the starting point.

## Theory

Theory, assumptions and limits of each method are in `theory/<method>/` of https://github.com/BlockResearchGroup/brg_framework.
