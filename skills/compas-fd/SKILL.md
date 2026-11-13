---
name: compas-fd
description: Form finding with the force density method using the compas_fd Python package (cable nets, membranes, hanging and funicular networks, constrained supports, selfweight). Use when the user mentions force density, FDM, form finding of nets, or imports compas_fd.
license: MIT
compatibility: Requires Python 3.9+ and the compas_fd package
metadata:
  package: compas_fd
  validated-against: "0.5.4"
  docs: https://blockresearchgroup.github.io/compas_fd
  repository: https://github.com/BlockResearchGroup/compas_fd
---

# compas_fd

Constrained form finding with the force density method. The package solves the equilibrium; this skill only says how to call it.

## Before writing code

1. Check that the package is installed and which version: `python -c "import compas_fd; print(compas_fd.__version__)"`.
   If it is missing, install it: `pip install compas_fd`.
   This skill was checked against 0.5.4. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory. For each name you plan to use:
   `python -c "import compas_fd.solvers as m; help(m.fd_numpy)"`.
3. Do not reimplement the method. Call the package.

## Entry points

| Task | Import |
| --- | --- |
| Equilibrium of a network | `from compas_fd.solvers import fd_numpy` |
| Equilibrium with sliding supports | `from compas_fd.solvers import fd_constrained_numpy` |
| Constraints on vertices | `from compas_fd.constraints import Constraint` |
| Selfweight from tributary areas | `from compas_fd.loads import SelfweightCalculator` |

## Workflow

1. Build `vertices`, `fixed`, `edges` and `forcedensities`. Add `loads` for selfweight or other nodal loads.
2. Call `fd_numpy(vertices=..., fixed=..., edges=..., forcedensities=..., loads=...)`. All arguments are keyword-only.
3. Read `result.vertices`, `result.forces`, `result.lengths` and `result.residuals`.

Conventions: positive force density is tension, negative is compression. Gravity loads point in negative Z. For sliding supports pass one constraint or `None` per vertex to `fd_constrained_numpy`.

## Check the result

Print the height range and the force range. Check that `result.residuals` is close to zero at the free vertices.

## Where to look next

- Documentation: https://blockresearchgroup.github.io/compas_fd
- Source and examples: https://github.com/BlockResearchGroup/compas_fd
- Theory, assumptions and limits: [references/theory.md](references/theory.md)
