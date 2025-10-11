# 变更日志 (Changelog)

所有显著的变更都会记录在此文件中。

本项目遵循[语义化版本](https://semver.mdn.cn/)规范。

## [Unreleased]

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
