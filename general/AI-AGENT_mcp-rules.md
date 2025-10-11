# AI-AGENT_mcp-rules.md

## 目标
- 为项目级 AI-AGENT 提供统一的 MCP 服务使用规范，确保选择得当、调用可追溯、风险可控。
- 指导代理在多 MCP 场景下分辨职责边界，避免重复调用或造成资源浪费。
- 保证所有外部服务调用均有日志、参数与结论记录，便于复盘与审计。

## 全局策略
- **工具选择**：以任务意图为先，避免同类服务并行调用；若存在原生能力可满足需求，优先使用本地/离线方案。
- **最小必要**：仅在确认输入、范围、速率后再调度 MCP；限定查询参数（结果数、时间窗、关键词等）。
- **结果可靠性**：输出需包含来源、时间戳与不确定性说明；可复核的要点优先。
- **可追溯性**：每次调用结束后立即在 `record/mcp-log.md` 中补全“工具调用简报”（触发原因、参数、结果概览、时间、是否重试）。
- **安全合规**：遵守目标服务的 ToS/隐私条款；严禁上传敏感数据；默认使用只读权限，若需写操作必须显式说明。
- **降级优先**：外部服务不可用时，应提供明确的降级方案或本地替代结论并标注风险。

## 安全与权限边界
- 严格遵守目录与网络白名单；如需扩展访问范围，须先更新根目录或凭证并记录原因。
- 涉及写操作或命令执行的服务必须评估对当前仓库/环境的影响，执行前向用户说明潜在副作用。

## 失败与降级流程
1. 判断失败原因（网络、权限、任务理解等）。
2. 如有备选服务，按优先级降级重试；无可替代方案时给出保守答案并记录阻塞因素。
3. 在 `mcp-log.md` 中补充失败说明和后续计划。

## 服务指引概览
| 服务 | 包名/入口 | 主要用途 | 写操作风险 |
| --- | --- | --- | --- |
| Filesystem | `@modelcontextprotocol/server-filesystem` | 受控文件读写、目录管理 | 高，需要限定根目录 |
| Playwright | `@playwright/mcp@latest` | 浏览器自动化、可访问性操作 | 中，涉及网页交互 |
| Shrimp Task Manager | `mcp-shrimp-task-manager` | 任务规划、执行与记忆持久化 | 中，写入数据目录 |
| DeepWiki | 远程 `https://mcp.deepwiki.com` | 仓库文档检索与问答 | 低，仅网络访问 |
| Desktop Commander | `@wonderwhy-er/desktop-commander` | 本地终端+文件系统增强 | 高，支持命令执行 |

## 服务详情

### 1. Filesystem（本地文件系统）
- **适用场景**：读取/写入仓库文件、查询目录结构、执行小范围文本替换。
- **启动建议**：使用 `npx @modelcontextprotocol/server-filesystem <allowed_dir>`；若客户端支持 Roots 协议，优先通过 Roots 动态下发访问目录。
- **使用要点**：
  - 操作前确认目标路径位于允许目录内，必要时更新 Roots 并记入日志。
  - 大文件编辑优先使用 `edit_file` + `dryRun` 预览差异，再执行正式修改。
  - `write_file` 为全量覆盖，适用于初始化或模板写入，需谨慎。
  - 使用 `list_allowed_directories` 与 `get_file_info` 核对权限及元数据。
- **风险防范**：禁止跨越白名单目录；若需创建/移动文件，应记录触发原因与回滚手段。
- **常用工具速览**：`read_text_file`、`read_media_file`、`edit_file`、`create_directory`、`list_directory_with_sizes`。

### 2. Playwright（浏览器自动化）
- **适用场景**：需要真实浏览器环境完成交互、获取动态内容、验证前端流程。
- **启动建议**：`npx @playwright/mcp@latest`；首次运行若提示未安装浏览器，调用 `browser_install`。
- **能力亮点**：
  - 通过可访问性树操作元素，避免截图识别；`browser_snapshot` 可获取结构上下文。
  - 提供点击、拖拽、表单填写、截图、PDF 输出、标签页管理、追踪记录等工具。
  - 可通过 `--caps=vision|pdf|verify|tracing` 启用额外功能，仅在确有需要时打开。
