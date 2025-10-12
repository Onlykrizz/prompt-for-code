# 待定项清单

## 🔍 待定项U001 - Flutter+Rust目录与文档结构

### ✅ 方案S001 - 【建议采纳 +78分】

**📍 原文位置**：（general/criterion-flutter/README.md，第1-5行）
> # Flutter 项目规范守则套件

**🎯 优化方案**：
> 新建 `general/criterion-flutter-rust/` 目录，包含 README、`规范守则_Rust计算协同.md`、`项目创建与维护指导.md`，聚焦Flutter与Rust协同方案。

**⚖️ 权衡分析**：
- ✅ **优势**（+45分）：命名直接表达Flutter+Rust主题，与既有目录一一对应。
- ✅ **优势**（+40分）：结构明确，便于维护守则与实践指南。
- ❌ **风险**（-7分）：需要同步更新README索引与CHANGELOG。

---

## 🔍 待定项U002 - React+Rust目录与文档结构

### ✅ 方案S001 - 【建议采纳 +78分】

**📍 原文位置**：（general/criterion-react/README.md，第1-5行）
> # React (TypeScript) 项目规范守则套件

**🎯 优化方案**：
> 新建 `general/criterion-react-rust/` 目录，包含 README、`规范守则_Rust计算协同.md`、`项目创建与维护指导.md`，突出React TypeScript与Rust后台计算融合。

**⚖️ 权衡分析**：
- ✅ **优势**（+45分）：命名清晰，与TypeScript生态区分明确。
- ✅ **优势**（+40分）：和Flutter目录保持平衡，易于扩展。
- ❌ **风险**（-7分）：需保证React/TS特性在指南中体现。

---

## 🔍 待定项U003 - Flutter+Rust实现方案遴选

### ✅ 方案S001 - 【建议采纳 +85分】

**📍 原文位置**：（ai-agent-memory/now-task.md，第7-12行）
> 搜索所有可能的实现方案，例如flutter_rust_bridge、tauri、dioxus等...

**🎯 优化方案**：
> 重点推荐 `flutter_rust_bridge` + 模块化Rust库（ffi/UniFFI备选）的组合，并对Tauri、WASM方案做对比说明。

**⚖️ 权衡分析**：
- ✅ **优势**（+45分）：社区成熟度高，维护成本相对较低。
- ✅ **优势**（+45分）：可覆盖移动、桌面，性能与开发效率平衡。
- ❌ **风险**（-5分）：需要在Linux/Windows等平台测试ffi兼容性。

---

## 🔍 待定项U004 - React+Rust实现方案遴选

### ✅ 方案S001 - 【建议采纳 +84分】

**📍 原文位置**：（ai-agent-memory/now-task.md，第7-12行）
> 搜索所有可能的实现方案，例如flutter_rust_bridge、tauri、dioxus等...

**🎯 优化方案**：
> 推荐“Rust服务（Axum/Actix）+ React TypeScript 前端”作为主线，对 WASM（wasm-pack + React）、Tauri（桌面）与 Dioxus (Web) 进行对比，提供选择建议。

**⚖️ 权衡分析**：
- ✅ **优势**（+44分）：后端Rust可独立扩展，前端技术栈成熟。
- ✅ **优势**（+44分）：兼容云原生部署与边缘渲染；WASM/Tauri作为细分补充。
- ❌ **风险**（-4分）：需在文档中明确使用场景分类，避免方案混淆。

---
