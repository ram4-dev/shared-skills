# shared-skills

Shared workflow and development skills for Pi (and other Agent Skills–
compatible harnesses), used across Ramiro's personal projects.

## Layout

- `skills/` — the actual skills (`sdd-*` SDD phases, `_shared` SDD references,
  `worktree-first-development`, `gentle-ai-bench`, `go-testing`,
  `systemic-issue-triage`, `humanlayer-*`, `herdr-development-orchestration`).

## How skills reach a project

Do **not** clone this repo into every project. The global Pi skill
`init-repo` (`~/.agents/skills/init-repo/`) copies `skills/*` into the
target repository's `.agents/skills/`:

```bash
# from a repo root (or anywhere inside it)
~/.agents/skills/init-repo/scripts/init-repo.sh           # copy missing skills
~/.agents/skills/init-repo/scripts/init-repo.sh --list    # preview
~/.agents/skills/init-repo/scripts/init-repo.sh --force   # refresh local copies
```

The script is idempotent: existing project-local skills are skipped unless
`--force` is passed.

## Versioning

Changes here are versioned by git. After updating shared skills, projects
refresh their local copies with `--force` at their own pace — project-local
skills are snapshots, not live links.
