# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个构建用于 Claude Code 的提示词模板库，包含通用指令和 Rust 特定的开发模板。

## 核心开发流程

### 1. 文档检阅与更新
- **开始前**：必须重新检阅 @CLAUDE.md
- **完成后**：将相关变动写入 @CLAUDE.md

### 2. 版本控制规范
- 每个功能在独立 Git 分支开发
- 完成后创建 Git 提交
- 遵循[语义化版本](https://semver.mdn.cn/)维护 changelog

### 3. 设计优先原则
遵循流程：`检阅@CLAUDE.md → 程序流程设计 → 编写代码 → 测试验证 → 文档更新 → 提交变更`

使用 PlantUML 进行流程图设计：
```bash
# 生成 PNG 格式流程图
java -jar "D:\service\my-tools\jar\plantuml.jar" program_flowchart/src/[文件名].txt -tpng -o ../png
```

### 4. 不确定性处理
遇到未知问题或模糊情况时，必须明确表示"我不知道"并询问用户。

## 项目结构

- `general/` - 通用开发指令
  - `CLAUDE-main.md` - 主指令文件
  - `CLAUDE-appoint.md` - 开发过程要求（含详细流程规范）
- `rust/` - Rust 项目模板（CLI、Web服务、库、跨平台、高性能系统）
- `program_flowchart/` - 流程图文档（src/png/txt）
- `CHANGELOG.md` - 版本变更记录

## 最近更新

### 2025-01-29
- 完善了 CLAUDE-appoint.md，添加了完整的开发流程指导
- 新增 Git 分支管理策略和提交规范
- 创建了 CHANGELOG.md 文件
- 添加了代码审查和回滚准备要求
- 整合了 README.md 中的所有新需求