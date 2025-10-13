# 现在的任务

我想对`src/`目录下的现有指令体系进行调整，请你分析我的要求后遵循规范流程，列出优化结果待定项，由我确认后再建立新文档：

- 这次任务的目的是在尽可能保持环节完整（除了少数需要删减，下面会提到）、保持原意的前提下，缩减指令文档篇幅，

- 这次任务除了要对本文档（这个`now-task.md`）进行准备工作的优化（遵循`AI-AGENT_step-before.md`和`undetermined-template.md`），还要在后续的任务主体中，在实际操作文件之前，对`src/`下的文档，需要改动的部分也要遵循模板列成待定项，由我确认后才能操作，也就是这次整个任务的流程大概会是：初始化->分析now-task.md优化后列出待定项->用户确认后开始执行任务->分析src/下文档，对要改动的部分列成待定项->用户确认后对文档进行删改->其他正常流程……

- 不要改动原本的ai-agent-memo-1，而是建立新的目录ai-agent-memo-2，在`src/ai-agent-memo-2`下创建文档建立新的指令体系

- 移除user-temp-opinion.md与相关指令

- 移除`mcp-log.csv`与`mcp-log.md`及其相关指令，不再对mcp调用进行记录

- 默认只有编程任务，不再区分general和programming，合并两个文档，保留完整流程，删减掉冗余内容，把精简后的文档存为AI-AGENT_criterion.md

- 大篇幅删减AI-AGENT_mcp-rules.md，可以不需要保留原意，不需要再有那些具体的建议，只要告诉AI-AGNET有哪些mcp，该在什么时候用这些mcp就好了，可以直接不保留AI-AGENT_mcp-rules.md，直接整合进AI-AGENT_criterion.md，

- 精简AI-AGENT_step-before.md