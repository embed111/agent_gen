# 2026-03-14 OpenClaw Rectification

## Context Read
1. Read `AGENTS.md`.
2. Read `docs/openclaw/workspace-openclaw-governance/需求概述.md`.
3. Read `docs/openclaw/workspace-openclaw-governance/需求详情-agent_gen工作区OpenClaw试点改造.md`.
4. Read `docs/openclaw/workspace-openclaw-governance/执行提示词-agent_gen工作区OpenClaw试点改造.md`.
5. Read `docs/openclaw/workspace-openclaw-governance/统一开工提示词-当前工作区OpenClaw整改.md`.

## Actions
1. Added `.codex/` core memory documents and local memory directory.
2. Aligned local workspace instructions and tooling from `agent.md` to `AGENTS.md`.
3. Kept `docs/`、`reports/`、`tests/`、`templates/` responsibilities unchanged.

## Verification Intent
1. Validate memory writes through this file plus `.codex/MEMORY.md` and `.codex/HEARTBEAT.md`.
2. Run minimal regression for workspace compliance and generation chain after the rename alignment.

## Verification Result
1. Session `20260314-111154-320`: `python workspace_compliance_checker.py --workspace . --report reports/workspace_compliance.md --json-report reports/workspace_compliance.json` passed with `22/22` checks.
2. Session `20260314-111200-829`: `python -m unittest -q tests.test_workspace_compliance_checker tests.test_agent_workspace_generator` passed with `8` tests.
