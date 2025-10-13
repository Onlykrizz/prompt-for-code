# 流程设计记录

## 用户临时意见文档（general/user-temp-opinion.md）设计要点
- 文档结构：
  - 标题：`# 用户临时意见`
  - 使用说明：提示本文件仅用于当前任务的临时决策，会随任务变动。
  - 选项段落：
    1. **选项A**："用户明确提出，本次任务过程不要创建和记录mcp-log.csv"，说明选择后将在执行阶段跳过CSV写入。
    2. **选项B**："本次任务需要记录mcp-log.csv，但除了记录行为本身需要的mcp-time调用和一个写入文件相关操作的mcp调用之外，还应该忽略下列mcp的记录"。
  - 忽略列表占位：提供示例列表如`- mcp-time`、`- mcp-desktop-commander`，提醒用户按需增删。
  - 用户意见说明区域：提示在列表后单独写一段，如“我已了解具体情况，本次任务不要记录mcp-log.csv”。
- 操作指引：
  - 在任务内容优化阶段，执行者需读取该文档，与`undetermined.md`确认结果一并纳入`optimized-task.md`。
  - 若用户未填写意见，应在流程设计中强调需要先确认。

## 指令体系调整方案
### general/AI-AGENT_mcp-rules.md
- 将所有“记录至mcp-log.md”的描述替换为`mcp-log.csv`，列出标准字段：时间戳、服务、调用类型、参数摘要、输出摘要、备注。
- 增补操作步骤：先调用`mcp-time`记录时间戳 → 执行目标MCP → 写入`mcp-log.csv`。
- 明确豁免条目：仅为记录日志而产生的`mcp-time`与对应写入动作可免记；若用户在临时意见文档中声明忽略其他MCP，应说明依赖该文档。
- 提醒保留`mcp-log.md`作为说明文档，并建议记录参考示例。

### general/AI-AGENT_general.md
- 在“任务前置准备-任务内容优化阶段”处补充：必须列出全部候选方案，写入`undetermined.md`，统一向用户确认，并在确认前禁止进入下一环节。
- 在“流程设计”前追加步骤：读取`general/user-temp-opinion.md`与`undetermined.md`确认结果后方可生成`optimized-task.md`。
- 在“文档更新”环节引用临时意见文档，提示若临时意见发生变更需同步记录。

### general/AI-AGENT_step-before.md
- 在“任务内容优化阶段”追加细化步骤：列出潜在优化项、写入`undetermined.md`、检查临时意见文档、与用户一次性确认。
- 在“待定项处理机制”下描述：确认结果需在`optimized-task.md`与临时意见文档中同步体现。

### general/AI-AGENT_check.md
- 在“流程设计”检查项中增加：已读取并整合`general/user-temp-opinion.md`；`optimized-task.md`已包含用户临时意见结果。
- 在“任务前置准备”检查项中补充：`undetermined.md`仅保留已采纳方案，临时意见已确认。

### user-temp-opinion.md（新增）
- 文件位于general目录，供用户逐任务填写可选需求。
- 保留两项默认选项与忽略列表占位，提示用户在列表后写入最终声明。
- 说明该文档为临时决策，会随任务更新；执行者需在生成`optimized-task.md`前读取。

## 执行顺序与依赖
1. 先创建`general/user-temp-opinion.md`并在文档更新环节引用。
2. 更新`general/AI-AGENT_mcp-rules.md`，随后调整`general/AI-AGENT_general.md`、`general/AI-AGENT_step-before.md`、`general/AI-AGENT_check.md`以保持术语一致。
3. 若`ai-agent-memory`下对应模板需同步（视最终变更范围而定），在文档更新阶段评估是否复制改动。
4. 在“任务主体流程循环”执行时，需根据临时意见确定真实执行策略，并在`mcp-log.csv`记录豁免依据。

## 风险与对策
- **风险**：忘记同步临时意见，导致执行策略与规范冲突。→ **对策**：在流程设计和检查清单中加入强制核对条目。
- **风险**：CSV记录说明不清晰，执行者误判豁免范围。→ **对策**：在`AI-AGENT_mcp-rules.md`提供示例及引用临时意见文档。
- **风险**：多文档修改导致语义不一致。→ **对策**：实施前再次审阅术语，执行阶段逐项比对。
