# 优化后任务描述

## 任务目标
- 将general目录下的MCP调用规范更新为统一使用`mcp-log.csv`记录，并明确“时间戳→执行→写入”流程与豁免场景。
- 强化任务前置准备流程，要求多维度优化分析、集中记录待定项、获取用户确认后方可进入下一环节，并在相关指引与检查清单中形成闭环。
- 建立“用户临时意见”文档机制，提供可选需求配置示例，确保在生成`optimized-task.md`时可以结合用户临时决策。

## 执行步骤
1. 修改`general/AI-AGENT_mcp-rules.md`：
   - 将所有`mcp-log.md`记录要求替换为`mcp-log.csv`结构化记录，列出标准字段、记录顺序、豁免条目（仅保留为日志而产生的`mcp-time`与写入动作）。
   - 追加操作示例或说明，提醒调用完成后立刻写入CSV，并保留`mcp-log.md`作为说明文件。
2. 强化任务前置准备流程文档：
   - 在`general/AI-AGENT_general.md`描述“任务内容优化阶段→列出所有候选方案→写入`undetermined.md`→统一向用户确认→确认结果并回填`optimized-task.md`”的强制要求，即使判定无优化空间也需写明依据，并禁止在未确认前进入后续环节。
   - 同步更新`general/AI-AGENT_step-before.md`细化执行步骤，`general/AI-AGENT_check.md`添加核对项，确保流程、操作与检查三者一致。
3. 新增“用户临时意见”机制：
   - 在general目录新增文档（建议命名为`general/user-temp-opinion.md`），包含两种默认选项（“不记录mcp-log.csv”与“记录但忽略指定MCP列表”）及示例列表占位，提示用户在文档末尾写明本次任务的最终意见。
   - 在`AI-AGENT_general.md`与`AI-AGENT_step-before.md`中加入引用，要求在生成`optimized-task.md`前读取并整合该文档内容。
4. 根据以上改动更新辅助文档：
   - 若需要，为`ai-agent-memory`或其他指引补充同步说明。
   - 更新`CHANGELOG.md`、相关状态记录与日志，确保流程可追溯。

## 验证标准
- `general/AI-AGENT_mcp-rules.md`中所有关于日志的叙述都聚焦在`mcp-log.csv`，并明确字段、顺序与豁免条目；示例或说明与要求一致。
- `general/AI-AGENT_general.md`、`general/AI-AGENT_step-before.md`、`general/AI-AGENT_check.md`包含多维度优化分析、集中确认待定项、无优化时需提供依据、未经确认不得进入下一环节等要点。
- `general/user-temp-opinion.md`存在，提供两种默认选项、忽略列表占位与用户填写说明，指引中已引用该文档并要求在生成`optimized-task.md`前结合用户意见。
- 所有相关文档语义、术语与格式保持一致，新增内容均以简体中文撰写；状态记录与`mcp-log.csv`补全本阶段操作。

## 已确认的用户决策
- U001 采纳方案S002：统一使用`mcp-log.csv`并规定豁免条目。
- U002 采纳方案S002：在流程、操作与检查文档中同步强化任务前置准备执行要求。