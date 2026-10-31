# OpenClaw Ecosystem Report 2026-03-02

> Issues: 500 | PRs: 500 | Projects covered: 11 | Generated at: 2026-03-02 00:07 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)

---

## OpenClaw Project Deep-Dive Report

# OpenClaw Project Report | 2026-03-02

---

## 1. Today's Overview

OpenClaw maintained **extremely high activity** today, generating **500 issue updates** (395 opened/active, 105 closed) and **500 PR updates** (450 pending merge, 50 merged/closed) within 24 hours, with no new version released. Community focus centered on **multi-platform stability fixes** (Windows/macOS/Linux), **messaging channel reliability** (Telegram/Signal/Feishu/WhatsApp), and **model integration optimization** (GPT-5.3-Codex, Ollama, Anthropic). The project shows a "fix-intensive" profile, with a large number of PRs targeting edge cases and configuration-management issues, indicating the product is moving from its feature-expansion phase into a **quality-consolidation phase**.

---

## 2. Version Releases

**No new version release**

The previous version `2026.2.27` was released yesterday, and no new version shipped today. The community is still actively reporting on several regressions introduced in `2026.2.26` (loss of macOS Intel support, Dashboard 404, duplicate Feishu plugin configuration).

---

## 3. Project Progress

### Key PRs merged/closed today

