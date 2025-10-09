- `specialization-agents` 目录下的文档主要用于定义 AI 代理的角色定位与协作规范，其结构以 YAML 头部开始，说明代理名称、描述、颜色等元信息，随后集中阐述交流语言、KISS/YAGNI/DRY/SOLID 等核心编程原则、核心职责、质量标准以及文档归档要求，并强调在识别代码坏味道时需先征询用户是否优化。例如：`specialization-agents/rust-cli-developer.md:1`、`specialization-agents/rust-cli-developer.md:10`、`specialization-agents/rust-cli-developer.md:100`、`specialization-agents/rust-cli-developer.md:109`。
- `rust` 目录下的 “规范指导***.md” 文档定位为具体项目模板或实践手册，完全聚焦于给出可落地的技术规范：列出带版本号的依赖、项目结构树、代码片段、配置示例以及测试与发布清单，例如 `rust/规范指导_CLI应用模板.md:35`、`rust/规范指导_CLI应用模板.md:110`、`rust/规范指导_Web服务模板.md:111`、`rust/规范指导_Web服务模板.md:151`。
- 二者整体关系是方法论与实施层的分工：`specialization-agents` 文档教会代理“如何思考与协作”，而 `rust/规范指导` 文档告诉开发者“具体怎么写和配置”。

### CLI 场景
- `rust/规范指导_CLI应用模板.md`：列出 `clap`、`anyhow`、`serde`、`dirs` 等依赖版本，给出命令行结构体、`main` 函数、项目目录、测试要点等具体实现细节（`rust/规范指导_CLI应用模板.md:35`、`rust/规范指导_CLI应用模板.md:60`、`rust/规范指导_CLI应用模板.md:77`、`rust/规范指导_CLI应用模板.md:110`）。
- `specialization-agents/rust-cli-developer.md`：强调用户体验优先、遵循 CLI 约定、数据安全与确认机制，并附加团队协作与质量准则（`specialization-agents/rust-cli-developer.md:32`、`specialization-agents/rust-cli-developer.md:83`、`specialization-agents/rust-cli-developer.md:90`、`specialization-agents/rust-cli-developer.md:109`）。

### Web 服务场景
- `rust/规范指导_Web服务模板.md`：提供 `axum` 启动代码、错误处理、服务层示例和配置加载逻辑，可直接复制到项目中（`rust/规范指导_Web服务模板.md:111`、`rust/规范指导_Web服务模板.md:151`、`rust/规范指导_Web服务模板.md:194`、`rust/规范指导_Web服务模板.md:229`）。
- `specialization-agents/rust-web-developer.md`：针对分层架构、异步优先、类型安全、性能和安全要求给出全面约束，并覆盖可观测性、部署策略（`specialization-agents/rust-web-developer.md:32`、`specialization-agents/rust-web-developer.md:74`、`specialization-agents/rust-web-developer.md:98`、`specialization-agents/rust-web-developer.md:140`）。

### 库项目场景
- `rust/规范指导_库项目模板.md`：展示 `lib.rs`、错误类型、构建器模式、feature 配置等模板，并说明文档与测试策略（`rust/规范指导_库项目模板.md:84`、`rust/规范指导_库项目模板.md:125`、`rust/规范指导_库项目模板.md:147`、`rust/规范指导_库项目模板.md:183`）。
- `specialization-agents/rust-library-developer.md`：聚焦 API 设计哲学、特性管理、文档发布流程及生态建设（`specialization-agents/rust-library-developer.md:32`、`specialization-agents/rust-library-developer.md:53`、`specialization-agents/rust-library-developer.md:86`、`specialization-agents/rust-library-developer.md:146`）。

### 跨平台场景
- `rust/规范指导_跨平台项目模板.md`：提供平台抽象 trait、路径/进程管理代码、信号处理与交叉编译脚本，直接指导实现（`rust/规范指导_跨平台项目模板.md:93`、`rust/规范指导_跨平台项目模板.md:124`、`rust/规范指导_跨平台项目模板.md:186`、`rust/规范指导_跨平台项目模板.md:246`）。
- `specialization-agents/rust-crossplatform-developer.md`：强调平台抽象、条件编译策略、测试矩阵与用户体验一致性（`specialization-agents/rust-crossplatform-developer.md:86`、`specialization-agents/rust-crossplatform-developer.md:98`、`specialization-agents/rust-crossplatform-developer.md:110`、`specialization-agents/rust-crossplatform-developer.md:132`）。

### 高性能系统场景
- `rust/规范指导_高性能系统项目模板.md`：包含内存分配器、无锁队列、Cargo profile 优化配置等示例（`rust/规范指导_高性能系统项目模板.md:127`、`rust/规范指导_高性能系统项目模板.md:154`、`rust/规范指导_高性能系统项目模板.md:192`、`rust/规范指导_高性能系统项目模板.md:197`）。
- `specialization-agents/rust-performance-developer.md`：设定性能目标、内存优化策略、并发模型、监控与测试要求，指导如何组织性能工程（`specialization-agents/rust-performance-developer.md:32`、`specialization-agents/rust-performance-developer.md:61`、`specialization-agents/rust-performance-developer.md:79`、`specialization-agents/rust-performance-developer.md:165`）。

总体而言，`specialization-agents` 提供战略层面的“行为准则+质量门槛”，`rust/规范指导` 系列提供战术层面的“直接可复用的技术方案与代码模板”。EOF
