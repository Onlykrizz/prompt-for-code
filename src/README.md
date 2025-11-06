# README

本目录用于集中维护AI代理执行任务所需的基础文档和模板。复用方式如下：

1. **初始化项目规范**
   - 将`Agents.md`复制到目标项目根目录。
   - 将`ai-agent-memo-4`复制到目标项目根目录下并重命名为`ai-agent-memory`。
   - 将`criterion-*`系列目录复制到目标项目的`ai-agent-memory`目录下。
   - 完成这一步后的，若目标项目路径为`/path/to/project/`，则其下至少应该有下列文件，
  /path/to/project/
  ├── Agents.md
  └── ai-agent-memory
      ├── AI-AGENT_check.md
      ├── AI-AGENT_general.md
      ├── ……（其他AI-AGENT_*.md文档）
      ├── criterion-python
      ├── ……（其他criterion-*目录）
      └── criterion-rust

2. **任务执行前准备**
   - 在复制完成后，项目中的`Agents.md`会提醒代理优先阅读`ai-agent-memory/`内的指引。
   - `AI-AGENT_criterion.md`整合任务六环节流程、MCP调用基准与执行自检表。
   - `AI-AGENT_step-before.md`提供任务前置准备的顺序清单。
   - `now-task.md`是“任务描述 + 必填检查表”模板，执行完毕需恢复为原始状态。
   - `undetermined-template.md`规范待定项的记录方式。

3. **工作状态记录**
   - 按`AI-AGENT_criterion.md`中的规范，新建`AI-AGENT_working-status.csv`并维护环节记录。
   - 将`AI-AGENT_working-status.csv`、`undetermined.md`、`optimized-task.md`等辅助文档统一存放至`ai-agent-output/YYYY-MM-DDTHH-MM-SS_UTC+8_任务简述/`目录，保持任务简述8-20字。
   - 提交前务必执行`git add .`以追踪全部未忽略文件，并在更新工作状态后优先维护`CHANGELOG.md`与版本号（生成新版本段落、写入日期、重建空的`[Unreleased]`）再进行提交。
   - 请确保每次复制后指引内容保持最新，若有新约定需回写到本目录。

4. **规范守则目录**
   - `criterion-rust/`：覆盖Rust CLI、Web、库、跨平台、高性能五类项目的规范守则。
   - `criterion-python/`：覆盖Python CLI、Web、数据科学、企业平台、高性能/分布式方向的规范守则。
   - `criterion-java/`：覆盖Java CLI、Web与微服务、企业平台、数据工程、高性能/分布式五类守则，并罗列权威资料链接。
   - `criterion-flutter/`：覆盖Flutter移动、桌面/Web、插件、企业可观测性、高性能动画等方向的守则。
   - `criterion-react/`：覆盖React(TypeScript) SPA、SSR/边缘渲染、设计系统、状态管理、性能质量等方向的守则。
   - `criterion-flutter-rust/`：针对Flutter与Rust协同的多方案守则与项目指导。
   - `criterion-react-rust/`：针对React(TypeScript)与Rust协同的多方案守则与项目指导。
5. **复制与阅读策略**
   - 初始化项目后，`src/`中除`Agents.md`外的文件会同步到`ai-agent-memory/`，作为常驻指令。
   - 默认仅需查阅`ai-agent-memory/`下除`criterion-*`系列目录之外的文档；遇到特定语言/框架/协同需求时，再按需阅读对应的`criterion-*`守则。

> 提示：若需要额外的运行脚本或配置片段，请在目标项目中自行维护，避免污染模板目录。
