# GitHub 今日 AI Trending 测开分析（2026-11-21）

## AI 架构与趋势

### 今日结构分布（粗分类）
- AI Agent / 编排框架: 5 个
- RAG / 知识库: 1 个

### 热门项目速览

#### 1. elementalsouls/Claude-BugHunter
- 链接：https://github.com/elementalsouls/Claude-BugHunter
- 归类：AI Agent / 编排框架
- Stars：14697
- 主要语言：Python
- Topics：ai-security, anthropic, application-security, bug-bounty, bugbounty, bugcrowd, claude, claude-code, claude-skills, ethical-hacking, hackerone, offensive-security
- 项目特色（基于 description/README 片段的轻量提炼）：
  - A Claude Code skill bundle for bug hunting and external red-team work - 82 skills, 15 slash commands, 681 disclosed-report patterns curated across 24 core vulnerability classes, plus enterprise identity + infrastructure attack matrices.
  - **Think** — `bb-methodology` + `redteam-mindset`: the 5-phase non-linear workflow, critical-thinking framework, and red-team operator discipline.
  - **Hunt webapps** — 58 `hunt-*` skills curated from 681 disclosed HackerOne reports: per-class detection patterns, payloads, bypass tables, and chain templates.
  - **Hit the perimeter** — enterprise platform chains (M365/Entra, Okta, vCenter, SSL-VPN appliances, SharePoint, cloud IAM): current 2024–2026 CVE chains + post-credential escalation.
  - **Ship it** — `triage-validation` + reporting + `evidence-hygiene`: the 7-Question Gate, VRT-aware severity, OOS rebuttals, PII redaction, and red-team deliverables.

#### 2. obra/superpowers
- 链接：https://github.com/obra/superpowers
- 归类：AI Agent / 编排框架
- Stars：322991
- 主要语言：Shell
- Topics：ai, brainstorming, coding, obra, sdlc, skills, subagent-driven-development, superpowers
- 项目特色（基于 description/README 片段的轻量提炼）：
  - An agentic skills framework & software development methodology that works.
  - How it works
  - Commercial Services
  - Getting Started
  - Claude Code
  - Antigravity

#### 3. HKUDS/CLI-Anything
- 链接：https://github.com/HKUDS/CLI-Anything
- 归类：AI Agent / 编排框架
- Stars：61563
- 主要语言：Python
- 项目特色（基于 description/README 片段的轻量提炼）：
  - "CLI-Anything: Making ALL Software Agent-Native" -- CLI-Hub: https://clianything.cc/
  - **2026-05-30** 🧭 **Hermes skill** proposed (#320), adding a CLI-Anything orchestration skill with installer scripts and HARNESS fallback guidance. 🗺️ **ArcGIS Pro** was proposed for the public registry (#318) as a Windows/ArcPy CLI for cartography, geoprocessing, feature editing, and live-Pro MCP workflows.
  - **2026-05-27** 🔧 **CLI-Hub** registry date updates now handle `python -m pip` install commands (#312), improving package-date detection for registry automation.
  - **2026-05-23** 📝 **Obsidian Agent CLI** was proposed for the public registry (#307), bringing a PyPI-installed Obsidian automation CLI with persistent agent memory workflows and a pinned skill link.
  - **2026-05-21** 🔒 **Sketch CLI** token-file handling was hardened against path traversal and symlink escapes (#304).
  - **2026-05-20** 📓 **Joplin CLI** was proposed (#300) with notebooks, notes, to-dos, tags, attachments, search/sync, import/export, server/E2EE helpers, full docs, packaged skill docs, and a 134-test validation baseline.

#### 4. jingyaogong/minimind
- 链接：https://github.com/jingyaogong/minimind
- 归类：AI Agent / 编排框架
- Stars：67820
- 主要语言：Python
- Topics：artificial-intelligence, large-language-model
- 项目特色（基于 description/README 片段的轻量提炼）：
  - 🧠 两小时从 0 训出你的 64M 大模型。Train your own 64M LLM from scratch in 2 hours.
  - 此开源项目旨在完全从 0 开始，仅用 3 块钱成本与 2 小时训练时间，即可训练出规模约为 64M 的超小语言模型 MiniMind。
  - MiniMind 系列极其轻量，主线最小版本体积约为 GPT-3 的 $\frac\{1\}\{2700\}$，力求让普通个人 GPU 也能快速完成训练与复现。
  - 项目同时开源了大模型的极简结构与完整训练链路，覆盖 MoE、数据清洗、预训练（Pretrain）、监督微调（SFT）、LoRA、RLHF（DPO）、RLAIF（PPO / GRPO / CISPO）、Tool Use、Agentic RL、自适应思考与模型蒸馏等全过程代码。
  - MiniMind 同时拓展了视觉模态模型 MiniMind-V（https://github.com/jingyaogong/minimind-v）、多模态 Omni 模型 MiniMind-O（https://github.com/jingyaogong/minimind-o）、扩散语言模型（MiniMind-dLM）、线性模型（MiniMind-Linear），详见 Discussion（https://github.com/jingyaogong/minimind/discussions）。
  - 项目所有核心算法代码均从 0 使用 PyTorch 原生实现，不依赖第三方库提供的高层抽象接口。

#### 5. firecrawl/firecrawl
- 链接：https://github.com/firecrawl/firecrawl
- 归类：AI Agent / 编排框架
- Stars：205509
- 主要语言：TypeScript
- Topics：ai, ai-agents, ai-crawler, ai-scraping, ai-search, crawler, data-extraction, html-to-markdown, llm, markdown, scraper, scraping
- 项目特色（基于 description/README 片段的轻量提炼）：
  - Knowledge infrastructure to make your agents smarter. Search, scrape and access 550+ data providers through one API.
  - **Firecrawl Local.** Run Firecrawl on your own machine as one binary that turns websites into clean markdown, plugs into your AI agent as an MCP server and serves the Firecrawl API on localhost.
  - **Firecrawl Cloud.** Use the hosted service at firecrawl.dev（https://firecrawl.dev/?ref=github） for everything Local does at scale with nothing to run, plus search and the 550+ data providers in Firecrawl Alexandria（https://alexandria.firecrawl.dev） for far more knowledge than scraping alone.
  - **Self-hosting.** Deploy the full Firecrawl server from `apps/api` with its own queues, workers and databases on your own infrastructure.

#### 6. nginx/nginx
- 链接：https://github.com/nginx/nginx
- 归类：RAG / 知识库
- Stars：32618
- 主要语言：C
- Topics：content-cache, http, http2, http3, https, load-balancer, mail-proxy-server, nginx, quic, reverse-proxy, security, tcp-proxy-server
- 项目特色（基于 description/README 片段的轻量提炼）：
  - The official NGINX Open Source repository.
  - How it works
  - Configurations
  - Downloading and installing
  - Stable and Mainline binaries

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

#### RAG / 知识库
- 将“正确性”拆成：接口契约正确 + 业务规则正确 + 模型/提示词行为可控 + 观测性可追溯。
- 默认把 LLM 视为“不确定的外部依赖”，用 Mock/录制回放/固定种子/评测集来把测试变成确定性。
- 把可测性当作架构能力：强制结构化输出（JSON Schema）、明确错误码、全链路 trace_id。
- 重点测：检索召回（Recall）与排序（Rank）——为每条问题准备‘期望命中文档集合’，做离线评测回归。
- 把向量库当数据库测：索引构建一致性、增量写入正确性、冷热数据切换、延迟与容量压测。
- 端到端测试要覆盖：空知识、知识过期、同义词、长文本截断、引用来源（citation）准确性。

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
