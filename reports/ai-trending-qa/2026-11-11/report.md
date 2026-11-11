# GitHub 今日 AI Trending 测开分析（2026-11-11）

## AI 架构与趋势

### 今日结构分布（粗分类）
- AI Agent / 编排框架: 6 个

### 热门项目速览

#### 1. meta/astryx
- 链接：https://github.com/meta/astryx
- 归类：AI Agent / 编排框架
- Stars：23487
- 主要语言：TypeScript
- 项目特色（基于 description/README 片段的轻量提炼）：
  - An open source design system that's fully customizable and agent ready
  - **Open internals.** Components are built to be composed at any level, not locked behind a closed top-level API. The building blocks you'd reach for are exported directly, and when you need to go deeper, swizzle ejects a component's full source into your project to own.
  - **No styling lock-in.** Astryx authors its styles with StyleX, but that's invisible to consumers. Override with `className` using Tailwind, CSS modules, or plain CSS — whatever your project already uses.
  - **Customize without wrapping.** A theme is a set of CSS custom property overrides, so a designer can make Astryx unmistakably theirs without forking or wrapping component source.
  - **Built for people and agents.** The API, docs, and CLI are designed together so a person and an AI assistant build the same way, from the same reference.
  - **Guidance over enforcement.** Components give you capability rather than guardra

#### 2. anthropics/skills
- 链接：https://github.com/anthropics/skills
- 归类：AI Agent / 编排框架
- Stars：192558
- 主要语言：Python
- Topics：agent-skills
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Public repository for Agent Skills
  - What are skills?（https://support.claude.com/en/articles/12512176-what-are-skills）
  - Using skills in Claude（https://support.claude.com/en/articles/12512180-using-skills-in-claude）
  - How to create custom skills（https://support.claude.com/en/articles/12512198-creating-custom-skills）
  - Equipping agents for the real world with Agent Skills（https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills）
  - ./skills: Skill examples for Creative & Design, Development & Technical, Enterprise & Communication, and Document Skills

#### 3. addyosmani/agent-skills
- 链接：https://github.com/addyosmani/agent-skills
- 归类：AI Agent / 编排框架
- Stars：115328
- 主要语言：JavaScript
- Topics：agent-skills, antigravity, claude-code, codex, cursor, skills
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Production-grade engineering skills for AI coding agents.

#### 4. homeassistant-ai/ha-mcp
- 链接：https://github.com/homeassistant-ai/ha-mcp
- 归类：AI Agent / 编排框架
- Stars：6800
- 主要语言：Python
- Topics：ai, claude, hacs, home-assistant, home-automation, llm, mcp, model-context-protocol
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Configure and automate Home Assistant with Claude, ChatGPT, and other AI assistants.
  - Install the **HA-MCP integration** (requires **Home Assistant 2026.8.0 or newer**; see compatibility details). On **Home Assistant 2026.8–2026.10**, open HACS, search for **HA-MCP**, then **Download**.
  - **Restart Home Assistant.**
  - Decide which administrator account the server acts as. Either create a long-lived access token on your own account (your profile → **Security** → **Long-lived access tokens** → **Create token**; it works from anywhere if it leaks, and the server's changes show under your name), or, safer, create an account just for HA-MCP under **Settings → People → Add person** with **Allow login**, **Local access only** and **Administrator** on. Never use your own login for the second option.
  - Go to **Settings → Devices & Services → Add Integration**, search for **HA-MCP** and choose **HA-MCP Server**. Paste your token, or enter the user name and password of the account you made for HA-MCP (HA-MCP creates its token), pick how clients may connect — **Remote access through Home Assistant** (start with **Secret URL**, the simplest; **Home Assistant sign-in** adds a login) and/or **Network access: Local network** — then click **Submit**. Both start disabled, so a client on another device needs one of them.
  - Copy the connect URL from the entry's **Configure** screen (**Settings → Devices & Services → “HA-MCP — Manage Home Assistant with AI” → HA-MCP Server → Configure**). A notification confirms the server started and points you there.

#### 5. vercel-labs/agent-browser
- 链接：https://github.com/vercel-labs/agent-browser
- 归类：AI Agent / 编排框架
- Stars：49406
- 主要语言：Rust
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Browser automation CLI for AI agents
  - **Homebrew:** `brew install agent-browser`, then `agent-browser install`.
  - **Linux:** `agent-browser install --with-deps` also installs the browser's system libraries.
  - **No install:** `npx agent-browser open example.com`.
  - link "Learn more" [ref=e1]
  - Refs describe the page at the time of the snapshot. After navigation or a DOM change, take a new snapshot before using refs again.

#### 6. sherlock-project/sherlock
- 链接：https://github.com/sherlock-project/sherlock
- 归类：AI Agent / 编排框架
- Stars：109340
- 主要语言：Python
- Topics：cli, cti, cybersecurity, forensics, hacktoberfest, information-gathering, infosec, linux, osint, pentesting, python, python3
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Hunt down social media accounts by username across social networks

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
