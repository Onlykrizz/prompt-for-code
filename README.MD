# 项目概述

这是一个构建用于 Claude Code 的提示词模板的项目。

## 项目结构

- **general/**: 通用模板和指南  
- **rust/**: Rust 语言的各种项目类型模板
- **specialization-agents/**: 专门化的开发者子代理定义

## Rust 专业化子代理

项目包含了以下5个专业化的 Rust 开发子代理：

1. **rust-cli-developer** - CLI应用开发专家
2. **rust-web-developer** - Web服务开发架构师
3. **rust-library-developer** - 库项目开发专家  
4. **rust-crossplatform-developer** - 跨平台开发架构师
5. **rust-performance-developer** - 高性能系统开发工程师

每个子代理都基于相应的 Rust 项目模板，为特定的应用场景提供专业的指导和最佳实践。

## 接下来的任务

接下来我希望再为它添加一些提示，把这些提示转为更合适、精准的表达，然后写入到CLAUDE-appoint.md中合适的位置：
- 当发现一个表面简短的问题实际上内含的目标与信息较多时，要交由sequential-thinking MCP服务进行分步思考
- 完成设计之后，开始编写程序代码时，根据可用的所有子代理，权衡程序特点与倾向选择最合适的子代理，将编程任务交给子代理完成，