# 优化后任务说明

## 背景
- 用户要求在 general 目录中新增 Flutter+Rust、React(TypeScript)+Rust 的规范守则，并提供项目创建与维护指导。
- 守则需覆盖多种 Rust 集成方案（如本地 FFI、flutter_rust_bridge、UniFFI、WASM、Tauri、Rust 服务端等），针对不同场景给出优劣分析与推荐流程。
- 任务在执行过程中无需再次征求确认。

## 目标
1. 创建 `general/criterion-flutter-rust/` 与 `general/criterion-react-rust/` 目录，各包含 README、综合守则、项目创建与维护指导。
2. 在守则中比较并收录多种 Rust 集成路径（Flutter：FFI/FlutterRustBridge/WASM/Tauri；React：Rust服务端、WASM、Tauri、Dioxus等），针对性能、开发体验、部署自由度、跨平台兼容性给出适用场景。
3. 项目指导文档需覆盖：环境准备、骨架初始化、模块边界、CI/CD、调试与部署维护步骤。
4. 全程记录关键资料来源于官方文档、社区反馈（issue/blog）并在 `mcp-log.md` 摘要。
5. 更新 `general/README.md` 与 `CHANGELOG.md`，保证索引与版本信息同步。

## 执行步骤
1. **资料调研**
   - 搜索 flutter_rust_bridge、UniFFI、ffigen、WASM、Tauri、Dioxus 等官方文档与社区经验，记录优缺点。
   - 收集 Rust 作为后端微服务（Axum/Actix）、命令行、WASM包的实践案例与性能数据。
2. **文档结构设计**
   - 为每个目录撰写 README，说明适用范围与文件结构。
   - 编写 `规范守则_Rust计算协同.md`：列出多方案对比表、架构原则、测试与运维要求。
   - 编写 `项目创建与维护指导.md`：分步骤描述环境搭建、代码组织、接口定义、CI/CD、调试与部署。
3. **方案评估**
   - 在守则中明确“推荐方案”及“备选方案”，并列出决策依据（性能、开发效率、平台限制、社区活跃度）。
   - 对跨平台差异（移动/桌面/Web/Edge）进行补充说明。
4. **验证与维护**
   - 使用 `rg` 检查命名与术语一致性。
   - 自查文档引用链接可用，确保包含官方来源与社区反馈。
   - 更新 `CHANGELOG.md`（新增 0.12.0）和 `general/README.md` 索引。
5. **收尾**
   - 更新 `AI-AGENT_working-status.csv` 至收尾状态。
   - 清理临时记录，确保所有内容已提交。

## 成功标准
- `general/criterion-flutter-rust/` 与 `general/criterion-react-rust/` 目录完整，包含 README、守则文档、项目指导文档。
- 文档覆盖至少三种以上实现方案的对比与适用场景，提供项目搭建、调试、部署与维护流程。
- README/CHANGELOG 索引更新到位，日志与状态记录完整，未创建 `mcp-log.csv`。
