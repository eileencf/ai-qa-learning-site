# GitHub 今日 AI Trending 测开分析（2026-11-16）

## AI 架构与趋势

### 今日结构分布（粗分类）
- AI Agent / 编排框架: 6 个

### 热门项目速览

#### 1. dream-num/univer
- 链接：https://github.com/dream-num/univer
- 归类：AI Agent / 编排框架
- Stars：26545
- 主要语言：TypeScript
- Topics：board, collaboration, doc, docx, excel, offce365, office, pdf, ppt, pptx, presentation, sdk
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Build your own AI office with Univer Office SDK. Bring editing, calculation, collaboration, and file processing into your product for people and AI agents. Built on an extensible open-source core.
  - 💡 What is Univer?
  - Open-source capabilities
  - 🚀 Build on the open-source foundation
  - Quick start: an open-source spreadsheet editor
  - Connect your application to editable content

#### 2. ag-ui-protocol/ag-ui
- 链接：https://github.com/ag-ui-protocol/ag-ui
- 归类：AI Agent / 编排框架
- Stars：18121
- 主要语言：TypeScript
- Topics：ag-ui-protocol, agent-frontend, agent-ui, agentic-workflow, ai-agents
- 项目特色（基于 description/README 片段的轻量提炼）：
  - AG-UI: the Agent-User Interaction Protocol. Bring Agents into Frontend Applications.
  - The AG-UI Dojo（https://dojo.ag-ui.com/）
  - Build AG-UI-powered applications(Quickstart)（https://docs.ag-ui.com/quickstart/applications）
  - Build new AG-UI framework integrations (Quickstart)（https://go.copilotkit.ai/agui-contribute）
  - Book a call to discuss an AG-UI integration with a new framework（https://calendly.com/markus-copilotkit/ag-ui）
  - Join the Discord Community（https://discord.gg/Jd3FzfdJa8）

#### 3. google-labs-code/stitch-skills
- 链接：https://github.com/google-labs-code/stitch-skills
- 归类：AI Agent / 编排框架
- Stars：9447
- 主要语言：TypeScript
- 项目特色（基于 description/README 片段的轻量提炼）：
  - A library of Agent Skills designed to work with the Stitch MCP server. Each skill follows the Agent Skills open standard, for compatibility with coding agents such as Antigravity, Gemini CLI, Claude Code, Cursor.
  - **`stitch-design`** — design-focused skills
  - **`stitch-build`** — build and component skills
  - **`stitch-utilities`** — utility and helper skills

#### 4. backnotprop/plannotator
- 链接：https://github.com/backnotprop/plannotator
- 归类：AI Agent / 编排框架
- Stars：12030
- 主要语言：TypeScript
- Topics：agents, claude-code, code-review, codex, obsidian, opencode, pi-mono, plan-mode, skills
- 项目特色（基于 description/README 片段的轻量提炼）：
  - The workspace to stay in the loop and on top of agents - shape, decide, plan, annotate, review code, share with team, and send all feedback to agents with one click.

#### 5. ChromeDevTools/chrome-devtools-mcp
- 链接：https://github.com/ChromeDevTools/chrome-devtools-mcp
- 归类：AI Agent / 编排框架
- Stars：57182
- 主要语言：TypeScript
- Topics：browser, chrome, chrome-devtools, debugging, devtools, mcp, mcp-server, puppeteer
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Chrome DevTools for coding agents
  - **Get performance insights**: Uses [Chrome
  - **Advanced browser debugging**: Analyze network requests, take screenshots and
  - **Reliable automation**. Uses
  - Node.js（https://nodejs.org/） LTS（https://github.com/nodejs/Release#release-schedule） version.
  - Chrome（https://www.google.com/chrome/） current stable version or newer.

#### 6. alibaba/open-code-review
- 链接：https://github.com/alibaba/open-code-review
- 归类：AI Agent / 编排框架
- Stars：52355
- 主要语言：Go
- Topics：agent, agent-skills, code-review, code-review-assistant, harness, repository-level-context
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Secure, fast, efficient, battle-tested at Alibaba's scale. Hybrid architecture code review tool: deterministic pipelines + LLM Agent, precise line-level comments, built-in multi-language ruleset (NPE, thread-safety, XSS, SQL injection), OpenAI & Anthropic compatible.
  - **Incomplete coverage** — On larger changesets, agents tend to "cut corners," selectively reviewing only some files and missing others.
  - **Position drift** —

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
