# GitHub 今日 AI Trending 测开分析（2026-11-18）

## AI 架构与趋势

### 今日结构分布（粗分类）
- AI Agent / 编排框架: 5 个
- 应用层 / UI: 1 个

### 热门项目速览

#### 1. elementalsouls/Claude-BugHunter
- 链接：https://github.com/elementalsouls/Claude-BugHunter
- 归类：AI Agent / 编排框架
- Stars：9882
- 主要语言：Python
- Topics：ai-security, anthropic, application-security, bug-bounty, bugbounty, bugcrowd, claude, claude-code, claude-skills, ethical-hacking, hackerone, offensive-security
- 项目特色（基于 description/README 片段的轻量提炼）：
  - A Claude Code skill bundle for bug hunting and external red-team work - 82 skills, 15 slash commands, 681 disclosed-report patterns curated across 24 core vulnerability classes, plus enterprise identity + infrastructure attack matrices.
  - **Think** — `bb-methodology` + `redteam-mindset`: the 5-phase non-linear workflow, critical-thinking framework, and red-team operator discipline.
  - **Hunt webapps** — 58 `hunt-*` skills curated from 681 disclosed HackerOne reports: per-class detection patterns, payloads, bypass tables, and chain templates.
  - **Hit the perimeter** — enterprise platform chains (M365/Entra, Okta, vCenter, SSL-VPN appliances, SharePoint, cloud IAM): current 2024–2026 CVE chains + post-credential escalation.
  - **Ship it** — `triage-validation` + reporting + `evidence-hygiene`: the 7-Question Gate, VRT-aware severity, OOS rebuttals, PII redaction, and red-team deliverables.

#### 2. mvanhorn/last30days-skill
- 链接：https://github.com/mvanhorn/last30days-skill
- 归类：AI Agent / 编排框架
- Stars：69373
- 主要语言：Python
- Topics：ai-prompts, ai-skill, bluesky, claude, claude-code, clawhub, deep-research, hackernews, instagram, openclaw, polymarket, recency
- 项目特色（基于 description/README 片段的轻量提炼）：
  - AI agent skill that researches any topic across Reddit, X, YouTube, HN, Polymarket, and the web - then synthesizes a grounded summary

#### 3. alibaba/open-code-review
- 链接：https://github.com/alibaba/open-code-review
- 归类：AI Agent / 编排框架
- Stars：53951
- 主要语言：Go
- Topics：agent, agent-skills, code-review, code-review-assistant, harness, repository-level-context
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Secure, fast, efficient, battle-tested at Alibaba's scale. Hybrid architecture code review tool: deterministic pipelines + LLM Agent, precise line-level comments, built-in multi-language ruleset (NPE, thread-safety, XSS, SQL injection), OpenAI & Anthropic compatible.
  - **Incomplete coverage** — On larger changesets, agents tend to "cut corners," selectively reviewing only some files and missing others.
  - **Position drift** —

#### 4. Tencent/LoopForge
- 链接：https://github.com/Tencent/LoopForge
- 归类：AI Agent / 编排框架
- Stars：3532
- 主要语言：Go
- Topics：agent-orchestration, agentic-workflow, ai-agents, ai-coding, claude-code, code-review, codebuddy, codex, coding-agents, cursor, developer-tools, human-on-the-loop
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Self-hosted workflows for coding-agent delivery. Orchestrate CodeBuddy, Codex and Claude Code with scripts and human approval gates. Includes Local workflows for coding assistants.
  - **Repeatable.** Same SOP, same stages, same checks for every requirement. Start from built-in backend, frontend, bug-fix and product SOPs.
  - **Separated roles.** Planning, implementation, review and testing each get their own prompt, executor, model, rules, Skills and MCP tools. A role works as an SOP node or as a subagent in chat.
  - **Human in the loop.** Approval gates where they matter. Read the report, approve, or send the work back to a chosen step.
  - **Observable and resumable.** Node status, tool traces, logs and artifacts in one place. Pause, retry a failed step, or rerun from any node.
  - **Your stack, your servers.** Ten coding-agent CLIs as executors, from CodeBuddy, Codex and Claude Code to OpenCode, Cursor CLI and more. GitHub, Skills and MCP as tools. Docker sandboxes or your own machine as the runtime.

#### 5. dream-num/univer
- 链接：https://github.com/dream-num/univer
- 归类：AI Agent / 编排框架
- Stars：29445
- 主要语言：TypeScript
- Topics：board, collaboration, doc, docx, excel, offce365, office, pdf, ppt, pptx, presentation, sdk
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Build your own AI office with Univer Office SDK. Bring editing, calculation, collaboration, and file processing into your product for people and AI agents. Built on an extensible open-source core.
  - 💡 What is Univer?
  - Open-source capabilities
  - 🚀 Build on the open-source foundation
  - Quick start: an open-source spreadsheet editor
  - Connect your application to editable content

#### 6. getarcaneapp/arcane
- 链接：https://github.com/getarcaneapp/arcane
- 归类：应用层 / UI
- Stars：9477
- 主要语言：Go
- Topics：compose, container-management, containers, docker, docker-compose, docker-management, go, self-hosted, sveltekit, typescript, web-ui
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Modern Docker Management, Designed for Everyone

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

#### 应用层 / UI
- 将“正确性”拆成：接口契约正确 + 业务规则正确 + 模型/提示词行为可控 + 观测性可追溯。
- 默认把 LLM 视为“不确定的外部依赖”，用 Mock/录制回放/固定种子/评测集来把测试变成确定性。
- 把可测性当作架构能力：强制结构化输出（JSON Schema）、明确错误码、全链路 trace_id。
- 重点测：用户路径与可用性——长对话、断网重连、输入法、文件上传、复制代码块等高频操作。
- 用 Playwright 建立‘关键路径回放’：登录→创建会话→提问→流式输出→引用/工具调用结果展示。
- 把前端埋点当作测试断言的一部分：关键交互必须产生日志/事件，方便线上回溯。

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