- **操作规范**：
  - 发送指令前描述目标元素（`element` 字段）与预期行为，确保权限请求准确。
  - 对外部网站遵守 robots 与速率限制，避免自动化滥用；必要时交替人工确认。
  - 动态页面建议先使用 `browser_wait_for` 等等待工具确保状态稳定。
- **输出要求**：保存关键截图或 PDF 结果，并在 `mcp-log.md` 标注 URL、步骤与耗时。

### 3. Shrimp Task Manager（智能任务管理）
- **适用场景**：需要让代理自主规划开发任务、跟踪执行状态、保持跨会话记忆。
- **部署提示**：`node dist/index.js` 或通过包管理器启动，务必设置 `DATA_DIR`（持久化目录），可选 `ENABLE_GUI`/`WEB_PORT`。
- **操作流程**：
  1. 新项目执行 `init_project_rules`，写入规范与约束。
  2. 通过 `plan_task`、`analyze_task` 生成任务树，必要时使用 `split_tasks` 自动拆解。
  3. `execute_task`/`continuous mode` 驱动执行，结束后调用 `verify_task`、`reflect_task` 复盘。
  4. 使用 `list_tasks`、`query_task` 检查进度，`get_task_detail` 查看历史。
- **数据安全**：`DATA_DIR` 可能包含中间产物，请纳入 `.gitignore`；删除任务前使用 `clear_all_tasks` 自动备份。
- **记录要求**：在 `mcp-log.md` 记下创建/完成的任务标识、推理摘要与剩余问题，便于接班。

### 4. DeepWiki（仓库知识检索）
- **适用场景**：快速了解公共或授权仓库的结构、文档与实现要点，辅助代码审阅或调研。
- **配置方式**：
  - 公共仓库使用 `"url": "https://mcp.deepwiki.com/sse"`；
  - 私有仓库改用 `https://mcp.devin.ai/sse` 并在 `headers` 中携带 `Authorization: Bearer <API_KEY>`；
  - 需要 Streamable HTTP 时可调用 `https://mcp.deepwiki.com/mcp`。
- **核心工具**：
  - `read_wiki_structure`：获取目录与主题列表，用于定位关注模块。
  - `read_wiki_contents`：读取指定页面的文档内容。
  - `ask_question`：针对仓库提出自然语言问题，返回上下文答案与引用。
- **使用要点**：
  - 首次查询前确认仓库是否已被 DeepWiki 收录；若未收录，需回退到本地阅读或其他文档源。
  - 问答结果用于参考，不可直接视为事实；必要时再结合源码验证。
- 请在日志中注明仓库地址、工具、关键结论与未解决问题。

### 5. Desktop Commander（终端与文件系统增强）
- **适用场景**：需要在本机执行终端命令、长任务或复杂文件操作，并获取实时输出。
- **安装建议**：`npx @wonderwhy-er/desktop-commander@latest setup`（支持自动更新）；可通过 `--debug` 开启调试模式，`remove` 命令卸载。
- **能力范围**：
  - 终端执行：支持输出流式返回、后台运行、超时设置。
  - 进程/会话管理：`list_processes`、`kill_process`、`list_sessions`、`interact_with_process` 等。
  - 文件与搜索：继承 filesystem 能力，同时提供 ripgrep 搜索与批量替换。
  - 数据分析：可直接请求运行 Python/Node/R 脚本，对本地 CSV/JSON 做即时分析。
  - 配置/反馈：`get_usage_stats`、`give_feedback_to_desktop_commander` 等辅助工具。
- **安全控制**：
  - 默认具有写权限与命令执行能力，务必在日志中描述命令目标、预期与风险。
  - 若需访问仓库外目录，应先得到授权并更新允许目录/环境变量。
- 运行可能改变系统状态的脚本时需提供回滚方案或额外确认。

## 记录与复盘要求
- 所有 MCP 调用均需在 `record/mcp-log.md` 留痕，包含：时间、服务、触发原因、主要参数、结果摘要、后续动作/风险。
- 任务结束前，对照本文件逐项核对：是否存在未关闭的远程会话、临时目录或待清理数据。
- 若新增 MCP 服务或调整现有规则，应同步修改本文件并在提交信息中注明“更新 MCP 规范”。
