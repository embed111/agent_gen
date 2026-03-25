# Schedule Center Acceptance Report V2

## 1. 验收对象

- ticket_id: `asg-20260324-115912-07588c`
- node_id: `node-20260324-115912-68350c`
- schedule_id: `sch-20260324-5cc2dfdb`
- schedule_name: `验收-定时任务-已编辑-20260324-115830`
- planned_trigger_at: `2026-03-24T09:15:00+08:00`
- trigger_rule_summary: `每月 24 号 09:15 + 每周 周二 09:15 + 每日 09:15 + 定时 2026-03-24 09:15`
- expected_artifact: `schedule-center-acceptance-report-v2`
- delivery_receiver: `Analyst`

## 2. 验收结论

本次“验收-定时任务-已编辑-20260324-115830 / 2026-03-24 09:15:00”验收通过。

命中创建、同分钟去重、日历结果叠加、任务中心状态详情和审计留痕均有真实落盘证据。任务中心终态快照仍处于 `running`，这符合执行清单中“回写真实等待或运行状态”的要求，不构成验收失败。

## 3. 验收项与证据

### 3.1 真实命中后创建任务中心实例

- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/scan_create_response.json` 记录 `POST /api/schedules/scan` 在 `now_at=2026-03-24 09:15` 返回 `hit_count=1`、`deduped_count=0`、`created_node_count=1`。
- 同一响应中创建的任务实例为 `asg-20260324-115912-07588c`，节点为 `node-20260324-115912-68350c`，并已写入 `dispatch_message=resume_scheduler_requested`。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/schedule_detail_after_scan.json` 记录 `last_trigger_at=2026-03-24T09:15:00+08:00`、`last_result_ticket_id=asg-20260324-115912-07588c`，证明列表详情已回写本次真实命中结果。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/task.json` 和 `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/nodes/node-20260324-115912-68350c.json` 证明任务图和节点实体已落盘。

### 3.2 立即请求既有调度流程

- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/audit/audit.jsonl` 的审计顺序为 `create_graph` -> `create_node` -> `resume_scheduler` -> `dispatch`，时间从 `2026-03-24T11:59:12+08:00` 连续到 `2026-03-24T11:59:14+08:00`。
- 其中 `resume_scheduler` 审计记录的 `target_status=running`，`dispatch` 审计记录绑定 `run_id=arun-20260324-115914-10b028`、`workspace_path=C:/work/J-Agents/agent_gen`，证明命中后立即续跑既有调度流程。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/runtime/schedule-center-browser/logs/events/schedules.jsonl` 同步记录 `create_assignment_node`，其 `dispatch_status=requested`、`dispatch_message=resume_scheduler_requested`。

### 3.3 回写真实等待或运行状态

- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/schedule_detail_after_scan.json` 的最近一次触发记录显示 `result_status_text=已建单待调度`、`assignment_status_text=待开始`，反映建单刚完成时的列表层状态。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/assignment_status_terminal.json` 的终态快照显示任务图 `scheduler_state=running`，`status_counts.running=1`，所选节点 `status=running`、`status_text=进行中`。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/runs/arun-20260324-115914-10b028/run.json` 记录当前真实执行批次 `status=running`，`latest_event_at=2026-03-24T12:01:48+08:00`。
- 列表层显示“待调度”而任务中心详情显示“运行中”并不冲突；两者是同一条执行链路在不同时间点的快照，符合“先建单，再恢复调度，再进入运行”的状态推进。

### 3.4 同分钟去重成立

- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/scan_dedupe_response.json` 对同一 `schedule_id=sch-20260324-5cc2dfdb`、同一 `now_at=2026-03-24 09:15` 的再次扫描返回 `hit_count=1`、`deduped_count=1`、`created_node_count=0`。
- 同一响应中的条目标记为 `status=deduped`，说明同一分钟不会重复创建第二个任务中心实例。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/runtime/schedule-center-browser/logs/events/schedules.jsonl` 还记录了同一个 `trigger_instance_id=sti-20260324-7c6a9fcf` 的 `trigger_deduped` 事件，与接口返回相互印证。

### 3.5 列表详情、日历视图与结果叠加成立

- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/screenshots/editor_edit.probe.json` 记录 `pass=true`、`editor_mode=edit`、`editor_name=验收-定时任务-已编辑-20260324-115830`、`editor_receiver_value=Analyst`，证明编辑后的计划配置被真实加载。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/screenshots/list_detail.probe.json` 记录 `pass=true`、`rule_chip_count=4`、`future_trigger_count=8`、`calendar_month=2026-03`，证明列表详情和未来计划视图都能展示四类规则组合后的结果。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/schedule_detail_after_scan.json` 的最近一次触发记录包含 `merged_rule_count=4`，并列出 `monthly:24:09:15`、`weekly:2:09:15`、`daily:09:15`、`once:2026-03-24T09:15:00+08:00` 四个规则键，证明 `2026-03-24 09:15` 的结果是“多规则合并后的单次命中”，不是重复展开。
- 同一文件的未来计划中，`2026-03-31T09:15:00+08:00` 的 `trigger_rule_summary=每周 周二 09:15 + 每日 09:15`、`merged_rule_count=2`，证明日历会把同日同分的多条规则叠加到一个结果槽位。
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/screenshots/result_detail.probe.json` 记录 `pass=true`、`recent_trigger_count=1`、`related_task_count=1`、`latest_result_status=running`、`latest_assignment_ticket_id=asg-20260324-115912-07588c`、`calendar_selected_date=2026-03-24`、`calendar_result_count=1`，证明结果详情和日历结果视图都已关联到本次真实任务实例。

## 4. 关键证据清单

- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/scan_create_response.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/scan_dedupe_response.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/schedule_detail_after_scan.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/api/assignment_status_terminal.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/screenshots/editor_edit.probe.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/screenshots/list_detail.probe.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/screenshots/result_detail.probe.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/task.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/nodes/node-20260324-115912-68350c.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/runs/arun-20260324-115914-10b028/run.json`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/task-output/tasks/asg-20260324-115912-07588c/audit/audit.jsonl`
- `C:/work/J-Agents/workflow/.test/evidence/schedule-center-browser/runtime/schedule-center-browser/logs/events/schedules.jsonl`

## 5. 面向 Analyst 的最终判断

- schedule center 列表详情可追溯。
- schedule center 日历视图与结果叠加可追溯。
- 任务中心状态详情可追溯。
- 审计留痕可追溯。
- 本次验收结论为 `PASS`。
