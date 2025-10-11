# README

本目录用于集中维护AI代理执行任务所需的基础文档和模板。复用方式如下：

1. **初始化项目规范**
   - 将`AI-AGENT_project.md`复制到目标项目根目录，并重命名为`AI-AGENT.md`。
   - 将除`AI-AGENT_project.md`以外的所有文件复制到目标项目的`ai-agent-memory/`目录下。

2. **任务执行前准备**
   - 在复制完成后，项目中的`AI-AGENT.md`会提醒代理优先阅读`ai-agent-memory/`内的指引。
   - `AI-AGENT_general.md`涵盖所有通用任务流程；如执行编程任务，再结合`AI-AGENT_programming.md`。
   - `AI-AGENT_check.md`提供阶段性检查清单，确保每个环节的工作质量。
   - `AI-AGENT_mcp-rules.md`汇总常用MCP服务的调用规范、安全边界与记录要求。
   - `now-task.md`是待用户填写的任务输入模板，执行完毕需恢复为原始状态。

3. **工作状态记录**
   - 按`AI-AGENT_general.md`中的规范，新建`AI-AGENT_working-status.csv`并维护环节记录。
   - 请确保每次复制后指引内容保持最新，若有新约定需回写到本目录。

> 提示：若需要额外的运行脚本或配置片段，请在目标项目中自行维护，避免污染模板目录。
