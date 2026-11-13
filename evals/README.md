# Evals

Measure before changing the design. Correctness first, then tokens, then time.

## Setups

| Id | Setup |
| --- | --- |
| A | Package only |
| B | MCP server as it is |
| C | MCP server after the fixes |
| D | Skills only |
| E | Skills and MCP server |

## Tasks

One file per task in `tasks/`. See `tasks/README.md` for the format.

| Id | Task | Check |
| --- | --- | --- |
| T1 | Hypar: one free node between four supports | Node equals (0.5, 0.5, 0.5) |
| T2 | Grid net with corner supports and selfweight | Residuals at free nodes below 1e-6 |
| T3 | Net with sliding supports on curves | Supports lie on their curves |
| T4 | Thrust network for a vault | Form and force diagrams exist; equilibrium holds |
| T5 | Explain why the method is linear and when it fails | Rubric of five facts |
| T6 | Choose the package for a described problem | Matches `catalog/methods.md` |
| T7 | A call that changed between two package versions | Passes on the installed version |
| T8 | Unrelated Python task | Control |

## Record per run

Agent app and version, model, setup, task, uncached input tokens, cached input tokens, output tokens, model calls, tool calls, wall time, pass or fail.

Run each task at least five times per setup. Put results in `results/` as CSV.

## Runner

To be written.
