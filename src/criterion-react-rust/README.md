# React(TypeScript) + Rust 协同守则套件

该目录面向以 TypeScript 为主的 React 应用与 Rust 计算模块的集成场景，覆盖服务端、WASM、Tauri 桌面、Dioxus 等方案。文档结构：

- `规范守则_Rust计算协同.md`：比较多种协同方式（Rust 后端 API、WASM、Tauri/Dioxus 桌面、命令行/批处理等），给出架构与运维建议。
- `项目创建与维护指导.md`：提供从项目初始化、共享类型、CI/CD到部署维护的操作指南，涵盖不同方案的步骤与风险提示。

使用建议：
1. 根据业务形态（Web、Edge、桌面、Hybrid）选择或组合合适方案。
2. 先阅读规范守则明确决策要点，再执行项目指导中的操作步骤。
3. 文档涉及的工具（Axum、Actix、wasm-pack、Tauri CLI、Dioxus）应在工程启动前完成环境准备。
