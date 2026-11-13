# GitHub 今日 AI Trending 测开分析（2026-11-13）

## AI 架构与趋势

### 今日结构分布（粗分类）
- AI Agent / 编排框架: 6 个

### 热门项目速览

#### 1. GoogleChrome/modern-web-guidance-src
- 链接：https://github.com/GoogleChrome/modern-web-guidance-src
- 归类：AI Agent / 编排框架
- Stars：3555
- 主要语言：TypeScript
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Keep your coding agent up to date with the latest web best practices
  - **Modern Browser APIs**: Helping models correctly structure APIs they frequently misuse.
  - **Performance & Accessibility**: Preferring platform-level APIs that can be optimized by the browser and include built-in accessibility affordances.
  - **Responsible Fallbacks**: Guiding models to use sensible, lightweight fallbacks instead of heavy polyfills or legacy libraries.

#### 2. openai/codex-security
- 链接：https://github.com/openai/codex-security
- 归类：AI Agent / 编排框架
- Stars：12633
- 主要语言：TypeScript
- Topics：ai-security, application-security, cli, code-scanning, codex, codex-security, cybersecurity, devsecops, nodejs, npm, openai, sdk
- 项目特色（基于 description/README 片段的轻量提炼）：
  - OpenAI's Codex Security CLI and TypeScript SDK for finding, validating, and fixing security vulnerabilities. npm: https://www.npmjs.com/package/@openai/codex-security
  - **In Codex:** choose a security workflow.
  - **In a terminal:** install the CLI and scan your repository.
  - **In automation:** use the TypeScript SDK or
  - Scan repositories, selected paths, or Git changes. Deep scans repeat Standard scans and return their deduplicated findings.
  - Validate candidate findings, generate patches, and verify existing fixes.

#### 3. QwenLM/qwen-code
- 链接：https://github.com/QwenLM/qwen-code
- 归类：AI Agent / 编排框架
- Stars：29968
- 主要语言：TypeScript
- Topics：agentic, ai, ai-agent, ai-coding, cli, coding-agent, developer-tools, llm, mcp, qwen, terminal, typescript
- 项目特色（基于 description/README 片段的轻量提炼）：
  - An open-source AI coding agent that lives in your terminal.
  - **Agentic out of the box** — Auto-Memory, Auto-Skills, SubAgents, Agent Teams, and MCP. Dynamic workflows, zero setup.
  - **Open-source, inside and out** — The framework and the Qwen models are open-source. They evolve together. No vendor lock-in.
  - **Multi-protocol** — Supports OpenAI, Anthropic, Gemini, and Qwen APIs. Any third-party provider or local model (Ollama / vLLM). Switch at runtime.
  - **Beyond the terminal** — IDE plugins, Desktop app, Web UI, SDKs, and chat integrations (Telegram / DingTalk / WeChat / Feishu).

#### 4. ashhart/TensorFold
- 链接：https://github.com/ashhart/TensorFold
- 归类：AI Agent / 编排框架
- Stars：2009
- 主要语言：Zig
- Topics：ai, ai-tools, llm, llm-inference, llm-tools
- 项目特色（基于 description/README 片段的轻量提炼）：
  - LLM Inference Engine for Metal, CUDA and Vulkan.

#### 5. addyosmani/agent-skills
- 链接：https://github.com/addyosmani/agent-skills
- 归类：AI Agent / 编排框架
- Stars：116831
- 主要语言：JavaScript
- Topics：agent-skills, antigravity, claude-code, codex, cursor, skills
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Production-grade engineering skills for AI coding agents.

#### 6. meta/astryx
- 链接：https://github.com/meta/astryx
- 归类：AI Agent / 编排框架
- Stars：26853
- 主要语言：TypeScript
- 项目特色（基于 description/README 片段的轻量提炼）：
  - An open source design system that's fully customizable and agent ready
  - **Open internals.** Components are built to be composed at any level, not locked behind a closed top-level API. The building blocks you'd reach for are exported directly, and when you need to go deeper, swizzle ejects a component's full source into your project to own.
  - **No styling lock-in.** Astryx authors its styles with StyleX, but that's invisible to consumers. Override with `className` using Tailwind, CSS modules, or plain CSS — whatever your project already uses.
  - **Customize without wrapping.** A theme is a set of CSS custom property overrides, so a designer can make Astryx unmistakably theirs without forking or wrapping component source.
  - **Built for people and agents.** The API, docs, and CLI are designed together so a person and an AI assistant build the same way, from the same reference.
  - **Guidance over enforcement.** Components give you capability rather than guardra

