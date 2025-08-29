# 变更日志 (Changelog)

所有显著的变更都会记录在此文件中。

本项目遵循[语义化版本](https://semver.mdn.cn/)规范。

## [Unreleased]

## [0.4.0] - 2025-08-30

### 新增 (Added)
- 添加了项目级别的Claude配置文件（CLAUDE.md）
- 添加了通用约定配置文件（CLAUDE-appoint.md）
- 添加了general目录下的项目和用户级配置文件
- 添加了专业化代理目录结构（specialization-agents/）

### 变更 (Changed)
- 更新了README.MD，明确项目用途和任务说明
- 优化了general目录下的README结构
- 删除了过时的CLAUDE-main.md文件

## [0.3.0] - 2025-08-30

### 新增 (Added)
- 添加了时间处理规范，要求使用 Python 命令获取实时时间
- 明确禁止使用硬编码时间或假设日期

## [0.2.0] - 2025-08-30

### 新增 (Added)
- 完善了 CLAUDE-appoint.md 文档，添加了完整的开发流程指导
- 添加了 Git 分支管理策略和规范
- 添加了提交信息规范（约定式提交）
- 添加了 Changelog 维护指南和格式示例（包含 [Unreleased] 使用说明）
- 添加了文档检阅要求和更新规范
- 添加了未知问题处理策略
- 添加了代码审查和回滚准备要求
- 创建了 CHANGELOG.md 文件

### 变更 (Changed)
- 更新了核心开发流程，在流程开始添加了"检阅@CLAUDE.md"步骤
- 更新了流程末尾，添加了"提交变更"步骤
- 重组了文档结构，添加了前置准备、编码与测试、版本控制等章节

## [0.1.0] - 2025-08-30

### 新增 (Added)
- 初始项目结构
- 基础 Rust 开发模板文档
- 通用指令文档（CLAUDE-main.md、CLAUDE-appoint.md）
- PlantUML 流程图设计规范