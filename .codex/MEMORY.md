# MEMORY

## Active Read Order
1. 先读 `AGENTS.md`。
2. 再读 `.codex/SOUL.md`、`.codex/USER.md`、近两天 `.codex/memory/*.md`、`.codex/MEMORY.md`。

## Stable Constraints
1. `.codex/*` 只记录生成经验、稳定约束、失败模式。
2. 正式报告、测试与模板职责留在现有目录。
3. 当前工作区顶层 Agent 工作文档使用 `AGENTS.md`。

## Known Failure Modes
1. 本地脚本、检查器或测试若仍引用 `agent.md`，会在目录治理后失效。
2. 把正式产物写入 `.codex/` 会污染记忆层并破坏边界。

## Latest Verification Snapshot
1. `20260314-111154-320`: `workspace_compliance_checker.py` passed with `22/22` checks.
2. `20260314-111200-829`: `python -m unittest -q tests.test_workspace_compliance_checker tests.test_agent_workspace_generator` passed with `8` tests.
