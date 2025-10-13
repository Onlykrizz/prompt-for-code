# 变更日志 (Changelog)

所有显著的变更都会记录在此文件中。

本项目遵循[语义化版本](https://semver.mdn.cn/)规范。

## [Unreleased]

## [0.13.0] - 2025-10-13
### 新增 (Added)
- 新增 `src/ai-agent-memo-2/AI-AGENT_criterion.md`、`AI-AGENT_step-before.md`、`AI-AGENT_check.md`、`undetermined-template.md` 与 `now-task.md`，提供精简版编程任务指引。

### 变更 (Changed)
- 调整 `src/Agents.md` 快速指引与工作要求摘要，对接精简指令体系并移除 MCP 日志默认要求。

## [0.12.0] - 2025-10-12
### 新增 (Added)
- 创建 `general/criterion-flutter-rust/` 与 `general/criterion-react-rust/`，提供 Flutter/React 与 Rust 协同的多方案守则与项目创建维护指导。

### 变更 (Changed)
- 在 `general/README.md` 增补 Flutter+Rust、React+Rust 目录索引。
- 调整 `AI-AGENT_general.md`、`AI-AGENT_check.md`、`AI-AGENT_step-before.md` 的阅读指引，默认仅需查阅非 `criterion-*` 文档，按需引用规范守则。

## [0.11.0] - 2025-10-12
### 新增 (Added)
- 新增 `general/criterion-flutter/` 目录，覆盖移动与平板、桌面与Web、插件与平台通道、企业与可观测性、高性能与图形动画五类Flutter守则。
- 新增 `general/criterion-react/` 目录，面向TypeScript生态的React守则，涵盖SPA、SSR与边缘渲染、设计系统、状态管理、性能优化等方向。

### 变更 (Changed)
- 在 `general/README.md` 补充 Flutter 与 React(TypeScript) 守则目录说明，保持索引完整。

## [0.10.0] - 2025-10-12
### 新增 (Added)
- 新增 `general/criterion-java/` 目录，覆盖 CLI与自动化脚本、Web与微服务、企业级平台与服务、数据工程与大数据、高性能与分布式计算五大方向的Java守则，整理核心原则、结构建议与权威参考链接。

### 变更 (Changed)
- 在 `general/README.md` 补充 Java 守则目录说明，保持多语言规范体系索引一致。

## [0.9.0] - 2025-10-12
### 新增 (Added)
- 创建 `general/user-temp-opinion.md` 模板，提供“无需记录”和“记录但忽略部分MCP”两种默认选项，并引导用户填写临时意见。
- 新增 `general/criterion-python/` 目录，覆盖 CLI、Web、数据科学、企业平台、高性能计算五大方向的Python规范守则，并附参考资料与项目骨架。

### 变更 (Changed)
- 强化 general 目录的任务前置准备与流程设计要求，执行前必须列出待定项、整合临时意见并获用户确认。
- 统一 general 下各指引（含 `AI-AGENT_mcp-rules.md`、`AI-AGENT_general.md`、`AI-AGENT_step-before.md`、`AI-AGENT_check.md`、`AI-AGENT_programming.md`、`Agents.md`、`README.md`）的日志规范，明确以 `mcp-log.csv` 为主记录、`mcp-log.md` 为说明文档。
- 将 `general/criterion-rust/` 下 `规范指导_*` 文件统一重命名为 `规范守则_*`，并同步更新文内标题与术语保持一致。

## [0.8.0] - 2025-10-11
### 变更 (Changed)
- 更新 general 目录指引，统一要求将`AI-AGENT_working-status.csv`、`undetermined.md`、`optimized-task.md`、`mcp-log.md`等辅助文档存放于`ai-agent-output/YYYY-MM-DDTHH-MM-SS_UTC_任务简述/`目录，并同步调整MCP日志路径。
- 在通用流程与检查清单中补充提交顺序规范：提交前执行`git add .`，并在更新工作状态后优先维护`CHANGELOG.md`。
- 在指令体系中新增强制要求：每次任务的“文档更新”环节必须维护`CHANGELOG.md`并更新版本号（创建新版本段落、写入日期并重建空的`[Unreleased]`区块）。

## [0.7.0] - 2025-09-02

### 变更 (Changed)
- 优化任务执行流程：整合分步提交、AI_AGENT文件变更检查和任务完成清理机制
- 增加任务开始前AI_AGENT文件变更状态检查机制
- 添加分步提交规范，确保每个步骤完成后及时提交  
- 强化CHANGELOG维护检查流程
- 增加任务完成后的清理检查项（清理AI_AGENT.md、now-task.md、undetermined.md等）
- 更新检查清单以涵盖完整的任务执行生命周期

## [0.6.0] - 2025-08-30

### 新增 (Added)
- 在AI-AGENT_appointment.md中添加了复杂问题分析规范，要求对复杂问题使用sequential-thinking MCP服务
- 在AI-AGENT_appointment.md中添加了专业化代理选择规范，明确不同Rust项目类型对应的代理选择标准
- 完善了编码阶段的指导原则，强化了技术栈匹配和代理协作开发的要求

### 变更 (Changed)
- 更新了AI_AGENT.md中的任务内容，明确了本次任务的具体目标和完成情况
- 优化了开发流程规范的结构化表达，提高了操作指导的精准性

## [0.5.0] - 2025-08-30

### 新增 (Added)
- 创建了5个Rust专业化子代理：
  - `rust-cli-developer.md` - CLI应用开发专家
  - `rust-web-developer.md` - Web服务开发架构师  
  - `rust-library-developer.md` - 库项目开发专家
  - `rust-crossplatform-developer.md` - 跨平台开发架构师
  - `rust-performance-developer.md` - 高性能系统开发工程师
- 每个子代理都基于相应的Rust项目模板，提供针对性的专业指导
- 所有子代理都严格遵循架构设计原则，避免代码坏迹象
- 为不同应用场景提供了完整的技术栈和最佳实践指导

## [0.4.0] - 2025-08-30

### 新增 (Added)
- 添加了项目级别的通用代理配置文件（AI_AGENT.md）
- 添加了通用约定配置文件（AI-AGENT_appointment.md）
- 添加了general目录下的项目和用户级配置文件
- 添加了专业化代理目录结构（specialization-agents/）

### 变更 (Changed)
- 更新了README.MD，明确项目用途和任务说明
- 优化了general目录下的README结构
- 删除了过时的主指令文件（原 CLAUDE-main.md）

## [0.3.0] - 2025-08-30

### 新增 (Added)
- 添加了时间处理规范，要求使用 Python 命令获取实时时间
- 明确禁止使用硬编码时间或假设日期

## [0.2.0] - 2025-08-30

### 新增 (Added)
- 完善了 AI-AGENT_appointment.md 文档，添加了完整的开发流程指导
- 添加了 Git 分支管理策略和规范
- 添加了提交信息规范（约定式提交）
- 添加了 Changelog 维护指南和格式示例（包含 [Unreleased] 使用说明）
- 添加了文档检阅要求和更新规范
- 添加了未知问题处理策略
- 添加了代码审查和回滚准备要求
- 创建了 CHANGELOG.md 文件

### 变更 (Changed)
- 更新了核心开发流程，在流程开始添加了"检阅@AI_AGENT.md"步骤
- 更新了流程末尾，添加了"提交变更"步骤
- 重组了文档结构，添加了前置准备、编码与测试、版本控制等章节

## [0.1.0] - 2025-08-30

### 新增 (Added)
- 初始项目结构
- 基础 Rust 开发模板文档
- 通用指令文档（AI_AGENT 主指令、AI-AGENT_appointment.md）
- PlantUML 流程图设计规范
