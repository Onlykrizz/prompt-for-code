# 优化后的任务

## 任务目标
- 在 `general/` 目录内同步更新现有指令文档，使其明确：工作状态与待定项等辅助文档需存放于 `ai-agent-output/YYYY-MM-DDTHH-MM-SS_UTC_任务简述/` 目录，并给出命名示例。
- 在通用流程指引中新增“提交前必须执行 `git add .` 跟踪全部未忽略文件”的统一要求，并说明其适用时机。
- 在“文档更新”环节补充“更新工作状态后、提交前需先维护 `CHANGELOG.md`”的强制顺序，确保流程闭环。

## 执行步骤
1. 复核 `general/` 目录内相关文件（含 `AI-AGENT_general.md`、`AI-AGENT_programming.md`、`AI-AGENT_check.md`、`AI-AGENT_step-before.md`、`AI-AGENT_project.md`、`AI-AGENT_mcp-rules.md`、`README.md`、`undetermined-template.md`），梳理与本次三项新增规范相关的陈述与示例。
2. 设计统一的新增/修改段落，描述新的存储目录结构、命名规范以及清理阶段不再删除这些文件的要求；同步替换旧的 `record/` 引用。
3. 在流程与提交规范段落中明确“在执行提交前需运行 `git add .`”的操作顺序与适用范围，确保与现有提交规范兼容。
4. 更新“文档更新”相关章节与检查清单，强调在提交前必须先维护 `CHANGELOG.md`，并指出执行顺序（更新工作状态 → 维护 CHANGELOG → 提交）。
5. 自检所有修改内容的措辞、格式与链接是否与原有文档保持一致，确认没有遗漏需要同步的文件。

## 验证标准
- `general/` 目录内涉及流程管理的文档均引用新的 `ai-agent-output/YYYY-MM-DDTHH-MM-SS_UTC_任务简述/` 存储规范且示例一致。
- 指南中显式要求在每次 `git commit` 前执行 `git add .`，并说明适用前提（排除 `.gitignore` 忽略项）。
- “文档更新”环节及其检查清单明确“更新工作状态后、提交前先维护 `CHANGELOG.md`”的顺序要求。
- 清理阶段不再要求删除或移动 `mcp-log.md`、`AI-AGENT_working-status.csv`、`undetermined.md`、`optimized-task.md`。
- 文档语言保持简体中文、风格统一，无拼写或链接错误。

## 风险与应对
- **漏改引用路径**：使用 `rg` 逐项检索 `record/` 与目标文件名，确保全部替换并复核。
- **新增规范与旧流程冲突**：修改前后保持段落上下文连贯，必要时增加说明避免理解歧义。
- **提交顺序说明不统一**：在多个文档中使用一致措辞，并在检查清单中再次强化，降低执行偏差风险。
