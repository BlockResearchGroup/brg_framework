---
name: brg-methods
description: Chooses the right Block Research Group COMPAS package for a structural design task (form finding of nets and membranes, funicular vaults, masonry assessment, discrete element models). Use when the user describes a structural form finding or masonry problem without naming a package, or asks which BRG or COMPAS package to use.
license: MIT
metadata:
  validated-against: "catalog of 2026-11-13"
---

# Which BRG package

Pick the package from the table, then use that package's skill. Do not solve the problem by hand when a package does it.

| The user wants | Method | Package | Skill |
| --- | --- | --- | --- |
| Shape of a cable net, membrane or hanging network from force densities | Force density | `compas_fd` | `compas-fd` |
| The same with material stiffness, initial lengths or large displacements | Dynamic relaxation | `compas_dr` | `compas-dr` |
| A compression-only vault shape under vertical loads, with form and force diagrams | Thrust network analysis | `compas_tna` | `compas-tna` |
| Is an existing masonry vault safe: minimum or maximum thrust, minimum thickness | Thrust network optimisation | `compas_tno` | `compas-tno` |
| A masonry structure as separate blocks with contacts | Discrete element model | `compas_dem` | `compas-dem` |
| Form and force diagrams of a 2D truss or funicular structure, or its load path | Algebraic graph statics | `compas_ags` | `compas-ags` |

## Rules

1. If two rows fit, ask one short question to choose. Do not guess.
2. If no row fits, say so. Do not force a package onto the task.
3. Check that the package is installed before writing code: `python -c "import <package>; print(<package>.__version__)"`.
4. Dependencies: `compas_tna` needs `compas_fd`. `compas_tno` needs `compas_tna`. `compas_dem` needs `compas_model`.

The full package list is in `catalog/packages.toml` of `brg_framework`.
