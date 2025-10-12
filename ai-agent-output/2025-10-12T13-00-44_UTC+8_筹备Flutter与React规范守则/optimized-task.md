# 优化后任务说明

## 背景
- 用户要求在 general 目录新增 Flutter 与 React(TypeScript) 的规范守则体系，并不再进行中途确认。
- 命名策略：新建 `general/criterion-flutter/` 与 `general/criterion-react/`，文档统一使用“规范守则_*”。
- Flutter 预期方向：移动与平板应用、桌面与Web、插件与平台通道、企业与可观测性、高性能与图形动画。
- React(TypeScript) 预期方向：单页应用与组件体系、SSR与边缘渲染、设计系统与可访问性、状态管理与数据同步、性能优化与质量保障。

## 目标
1. 为 Flutter 与 React 生成对应目录、README 与五份守则文档，覆盖所列方向。
2. 每份守则包含项目定义、核心原则、结构建议、工具与测试方案、运维要点、参考资料（突出TypeScript最佳实践）。
3. 记录调研过程中的关键资料与链接至 `mcp-log.md`。
4. 更新 `general/README.md`、`CHANGELOG.md`，保持多语言守则索引一致。

## 执行步骤
1. **进一步调研**
   - 总结 Flutter 官方文档、Dart/Flutter最佳实践、Google官方指南、社区经验。
   - 针对 React(TypeScript) 调研 React 官方文档、TypeScript Handbook、Next.js/Remix/Design System 资料、性能调优文章。
2. **文档撰写**
   - 创建 `criterion-flutter` 与 `criterion-react` 目录，先编写 README 与结构说明。
   - 逐份撰写守则文档，引用官方或权威资料，并给出项目骨架、工具链、测试与运维建议。
   - 采用与现有守则一致的格式与命名。
3. **验证与维护**
   - 使用 `rg` 检查命名一致性，确认无旧术语残留。
   - 自查文档结构完整与链接有效。
   - 更新 `CHANGELOG.md`（增加 0.11.0）与 `general/README.md`，重建空的 `[Unreleased]`。
4. **收尾**
   - 维护 `AI-AGENT_working-status.csv` 直至收尾阶段。
   - 清理临时笔记，确保所有改动已有提交。

## 成功标准
- `general/criterion-flutter/`、`general/criterion-react/` 目录存在并包含 README + 五份守则。
- 文档内容涵盖架构、工具、测试、运维及参考资料，突出 TypeScript／Flutter 特性。
- README 与 CHANGELOG 更新到位，状态记录与日志完整。
- 未创建新的 `mcp-log.csv`，所有MCP使用记录在 `mcp-log.md`。
