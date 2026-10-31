# OpenClaw Ecosystem Report 2026-03-01

> Issues: 500 | PRs: 500 | Projects covered: 10 | Generated at: 2026-03-01 00:08 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)

---

## OpenClaw Project Deep-Dive Report

# OpenClaw Project Report | 2026-03-01

## 1. Today at a Glance

OpenClaw maintained **extremely high development activity** today, with **500 issue updates** (373 new/active, 127 closed) and **500 PR updates** (401 pending merge, 99 merged/closed) within 24 hours, and no new release. The community focused on three main threads: **message lifecycle reliability engineering** (persistent deduplication, write-ahead logging, delivery queues), **multilingual internationalization** (the i18n system landing), and **authentication and cost optimization** (Anthropic OAuth fixes, prompt caching issues). Notably, @nohat submitted 6 PRs in a single day leading the messaging infrastructure refactor, showing the core architecture evolving toward production-grade reliability.

---

## 2. Releases

**No new release** (v2026.2.26 remains the latest version, but there is an Intel Mac regression reported in [#28877](https://github.com/openclaw/openclaw/issues/28877)).

---

## 3. Project Progress

### Key Merged/Closed PRs

| PR | Author | Core contribution | Project advancement |
|:---|:---|:---|:---|
| [#13622](https://github.com/openclaw/openclaw/pull/13622) | @vaur94 | Full Web UI internationalization system (EN/TR/FR/DE) | **Milestone**: the i18n architecture landed, laying the foundation for globalization |
| [#29993-29996](https://github.com/openclaw/openclaw/pull/29993) | @nohat | Batch-added the unified `sendPayload` interface across 16+ channel adapters | Standardizes the message delivery pipeline, supporting the upcoming outbox refactor |
| [#30112](https://github.com/openclaw/openclaw/pull/30112) | @kevinWangSheng | Kimi Coding subscription auth fix (User-Agent) + in-memory proxy environment variables | Unblocks subscription access for users in China and fixes enterprise proxy scenarios |

### Architecture-Level Advances (Pending Merge)

| PR | Author | Technical debt/innovation | Impact |
|:---|:---|:---|:---|
| [#30009](https://github.com/openclaw/openclaw/pull/30009) / [#30011](https://github.com/openclaw/openclaw/pull/30011) / [#30012](https://github.com/openclaw/openclaw/pull/30012) | @nohat | **Write-ahead log outbox + persistent turn tracking + orphan recovery** | **Exactly-once delivery** semantics for messages; no message loss on gateway restart |
| [#29793](https://github.com/openclaw/openclaw/pull/29793) | @nathan-deepmm | Concurrent write lock for workspace files | Solves lost updates when multiple agents share a workspace |
| [#16565](https://github.com/openclaw/openclaw/pull/16565) | @mdlmarkham | Agent-to-Agent invocation and debate tools | Multi-agent collaboration architecture, closing in on AutoGen/CrewAI capabilities |

**Overall assessment**: The project is leaping from "feature-complete" to "enterprise-grade reliability"; the message lifecycle and concurrency control are key investments at the infrastructure level.

---

## 4. Community Hotspots

### 🔥 Most-Discussed Issues

| Issue | Comments | Core ask | Status |
|:---|:---|:---|:---|
| [#3460](https://github.com/openclaw/openclaw/issues/3460) i18n & Localization Support | **71 comments** | Users worldwide strongly request multilingual support, but the maintainers have explicitly said they have "no bandwidth to support it" | **Open**; community PR #13622 already provides a partial implementation |
| [#4531](https://github.com/openclaw/openclaw/issues/4531) Docker pairing disconnects (1008) | 36 comments | WebSocket stability for self-hosted deployments | **Closed**; the pairing flow needs optimization |
| [#1818](https://github.com/openclaw/openclaw/issues/1818) Ubuntu systemd service not installed | 31 comments | systemd integration for Linux production deployments | **Closed**; root cause was user-service detection logic |
| [#9095](https://github.com/openclaw/openclaw/issues/9095) / [#23538](https://github.com/openclaw/openclaw/issues/23538) Anthropic OAuth 401 | 24+16 comments | **Blocking failure for subscription users**: the setup-token is stored successfully but fails at runtime | **#9095 Closed, #23538 Open**; suspected version regression |

### Analysis of the Underlying Asks

- **The 71 comments on #3460** show internationalization is a **growth bottleneck**: non-English users cannot use advanced features (such as the TUI `/` commands), while the maintenance team is resource-constrained, creating tension between "what the community wants" and "what the team can deliver".
- **The Anthropic OAuth twin issues** reveal a **state-inconsistency bug** in the authentication layer: the contexts for token storage and runtime usage are separated, possibly involving profile isolation or the token refresh mechanism.

---

## 5. Bugs and Stability

### 🔴 Critical (Blocks Usage)

| Issue | Symptom | Fix status | Impact scope |
|:---|:---|:---|:---|
| [#28877](https://github.com/openclaw/openclaw/issues/28877) | macOS v2026.2.26 is **arm64-only**; crashes on Intel Macs | **No PR**; the build configuration urgently needs a rollback | Intel Mac users completely unable to use it |
| [#23538](https://github.com/openclaw/openclaw/issues/23538) | Anthropic setup-token 401 (reproducible with an isolated profile) | **Open**; the #9095 fix may be incomplete | Claude subscription users |
| [#29572](https://github.com/openclaw/openclaw/issues/29572) | The `/model` TUI command fails silently; the model is not actually switched | **Open**; sessions.patch returns 200 but the state is not persisted | Multi-model users |
| [#26207](https://github.com/openclaw/openclaw/issues/26207) | v2026.2.24 `setGlobalDispatcher` breaks HTTP proxies | **Open**; GFW/enterprise proxy users cannot connect | Users in mainland China and enterprises |

### 🟡 High (Cost/Experience Degraded)

| Issue | Symptom | Fix status |
|:---|:---|:---|
| [#20894](https://github.com/openclaw/openclaw/issues/20894) / [#19989](https://github.com/openclaw/openclaw/issues/19989) / [#23715](https://github.com/openclaw/openclaw/issues/23715) | **Prompt cache misses causing 5-100x cost spikes** | #20894, #19989 **Closed**; #23715 **Open** (shared system prompt prefix issue) |
| [#7631](https://github.com/openclaw/openclaw/issues/7631) | Windows `spawn EINVAL` plugin installation failure | **Open**; a Node child process permission issue |
| [#29757](https://github.com/openclaw/openclaw/issues/29757) | Cron jobs run repeatedly after 2 hours | **Open**; a timezone/scheduler logic bug |

### 🟢 Medium/Low

- [#29214](https://github.com/openclaw/openclaw/issues/29214) Signal group-chat @mention not working
- [#28042](https://github.com/openclaw/openclaw/issues/28042) Avatar endpoint 404

---

## 6. Feature Requests and Roadmap Signals

### High Probability of Making the Next Release (PR exists or strong signals)

| Request | Issue/PR | Evidence |
|:---|:---|:---|
| **Full i18n system** | #3460 + #13622 (merged) + #28920 (Russian PR) | The architecture has landed; extending to more languages is cheap |
| **Encrypted key management** | [#7916](https://github.com/openclaw/openclaw/issues/7916) | 13 comments, 9 👍; a hard requirement for security compliance |
| **LLM input/output middleware hooks** | [#20416](https://github.com/openclaw/openclaw/issues/20416) | Enterprise needs for PII masking and content filtering |
| **Cron session isolation option** | [#20092](https://github.com/openclaw/openclaw/issues/20092) | 8 👍; PR #30140 fixes a related timeout issue |

### Long-Term Roadmap Signals (Require Architecture Decisions)

| Request | Issue | Blocker |
|:---|:---|:---|
| **Prevent agents from leaking API keys** | [#11829](https://github.com/openclaw/openclaw/issues/11829) | Requires refactoring prompt serialization and system prompt isolation |
| **Brave Search alternative** | [#16629](https://github.com/openclaw/openclaw/issues/16629) | With Brave going paid, DuckDuckGo/SearXNG need evaluation |
| **WeChat integration** | [#29591](https://github.com/openclaw/openclaw/issues/29591) | An unofficial ecosystem; compliance risk |

---

## 7. User Feedback Summary

### 😤 Core Pain Points

> *"5x API costs due to ineffective prompt caching"* — @svenssonaxel [#23715](https://github.com/openclaw/openclaw/issues/23715)

> *"Model context window too small (4096 tokens). Minimum is 16000"* — a default-configuration trap for custom API providers [#21653](https://github.com/openclaw/openclaw/issues/21653)

> *"CLI is extremely slow on pi4b — 17+ seconds for --help"* — performance on embedded devices [#5871](https://github.com/openclaw/openclaw/issues/5871)

> *"Telegram messages replaced on model failures"* — error handling eroding user trust [#19982](https://github.com/openclaw/openclaw/issues/19982)

### ✅ Satisfaction Scenarios

- Fast Docker deployment flow ([#4531](https://github.com/openclaw/openclaw/issues/4531) has problems, but the docs are clear)
- Unified multi-channel abstraction (users actively test the Signal, WhatsApp, and Telegram integrations)

### 📊 Usage Pattern Insights

- **Enterprise/self-hosted users**: highly focused on systemd, HTTP proxies, and key encryption
- **Cost-sensitive users**: dense feedback on prompt caching, model switching, and token billing
- **Chinese community**: strong demand for WeChat integration (#29591); the Kimi Coding subscription fix is urgent

---

## 8. Pending Backlog

### ⚠️ Long-Running Issues Needing Maintainer Attention

| Issue | Days | Risk | Suggested action |
|:---|:---|:---|:---|
| [#3460](https://github.com/openclaw/openclaw/issues/3460) official i18n support | 32 days | A community PR already exists; an official stance on the merge strategy is needed | Define the i18n maintenance model (community-driven vs official core) |
| [#5871](https://github.com/openclaw/openclaw/issues/5871) Pi4B CLI performance | 28 days | Usability in embedded scenarios | Profile performance; evaluate tree-shaking or a Rust rewrite |
| [#7916](https://github.com/openclaw/openclaw/issues/7916) encrypted key management | 26 days | A security compliance blocker | Prioritize in the Q2 roadmap |
| [#11829](https://github.com/openclaw/openclaw/issues/11829) API key leak prevention | 21 days | A barrier to enterprise adoption | Design the security architecture together with #7916 |
| [#20416](https://github.com/openclaw/openclaw/issues/20416) LLM middleware hooks | 11 days | Ecosystem extensibility | Evaluate compatibility with the existing plugin system |

### 🔧 Risks in PRs Pending Merge

- **#30009/#30011/#30012** (nohat's message lifecycle refactor): large batch PRs; the SQLite schema migrations and backward compatibility need careful review
- **#16565** (A2A agent invocation): a major architectural change; needs API design review

---

*Generated at: 2026-03-01 | Data source: OpenClaw GitHub public API*

---

## Cross-Ecosystem Comparison

# Comparative Analysis Report on the Open-Source Ecosystem of Personal AI Assistants
**Data baseline: 2026-03-01 | Analysis window: 24 hours**

---

## 1. Ecosystem Overview

The open-source ecosystem of personal AI assistants/autonomous agents is at **a critical stage of leaping from "feature-complete" to "production-grade reliability"**. The leading project OpenClaw maintains absolute dominance with 500+ issues/PRs of daily activity, but emerging forces such as ZeroClaw, PicoClaw, and NanoBot are catching up fast along differentiated paths: Rust/Go rewrites, multi-channel architectures, and enterprise-grade features. The ecosystem's technical focus is highly convergent: **message lifecycle reliability** (persistence, exactly-once delivery), **multi-vendor model compatibility** (OpenRouter, local Ollama, reasoning-model adaptation), and **enterprise deployment readiness** (OAuth, quota management, multi-tenancy) are the shared battlefronts. Meanwhile, "last-mile" experience issues such as Windows platform support, internationalization, and cost governance have become the main friction points driving user churn.

---

## 2. Project Activity Comparison

| Project | Language/framework | Issues (new/closed/active) | PRs (new/closed/pending) | Release | Health assessment |
|:---|:---|:---:|:---:|:---:|:---|
| **OpenClaw** | TypeScript/Node | 500 (373/127/500) | 500 (99/401) | None | 🟢 **Extremely active, architecture transition period** — dominated by messaging reliability refactors; the Intel Mac regression is unresolved |
| **ZeroClaw** | Rust | 50 (10/40/50) | 50 (44/6) | None | 🟢 **Intense iteration, quality sprint** — a CI queue backlog of 380+ is the bottleneck; dense compile-stability fixes |
| **NanoBot** | Python | 25 (21/4/25) | 79 (25/54) | v0.1.4.post3 | 🟢 **Fast iteration, pushing on enterprise channels** — QQ/Feishu/DingTalk stability fixes; the PR backlog needs attention |
| **PicoClaw** | Go | 85 (76/9/85) | 94 (18/76) | v0.2.0 (maintenance) | 🟢 **Extremely active, reliability hardening** — provider ecosystem expansion; systematic fixes for gateway concurrency/memory leaks |
| **NanoClaw** | TypeScript/Node | 12 (4/8/12) | 37 (9/28) | None | 🟡 **Steady maintenance, technical-debt cleanup** — 8 code-quality issues fixed in a batch; multi-channel architecture refactor underway |
| **IronClaw** | Rust | 10 (10/0/10) | 25 (2/23) | None | 🟡 **Highly active, review bottleneck** — 6 PRs hardening the install experience in matrix fashion; 23 PRs awaiting review |
| **ZeptoClaw** | Rust | 8 (8/0/8) | 2 (1/1) | None | 🟡 **Maintainer-driven roadmap** — 7 self-filed issues exploring multimodal/enterprise/IoT; community participation yet to be activated |
| **LobsterAI** | Python | 21 (19/2/21) | 4 (2/2) | None | 🟡 **High feedback pressure, responsive** — Ollama/Windows issues erupting in clusters; fast IM integration iteration |
| **EasyClaw** | Unspecified | 0 (0/0/0) | 0 (0/0) | v1.5.12+v1.5.13 | 🔴 **Silent maintenance, community dormant** — both back-to-back releases are macOS docs; zero issue/PR activity |
| **TinyClaw** | Unspecified | 1 (0/1/1) | 1 (0/1) | v0.0.7 (empty release) | 🔴 **Very low activity, trust crisis** — the Windows compatibility issue was closed on an emotional note with no technical response |

---

## 3. OpenClaw's Position in the Ecosystem

| Dimension | OpenClaw's performance | Ecosystem comparison |
|:---|:---|:---|
| **Community size** | Absolute lead: 500 issues/PRs of daily activity ≈ the sum of ranks 2-4 | ZeroClaw 50, PicoClaw 85, NanoBot 25 — a clear order-of-magnitude gap |
| **Technical route** | **Reliability-first incremental evolution** — message lifecycle (outbox, WAL, orphan recovery), concurrency control, persistent turn tracking | ZeroClaw/PicoClaw chose **Rust/Go rewrites** pursuing performance and memory safety; NanoBot bets on **the Python ecosystem and academic scenarios** |
| **Core strengths** | ① **The most mature channel abstraction** (16+ adapters unified behind the `sendPayload` interface)<br>② **Enterprise-grade reliability investment** (exactly-once delivery semantics)<br>③ **The largest skill ecosystem** (OpenClaw SKILL has become the de facto standard) | Weaknesses: high Node.js runtime resource usage (ZeroClaw users report 1.5GB of gateway overhead) and criticized compile/startup speed |
| **Competitive pressure** | ZeroClaw directly targets the migration path (#88 production-grade migration checklist); PicoClaw dissolves provider fragmentation with a LiteLLM unified proxy layer | Watch for churn in "performance-sensitive user" and "multi-vendor heterogeneous deployment" scenarios |

**Key differentiator**: OpenClaw is **the only project that has entered the deep water of "reliability engineering"** (@nohat's WAL/outbox refactor), while competitors are still filling feature gaps or migrating at the language level.

---

## 4. Commonly Focused Technical Directions

| Technical direction | Projects involved | Specific asks and signal strength |
|:---|:---|:---|
| **Message lifecycle reliability** | OpenClaw ⭐⭐⭐⭐⭐, ZeroClaw ⭐⭐⭐⭐, NanoClaw ⭐⭐⭐⭐ | OpenClaw: WAL + outbox + orphan recovery; ZeroClaw: in-memory data optimization; NanoClaw: OOM crash fix (ghost sockets) |
| **Multi-vendor model compatibility** | PicoClaw ⭐⭐⭐⭐⭐, LobsterAI ⭐⭐⭐⭐⭐, ZeptoClaw ⭐⭐⭐⭐⭐, ZeroClaw ⭐⭐⭐⭐ | PicoClaw: dense OpenRouter/Groq/MiniMax/LiteLLM PRs; LobsterAI: local Ollama models "completely unusable"; ZeptoClaw: Azure/Bedrock presets; ZeroClaw: hardcoded Anthropic ID fix |
| **Reasoning-model adaptation** | NanoBot ⭐⭐⭐⭐⭐, LobsterAI ⭐⭐⭐⭐ | NanoBot: `reasoning_content` field compatibility for DeepSeek/Kimi/o1; LobsterAI: prompt cache misses causing 5-100x cost spikes |
| **Enterprise deployment readiness** | IronClaw ⭐⭐⭐⭐⭐, ZeptoClaw ⭐⭐⭐⭐, OpenClaw ⭐⭐⭐⭐ | IronClaw: PostgreSQL version checks, TLS, multi-tenancy; ZeptoClaw: quota management, OAuth; OpenClaw: Anthropic OAuth fix |
| **Cost governance and caching** | OpenClaw ⭐⭐⭐⭐⭐, ZeptoClaw ⭐⭐⭐⭐ | OpenClaw: prompt cache misses (#20894/#19989/#23715); ZeptoClaw: per-provider quota management |
| **Windows platform support** | LobsterAI ⭐⭐⭐⭐⭐, TinyClaw ⭐⭐⭐⭐⭐, OpenClaw ⭐⭐⭐ | LobsterAI: 404 errors, garbled text, and permission issues erupting in clusters; TinyClaw: the "completely unusable" trust crisis; OpenClaw: `spawn EINVAL` plugin installation failure |
| **Internationalization (i18n)** | OpenClaw ⭐⭐⭐⭐⭐, ZeroClaw ⭐⭐⭐ | OpenClaw: #3460 with 71 comments; community PR #13622 already merged EN/TR/FR/DE; ZeroClaw: architecture ready, cheap to add languages |
| **Multi-channel architecture decoupling** | NanoClaw ⭐⭐⭐⭐⭐, ZeroClaw ⭐⭐⭐⭐ | NanoClaw: #500 pluggable architecture refactor (WhatsApp hard-coupling → generic abstraction); ZeroClaw: continuous DingTalk/Feishu/BlueBubbles iMessage expansion |

---

## 5. Differentiated Positioning Analysis

| Project | Core feature focus | Target user profile | Key technical architecture differences |
|:---|:---|:---|:---|
| **OpenClaw** | Enterprise-grade reliability, the largest channel ecosystem, a skill marketplace | Technical teams, multi-agent coordination scenarios, production environments needing "exactly-once" message guarantees | Node.js + SQLite; incremental reliability engineering; skills as plugins |
| **ZeroClaw** | Performance and memory efficiency; a landing spot for OpenClaw migrations | Users on resource-constrained VPSes (4vCPU/30GB RAM), Rust ecosystem fans, cost-sensitive users | Full-stack Rust; a "merge-first" migration strategy; a WASM skill runtime |
| **PicoClaw** | Lightweight gateway, unified provider proxy, local-model-first | Embedded/edge devices, multi-vendor routing needs, Go ecosystem users | Implemented in Go; a LiteLLM proxy layer dissolving fragmentation; pursuing smaller binaries |
| **NanoBot** | Academic/research scenarios, rapid prototyping, multi-channel enterprise IM | University labs, Feishu/DingTalk/QQ enterprise users, the Python data science ecosystem | Python + Qdrant vector storage; context noise reduction against hallucination; Skill as MCP |
| **IronClaw** | WASM secure execution, the NEAR blockchain ecosystem, multi-tenant SaaS | Blockchain developers; security-sensitive scenarios needing key scanning/isolation; a WASM plugin marketplace | Rust + WASM sandbox; NEAR AI integration; multi-scope memory architecture |
| **ZeptoClaw** | Multimodal (vision), IoT hardware, enterprise presets | Hardware makers (MQTT), consumer scenarios needing visual input, Azure/Bedrock enterprises | Rust; serial/UART/MQTT hardware channels; rapid roadmap iteration |
| **LobsterAI** | The Youdao Cloud Notes ecosystem, finely polished IM integrations, rapid version iteration | Chinese-speaking knowledge workers, heavy Feishu users, scenarios needing note integration | Python; synergy with the Youdao product matrix; a "release a day" cadence |
| **NanoClaw** | Finance/trading scenarios, containerized deployment, real-time tracking | Quant traders, professional users needing paper/live isolation, DevOps teams | TypeScript; atomic deployment pipelines; graceful Docker shutdown |
| **EasyClaw** | Desktop ease of use, macOS-first | Non-technical end users, individuals wanting one-click installation | Unspecified; both releases focus on Gatekeeper bypass documentation |
| **TinyClaw** | The OpenViking plugin ecosystem | Users with specific plugin needs | Unspecified; Windows support in doubt |

---

## 6. Community Heat and Maturity Tiers

| Tier | Projects | Characteristics | Stage assessment |
|:---|:---|:---|:---|
| **L1: Architecture transition** | OpenClaw | 500+ daily activity; a core refactor (WAL/outbox); moving from feature-complete → production-reliable | High risk, high reward; watch backward compatibility |
| **L2: Rapid iteration** | ZeroClaw, PicoClaw, NanoBot | 50-100 daily activity; feature sprints and quality fixes in parallel; the CI/PR backlog is the bottleneck | Scaling phase; review bandwidth needs strengthening |
| **L3: Quality consolidation** | NanoClaw, IronClaw | Proactive technical-debt cleanup (8 issues fixed in a batch); matrix-style hardening of the install experience | Steady, but review stagnation must be avoided |
| **L4: Roadmap exploration** | ZeptoClaw | 7 maintainer-driven strategic issues; community participation yet to be activated | An open RFC process is needed to bring in outside input |
| **L5: Feedback pressure** | LobsterAI | A high bug-report rate (Ollama/Windows); fast responses but architectural debt is showing | Balance iteration speed against root-cause fixes |
| **L6: Silence/crisis** | EasyClaw, TinyClaw | Zero activity or poorly handled negative events | EasyClaw needs to activate its community; TinyClaw needs to repair trust |

---

## 7. Trend Signals Worth Watching

| Trend | Signal sources | Reference value for developers |
|:---|:---|:---|
| **"Reasoning-model compatibility" is the new compatibility layer** | NanoBot, LobsterAI, and OpenClaw are seeing dense demand for `reasoning_content`, prompt caching, and thinking-content filtering | When designing an LLM abstraction layer, the **non-standard fields** and **cost structure** of reasoning models (DeepSeek-R1, Kimi, o1/o3) must be first-class citizens, not afterthought patches |
| **Local model deployment is shifting from a "hobbyist option" to a "cost necessity"** | LobsterAI #174 "Ollama never worked"; PicoClaw #28 one-click LM Studio connection; OpenClaw #5871 Pi4B performance | Edge/local inference optimization (quantization, hot model switching, memory management) will become a differentiating competitive strength rather than an edge feature |
| **Provider fragmentation is spawning a "unified proxy layer" standard** | PicoClaw #930 LiteLLM; ZeroClaw's hardcoded Anthropic ID fix; ZeptoClaw's Azure/Bedrock presets | New projects should integrate LiteLLM/a unified proxy layer first instead of adapting providers one by one; existing projects need to evaluate migration costs |
| **Multi-channel architecture is evolving from "channel adapters" to a "pluggable runtime"** | NanoClaw's #500 refactor; ZeroClaw's dense DingTalk/Feishu/BlueBubbles landings | The notion of a "channel" is generalizing into "interaction endpoints" (IM, email, hardware, web); unified abstractions for session isolation, identity, and rate limiting are needed |
| **Cost governance is moving forward from "after-the-fact bills" to "real-time quotas"** | ZeptoClaw #200 per-provider quotas; OpenClaw prompt cache misses; NanoBot abnormal token consumption | Enterprise scenarios need **per-call budget control** and **model fallback routing**, not just reliance on vendor-side limits |
| **Windows support is becoming a litmus test for "inclusiveness"** | TinyClaw's trust crisis; LobsterAI's clustered eruption of garbled text/404s; OpenClaw's `spawn EINVAL` | Claiming cross-platform support requires **automated Windows CI** and **native installers**, not "theoretical support" that exists only in documentation |
| **The skill/tool ecosystem is migrating from "code plugins" to "WASM sandbox + MCP"** | IronClaw's WASM channel; ZeroClaw's native MCP client; NanoBot's Skill as MCP | Secure execution and ecosystem interop needs are driving runtime isolation standardization; WASM + MCP may become the next-generation skill protocol stack |

---

**Report conclusion**: OpenClaw holds its leadership through reliability-engineering depth and ecosystem scale, but the Rust-rewrite camp (ZeroClaw, IronClaw, ZeptoClaw) and the Python pragmatist camp (NanoBot, LobsterAI) are forming an encirclement across performance, enterprise features, and vertical scenarios. The decisive factors over the next 6-12 months will be: **the maturity of unified abstractions for multi-model routing**, **the ability to optimize reasoning-model costs**, and **the completeness of the "last-mile" experience for Windows/enterprise deployments**.

---

## Detailed Reports for Same-Track Projects

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Report | 2026-03-01

## 1. Today at a Glance

ZeroClaw showed **intense iteration** today: within 24 hours it processed **50 issues** (40 closed/10 active) and **50 PRs** (44 merged/closed, 6 pending merge), with no new release. The project is in a **dense bug-fixing and feature-sprint phase**; compile-stability issues (S0-level) got quick responses, while community demand keeps heating up for iMessage support, OpenClaw migration paths, and multi-provider compatibility. CI infrastructure shows a significant bottleneck (an Actions queue backlog of more than 380), which may become a near-term delivery risk.

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### Core Feature Landings

| PR | Author | Key progress |
|:---|:---|:---|
| [#2212](https://github.com/zeroclaw-labs/zeroclaw/pull/2212) | @chumyin | **The OpenClaw migration tool is officially live**: implements a "merge-first" migration strategy, resolving data drift and overwrite risks, with an onboarding wizard and in-agent operations |
| [#2271](https://github.com/zeroclaw-labs/zeroclaw/pull/2271) | @maxtongwang | **The BlueBubbles iMessage channel merged**: fills the gap on the mainstream US IM platform; a webhook push architecture supporting macOS self-hosting |
| [#2296](https://github.com/zeroclaw-labs/zeroclaw/pull/2296) | @theonlyhennygod | **A SKILL.toml native tool handler**: skill-ecosystem infrastructure is ready, supporting trusted-domain installation and transparent preloading |
| [#1842](https://github.com/zeroclaw-labs/zeroclaw/pull/1842) | @zverozabr | **A circuit-breaker mechanism + provider health tracking**: prevents cascading failures and automatically fails over to healthy nodes |

### Channel and Integration Enhancements

| PR | Description |
|:---|:---|
| [#2297](https://github.com/zeroclaw-labs/zeroclaw/pull/2297) | DingTalk Open API proactive message sending (solves the cron reminder scenario)|
| [#2198](https://github.com/zeroclaw-labs/zeroclaw/pull/2198) | Configurable ACK emoji policy + the `channel_ack_config` tool |
| [#2147](https://github.com/zeroclaw-labs/zeroclaw/pull/2147) | Enriched DingTalk callback text payloads |
| [#1843](https://github.com/zeroclaw-labs/zeroclaw/pull/1843) | **A native MCP client**: stdio/HTTP/SSE tri-protocol support, connecting to the Claude Desktop ecosystem |

### Infrastructure and Reliability

| PR | Description |
|:---|:---|
| [#2300](https://github.com/zeroclaw-labs/zeroclaw/pull/2300) | Fix for error propagation in Prometheus metric registration (high risk)|
| [#2294](https://github.com/zeroclaw-labs/zeroclaw/pull/2294) | Aligned the wasmtime ecosystem dependencies to 36.0.6 |
| [#2295](https://github.com/zeroclaw-labs/zeroclaw/pull/2295) | OAuth UX improvements for server environments |
| [#2298](https://github.com/zeroclaw-labs/zeroclaw/pull/2298) | A REST-first PR validator (avoids GraphQL rate limits)|

---

## 4. Community Hotspots

### High-Interaction Issues (comments ≥ 4)

| Issue | Comments | Core ask | Status |
|:---|:---|:---|:---|
| [#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88) | 6 | **Production-grade OpenClaw→ZeroClaw migration blocker list**: the 4vCPU/30GB RAM VPS scenario; memory-usage optimization (the current OpenClaw gateway costs 1.5GB)| 🔄 Ongoing tracking |
| [#2175](https://github.com/zeroclaw-labs/zeroclaw/issues/2175) | 8 | **Compile error**: non-exhaustive pattern match on `ChannelRuntimeCommand` (`ApprovePendingRequest`/`DenyToolApproval` not covered)| ✅ Closed |
| [#2079](https://github.com/zeroclaw-labs/zeroclaw/issues/2079) | 5 | **A native GitHub channel**: a unified interface for observing/operating on repo activity (issues/PRs/comments/reviews) | ✅ Closed |
| [#2058](https://github.com/zeroclaw-labs/zeroclaw/issues/2058) | 5 | **OneBot v11 protocol support**: QQ Bot functionality is limited and needs community protocol supplements | ✅ Closed |
| [#2053](https://github.com/zeroclaw-labs/zeroclaw/issues/2053) | 5 | **Runtime configuration CLI**: `config show/get/set` subcommands, no more hand-editing toml | ✅ Closed |
| [#2270](https://github.com/zeroclaw-labs/zeroclaw/issues/2270) | 4 | **Hardcoded fallback model ID breaks non-Anthropic providers**: `anthropic/claude-sonnet-4-20250514` returns 400 on OpenRouter/Vertex/Bedrock | ✅ Closed |
| [#2223](https://github.com/zeroclaw-labs/zeroclaw/issues/2223) | 4 | **Web chat history loss**: `ws.rs` in-memory storage; a page refresh wipes it | ✅ Closed |

**Ask analysis**: production-migration readiness, multi-provider compatibility, and enterprise-grade observability/configuration management are the community's three most urgent themes.

---

## 5. Bugs and Stability

### S0 - Data Loss/Security Risk (Fixed)

| Issue | Problem | Fix PR |
|:---|:---|:---|
| [#2175](https://github.com/zeroclaw-labs/zeroclaw/issues/2175) | Compile failure: incomplete `ChannelRuntimeCommand` match | Merged |
| [#2206](https://github.com/zeroclaw-labs/zeroclaw/issues/2206) | v0.1.7 compile failure: missing `runtime_perplexity_filter_snapshot`; `DocxReadTool` undeclared | Merged |
| [#2230](https://github.com/zeroclaw-labs/zeroclaw/issues/2230) | `channel-lark` Windows compile failure | Merged |

### S1 - Workflow Blockage

| Issue | Problem | Status |
|:---|:---|:---|
| [#2275](https://github.com/zeroclaw-labs/zeroclaw/issues/2275) | README installation instructions accidentally deleted (commit 7d65b29) | ✅ Closed |

### S2 - Behavior Degradation

| Issue | Problem | Status |
|:---|:---|:---|
| [#2223](https://github.com/zeroclaw-labs/zeroclaw/issues/2223) | WebSocket chat history kept in memory, lost on refresh | ✅ Closed |
| [#2233](https://github.com/zeroclaw-labs/zeroclaw/issues/2233) | Feishu channel message duplication + configuration issues | ✅ Closed |
| [#2220](https://github.com/zeroclaw-labs/zeroclaw/issues/2220) | Cron jobs executing repeatedly in a loop | ✅ Closed |
| [#2210](https://github.com/zeroclaw-labs/zeroclaw/issues/2210) | Memory stores only user messages; agent replies are lost | ✅ Closed |
| [#2224](https://github.com/zeroclaw-labs/zeroclaw/issues/2224) | Slack shows raw user IDs instead of display names | ✅ Closed |
| [#2176](https://github.com/zeroclaw-labs/zeroclaw/issues/2176) | Web UI Agent Chat fails to connect when `require_pairing=true` | ✅ Closed |
| [#2181](https://github.com/zeroclaw-labs/zeroclaw/issues/2181) | QQ messages have no historical context | ✅ Closed |

### Pending Fix

| Issue | Problem | Severity |
|:---|:---|:---|
| [#2168](https://github.com/zeroclaw-labs/zeroclaw/issues/2168) | The Web Dashboard Agent tab is broken: `web/dist` assets mismatch the `ws.ts` auth changes | S2 |

---

## 6. Feature Requests and Roadmap Signals

### Slated for Recent Versions (PR exists or a clear plan)

| Request | Issue/PR | Signal strength |
|:---|:---|:---|
| Native GitHub channel | [#2079](https://github.com/zeroclaw-labs/zeroclaw/issues/2079) | ⭐⭐⭐ High (closed, pending implementation)|
| OneBot v11 support | [#2058](https://github.com/zeroclaw-labs/zeroclaw/issues/2058) | ⭐⭐⭐ High (closed)|
| Runtime configuration CLI | [#2053](https://github.com/zeroclaw-labs/zeroclaw/issues/2053) | ⭐⭐⭐ High (closed)|
| Cortex Memory backend | [#2208](https://github.com/zeroclaw-labs/zeroclaw/issues/2208) | ⭐⭐⭐ High (community ecosystem integration)|
| Sub-agent support | [#2204](https://github.com/zeroclaw-labs/zeroclaw/issues/2204) | ⭐⭐⭐ High (an architecture-level need)|

### Under Roadmap Discussion (RFI/design stage)

| Request | Issue | Description |
|:---|:---|:---|
| Multi-crate workspace split | [#2263](https://github.com/zeroclaw-labs/zeroclaw/issues/2263) | Formalized in M4-5; compile-time optimization; an RFI has been issued |
| Token consumption and cost management | [#2269](https://github.com/zeroclaw-labs/zeroclaw/issues/2269) | Cost feasibility for production deployments; tiered model routing |
| Memory re-indexing | [#2273](https://github.com/zeroclaw-labs/zeroclaw/issues/2273) | Embeddings going stale after model changes |

### To Be Evaluated

| Request | Issue | User scenario |
|:---|:---|:---|
| `default_model` hint support | [#2234](https://github.com/zeroclaw-labs/zeroclaw/issues/2234) | Configurable model routing |
| Local-model tool-count optimization | [#2264](https://github.com/zeroclaw-labs/zeroclaw/issues/2264) | Token waste from 33 tools on a 30B local model |

---

## 7. User Feedback Summary

### Pain Points

| Scenario | Source |
|:---|:---|
| **Compile stability**: v0.1.7 saw consecutive compile failures, hurting trust | [#2175](https://github.com/zeroclaw-labs/zeroclaw/issues/2175), [#2206](https://github.com/zeroclaw-labs/zeroclaw/issues/2206) |
| **Provider lock-in**: hardcoded Anthropic model IDs exclude heterogeneous deployments | [#2270](https://github.com/zeroclaw-labs/zeroclaw/issues/2270) |
| **Memory management**: web history loss; memory holds only user messages | [#2223](https://github.com/zeroclaw-labs/zeroclaw/issues/2223), [#2210](https://github.com/zeroclaw-labs/zeroclaw/issues/2210) |
| **CI bottleneck**: self-hosted runner queue saturation with a p99 wait of 656 minutes | [#2299](https://github.com/zeroclaw-labs/zeroclaw/issues/2299) |

### Satisfaction Points

- The OpenClaw migration path is getting official attention ([#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88) is highly upvoted)
- Enterprise channels such as DingTalk/Feishu keep improving
- iMessage support landed quickly

### Typical User Profile

> "We run OpenClaw in production on a 4vCPU/30GB RAM VPS, coordinating multiple AI sub-agents (Claude Code sessions). ZeroClaw's memory data caught our attention — the OpenClaw gateway currently costs about 1.5GB, directly competing for resources with our 3 concurrent Claude sessions." — @MbBrainz

---

## 8. Pending Backlog

### High-Priority Reminders

| Issue | Days | Risk | Suggested action |
|:---|:---|:---|:---|
| [#2299](https://github.com/zeroclaw-labs/zeroclaw/issues/2299) | 0 (new) | **CI infrastructure collapse risk**: 382 queued runs, longest wait 17+ hours | Urgently scale up runners or optimize the parallelism strategy |
| [#2263](https://github.com/zeroclaw-labs/zeroclaw/issues/2263) | 0 (new) | Multi-crate split RFI deadline | Maintainers need to respond to the design proposal |
| [#2269](https://github.com/zeroclaw-labs/zeroclaw/issues/2269) | 0 (new) | Production cost-model design | Needs a joint product/architecture review |
| [#1849](https://github.com/zeroclaw-labs/zeroclaw/pull/1849) | 4 | Prometheus error propagation (duplicate of #2300)| Close after evaluating #2300 as the replacement |
| [#2229](https://github.com/zeroclaw-labs/zeroclaw/pull/2229) | 1 | An XL-sized build-fix PR; restores the SOP/MQTT merge line | Needs review from a core maintainer |
| [#1870](https://github.com/zeroclaw-labs/zeroclaw/pull/1870) | 3 | Centralized provider-descriptor refactor | Medium priority; avoid conflicting with #1842 |

---

**Generated at**: 2026-03-01 \
**Data coverage**: GitHub activity over the past 24 hours

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw Project Report | 2026-03-01

> **Project URL**: https://github.com/gaoyangz77/easyclaw \
> **Observation window**: 2026-02-28 to 2026-03-01 (24 hours)

---

## 1. Today at a Glance

EasyClaw today shows the profile of **low code activity but a high release cadence**. Over the past 24 hours there were no new or closed issues or PRs, and community discussion is in a quiet period; however, the project shipped two patch releases in a row, **v1.5.12** and **v1.5.13**, indicating the maintainer is focused on **documentation polish and distribution optimization for the macOS installation experience**. Overall health assessment: **under stable maintenance**; core development activity has shifted toward release iteration rather than feature expansion. It is suitable for users to upgrade, but the persistently low community participation needs attention.

---

## 2. Releases

### 🔖 v1.5.13 | Latest
**Released at**: 2026-03-01 \
**Release link**: https://github.com/gaoyangz77/easyclaw/releases/tag/v1.5.13

| Dimension | Details |
|:---|:---|
| **Update type** | Documentation/distribution patch |
| **Core change** | Added a complete solution guide for the macOS Gatekeeper blocking issue |
| **Breaking changes** | None |
| **Migration note** | No migration needed; if macOS users hit the "damaged" prompt, they can remove the quarantine with the Terminal command in the release |

> **Key excerpt**: The release includes a bilingual (Chinese/English) macOS installation troubleshooting guide, providing Terminal fix steps for the `"'EasyClaw' is damaged and can't be opened"` error (the command is not fully shown; presumably an `xattr -cr` or `spctl` operation).

---

### 🔖 v1.5.12
**Released at**: 2026-02-28 (inferred, based on continuity with v1.5.13) \
**Release link**: https://github.com/gaoyangz77/easyclaw/releases/tag/v1.5.12

| Dimension | Details |
|:---|:---|
| **Update type** | Same as v1.5.13; macOS installation documentation optimization |
| **Relation to v1.5.13** | The content overlaps heavily; presumably a **rapid-iteration fix** or **batched uploads of multi-platform distribution packages** |

**Release cadence analysis**: Two releases within 24 hours with similar content; possible reasons:
- ① A problem was found after v1.5.12 shipped, and v1.5.13 fixed it urgently
- ② Version tags distinguishing Intel/Apple Silicon dual-architecture packages
- ③ A test trigger of the automated release pipeline

**Suggestion for the maintainer**: State the differences between versions in the release notes to avoid confusing users.

---

## 3. Project Progress

| Metric | Value | Status |
|:---|:---|:---|
| Merged PRs | 0 | — |
| Closed PRs | 0 | — |
| Feature progress | None | No code-level progress today |

**Progress assessment**: ⏸️ **Stalled**. No code merged today; core features did not move forward. The two consecutive releases are both **peripheral documentation polish**, showing the current priority is **lowering the onboarding barrier for new users** rather than feature iteration. This strategy is reasonable (macOS signing issues are a common desktop-app pain point), but in the long run "experience polish" and "feature evolution" need to be balanced.

---

## 4. Community Hotspots

**No active discussions today**.

| Metric | Value | Notes |
|:---|:---|:---|
| Active issues | 0 | No new issues, comments, or reactions |
| Active PRs | 0 | None awaiting review or merge discussion |
| Community participation | Extremely low | Zero interactions in 24 hours |

**Deeper signal**: Zero issues/PRs may reflect:
- ✅ A mature, stable project where users hit no blocking problems
- ⚠️ A small user base or poor feedback channels
- ⚠️ Insufficient community building; users lack motivation to participate

**Suggestion**: The maintainer could proactively enable the Discussions section or post a "user stories" call to activate the community.

---

## 5. Bugs and Stability

| Severity | Count | Details | Fix PR |
|:---|:---|:---|:---|
| 🔴 Critical | 0 | — | — |
| 🟠 High | 0 | — | — |
| 🟡 Medium | 0 | — | — |
| 🟢 Low | 0 | — | — |

**Stability assessment**: ✅ **No new bug reports**. Note, however, that **the release notes of v1.5.12/13 themselves reveal a known issue** — macOS Gatekeeper blocking is not an app bug, but it is **a distribution-level stability obstacle**. The maintainer has mitigated it with documentation; the long-term recommendation is to apply for Apple Developer ID signing for a permanent fix.

---

## 6. Feature Requests and Roadmap Signals

| Source | Content | Likelihood assessment |
|:---|:---|:---|
| Today's issues | None | — |
| Implicit release signals | Desktop experience optimization (macOS signing/installation) | 🔶 **High** — two consecutive releases focus on this; v1.6.x will presumably introduce proper signing |
| Speculative directions | Windows/Linux installer optimization, an auto-update mechanism | 🔶 **Medium** — following the macOS playbook, may proceed in parallel |

**Roadmap judgment**: The project is in a **"polish phase"**; the next milestones may be:
1. **v1.6.0**: Signed distribution on all platforms + auto-update
2. **v2.0 signals**: None yet (no architecture-level PRs or RFCs)

---

## 7. User Feedback Summary

**No direct user feedback today** (zero issues/zero PR comments).

**Indirect feedback extracted** (inferred from release content):

| Pain point | Source | Severity |
|:---|:---|:---|
| The macOS installation flow is blocked; users mistakenly think the file is damaged | Historical user reports → drove the v1.5.12/13 releases | High (blocks new-user conversion)|
| Lack of Chinese documentation | Answered by making the release bilingual | Medium |
| Unfamiliar with command-line fix steps | Release steps truncated (missing after `pres`)| Medium |

**Satisfaction inference**: Existing users are probably satisfied with the core features (no bug reports), but **the new-user onboarding experience has friction**.

---

## 8. Pending Backlog

| Type | Count | Longest age | Attention needed |
|:---|:---|:---|:---|
| Unanswered issues | 0 | — | — |
| Unanswered PRs | 0 | — | — |
| Legacy-version technical debt | Presumably exists | — | Suggest the maintainer review unclosed issues from before v1.5.12 |

**Backlog health**: ✅ **No backlog currently**. But watch out for the **hidden debt** behind "zero activity":
- Regularly scan **historical issues not linked to a release**
- Consider enabling **GitHub Discussions** to divert how-to questions

---

## 📊 Today's Health Score

| Dimension | Score | Notes |
|:---|:---|:---|
| Code activity | ⭐⭐☆☆☆ (2/5) | No PR merges |
| Release cadence | ⭐⭐⭐⭐⭐ (5/5) | Two consecutive releases |
| Community health | ⭐☆☆☆☆ (1/5) | Zero interactions |
| Documentation | ⭐⭐⭐⭐☆ (4/5) | Actively adding installation guides |
| Stability | ⭐⭐⭐⭐⭐ (5/5) | No new bugs |

**Overall**: ⭐⭐⭐☆☆ (3/5) — **solid maintenance, community yet to grow**

---

*This report is generated from public GitHub data; for deeper analysis, please provide issue/PR history or Discussions content.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Report | 2026-03-01

## 1. Today at a Glance

The LobsterAI community was extremely active today, with **21 issue updates** (19 active/new, 2 closed) and **4 PR updates** (2 pending merge, 2 merged/closed) within 24 hours. The project is in a rapid-iteration phase with user feedback pouring in, and the core pain points concentrate in three areas: **local model compatibility (Ollama), Windows platform stability, and multi-vendor API adaptation**. The maintenance team is responsive — today's merged PRs resolved the Feishu IM render mode and thinking-content filtering issues — but the backlog of feature requests and platform adaptation issues still needs sustained attention.

---

## 2. Releases

**No new release**

> Note: The latest version remains v0.1.22; user feedback repeatedly mentions that this version still has Ollama connection timeouts, Windows errors, and similar problems.

---

## 3. Project Progress

### Merged/Closed PRs

| PR | Author | Core improvement | Impact |
|:---|:---|:---|:---|
| [#83](https://github.com/netease-youdao/LobsterAI/pull/83) | @liugang519 | **Feishu IM rendering optimization**: the default renderMode switched to card with markdown support; **IM replies now filter thinking content** | Directly answers a high-frequency community ask (Issue #28), improving the IM integration experience |
| [#155](https://github.com/netease-youdao/LobsterAI/pull/155) | @liuzhq1986 | App update related (specific changes not described in detail) | Continued iteration on application-layer features |

### PRs Pending Merge

| PR | Author | Status | Value |
|:---|:---|:---|:---|
| [#127](https://github.com/netease-youdao/LobsterAI/pull/127) | @mammut001 | **Fixes the default-model problem in settings** — after setup it automatically picks the first enabled provider as activeProvider, avoiding stale baseUrl values from old configs | 🔴 **High priority**: resolves the root cause of multi-vendor configuration confusion |
| [#113](https://github.com/netease-youdao/LobsterAI/pull/113) | @hyooeewee | Dev-experience polish: adds `.vscode` to gitignore and symlinks `CLAUDE.md` to `AGENTS.md` | A maintainability improvement |

**Overall assessment**: Today's merged PRs targeted the UX problems of IM integration, but the core architectural issues (default model selection, multi-vendor adaptation) can only be fundamentally improved after #127 merges.

---

## 4. Community Hotspots

### Most-Discussed Issues

| Rank | Issue | Comments | Core ask |
|:---|:---|:---:|:---|
| 🥇 | [#150](https://github.com/netease-youdao/LobsterAI/issues/150) Ollama local deployment unusable | **4** | **Local model support is a hard need**: users want to escape cloud API limits and cut token costs, but the current implementation suffers connection timeouts and unresponsiveness |
| 🥈 | [#28](https://github.com/netease-youdao/LobsterAI/issues/28) [Closed] IM bot thinking-process display control | **3** | Resolved by PR #83, validating how fast the community feedback loop responds |
| 🥉 | [#185](https://github.com/netease-youdao/LobsterAI/issues/185) Suggest custom providers support the new OpenAI format | **2** | **API standard follow-up is lagging**: gpt-5.3-codex needs the new Responses API format, and users want LobsterAI to adapt to the latest model capabilities quickly |

**Underlying signal**: community demand is strong for **cost control (local models)** and **frontier model adaptation**; the project must balance "stable compatibility with the existing ecosystem" against "quickly following the latest standards".

---

## 5. Bugs and Stability

### 🔴 Critical (Blocks Usage)

| Issue | Platform/scenario | Symptom | Fix PR |
|:---|:---|:---|:---:|
| [#150](https://github.com/netease-youdao/LobsterAI/issues/150) | Ollama local deployment | Completely unusable; long unresponsiveness or timeouts | ❌ None |
| [#144](https://github.com/netease-youdao/LobsterAI/issues/144) [#184](https://github.com/netease-youdao/LobsterAI/issues/184) | Windows 11 | 404 Not Found errors (Anthropic SDK related) | ❌ None |
| [#187](https://github.com/netease-youdao/LobsterAI/issues/187) | Non-Alibaba models | Everything except Alibaba models is unusable | ❌ None |
| [#188](https://github.com/netease-youdao/LobsterAI/issues/188) | Skill system | All enabled by default but every call fails; the cygpath dependency is undocumented | ❌ None |
| [#139](https://github.com/netease-youdao/LobsterAI/issues/139) | IMAP mailbox configuration | The Claude Code process exits and cannot recover after configuration | ❌ None |

### 🟡 Medium (Affects Experience)

| Issue | Problem | Notes |
|:---|:---|:---|
| [#141](https://github.com/netease-youdao/LobsterAI/issues/141) | Sandbox file-read path concatenation error | Has a screenshot; clearly located |
| [#183](https://github.com/netease-youdao/LobsterAI/issues/183) | Garbled Chinese text in the Windows command line (a GBK/UTF-8 encoding issue) | Needs transcoding |
| [#180](https://github.com/netease-youdao/LobsterAI/issues/180) | [Closed] Insufficient read permission on Linux | ✅ Resolved |
| [#175](https://github.com/netease-youdao/LobsterAI/issues/175) | Private-cloud deployed models error on the Max_tokens parameter | DeepSeek/Qwen3 on-premises deployment scenario |
| [#178](https://github.com/netease-youdao/LobsterAI/issues/178) | NVIDIA LLM API connection failure | Custom configuration has no effect |

### 🟢 Performance and Resources

| Issue | Problem |
|:---|:---|
| [#177](https://github.com/netease-youdao/LobsterAI/issues/177) | Excessively high memory usage (a screenshot shows the resource consumption) |

---

## 6. Feature Requests and Roadmap Signals

| Issue | Request | Feasibility assessment | Likelihood of next release |
|:---|:---|:---|:---:|
| [#185](https://github.com/netease-youdao/LobsterAI/issues/185) | Support the new OpenAI Responses API format | Technical debt; requires refactoring the provider layer | 🔶 High (model adaptation is a core capability) |
| [#176](https://github.com/netease-youdao/LobsterAI/issues/176) | Task record grouping, notes, built-in Skill editing, TODO lists | A clear product direction with big synergy potential with the Youdao Cloud Notes ecosystem | 🔶 Medium-high (differentiating competitiveness) |
| [#181](https://github.com/netease-youdao/LobsterAI/issues/181) | @-trigger control for Telegram bot group chats | A need for finer-grained IM integration | 🔶 Medium (the approach of PR #83 can be reused) |
| [#179](https://github.com/netease-youdao/LobsterAI/issues/179) | A mechanism to start a new session from IM | A foundational session-management capability | 🔶 Medium |
| [#182](https://github.com/netease-youdao/LobsterAI/issues/182) | Headless/browser-access support | A server deployment scenario; the architecture rework cost needs evaluation | 🔷 Medium-low |
| [#174](https://github.com/netease-youdao/LobsterAI/issues/174) | Strengthen Ollama invocation | Related to #150; needs a systematic fix | 🔶 High (the loudest community voice) |

**Key insight**: Users compare LobsterAI with "the original OpenClaw" ([#186](https://github.com/netease-youdao/LobsterAI/issues/186)), pointing out the gap in **memory capability** — a potential long-term competitive risk.

---

## 7. User Feedback Summary

### 😊 Satisfaction Points
- **Fast iteration**: "The lobster has been shipping a version a day lately; you can tell problems are being fixed very quickly" ([#174](https://github.com/netease-youdao/LobsterAI/issues/174))
- **Timely IM integration response**: the resolution of Issue #28 shows how much the team values user feedback

### 😤 Core Pain Points

| Pain point | Typical feedback | Source |
|:---|:---|:---|
| **Ollama nearly unusable** | "From version 0.1.17 to now 0.1.22, not a single success" | [#174](https://github.com/netease-youdao/LobsterAI/issues/174) |
| **Poor Windows experience** | Garbled text, 404 errors, and permission issues erupting in clusters | #144, #183, #184 |
| **A feeling of vendor lock-in** | "It seems no non-Alibaba model works" | [#187](https://github.com/netease-youdao/LobsterAI/issues/187) |
| **Memory worse than competitors** | "Tried several models, none worked; not as good as the original openclaw" | [#186](https://github.com/netease-youdao/LobsterAI/issues/186) |
| **Missing docs/dependencies** | "The official tutorial doesn't seem to mention [cygpath]" | [#188](https://github.com/netease-youdao/LobsterAI/issues/188) |

### Usage Scenario Insights
- **Cost-sensitive users**: heavily dependent on local Ollama to cut token consumption
- **Enterprise/on-premises deployment**: need to connect to private-cloud models (DeepSeek/Qwen3) and are hitting parameter compatibility issues
- **IM automation**: Feishu, Discord, and Telegram group integrations are high-frequency scenarios

---

## 8. Pending Backlog

### Needs Maintainer Attention

| Issue/PR | Backlog reason | Suggested action |
|:---|:---|:---|
| [#127](https://github.com/netease-youdao/LobsterAI/pull/127) | Pending merge — fixes the default model selection logic and affects all multi-vendor users | **Merge first**; can resolve a large share of "model unusable" reports |
| [#150](https://github.com/netease-youdao/LobsterAI/issues/150) + [#174](https://github.com/netease-youdao/LobsterAI/issues/174) | Ollama support problems are scattered across multiple issues with no unified tracking | Create a meta-issue for unified planning, or assign a dedicated owner |
| [#176](https://github.com/netease-youdao/LobsterAI/issues/176) | A big product feature request involving synergy with the Youdao Cloud Notes ecosystem | Evaluate adding it to the official roadmap and set user expectations |
| [#186](https://github.com/netease-youdao/LobsterAI/issues/186) | Memory capability comparison against competitor OpenClaw | Technical research to identify the root cause of the gap (model layer? architecture layer?) |

---

**Generated at**: 2026-03-01 \
**Data source**: GitHub API / manually compiled \
**Project URL**: https://github.com/netease-youdao/LobsterAI

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Report | 2026-03-01

> **Project URL**: [github.com/qhkm/zeptoclaw](https://github.com/qhkm/zeptoclaw) \
> **Positioning**: An open-source framework for AI agents and personal AI assistants

---

## 1. Today at a Glance

Over the past 24 hours ZeptoClaw has been in a **high-activity development state**: core maintainer @qhkm filed 7 feature issues and 1 security-fix PR in a single day, while community contributor @superhero75 keeps reporting Telegram-scenario needs. All 8 active issues are newly opened, covering strategic directions such as multimodal, IoT, and enterprise integration; on the PR side, #192 (the MCP stdio transport) was merged, and #194 (a security fix) awaits review. Overall signal: **the project is leaping from "basic framework" to "production-grade platform"**, with enterprise features (Azure/Bedrock, quota management) and the hardware ecosystem (MQTT) as new focal points.

---

## 2. Releases

**No new release** \
The latest release is still a historical version; watch for a v0.x milestone release potentially triggered by the feature cluster now taking shape (vision support + enterprise providers + quota management).

---

## 3. Project Progress

| PR | Status | Core contribution | Progress |
|:---|:---|:---|:---|
| [#192](https://github.com/qhkm/zeptoclaw/pull/192) | **Merged** | MCP protocol support for the **stdio transport**, implementing the transport abstraction architecture (a unified Http/Stdio interface) | ⭐⭐⭐⭐☆ **Architecture upgrade**: opens an access path for local MCP servers (e.g., the Claude Desktop plugin ecosystem); key infrastructure for "tools as a service" |
| [#195](https://github.com/qhkm/zeptoclaw/pull/195) | Pending merge | Security hardening: 6 new regexes for dangerous git commands in the shell blocklist (`push --force`, `reset --hard`, `clean -f`, etc.) | ⭐⭐⭐⭐⭐ **Security red line**: blocks the path where sub-agents bypass the safe git tools via shell; essential for production deployment |

**Technical-debt signal**: with #192 merged, watch the MCP shutdown lifecycle and the edge cases in transport error handling.

---

## 4. Community Hotspots

| Rank | Issue | Heat indicators | Ask analysis |
|:---|:---|:---|:---|
| 🔥1 | [#193](https://github.com/qhkm/zeptoclaw/issues/193) Telegram endpoint hot-switching | 3 comments; @superhero75 keeps following up | **A real pain point**: an escape hatch when LLM endpoints rate-limit/fail on the road; the user explicitly benchmarks the OpenClaw-style `/models` + `/model` command design — the interaction-layer need is clear |
| 2 | [#196](https://github.com/qhkm/zeptoclaw/issues/196) SearXNG search integration | 0 comments, but it fits the self-hosting trend | A typical ask from cost-sensitive users: replacing paid search APIs; highly aligned with ZeptoClaw's "decentralized" positioning |
| 3 | The other 6 issues self-filed by @qhkm | 0 comments; maintainer-driven | Roadmap-level feature exploration; the window for community participation has not opened yet |

**Insight**: #193 is currently the only feature request with real user dialogue; responding to it first is recommended to keep community contributors engaged.

---

## 5. Bugs and Stability

| Severity | Issue/PR | Description | Fix status |
|:---|:---|:---|:---|
| 🔴 **Critical** | [#194](https://github.com/qhkm/zeptoclaw/issues/194) / [#195](https://github.com/qhkm/zeptoclaw/pull/195) | Sub-agents can execute destructive git operations (force-push, hard reset) via shell, bypassing the safe git tools | **PR #195 pending merge**; expected to be resolved within 24h |
| 🟡 Medium | — | No new stability issues | — |

**Security assessment**: #194 is a "design-level privilege escape" affecting multi-tenant/shared-repository deployment scenarios. After #195 merges, add integration tests: verify that a sub-agent attempting `git push --force` is blocked and gets a clear error.

---

## 6. Feature Requests and Roadmap Signals

| Issue | Feature area | Likelihood of next release | Key dependency |
|:---|:---|:---|:---|
| [#197](https://github.com/qhkm/zeptoclaw/issues/197) Vision input across all channels | Multimodal core | ⭐⭐⭐⭐⭐ **Very high** | "Table stakes for a messaging bot in 2026"; the maintainer has made the priority explicit |
| [#198](https://github.com/qhkm/zeptoclaw/issues/198) Azure OpenAI / Bedrock presets | Enterprise integration | ⭐⭐⭐⭐⭐ **Very high** | Unlocks enterprise customers with zero code; configuration-layer work with no architectural risk |
| [#200](https://github.com/qhkm/zeptoclaw/issues/200) Per-provider quota management | Cost governance | ⭐⭐⭐⭐☆ **High** | Depends on the maturity of the #197/#198 provider abstraction |
| [#199](https://github.com/qhkm/zeptoclaw/issues/199) MQTT IoT channel | Hardware ecosystem | ⭐⭐⭐☆☆ **Medium** | The fusion plan with the existing serial/UART architecture needs evaluation |
| [#201](https://github.com/qhkm/zeptoclaw/issues/201) DOCX extraction tool | Document processing | ⭐⭐⭐⭐☆ **High** | Same pattern as the `pdf_read` tool; low implementation cost |
| [#196](https://github.com/qhkm/zeptoclaw/issues/196) SearXNG search | Tool ecosystem | ⭐⭐⭐☆☆ **Medium** | Requires designing a generic search tool abstraction (a unified interface for SearXNG / SerpAPI / Bing) |
| [#193](https://github.com/qhkm/zeptoclaw/issues/193) Telegram endpoint switching | Interaction optimization | ⭐⭐⭐⭐☆ **High** | The community contributor has provided requirement details; a good fit for the `good first issue` label |

**Roadmap speculation**: The next version (v0.x) will most likely bundle **#197 + #198 + #201**, forming a production-grade feature triangle of "vision + enterprise + documents".

---

## 7. User Feedback Summary

> Distilled from the #193 comment thread and the issue description

| Dimension | Details |
|:---|:---|
| **Pain point** | "Most llm endpoints have rate limit, it is difficult to switch to another model/endpoint **on the road**" — anxiety about service continuity while mobile/away |
| **Usage scenario** | Telegram as the primary interaction surface, needing OpenClaw-style command-driven model management (`/models` listing, `/model <name>` switching) |
| **Satisfaction point** | ZeptoClaw's multi-channel architecture (Telegram/Discord/WhatsApp/Slack/Lark/email) is taken as a given; the user chooses to dig into the Telegram scenario |
| **Dissatisfaction/expectation** | For endpoint switching the user says "scope estimate: No idea" — unsure about implementation complexity and needs a feasibility response from the maintainer |

**Suggested action**: @qhkm could reply in #193 with a technical feasibility assessment (whether to reuse the existing provider configuration hot-reload mechanism) and invite @superhero75 to join the command interaction design.

---

## 8. Pending Backlog

> All of today's items are newly opened issues/PRs with no long-term backlog. But watch the following **hidden debt**:

| Risk item | Description | Suggested action |
|:---|:---|:---|
| #193 community contributor response window | @superhero75 has contributed 2 feature requests in a row and may churn if no maintainer responds within 48h | Reply with a feasibility assessment first |
| MCP #192 documentation gap | The merged content involves the transport abstraction architecture, but the PR description did not update the user docs | Add `docs/mcp.md` or rustdoc in the code |
| The digestion pace of 7 self-filed issues in one day | @qhkm dropped four themes at once — multimodal, IoT, enterprise, cost governance — and community information overload must be avoided | Create a GitHub Project board with priority labels (P0/P1/P2) |

---

**Generated at**: 2026-03-01 \
**Data cutoff**: 2026-02-28 24:00 UTC \
**Maintainer**: @qhkm | Active contributor: @superhero75

</details>

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Report | 2026-03-01

## 1. Today at a Glance

NanoBot stayed **extremely active** today, with **25 issue updates** (21 active/new, 4 closed) and **79 PR updates** (54 pending merge, 25 merged/closed) within 24 hours, plus the **v0.1.4.post3** patch release. The contributor base keeps growing, with 16 new contributors. Core work focused on **multi-channel stability fixes** (QQ, DingTalk, Feishu, Matrix, Telegram), **reasoning-model compatibility** (DeepSeek, Moonshot Kimi), and a **memory architecture upgrade** (Qdrant vector storage). The project is in a rapid-iteration phase with a high PR backlog (54 pending merge); merge throughput needs attention.

---

## 2. Releases

### [v0.1.4.post3](https://github.com/HKUDS/nanobot/releases/tag/v0.1.4.post3)

| Attribute | Details |
|:---|:---|
| **Release date** | 2026-02-28 |
| **PRs merged** | 33 |
| **New contributors** | 16 |
| **Core themes** | Context noise reduction, session history hardening, ghost message elimination |

**Key improvements:**
- **"Less noise in → less hallucination out"** — reduces model hallucination by cleaning up context, strengthening session history management, and cutting ghost messages
- Context window optimization: a smarter context-trimming strategy
- Session isolation enhancement: prevents history messages from polluting the current conversation

**Migration notes:** Upgrading is recommended for all users, especially those running multi-session instances long-term; response quality improves noticeably.

---

## 3. Project Progress

### Important PRs Merged/Closed Today

| PR | Author | Core contribution | Status |
|:---|:---|:---|:---|
| [#1346](https://github.com/HKUDS/nanobot/pull/1346) | @zerone0x | **Fixed the QQ channel read-only file system error** — disables botpy file logging, resolving startup failures under systemd `ProtectSystem=strict` | ✅ Merged |
| [#1348](https://github.com/HKUDS/nanobot/pull/1348) | @yorkhellen | **Fixed the Feishu channel startup crash** — removes the call to the nonexistent `lark.ws.Client.stop()` method | ✅ Merged |
| [#1330](https://github.com/HKUDS/nanobot/pull/1330) | @fengxiaohu | **Fixed reasoning-model compatibility** — allows the `reasoning_content` field in message history, resolving Moonshot Kimi tool-call failures | ✅ Merged |
| [#1337](https://github.com/HKUDS/nanobot/pull/1337) | @asdf17128 | **DingTalk channel enhancement** — supports sending image messages (previously file attachments only) | ✅ Merged |
| [#1351](https://github.com/HKUDS/nanobot/pull/1351) | @Re-bin | **Added reasoning-effort configuration** — the `reasoning_effort` parameter (low/medium/high), supporting thinking modes on models like OpenAI o1 | ✅ Merged |
| [#1347](https://github.com/HKUDS/nanobot/pull/1347) | @Re-bin | **Refactor** — simplifies sub-agent prompt construction by reusing ContextBuilder, cutting lines of code by 42% | ✅ Merged |

**Overall progress assessment:** Today's merged PRs concentrated on **production stability problems of enterprise IM channels** (QQ, Feishu, DingTalk) and filled in **reasoning-model ecosystem support** (DeepSeek, Kimi, o1). The project took a key step forward in enterprise deployment reliability.

---

## 4. Community Hotspots

### High-Discussion Issues

| Issue | Comments | Core ask | Analysis |
|:---|:---|:---|:---|
| [#215 Feishu cannot establish a long connection](https://github.com/HKUDS/nanobot/issues/215) | **21** | Long-connection mode still cannot be enabled after Feishu event subscription is configured | **A deployment blocker for enterprise users** — a gap between the configuration docs and actual behavior makes self-service troubleshooting hard |
| [#222 Multi agents setup - Supported?](https://github.com/HKUDS/nanobot/issues/222) | **6** | The support status of multi-agent configuration and missing documentation | **A perception gap on architecture capability** — users infer multi-agent support from the config, but without official guidance they easily misconfigure |
| [#1302 per-session working directory isolation](https://github.com/HKUDS/nanobot/issues/1302) | **4** | Multiple sessions sharing a working directory cause file conflicts | **A hard need for multi-tenant scenarios** — PR [#1345](https://github.com/HKUDS/nanobot/pull/1345) is addressing it |

**Hotspot trend:** Enterprise users' scaled deployment needs are prominent (Feishu, multi-agent isolation, working-directory isolation); the project needs stronger enterprise documentation and configuration validation tooling.

---

## 5. Bugs and Stability

### Sorted by Severity

| Priority | Issue | Description | Fix PR | Status |
|:---|:---|:---|:---|:---|
| 🔴 **P0-fixed** | [#1343](https://github.com/HKUDS/nanobot/issues/1343) | QQ channel systemd service startup failure: `Read-only file system: '/botpy.log'` | [#1346](https://github.com/HKUDS/nanobot/pull/1346) | ✅ Merged |
| 🔴 **P0-fixed** | [#1348](https://github.com/HKUDS/nanobot/pull/1348) | Feishu channel startup crash: call to the nonexistent method `lark.ws.Client.stop()` | [#1348](https://github.com/HKUDS/nanobot/pull/1348) | ✅ Merged |
| 🟡 **P1-active** | [#1313](https://github.com/HKUDS/nanobot/issues/1313) | Moonshot Kimi reasoning-model tool-call failure: missing `reasoning_content` | [#1330](https://github.com/HKUDS/nanobot/pull/1330) | ✅ Merged |
| 🟡 **P1-active** | [#1225](https://github.com/HKUDS/nanobot/issues/1225) | DeepSeek-R1 reasoning-model request format error: missing `reasoning_content` | Whether #1330 covers it needs verification | 🔍 Needs confirmation |
| 🟡 **P1-active** | [#1300](https://github.com/HKUDS/nanobot/issues/1300) | The Matrix channel completely fails to start | None | ❌ Pending fix |
| 🟡 **P1-active** | [#1315](https://github.com/HKUDS/nanobot/issues/1315) | Discord slash commands conflict with native commands; memory clearing broken | None | ❌ Pending fix |
| 🟢 **P2-active** | [#1318](https://github.com/HKUDS/nanobot/issues/1318) | The bot replies to messages repeatedly after a Skill is installed | None | ❌ Pending fix |
| 🟢 **P2-active** | [#1332](https://github.com/HKUDS/nanobot/issues/1332) | Abnormal token consumption: a single "hello" costs 5000+ tokens | None | ❌ Needs analysis |

**Stability assessment:** Three P0 production issues were fixed today, but the Matrix and Discord channels still have blocking bugs. Reasoning-model compatibility problems show a trend of erupting in clusters (DeepSeek, Kimi, Codex).

---

## 6. Feature Requests and Roadmap Signals

| Request | Issue/PR | Maturity | Likelihood of next version |
|:---|:---|:---|:---|
| **Claude Code subscription support** | [#281](https://github.com/HKUDS/nanobot/issues/281) + [#1333](https://github.com/HKUDS/nanobot/pull/1333) | 🟢 PR submitted | **High** — strong user demand, PR ready |
| **Multi search engine support (Baidu)** | [#1354](https://github.com/HKUDS/nanobot/pull/1354) | 🟢 PR submitted | **High** — a hard need for users in China; code complete |
| **Web chat UI (SSE streaming)** | [#1341](https://github.com/HKUDS/nanobot/pull/1341) | 🟢 PR submitted | **Medium-high** — lowers the barrier for new users |
| **Qdrant multi-embedding-model support** | [#1357](https://github.com/HKUDS/nanobot/pull/1357) | 🟢 PR submitted | **Medium-high** — a core memory architecture upgrade |
| **Per-session working directory isolation** | [#1302](https://github.com/HKUDS/nanobot/issues/1302) + [#1345](https://github.com/HKUDS/nanobot/pull/1345) | 🟡 PR awaiting review | **Medium** — architectural changes need care |
| **Window Protocol/native iOS app** | [#339](https://github.com/HKUDS/nanobot/pull/339) | 🟡 Long-running PR | **Medium-low** — innovative but a heavy maintenance burden |
| **Telegram message reaction support** | [#1334](https://github.com/HKUDS/nanobot/issues/1334) + [#1338](https://github.com/HKUDS/nanobot/issues/1338) | 🔴 Duplicate issue | **Low** — duplicate requests must be merged first |

---

## 7. User Feedback Summary

### Real Pain Points

| Scenario | Feedback source | Core complaint |
|:---|:---|:---|
| **Enterprise deployment** | [#215](https://github.com/HKUDS/nanobot/issues/215) Feishu users | "The configuration is all correct but the long connection never establishes; there's no troubleshooting documentation" |
| **Cost control** | [#1332](https://github.com/HKUDS/nanobot/issues/1332) | "hello costs 5000 tokens; asking one installation question costs 30 thousand tokens" |
| **Model compatibility** | [#1313](https://github.com/HKUDS/nanobot/issues/1313), [#1225](https://github.com/HKUDS/nanobot/issues/1225) | "Reasoning models crash as soon as they're used, and the error messages are unreadable" |
| **Multi-user isolation** | [#1302](https://github.com/HKUDS/nanobot/issues/1302) | "Files from different users get mixed together and pollute each other" |
| **Skill ecosystem** | [#1328](https://github.com/HKUDS/nanobot/issues/1328) | "Gateway users can't use skills created by agents" |
| **Output format** | [#110](https://github.com/HKUDS/nanobot/issues/110) | "Told it repeatedly not to use markdown, it still outputs markdown" |

### Positive Feedback
- [#1358](https://github.com/HKUDS/nanobot/issues/1358) user: "Got Whisper transcription running locally on a 2019 MBP + Docker + OpenRouter; not fast but extremely accurate"

---

## 8. Pending Backlog

### High-Value Items Needing Maintainer Attention

| Type | Item | Waiting time | Risk/opportunity |
|:---|:---|:---|:---|
| **PR backlog** | [#339](https://github.com/HKUDS/nanobot/pull/339) Window Protocol | ~20 days | A differentiating native iOS experience, but review is stalled |
| **PR backlog** | [#1299](https://github.com/HKUDS/nanobot/pull/1299) Cursor CLI configuration support | ~1 day | Low code risk; a quick merge improves the developer experience |
| **Duplicate issue** | [#1334](https://github.com/HKUDS/nanobot/issues/1334) vs [#1338](https://github.com/HKUDS/nanobot/issues/1338) Telegram Reaction | Same day | Need to mark as duplicate and track together |
| **Security audit** | [#1232](https://github.com/HKUDS/nanobot/issues/1232) SkillSec security assessment proposal | ~2 days | A 25k+ stars project should take security audits seriously; an official response is recommended |
| **Architecture debt** | [#1310](https://github.com/HKUDS/nanobot/issues/1310) Information loss in the two-phase heartbeat mechanism | Today | A core task-tracking mechanism; needs an architecture-level evaluation |

---

**Generated at:** 2026-03-01 \
**Data source:** GitHub API (HKUDS/nanobot)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Report | 2026-03-01

## 1. Today at a Glance

PicoClaw was **extremely active** today, with **85 issue updates** (89% new/active) and **94 PR updates** (81% pending merge) within 24 hours, as community contributors keep pouring in. The project just released **v0.2.0**, but the changelog shows it is mostly documentation and QR-code updates; feature iteration remains concentrated on the main branch. The provider ecosystem (OpenRouter, Groq, MiniMax, LiteLLM, etc.) was today's technical focus, while gateway stability, session persistence, and error-handling PRs emerged in clusters, signaling the project's move from a feature-expansion phase into a **reliability-hardening phase**.

---

## 2. Releases

### [v0.2.0](https://github.com/sipeed/picoclaw/releases/tag/v0.2.0) Released

| Attribute | Content |
|:---|:---|
| **Release date** | 2026-02-28 |
| **Core changes** | Documentation maintenance: updated the WeChat QR code, removed unused MP4 files, added CONTRIBUTING.md |
| **Breaking changes** | None |
| **Migration note** | No migration needed; a purely maintenance release |

> ⚠️ **Observation**: The version number jumped while feature changes are minimal; the maintainer should consider a finer-grained versioning strategy (e.g., 0.1.3) to avoid a gap between users' feature expectations for a new version and reality.

---

## 3. Project Progress

### Today's Key PR Advances (18 merged/closed)

| PR | Author | Progress | Technical value |
|:---|:---|:---|:---|
| [#920](https://github.com/sipeed/picoclaw/pull/920) | @CZH-THU | **Key bug fix** | `gateway status` no longer wrongly starts the full gateway runtime, resolving the multi-instance contention problem |
| [#919](https://github.com/sipeed/picoclaw/pull/919) | @CZH-THU | Reliability improvement | Better error handling for the GitHub Copilot provider; no more ignored `SendAndWait` errors |
| [#918](https://github.com/sipeed/picoclaw/pull/918) | @alexhoshina | Concurrency safety | Fixed context leaks and data races in the WeCom channel |
| [#917](https://github.com/sipeed/picoclaw/pull/917) | @ItsT0ng | Resource management | Cancels the context promptly after transcription in the Slack channel, preventing resource leaks |
| [#913](https://github.com/sipeed/picoclaw/pull/913) | @westwind027 | Tool enhancement | Local improvement commits for the shell tool |
| [#911](https://github.com/sipeed/picoclaw/pull/911) | @ItsT0ng | Performance optimization | HTTP status regexes precompiled, avoiding recompilation on every error classification |
| [#883](https://github.com/sipeed/picoclaw/pull/883) | @afjcjsbx | Stability hardening | The WebFetch tool gains strict memory limits (prevents OOM/bandwidth exhaustion) |
| [#864](https://github.com/sipeed/picoclaw/pull/864) | @afjcjsbx | Reliability improvement | Better error handling for state manager file operations |

**Overall assessment**: Today's merged PRs focus on **stability, resource management, and concurrency safety**, marking the project's evolution from "feature-complete" to "production-reliable". Low-level problems such as gateway multi-instance contention, memory leaks, and data races received systematic fixes.

---

## 4. Community Hotspots

### Most-Discussed Issues (sorted by comments)

| Rank | Issue | Comments | Core ask | Underlying signal |
|:---|:---|:---:|:---|:---|
| 1 | [#694](https://github.com/sipeed/picoclaw/issues/694) OpenRouter API configuration | 14 | Missing documentation for multi-model routing configuration | **Provider configuration UX is the biggest pain point**; users need clearer configuration examples |
| 2 | [#4](https://github.com/sipeed/picoclaw/issues/4) Gateway not visible on the local network | 11 | AMD Ryzen + Ubuntu: the gateway cannot be discovered after startup | Closed, but it reflects that the **gateway network discovery mechanism** still needs work |
| 3 | [#901](https://github.com/sipeed/picoclaw/issues/901) Failing to add OpenRouter/free models | 10 | Free-model identification and configuration problems | **The OpenRouter integration is not mature enough**; the free/paid model distinction logic needs improvement |
| 4 | [#680](https://github.com/sipeed/picoclaw/issues/680) Default api_base points to GLM | 10 | DeepSeek configuration wrongly routed to GLM | **The provider routing logic has a hardcoding trap** |
| 5 | [#79](https://github.com/sipeed/picoclaw/issues/79) Gemini 3 Flash function-calling failure | 9 | Tool calls fail due to the missing thought_signature | **Adaptation to Google's latest model lags behind** |
| 6 | [#28](https://github.com/sipeed/picoclaw/issues/28) Easy LM Studio connection | 8 | The need for one-click local LLM connection | **The local-model user base is huge**; LM Studio/Ollama integration is a differentiation opportunity |
| 7 | [#148](https://github.com/sipeed/picoclaw/issues/148) OpenClaw SKILL compatibility | 8 | An ecosystem compatibility ask | Users want **skill ecosystem interop** to avoid duplicated development |

### High-Value PR Discussions

| PR | Technical direction | Significance |
|:---|:---|:---|
| [#930](https://github.com/sipeed/picoclaw/pull/930) LiteLLM provider alias support | Unified proxy layer | Solves multi-provider fragmentation; one PR covers dozens of model backends |
| [#633](https://github.com/sipeed/picoclaw/pull/633) MiniMax provider | Support for domestic models | Answers the [#675](https://github.com/sipeed/picoclaw/issues/675) feature request, filling the MiniMax-M2.5 support gap |
| [#926](https://github.com/sipeed/picoclaw/pull/926) Anthropic OAuth login | Enterprise-grade authentication | Supports setup-token and usage monitoring, aimed at team deployment scenarios |
| [#925](https://github.com/sipeed/picoclaw/pull/925) Route OpenAI/Gemini protocols to SDKs | Architecture optimization | Official SDKs replace the HTTP compatibility layer, gaining full feature support |

---

## 5. Bugs and Stability

### Bugs Reported Today (by severity)

| Severity | Issue/PR | Description | Status |
|:---|:---|:---|:---|
| 🔴 **P0 - data corruption** | [#704](https://github.com/sipeed/picoclaw/issues/704) | A race condition in session history mismatches tool_call_ids with response messages, HTTP 400 | Pending fix; [#711](https://github.com/sipeed/picoclaw/issues/711) proposes a JSONL persistence scheme |
| 🔴 **P0 - feature completely broken** | [#901](https://github.com/sipeed/picoclaw/issues/901) | OpenRouter/free models cannot be added at all | Under investigation |
| 🟡 **P1 - core feature malfunction** | [#680](https://github.com/sipeed/picoclaw/issues/680) | The default api_base is hardcoded to GLM, overriding DeepSeek and other configurations | Pending fix |
| 🟡 **P1 - core feature malfunction** | [#748](https://github.com/sipeed/picoclaw/issues/748) | Groq API tool-call format error (`<function=name>` is a non-standard format) | Pending fix |
| 🟡 **P1 - provider adaptation** | [#79](https://github.com/sipeed/picoclaw/issues/79) | Gemini 3 Flash Preview function calling fails due to the missing thought_signature | Pending fix |
| 🟡 **P1 - user experience** | [#778](https://github.com/sipeed/picoclaw/issues/778) | Session summaries lose context; conversation quality drops after compression | Pending fix |
| 🟢 **P2 - configuration experience** | [#109](https://github.com/sipeed/picoclaw/issues/109) | Local Ollama configuration still prompts "no API key" | Pending fix |
| 🟢 **P2 - fixed** | [#671](https://github.com/sipeed/picoclaw/issues/671) | `gateway status` starts extra worker processes | ✅ Fixed by [#920](https://github.com/sipeed/picoclaw/pull/920) |
| 🟢 **P2 - fixed** | [#683](https://github.com/sipeed/picoclaw/issues/683) | Network timeouts misclassified as context-window errors | Closed |

### Stability-Fix PRs (Pending Merge Today)

- [#920](https://github.com/sipeed/picoclaw/pull/920) Gateway status command fix
- [#919](https://github.com/sipeed/picoclaw/pull/919) Copilot error handling
- [#918](https://github.com/sipeed/picoclaw/pull/918) / [#917](https://github.com/sipeed/picoclaw/pull/917) Channel resource-leak fixes
- [#883](https://github.com/sipeed/picoclaw/pull/883) WebFetch memory limits
- [#864](https://github.com/sipeed/picoclaw/pull/864) State file-operation error handling

---

## 6. Feature Requests and Roadmap Signals

### High Probability of Making the Next Release (PR exists or strong signals)

| Feature | Source | Evidence | Expected version |
|:---|:---|:---|:---:|
| **LiteLLM unified proxy** | PR [#930](https://github.com/sipeed/picoclaw/pull/930) | Newly filed today; solves the core provider fragmentation pain point | v0.3.0 |
| **MiniMax support** | PR [#633](https://github.com/sipeed/picoclaw/pull/633) + Issue [#675](https://github.com/sipeed/picoclaw/issues/675) | Clear demand for domestic models; PR ready | v0.2.1 |
| **Anthropic OAuth** | PR [#926](https://github.com/sipeed/picoclaw/pull/926) | A hard need for enterprise team deployment | v0.2.1 |
| **Session JSONL persistence** | Issue [#711](https://github.com/sipeed/picoclaw/issues/711) | Solves the #704 data corruption problem; an architecture-level improvement | v0.3.0 |
| **Agent sandbox (Docker)** | PR [#536](https://github.com/sipeed/picoclaw/pull/536) | A secure execution environment; WIP | v0.3.0 |

### Strong User Demand but No PR Yet

| Feature | Source | User voice | Suggested priority |
|:---|:---|:---|:---:|
| **LM Studio one-click connection** | [#28](https://github.com/sipeed/picoclaw/issues/28) (8 comments, 👍1) | "just outside my reach" — the technical barrier blocks local users | P1 |
| **OpenClaw SKILL compatibility** | [#148](https://github.com/sipeed/picoclaw/issues/148) (8 comments, 👍2) | Ecosystem interop avoids duplicated development | P2 |
| **Azure OpenAI** | [#260](https://github.com/sipeed/picoclaw/issues/260) | Enterprise compliance needs | P2 |
| **`picoclaw doctor` diagnostics tool** | [#39](https://github.com/sipeed/picoclaw/issues/39) | Configuration validation, health checks, repair workflows | P2 |
| **Remote agent communication** | [#669](https://github.com/sipeed/picoclaw/issues/669) | Clustered agent architecture | P3 |

---

## 7. User Feedback Summary

### Real Pain Points

> *"My current config structure... How to set config for openrouter api?"* — @0xSaurabhx [#694](https://github.com/sipeed/picoclaw/issues/694)

**A configuration discoverability crisis**: even with a JSON structure provided, users still cannot configure OpenRouter correctly — documentation and validation are both missing.

> *"Task hang without retry, logs output 'error' then stop"* — @manhnt9 [#629](https://github.com/sipeed/picoclaw/issues/629)

**Long-task reliability**: LLM call failures have no retry mechanism; long tasks crash midway and cannot recover.

> *"Summary contains no relevant context"* — @hum-ma [#778](https://github.com/sipeed/picoclaw/issues/778)

**Session compression quality**: the summarization mechanism loses key context; conversations "forget" after compression.

### Usage Scenario Insights

| Scenario | Representative issues | Estimated share |
|:---|:---|:---:|
| Local/on-premises deployment | #28 LM Studio, #75 Ollama, #109 local configuration | ~25% |
| Multi-model routing | #694 OpenRouter, #901 free models, #680 configuration conflict | ~30% |
| Enterprise/team deployment | #926 OAuth, #260 Azure, #669 remote communication | ~20% |
| Channel integration | #639 Discord, #99 WhatsApp, #667 Telegram | ~15% |
| Edge/embedded | #171 smaller binaries, constrained hardware resources | ~10% |

### Satisfaction Signals

- ✅ Positive: the CLI agent runs single tasks stably (mentioned in [#36](https://github.com/sipeed/picoclaw/issues/36))
- ❌ Negative: gateway-mode reliability is below expectations ([#36](https://github.com/sipeed/picoclaw/issues/36) Telegram hangs, [#671](https://github.com/sipeed/picoclaw/issues/671) multi-instance contention)

---

## 8. Pending Backlog

### Important Issues Long Unanswered (>7 days, high interaction)

| Issue | Days | Comments | Risk | Suggested action |
|:---|:---:|:---:|:---|:---|
| [#75](https://github.com/sipeed/picoclaw/issues/75) Ollama support | 16 | 6, 👍6 | Churn among local-model users | An official response and joint planning with #28 |
| [#79](https://github.com/sipeed/picoclaw/issues/79) Gemini 3 Flash | 16 | 9 | Lagging adaptation to Google's latest model | Fix first or document the limitation |
| [#28](https://github.com/sipeed/picoclaw/issues/28) LM Studio | 17 | 8 | The local-user base is being ignored | Unify the local-model strategy with #75 |
| [#39](https://github.com/sipeed/picoclaw/issues/39) doctor command | 18 | 3 | Support costs stay high | Recruit community contributors |
| [#171](https://github.com/sipeed/picoclaw/issues/171) Smaller binaries | 15 | 3 | Expansion into embedded scenarios blocked | Evaluate the feasibility of a build-tags PR |

### High-Value PRs Awaiting Review

| PR | Days waiting | Value | Blocking risk |
|:---|:---:|:---|:---|
| [#633](https://github.com/sipeed/picoclaw/pull/633) MiniMax | 7 | The domestic model ecosystem | The author may lose motivation |
| [#536](https://github.com/sipeed/picoclaw/pull/536) Docker sandbox | 9 | Foundation for secure execution | Needs an architecture review; long-term WIP |
| [#300](https://github.com/sipeed/picoclaw/pull/300) Telegram commands | 12 | User experience | A simple feature with a fast-merge window |

---

## Appendix: Data Quick Reference

| Metric | Value | Period-over-period assessment |
|:---|:---:|:---|
| Issue updates | 85 | 🔥 Extremely high |
| PR updates | 94 | 🔥 Extremely high |
| Releases | 1 (v0.2.0) | Maintenance release |
| PRs pending merge | 76 | Review bandwidth needs attention |
| Most active community topic | Provider configuration/routing | A typical trait of the ecosystem-integration phase |

---

*Generated at: 2026-03-01* \
*Data source: GitHub API / sipeed/picoclaw*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Report | 2026-03-01

## 1. Today at a Glance

NanoClaw showed **very high activity** today, processing **37 PRs** (9 merged/closed, 28 awaiting review) and **12 issues** (8 closed, 4 pending) within 24 hours. Core maintainer @klangberater efficiently closed 8 code-quality and security-related issues in a single day, showing the team's proactive technical-debt cleanup. Community contributors focused on three directions: **stability fixes** (OOM crashes, memory leaks), **multi-channel expansion** (Gmail, Slack, Feishu), and **architecture modernization** (a pluggable channel architecture, third-party model support). Overall project health is good, but the PR backlog rate (75%) suggests review bandwidth may become a bottleneck.

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### Important PRs Merged/Closed

| PR | Author | Core contribution | Project advancement |
|:---|:---|:---|:---|
| [#593](https://github.com/qwibitai/nanoclaw/pull/593) | @tglowaski | **Atomic deployment pipeline + Dev Container** | Production reliability greatly improved; failed deployments have zero impact; a standardized dev environment |
| [#594](https://github.com/qwibitai/nanoclaw/pull/594) | @tglowaski | **Real-time trade tracking + run isolation** | Stronger finance-scenario capability; paper trading separated from live trading; Dashboard filtering |
| [#470](https://github.com/qwibitai/nanoclaw/pull/470) | @youyouhe | **Graceful Docker container shutdown** | Solves systemd's 90s-timeout forced container kill, guaranteeing data integrity |
| [#600](https://github.com/qwibitai/nanoclaw/pull/600) | @miiimchelle | **Job-hunt workflow personalization + AI-Slop reviewer** | Vertical-scenario expansion, but closed (possibly merged into another branch) |
| [#589](https://github.com/qwibitai/nanoclaw/pull/589) | @pkhlebko | **Telegram models v1** | Channel expansion, but closed (the plan may have changed) |

### Code-Quality Push (8 Issues Fixed in a Batch)

@klangberater systematically fixed deep-seated defects today:
- **Memory safety**: container output buffers not released [#582](https://github.com/qwibitai/nanoclaw/issues/582)
- **Concurrency safety**: GroupQueue race condition [#578](https://github.com/qwibitai/nanoclaw/issues/578), inconsistent retry logic [#583](https://github.com/qwibitai/nanoclaw/issues/583)
- **Input validation**: path-traversal edge cases [#584](https://github.com/qwibitai/nanoclaw/issues/584), MAX_CONCURRENT_CONTAINERS has no upper bound [#581](https://github.com/qwibitai/nanoclaw/issues/581)
- **Error handling**: silently swallowed errors [#580](https://github.com/qwibitai/nanoclaw/issues/580), unguarded JSON.parse [#579](https://github.com/qwibitai/nanoclaw/issues/579)
- **Build fixes**: Rollup dependency issues [#585](https://github.com/qwibitai/nanoclaw/issues/585)

---

## 4. Community Hotspots

### High-Attention Topics

| Topic | Type | Heat signal | Core ask analysis |
|:---|:---|:---|:---|
| [#595](https://github.com/qwibitai/nanoclaw/issues/595) / [#596](https://github.com/qwibitai/nanoclaw/pull/596) | Bug + fix PR | A production crash; a critical fix PR already exists | **Long-run stability**: the ~40-hour OOM crash is a memory leak from old sockets not being destroyed during WhatsApp reconnects. Community user @scruffalo proactively provided detailed logs and a fix, showing how deeply production users are engaged |
| [#500](https://github.com/qwibitai/nanoclaw/pull/500) | Architecture refactor | The underlying infrastructure for multi-channel expansion | **Decoupling the hardcoded architecture**: moving from WhatsApp hard-coupling to a "pluggable multi-channel architecture" is a key step in the project's evolution from a single-IM tool to a general AI assistant platform |
| [#598](https://github.com/qwibitai/nanoclaw/pull/598) | Feature expansion | Enterprise integration scenarios | **A hard need for multi-channel**: Gmail + Slack support reflects enterprise users' wish to run NanoClaw as a central AI workbench |
| [#592](https://github.com/qwibitai/nanoclaw/pull/592) | Model support | The third-party LLM ecosystem | **Vendor diversification**: ANTHROPIC_BASE_URL and custom token support meet enterprise on-premises deployment and cost-optimization needs |

### Ask Insights
- **Rising enterprise demand**: PRs for Slack, Gmail, Google Workspace MCP, etc. appeared together — a clear signal
- **Stability before features**: the OOM crash issue and its fix PR appeared the same day; the community responded quickly
- **Geographic expansion**: Feishu/Lark support [#590](https://github.com/qwibitai/nanoclaw/pull/590) reflects demand in China/Southeast Asia

---

## 5. Bugs and Stability

| Severity | Problem | Status | Fix PR | Impact scope |
|:---|:---|:---|:---|:---|
| 🔴 **Critical** | OOM crash: ghost sockets accumulate on WhatsApp reconnect | Critical fix available | [#596](https://github.com/qwibitai/nanoclaw/pull/596) | Long-running instances (>40h), production environments |
| 🟡 **High** | Scheduler tasks execute repeatedly (execution exceeds the poll interval) | Awaiting review | [#601](https://github.com/qwibitai/nanoclaw/pull/601) | Scheduled-task scenarios |
| 🟡 **High** | Linux orphan containers not cleaned up | Awaiting review | [#588](https://github.com/qwibitai/nanoclaw/pull/588) | Linux production deployments |
| 🟢 **Medium** | Mobile website layout errors | Pending | None | Docs/brand experience |
| 🟢 **Medium** | Containers lack the `jq` tool | Pending | None | API response parsing, a safer alternative |

**Note**: The 8 issues closed by @klangberater were all latent defects found in code review, with no user reports of actual triggers yet — a display of **proactive defensive maintenance**.

---

## 6. Feature Requests and Roadmap Signals

| Feature direction | Representative PR/issue | Maturity | Likelihood of next version |
|:---|:---|:---|:---|
| **Multi-channel architecture refactor** | [#500](https://github.com/qwibitai/nanoclaw/pull/500) | A core architecture PR with a large blast radius | ⭐⭐⭐⭐⭐ High priority; infrastructure-grade |
| **Third-party model support** | [#592](https://github.com/qwibitai/nanoclaw/pull/592) | Configuration-layer expansion, low invasiveness | ⭐⭐⭐⭐⭐ High likelihood; clear community demand |
| **Google Workspace integration** | [#597](https://github.com/qwibitai/nanoclaw/pull/597) | As an MCP Skill, standardized | ⭐⭐⭐⭐☆ High likelihood; enterprise scenario |
| **Feishu/Lark channel** | [#590](https://github.com/qwibitai/nanoclaw/pull/590) | A new Skill with a mature pattern | ⭐⭐⭐⭐☆ High likelihood; geographic expansion |
| **Gmail + Slack channels** | [#598](https://github.com/qwibitai/nanoclaw/pull/598) | A personally customized PR that needs generalizing | ⭐⭐⭐☆☆ Medium; may be folded into #500 |
| **Job-hunt/resume workflow** | [#600](https://github.com/qwibitai/nanoclaw/pull/600) (closed)| A vertical scenario, overly specific | ⭐⭐☆☆☆ Low likelihood; may become a sample Skill |
| **Team dashboard** | [#344](https://github.com/qwibitai/nanoclaw/pull/344) | Long-open; needs maintainer feedback | ⭐⭐⭐☆☆ Medium; the UI direction is undecided |

---

## 7. User Feedback Summary

### Real Pain Points
> *"NanoClaw crashes with a JavaScript heap OOM error after running for ~40 hours... `launchd` restarts the process silently, so the bot stops responding briefly then recovers — easy to miss without checking `logs/nanoclaw.error.log`"* — @scruffalo [#595](https://github.com/qwibitai/nanoclaw/issues/595)

**Insight**: silent failures are more dangerous than crashes; better observability is needed (a health check endpoint?)

> *"it would be wise to include jq for parsing responses... Right now, the swam tends to use `node -e` for parsing, but that can cause eval attacks"* — @ErikDeBruijn [#574](https://github.com/qwibitai/nanoclaw/issues/574)

**Insight**: security-minded community members are watching the attack surface of the container toolchain

### Usage Scenarios
- **Long-running services**: the OOM issue shows users deploy NanoClaw as 24/7 infrastructure
- **Multi-IM workbench**: parallel requests for Gmail/Slack/Feishu — additive, not replacements
- **Finance/trading scenarios**: the real-time trade tracking PR reveals a professional user base

### Satisfaction Signals
- Proactive fix contributions: @scruffalo filed a complete fix PR alongside the problem report
- Detailed problem reports: including logs, reproduction steps, and system environment

---

## 8. Pending Backlog

| PR/Issue | Open duration | Risk | Suggested action |
|:---|:---|:---|:---|
| [#344](https://github.com/qwibitai/nanoclaw/pull/344) Add agent team dashboard | 8 days | Feature complete but no maintainer feedback; the contributor may churn | Clarify the dashboard's product direction, or provide design feedback |
| [#506](https://github.com/qwibitai/nanoclaw/pull/506) Save tokens in debug skill | 3 days | A simple optimization; an unnecessary backlog item | Review quickly and merge or close |
| [#466](https://github.com/qwibitai/nanoclaw/pull/466) Exponential backoff for WhatsApp reconnect | 5 days | Related to but independent of #596; possible conflict | Coordinate the approaches of @ianzein2 and @scruffalo |
| [#491](https://github.com/qwibitai/nanoclaw/pull/491) Filter protocol messages | 4 days | A performance optimization, low invasiveness | Review first to reduce wasted processing |
| [#385](https://github.com/qwibitai/nanoclaw/pull/385) @mention support for WhatsApp | 7 days | A social feature, user experience | Evaluate compatibility with the core architecture |

**Maintainer note**: Of the 28 PRs awaiting review, **the architecture-level PR #500** and **the stability fix #596** should be handled first, to unblock the downstream PRs depending on them.

---

*This report is generated from public GitHub data, time range: 2026-02-28 UTC*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Report | 2026-03-01

---

## 1. Today at a Glance

IronClaw was in a **high-intensity active state** today; 25 PR updates in a single day (23 awaiting review) set a recent peak. Core contributor @zmanian led 14 PR submissions, focusing on **install-experience hardening** (PostgreSQL version checks, pgvector validation, TLS support) and **security-layer reinforcement** (inbound message key scanning, key-name normalization). The community simultaneously produced major feature proposals such as a multi-tenant architecture (the #348-#351 series) and Podman support (#414). On the issue side, 10 newly opened with none closed, reflecting the typical support pressure of a user-base expansion phase. Overall assessment: **a healthy development rhythm, but the code-review queue backlog needs attention**.

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### PRs Merged/Closed Today (2)

| PR | Author | Core contribution | Significance for the project |
|:---|:---|:---|:---|
| [#295](https://github.com/nearai/ironclaw/pull/295) | @zmanian | Skills system integration tests (Tier 1-3) | Establishes a quality baseline for the skill ecosystem, paving the way for a third-party skill marketplace |
| [#425](https://github.com/nearai/ironclaw/pull/425) | @BroccoliFin | Dynamic CLI log-level control (`--logs`) | Improves operational observability and reduces production debugging friction |

### Key Progress Areas

**Systematic install-experience hardening** (6 PRs forming a complete fix matrix):
- **The PostgreSQL ecosystem**: #423 adds a version check (≥15) + a pgvector preflight; #427 introduces TLS support, unlocking managed databases (AWS RDS/Neon/Supabase)
- **Tunnel configuration**: #424 validates the cloudflared binary and token format; #430 fixes Tailscale daemon-mode hangs
- **Credential management**: #431 normalizes key-name casing, curing the Slack "not_authed" error at the root

**Proactive security-layer defense**:
- [#433](https://github.com/nearai/ironclaw/pull/433) Inbound message key scanning — blocks the loop-leak risk from users accidentally pasting API keys

**WASM channel integrity**:
- [#421](https://github.com/nearai/ironclaw/pull/421) Completes the credential injection mechanism so the `credentials` block in `capabilities.json` actually takes effect

---

## 4. Community Hotspots

### Discussion Focus: Installation Friction and Cross-Project Learning

| Topic | Heat indicators | Core ask analysis |
|:---|:---|:---|
| [#407 Ideas from Hermes Agent worth adopting](https://github.com/nearai/ironclaw/issues/407) | 2 comments; @zmanian involved | **An architecture benchmarking need**: users want IronClaw to absorb Hermes Agent's mature patterns (multi-channel, tool execution, memory, skills), hinting the project needs a sharper differentiated value proposition |
| [#413 Slack Channel fails with "not_authed"](https://github.com/nearai/ironclaw/issues/413) | 1 comment; a v0.12.0 regression | **Credential injection failure + CLI config amnesia**: users hit a double configuration-layer break; fix PRs #431 and #426 already exist |

### The Multi-Tenant Architecture Trilogy (Long-Running Hotspot)

| PR chain | Status | Technical-debt signal |
|:---|:---|:---|
| [#348](https://github.com/nearai/ironclaw/pull/348) → #349 → #351 | All awaiting review | Layered memory → multi-scope reads → user-isolated workspaces, forming the complete implementation of Issue #59. The dependency chain is long; merging #348 first is recommended to cut rebase costs |

---

## 5. Bugs and Stability

| Severity | Issue/PR | Description | Fix status |
|:---|:---|:---|:---|
| 🔴 **High** | [#413](https://github.com/nearai/ironclaw/issues/413) | Slack WASM channel "not_authed" + CLI config lost on restart | ✅ #431 (key-name normalization), #426 (.env persistence) |
| 🔴 **High** | [#415](https://github.com/nearai/ironclaw/issues/415) | The setup wizard does not validate the PostgreSQL version (accepting PG 14 causes migration failures) | ✅ #423 |
| 🔴 **High** | [#416](https://github.com/nearai/ironclaw/issues/416) | No pgvector preflight; cryptic migration error messages | ✅ #423 |
| 🟡 **Medium** | [#418](https://github.com/nearai/ironclaw/issues/418) | The Cloudflare tunnel does not check the binary/validate the token | ✅ #424 |
| 🟡 **Medium** | [#419](https://github.com/nearai/ironclaw/issues/419) | Conflicting cloudflared services not detected (brew vs system) | 🔄 #428 (included in the batch fix) |
| 🟡 **Medium** | [#420](https://github.com/nearai/ironclaw/issues/420) | The zsh completion file does not guard `compdef` calls | ✅ #422 |
| 🟡 **Medium** | [#417](https://github.com/nearai/ironclaw/issues/417) | No guidance for macOS Docker auto-start | 🔄 #428 |
| 🟢 **Low** | [#410](https://github.com/nearai/ironclaw/issues/410) | Tablet UI cropping | ⏳ Awaiting response |

**Regression risk**: #413 reveals a configuration-persistence defect in v0.12.0; an emergency patch release is recommended.

---

## 6. Feature Requests and Roadmap Signals

| Request | Source | Feasibility assessment | Version signal |
|:---|:---|:---|:---|
| **WASM-extended key operation capability** | [#412](https://github.com/nearai/ironclaw/issues/412) @dpc | High — a hard need for secure signing scenarios; requires designing an HSM abstraction layer | v0.13+ |
| **Native Podman support** | [#414](https://github.com/nearai/ironclaw/pull/414) @elohmeier | High — bollard is already compatible; no new dependencies | v0.12.1 or v0.13 |
| **Multi-tenant/workspace isolation** | The #348-#351 series | Medium — architecturally complex; needs phased delivery | A v0.14 flagship feature |
| **WhatsApp enterprise-grade reliability** | [#403](https://github.com/nearai/ironclaw/pull/403) @jrevillard | High — webhook verification + dedup + read receipts; production ready | v0.12.1 |

**Roadmap inference**: short term focuses on install-experience polish (v0.12.1); mid term bets on multi-tenant enterprise features (v0.14); long term needs a response to WASM secure-computing extensions.

---

## 7. User Feedback Summary

### Real Pain Points

> *"The setup wizard accepted any DATABASE_URL and attempts to run migrations without checking the PostgreSQL server version"* —— [#415](https://github.com/nearai/ironclaw/issues/415)

**Diagnosis**: early users were mostly tech enthusiasts; the project is now expanding to a broader developer population, making a **defensive setup wizard** a hard need. @zmanian's 6 setup-related PRs in one day precisely answer this trend.

> *"If a user sources this file before compinit has run in their .zshrc, they get: compdef: command not found"* —— [#420](https://github.com/nearai/ironclaw/issues/420)

**Diagnosis**: shell-integration details affect the professional developer experience; the mature patterns of tools like rustup/starship should be followed.

### Satisfaction Signals

- The Hermes Agent benchmarking proposal (#407) hints that users endorse IronClaw's **architectural positioning**
- The merge of the skills system tests (#295) reflects long-term confidence in the **extension ecosystem**

### Dissatisfaction Signals

- No response on tablet UI cropping (#410); there is a blind spot in the **mobile/multi-device experience**
- Config loss on restart (#413) creates the negative perception of "config amnesia"

---

## 8. Pending Backlog

| Type | Item | Days in backlog | Risk note |
|:---|:---|:---|:---|
| 📚 Documentation | [#294 Comprehensive documentation suite](https://github.com/nearai/ironclaw/pull/294) | 7 days | Blocks new-contributor onboarding; echoes the #407 benchmarking need |
| 🔧 Feature | [#403 WhatsApp enterprise-grade reliability](https://github.com/nearai/ironclaw/pull/403) | 2 days | Fully implemented; review resources needed |
| 🏗️ Architecture | [#348-#351 multi-tenant chain](https://github.com/nearai/ironclaw/pull/348) | 5 days | Blocked by the dependency chain; suggest @standardtoaster sync the merge cadence with the maintainers |
| 🐛 Bug | [#410 Tablet UI cropped](https://github.com/nearai/ironclaw/issues/410) | 1 day | Missing response; hurts impressions among mobile users |

---

**Data as of**: 2026-03-01 00:00 UTC \
**Project health**: 🟢 Active development (fast code flow) | 🟡 Review backlog (23 PRs awaiting review) | 🔴 Install-experience regression needs attention

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Report | 2026-03-01

> **Project**: [TinyAGI/tinyclaw](https://github.com/TinyAGI/tinyclaw) — An open-source framework for AI agents and personal AI assistants \
> **Analysis date**: 2026-03-01 \
> **Data window**: the past 24 hours

---

## 1. Today at a Glance

TinyClaw's activity was **low** today: only one release (v0.0.7) and one issue closed, with no new issues or PR merges. The community saw a **notable cross-platform compatibility dispute** — a Windows user left heated feedback after hitting multiple blockers during setup, revealing a gap between the project's Windows support documentation and the actual experience. On the technical side, the hardening work on the OpenViking plugin architecture is still ongoing and pending merge.

---

## 2. Releases

### [v0.0.7](https://github.com/TinyAGI/tinyclaw/releases/tag/v0.0.7) | 2026-03-01

| Attribute | Details |
|:---|:---|
| **Type** | Version bump (chore) |
| **Changes** | Only bumps the version from 0.0.6 to 0.0.7 ([#148](https://github.com/TinyAGI/tinyclaw/pull/148)) |
| **Breaking changes** | None |
| **Migration note** | No action needed |

**Assessment**: This release is an **empty version** with no functional updates or fixes. Given the community's Windows compatibility feedback, the maintenance team should consider accelerating the release cadence of substantive fixes, to avoid version-number inflation and a gap with user expectations.

---

## 3. Project Progress

### PRs/Issues Merged/Closed Today

| Item | Status | Notes |
|:---|:---|:---|
| [#151](https://github.com/TinyAGI/tinyclaw/issues/151) | **Closed** | A non-technical issue closed for its heated tone. No actual code improvement resulted, but it exposed real deficiencies in Windows support |

### Work in Progress

| PR | Status | Progress assessment |
|:---|:---|:---|
| [#150](https://github.com/TinyAGI/tinyclaw/pull/150) | 🟡 **Pending merge** | Continuation of the OpenViking plugin architecture work; rebased onto main from the #149 hardening work |

**Overall progress**: ⭐☆☆☆☆ (1/5) \
No feature merges today; core development is stalled at the PR review stage. Iterating the OpenViking plugin stack is the main near-term technical direction, but it has not landed yet.

---

## 4. Community Hotspots

### 🔥 Top Heat: [#151 - "this shit aint for Windows quit lying"](https://github.com/TinyAGI/tinyclaw/issues/151)

| Metric | Value |
|:---|:---|
| Author | @SiN-Kiliko |
| Comments | 2 |
| Sentiment | 😤 Strongly negative |
| Closed at | 2026-03-01 (about 1 day after creation)|

**The user's complete path of pain**:
```
 defeating package managers
    → installing jq
    → fixing a corrupted settings.json
    → forcing PowerShell to run Linux scripts
    → the scripts demand a nonexistent Linux window manager
    → the error output still shows the "✓" success marker
```

**Ask analysis**:
| Surface ask | Deeper ask |
|:---|:---|
| Stop the false advertising of "Windows support" | Build a real cross-platform testing and documentation system |
| Fix the technical problems | Respect users' time costs and provide an honest platform-support statement |

**Project response**: The issue was closed with no technical response or fix commitment.

---

## 5. Bugs and Stability

| Severity | Problem | Source | Fix PR | Status |
|:---|:---|:---|:---|:---|
| 🔴 **High** | Windows completely unusable: scripts depend on a Linux window manager, and the error-handling logic is flawed (failures still show ✓) | [#151](https://github.com/TinyAGI/tinyclaw/issues/151) | None | ❌ Not acknowledged |
| 🟡 **Medium** | Installation docs don't match actual dependencies (jq, corrupted settings.json) | [#151](https://github.com/TinyAGI/tinyclaw/issues/151) | None | ❌ Not tracked |

**Risk assessment**: The Windows compatibility problem has escalated from "technical debt" to a **trust crisis**. The current handling (closing the issue without a response) may inflame community sentiment.

---

## 6. Feature Requests and Roadmap Signals

| Source | Implied need | Link to existing PRs | Likelihood |
|:---|:---|:---|:---|
| [#151](https://github.com/TinyAGI/tinyclaw/issues/151) user feedback | Native Windows support / clear WSL guidance / platform detection with friendly errors | No direct link | Low (not in official tracking) |
| [#150](https://github.com/TinyAGI/tinyclaw/pull/150) | OpenViking plugin ecosystem expansion | Itself the implementation | High (submitted, awaiting review) |

**Roadmap signal**: The project currently focuses on **hardening the OpenViking plugin architecture** (#149 → #150); platform compatibility is not yet a priority.

---

## 7. User Feedback Summary

### 💔 Pain Points (from [#151](https://github.com/TinyAGI/tinyclaw/issues/151))

| Dimension | Details |
|:---|:---|
| **Time cost** | "defeating package managers" — repeated fights with package managers |
| **Configuration hell** | Manually fixing settings.json; scripts forced to run cross-platform |
| **Misleading feedback** | Failed flows still show the ✓ success marker, causing confusion |
| **Broken trust** | The docs claim Windows support, but the actual experience completely contradicts it |

### 🎯 Usage Scenarios
- **Target users**: Developers who want to deploy an AI assistant on Windows
- **Actual barrier**: Requires Linux-environment knowledge + manual troubleshooting skills, far beyond the advertised ease of use

### 📊 Satisfaction Assessment
- This user: ⭐☆☆☆☆ (extremely dissatisfied, churned)
- The potential Windows user base: high churn risk

---

## 8. Pending Backlog

| PR/Issue | Created | Last updated | Blocking reason | Suggested action |
|:---|:---|:---|:---|:---|
| [#150](https://github.com/TinyAGI/tinyclaw/pull/150) | 2026-02-27 | 2026-02-28 | Awaiting review | ⚠️ **Merge first** — core feature development, waiting 3+ days |
| Issues derived from [#151](https://github.com/TinyAGI/tinyclaw/issues/151) | — | — | The original issue was closed | 🔴 **Open a tracking issue** — log Windows compatibility as a formal bug so that emotional handling doesn't bury the technical debt |

---

## Health Score

| Dimension | Score | Notes |
|:---|:---:|:---|
| Code activity | ⭐⭐☆☆☆ | No merges; development stalled |
| Community response | ⭐☆☆☆☆ | Issue closed with no technical response |
| Version management | ⭐⭐☆☆☆ | Empty release; cadence in doubt |
| Cross-platform support | ⭐☆☆☆☆ | Severe deficiencies untracked |
| **Overall health** | **⭐⭐☆☆☆** | Technical debt accumulating; community trust under strain |

---

> **Analyst's note**: This week the maintenance team is advised to (1) review and merge #150 to restore the development cadence; and (2) set up formal issue tracking for Windows compatibility, or explicitly update the docs to declare the limitation and repair user trust.

</details>

---
*This report was auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*