# 规范守则 - Flutter 与 Rust 计算协同

## 适用范围
- Flutter 移动/桌面/Web 应用需要引入高性能、跨平台的 Rust 业务逻辑或算法。
- 既可采用嵌入式模式（Flutter 调用本地 Rust 动态库），也可采用 WebAssembly、后台服务、Tauri 桌面封装等方案。

## 推荐方案概览
| 场景 | 首选方案 | 备选方案 | 关键优势 | 主要限制 |
| --- | --- | --- | --- | --- |
| 移动/桌面本地计算 | **flutter_rust_bridge** + 模块化 Rust crate | 原生 FFI 模板、UniFFI | 类型安全、高性能、自动代码生成、Flutter Favorite 生态 | 需维护 bridge 生成流程，跨平台 CI 配置复杂 |
| Flutter Web / 跨端统一 | **Rust → WASM** + Flutter Web wasm renderer | 单独 Web 后端服务 | 浏览器端高性能、共享业务逻辑 | 对 DOM 交互有限制，调试工具链相对复杂 |
| 桌面应用 | **Tauri + Flutter** (Hybrid) | Rust FFI 嵌入 Flutter Desktop | 可复用 Rust 命令系统、轻量分发、访问原生 API | UI 需要在 Flutter 与 webview/Tauri 间协调；Tauri 对 Rust 版本有兼容性注意事项 |
| 原生扩展/插件发布 | **Federated 插件 + flutter_rust_bridge/FFI** | UniFFI | 支持发布到 pub.dev，易于复用 | 需要维护多平台脚本与示例工程 |

> 实践建议：将核心性能敏感逻辑封装为独立 Rust crate，暴露稳定接口；使用 flutter_rust_bridge 自动生成桥接代码，同时保留纯 FFI fallback 以应对特殊平台需求。

## 架构原则
1. **双仓或Monorepo管理**：推荐 Flutter 与 Rust 采用同仓 monorepo（melos + cargo workspace），便于共享CI与版本号；如需独立仓库，使用 Git submodule 或自定义脚本同步。
2. **边界清晰**：在 Dart 层定义 service/bridge，对外暴露纯 Dart API；Rust 层维持 domain/service 模块，禁止将平台细节泄露至 UI。
3. **类型与错误统一**：使用 `flutter_rust_bridge` 的自定义类型或 `serde` 序列化；错误统一转译为 `RustError` → `FlutterError`，记录错误码。
4. **性能考虑**：跨 FFI 调用需批量化；大数据传输采用 `zero-copy` (FRB 支持) 或共享内存；异步任务使用 `tokio`/`async-std` 搭配 `FlutterBackgroundExecutor`。

## 方案评估
### flutter_rust_bridge（FRB）
- 官方文档：[Quickstart](https://cjycode.com/flutter_rust_bridge/quickstart) | [性能指南](https://cjycode.com/flutter_rust_bridge/guides/performance/overview)
- **优点**：
  - 自动生成桥接代码，支持任意复杂类型、Stream/async；获得 Flutter Favorite。 
  - Flutter/Dart 层仅需引入自动生成文件，减少手写 unsafe FFI。
  - 支持 iOS/Android/macOS/Windows/Linux；结合 `cargo ndk`、`cargo lipo`。
- **注意事项**：
  - 需要在CI中安装Rust与Dart工具链，定期运行 `frb_codegen`。
  - 大批量数据传输仍需关注内存占用，可考虑压缩或分页。

### 纯 FFI / UniFFI
- FFI 模板示例：[flutter-rust-ffi](https://github.com/brickpop/flutter-rust-ffi)
- UniFFI 文档：[Guide](https://mozilla.github.io/uniffi-rs/latest/)
- **优点**：最大灵活性、无额外生成层；UniFFI 支持多语言共享。
- **限制**：需要手动处理 `unsafe`、内存管理、类型转换；开发成本较高。
- **适用场景**：对生成器不信任、需要极致控制，或已采用 UniFFI 服务多平台的团队。

### Rust → WASM
- 官方文档：[Flutter Web WASM](https://docs.flutter.dev/platform-integration/web/wasm)
- **优点**：在浏览器端运行高性能逻辑，避免服务器往返。
- **限制**：访问平台资源有限；WASM 与 Dart 交互需考虑数据拷贝；调试工具链较新。
- **适用场景**：Flutter Web 应用或需在多端共享算法的场合。

### Tauri / 混合方案
- Tauri + React 示例可借鉴架构；对 Flutter，可在桌面端同时运行 Tauri 容器 + Flutter 外壳，以Rust驱动系统级能力。
- **优点**：提供现成命令系统、插件生态、轻量包体。
- **限制**：与Flutter桌面组合需要自定义通信（如通过Localhost API）；Tauri对Rust edition存在兼容问题（Issue #11829）。

## 测试与运维
- **单元测试**：Rust 层使用 `cargo test`；Dart 层 `flutter test`。可通过 `flutter_rust_bridge` 提供的调试宏输出日志。
- **集成测试**：使用 `integration_test` 调用实际Rust接口；必要时在CI设备农场运行。
- **性能监控**：对关键调用点记录耗时；Rust使用 `tracing` 输出；Flutter端结合 `DevTools`/Crashlytics。
- **发布策略**：
  - 移动端：在 CI 中编译对应架构动态库/静态库，并将生成产物打包入 Flutter Runner。
  - Web：提供 wasm 包与 loader JS，部署到 CDN；Flutter Web 配置 `--wasm` renderer。
  - 桌面：产出 `.msix`、`.dmg` 或 AppImage，确保 Rust 运行库随附。

## 参考资料
- flutter_rust_bridge：<https://pub.dev/packages/flutter_rust_bridge>
- Dart FFI 模板：<https://github.com/brickpop/flutter-rust-ffi>
- Flutter WASM 支持：<https://tech.appunite.com/posts/flutter-web-assembly-wasm>
- 社区反馈（性能、内存）：<https://github.com/fzyzcjy/flutter_rust_bridge/issues/2197>
- Rust 2024 回顾（移动融合）：<https://rust-dd.com/post/rust-2024-wrap-up-biggest-changes-and-future-outlook>
