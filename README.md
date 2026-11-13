# brg_framework

Shared knowledge for the Block Research Group Python packages: theory, a catalog of packages, agent skills and one MCP server.

Status: in progress. Skills and server exist; theory and hooks are still to be written.

This is the lab layer on top of COMPAS. Installing Python and COMPAS itself is covered by [COMPAS](https://compas.dev). This repository adds BRG theory and points to the individual BRG packages.

## Goal

Help coding agents (Claude Code, Codex, Kimi Code, Antigravity) find the right theory and write correct Python with the right BRG package and version.

## In one line

Write the knowledge once as Markdown. Coders get it as Agent Skills, learners get it through one hosted MCP server.

All content lives in this repository. It reaches people in three ways:

| Who | How they get it | Folder |
| --- | --- | --- |
| Coders using Claude Code, Codex, Kimi Code or Antigravity | Skills installed in their project: each package's own skill, plus the shared ones from here | `skills/` in each package and here |
| Students and anyone learning in a chat app | Hosted MCP server, each student adds it once to their own account | `server/` |
| Everyone else | Website | `theory/`, built with `mkdocs.yml` |

## Two kinds of users

The content is the same for both. Only the door differs.

| | Learners | Coders |
| --- | --- | --- |
| Who | Students and others who want to read theory, see examples and do exercises. They do not write a project | People writing Python with BRG packages |
| What they ask | "Explain force density." "Show me a hypar example." "Give me exercise 2." | "Form-find this net with compas_fd." "Why does my solver fail?" |
| Door | The MCP server | Skills on disk |
| Why | Nothing to install. Always the newest text. The full answer appears in the chat, not a link | Matches the installed package version. Works offline. The agent reads only what it needs |
| Extras | Links to notebooks on the teaching website | Scripts and optional hooks that copy examples as files |

A person can be both. A student who starts to code installs the skills as well.

### Install for learners

One step: add the hosted MCP server to your own account. Nothing else.

**In a chat app (Claude, ChatGPT, on web or phone).** Add it as a custom connector:

```text
https://<to be decided>/mcp
```

**In Antigravity.** Add the server to `~/.gemini/config/mcp_config.json`.

Hosted:

```json
{
  "mcpServers": {
    "brg": { "serverUrl": "https://<to be decided>/mcp" }
  }
}
```

Local, only for developing the server (needs [uv](https://docs.astral.sh/uv/) and a clone of this repository):

```json
{
  "mcpServers": {
    "brg": {
      "command": "uv",
      "args": ["--directory", "/path/to/brg_framework/server", "run", "brg-mcp"]
    }
  }
}
```

Then ask in plain words, for example "explain the force density method" or "show the hypar example". The answer is the BRG text itself, shown in the chat.

### Install for coders

Two steps, inside the project where you write code.

1. Install the package you need. For Python and COMPAS itself, follow the [COMPAS installation guide](https://compas.dev) first.

```bash
pip install compas_fd
```

2. Install the skill of that package, and the shared skills from here:

```bash
npx skills add BlockResearchGroup/compas_fd
npx skills add BlockResearchGroup/brg_framework
```

Or copy the `skills/*` folders by hand:

| Agent app | Copy into |
| --- | --- |
| Claude Code | `.claude/skills/` |
| Codex, Kimi Code, Antigravity | `.agents/skills/` |

Optional third step, for fast copying of examples:

```bash
brg hooks install
```

Coders do not need the MCP server. They can add it too if they want the teaching material in the same session.

### What each user gets

| Content | Learners, through MCP | Coders, through skills |
| --- | --- | --- |
| Theory: explanation, assumptions, limits | yes | yes, loaded when needed |
| Glossary and references | yes | yes, loaded when needed |
| Exercises and notebooks | yes | no |
| Examples to read | yes | yes |
| Examples copied into the project as files | no | yes |
| API of the installed version | no | yes |
| Pitfalls and conventions for a package | no | yes |

## The five rules

1. **One source.** Knowledge is Markdown in git. Skill references, website pages and server replies are generated from it or read it directly. Nothing is edited twice.
2. **Each package carries its own skill. This repository holds only skills that span several packages**, such as choosing a method. Each is a folder with a `SKILL.md` that follows the [Agent Skills specification](https://agentskills.io/specification). The `name` is lowercase with hyphens and equals the folder name: `compas-fd`, not `compas_fd`. The `description` says what it does and when to use it. Keep the body under 500 lines.
3. **The installed package is the API truth.** A skill never copies signatures. It tells the agent to check the installed version and read the docstring.
4. **Every example is a real `.py` file that CI runs** against a pinned package version.
5. **One MCP server, with two tools at most.** For learners it returns the full BRG text, and the chat shows that text as the answer, not a link.

## What belongs where

This repository is the lab layer and the pointer. It holds the theory, the catalog and the skills that span several packages. Each package holds its own code, docs, examples and its own skill.

| Content | Home |
| --- | --- |
| Method theory: derivations, assumptions, limits, glossary, papers | `brg_framework` |
| Teaching: exercises, notebooks, slides | `brg_framework` |
| Catalog of packages (generated from each package's manifest) | `brg_framework` |
| Method-choice skill | `brg_framework` |
| MCP server | `brg_framework`, in `server/` |
| API reference: source and docstrings | the package |
| Examples and the tests that run them | the package |
| Package skill: how to use that one package | the package, in `skills/` |
| Skills that combine several packages | `brg_framework`, in `skills/` |
| `AGENTS.md` for contributors | the package |

No package imports `brg_framework`. It is content, not a runtime dependency.

## Layout of this repository

```text
brg_framework/
├── AGENTS.md                  # for people and agents editing this repository
├── theory/
│   ├── fd/                    # force density
│   │   ├── index.md           # what, when, assumptions, limits
│   │   ├── formulation.md     # equations with stable ids
│   │   ├── glossary.md
│   │   ├── references.md
│   │   └── teaching/          # exercises, notebooks, slides
│   └── tna/ ...
├── catalog/
│   ├── packages.toml          # generated from each package's manifest
│   └── methods.md             # method to package decision table
├── skills/
│   ├── brg-methods/SKILL.md   # which method, which package
│   └── ...                    # other skills that combine several packages
│                              # compas-fd/ etc. are drafts, to move into their packages
├── server/                    # the MCP adapter (FastMCP), optional install
├── evals/                     # tasks, checkers, runner
└── mkdocs.yml                 # website built from theory/ and catalog/
```

## Layout of each package

Each package carries its own skill, so it is versioned and released with the code.

```text
compas_fd/
├── AGENTS.md                  # build, test, lint, conventions
├── skills/
│   └── compas-fd/
│       ├── SKILL.md           # how to use this package
│       └── references/        # links to theory in brg_framework
├── docs/
│   ├── examples/*.py          # one runnable file per example
│   └── trace.toml             # theory id, symbol, example, test
└── tests/
    └── test_examples.py       # runs every docs/examples/*.py
```

## Skill template

```text
---
name: compas-fd
description: Form finding with the force density method using the compas_fd Python package (cable nets, membranes, hanging and funicular networks, constrained supports, selfweight). Use when the user mentions force density, FDM, form finding of nets, or imports compas_fd.
license: MIT
compatibility: Requires Python 3.9+ and the compas_fd package
metadata:
  package: compas_fd
  validated-against: "0.5.4"
---

# compas_fd

1. Check the installed version: `python -c "import compas_fd; print(compas_fd.__version__)"`.
   This skill was checked against 0.5.4. If the version differs, trust the installed docstrings over this file.
2. Read the API from the installed package, not from memory:
   `python -c "from compas_fd.solvers import fd_numpy; help(fd_numpy)"`.
3. Build `vertices`, `fixed`, `edges` and `forcedensities` first. Add `loads` for selfweight.
4. Positive force density is tension, negative is compression. Gravity loads point in negative Z.
5. For sliding supports use `fd_constrained_numpy`, with one constraint or `None` per vertex.
6. Verify before answering: print the height range and check `result.residuals` at the free vertices.

Theory and limits: references/theory.md
Checked examples: references/examples.md
```

`validated-against` is a BRG convention inside the standard `metadata` map. The specification has no version field.

## Linking theory to code

Write each link once, as data, and let CI check it. Never write a line number or a `main` link by hand.

```toml
[[trace]]
theory  = "fd/formulation#equilibrium"
symbol  = "compas_fd.solvers.fd_numpy"
example = "docs/examples/hypar.py"
test    = "tests/test_hypar.py::test_hypar"
```

CI checks that the theory id exists, the symbol imports, the example runs and the test is collected. It derives the source link from the symbol and pins it to the release tag.

## Installing skills

| Agent app | Project folder |
| --- | --- |
| Claude Code | `.claude/skills/` |
| Codex, Kimi Code, Antigravity | `.agents/skills/` |

Copy or link the `skills/*` folders into those folders. `npx skills add BlockResearchGroup/<repository>` does the same; it is a third-party tool.

| Skill | Where it comes from |
| --- | --- |
| `compas-fd`, `compas-tna`, ... | the package repository |
| `brg-methods` and other skills that combine packages | this repository |

Each package skill records the package version it was checked against. When the package changes, its maintainer updates the skill in the same pull request.

## MCP server

- Lives in `server/` in this repository, built with FastMCP.
- Hosted at one web address. Each student adds it to their own account.
- Reads the same Markdown files. It holds no content of its own.
- Returns the full text, and the chat shows it as the answer.
- No per-package servers.
- Serving the skills over MCP comes later, once agent apps support the MCP Skills extension.

## Scripts and hooks

Goal: copy code as it is, without the model retyping it. A script that copies a file costs almost no tokens and no waiting.

Two layers, one script:

1. **Script in the skill (works everywhere).** Each package's skill has `scripts/copy_example.py`. The skill text tells the agent to run it. The file lands on disk unchanged. Scripts are part of the Agent Skills standard, so this works in all four agent apps with no setup.
2. **Hook (optional, faster).** The agent app runs the same script by itself at a fixed moment, without a model call.

Rules that keep hooks compatible with all four agent apps:

- **One script does the work**: `hooks/brg_hook.py`. No logic lives in a config file.
- **Only the four shared events**: `SessionStart`, `PreToolUse`, `PostToolUse`, `Stop`.
- **The script reads JSON from stdin and accepts both spellings** of each field (`tool_name` and `toolName`), because the agent apps differ.
- **Four small config files call that one script.** `brg hooks install` writes them.
- **Nothing depends on a hook.** Everything a hook does must also be reachable through the skill script.

| Agent app | Hook config written by the installer |
| --- | --- |
| Claude Code | `.claude/settings.json` |
| Codex | `.codex/hooks.json` (the user must review and trust it once) |
| Antigravity | `.agents/hooks.json` |
| Kimi Code | `[[hooks]]` in the user's `~/.kimi-code/config.toml`; it has no project-level hook file |

```text
brg_framework/
├── hooks/
│   ├── brg_hook.py            # the one script
│   └── install.py             # writes the four config files
compas_fd/
└── skills/compas-fd/
    └── scripts/copy_example.py   # in the package
```

## Migration from mcp-server-brg

- [ ] Delete the `greet` tool.
- [ ] Keep showing the full page text in chat for learners. Drop the word-for-word instruction only for the editor mode.
- [ ] Remove editor detection and the write, install and run instruction.
- [ ] List topics, not pages, in the server instructions.
- [ ] Keep all twelve compas_fd examples in one place and remove the duplicate.
- [x] Add `brg-methods` here.
- [x] Draft package skills here: `compas-fd`, `compas-dr`, `compas-tna`, `compas-tno`, `compas-dem`, `compas-ags`.
- [ ] Move each draft into its package's `skills/` folder, then delete it here.
- [ ] Host the server at a web address.
- [ ] Run every Python example in CI against a pinned package version.
- [ ] Measure before going further (below).

## Measure first

Compare five setups on the same tasks: package only, today's server, fixed server, skills only, skills and server. Record input, cached and output tokens, model calls, wall time, and pass or fail. Judge correctness first, then tokens, then time. No saving is claimed until these numbers exist.

## Decisions

| Question | Decision |
| --- | --- |
| Does teaching need the page text in chat, or is a link enough? | The text. Learners get the answer in the chat, not a link |
| Is the server hosted, or run by each user? | Hosted. Each student adds it to their own account |
| Where do package skills live? | In each package. This repository is the pointer. Only skills that combine several packages live here |
| Where is Python and COMPAS installation explained? | In [COMPAS](https://compas.dev). This repository only covers the BRG layer |
| Which packages are covered? | The list in `catalog/packages.toml`. More are added there over time |

## References

- [Agent Skills specification](https://agentskills.io/specification)
- [AGENTS.md](https://agents.md/)
- [MCP 2026-07-28 release](https://blog.modelcontextprotocol.io/posts/2026-07-28/)
- [MCP Skills extension](https://modelcontextprotocol.io/extensions/skills/overview)
- [FastMCP](https://gofastmcp.com/docs/changelog)
- [AAIF projects](https://aaif.io/projects)
