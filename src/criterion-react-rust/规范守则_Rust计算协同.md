# 规范守则 - React(TypeScript) 与 Rust 计算协同

## 适用范围
- 需要在 React(TypeScript) 项目中调用 Rust 高性能逻辑或将 Rust 作为后台服务、桌面容器的团队。
- 支持 Web、Edge、桌面（Tauri）、命令行等多环境部署。

## 方案对比概览
| 场景 | 推荐方案 | 备选方案 | 优势 | 限制 |
| --- | --- | --- | --- | --- |
| Web/云原生前端 | **Rust 服务端 (Axum/Actix) + REST/gRPC + React 前端** | WASM、Dioxus SSR | 技术栈成熟、易扩展、可独立部署 | 需维护服务端部署、客户端需处理网络延迟 |
| 浏览器内高性能计算 | **Rust → WASM（wasm-pack） + React** | Web Worker + Rust、Service Worker | 计算贴近用户、共享业务逻辑 | 与 DOM 交互受限，调试工具链更复杂 |
| 桌面应用 | **Tauri 2 + React(TypeScript)** | Dioxus Desktop、Electron + Rust后端 | 轻量、安全、可调用原生API，包体小 | 需关注 Tauri 与 Rust 版本兼容性、UI 部分仍依赖 Web 技术 |
| 全栈 Rust UI | **Dioxus (Rust) + React 互操作** | Yew、Leptos | Rust 端统一 UI & 逻辑，可跨桌面/浏览器 | 生态仍在演进，开发体验与 React 有差异 |
| 批处理/CLI 集成 | **Rust CLI + React 管理后台** | Wasm CLI、Axum 后台任务 | Rust CLI 性能强，React 负责监控与配置 | 需要同步 CLI 与前端 API 协议 |

## 架构原则
1. **模块化与共享类型**：使用 `cargo workspace` + `pnpm workspace`；通过 `typeshare`、`typify` 或自定义生成器在 Rust/TS 间共享类型。
2. **接口契约清晰**：REST 使用 OpenAPI/Swagger、gRPC 使用 `tonic`；WASM 使用 `wasm-bindgen` 暴露类型安全接口。
3. **安全与性能**：
   - 服务端：Rust API 使用 `tower` 中间件进行速率限制、JWT 校验。
   - WASM：隔离时间耗时操作，避免阻塞主线程，配合 Web Worker。
   - Tauri：遵循最小权限原则、白名单调用。

## 方案分析
### Rust 服务端 + React 前端
- 文档：Axum + React示例 <https://dev.to/alexeagleson/how-to-set-up-a-fullstack-rust-project-with-axum-react-vite-and-shared-types-429e>
- **优点**：前后端解耦、利于云部署、可使用 REST/gRPC/WebSocket；配合 `sqlx`/`sea-orm` 实现可靠后端。
- **限制**：需维护服务端运行环境、横向扩展成本。
- **最佳实践**：使用 `openapi` + `ts` 生成客户端 SDK；CI 中执行 `cargo fmt/lint/audit` 与 `pnpm lint/test`。

### Rust → WASM
- 文档：MDN Rust to Wasm、React + WASM 示例。
- **优点**：无需网络往返、可在边缘运行；适合图像处理、加密、复杂计算。
- **限制**：与 DOM 交互需通过 JS glue；部分 API 不可用（如多线程，除非使用 `wasm32-wasi`）。
- **建议**：使用 `wasm-pack build --target bundler`，在 Vite/Next 中通过 `async` 动态导入；性能关键逻辑放入 Web Worker。

### Tauri 2 + React
- 文档：<https://dev.to/rain9/tauri-2-quick-start-with-tauri-react-open-source-h5n>
- **优点**：Rust 后端接入系统 API，前端复用 React 生态；包体远小于 Electron。
- **限制**：Tauri 对 Rust edition/依赖有兼容要求（Issue #11829）；需要处理多窗口、状态共享。
- **建议**：`src-tauri` 管理命令与状态，React 层通过 `@tauri-apps/api` 交互；CI 中打包 `.appimage/.msix` 等。

### Dioxus / Rust UI
- 文档：Dioxus 0.7 Roadmap、社区反馈。
- **优点**：全Rust栈、无TS；支持Web、桌面、TUI。
- **限制**：生态尚新，UI能力与React不同；适合作为实验或局部替换。

## 测试与运维
- **单元测试**：Rust 使用 `cargo test`、React 使用 `pnpm test`；WASM 使用 `wasm-pack test --node`。
- **端到端测试**：Playwright（覆盖 SSR/WASM/Tauri）。
- **性能监控**：
  - 服务端：`tracing` + OpenTelemetry；部署 Prometheus/Grafana。
  - 前端：Web Vitals、Sentry、Datadog RUM。
  - Tauri：`tauri::plugin::log`，收集系统日志。
- **CI/CD**：
  - GitHub Actions matrix：`cargo fmt/clippy/audit`、`pnpm lint/test/build`。
  - WASM/Edge：构建时执行 `wasm-pack` 并上传到 CDN。
  - Tauri：`tauri-action` 打包并签名。

## 参考资料
- Axum + React 全栈模板：<https://dev.to/alexeagleson/how-to-set-up-a-fullstack-rust-project-with-axum-react-vite-and-shared-types-429e>
- wasm-pack + React 模板：<https://github.com/gumonteilh-hub/react-wasm-template>
- Tauri 官方模板：<https://github.com/dannysmith/tauri-template>
- Dioxus Roadmap 与讨论：<https://github.com/DioxusLabs/dioxus/discussions/3523>
- Rust/React 性能优化案例：<https://medium.com/@theNewGenCoder/react-rust-webassembly-for-high-performance-frontends-0ce804edd714>
