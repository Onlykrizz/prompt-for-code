# 规范守则 - Web与微服务

## 项目类型
- REST/GraphQL API、事件驱动服务、Serverless 函数、流式处理网关
- 主流技术栈：Spring Boot / Spring Cloud、Quarkus、Micronaut、Jakarta EE、Helidon

## 架构与扩展性
- 遵循 [Twelve-Factor App](https://12factor.net/) 原则构建无状态服务，配置与密钥全部外置。
- 分层或六边形架构：Controller/Router → Service → Domain → Repository，禁止业务逻辑留在注解或拦截器中。
- 使用API契约（OpenAPI、AsyncAPI）驱动接口设计，配合 [SpringDoc](https://springdoc.org/) 或 [MicroProfile OpenAPI](https://openliberty.io/docs/latest/openapi.html)。
- 在多模块/多服务场景下，通过Gradle/Maven BOM管理版本，避免“Jar Hell”。

## 可靠性与可观测性
- 接入 [OpenTelemetry Java](https://opentelemetry.io/docs/languages/java/) 自动化采集trace/metrics/log，统一推送至观察平台。
- 对外暴露健康检查 (`/actuator/health`)、就绪检查 (`/readyz`)、指标端点 (`/actuator/prometheus`)。
- 使用 [Resilience4j](https://resilience4j.readme.io/) / Spring Cloud CircuitBreaker 实现超时、重试、限流、熔断。
- 安全基线：启用TLS、HSTS、CORS白名单；认证建议采用OAuth 2.1 + OpenID Connect，委托给Identity Provider。

## 数据与配置管理
- 数据迁移工具：Flyway/Liquibase，并在CI执行`-check`模式防止遗漏。
- 缓存分层：Caffeine本地缓存 + Redis/Memcached分布式缓存，设计TTL与失效策略。
- 秘钥管理：接入Vault、AWS Secrets Manager或KMS，不在配置文件写明密钥。

## 项目骨架示例（Spring Boot）
```
service/
├── build.gradle.kts
├── src/main/java/
│   ├── com/example/app/Application.java
│   ├── interfaces/http/ApiController.java
│   ├── application/OrderService.java
│   ├── domain/model/Order.java
│   ├── infrastructure/persistence/OrderRepository.java
│   └── infrastructure/config/ObservabilityConfig.java
├── src/main/resources/
│   ├── application.yml
│   └── logback-spring.xml
├── src/test/java/
│   ├── interfaces/http/ApiControllerTest.java
│   ├── application/OrderServiceTest.java
│   └── infrastructure/persistence/OrderRepositoryIT.java
└── docker/
    ├── Dockerfile
    └── docker-compose.yml
```

## 测试与交付
- 单元测试：JUnit 5 + Mockito + AssertJ；对Web层使用 `@WebMvcTest` / `RestAssured`。
- 合约测试：Spring Cloud Contract、Pact，确保上下游兼容。
- 性能测试：`k6` / `Gatling`，建立P95、P99指标，结合Spring Boot Actuator观察。
- 安全测试：OWASP ZAP、Dependency-Check、Snyk；确保依赖更新策略（Renovate、Dependabot）。
- 部署：多阶段Dockerfile、运行时只读文件系统；Kubernetes/Knative 上启用滚动升级与金丝雀策略。

## 运维与SRE
- SLO示例：`P95 < 200ms`、`错误率 < 0.5%`、`可用性 99.9%`。违反阈值时触发熔断或流量降级。
- 配置管控：使用 [Spring Cloud Config](https://spring.io/projects/spring-cloud-config) 或 GitOps pipeline 管理配置漂移。
- 引入 [Spring Boot Production Checklist](https://github.com/arsy786/springboot-best-practices) 与 [Bootiful Spring Boot 2024](https://spring.io/blog/2024/03/11/bootiful-spring-boot-in-2024-part-1) 提供的生产级清单。

## 参考资料
- [Spring Boot Production Best Practices](https://medium.com/@behboodiaref/14-critical-spring-boot-best-practices-for-production-ready-applications-750069403991)
- [Bootiful Spring Boot in 2024](https://spring.io/blog/2024/03/11/bootiful-spring-boot-in-2024-part-1)
- [Microservices on AWS 白皮书](https://docs.aws.amazon.com/whitepapers/latest/microservices-on-aws/microservices-on-aws.html)
- [OpenTelemetry Java](https://opentelemetry.io/docs/languages/java/)
- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
- [Alibaba Java 开发手册（终极版）](https://developer.aliyun.com/ebook/386)
