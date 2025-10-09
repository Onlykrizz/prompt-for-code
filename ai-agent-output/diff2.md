# specialization-agents (A) 与 rust/规范指导系 (B) 差异对照

## 总体差异
- A独有：
  - **代理元信息注册**：通过 YAML 头描述代理身份、模型继承与配色，B 无对应元数据（specialization-agents/rust-cli-developer.md:1-6）。
  - **行为准则/方法论约束**：反复强调沟通语言、KISS/YAGNI/DRY/SOLID 等原则及坏味道处理流程（specialization-agents/rust-cli-developer.md:10-24, specialization-agents/rust-cli-developer.md:90-101）。
  - **文档归档流程**：要求将正式文档放入 `docs/`、讨论材料放入 `discuss/`（specialization-agents/rust-cli-developer.md:109-113）。
- B独有：
  - **依赖清单与版本**：列出 `Cargo.toml` 片段明确版本号，A 仅给库名（rust/规范指导_CLI应用模板.md:35-58）。
  - **项目结构模板**：提供目录树帮助快速搭建骨架（rust/规范指导_CLI应用模板.md:60-71）。
  - **可直接复用的代码示例**：包含 `main`、错误处理、特性配置等完整片段（rust/规范指导_Web服务模板.md:111-148, rust/规范指导_高性能系统项目模板.md:127-152）。

## CLI 场景
- A独有：
  - **用户体验与安全准则**：强调 CLI 需提供标准选项、确认机制、进度指示（specialization-agents/rust-cli-developer.md:32-87）。
  - **质量门槛与坏味道警示**：要求发现坏味道先征询用户并给出建议（specialization-agents/rust-cli-developer.md:90-101）。
- B独有：
  - **命令行结构体模板**：给出 `Cli`、`Commands` 的 `clap` 派生示例（rust/规范指导_CLI应用模板.md:77-107）。
  - **入口函数骨架**：示范 `main` 中日志设置与子命令分发（rust/规范指导_CLI应用模板.md:110-126）。
  - **测试要点列表**：列出 `assert_cmd` 与退出码校验等具体用例（rust/规范指导_CLI应用模板.md:130-134）。

## Web 服务场景
- A独有：
  - **架构原则抽象**：分层职责、异步优先、可观测性等整体约束（specialization-agents/rust-web-developer.md:32-124）。
  - **部署与运维策略**：涵盖 Docker、蓝绿发布、配置隔离（specialization-agents/rust-web-developer.md:147-151）。
- B独有：
  - **服务启动代码**：`axum` 路由、状态注入、监听逻辑可直接复制（rust/规范指导_Web服务模板.md:111-148）。
  - **统一错误响应实现**：`AppError` 与 `IntoResponse` 具体写法（rust/规范指导_Web服务模板.md:151-199）。
  - **请求处理与服务层样例**：`create_user`、`UserService` 等业务模板（rust/规范指导_Web服务模板.md:200-276）。

## 库项目场景
- A独有：
  - **API 设计哲学**：零成本抽象、渐进式披露、组合优先（specialization-agents/rust-library-developer.md:32-53）。
  - **生态与版本策略**：语义化版本、deprecated 迁移、社区集成（specialization-agents/rust-library-developer.md:146-182）。
- B独有：
  - **`lib.rs` 注释与导出模板**：含 `#![deny(missing_docs)]`、公共 API re-export（rust/规范指导_库项目模板.md:84-121）。
  - **错误类型与 Result 别名实现**（rust/规范指导_库项目模板.md:123-145）。
  - **构建器模式范例**（rust/规范指导_库项目模板.md:147-181）。

## 跨平台场景
- A独有：
  - **平台抽象策略说明**：trait 统一接口、工厂模式、条件编译集中管理（specialization-agents/rust-crossplatform-developer.md:86-109）。
  - **发行与 UX 规范**：安装体验、自动更新、平台限制记录（specialization-agents/rust-crossplatform-developer.md:132-143, specialization-agents/rust-crossplatform-developer.md:166-172）。
- B独有：
  - **平台操作 trait 与实现骨架**（rust/规范指导_跨平台项目模板.md:93-121）。
  - **路径/进程/信号工具代码**：涵盖 UNC 处理、`which` 查找、跨平台信号监听（rust/规范指导_跨平台项目模板.md:124-205, rust/规范指导_跨平台项目模板.md:206-240）。
  - **交叉编译脚本模板**（rust/规范指导_跨平台项目模板.md:246-300）。

## 高性能系统场景
- A独有：
  - **性能目标与指标体系**：P99 延迟、QPS、资源效率等硬指标（specialization-agents/rust-performance-developer.md:32-37）。
  - **性能工程流程**：监控、分析工具、回归测试策略（specialization-agents/rust-performance-developer.md:144-197）。
- B独有：
  - **内存分配器与锁自由结构代码**：`fast_alloc`、`HighPerformanceQueue` 等实现（rust/规范指导_高性能系统项目模板.md:127-194）。
  - **Cargo Profile 优化配置示例**（rust/规范指导_高性能系统项目模板.md:74-96, rust/规范指导_高性能系统项目模板.md:196-200）。
  - **依赖与推荐库清单**：`tokio`、`crossbeam`、`bytes` 等精确版本（rust/规范指导_高性能系统项目模板.md:35-72）。
