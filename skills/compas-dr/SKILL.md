---
name: compas-dr
description: Form finding and analysis of networks of axial-force members with the dynamic relaxation method using the compas_dr Python package. Use when the user mentions dynamic relaxation, DR, form finding with material stiffness or initial lengths, or imports compas_dr.
license: MIT
compatibility: Requires Python 3.9+ and the compas_dr package
metadata:
  package: compas_dr
  validated-against: "0.3.1"
  docs: https://blockresearchgroup.github.io/compas_dr
  repository: https://github.com/BlockResearchGroup/compas_dr
---

# compas_dr

Constrained form finding with dynamic relaxation. The package runs the iteration; this skill only says how to call it.

## Before writing code

1. Check that the package is installed and which version: `python -c "import compas_dr; print(compas_dr.__version__)"`.
   If it is missing, install it: `pip install compas_dr`. If Python or COMPAS itself is missing, follow https://compas.dev first.
   This skill was checked against 0.3.1. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory. For each name you plan to use:
   `python -c "import compas_dr.solvers as m; help(m.dr_numpy)"`.
3. Do not reimplement the method. Call the package.

## Entry points

| Task | Import |
| --- | --- |
| Dynamic relaxation with numpy | `from compas_dr.solvers import dr_numpy` |
| Dynamic relaxation with constraints | `from compas_dr.solvers import dr_constrained_numpy` |
| Input and result data | `from compas_dr.numdata import InputData`, `ResultData` |

## Workflow

1. Read `help(compas_dr.numdata.InputData)` and build the input data object from it.
2. Call `dr_numpy(indata, kmax=..., tol1=..., tol2=...)`. It returns a result data object.
3. Read the fields of the result with `help(compas_dr.numdata.ResultData)`.

`dr_numpy` iterates until the residual tolerance `tol1` or the displacement tolerance `tol2` is met, or `kmax` is reached.

## Check the result

Report whether the solver stopped on a tolerance or on `kmax`. A run that stops on `kmax` has not converged.

## Where to look next

- Documentation: https://blockresearchgroup.github.io/compas_dr
- Source and examples: https://github.com/BlockResearchGroup/compas_dr
- Theory, assumptions and limits: [references/theory.md](references/theory.md)
