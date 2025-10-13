# 优化后任务说明

## 任务目标
- 在不改动 `src/ai-agent-memo-1` 的前提下，于 `src/ai-agent-memo-2` 建立精简版指令体系。
- 合并 `AI-AGENT_general.md` 与 `AI-AGENT_programming.md`，吸收 `AI-AGENT_mcp-rules.md` 核心信息，形成单一的 `AI-AGENT_criterion.md`。
- 精简 `AI-AGENT_step-before.md`，保留执行主线并链接至 `AI-AGENT_criterion.md` 的详细说明。
- 移除 user-temp 与 MCP 日志相关流程，仅保留说明性提示。

## 已确认策略
1. **目录结构（U001S001）**  
   - 在 `src/ai-agent-memo-2/` 下创建：`AI-AGENT_criterion.md`、`AI-AGENT_step-before.md`、`AI-AGENT_check.md`、`undetermined-template.md`、`now-task.md`。  
   - 不再保留 user-temp-opinion 或 mcp-log 相关文件。
2. **主指令结构（U002S001）**  
   - `AI-AGENT_criterion.md` 以六个环节为主线，章节结构：环节概览 → 关键要求 → 验证/测试要点 → MCP 使用场景速览。
3. **MCP/user-temp 处理（U003S002）**  
   - 在新文档中仅保留一句说明“本版本不再维护 user-temp 与 MCP 日志流程”，无额外迁移指引。
4. **前置流程（U004S001）**  
   - `AI-AGENT_step-before.md` 保留“任务分析 → 内容优化 → 待定项处理 → 结果生成”四段结构，每段压缩为 3-4 条动作，并链接至主文档。

## 下一阶段任务拆解
1. 进入流程设计环节：梳理 `AI-AGENT_criterion.md` 章节要点、各文件间引用关系以及需要修改的旧文档。
2. 在执行前，对 `src/` 下各目标文档逐一分析并形成待定项，待确认后再进行编辑。
3. 根据确认方案撰写/更新 `ai-agent-memo-2` 下各文件内容，并删除或调整旧指令中与 user-temp、MCP 日志有关的段落。
4. 验证新文档覆盖全部流程需求，整理测试/验证记录。
5. 更新 `CHANGELOG.md` 与其他必要文档，完成收尾。

## 验证标准
- `src/ai-agent-memo-2/` 中新增文件齐全、结构符合集成方案。
- `AI-AGENT_criterion.md` 章节与内容符合合并计划，涵盖六环节重点与 MCP 使用场景列表，篇幅较原体系明显缩减。
- `AI-AGENT_step-before.md` 精简为四段结构且跳转链接正确，所有 user-temp/MCP 日志指令已移除。
- `AI-AGENT_check.md`、`undetermined-template.md`、`now-task.md` 与新流程一致，无遗留旧指令。
- `CHANGELOG.md` 记录本次改动，新旧流程切换说明明确，仓库状态整洁。
