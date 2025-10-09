# Rust项目开发规范 - 精简版AI_AGENT.md指南

## 核心开发原则

### 代码组织
- 使用清晰的模块结构，单一职责原则
- 工作区项目采用多crate架构
- 避免循环依赖，使用依赖注入

### 错误处理
- 统一使用`Result<T, E>`类型，避免panic
- 使用`thiserror`或`anyhow`进行错误管理
- 提供有意义的错误信息和恢复建议

### 性能优化
- 优先使用零成本抽象
- 合理选择智能指针（Box/Rc/Arc）
- 异步代码使用`tokio`生态系统

### 代码质量
- 所有公共API必须有文档注释
- 保持测试覆盖率>80%
- 使用`rustfmt`和`clippy`保持代码质量

## 项目配置标准

### Cargo.toml要求
```toml
[package]
edition = "2021"
license = "MIT OR Apache-2.0"
description = "简短项目描述"
repository = "https://github.com/user/project"
keywords = ["相关", "关键词"]
categories = ["development-tools"]

[profile.release]
lto = true
codegen-units = 1
strip = true
```

### 开发工具配置
- 使用`rust-toolchain.toml`锁定工具链版本
- 配置`rustfmt.toml`统一代码格式
- 设置`clippy.toml`定制检查规则

### CI/CD要求
- 自动化测试（单元、集成、文档测试）
- 代码格式检查和静态分析
- 多平台构建验证
- 依赖安全审计

## 测试策略

### 测试分层
- **单元测试**：测试单个函数/方法
- **集成测试**：测试模块间交互
- **基准测试**：性能关键代码性能验证

### 测试覆盖
- 正常情况、边界条件、错误情况
- 异步代码使用`tokio-test`
- Mock和测试替身使用`mockall`

## 文档规范

### 代码文档
- 所有`pub`项目必须有文档注释
- 包含使用示例和错误说明
- 使用`cargo doc`验证文档生成

### 项目文档
- `README.md`：项目介绍、安装、基本使用
- `CONTRIBUTING.md`：贡献指南
- `CHANGELOG.md`：版本变更记录

## 依赖管理

### 依赖选择原则
- 优先使用成熟、维护活跃的crate
- 避免重复功能的依赖
- 定期更新和安全审计

### 特性管理
- 使用feature flags控制可选功能
- 默认feature集合保持最小
- 在工作区中统一管理依赖版本

## 发布流程

### 版本管理
- 遵循语义化版本控制
- 维护详细的变更日志
- 使用git tag标记发布版本

### 发布检查清单
- [ ] 所有测试通过
- [ ] 文档更新完整
- [ ] 版本号正确更新
- [ ] 变更日志记录完整
- [ ] 安全漏洞检查通过