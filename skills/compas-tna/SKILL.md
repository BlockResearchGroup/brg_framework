---
name: compas-tna
description: Form finding of compression-only funicular networks under vertical loads with thrust network analysis using the compas_tna Python package (form and force diagrams, horizontal and vertical equilibrium). Use when the user mentions TNA, thrust networks, funicular vaults, form and force diagrams, or imports compas_tna.
license: MIT
compatibility: Requires Python 3.9+ and the compas_tna package
metadata:
  package: compas_tna
  validated-against: "0.9.0"
  docs: https://blockresearchgroup.github.io/compas_tna
  repository: https://github.com/BlockResearchGroup/compas_tna
---

# compas_tna

Thrust network analysis for compression-only vaults under vertical loads. The package computes the diagrams and the equilibrium; this skill only says how to call it. It depends on `compas_fd` and `compas_cgal`.

## Before writing code

1. Check that the package is installed and which version: `python -c "import compas_tna; print(compas_tna.__version__)"`.
   If it is missing, install it: `pip install compas_tna`.
   This skill was checked against 0.9.0. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory. For each name you plan to use:
   `python -c "import compas_tna.equilibrium as m; help(m.vertical_from_zmax)"`.
3. Do not reimplement the method. Call the package.

## Entry points

| Task | Import |
| --- | --- |
| Form diagram | `from compas_tna.diagrams import FormDiagram` |
| Force diagram | `from compas_tna.diagrams import ForceDiagram` |
| Horizontal equilibrium | `from compas_tna.equilibrium import horizontal_nodal_numpy` |
| Vertical equilibrium for a target height | `from compas_tna.equilibrium import vertical_from_zmax` |
| Vertical equilibrium from force densities | `from compas_tna.equilibrium import vertical_from_q` |
| Relax boundary openings | `from compas_tna.equilibrium import relax_boundary_openings` |

## Workflow

1. Make the form diagram: `FormDiagram.from_mesh(mesh)` or `FormDiagram.from_lines(...)`.
2. Set supports and loads on the form diagram. Read `help(FormDiagram)` for the attribute names of the installed version.
3. Make the force diagram: `ForceDiagram.from_formdiagram(form)`.
4. Horizontal equilibrium: `horizontal_nodal_numpy(form, force, alpha=..., kmax=...)`.
5. Vertical equilibrium: `vertical_from_zmax(form, zmax)`. It returns the form diagram and the scale of the force diagram.

The API changed between 0.7, 0.8 and 0.9. Always check the installed version first.

## Check the result

Report the highest point of the thrust network and the scale returned by `vertical_from_zmax`. Check that form and force edges are parallel within tolerance after the horizontal step.

## Where to look next

- Documentation: https://blockresearchgroup.github.io/compas_tna
- Source and examples: https://github.com/BlockResearchGroup/compas_tna
- Theory, assumptions and limits: [references/theory.md](references/theory.md)
