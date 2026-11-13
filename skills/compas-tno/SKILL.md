---
name: compas-tno
description: Assessment of masonry vaults by finding admissible thrust networks with nonlinear optimisation using the compas_tno Python package (minimum and maximum thrust, minimum thickness, settlements, maximum load). Use when the user mentions TNO, thrust network optimisation, admissible thrust networks, safety of masonry vaults, or imports compas_tno.
license: MIT
compatibility: Requires Python 3.9+ and the compas_tno package
metadata:
  package: compas_tno
  validated-against: "0.4.0"
  docs: https://blockresearchgroup.github.io/compas_tno
  repository: https://github.com/BlockResearchGroup/compas_tno
---

# compas_tno

Masonry assessment by optimisation of funicular thrust networks. The package sets up and solves the optimisation; this skill only says how to call it. It depends on `compas_tna` and `cvxpy`.

## Before writing code

1. Check that the package is installed and which version: `python -c "import compas_tno; print(compas_tno.__version__)"`.
   If it is missing, install it: `pip install compas_tno`.
   This skill was checked against 0.4.0. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory. For each name you plan to use:
   `python -c "import compas_tno.problems as m; help(m)"`.
3. Do not reimplement the method. Call the package.

## Entry points

The package is being refactored for COMPAS 2, so names move between versions. Do not rely on a fixed list.

List what the installed version offers:

`python -c "import compas_tno, pkgutil; print([m.name for m in pkgutil.iter_modules(compas_tno.__path__)])"`

In 0.4.0 the modules are `algorithms`, `analysis`, `optimisers`, `problems`, `solvers` and `utilities`.

## Workflow

1. Tell the user that this package is being refactored and that older tutorials may not match.
2. Find the example closest to the task in the documentation: minimum and maximum thrust, minimum thickness, settlement, maximum load.
3. Adapt that example. Check every imported name against the installed version with `help()`.

## Check the result

Report the solver status and the objective value. Do not report a result from a run that did not converge.

## Where to look next

- Documentation: https://blockresearchgroup.github.io/compas_tno
- Source and examples: https://github.com/BlockResearchGroup/compas_tno
- Theory, assumptions and limits: [references/theory.md](references/theory.md)
