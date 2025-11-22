# AGENTS.md

!!! 在开始任何工作前，必须先阅读本文件，并逐一查阅`ai-agent-memory/`目录中的所有指引。

## 快速指引
- `ai-agent-memory/AI-AGENT_general.md`：通用任务的完整流程与工作状态记录规范。
- `ai-agent-memory/AI-AGENT_programming.md`：编程/开发任务的额外要求、测试与提交规范。
- `ai-agent-memory/AI-AGENT_check.md`：六大环节的核对清单，确保每一步可追溯、可验证。
- `ai-agent-memory/now-task.md`：待用户填写的任务描述模板，执行前必须完成“任务内容预处理”。
- `ai-agent-memory/AI-AGENT_mcp-rules.md`：本项目常用MCP服务的调用规范、安全边界与日志要求。

## 工作要求摘要
1. **工作状态同步**：首次进入“任务前置准备”环节时创建`AI-AGENT_working-status.csv`，并将`AI-AGENT_working-status.csv`、`undetermined.md`、`optimized-task.md`、`mcp-log.csv`与`mcp-log.md`等辅助文档统一存放在`ai-agent-output/YYYY-MM-DDTHH-MM-SS_UTC_任务简述/`目录下（任务简述控制在8-20字），按环节维护记录并在每次更新该文件后立即创建git提交以保留状态变更轨迹。
2. **流程驱动执行**：严格遵循“任务前置准备 → 流程设计 → 任务主体流程循环 → 验证结果 → 文档更新 → 收尾”的顺序执行，返工时需回退环节并记录原因。
3. **信息留痕**：所有阶段性成果、关键决策、风险与约定必须记录在相应文档中（含本文件、流程设计文档、`optimized-task.md`等）。
4. **交付完成标准**：通过`AI-AGENT_check.md`逐环节核对，验证交付物满足成功标准后方可收尾。
5. **提交顺序要求**：每次准备提交前先运行`git add .`以追踪所有未被`.gitignore`忽略的文件；在“文档更新”环节更新工作状态后，务必先维护`CHANGELOG.md`并生成新的版本号段落（写入日期、重建空的`[Unreleased]`区块），然后创建提交。

如需新增或调整项目约定，请在完成任务后同步更新本文件与模板库中的原始文档。
