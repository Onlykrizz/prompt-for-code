# 流程设计

## 修改范围
- `general/AI-AGENT_general.md`
- `general/AI-AGENT_programming.md`
- `general/AI-AGENT_project.md`
- `general/AI-AGENT_check.md`
- `general/AI-AGENT_step-before.md`
- `general/README.md`
- `CHANGELOG.md`

## 核心新增要求
1. 在文档更新阶段明确两项动作：
   - 维护 `CHANGELOG.md` 内容；
   - 更新版本号：创建新版本条目、写入日期、重建空的 `[Unreleased]` 区块。
2. 检查清单与项目级摘要需同步强调上述顺序。
3. 参考现有最新版本 `0.7.0`，计划将当前变更发布为 `0.8.0`（日期采用任务执行日）。

## 执行步骤
1. 更新流程性文档（general、programming、project、step-before、README），在文档更新或收尾段落添加“维护 CHANGELOG 并更新版本号（含新条目与 Unreleased 重建）”描述。
2. 调整 `AI-AGENT_check.md`，在文档更新与收尾检查项加入版本号更新确认。
3. 迁移 `CHANGELOG.md` 中 `[Unreleased]` 内容至 `0.8.0` 段落，写入日期 `2025-10-11`，新增空的 `[Unreleased]`。
4. 复核所有文档用语保持一致，使用 `rg` 检查 `CHANGELOG`、`版本号`、`Unreleased` 等关键词，确保无遗漏。

## 验证计划
- 对照 `optimized-task.md` 中的验证标准逐项确认。
- 手动自检 CHANGELOG，确保存在新版本段落与空 `[Unreleased]`。
- 使用 `git diff` 确认所有目标文件已更新预期内容。