## 对日常 QA 工作的工程化启发（如何测试此类架构）

### 1) 面向 AI Agent 产品质量的通用原则

- 把 LLM 当作不可控依赖：测试要尽可能确定性（Mock/回放/固定评测集），线上靠观测性兜底。
- 优先把输出结构化：JSON Schema / 受控枚举 / error code，让断言从‘主观’变成‘可自动化判定’。
- 关键路径必须可回放：对话、工具调用、检索命中、模型版本，都要可复现。

### 2) 按架构类型给测试策略（可直接套用）

#### AI Agent / 编排框架
- 将“正确性”拆成：接口契约正确 + 业务规则正确 + 模型/提示词行为可控 + 观测性可追溯。
- 默认把 LLM 视为“不确定的外部依赖”，用 Mock/录制回放/固定种子/评测集来把测试变成确定性。
- 把可测性当作架构能力：强制结构化输出（JSON Schema）、明确错误码、全链路 trace_id。
- 重点测：工具调用（tool/function calling）分支覆盖、状态机/工作流回滚、长链路超时与重试策略。
- 用 Golang Ginkgo 做后端校验：对每个工具 API 做 contract test + 幂等性测试 + 权限边界测试。
- 把关键对话流固化成“场景回放测试”：同一输入在固定依赖下输出必须稳定（snapshot / golden）。

### 3) Golang Ginkgo 后端校验：最小可用模板

以下片段用于说明思路（按你们的框架/路由替换即可）：

```go
package api_test

import (
  "net/http"
  "github.com/onsi/ginkgo/v2"
  "github.com/onsi/gomega"
)

var _ = ginkgo.Describe("Tool API Contract", func() {
  ginkgo.It("should return stable JSON schema for success", func() {
    resp, err := http.Get("http://localhost:8080/api/tool/foo?x=1")
    gomega.Expect(err).ToNot(gomega.HaveOccurred())
    gomega.Expect(resp.StatusCode).To(gomega.Equal(http.StatusOK))
    // TODO: 读取 body 做 JSON Schema 校验 / 字段断言
  })
})
```

### 4) Playwright 端到端自动化：关键路径回放模板

```ts
import { test, expect } from '@playwright/test';

test('chat streaming should be stable', async ({ page }) => {
  await page.goto('https://your-console.example.com');
  // TODO: 登录

  await page.getByRole('textbox', { name: '输入' }).fill('解释一下这个项目的核心能力');
  await page.getByRole('button', { name: '发送' }).click();

  // 关键：对流式输出做“最终一致性”断言
  await expect(page.getByTestId('assistant-message').last()).toContainText('核心');
});
```

## 可落地的行动指南（如何在现有自动化框架中应用）

1. 在现有自动化仓库中新建 `ai_agent_quality/` 目录，沉淀：评测集、对话回放用例、golden snapshots。
2. 为后端（Golang）增加 Ginkgo 套件：
  - Contract tests（OpenAPI/JSON Schema）
  - 工具 API 幂等性 + 权限边界
  - 关键业务规则的 table-driven tests
3. 为前端/控制台增加 Playwright 套件：
  - 关键路径回放（含流式输出断言）
  - 断网/慢网/重试场景
  - 可访问性（a11y）与错误提示一致性
4. 把 LLM 依赖抽象为 Provider 接口：测试环境默认 Mock（录制回放），必要时才走真实模型。
5. 建立‘变更影响面’机制：prompt/模型/检索策略/工具列表任一变化，都要触发评测回归 + 差分报告。

---
### 附：生成数据说明
- 数据源：GitHub Trending +（优先）GitHub REST API；API 受限时自动降级为抓取 GitHub Repo HTML 页面
- 说明：AI 过滤与分类为规则驱动，可按团队需求持续迭代；如需更智能的总结，可在此报告基础上再做人工/LLM 精炼。
