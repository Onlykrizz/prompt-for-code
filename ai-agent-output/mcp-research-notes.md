# MCP 服务调研笔记

## @modelcontextprotocol/server-filesystem
- **定位**：官方文件系统参考服务器，提供受控的读写、目录管理与搜索功能。
- **接入方式**：推荐通过 `npx @modelcontextprotocol/server-filesystem <allowed_dirs>` 启动，或依赖支持 Roots 协议的客户端动态下发允许目录。
- **访问控制**：启动时可通过命令行指定允许访问的根目录；若客户端支持 Roots，则以客户端提供的目录列表覆盖本地配置。
- **关键工具**：
  - `read_text_file`/`read_media_file`/`read_multiple_files`：读取文本或媒体资源。
  - `write_file`、`edit_file`：写入或局部编辑文件，`edit_file` 支持 dryRun 与差异输出。
  - `create_directory`、`list_directory`、`list_directory_with_sizes`：目录管理与容量统计。
  - `get_file_info`、`list_allowed_directories`：查询元数据与安全边界。
- **安全提示**：必须至少配置一个允许目录；`write_file` 会整体覆盖文件，批量修改推荐优先使用 `edit_file`。

## @playwright/mcp@latest
- **定位**：由微软维护的 Playwright MCP 服务器，基于可访问性树实现浏览器自动化，避免截图驱动的高延迟方案。
- **前置要求**：Node.js 18+；典型配置 `npx @playwright/mcp@latest`。可通过 `--caps` 启用额外能力（例如 `vision`、`pdf`、`verify`）。
- **核心能力**：
  - 页面导航与状态校验（`browser_open`、`browser_wait_for`）。
  - 结构化交互：点击、表单填写、下拉选择、鼠标拖拽等操作均需提供 `element` 描述与 Playwright 生成的权限引用。
  - 资源导出：截图、PDF、可选追踪。
  - 标签页与窗口管理、浏览器安装检测等辅助工具。
- **最佳实践**：
  - 首次运行建议调用 `browser_install` 安装所需浏览器内核。
  - 大型 DOM 建议配合 `browser_snapshot` 观测结构后再操作；`vision` 与坐标操作为显式 opt-in。

## mcp-shrimp-task-manager
- **定位**：专为智能体设计的任务管理与分解工具，强调链式思考、反思与开发流程落地。
- **部署**：源码在 GitHub；典型配置 `node dist/index.js`，需要设置持久化目录 `DATA_DIR`，可选 Web GUI（`ENABLE_GUI=true`）。
- **主要特性**：
  - 任务全生命周期：`plan_task`、`execute_task`、`update_task`、`verify_task`、`reflect_task`、`list_tasks` 等工具覆盖规划、执行、验证、复盘。
  - 复杂任务拆解与依赖跟踪：`split_tasks`、`analyze_task`、`query_task`。
  - 持久化记忆：任务、规则、研究结果保存在 `DATA_DIR`，跨会话可恢复。
  - 研究/规则模块：`research_mode`、`init_project_rules` 支撑前期调研与标准化。
- **使用建议**：
  - 新项目优先执行 `init_project_rules`，随后 `plan_task`→`execute_task`→`verify_task` 形成闭环。
  - 大任务可借助 `split_tasks` 自动拆分；`continuous mode` 可批量执行待办。

## mcp-deepwiki@latest
- **定位**：DeepSeek 团队提供的远程 MCP 服务，暴露 DeepWiki 仓库文档与问答检索能力。
- **接入方式**：
  - 公共仓库：`"url": "https://mcp.deepwiki.com/sse"`（SSE 协议）。
  - 私有/授权仓库：使用 `https://mcp.devin.ai/sse` 并在 `headers` 中携带 `Authorization: Bearer <API_KEY>`。
  - 同时提供 `https://mcp.deepwiki.com/mcp`（Streamable HTTP）。
- **可用工具**：
  - `read_wiki_structure`：获取仓库文档主题树。
  - `read_wiki_contents`：按页面读取文档内容。
  - `ask_question`：基于 DeepWiki 上下文的自然语言问答。
- **提示**：推荐优先使用 `/sse` 以获得与官方规范兼容的推流能力；在 Claude Code 中可使用 `claude mcp add -s user -t http ...` 快速注册。

## @wonderwhy-er/desktop-commander
- **定位**：社区热门的本地开发增强 MCP，整合文件系统操作、终端执行、进程管理与数据分析等能力。
- **安装**：`npx @wonderwhy-er/desktop-commander@latest setup`，或通过脚本/Smithery 安装；支持自动更新与调试模式。
- **核心能力**：
  - 终端命令执行与过程控制：支持长时任务、输出流式回传、后台运行、超时管理。
  - 进程/会话管理：`list_processes`、`kill_process`、`list_sessions` 等。
  - 文件系统与代码编辑：复用官方 filesystem 能力，额外提供 ripgrep 搜索、批量替换、上下文 diff。
  - 数据处理：可直接请求执行内存中的 Python/Node/R 代码，对 CSV/JSON 做即时分析。
  - 配置与遥测：`get_usage_stats`、`give_feedback_to_desktop_commander` 等工具；提供本地日志轮换与可选遥测开关。
- **安全注意**：默认具备写权限，需结合客户端沙箱或 `.mcpignore` 控制访问范围；建议明确告知可能的副作用（如覆盖写入、shell 命令执行）。
