# 执行提示词：agent_gen 工作区 OpenClaw 试点改造

## 当前工作区路径
1. 工作区根目录：`D:\code\AI\J-Agents\agent_gen`
2. 需求文档目录：`D:\code\AI\J-Agents\agent_gen\docs\openclaw\workspace-openclaw-governance`
3. 本轮所有新增、修改、验证都只能发生在上述 `agent_gen` 工作区根目录内。

请按照以下文件执行当前 `agent_gen` 工作区整改，不要扩散到其他目录：

1. `D:\code\AI\J-Agents\agent_gen\docs\openclaw\workspace-openclaw-governance\需求概述.md`
2. `D:\code\AI\J-Agents\agent_gen\docs\openclaw\workspace-openclaw-governance\需求详情-agent_gen工作区OpenClaw试点改造.md`

## 本轮目标
1. 为当前工作区补齐 OpenClaw 风格 `.codex/` 记忆层。
2. 保持“配置优先、最小假设、脚本化生成”的原有工作方式不变。

## 必做事项
1. 创建：
   - `.codex/SOUL.md`
   - `.codex/USER.md`
   - `.codex/MEMORY.md`
   - `.codex/TOOLS.md`
   - `.codex/HEARTBEAT.md`
   - `.codex/memory/`
2. 更新 `AGENTS.md`，补齐 OpenClaw 风格读取顺序。
3. 明确 `.codex/*` 只记录生成经验、稳定约束、失败模式。
4. 保留现有 `docs/`、`reports/`、`tests/`、模板和脚本的职责不变。

## 禁止事项
1. 不要重构生成脚本或配置模型。
2. 不要把正式报告/测试产物写进记忆层。
3. 不要修改其他工作区。

## 交付物
1. 改造后的目录清单。
2. `AGENTS.md` 更新说明。
3. 启动读取与记忆写入验证证据。
4. 最小生成回归结果。
