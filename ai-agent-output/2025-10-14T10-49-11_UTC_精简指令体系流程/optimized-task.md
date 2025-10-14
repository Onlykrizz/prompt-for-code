# 优化后任务描述

## 执行前约束
| 项目 | 状态 | 备注 |
| --- | --- | --- |
| 不记录`mcp-log.csv`与`mcp-log.md` | 已确认 | 用户在 now-task 中指定，后续由状态记录代替日志。 |

## 任务背景
- 用户希望在保留原始流程意图与关键动作的前提下，大幅精简指令体系篇幅。
- 旧版指引分散于`AI-AGENT_general.md`、`AI-AGENT_programming.md`、`AI-AGENT_mcp-rules.md`等多份文档，存在重复内容。
- 本次重构仅新增`src/ai-agent-memo-3`目录，原`ai-agent-memo-1`仅作参考，不修改也不删除。

## 目标与交付范围
- 在`src/ai-agent-memo-3`下建立新的指令体系：
  - 核心文档：`AI-AGENT_criterion.md`，整合流程、MCP基准、模板命令与自检表。
  - 配套文档：经精简的`AI-AGENT_step-before.md`、更新后的`now-task.md`、模板/示例所需的其他文件。
- 移除或不再使用`user-temp-opinion.md`、`mcp-log.csv`、`mcp-log.md`及其在流程中的相关指令。
- 默认仅处理编程任务，流程中不再区分general/programming路径。

## 执行步骤
1. **目录与文件初始化**：创建`src/ai-agent-memo-3/`及必要子目录，复制或重建所需模板文件的基础骨架。
2. **撰写`AI-AGENT_criterion.md`**：
   - 以六大环节为主线，每节包含“核心必做”“补充细则”“模板/命令”三个子区块，确保每区块条目 ≤12 条。
   - 在流程中整合MCP使用说明，提供“MCP调用基准表”，说明触发条件与最少记录方式。
   - 将原`AI-AGENT_check.md`的检查项整合为文末“执行自检表”，方便勾选。
3. **精简`AI-AGENT_step-before.md`**：保留任务前置准备的关键步骤，删除冗余阐述，并与新的约束（例如如何使用“执行前约束”表格）对齐。
4. **重写`now-task.md`模板**：采用“任务描述 + 必填检查表”结构，引导用户明确约束、是否需要流程图等信息，并指向`ai-agent-memo-3`。
5. **更新其他必要模板/示例**：根据需要提供`undetermined-template.md`或其他与新流程匹配的参考，确保不再引用被移除的文件。
6. **确认旧文档引用方式**：在新指引内说明`ai-agent-memo-1`仅为历史参考，避免误用旧流程。
7. **验证与文档记录**：按照新自检表逐项核对，确保所有环节与模板相互呼应，并在状态文档中记录完成情况。

## 验证标准
- `src/ai-agent-memo-3/AI-AGENT_criterion.md`存在且结构满足三段式要求，覆盖六大环节、MCP基准和自检表。
- `AI-AGENT_step-before.md`与`now-task.md`完成精简调整，不再引用`user-temp-opinion.md`或`mcp-log`文件。
- `ai-agent-output`中的流程文件与新指引描述保持一致，能够支持未来任务执行。
- 项目中不再新增或引用`user-temp-opinion.md`、`mcp-log.csv/md`。
- 最新一条状态记录表明已切换至“流程设计”环节并概述设计准备情况。