| PR | Author | Core Contribution | Impact Assessment |
|:---|:---|:---|:---|
| [#31079](https://github.com/openclaw/openclaw/pull/31079) | @vincentkoc | Added contributor credits missing from the 2026.3.1 changelog | Community governance |
| [#30881](https://github.com/openclaw/openclaw/pull/30881) | @liuxiaopai-ai | Fixed an infinite loop in session replay caused by blank `toolResult` names | **High** - resolves a long-standing stability issue |
| [#30769](https://github.com/openclaw/openclaw/pull/30769) | @kevinWangSheng | Prevented streaming tool-call names from being truncated into empty strings | **High** - preventive fix |
| [#30735](https://github.com/openclaw/openclaw/pull/30735) | @Sid-Qin | Same as above, a duplicate fix (shows parallel community contribution) | - |
| [#30620](https://github.com/openclaw/openclaw/pull/30620) | @Sid-Qin | Normalized tool-call aliases in real time, fixing Kimi/Ollama tool-matching failures | **High** - Chinese-model compatibility |
| [#29710](https://github.com/openclaw/openclaw/pull/29710) | @Sid-Qin | Prefer bundled plugins over duplicate items discovered globally, fixing the Feishu pairing loop | **High** - upgrade experience |
| [#31082](https://github.com/openclaw/openclaw/pull/31082) | @YuzuruS | Mark cron `announce` status as success rather than error when delivery fails | **Medium** - alert noise reduction |
| [#29610](https://github.com/openclaw/openclaw/pull/29610) | @hclsys | Use the correct `msg_type=file` for Feishu video files | **Medium** - channel feature fix |

### Overall Progress Assessment

Today's merged PRs focused on the two major themes of **"tool-call reliability"** and **"configuration/upgrade stability"**, fixing multiple edge cases that caused infinite loops or silent failures. Project quality infrastructure (contributor credits, tightened CI permissions) improved in parallel.

---

## 4. Community Highlights

### Most-discussed Issues

| Rank | Issue | Comments | Core Request | Status |
|:---|:---|:---:|:---|:---|
| 1 | [#3460](https://github.com/openclaw/openclaw/issues/3460) Internationalization (i18n) and localization support | **72** | Global users strongly demand multilingual support, but the maintainer team stated clearly it **currently has no resources for it**; it needs to be community-led | 🔴 Open long-term |
| 2 | [#75](https://github.com/openclaw/openclaw/issues/75) Linux/Windows desktop app | **30** | Users want a native app with feature parity with macOS; 55 👍 shows strong demand | 🔴 Open, labeled `help wanted` |
| 3 | [#16862](https://github.com/openclaw/openclaw/issues/16862) Web UI error: missing scope operator.read | **29** | Permission issue with LAN-bound configuration after upgrading to 2026.2.14 | ✅ Closed |
| 4 | [#7631](https://github.com/openclaw/openclaw/issues/7631) Windows plugin installation fails with spawn EINVAL | **19** | npm child-process invocation issue on Windows | 🔴 Open |
| 5 | [#5871](https://github.com/openclaw/openclaw/issues/5871) CLI extremely slow (17s+) on Raspberry Pi 4B | **16** | Need for performance optimization on low-end ARM devices | 🔴 Open |

### Hotspot Analysis

- **Internationalization (#3460)** became the community's biggest point of tension: 72 comments show global user enthusiasm, but the official "no bandwidth" stance sparked discussion about open source project governance models.
- **Cross-platform desktop app (#75)** is the second-largest feature gap, with Linux/Windows users applying continuous pressure.
- **Windows platform stability** problems broke out in a concentrated wave (related to #7631 and #7631), showing insufficient test coverage on that platform.

---

## 5. Bugs and Stability

### Sorted by Severity

| Severity | Issue | Description | Fix Status |
|:---|:---|:---|:---|
| 🔴 **P0-Regression** | [#28877](https://github.com/openclaw/openclaw/issues/28877) | macOS 2026.2.26 is arm64-only; Intel Macs crash (2026.2.25 shipped a universal binary) | 🔧 Urgent fix pending |
| 🔴 **P0-Broken functionality** | [#14215](https://github.com/openclaw/openclaw/issues/14215) | Browser control completely broken (both the Chrome extension and managed configuration fail) | 🔧 Diagnosis pending |
| 🟡 **P1-Feature degradation** | [#29525](https://github.com/openclaw/openclaw/issues/29525) | Dashboard UI 404 (2026.2.26) | 🔧 Pending fix |
| 🟡 **P1-Configuration loss** | [#21009](https://github.com/openclaw/openclaw/issues/21009) | Mac App overwrites openclaw.json and deletes gateway.auth, causing a crash loop with LAN binding | 🔧 Pending fix |
| 🟡 **P1-Channel failure** | [#29420](https://github.com/openclaw/openclaw/issues/29420) | Discord WebSocket reconnect loses events (seq gap); mention messages are lost | ✅ Closed |
| 🟡 **P1-Model compatibility** | [#18282](https://github.com/openclaw/openclaw/issues/18282) | GPT-5.2 reasoning item causes a 400-error loop | 🔧 Pending fix |
| 🟢 **P2-Edge case** | [#30723](https://github.com/openclaw/openclaw/issues/30723) | Tool I/O lost in Telegram DMs | ✅ Closed |

### Fix PRs in progress

- [#31083](https://github.com/openclaw/openclaw/pull/31083) - GPT-5.3-Codex API key routing fix
- [#31081](https://github.com/openclaw/openclaw/pull/31081) - Version detection prefers module metadata over stale environment variables
- [#31077](https://github.com/openclaw/openclaw/pull/31077) - Telegram reply-mode fix

---

## 6. Feature Requests and Roadmap Signals

### Key feature requests from users

| Issue | Feature | Feasibility Signal | Likelihood |
|:---|:---|:---|:---:|
| [#3460](https://github.com/openclaw/openclaw/issues/3460) | Full i18n/l10n framework | Community PRs exist but lack official coordination | ⭐⭐⭐ Medium |
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows desktop app | Large tech-stack divergence; needs an Electron/Tauri approach | ⭐⭐ Low |
| [#10010](https://github.com/openclaw/openclaw/issues/10010) | Agent Teams - parallel agent coordination | Inspired by Claude Code; fits the existing `sessions_spawn` foundation | ⭐⭐⭐⭐ High |
| [#17700](https://github.com/openclaw/openclaw/issues/17700) | Atomic configuration management + crash rollback | Production-critical need with a detailed technical proposal | ⭐⭐⭐⭐ High |

### Roadmap Signals

- **Agent Teams (#10010)** is most likely to make the next release: it fits the existing architecture well and a competitor (Claude Code) has already validated the demand.
- **Hardened configuration management (#17700)** is flagged as "the No.1 cause of gateway outages" and is expected to be prioritized.
- **i18n** needs a community-led model; the maintainers may provide the framework but will not take on translation maintenance.

---

## 7. User Feedback Summary

### Real Pain Points

> *"After the upgrade Feishu is completely unusable; every time it starts

---

## Ecosystem Cross-Comparison

# Personal AI Assistant Open Source Ecosystem Comparison Report
**Analysis date: 2026-03-02**

---

## 1. Ecosystem Landscape

The open source ecosystem for personal AI assistants/autonomous agents is going through a **collective transition from feature expansion to quality consolidation**. Leading projects (OpenClaw, ZeroClaw) have entered a "fix-intensive" stage, handling 400-500 issues/PRs per day and focusing on tool-call reliability, configuration stability, and multi-platform compatibility; mid-sized projects (PicoClaw, IronClaw, LobsterAI) are catching up quickly, building differentiation on enterprise features (multi-tenancy, quota management, audit logs); emerging projects (ZeptoClaw, TinyClaw, EasyClaw) show a "single-maintainer-driven" or "maintenance-response" profile, with clearly stratified community participation and code-iteration density. Overall technical directions are converging on: **a unified provider compatibility layer, WASM/MCP plugin ecosystems, and session-level isolation architecture**, while internationalization, cross-platform desktop apps, and cost control remain common weaknesses.

---

## 2. Activity Comparison by Project

| Project | Issues (new/closed) | PRs (pending/merged) | Version Release | Health Assessment |
|:---|:---|:---|:---|:---|
| **OpenClaw** | 395/105 | 450/50 | None | 🔶 Extremely high activity, heavy backlog pressure, quality-consolidation phase |
| **ZeroClaw** | 23/27 | 22/28 | None | 🟢 Rapid-iteration phase, high merge rate, rising production readiness |
| **PicoClaw** | 16/7 | 46/25 | None | 🟢 High activity, dense security fixes, mid-architecture refactor |
| **IronClaw** | ~17 closed | 36/14 | None | 🔶 Heavy maintenance, notable PR backlog, enterprise features pending unlock |
| **LobsterAI** | 8/0 | 8 merged | **v0.1.23** | 🟡 Release window, issue digestion lagging output |
| **ZeptoClaw** | 0/9 | 1/9 | None | 🟢 Single maintainer iterating at high speed, zero community discussion |
| **TinyClaw** | 2/0 | 1/0 | None | 🟡 Moderate activity, critical architecture-upgrade period |
| **EasyClaw** | 2/0 | 0/0 | **v1.5.13** | 🔴 Maintenance-response period, feature iteration stalled |
| NanoBot | — | — | — | ⚫ Summary generation failed |
| NanoClaw | — | — | — | ⚫ Summary generation failed |
| CoPaw | — | — | — | ⚫ Summary generation failed |

> **Note**: OpenClaw's data volume is **10-20x** that of the other projects, making it the ecosystem's absolute core reference.

---

## 3. OpenClaw's Position in the Ecosystem

| Dimension | OpenClaw Performance | Ecosystem Comparison |
|:---|:---|:---|
| **Community scale** | 500 issues + 500 PRs/day, clear leader | ZeroClaw is only **10%** of it, PicoClaw **5%** |
| **Technical maturity** | Quality-consolidation phase: fixing edge cases, configuration management, regressions | ZeptoClaw/IronClaw are in the feature-delivery phase, LobsterAI in the experience-polish phase |
| **Architecture openness** | Multi-platform native (Windows/macOS/Linux), multi-channel (Telegram/Signal/Feishu/WhatsApp), multi-model (GPT-5.3/Ollama/Anthropic) | ZeroClaw emphasizes WASM plugins + the MCP ecosystem; IronClaw bets on a WASM tool marketplace; PicoClaw focuses on embedded/edge scenarios |
| **Core weaknesses** | **Internationalization (#3460, 72 comments, officially declined)**, cross-platform desktop app (#75, 55 👍, labeled help wanted) | ZeroClaw already supports native Discord buttons and BlueBubbles iMessage; ZeptoClaw has vision input on all channels |
| **Governance model** | Maintainer-led + parallel community contributions (e.g. #30735/#30769 duplicate fixes) | ZeptoClaw is purely maintainer-driven; EasyClaw's maintainer response lags |

**Key difference**: OpenClaw is **the only full-stack project covering both consumer and enterprise scenarios**, but its "no resources for i18n" stance exposes the universal tension of sustainable open source governance — the trade-off between feature breadth and maintenance depth.

---

## 4. Common Technical Directions

| Technical Direction | Projects Involved | Specific Needs | Urgency |
|:---|:---|:---|:---:|
| **Session/thread-level isolation** | TinyClaw (#144→#152), OpenClaw (implied by multi-channel stability) | End cross-platform context crosstalk and privacy leaks | ⭐⭐⭐⭐⭐ |
| **Cost control and quota management** | ZeroClaw (#2269), ZeptoClaw (#210), PicoClaw (#295) | per-provider usage limits, automatic downgrade/upgrade routing | ⭐⭐⭐⭐⭐ |
| **WASM/MCP plugin ecosystem** | ZeroClaw (#1380, #1365), IronClaw (#387, #439), LobsterAI (#198) | external MCP server support, WASM tool auth UX, graphical configuration | ⭐⭐⭐⭐☆ |
| **Security sandbox and auditing** | PicoClaw (#964, #195, #962), ZeroClaw (lock-poisoning recovery), ZeptoClaw (#195) | Shell command interception, credential-leak protection, operation-trail logging | ⭐⭐⭐⭐☆ |
| **Enterprise deployment presets** | ZeptoClaw (#211), IronClaw (#348-351), ZeroClaw (multi-tenancy) | zero-code Azure/Bedrock onboarding, multi-tenant isolation, LDAP/SSO | ⭐⭐⭐⭐☆ |
| **Voice/multimodal input** | ZeroClaw (Whisper acceleration), ZeptoClaw (#202), PicoClaw (#945/#947 fixes) | local STT, all-channel vision input, voice-message reliability | ⭐⭐⭐☆☆ |
| **Configuration management and hot reload** | OpenClaw (#17700, #29710), PicoClaw (#949), LobsterAI (#198) | atomic configuration, crash rollback, runtime model switching | ⭐⭐⭐⭐☆ |

**Signal**: **Cost control** and **enterprise isolation** are shifting from "differentiating features" to **table stakes** — ZeptoClaw merged a quota system plus multi-cloud presets within a single day, showing how white-hot this race has become.

---

## 5. Differentiation Analysis

| Project | Functional Focus | Target Users | Technical Architecture |
|:---|:---|:---|:---|
| **OpenClaw** | Full-stack generalist: multi-channel × multi-model × multi-platform | Tech enthusiasts + early enterprise users | Mostly Node.js, plugin-based and config-driven, the most complete ecosystem |
| **ZeroClaw** | Production-ready: HITL interactions, cost optimization, WASM plugins | Production deployers, multi-tenant scenarios | Rust core, WASM runtime, native MCP support |
| **PicoClaw** | Edge/embedded: security sandbox, lightweight runtime, hardware agent | IoT developers, edge-computing scenarios | Mostly Go, layered Channel-Agent architecture, armv6 support |
| **IronClaw** | WASM tool marketplace, programmatic invocation, setup wizard | WASM tool developers, heavy CLI users | Rust + WASM first, Registry ecosystem, multi-tenant architecture pending unlock |
| **LobsterAI** | Chinese localization, Skill ecosystem, zero-dependency deployment | Chinese non-technical users, office automation | Electron wrapper, bundled Python on Windows, NetEase backing |
| **ZeptoClaw** | Enterprise gateway: multi-cloud presets, quota management, OAuth | Enterprise IT admins, multi-tenant SaaS | Rust, unified backend through an OpenAI-compatible layer, single maintainer |
| **TinyClaw** | Minimalist multi-platform: Claude/Codex agents | Individual developers, rapid prototyping | Python, thread-level isolation architecture being upgraded |
| **EasyClaw** | Clean conversational experience | Early adopters, productivity-oriented users | Electron, minimal features, risk of stalled iteration |

**Key insight**: The tech stacks split into **Rust (ZeroClaw, IronClaw, ZeptoClaw) vs Node.js/Go/Python (OpenClaw, PicoClaw, TinyClaw, LobsterAI, EasyClaw)**; the Rust camp bets on performance, safety, and WASM, while the traditional-stack camp pursues ecosystem velocity and developer friendliness.

---

## 6. Community Heat and Maturity Tiers

| Tier | Projects | Characteristics | Key Metrics |
|:---|:---|:---|:---|
| **L1: Ecosystem core** | OpenClaw | Quality-consolidation phase, governance tension surfacing | 500 issues+PRs/day, the i18n decline sparking discussion |
| **L2: Rapid iteration** | ZeroClaw, PicoClaw, ZeptoClaw | Dense feature delivery, production readiness jumping | 20-50 issues+PRs/day, merge rate >50% |
| **L3: Release window** | LobsterAI, IronClaw | Critical period for version releases or enterprise feature unlocks | v0.1.23 released, 36 PRs pending merge |
| **L4: Architecture upgrade** | TinyClaw | Core refactor deciding the long-term direction | #152 session-isolation PR pending review, Windows compatibility dispute |
| **L5: Maintenance response** | EasyClaw | Feature iteration stalled, dependent on the maintainer's return | 0 PR activity, high-value user feedback awaiting response |
| **L6: Missing data** | NanoBot, NanoClaw, CoPaw | Cannot be assessed | — |

**Risk warning**: EasyClaw's "high-emotional-value users + zero technical response" combination is the classic pattern of an early project losing seed users; if IronClaw's 36-PR backlog persists, it could block the launch of key enterprise features such as multi-tenancy.

---

## 7. Trend Signals Worth Watching

| Trend | Evidence | Reference Value for Developers |
|:---|:---|:---|
| **The shift from "configuration as code" to "configuration as product"** | OpenClaw #17700, LobsterAI #198, PicoClaw #949 | Graphical configuration UIs, runtime hot reload, and atomic rollback will become the user-experience dividing line |
| **Cost awareness moving from "an afterthought" to "an architecture-level design"** | ZeroClaw #2269, ZeptoClaw #210, PicoClaw #295 | New projects should build in per-provider quotas, automatic downgrade routing, and token-efficiency governance |
| **WASM as the default choice for plugin/tool ecosystems** | ZeroClaw #1365, IronClaw's WASM tool marketplace, ZeptoClaw's security sandbox | Investing in WASM runtime capabilities (resource limits, hot loading, cross-language bindings) is key to ecosystem expansion |
| **Session isolation shifting from "advanced feature" to "basic security"** | TinyClaw #152, OpenClaw multi-channel stability, ZeroClaw multi-tenancy | In multi-platform deployments, thread-level session isolation is the baseline for privacy and reliability |
| **Chinese model integrations becoming "standard equipment"** | ZeptoClaw DeepSeek+Kimi, OpenClaw Kimi/Ollama compatibility, PicoClaw glm-4.7 | OpenAI-compatible layers should reserve handling paths for Chinese models' special parameters (reasoning items, tool-matching aliases) |
| **Paradigm divergence in i18n governance models** | OpenClaw #3460 "community-led" vs other projects' silence | Establishing an i18n framework early (even if the officials don't maintain translations) reduces later community tension |
| **The "lobster" nickname forming category mindshare** | EasyClaw user feedback | Category nicknames may emerge in the Chinese market; watch the localization strategies of LobsterAI/EasyClaw and similar projects |

---

**Analyst's closing note**: The 2026-03-02 ecosystem snapshot shows the personal AI assistant track moving from a "feature race" into a dual-track stage of "quality consolidation + enterprise readiness". OpenClaw's governance tension, ZeroClaw/ZeptoClaw's production-grade feature sprint, and the technical convergence on WASM/cost control/session isolation together point to a more mature, more stratified competitive landscape. For newcomers, **differentiated scenarios (edge computing, vertical industries, specific audiences)** offer better survival value than chasing the full stack.

---

## Detailed Reports for Same-Track Projects

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Report | 2026-03-02

## 1. Today's Overview

ZeroClaw showed extremely high development activity today: **50 issue updates (23 opened/active, 27 closed)** and **50 PR updates (22 pending merge, 28 merged/closed)** within 24 hours indicate the project is in a rapid-iteration phase. Core progress concentrated on **multi-channel interaction upgrades** (native Discord/Telegram approval buttons, rich BlueBubbles iMessage features), **smarter memory systems** (time decay, pre-compression persistence), and **production-grade stability hardening** (lock-poisoning recovery, WebSocket subprotocol negotiation). Community discussion of **cost control** and **enterprise deployment** (multi-tenancy, CRM scenarios) heated up markedly, showing the user base expanding from early adopters toward production use cases.

---

## 2. Version Releases

**No new version release** — no release shipped today, but the large number of merged PRs suggests the team may be accumulating changes for a v0.2.0 or v0.1.9 release.

---

## 3. Project Progress

### Notable merged/closed PRs

| PR | Author | Core Contribution | Status |
|:---|:---|:---|:---|
| [#2447](https://github.com/zeroclaw-labs/zeroclaw/pull/2447) | @theonlyhennygod | **Fixed stale system timestamps**: the "current time" now refreshes every turn in long sessions, fixing time-perception errors in multi-turn conversations | ✅ Merged |
| [#2448](https://github.com/zeroclaw-labs/zeroclaw/pull/2448) | @theonlyhennygod | **Native Discord approval buttons**: replaced text commands with the Components API, a major interaction-experience upgrade | ✅ Merged |
| [#2449](https://github.com/zeroclaw-labs/zeroclaw/pull/2449) | @theonlyhennygod | **Default configuration improvements**: expanded the safe-command allowlist to match real workflow needs, reducing friction for new users | ✅ Merged |
| [#2457](https://github.com/zeroclaw-labs/zeroclaw/pull/2457) | @maxtongwang | **Faster local Whisper transcription**: BlueBubbles voice memo transcription dropped from 30-90s to near real time using whisper.cpp | ✅ Merged |
| [#1954](https://github.com/zeroclaw-labs/zeroclaw/pull/1954) | @reidliu41 | **WebSocket subprotocol negotiation**: fixed Agent Chat connection failures | ✅ Merged |
| [#1365](https://github.com/zeroclaw-labs/zeroclaw/pull/1365) | @gh-xj | **WASM plugin runtime (Part 2/2)**: completed the plugin execution bridge, resource limits, and documentation; plugin-ecosystem infrastructure is ready | ✅ Merged |

**Overall progress assessment**: today's merged PRs covered **user experience** (3), **performance** (1), **stability** (2), and **ecosystem expansion** (1); the project took a substantive step toward production readiness, especially in native multi-channel interactions and local AI inference acceleration.

---

## 4. Community Highlights

### Most-discussed Issues

| Issue | Comments | Core Request | Analysis |
|:---|:---|:---|:---|
| [#1380](https://github.com/zeroclaw-labs/zeroclaw/issues/1380) | 11 comments, 👍8 | **External MCP server support** | The community's strongest request: support npm/remote MCP servers to expand the tool ecosystem. Closed, but the high vote count shows an official roadmap response is needed |
| [#2269](https://github.com/zeroclaw-labs/zeroclaw/issues/2269) | 7 comments | **Token consumption and cost management** | Core pain point for production deployments: running everything on a high-end model costs too much; needs tiered routing (lightweight models for email/notifications, high-end models for complex tasks) |
| [#2388](https://github.com/zeroclaw-labs/zeroclaw/issues/2388) | 6 comments | **Deep agent-team orchestration** | Enterprise-grade need: testable orchestration paths for complex tasks, including token-efficiency governance and topology benchmarks |
| [#1865](https://github.com/zeroclaw-labs/zeroclaw/issues/1865) | 5 comments | **Telegram HITL inline buttons** | Appeared alongside the Discord button PR, showing consistent multi-channel interactions are a widespread expectation |
| [#2325](https://github.com/zeroclaw-labs/zeroclaw/issues/2325) | 5 comments | **Feishu channel compilation issue** | Caused by the missing `channel-lark` feature flag, reflecting the configuration complexity that feature modularization brings |

**Underlying demand**: the community is shifting from "it runs" to "it's production-ready" — cost control, enterprise integration (Feishu/Discord/Telegram), and extensible architecture (MCP/WASM plugins) are the focus.

---

## 5. Bugs and Stability

| Severity | Issue | Description | Fix PR | Status |
|:---|:---|:---|:---|:---|
| **S1 - Workflow blocked** | [#2325](https://github.com/zeroclaw-labs/zeroclaw/issues/2325) | Feishu channel build missing the `channel-lark` feature flag | To be confirmed | ⚠️ Closed, fix needs verification |
| **S1 - Workflow blocked** | [#2405](https://github.com/zeroclaw-labs/zeroclaw/issues/2405) | NVIDIA NIM (minimax-m2.5) tool calls return 400 errors | To be confirmed | ⚠️ Closed |
| **S1 - Workflow blocked** | [#2168](https://github.com/zeroclaw-labs/zeroclaw/issues/2168) | Web Dashboard Agent tab WebSocket connection failure (stale assets) | [#1954](https://github.com/zeroclaw-labs/zeroclaw/pull/1954) | ✅ Fixed |
| **S2 - Degraded behavior** | [#2411](https://github.com/zeroclaw-labs/zeroclaw/issues/2411) | Anthropic provider's empty text blocks not filtered | To be confirmed | ⚠️ Closed |
| **S2 - Degraded behavior** | [#2367](https://github.com/zeroclaw-labs/zeroclaw/issues/2367) | System-prompt timestamps stale across turns | [#2447](https://github.com/zeroclaw-labs/zeroclaw/pull/2447) | ✅ Fixed |
| **S2 - Degraded behavior** | [#2391](https://github.com/zeroclaw-labs/zeroclaw/issues/2391) | MCP HTTP transport missing the `Accept` header, causing 406/415 | To be confirmed | ⚠️ Closed |

**Stability outlook**: two S2 issues were fixed today; S1 issues mostly relate to specific provider/channel configurations, and overall core-runtime stability is good. Pending PRs include key hardening:
- [#2462](https://github.com/zeroclaw-labs/zeroclaw/pull/2462) - Lock-poisoning recovery mechanism (avoids process crashes)
- [#2454](https://github.com/zeroclaw-labs/zeroclaw/pull/2454) - web_fetch redirect fix

---

## 6. Feature Requests and Roadmap Signals

| Feature Request | Issue | Related PR | Likelihood | Notes |
|:---|:---|:---|:---|:---|
| **External MCP server support** | [#1380](https://github.com/zeroclaw-labs/zeroclaw/issues/1380) | None | 🔶 High | 11 comments + 8 votes, core to ecosystem expansion |
| **Tiered token-cost routing** | [#2269](https://github.com/zeroclaw-labs/zeroclaw/issues/2269) | [#2373](https://github.com/zeroclaw-labs/zeroclaw/pull/2373) | 🔶 High | The PR already provides a provider-agnostic max-token continuation strategy |
| **Agent lifecycle state machine** | [#2308](https://github.com/zeroclaw-labs/zeroclaw/issues/2308) | None | 🔶 Medium | Essential for daemon/monitoring; in RFI stage |
| **Chat-based CRM scenarios** | [#2274](https://github.com/zeroclaw-labs/zeroclaw/issues/2274) | None | 🔶 Medium | Productionization signal; needs a lightweight runtime + multi-tenancy |
| **Agent team orchestration** | [#2388](https://github.com/zeroclaw-labs/zeroclaw/issues/2388) | [#2420](https://github.com/zeroclaw-labs/zeroclaw/pull/2420) | 🟢 In development | The PR provides team/sub-agent separation with runtime hot configuration |
| **Feishu document operation tools** | Implied need | [#1853](https://github.com/zeroclaw-labs/zeroclaw/pull/1853) | 🟢 In development | 13-operation Feish

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Report | 2026-03-02

## 1. Today's Overview

PicoClaw stayed **highly active** today, generating **23 issue updates** (16 opened/active, 7 closed) and **71 PR updates** (46 pending merge, 25 merged/closed) within 24 hours. The project's core focus is on **security sandbox fixes** (shell-guard-related issues #964, #797, #386 appearing in bursts), **multi-provider compatibility** (OpenRouter, Anthropic, Groq, etc.), and **voice feature regression fixes** (#945/#947). The Channel system refactor (#621) reached 83% and was closed, while the Agent system refactor (#772) is underway. Overall health is good, but security-related bugs need priority handling.

---

## 2. Version Releases

**No new version release**

---

## 3. Project Progress

### Notable merged/closed PRs

| PR | Author | Core Contribution | Project Impact |
|:---|:---|:---|:---|
| [#833](https://github.com/sipeed/picoclaw/pull/833) | @lucamartinetti | **Fixed web_fetch tool content return** — restored `ForLLM` from a summary string to the actual extracted text | Fixed a key v0.2.0 regression, restoring the LLM's ability to fetch web content |
| [#896](https://github.com/sipeed/picoclaw/pull/896) | @keithy | **Environment variable configuration support** — added `PICOCLAW_CONFIG` and `PICOCLAW_HOME` | Improves deployment flexibility for containerized/multi-instance scenarios |
| [#970](https://github.com/sipeed/picoclaw/pull/970) | @dj-oyu | **Fixed heartbeat task display glitch** — resolved garbled Telegram status bubbles | Better UX for async tasks |
| [#969](https://github.com/sipeed/picoclaw/pull/969) | @dj-oyu | **Upstream merge** — resolved 65 file conflicts, integrating the Channel refactor, Launcher TUI, and armv6 support | Stays in sync with upstream and lays the v0.3.0 architectural foundation |
| [#686](https://github.com/sipeed/picoclaw/pull/686) | @dimensi | **Deepgram STT provider** — extracted a `Transcriber` interface and added Deepgram support | Decouples the voice module, paving the way for the #945 fix |
| [#780](https://github.com/sipeed/picoclaw/pull/780) | @brenzel | **Fixed curl URL calls being falsely blocked** — improved `guardCommand` argument parsing | Resolves security-sandbox false positives (later strengthened by #968) |
| [#962](https://github.com/sipeed/picoclaw/pull/962) | @vvr3ddy | **Audit log enhancements** — records Agent tool-call trails | Meets enterprise compliance needs |

### Milestone closed

- **[#621](https://github.com/sipeed/picoclaw/issues/621) Channel system refactor** — 83% complete (10/12 phases), core architecture merged, remaining phases moved to later iterations

---

## 4. Community Highlights

### Most-discussed Issues

| Issue | Comments | Hotspot Analysis |
|:---|:---|:---|
| [#901](https://github.com/sipeed/picoclaw/issues/901) | 11 comments | **OpenRouter "free" model configuration pain** — users cannot directly use `model: "free"`; the community has submitted fix PR [#954](https://github.com/sipeed/picoclaw/pull/954) mapping it to `openrouter/auto` |
| [#295](https://github.com/sipeed/picoclaw/issues/295) | 9 comments | **Smart model routing roadmap** — a core cost/performance optimization need; users strongly expect automatic downgrade/upgrade policies |
| [#621](https://github.com/sipeed/picoclaw/issues/621) | 5 comments | Channel refactor progress tracking; the high 👍 count (4) reflects community attention to architectural stability |
| [#671](https://github.com/sipeed/picoclaw/issues/671) | 4 comments | `gateway status` mistakenly spawns extra worker processes, hurting Discord stability |

**Core requests**: lower model usage costs (#295), simpler provider configuration (#901), better system stability (#671, #621)

---

## 5. Bugs and Stability

| Severity | Issue | Description | Status |
|:---|:---|:---|:---|
| 🔴 **Critical** | [#972](https://github.com/sipeed/picoclaw/issues/972) | **Sub-agent credential leak** — configuration mismatch causes recursive failures; CLI/channel output exposes sensitive information | 🆕 Reported today, no fix PR |
| 🔴 **Critical** | [#945](https://github.com/sipeed/picoclaw/issues/945) | **Voice completely broken** — v0.2.0 removed `voice` package imports, breaking voice messages | 🟡 Fix PR [#947](https://github.com/sipeed/picoclaw/pull/947) pending merge |
| 🟠 **High** | [#964](https://github.com/sipeed/picoclaw/issues/964) | **Security sandbox falsely blocks `/dev/null` redirection** — under restricted-workspace mode, models like glm-4.7 cannot be used | 🟡 Fix PR [#967](https://github.com/sipeed/picoclaw/pull/967) pending merge |
| 🟠 **High** | [#797](https://github.com/sipeed/picoclaw/issues/797) | **`guardCommand` decision-logic bug** — security guard false positives | 🟡 Related PR [#968](https://github.com/sipeed/picoclaw/pull/968) pending merge |
| 🟠 **High** | [#794](https://github.com/sipeed/picoclaw/issues/794) | **Codex API 400 errors** — `gpt-5.3-codex` calls fail under headless-device auth mode | 🟡 Fix PR [#898](https://github.com/sipeed/picoclaw/pull/898) pending merge |
| 🟡 **Medium** | [#966](https://github.com/sipeed/picoclaw/issues/966) | **Qwen 3.5 thinking model returns empty content** — reasoning consumes all tokens, leaving no output | 🆕 Reported today, no fix PR |
| 🟡 **Medium** | [#965](https://github.com/sipeed/picoclaw/issues/965) | **Incomplete block-device protection** — only intercepts `/dev/sd*`, missing `/dev/mmcblk*`, `/dev/nvme*` | 🆕 Reported today, no fix PR |
| 🟡 **Medium** | [#958](https://github.com/sipeed/picoclaw/issues/958) | **Ollama model-not-found error** — `ModelName` not set correctly during configuration migration | 🟡 Fix PR [#963](https://github.com/sipeed/picoclaw/pull/963) pending merge |

---

## 6. Feature Requests and Roadmap Signals

| Feature Request | Issue | Feasibility Assessment | Version Signal |
|:---|:---|:---|:---|
| **Smart model routing** | [#295](https://github.com/sipeed/picoclaw/issues/295) | High — the architecture already supports multiple models; a routing layer needs to be added | **v0.3.0 candidate** |
| **Self-upgrade support** | [#618](https://github.com/sipeed/picoclaw/issues/618) | Medium — needs multi-platform package-manager integration (deb/winget/opkg) | Long-term roadmap |
| **Telegram custom API server** | [#880](https://github.com/sipeed/picoclaw/issues/880) | High — configuration extension; essential in regions like Iran | **Likely soon** |
| **Configurable tool execution timeout** | [#906](https://github.com/sipeed/picoclaw/issues/906) | High — the hardcoded 60-second limit affects long tasks | **v0.2.1 candidate** |
| **Build-time feature trimming** | [#923](https://github.com/sipeed/picoclaw/issues/923) | Medium — embedded-device need; requires rebuilding the build system | Long-term roadmap |
| **File attachment support on all platforms** | [#948](https://github.com/sipeed/picoclaw/issues/948) | High — text-only today; a UX bottleneck | **v0.3.0 candidate** |
| **Comprehensive security framework** | [#782](https://github.com/sipeed/picoclaw/issues/782) | Medium — audit-log PR [#962](https://github.com/sipeed/picoclaw/pull/962) merged; needs extensions for secrets management and input validation | Phased delivery |
| **Runtime model switching** | [#949](https://github.com/sipeed/picoclaw/pull/949) | High — PR submitted, implementing the Telegram `/model` command | **Very likely in v0.2.1** |

---

## 7. User Feedback Summary

### Pain points
- **High configuration complexity**: OpenRouter "free" model and local Ollama model configuration are unintuitive (#901, #958)
- **Overly restrictive security sandbox**: `/dev/null` redirection and curl URL calls falsely blocked (#964, #797, #386)
- **Feature regressions**: v0.2.0 voice completely broken (#945), web_fetch returning summaries instead of content (#833)
- **Poor async task feedback**: heartbeat task display garbled (#970, fixed)

### Use cases
- **Chinese developers**: want Baidu browser/search integration (#266, marked wontfix, pivoting to a generic approach)
- **Network-restricted regions** (Iran, China): Telegram custom API server is essential (#880)
- **Embedded/edge devices**: need smaller builds (#923), armv6 support (merged in #969)

### Satisfaction
- Transparent Channel refactor progress (#621 with high 👍)
- Multi-STT provider support (Deepgram #686) well received

---

## 8. Pending Backlog

| Type | Item | Created | Risk |
|:---|:---|:---|:---|
| **Roadmap issue** | [#772](https://github.com/sipeed/picoclaw/issues/772) Agent system refactor | 2026-02-25 | Depends on the Channel refactor; avoid delays like those seen with #621 |
| **Long-term feature** | [#618](https://github.com/sipeed/picoclaw/issues/618) self-upgrade support | 2026-02-22 | Security-critical; raised repeatedly by the community; consider raising priority |
| **PR pending merge** | [#967](https://github.com/sipeed/picoclaw/pull/967) security sandbox fix | Today | Blocks mainstream models like glm-4.7; review within 24h recommended |
| **PR pending merge** | [#947](https://github.com/sipeed/picoclaw/pull/947) voice fix | Today | Core v0.2.0 feature regression; prioritize merging |
| **Critical bug** | [#972](https://github.com/sipeed/picoclaw/issues/972) credential leak | Today | **Security risk, needs immediate response** |

---

*This report is generated from public GitHub data, time range: 2026-03-01 00:00 - 2026-03-01 23:59 UTC*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Report | 2026-03-02

## 1. Today's Overview

IronClaw was in **heavy-maintenance mode** today: 17 issues closed and 14 PRs handled within 24 hours, but 36 PRs remain pending merge — significant backlog pressure. Community activity concentrated on two themes: **channel stability** (Telegram, Slack, Tailscale) and the **setup wizard experience**. Core contributor @zmanian drove fixes for 8 issues, showing a concentrated push on the setup flow and WASM channels. The multi-tenant architecture PR trilogy (#348/#349/#351) is still waiting to be merged, making it the critical path blocking the project's architectural upgrade.

---

## 2. Version Releases

**No new version release**

---

## 3. Project Progress

### Important issues closed today (17)

| Theme | Count | Representative Issues | Progress Notes |
|:---|:---|:---|:---|
| **Setup wizard robustness** | 5 | [#415](https://github.com/nearai/ironclaw/issues/415), [#416](https://github.com/nearai/ironclaw/issues/416), [#417](https://github.com/nearai/ironclaw/issues/417), [#418](https://github.com/nearai/ironclaw/issues/418), [#419](https://github.com/nearai/ironclaw/issues/419) | Added PostgreSQL version detection, pgvector pre-checks, Docker autostart guidance, Cloudflare binary verification, conflicting-service detection |
| **Channel stability** | 4 | [#392](https://github.com/nearai/ironclaw/issues/392), [#393](https://github.com/nearai/ironclaw/issues/393), [#394](https://github.com/nearai/ironclaw/issues/394), [#413](https://github.com/nearai/ironclaw/issues/413) | Persistent Telegram activation, Secrets-scan infinite-loop fix, automatic Tailscale tunnel establishment, Slack auth injection fix |
| **Data and connectivity** | 3 | [#363](https://github.com/nearai/ironclaw/issues/363), [#358](https://github.com/nearai/ironclaw/issues/358), [#344](https://github.com/nearai/ironclaw/issues/344) | PostgreSQL TLS support, credential cleanup on extension uninstall, Ollama embedding model configuration |
| **Code quality** | 2 | [#338](https://github.com/nearai/ironclaw/issues/338), [#330](https://github.com/nearai/ironclaw/issues/330) | Clippy complexity lints, structured error types |
| **Others** | 3 | [#400](https://github.com/nearai/ironclaw/issues/400), [#406](https://github.com/nearai/ironclaw/issues/406), [#420](https://github.com/nearai/ironclaw/issues/420) | Model-name truncation fix, Discord/WhatsApp build scripts, zsh completion compatibility |

**Key architectural progress**: the multi-tenant PR trilogy (#348/#349/#351) is still pending merge; the series introduces tiered memory, per-user workspace isolation, and per-user authentication, and is the core implementation of Issue #59. Of the 36 pending PRs, this series accounts for 3 XL-sized changes that, once merged, will meaningfully improve enterprise deployment capability.

---

## 4. Community Highlights

### High-discussion topics

| Issue | Comments | Hotspot Analysis |
|:---|:---|:---|
| [#387 GoogleCalendar WASM tool auth failure](https://github.com/nearai/ironclaw/issues/387) | **7** | **The auth UX bottleneck of the WASM tool ecosystem**. Users hold a `credentials.json` but don't know how to use it with `ironclaw tool auth`, reflecting a serious lack of WASM tool documentation and CLI guidance. The issue has been active for 4 days with no core maintainer response, risking churn among early adopters |
| [#394 Tailscale tunnel not established automatically](https://github.com/nearai/ironclaw/issues/394) | 2 | Closed. Users expect a "zero-config tunnel" vs the reality of manually running `tailscale funnel` — a product expectation-management issue |
| [#352 Automated QA system](https://github.com/nearai/ironclaw/issues/352) | 1 | Long-term architecture topic. A 4-layer test plan built from 40 historical bugs (schema validation → integration tests → E2E → chaos testing), echoing today's flood of channel bugs — implementing it earlier could have avoided #393's infinite loop and #392's state loss |

### Insight into demands
- **Immediate pain point**: the "last mile" auth experience of WASM tools (GoogleCalendar, Gmail, etc.)
- **Deeper demand**: the reliability leap from "it runs" to "production-ready", which needs automated testing as a safety net

---

## 5. Bugs and Stability

### Sorted by severity

| Severity | Issue | Status | Impact | Fix PR |
|:---|:---|:---|:---|:---|
| **🔴 High** | [#393 Telegram Secrets scan infinite loop](https://github.com/nearai/ironclaw/issues/393) | ✅ Closed | Pasting an API key triggers infinite error retries; the channel must be disabled to stop it | Merged |
| **🔴 High** | [#443 Telegram group messages unfiltered](https://github.com/nearai/ironclaw/issues/443) | 🆕 New | With `owner_id: null`, it responds to all users' messages — unauthorized access risk | None |
| **🟡 Medium** | [#448 Telegram bot setup error](https://github.com/nearai/ironclaw/issues/448) | 🆕 New | Configuration screenshot shows an anomaly; the specific error is pending diagnosis | None |
| **🟡 Medium** | [#439 Registry update workflow failure](https://github.com/nearai/ironclaw/issues/439) | 🆕 New | **Blocks WASM channel/tool installation**; GitHub branch-protection rules break CI | None |
| **🟡 Medium** | [#268 tool schema normalization issues](https://github.com/nearai/ironclaw/issues/268) | Active | OpenAI-compatible model calls fail, affecting gpt-4o/gpt-5.1 users | None |
| **🟢 Low** | [#387 GoogleCalendar auth](https://github.com/nearai/ironclaw/issues/387) | Active | The feature works but the UX is broken | None |

### Stability assessment
- **Today's fix rate**: 17/23 issues closed (74%), but 3 new high/medium-priority issues
- **Blocking risk**: the #439 Registry workflow failure directly hinders WASM ecosystem expansion and needs urgent handling

---

## 6. Feature Requests and Roadmap Signals

| Direction | Signal Source | Likelihood | Basis |
|:---|:---|:---|:---|
| **Multi-tenancy/enterprise isolation** | #348/#349/#351 PR trilogy | ⭐⭐⭐⭐⭐ Very high | Code complete, awaiting merge; Issue #59 tracks it long-term |
| **Programmatic tool calls (PTC)** | [#408 PR](https://github.com/nearai/ironclaw/pull/408) | ⭐⭐⭐⭐⭐ Very high | Updated today, with a complete implementation of ToolExecutor, SDK, and E2E tests |
| **AWS Bedrock support** | [#345 PR](https://github.com/nearai/ironclaw/pull/345) | ⭐⭐⭐⭐☆ High | XL-sized PR, native Converse API integration, clear enterprise demand |
| **Anthropic OAuth** | [#384 PR](https://github.com/nearai/ironclaw/pull/384) | ⭐⭐⭐⭐☆ High | Supports the `claude login` flow, reducing API key management friction |
| **Per-tool retry mechanism** | [#357 PR](https://github.com/nearai/ironclaw/pull/357) | ⭐⭐⭐⭐☆ High | Exponential backoff + jitter, a production necessity |
| **OpenClaw data migration** | [#388 PR](https://github.com/nearai/ironclaw/pull/388) | ⭐⭐⭐☆☆ Medium | Five-stage import pipeline, but depends on the size of OpenClaw's historical user base |
| **MCP auth fix** | [#313 PR](https://github.com/nearai/ironclaw/pull/313) | ⭐⭐⭐☆☆ Medium | Closes #299, but the PR has been open 9 days without merge |

---

## 7. User Feedback Summary

### Real pain points (from issue comments)

| Scenario | Verbatim Quote | Problem Category |
|:---|:---|:---|
| **WASM tool auth confusion** | *"I have a credentials.json file, no Idea how to use it"* | Missing documentation/CLI guidance |
| **Telegram state not persisted** | *"Every time I restart my instance, I need to click on activate"* | Configuration persistence flaw |
| **Secrets scan backfire** | *"The storm only ended after I disabled the telegram channel"* | Security mechanism lacks circuit-breaker design |
| **Tailscale expectation gap** | *"expectation is pretty much that it does that by itself"* | Product positioning mismatched with user mental model |
| **Embedding model configuration confusion** | *"How do i use ollama embeddings model nomic-embed-text"* | Multi-provider configuration docs scattered |

### Satisfaction signals
- ✅ **Fast fix**: #394

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Report | 2026-03-02

---

## 1. Today's Overview

LobsterAI showed **high development activity** today: within 24 hours it merged/closed **8 PRs** (including 2 feature additions and 3 key bug fixes) and released **v0.1.23**. The community filed **8 new issues** in parallel, focused on multi-model compatibility, session stability, and IM integration quota problems, with zero issues closed — issue digestion is lagging output. The project overall is in a **rapid-iteration phase**, and landing dependency-free Windows deployment is today's biggest milestone.

---

## 2. Version Releases

### v0.1.23 (released 2026-03-01)
🔗 [Release page](https://github.com/netease-youdao/LobsterAI/releases/tag/v0.1.23)

| Category | Content | Impact Assessment |
|:---|:---|:---|
| **New feature** | Windows bundled Python runtime support ([#192](https://github.com/netease-youdao/LobsterAI/pull/192)) | **Major experience improvement**: end users no longer need to install Python manually; the runtime is synced into userData and injected into PATH automatically, covering cowork sessions, skills, and skill services |
| **New feature** | Skill improvements ([#193](https://github.com/netease-youdao/LobsterAI/pull/193)) | Feature enhancement, details pending documentation |
| **Bug fix** | Disambiguate model selection by provider key ([#194](https://github.com/netease-youdao/LobsterAI/pull/194)) | **Key fix**: resolves same-model-ID conflicts across multiple providers, preventing user selections from being silently overridden |

**Migration notes**: after upgrading, the first launch on Windows automatically completes the Python runtime deployment; ~200MB of disk space is recommended. Users with custom provider configurations should verify that model selection behaves correctly.

---

## 3. Project Progress

| PR | Author | Type | Contribution |
|:---|:---|:---|:---|
| [#192](https://github.com/netease-youdao/LobsterAI/pull/192) | @fisherdaddy | Feature | **Zero-dependency Windows deployment** — removes the Python environment barrier, greatly lowering the onboarding cost for non-technical users |
| [#193](https://github.com/netease-youdao/LobsterAI/pull/193) | @liuzhq1986 | Feature | Skill system improvements, laying the groundwork for the future skill ecosystem |
| [#194](https://github.com/netease-youdao/LobsterAI/pull/194) | @fisherdaddy | Fix | **Core stability fix** — reliable model selection across multiple providers |
| [#123](https://github.com/netease-youdao/LobsterAI/pull/123) | @mammut001 | Fix | MiniMax API invalid-parameter error, unblocking that vendor's service pipeline |
| [#127](https://github.com/netease-youdao/LobsterAI/pull/127) | @mammut001 | Fix | Improved default-model logic on the settings page, preventing stale configuration pollution |
| [#167](https://github.com/netease-youdao/LobsterAI/pull/167) | @fisherdaddy | Fix | Custom email advanced-settings bug fix + UX polish |
| [#160](https://github.com/netease-youdao/LobsterAI/pull/160) | @fisherdaddy | Fix | Fixed garbled Chinese output in WebSearch skills, improving the localized experience |
| [#129](https://github.com/netease-youdao/LobsterAI/pull/129) | @fisherdaddy | Feature | System proxy settings support (off by default), adapting to corporate network environments |

**Overall progress**: today's merges span **deployment experience, multi-vendor compatibility, Chinese localization, and corporate network adaptation**; the project clearly leveled up from "features work" to "pleasant to use".

---

## 4. Community Highlights

| Rank | Issue/PR | Heat Metrics | Core Request Analysis |
|:---|:---|:---|:---|
| 🔥1 | [#187](https://github.com/netease-youdao/LobsterAI/issues/187) Non-Alibaba models all seem broken | 2 comments, with screenshots | **Multi-vendor compatibility crisis**: users report that all non-Alibaba Cloud models (OpenAI, MiniMax, etc.) are broken, with screenshots showing configuration UI anomalies. Combined with the "model selection ambiguity" fixed today by [#194](https://github.com/netease-youdao/LobsterAI/pull/194), this issue may be partially relieved in v0.1.23, but needs verification |
| 🔥2 | [#191](https://github.com/netease-youdao/LobsterAI/issues/191) API Error after several chats in one session | 1 comment | **Session state management flaw**: the ID-matching logic between `tool_calls` and `tool messages` breaks in long sessions, causing unrecoverable conversation interruptions. An architecture-level bug affecting the core use case |
| 🔥3 | [#198](https://github.com/netease-youdao/LobsterAI/issues/198) Can you add an MCP settings UI | 0 comments, high potential value | **Configuration UX request**: users want a graphical UI for configuring MCP (Model Context Protocol), and also raise multi-model switching/routing and a mobile version. Shows the configuration layer is still too technical for ordinary users |

**Signal underneath**: the community is shifting from "try-it users" to "heavy users", with sharply rising demands for **stability, configuration friendliness, and cross-platform capability**.

---

## 5. Bugs and Stability

| Severity | Issue | Symptom | Fix Status | Notes |
|:---|:---|:---|:---|:---|
| 🔴 **P0-Blocker** | [#191](https://github.com/netease-youdao/LobsterAI/issues/191) | Long-session tool-call chains break; conversations die completely | ❌ No PR | Needs an urgent fix; affects productivity scenarios |
| 🟡 **P1-High** | [#187](https://github.com/netease-youdao/LobsterAI/issues/187) | All non-Alibaba models unusable | 🟡 Possibly fixed | v0.1.23 [#194](https://github.com/netease-youdao/LobsterAI/pull/194) may be related; needs user verification |
| 🟡 **P1-High** | [#190](https://github.com/netease-youdao/LobsterAI/issues/190) | All historical sessions lost after upgrading from v0.1.22 | ❌ No PR | **Data-loss incident**; migration/backup mechanism needs urgent investigation |
| 🟢 **P2-Medium** | [#196](https://github.com/netease-youdao/LobsterAI/issues/196) | "Unknown skill" error after importing Vercel find-skills | ❌ No PR | Skill registration/discovery mechanism issue |
| 🟢 **P2-Medium** | [#195](https://github.com/netease-youdao/LobsterAI/issues/195) | Email skill cannot search for specific senders (invoice emails) | ❌ No PR | Edge case in email parsing/indexing logic |
| 🟢 **P2-Medium** | [#197](https://github.com/netease-youdao/LobsterAI/issues/197) | DingTalk IM suddenly stopped connecting, suspected quota limit | ❌ No PR | Needs quota-policy clarification or a service-status check |

---

## 6. Feature Requests and Roadmap Signals

| Issue | Request | Feasibility Assessment | Likelihood for Next Version |
|:---|:---|:---|:---|
| [#198](https://github.com/netease-youdao/LobsterAI/issues/198) | Graphical MCP settings UI + multi-model switching/routing | Medium | **High** — aligns with today's skill-improvement direction; the configuration layer is an obvious weakness |
| [#198](https://github.com/netease-youdao/LobsterAI/issues/198) | Mobile version | Low-Medium | **Medium** — a long-standing cross-platform request, but resource-heavy |
| [#189](https://github.com/netease-youdao/LobsterAI/issues/189) | OpenAI OAuth support | Medium | **Medium-High** — authentication-system expansion, essential for enterprise users, manageable technical debt |

**Roadmap signal**: the project's next phase may focus on **"configuration for everyone"** (MCP GUI, model routing) and **"identity-system completeness"** (OAuth support).

---

## 7. User Feedback Summary

> Distilled from issue descriptions and discussions

| Dimension | Feedback |
|:---|:---|
| **Pain points** | "All historical sessions lost after the upgrade" — **data-reliability anxiety**; frequent crashes in long sessions — a **stability trust crisis** |
| **Scenarios** | Invoice email search, DingTalk IM integration, flexible multi-model switching — **enterprise office/finance automation scenarios** stand out |
| **Satisfiers** | Python-free Windows install (implied expectation), skill extensibility |
| **Dissatisfiers** | High configuration barrier (manual JSON/environment-variable edits), unfriendly error messages (raw API Error stacks), opaque vendor compatibility |

**Key insight**: users treat LobsterAI as an **"automation office gateway"** rather than a mere chat tool, with production-grade expectations for **data persistence, service stability, and enterprise-system integration**

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Report | 2026-03-02

## 1. Today's Overview

TinyClaw's activity over the past 24 hours was **moderately low**, with the community focused on core architecture improvements. Key progress: PR #152 submitted a complete implementation of the widely requested multi-thread session-isolation feature, directly answering the feature request in Issue #144. Meanwhile, the Windows compatibility complaint Issue #151 was closed by the maintainer, showing cross-platform support remains a sensitive topic. No new version was released; the project is in a feature-iteration phase rather than a release window.

---

## 2. Version Releases

**No new version release**

---

## 3. Project Progress

| PR | Status | Progress Notes |
|:---|:---|:---|
| [#152](https://github.com/TinyAGI/tinyclaw/pull/152) feat: per-thread session isolation for Claude and Codex agents | 🟡 **Pending merge** | **Core architecture upgrade**: introduces a `thread_sessions` table implementing the `(agent_id, thread_id) → session_id` mapping, ending cross-platform context crosstalk. The Claude side replaces the global `-c` flag with `--session-id`/`-r`, with the Codex side adapted in sync. If merged, this PR marks TinyClaw stepping from a "single-session global agent" toward a "multi-tenant isolated architecture", laying the foundation for production deployment. |

**Overall progress assessment**: a major architectural step that resolves the long-standing context-pollution pain point for multi-platform users.

---

## 4. Community Highlights

| Item | Heat Metrics | Request Analysis |
|:---|:---|:---|
| [#151](https://github.com/TinyAGI/tinyclaw/issues/151) this shit aint for Windows quit lying | 2 comments, heated | **Core conflict**: docs/marketing claim Windows support, but the actual experience fails due to reliance on Linux window managers and PowerShell script compatibility. The user went through "fix settings.json → install jq → force-run Linux scripts" and still failed, feeling strongly deceived. Requests: **honestly label the platform support scope** or **actually solve the Windows compatibility layer**. The way it was closed (without substantive response) may deepen community trust erosion. |
| [#144](https://github.com/TinyAGI/tinyclaw/issues/144) feat: per-thread session isolation | 0 comments, but PR #152 responds directly | A must-have for enterprise/multi-user scenarios: Telegram topics and Discord threads leaking context into each other causes privacy exposure and logic confusion. User @bchoor proposed a concrete technical approach (`--session-id`/`--resume`), and @jliao quickly implemented it, showing core contributors agree on the architectural direction. |

---

## 5. Bugs and Stability

| Severity | Item | Status | Notes |
|:---|:---|:---|:---|
| 🔴 **High** | [#151](https://github.com/TinyAGI/tinyclaw/issues/151) Windows installation completely broken | ❌ Closed, **without a fix** | A fundamental disconnect between platform-support claims and the actual code, hurting potential user acquisition. Closing the issue without resolving the substance keeps the risk accumulating. |
| 🟡 Medium | — | — | No new crash or regression reports today |

> **Risk warning**: closing rather than resolving the Windows compatibility problem may trigger more negative word of mouth. The maintainers should either remove the Windows support claim or create a tracking issue to solve it systematically.

---

## 6. Feature Requests and Roadmap Signals

| Request | Source | Implementation Status | Likelihood |
|:---|:---|:---|:---|
| Thread-level session isolation | [#144](https://github.com/TinyAGI/tinyclaw/issues/144) + [#152](https://github.com/TinyAGI/tinyclaw/pull/152) | 🟡 PR pending review | **Very high** — code complete, and the architecture fits the multi-tenant direction |
| True native Windows support | Implied by [#151](https://github.com/TinyAGI/tinyclaw/issues/151) | ❌ No PR | Low — needs a WSL rebuild or a cross-platform abstraction layer; resource-heavy |

**Roadmap signal**: the project is transforming from a "personal tool" into a "deployable service"; session isolation is the first step, and enterprise needs such as permission models, audit logs, and configuration hot reload may follow.

---

## 7. User Feedback Summary

| Dimension | Details |
|:---|:---|
| **Pain points** | Windows users hit a "death-march install flow": package-manager conflicts → manual config fixes → script incompatibilities → finally discovering a hard dependency on Linux-only components |
| **Scenarios** | Context bleeds across multi-platform deployments (Telegram + Discord concurrently), with no way to isolate conversation histories of different users/topics |
| **Satisfiers** | The feature request [#144](https://github.com/TinyAGI/tinyclaw/issues/144) got a fast technical response, with a complete implementation in PR #152 |
| **Dissatisfiers** | Platform-support claims badly mismatch the actual experience; the way the issue was closed looks like avoidance rather than resolution |

**Typical user persona**: technically capable self-hosters who expect cross-platform consistency and have explicit requirements for architectural extensibility.

---

## 8. Pending Backlog

| Item | Age | Risk | Suggested Action |
|:---|:---|:---|:---|
| [#152](https://github.com/TinyAGI/tinyclaw/pull/152) | 1 day (newly submitted) | Architecture change needs careful review | Prioritized merge window; complete review within 48h |
| Windows compatibility issues | Long-standing, latent | Losing user acquisition | Create a meta-issue or update the docs to state the limitations honestly |

---

**Data source**: GitHub API | **Generated at**: 2026-03-02 | **Project URL**: https://github.com/TinyAGI/tinyclaw

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

⚠️ Summary generation failed.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Report | 2026-03-02

> **Project URL**: [github.com/qhkm/zeptoclaw](https://github.com/qhkm/zeptoclaw) \
> **Reporting period**: 2026-03-01 to 2026-03-02 (past 24 hours)

---

## 1. Today's Overview

ZeptoClaw showed **extremely high development activity** today: **9 PRs merged/closed** and **9 issues closed** within 24 hours, with **0 new issues**. The project is in a **dense feature-delivery phase**; core maintainer @qhkm drove all the merges, covering key areas such as enterprise deployment (Azure/Bedrock), security hardening, multimodal capabilities, and IoT expansion. The only pending item is dependency-upgrade PR #183; overall project health is excellent and technical debt is well controlled.

---

## 2. Version Releases

**No new version release**

---

## 3. Project Progress

The 9 PRs merged today pushed the project through **three major strategic leaps**:

| Dimension | Progress | Key PR |
|:---|:---|:---|
| **Enterprise readiness** | Azure OpenAI + Amazon Bedrock presets shipped, unlocking zero-code enterprise deployment | [#211](https://github.com/qhkm/zeptoclaw/pull/211) |
| **Security hardening** | The sub-agent shell tool gained 6 groups of dangerous Git command blocks, stopping destructive operations like force-push/reset --hard | [#195](https://github.com/qhkm/zeptoclaw/pull/195) |
| **Cost control** |  The per-provider usage quota system landed, supporting reject/downgrade/alert modes | [#210](https://github.com/qhkm/zeptoclaw/pull/210) |
| **Model ecosystem** | DeepSeek + Kimi, two Chinese LLMs, integrated; the OpenAI-compatible layer now spans 6+ mainstream vendors | [#208](https://github.com/qhkm/zeptoclaw/pull/208) |
| **Hardware boundary** | MQTT channel enabled; IoT devices freed from the "serial tether" to WiFi/network communication | [#209](https://github.com/qhkm/zeptoclaw/pull/209) |
| **Multimodal** | Vision/image input on all channels; the message pipeline natively supports three sources: Base64/URL/file path | [#202](https://github.com/qhkm/zeptoclaw/pull/202) |
| **Document handling** | DOCX text-extraction tool completed; PDF/DOCX dual-format coverage for business scenarios | [#206](https://github.com/qhkm/zeptoclaw/pull/206) |
| **Auth experience** | OpenAI OAuth one-click login, supporting Codex CLI token import + a browser-native authorization flow | [#205](https://github.com/qhkm/zeptoclaw/pull/205) |

**Architectural evolution**: all new providers are integrated through the `OpenAIProvider` compatibility layer, validating the extensibility of the "unified backend + configuration-driven" design.

---

## 4. Community Highlights

**No community discussion hotspots today** — all 9 issues and 10 PRs have **0 comments and 0 reactions**.

**Signal interpretation**:
- Feature requests were initiated and closed out by the core maintainer (#198-#207 were all created by @qhkm)
- The participation model leans toward "maintainer-driven design"; external contributors have not yet formed a discussion culture
- Worth noting: #207 (DeepSeek/Kimi support) was first raised by @jxnding; although it was an empty template, it was implemented quickly, reflecting the maintainer's strong responsiveness to Chinese-model demand

---

## 5. Bugs and Stability

| Severity | Problem | Status | Fix PR |
|:---|:---|:---|:---|
| 🔴 **High** | Sub-agents could bypass the safe Git tools via the shell to run destructive operations (force-push, reset --hard, etc.) | **Fixed** | [#195](https://github.com/qhkm/zeptoclaw/pull/195) |
| 🟡 **Medium** | reqwest 0.12 → 0.13 upgrade blocked by the gogcli-rs dependency | Pending | [#183](https://github.com/qhkm/zeptoclaw/pull/183) |

**Security fix details**: PR #195 added 6 groups of regex rules in `src/security/shell_blocklist.rs`, covering dangerous patterns such as `git push --force/-f`, `git reset --hard`, `git clean -f`, `git checkout -- .`, and `git branch -D`, while keeping an allowlist for read-only operations like `git fetch`/`git log`.

---

## 6. Feature Requests and Roadmap Signals

| Request Source | Feature | Implementation Status | Likelihood for Next Version |
|:---|:---|:---|:---|
| #198 / #211 | Azure OpenAI & Bedrock presets | ✅ Merged | — |
| #200 / #210 | per-provider usage quotas | ✅ Merged | — |
| #207 / #208 | DeepSeek + Kimi support | ✅ Merged | — |
| #199 / #209 | MQTT IoT channel | ✅ Merged | — |
| #201 / #206 | DOCX text extraction | ✅ Merged | — |
| #203 / #205 | OpenAI OAuth authentication | ✅ Merged | — |
| #197 / #202 | All-channel vision input | ✅ Merged | — |

**Roadmap signals**:
- **Enterprise gateway direction**: quota management + multi-cloud provider presets show the project evolving toward a "multi-tenant AI gateway"
- **Edge computing direction**: the dual MQTT + serial channels cement its hardware-agent positioning
- **Compliance direction**: the #204 disclaimer PR proactively draws a line from cryptocurrency, reducing legal risk

---

## 7. User Feedback Summary

**No user comment data today**; design demands distilled from issue descriptions:

| Pain-Point Scenario | Corresponding Implementation | Inferred Satisfaction |
|:---|:---|:---|
| "Enterprise deployment needs Azure/Bedrock but I don't want to write new provider code" | #211 zero-code presets | High |
| "Sub-agents might destroy the code repository by accident" | #195 shell blocklist | High |
| "Under multi-user scenarios, one provider's costs spiral out of control" | #210 quota system | High |
| "Devices like the ESP32 must be wired to serial to communicate" | #209 MQTT wireless channel | High |
| "Users send DOCX reports that can't be parsed" | #206 DOCX tool | High |
| "I have to manually copy my OpenAI API key every time" | #205 OAuth one-click login | High |

**Missing feedback**: no performance benchmarks, no edge-case reports, no multilingual/i18n requests.

---

## 8. Pending Backlog

| Item | Created | Blocking Reason | Suggested Action |
|:---|:---|:---|:---|
| [#183](https://github.com/qhkm/zeptoclaw/pull/183) Update dependencies | 2026-02-26 | Waiting for upstream gogcli-rs to upgrade reqwest 0.13 | @qhkm could evaluate a temporary fork fix or pushing an upstream PR |
| — | — | — | — |

**Backlog health**: only 1 pending PR and no long-unanswered issues — excellent maintenance state.

---

> **Analyst's note**: ZeptoClaw showed a "single maintainer iterating at high speed" profile today — extremely dense feature delivery but low community participation. Watch next for: 1) onboarding mechanisms for external contributors; 2) documentation/examples catching up after feature merges; 3) a resolution path for the #183 dependency blockage.

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw Project Report | 2026-03-02

> **Positioning**: AI agent and personal AI assistant tool | **Repository**: [github.com/gaoyangz77/easyclaw](https://github.com/gaoyangz77/easyclaw)

---

## 1. Today's Overview

EasyClaw's activity was **moderately low** today, with key developments centered on a **patch release** and **feature-gap feedback**. The community added 2 open issues in the past 24 hours with no PR activity, indicating a "maintenance-response period" rather than a "feature-iteration period". The rushed v1.5.13 release mainly addresses macOS signing compatibility, indirectly showing cross-platform deployment remains a persistent challenge for this project. User feedback shows the typical early-product pattern of "high satisfaction + clear feature gaps".

---

## 2. Version Releases

### v1.5.13 — macOS compatibility hotfix
| Attribute | Details |
|:---|:---|
| **Release type** | Patch release |
| **Core change** | Added macOS Gatekeeper bypass documentation and installation guidance |
| **Breaking changes** | None |
| **Migration notes** | macOS users seeing an "'EasyClaw' is damaged" prompt should run `xattr -cr /Applications/EasyClaw.app` in Terminal or manually allow the app in System Settings |

**Deep dive**: this release involves no code changes — it is an **emergency response at the documentation/distribution layer**. Unsigned apps being blocked by Gatekeeper is a common pain for Electron/indie-developer apps; this fix lowers the first-run barrier for macOS users, but long term an Apple Developer signature is still needed to eliminate the broken experience.

🔗 [Release page](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.5.13)

---

## 3. Project Progress

**No code-level feature progress today** (0 PRs merged/closed).

The project overall is **stalled**: no visible codebase iteration since v1.5.13 was released. Combined with the missing "multi-conversation" and "task scheduling" core features reported in Issues #3 and #4, the maintainer is likely either:
- in a short break, or
- preparing a larger feature rework (though there is no public roadmap to support this)

**Health warning**: consecutive days with no PR activity + a pile-up of feature-type issues; watch the maintainer's response time.

---

## 4. Community Highlights

### 🔥 Issue #3: model switching and multi-conversation limits
| Metric | Data |
|:---|:---|
| Comments | 2 (including the author's follow-up) |
| Interaction pattern | Users proactively adding details, showing the problem is reproducible |
| Core requests | ① Switch AI models mid-conversation ② Parallel multi-session ③ Remove structured markers from replies |

**Signal underneath**: users compare EasyClaw against the official ChatGPT/Claude clients and expect **equally flexible conversation management**. The current single-model, single-session design may stem from simplified state management at the architecture level, but it has become a **core experience bottleneck**.

🔗 [Issue #3](https://github.com/gaoyangz77/easyclaw/issues/3)

### ⭐ Issue #4: task scheduling and conversation history requests
| Metric | Data |
|:---|:---|
| 👍 count | 1 (community endorsement) |
| Sentiment | **Highly positive** — "the one that suits me best", "I'll recommend it to my colleagues tomorrow" |
| Feature gaps | ① Task scheduling ② Persistent conversation history |

**Signal underneath**: this user has completed **product-market fit validation** (a PMF signal) and is willing to spread the word organically. The two missing features point to **productivity scenarios** (scheduled tasks) and **data-asset accumulation** (history) — the key leap for an AI assistant upgrading from "toy" to "tool".

🔗 [Issue #4](https://github.com/gaoyangz77/easyclaw/issues/4)

---

## 5. Bugs and Stability

| Severity | Description | Source | Fix PR | Status |
|:---|:---|:---|:---:|:---|
| **P2-Functional defect** | Replies contain structured markers (not plain-text output) | Issue #3 | ❌ None | 🔴 Open |
| **P3-Experience limitation** | Cannot switch models / run parallel sessions | Issue #3 | ❌ None | 🔴 Open |

**Note**: no P0-P1 problems (crashes, data loss, security vulnerabilities) were reported today. The existing issues are all **design choices or unimplemented features**, not runtime bugs.

---

## 6. Feature Requests and Roadmap Signals

| Feature Request | Source | User Urgency | Technical Feasibility (estimated) | Likelihood for Next Version |
|:---|:---|:---:|:---|:---:|
| Conversation history | Issue #4 | ⭐⭐⭐⭐⭐ | High (local storage / cloud sync) | **70%** — infrastructure-level need |
| Task scheduling system | Issue #4 | ⭐⭐⭐⭐⭐ | Medium (needs timers + background wake) | **40%** — large architectural change |
| Parallel multi-session | Issue #3 | ⭐⭐⭐⭐☆ | Medium (state-management refactor) | **50%** — core to the experience but engineering-heavy |
| Live model switching | Issue #3 | ⭐⭐⭐⭐☆ | High (config hot reload) | **60%** — relatively independent module |

**Key judgment**: the author of Issue #4 explicitly expressed willingness to spread the word; if the maintainer wants to **ride this growth moment**, they should prioritize this user's two requests (history + task scheduling) to close the word-of-mouth loop.

---

## 7. User Feedback Summary

### ✅ Satisfiers
> *"I've tried many versions of the lobster assistants, and this is the one that suits me best"* — Issue #4

- **Precise positioning**: among similar "lobster" tools (possibly referring to the LangChain/LangGraph ecosystem or a nickname in the Chinese AI assistant circle), EasyClaw's **simplicity** is recognized
- **Basic experience passes**: solid enough to support users' core workflows and build attachment

### ❌ Pain points and scenarios
| Pain Point | Real Scenario | Implied Need |
|:---|:---|:---|
| Structured markers in replies | Extra cleanup needed when copying plain-text answers | Customizable output format (Markdown/plain text/JSON) |
| No conversation history | Yesterday's query results can't be found and must be re-asked | Local knowledge base + retrieval |
| No task scheduling | Want AI to run scheduled report generation / data monitoring | Upgrading from "conversational" to "agentic" |

### 🎯 Emerging user persona
- **Early adopters**: willing to try non-mainstream tools and tolerate missing features
- **Productivity-oriented**: not for entertainment; chasing efficiency gains
- **Propagation nodes**: have influence in their colleague circles ("I'll recommend it to my colleagues tomorrow")

---

## 8. Pending Backlog

**No long-standing backlog items** (the repository is new, only 4 issues total), but watch these **response-time risks**:

| Issue | Created | Current Status | Suggested Action |
|:---|:---|:---|:---|
| #3 Model switching and multi-conversation | 2026-03-01 | Open, 2 comments awaiting reply | The maintainer should confirm within 48h whether this is intended design or a scheduled fix |
| #4 Task scheduling and conversation history | 2026-03-01 | Open, high-emotional-value user | Reply first and invite them to the beta/requirement discussions |

**Health advice**: as an early-stage project, the maintainer should establish a **<24h first-response mechanism for issues** and turn the author of Issue #4 into a **core contributor or seed user**.

---

*Report generated at: 2026-03-02 | Data source: public GitHub API data*

</details>

---
*This report was auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*