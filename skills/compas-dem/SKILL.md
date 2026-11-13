---
name: compas-dem
description: Discrete element models of masonry with the compas_dem Python package (block models of arches, walls, domes and vaults, contacts between blocks, supports, equilibrium analysis). Use when the user mentions discrete elements, DEM, block models, masonry assemblies, contacts between blocks, or imports compas_dem.
license: MIT
compatibility: Requires Python 3.9+ and the compas_dem package
metadata:
  package: compas_dem
  validated-against: "0.6.0"
  docs: https://blockresearchgroup.github.io/compas_dem
  repository: https://github.com/BlockResearchGroup/compas_dem
---

# compas_dem

Discrete element models for masonry design and assessment. The package builds the block model and its contacts; this skill only says how to call it. It depends on `compas_model`, `compas_cgal` and `compas_libigl`.

## Before writing code

1. Check that the package is installed and which version: `python -c "import compas_dem; print(compas_dem.__version__)"`.
   If it is missing, install it: `pip install compas_dem`. If Python or COMPAS itself is missing, follow https://compas.dev first.
   This skill was checked against 0.6.0. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory. For each name you plan to use:
   `python -c "import compas_dem.models as m; help(m.BlockModel)"`.
3. Do not reimplement the method. Call the package.

## Entry points

| Task | Import |
| --- | --- |
| Block model | `from compas_dem.models import BlockModel` |
| Parametric geometry (arch, wall, dome, barrel vault) | `from compas_dem.templates import ArchTemplate` and others in `compas_dem.templates` |
| Viewer | `from compas_dem.viewer import DEMViewer` |
| Analysis back ends | modules in `compas_dem.analysis` |

## Workflow

1. Make a template: `ArchTemplate(rise=3, span=10, thickness=0.5, depth=0.5, n=50)`.
2. Make the model: `model = BlockModel.from_template(template)`.
3. Compute contacts: `model.compute_contacts(tolerance=0.001)`.
4. Mark supports: set `is_support = True` on the elements that are supports. In the arch example these are the nodes of degree 1: `model.graph.nodes_where(degree=1)`.
5. Show it: `DEMViewer(model)`, then `viewer.setup()` and `viewer.show()`. Skip the viewer in scripts that must run without a display.

The equilibrium analysis back ends need extra installs. Read the package README before using them.

## Check the result

Print the number of blocks, the number of contacts and the number of supports. A model with no contacts or no supports is not ready for analysis.

## Where to look next

- Documentation: https://blockresearchgroup.github.io/compas_dem
- Source and examples: https://github.com/BlockResearchGroup/compas_dem
- Theory, assumptions and limits: [references/theory.md](references/theory.md)
