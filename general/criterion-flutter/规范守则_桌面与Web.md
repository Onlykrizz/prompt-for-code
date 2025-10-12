# 规范守则 - 桌面与Web

## 项目类型
- Flutter Web、Windows、macOS、Linux 桌面应用，以及统一代码跨端交付。
- 常见需求：自适应布局、热键、文件系统访问、PWA/桌面安装包。

## 核心原则
### 1. 平台适配
- 启用 `flutter config --enable-web/--enable-windows` 等必要开关，使用 `kIsWeb`、`Platform.isX` 控制平台差异。
- Web 环境遵循 [Flutter Web 性能与限制](https://docs.flutter.dev/platform-integration/web) 建议，避免大量自定义绘制；桌面端注意窗口大小调整。
- 使用 `go_router` 或 `beamer` 支持URL导航与浏览器历史管理。

### 2. UI 与输入体验
- 采用响应式布局方案（`LayoutBuilder`、`MediaQueryData`、`AdaptiveLayout`）。
- 桌面端提供键鼠支持：使用 `Shortcuts`、`Actions`、`FocusTraversalGroup`。
- Web PWA：配置 `web/manifest.json`、`service_worker.js`，并评估SEO需求。

### 3. 原生集成
- 桌面：使用 `ffi` 调用原生动态库或通过插件访问系统API；保持安全约束（签名/沙盒）。
- Web：与 JavaScript 互操作使用 `dart:js_interop`，注意异步Promise与错误处理。

## 项目结构建议
```
desktop_web_app/
├── lib/
│   ├── main.dart
│   ├── bootstrap.dart          # Web入口（JS interop初始化）
│   ├── presentation/
│   └── infrastructure/
├── web/
│   ├── index.html
│   ├── manifest.json
│   └── sw.js
├── linux/
├── macos/
├── windows/
└── test/
```

## 测试与交付
- Web：使用 `flutter test --platform chrome`、`integration_test` 结合 `puppeteer` 或 `cypress` 进行端到端验证。
- 桌面：利用 `integration_test` + `flutter drive --target`；构建后通过 `msix`、`dmg`、`AppImage` 分发。
- 持续集成：GitHub Actions、Azure Pipelines，分别构建多平台产物并运行 `flutter analyze`、`dart test`。

## 可观测性与优化
- Web性能：开启 `CanvasKit` 并按需启用`--web-renderer`；使用Chrome DevTools分析CPU/GPU瓶颈。
- 桌面性能：关注帧率、内存；必要时采用 `Platform.isLinux` 等条件下启用原生菜单/托盘。
- 日志：使用 `logger` 包统一输出；Web端上传到ELK/Datadog，桌面端写入本地文件并定期上传。

## 参考资料
- [Flutter Web Best Practices](https://docs.flutter.dev/deployment/web)
- [Desktop support for Flutter](https://docs.flutter.dev/platform-integration/desktop)
- [go_router documentation](https://pub.dev/packages/go_router)
- [Flutter PWA Guide](https://docs.flutter.dev/deployment/web#progressive-web-apps)
- [Flutter Windows packaging (msix)](https://docs.flutter.dev/deployment/windows)
