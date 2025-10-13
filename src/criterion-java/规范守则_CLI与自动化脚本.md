# 规范守则 - CLI与自动化脚本

## 项目类型
- DevOps/平台运维脚本、构建工具、批处理任务、数据迁移工具
- 交付形态：单命令可执行Jar、JBang脚本、容器化任务、CI管道步骤

## 核心原则
### 1. 用户体验与可发现性
- 使用 [Picocli](https://picocli.info/) 或 [JBang](https://www.jbang.dev/) 提供一致的参数解析、彩色帮助与自动补全。
- 支持`--help`、`--version`、`--json`等标准开关；错误信息指向解决方案。
- 对长任务提供进度反馈（`System.Logger`、`jansi`、`progressbar`）。

### 2. 配置与可移植性
- 配置优先顺序：命令行参数 > 环境变量 > 配置文件（YAML/Properties）。
- 遵循[XDG Base Directory](https://specifications.freedesktop.org/basedir-spec/latest/)或平台约定存放缓存/日志。
- 构建可重复运行的发行包：使用Maven/Gradle定义`application`插件或Shadow Jar。

### 3. 安全与可审计
- 危险操作默认启用`--dry-run`或二次确认。
- 将关键操作写入审计日志（字段：命令、参数摘要、用户、时间、结果码）。
- 使用`spotbugs`、`OWASP Dependency-Check`定期扫描依赖风险。

## 项目骨架建议
```
cli-tool/
├── build.gradle.kts / pom.xml
├── src/main/java/
│   ├── cli/Application.java      # picocli入口
│   ├── cli/commands/             # 子命令
│   └── support/ConfigLoader.java
├── src/main/resources/
├── src/test/java/
│   ├── cli/commands/ApplicationTest.java
│   └── fixtures/
└── scripts/
    └── release.sh
```

### 示例入口
```java
@Command(name = "datatool", mixinStandardHelpOptions = true)
public class DataTool implements Runnable {
    @Option(names = "--config", description = "配置文件路径", required = true)
    private Path configPath;

    @Option(names = "--dry-run", description = "执行前预览")
    private boolean dryRun;

    @Override
    public void run() {
        Config config = ConfigLoader.load(configPath);
        new JobRunner(config).execute(dryRun);
    }

    public static void main(String[] args) {
        int exitCode = new CommandLine(new DataTool())
                .setExecutionExceptionHandler(new AdviceHandler())
                .execute(args);
        System.exit(exitCode);
    }
}
```

## 测试与交付策略
- 使用 `picocli.CommandLine` 的 `ParseResult`、`IT` 测试 + [System Lambda](https://stefanbirkner.github.io/system-lambda/) 验证输出。
- 在CI中构建多平台可执行物（`jlink`/`native-image`）并执行烟雾测试。
- 提供 Dockerfile 或 JBang.catalog 以便快捷分发；发布前执行 `mvn verify`、`gradle check`。
- 记录版本信息（`git commit`+ `git describe`）并嵌入 `--version` 输出。

## 运行与运维
- 结构化日志：使用 `java.util.logging` bridge或 `Logback` JSON encoder 输出机器可读日志。
- 针对计划任务加入幂等设计、重试与超时配置。
- 在CI/CD（GitHub Actions、Jenkins）中构建自动回滚策略，失败时输出诊断包。

## 参考资料
- [Picocli 官方文档](https://picocli.info/) – 命令行参数解析与帮助生成。
- [Baeldung: Creating CLI with Picocli](https://www.baeldung.com/java-picocli-create-command-line-program) – CLI实现最佳实践示例。
- [JBang 文档](https://www.jbang.dev/documentation) – 以脚本形式分发Java自动化工具。
- [Effective Java](https://www.javaguides.net/2025/02/effective-java-15-best-practices.html) – Joshua Bloch 对资源管理、并发与API设计的建议。
- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) – 统一编码风格与格式化规范。
