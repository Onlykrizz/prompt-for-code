# 规范守则 - SSR与边缘渲染

## 项目类型
- Next.js 14+/App Router、Remix、Astro等支持SSR/SSG/ISR的React方案，涵盖边缘计算部署（Vercel Edge、Cloudflare Workers）。

## 核心原则
### 1. 路由与数据获取
- 使用 Next.js App Router 的 `layout.tsx`/`page.tsx` 分层，利用 `generateMetadata` 统一SEO；数据获取使用 `fetch` + Cache Options（`revalidate`、`cache: 'no-store'`）。
- Remix 采用 Loader/Action，保持Server/Client边界清晰。
- Edge函数中处理敏感操作时注意限制长耗时和文件访问。

### 2. TypeScript 与环境变量
- 在 `next-env.d.ts` 与 `env.mjs` 定义类型安全的环境变量；使用 `zod`/`envsafe` 验证。
- 对 API 响应使用 `zod` 或 `io-ts` 解构，保证服务端与客户端一致。

### 3. 构建与部署
- 遵循 [Next.js Production Checklist](https://nextjs.org/docs/14/app/building-your-application/deploying/production-checklist)，启用 `next lint`、`next build`、`next test`。
- 将 CDN/Edge 缓存策略作为配置的一部分（`headers()`、`cookies()`）。
- SSR 场景下监控 TTFB、FCP、LCP 指标，并在Edge平台设置告警。

## 项目结构示例（Next.js App Router）
```
next-app/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── dashboard/
│   └── api/
├── src/
│   ├── components/
│   ├── lib/
│   ├── server/
│   └── types/
├── public/
├── next.config.mjs
└── tsconfig.json
```

## 测试与质量
- 单元测试：Vitest/Jest；对Server Actions使用 `@testing-library/react` + node环境模拟。
- 端到端测试：Playwright/Cypress，覆盖SSR渲染与Edge功能。
- 性能测试：使用 `lighthouse-ci`、`next build --profile` 获取bundle分析；对Edge部署进行负载测试。

## 参考资料
- [Next.js Production Checklist](https://nextjs.org/docs/14/app/building-your-application/deploying/production-checklist)
- [Next.js 14 Release Notes](https://nextjs.org/blog/next-14)
- [Using Next.js with TypeScript: Best Practices](https://emirbalic.com/using-next-js-with-typescript-best-practices-for-2024/)
- [Remix Docs](https://remix.run/docs/en/main)
