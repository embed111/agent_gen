# 需求详情：agent_gen 工作区 OpenClaw 试点改造

## 1. 主题目标与价值说明
为 `agent_gen` 补齐 OpenClaw 风格 `.codex/` 记忆层，同时保持其“配置优先、最小假设、脚本化生成”的核心工作方式不变。

## 2. 用户画像与使用场景
1. 用户画像：生成 agent、owner、执行维护者。
2. 使用场景：
   - 恢复近期生成策略与失败模式；
   - 保持正式输出继续落到 `docs/`、`reports/`、`tests/`。

## 3. 用户旅程或关键流程
1. 新增 `.codex/`。
2. 更新 `AGENTS.md`。
3. 回归生成链路。

## 4. 功能需求清单
### FR-AGG-01 新增记忆层
1. 新增：
   - `.codex/SOUL.md`
   - `.codex/USER.md`
   - `.codex/MEMORY.md`
   - `.codex/TOOLS.md`
   - `.codex/HEARTBEAT.md`
   - `.codex/memory/`

### FR-AGG-02 更新读取顺序
1. `AGENTS.md` 增加：
   - `.codex/SOUL.md`
   - `.codex/USER.md`
   - 近两天 `.codex/memory/*.md`
   - 主会话 `.codex/MEMORY.md`

### FR-AGG-03 记忆内容边界
1. `.codex/*` 只记录生成经验、稳定约束、失败模式。
2. 正式报告、测试与模板仍留在现有目录。

## 5. 非功能需求
1. 不破坏配置驱动模式。
2. 不引入额外复杂目录。

## 6. 验收标准
1. Given 已完成改造
2. When 检查 `../agent_gen/.codex/`
3. Then 核心文档与 `memory/` 已存在
4. And `AGENTS.md` 已具备 OpenClaw 风格读取顺序

## 7. 边界条件与异常处理
1. 若当前不需要本地技能，不强制新增 `.codex/skills/`。

## 8. 依赖项与开放问题
1. 依赖执行方更新 `AGENTS.md`。
2. 开放问题：是否后续把模板规范沉淀进 `.codex/TOOLS.md`；本轮不强制。
