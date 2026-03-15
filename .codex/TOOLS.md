# TOOLS

## Stable Tooling Rules
1. 优先使用定向检索、摘要和分段读取，避免无差别读取大日志或大文件。
2. 使用 `workspace_compliance_checker.py` 做工作区最小合规验证。
3. 使用 `agent_workspace_generator.py` 做最小生成链路回归。
4. 对重复验证流程优先使用可复用脚本入口，并将临时产物隔离到独立测试会话目录。
