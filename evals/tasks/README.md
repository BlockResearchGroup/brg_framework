# Tasks

One Markdown file per task: `t1_hypar.md`, `t2_selfweight.md`, and so on.

```text
---
id: t1
packages: [compas_fd]
check: check_t1.py
---

The exact prompt given to the agent, word for word.
```

`check_*.py` runs the code the agent wrote and exits with 0 for pass and 1 for fail.

To be written.
