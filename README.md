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

## Orchestration rule

The mandatory layering between orchestrator and implementation is defined in
[SYSTEM_PROMPT.md](SYSTEM_PROMPT.md): the main conversation always starts a
HumanLayer workflow for any development work, and the implementation executor
always uses the SDD skills.

## Versioning

The repo also ships `AGENTS.md.snippet`: a marker-delimited block
with the orchestration rule that `init-repo.sh` appends to each project's
`AGENTS.md` (idempotent; `--force` refreshes it).

Changes here are versioned by git. After updating shared skills, projects
refresh their local copies with `--force` at their own pace — project-local
skills are snapshots, not live links.
