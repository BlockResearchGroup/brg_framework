---
name: compas-ags
description: Two-dimensional graphic statics with the compas_ags Python package (reciprocal form and force diagrams of trusses and funicular structures, bi-directional updates, constraints, load-path optimisation). Use when the user mentions graphic statics, AGS, form and force diagrams of a 2D truss, load path, or imports compas_ags.
license: MIT
compatibility: Requires Python 3.9+ and the compas_ags package
metadata:
  package: compas_ags
  validated-against: "1.3.3"
  docs: https://blockresearchgroup.github.io/compas_ags/latest
  repository: https://github.com/BlockResearchGroup/compas_ags
---

# compas_ags

Computational graphic statics in 2D: algebraic graph statics, its bi-directional version and load-path optimisation. The package builds and updates the diagrams; this skill only says how to call it. It depends on `compas` and `sympy`.

## Before writing code

1. Check that the package is installed and which version: `python -c "import compas_ags; print(compas_ags.__version__)"`.
   If it is missing, install it: `pip install compas_ags`.
   This skill was checked against 1.3.3. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory. For each name you plan to use:
   `python -c "import compas_ags.ags as m; help(m.graphstatics)"`.
3. Do not reimplement the method. Call the package.

## Entry points

| Task | Import |
| --- | --- |
| Graph of the structure | `from compas_ags.diagrams import FormGraph` |
| Form diagram | `from compas_ags.diagrams import FormDiagram` |
| Force diagram | `from compas_ags.diagrams import ForceDiagram` |
| Updates between the diagrams | `from compas_ags.ags import graphstatics` |
| Load-path optimisation | `from compas_ags.ags import loadpath` |
| Constraints | `from compas_ags.ags import constraints` |
| Viewer | `from compas_ags.viewer import AGSViewer` |

## Workflow

1. Make the graph: `FormGraph.from_lines(lines)` or `FormGraph.from_obj(path)`. The sample `.obj` files used in the documentation are in the `data/` folder of the repository. A pip install does not include them, so `compas_ags.get(...)` fails there.
2. Make the form diagram: `form = FormDiagram.from_graph(graph)`.
3. Make the force diagram: `force = ForceDiagram.from_formdiagram(form)`.
4. Set the force in the independent edges, for example `form.edge_force(0, -3.0)`.
5. Update the force densities: `graphstatics.form_update_q_from_qind(form)`.
6. Update the force diagram: `graphstatics.force_update_from_form(force, form)`.
7. To drive the form from a changed force diagram, use `graphstatics.form_update_from_force(form, force)`.

This is 2D only. For 3D vaults use `compas_tna`.

## Check the result

Print the edge forces of the form diagram. Check that every form edge is parallel to its force edge.

## Where to look next

- Documentation: https://blockresearchgroup.github.io/compas_ags/latest
- Source and examples: https://github.com/BlockResearchGroup/compas_ags
- Theory, assumptions and limits: [references/theory.md](references/theory.md)
