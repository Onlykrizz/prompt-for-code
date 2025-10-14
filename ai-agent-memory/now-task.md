# 现在的任务

我想对`src/`目录下的现有指令体系进行调整，请你分析我的要求后遵循规范流程，列出优化结果待定项，由我确认后再建立新文档：

- 这次任务的目的是在尽可能保持环节完整（除了少数需要删减，下面会提到）、保持原意的前提下，缩减指令文档篇幅，
- 不要改动原本的ai-agent-memo-1，而是建立新的目录ai-agent-memo-3，在`src/ai-agent-memo-3`下创建文档建立新的指令体系
- 忽略ai-agent-memo-2，不要读取，也不参考ai-agent-memo-2
- 分析优化方案时，默认后续不再维护ai-agent-memo-1，仅在本次任务中提供参考用，不修改，不删除，后续仅作为存档保留，
- 移除user-temp-opinion.md与相关指令
- 移除`mcp-log.csv`与`mcp-log.md`及其相关指令，不再对mcp调用进行记录
- 默认只有编程任务，不再区分general和programming，合并两个文档，保留完整流程，把精简后的文档存为AI-AGENT_criterion.md
- 大篇幅删减AI-AGENT_mcp-rules.md，可以不需要保留原意，不需要再有那些具体的建议，只要告诉AI-AGNET有哪些mcp，该在什么时候用这些mcp就好了，可以直接不保留AI-AGENT_mcp-rules.md，直接整合进AI-AGENT_criterion.md，
- 精简AI-AGENT_step-before.md
- 所谓的“精简”必须保留：
    - 所有关键步骤
    - 需要创建、初始化、后续环节中要维护的文档
    - 固定模板代码
    - 模板命令，例如plantuml的命令