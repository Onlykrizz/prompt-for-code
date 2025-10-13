# 流程设计草案

## 文档覆盖范围
- `general/AI-AGENT_general.md`
- `general/AI-AGENT_programming.md`
- `general/AI-AGENT_check.md`
- `general/AI-AGENT_step-before.md`
- `general/AI-AGENT_project.md`
- `general/AI-AGENT_mcp-rules.md`
- `general/README.md`
- `general/undetermined-template.md`

## 修改要点拆解
1. **目录与文件存储规范**
   - 统一说明：`mcp-log.md`、`AI-AGENT_working-status.csv`、`undetermined.md`、`optimized-task.md` 等辅助文档必须存放在 `ai-agent-output/YYYY-MM-DDTHH-MM-SS_UTC_任务简述/` 目录。
   - 插入命名示例，强调任务简述 8-20 字要求。
   - 更新清理环节描述：不再删除上述文件，仅保留 `now-task.md` 初始化操作。
   - 替换 `record/mcp-log.md` 等旧路径引用。

2. **提交前追踪未追踪文件**
   - 在流程与提交规范部分强调：“每次执行 `git commit` 前必须运行 `git add .`，将未被 `.gitignore` 忽略的文件全部纳入追踪”。
   - 在编程补充指引中同步该规则，确保与测试脚本流程不冲突。
   - 在检查清单中加入核对项。

3. **CHANGELOG 维护顺序**
   - 在“文档更新”环节说明顺序：更新工作状态 → 维护 `CHANGELOG.md` → 创建 `git commit`。
   - 在编程指引与检查清单内同步这一顺序要求。

## 执行顺序
1. 先更新 `AI-AGENT_general.md` 与 `AI-AGENT_project.md`，确定基线描述。
2. 同步调整 `AI-AGENT_step-before.md`、`AI-AGENT_programming.md` 与模板、检查清单内容。
3. 修改 `AI-AGENT_mcp-rules.md` 中的日志路径，并在 `README.md`、`undetermined-template.md` 中更新示例。
4. 变更完成后统一校对术语与格式，再进入验证阶段。

## 验证计划
- 使用 `rg` 关键字检查：`record/`、`git add`、`CHANGELOG` 对应语句是否覆盖。
- 对照 `optimized-task.md` 验证标准逐项查验。
- 复核 `AI-AGENT_check.md` 的打勾项确保新增内容一致。