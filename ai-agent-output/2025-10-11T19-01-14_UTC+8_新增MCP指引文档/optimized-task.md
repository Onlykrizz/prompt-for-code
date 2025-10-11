# 优化后的任务

## 任务目标
- 重新梳理 `general/AI-AGENT_mcp-rules.md`，确保继承 `ai-agent-memory/mcp-rules.md` 既有内容并扩展为项目级统一规范。
- 补回 `ai-agent-memory/mcp-rules.md` 中原有的 MCP（Sequential Thinking、web-search、Context7、Serena）的服务指引，并与新增的 filesystem、playwright、shrimp-task-manager、deepwiki、desktop-commander 指南整合为一份完整清单。
- 对所有纳入的 MCP 服务核对官方或权威资料，提炼调用场景、关键参数、风险控制与降级策略。
- 校准 general 目录内其他指引（如 README、AI-AGENT_general.md 等）对新规范的引用，保证文档体系无遗漏。

## 执行步骤
1. 复核 general 目录现有文档结构与引用，确认 `AI-AGENT_mcp-rules.md` 的定位以及缺失的既有 MCP 条目。
2. 梳理 `ai-agent-memory/mcp-rules.md` 内容，列出必须覆盖的通用策略与服务指引；记录需要补写的段落。
3. 针对 Sequential Thinking、web-search、Context7、Serena 等既有 MCP 补充官方资料调研，整理核心使用要点，并更新 `ai-agent-output/mcp-research-notes.md` 作为引用依据。
4. 按统一格式整合所有 MCP 指南（含原新增五项），编写或修订 `general/AI-AGENT_mcp-rules.md`，确保结构、措辞与项目规范一致。
5. 同步更新 general 目录内相关文档（如 README、AI-AGENT_general.md 等），说明新规范内容与使用方式。
6. 自检文档链接、术语、引用格式及风险提示，确保满足质量要求并便于后续维护。

## 验证标准
- `general/AI-AGENT_mcp-rules.md` 包含通用策略与九项 MCP 服务（Sequential Thinking、web-search、Context7、Serena、filesystem、playwright、shrimp-task-manager、deepwiki、desktop-commander）的指引。
- 每个服务条目均基于官方资料撰写，覆盖适用场景、关键参数/限制、风险控制或失败回退建议，并在 `ai-agent-output/mcp-research-notes.md` 中留存调研依据。
- general 目录相关文档引用新规范且无断链或描述遗漏，整体风格与原有规范一致。
- 文档语言、格式、命名等符合项目要求，可直接指导代理执行。

## 风险与应对
- **官方资料缺失或变动**：保留来源与检索时间，必要时说明不确定性与替代方案。
- **历史描述与新内容冲突**：对照 `ai-agent-memory/mcp-rules.md` 与现有 general 文档，发现冲突时及时修订措辞并记录原因。
- **信息量过大难以执行**：使用分组、小节与表格突出关键要点，避免冗余描述，必要时附加参考链接供深入阅读。
