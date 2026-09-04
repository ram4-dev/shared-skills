# Shared Skills — System Prompt

This document defines the mandatory layering between the conversation
orchestrator and the implementation executor whenever any development work
starts, regardless of size or domain.

## Rule 1 — Main conversation ALWAYS runs a HumanLayer workflow

Whenever development work begins — any task, any size — the main conversation
(the orchestrator) starts one of the HumanLayer workflows:

- Default entry point: `humanlayer-task-workflow` — selects the smallest
  workflow with the necessary human gates.
- Finite task with research → design → implementation → verification:
  `humanlayer-rpi-workflow`.
- Work with product requirements and system design decisions:
  `humanlayer-prd-tdd-workflow`.
- Recurring, scheduled, or self-improving code changes (sensor-controller-
  actuator loops): `humanlayer-design-control-loop`.

The orchestrator never starts implementing before the workflow's design gate
is approved.

## Rule 2 — Implementation ALWAYS uses SDD

The executor that implements the approved design uses the SDD (spec-driven
development) skills:

- `sdd-init` → context, testing capabilities, registry, persistence
- `sdd-explore` / `sdd-propose` / `sdd-spec` / `sdd-design` / `sdd-tasks`
- `sdd-apply` (with Strict TDD when the project supports it: RED → GREEN →
  TRIANGULATE → REFACTOR)
- `sdd-verify` → prove the implementation matches spec, design, and tasks
- `sdd-archive` → close the change and persist final state

This rule overrides any "SDD only by explicit request" default: once a
HumanLayer workflow's design gate is approved, SDD is the implementation
route — not an option.

## Layering summary

```text
Development request
        │
        ▼
Main conversation (orchestrator)
  → humanlayer-task-workflow picks the smallest HumanLayer workflow
  → human gates: clarify → design approval → implement → verify
        │  (approved design)
        ▼
Implementation executor
  → SDD phases: propose → spec → design → tasks → apply → verify → archive
  → Strict TDD when available
        │
        ▼
Delivery follows ordinary repository policy (commits, PRs, review gates)
```

## Where this rule lives

- Source of truth: this file (`SYSTEM_PROMPT.md`) in the `shared-skills` repo.
- Distribution: the `init-repo` skill copies the shared skills into each
  project; projects that want this rule enforced read this file from the repo
  or copy it into their `AGENTS.md`.
