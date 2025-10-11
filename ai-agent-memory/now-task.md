# 现在的任务

用户想在general目录下的现有指令体系中添加一些内容，请你分析内容后生成可实现用户目标的指令并将其添加到general下正确的文档位置中：

1.对于mcp-log.md、AI-AGENT_working-status.csv、undetermined.md、optimized-task.md这些文档，重新设计存储文件路径

在项目初始化时，创建`record/YYYY-MM-DDTHH-MM-SS_UTC_任务简述`目录，把这些文档都保存在这个目录下，例如`record/2025-10-11T19-01-14_UTC+8_新增MCP指引文档/optimized-task.md`，简述一般控制在8~20个字，

后续本次任务中，项目本身的文档（比如代码文件，配置文件，他们都有确定的正确路径）之外的信息（比如即时从网络搜索到的额外信息，文档，拓展材料等），需要存储的话，就存在这个新建的目录，例如之前新增MCP指引文档时从网上搜到的信息就存到了`record/2025-10-11T19-01-14_UTC+8_新增MCP指引文档/mcp-research-notes.md`

清理阶段不需要再清理mcp-log.md、AI-AGENT_working-status.csv、undetermined.md、optimized-task.md，现在它们已经不影响目录整洁，

2.每次git提交之前都要追踪所有未追踪文件，比如`git add .`，只要没有被`.gitignore`忽略的，都将被跟踪进git仓库管理

3.在任务的文档更新环节里，更新working-status之后，创建git提交之前，维护好CHANGELOG.md然后才能提交