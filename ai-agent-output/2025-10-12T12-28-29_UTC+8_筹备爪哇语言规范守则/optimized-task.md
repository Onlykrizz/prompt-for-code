# 优化后任务说明

## 背景
- 用户要求在general目录下新增Java规范守则体系，并与既有Rust/Python守则保持结构一致。
- 命名方案：`general/criterion-java/`目录内统一使用“规范守则_*”文件名。
- 已规划五大方向：CLI与自动化脚本、Web与微服务、企业级平台与服务、数据工程与大数据、高性能与分布式计算。
- 需调研Java领域权威资料、框架最佳实践及知名专家或著作，引用来源并收录于文档。

## 目标
1. 建立`general/criterion-java/`目录，编写README与五份方向守则文档。
2. 每份守则包含：项目类型定义、核心原则、项目结构建议、工具/框架推荐、测试与交付策略、运维要点、参考资料。
3. 汇总调研时获取的资料链接，在文档中列出并在`mcp-log.md`做摘要留痕。
4. 更新general/README及CHANGELOG，记录新增Java守则体系。

## 执行步骤
1. **资料调研准备**
   - 汇总Rust目录现有结构，提取可复用的段落骨架。
   - 列出每个方向需要覆盖的核心主题与关键框架（如Spring Boot、Quarkus、Android、Spark、Flink、Netty、JVM调优等）。
2. **调研执行**
   - 使用`mcp-web-search`获取官方文档、知名书籍、企业规约（Effective Java、Google Java Style、Alibaba Java开发手册等）。
   - 每次检索完成后在`mcp-log.md`记录时间、目标与主要收获。
3. **文档撰写**
   - 创建`general/criterion-java/`目录及README，描述用途与目录结构。
   - 按五大方向生成`规范守则_*`文档，填充内容并引用调研链接。
   - 确保与已存在的Rust/Python守则在格式上保持一致，适当调整以匹配Java生态特点。
4. **验证与维护**
   - 使用`rg`确认general目录中命名统一且无旧术语残留。
   - 自查文档链接与章节完整性，确保成功标准达成。
   - 更新`CHANGELOG.md`新增版本条目，重建空的`[Unreleased]`。
   - 在general/README补充Java守则目录说明。
5. **收尾**
   - 维护`AI-AGENT_working-status.csv`至收尾阶段。
   - 清理临时草稿，确认无遗漏提交。

## 成功标准
- `general/criterion-java/`目录生成且包含README与五份规范守则文档，结构一致、内容完整、引用清晰。
- 文档中列出的参考资料均指向权威来源（官方文档、经典书籍、行业最佳实践）。
- general目录索引与CHANGELOG更新到位，无遗漏命名差异。
- 状态记录与日志符合项目要求，未创建`mcp-log.csv`。
