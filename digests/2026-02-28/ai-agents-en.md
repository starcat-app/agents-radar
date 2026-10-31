# OpenClaw Ecosystem Report 2026-02-28

> Issues: 500 | PRs: 500 | Projects covered: 10 | Generated at: 2026-02-28 03:32 UTC

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

## OpenClaw Project In-Depth Report

# OpenClaw Project Report | 2026-02-28

---

## 1. Today at a Glance

OpenClaw maintained **extremely high activity** today, with **500 Issue updates** (386 opened/active, 114 closed) and **500 PR updates** (364 pending merge, 136 merged/closed) within 24 hours, and no new release. Community focus concentrated on **installation and deployment issues** (pnpm/npm global install path verification), **multi-channel stability** (Feishu, Telegram, Discord), and **security architecture** (API key protection, skill installation hooks). Notably, the plugin path security verification introduced in v2026.2.26 conflicts with pnpm global installs, making it today's most frequent blocking issue.

---

## 2. Releases

**No new release** (the latest version remains 2026.2.26)

> ⚠️ Known issue: the plugin path security verification in v2026.2.26 breaks pnpm global installs; the community is urgently working on a fix.

---

## 3. Project Progress

### Notable merged/closed PRs

| PR | Author | Core improvement | Related Issue |
|:---|:---|:---|:---|
| [#29264](https://github.com/openclaw/openclaw/pull/29264) | @paceyw | Feishu channel automatically converts local image-path text into image messages | Fixes image paths leaking as plain text |
| [#28529](https://github.com/openclaw/openclaw/pull/28529) | @cowboy129 | Feishu channel adds reaction event listening (im.message.reaction.created/deleted) | Enables passively responding to user emoji reactions |
| [#24978](https://github.com/openclaw/openclaw/pull/24978) | @mcaxtr | Restores the Feishu dmPolicy default to "open", fixing the breaking change introduced in v2026.2.14 | [#17741](https://github.com/openclaw/openclaw/issues/17741) |
| [#29374](https://github.com/openclaw/openclaw/pull/29374) | @obviyus | Android node capability list refactor, unified runtime flags | Reduces capability-drift risk |
| [#16284](https://github.com/openclaw/openclaw/pull/16284) | @Yaxuan42 | Feishu multi-account credential isolation, supporting routing tool credentials by account parameter | Fixes multi-account configuration conflicts |

**Overall progress**: the Feishu channel was today's key optimization target, delivering three major improvements — the full reaction-event chain, the image-message experience, and multi-account isolation; the Android mobile architecture continues to be polished.

---

## 4. Community Hotspots

### 🔥 Most-discussed Issues

| Issue | Comments | Core request | Status |
|:---|:---|:---|:---|
| [#4855](https://github.com/openclaw/openclaw/issues/4855) Control UI assets not found on npm global install | 37 | **Global install path resolution failure** — `resolveControlUiDistIndexPath` cannot locate bundled assets, affecting all npm global install users | ✅ Closed |
| [#19184](https://github.com/openclaw/openclaw/issues/19184) OpenAI Responses 400 error loop on gpt-5.2 | 23 | **Reasoning-model compatibility** — gpt-5.2 reasoning-type items missing follow-up items cause an infinite loop | ✅ Closed |
| [#21653](https://github.com/openclaw/openclaw/issues/21653) Custom API providers 4096-token context window limit | 19 | **Custom provider configuration experience** — the default context window is too low, causing the agent to fail immediately | 🔴 Open |
| [#4544](https://github.com/openclaw/openclaw/issues/4544) Cannot change model to Ollama Deepseek-r1 | 17 | **Local model switching experience** — command recognition issues when switching from a cloud model to a local Ollama model | ✅ Closed |
| [#7631](https://github.com/openclaw/openclaw/issues/7631) Windows: `openclaw plugins install` spawn EINVAL | 16 | **Windows plugin installation blocked** — child_process spawn arguments are incompatible on Windows | 🔴 Open, no PR |

**Analysis of underlying needs**: the installation/deployment experience (global installs, Windows compatibility) and **smarter model configuration** (auto-detecting context windows, smoothly switching between local and cloud models) are users' two most urgent pain points.

---

## 5. Bugs and Stability

### 🔴 Critical (blocks features/data safety)

| Issue | Description | Impact scope | Fix PR |
|:---|:---|:---|:---|
| [#28175](https://github.com/openclaw/openclaw/issues/28175) [#28122](https://github.com/openclaw/openclaw/issues/28122) | **pnpm global installs blocked by security verification** — "unsafe plugin manifest path" error; v2026.2.26 regression | All pnpm global install users | 🔄 Under community discussion; temporarily using npm recommended |
| [#28877](https://github.com/openclaw/openclaw/issues/28877) | **macOS app became arm64-only**; Intel Macs cannot launch it | Intel Mac users | 🔍 Build fix needed |
| [#26207](https://github.com/openclaw/openclaw/issues/26207) | **v2026.2.24 proxy configuration broken** — `setGlobalDispatcher` breaks all outbound HTTP proxies | Users who need proxy access (e.g. GFW environments) | 🔍 Needs rollback or fix |
| [#27053](https://github.com/openclaw/openclaw/issues/27053) | **Typing indicator persists indefinitely** — regression from the keepalive feature introduced by PR #25886 | All channels using typing indicators | 🔍 Fix needed |
| [#28386](https://github.com/openclaw/openclaw/issues/28386) | **minimax-portal OAuth 401**, v2026.2.26 regression; fine in v2026.2.24 | minimax users | 🔍 Investigation needed |

### 🟡 Medium (limited functionality/degraded experience)

| Issue | Description | Status |
|:---|:---|:---|
| [#29134](https://github.com/openclaw/openclaw/issues/29134) | Windows ACP runtime backend reports unavailable, but the acpx CLI works fine | Open |
| [#23538](https://github.com/openclaw/openclaw/issues/23538) | Anthropic setup-token auth returns 401; reproducible in isolated environments | Open |
| [#27921](https://github.com/openclaw/openclaw/issues/27921) | Cron jobs `mode:announce` send duplicate messages | Open |
| [#27409](https://github.com/openclaw/openclaw/issues/27409) | Discord REST API "fetch failed"; proxy configuration ineffective | Open |

---

## 6. Feature Requests and Roadmap Signals

### New features users strongly want

| Issue/PR | Feature | User motivation | Likelihood of inclusion |
|:---|:---|:---|:---|
| [#18677](https://github.com/openclaw/openclaw/issues/18677) | **Security Scan Hook API for skill:install** | Security scanning before skill installation to guard against malicious code | ⭐⭐⭐⭐⭐ High — VirusTotal integration already mentioned; a community security focus |
| [#7916](https://github.com/openclaw/openclaw/issues/7916) | **Encrypted API keys / key management** | Currently stores `auth-profiles.json` and `openclaw.json` in plaintext | ⭐⭐⭐⭐⭐ High — core of the security roadmap |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) | **Prebuilt Android APK releases** | Users cannot compile the Android companion app themselves | ⭐⭐⭐⭐☆ Medium-high — PR #29374 provides the refactoring groundwork |
| [#29308](https://github.com/openclaw/openclaw/pull/29308) | **WeCom channel plugin** | Demand for Chinese enterprise IM integration | ⭐⭐⭐⭐☆ Medium-high — PR submitted with complete functionality |
| [#28691](https://github.com/openclaw/openclaw/pull/28691) | **Gateway dashboard Terminal + FileExplore** | Manage hosts directly without SSH | ⭐⭐⭐⭐☆ Medium-high — large PR awaiting review |
| [#29319](https://github.com/openclaw/openclaw/pull/29319) | **Evolution Framework - autonomous continuous learning** | 40-60 rounds of autonomous exploration sessions with safety mechanisms | ⭐⭐⭐☆☆ Medium — community example; production readiness needs evaluation |
| [#25480](https://github.com/openclaw/openclaw/pull/25480) | **Guardian security layer** — tool-call blacklist + LLM intent verification | Two-phase verification of dangerous operations | ⭐⭐⭐⭐⭐ High — directly answers the #18677 request |

**Roadmap signals**: security architecture (key encryption, skill scanning, the Guardian layer) and **enterprise-grade channels** (WeCom, deep Feishu optimization) are clear priorities for the next version.

---

## 7. User Feedback Summary

### 💬 Real pain points

> *"pnpm global install should be supported as documented"* — [#28175](https://github.com/openclaw/openclaw/issues/28175)
>
> **Core complaint**: the pnpm support promised in the official docs was broken by security verification in v2026.2.26, forcing users back to npm.

> *"Model context window too small (4096 tokens). Minimum is 16000"* — [#21653](https://github.com/openclaw/openclaw/issues/21653)
>
> **Configuration experience flaw**: default configuration for custom API providers is too conservative; novice users cannot understand why the agent "suddenly fails".

> *"Intel Macs with 'You can't open the application because this application is not supported on this Mac'"* — [#28877](https://github.com/openclaw/openclaw/issues/28877)
>
> **Release quality**: releases did not verify multi-architecture builds, leaving user machines "collateral damage".

### ✅ Satisfaction scenarios

- The Feishu reaction event listening [#28529](https://github.com/openclaw/openclaw/pull/28529) was merged quickly; enterprise users appreciated the response speed
- Multi-account credential isolation [#16284](https://github.com/openclaw/openclaw/pull/16284) resolved the long-standing credential-confusion problem

---

## 8. Pending Backlog

### ⚠️ Important items long awaiting a response

| Issue/PR | Days | Problem | Suggested action |
|:---|:---|:---|:---|
| [#11829](https://github.com/openclaw/openclaw/issues/11829) | 20 days | **Systemic risk of API keys leaking to the LLM** — model catalog serialization, chat history exposure, tool response leakage | Maintainers need to confirm roadmap priority |
| [#16521](https://github.com/openclaw/openclaw/issues/16521) | 14 days | **Error classifier false positives** — the regex-based heuristic classification in `sanitizeUserFacingText()` misjudges billing/rate-limit errors | Label `good first issue` or assign a refactor |
| [#18470](https://github.com/openclaw/openclaw/issues/18470) | 12 days | **Gateway deadlock** — invoking internal commands during an active agent turn causes blocking | Core maintainers need to investigate the concurrency model |
| [#20222](https://github.com/openclaw/openclaw/issues/20222) | 10 days | **Google Chat webhook infinite restart loop** — v2026.2.17 regression with no error logs | Add debug logging or investigate a rollback |
| [#15582](https://github.com/openclaw/openclaw/issues/15582) | 15 days | **Remote CDP (Browserless) port conflict misjudgment** | Needs reproduction on Windows/WSL2 |

---

**Daily report generated at**: 2026-02-28 \
**Data source**: GitHub API (openclaw/openclaw)

---

## Cross-Ecosystem Comparison

# Personal AI Assistant Open Source Ecosystem Comparison Report
**Analysis date: 2026-02-28**

---

## 1. Ecosystem Overview

The open source ecosystem for personal AI assistants/autonomous agents is going through **a pivotal leap from "single-point tools" to "multi-channel platforms"**. Leading projects (OpenClaw, NanoBot, PicoClaw) handle 20-40 PRs a day, and community focus is highly concentrated on **MCP protocol integration** (5+ projects working on it), **deep enterprise IM adaptation** (full coverage across Feishu/DingTalk/Discord/Telegram), and **security architecture hardening** (key encryption, skill sandboxes, audit logs). Meanwhile, **resource efficiency** has become a new competitive dimension — ZeroClaw benchmarks its <5MB memory footprint against OpenClaw's 1.5GB, triggering migration discussions; **native Windows support** has been upgraded from a fringe need to a core differentiator. Overall, the ecosystem shows a pattern of "feature expansion and quality consolidation proceeding in parallel, with head concentration and long-tail segmentation coexisting".

---

## 2. Project Activity Comparison

| Project | Today's Issues | Today's PRs | Releases | Health assessment | Stage positioning |
|:---|:---:|:---:|:---:|:---|:---|
| **OpenClaw** | 500 updates (386 active/114 closed) | 500 updates (364 pending merge/136 processed) | ❌ None | 🟡 **High activity, high backlog** — 27% merge rate; the pnpm global-install regression blocks some users | Quality consolidation phase |
| **ZeroClaw** | 41 closed (82% close rate) | 50 updates (3 merged/47 awaiting review, 6% merge rate) | ❌ None | 🟡 **High throughput, review bottleneck** — efficient Issue cleanup but a serious PR backlog | Rapid iteration phase |
| **LobsterAI** | 28 updates (21 active/7 closed) | 21 updates (16 merged/5 awaiting review, 76% merge rate) | ✅ v0.1.22 | 🟢 **Healthy iteration** — high merge rate; quick response on Ollama experience improvements | Rapid iteration phase |
| **NanoBot** | 32 updates (25 active/7 closed) | 72 updates (32 processed/40 pending merge) | ❌ None | 🟡 **High activity, high backlog** — 40 backlogged PRs; significant merge pressure | Feature expansion phase |
| **PicoClaw** | 29 updates (16 active/13 closed) | 91 updates (34 processed/57 pending merge) | ❌ None | 🟡 **Extremely high activity, extremely high backlog** — 57 PRs pending merge, the most in the ecosystem | Feature expansion phase |
| **NanoClaw** | Data not disclosed | 37 updates (8 processed/29 pending merge) | ❌ None | 🟡 **Architecture-refactor driven** — the #500 pluggable-channels refactor has become the center of gravity | Architecture transition phase |
| **IronClaw** | 6 updates (5 active/1 closed) | 27 updates (13 processed/14 awaiting review, 48% merge rate) | ❌ None (v0.13.0 pending release) | 🟢 **Healthy pace** — balanced review throughput; testing-system milestone | Stability consolidation phase |
| **TinyClaw** | 1 opened | 8 updates (4 processed/4 awaiting review) | ❌ None | 🟢 **Healthy early stage** — plugin system landed; enterprise needs starting to surface | Platform take-off phase |
| **ZeptoClaw** | 2 updates (1 opened/1 closed) | 2 updates (1 merged/1 awaiting review) | ❌ None | 🟢 **Steady progress** — MCP stdio transport milestone | Infrastructure deepening phase |
| **EasyClaw** | 1 closed | 0 updates | ✅ v1.5.11/v1.5.12 released back-to-back | 🟡 **Low activity, documentation maintenance** — functional commits stalled; insufficient version transparency | Stable observation phase |

---

## 3. OpenClaw's Position in the Ecosystem

| Dimension | OpenClaw characteristics | Ecosystem comparison |
|:---|:---|:---|
| **Community size** | **Absolute lead** — 500 daily Issue/PR updates, roughly 5-6x the runner-up (PicoClaw's 91 PRs) | The ecosystem's largest single project, but its 27% merge rate trails LobsterAI (76%) and IronClaw (48%) |
| **Technical route** | **TypeScript/Node ecosystem + plugin architecture** — pnpm/npm toolchain, skill marketplace, Control UI visualization | For comparison: ZeroClaw (Rust/ultimate performance), NanoBot (Python/academic-research oriented), IronClaw (Rust/WASM sandbox) |
| **Core strengths** | ① **Widest channel coverage** — enterprise-grade deep integration with Feishu/Telegram/Discord/Slack/WhatsApp<br>② **Mature ecosystem toolchain** — skill marketplace, scheduled tasks, multi-account isolation<br>③ **Proven enterprise scenarios** — production-grade features such as multi-account credential isolation and reaction event listening | For comparison: LobsterAI is catching up (NetEase Xiaomifeng, Volcengine); PicoClaw is close on channel count but behind on stability |
| **Current weaknesses** | ① **Installation experience regression** — v2026.2.26 security verification blocks pnpm global installs<br>② **Architectural weight** — 1.5GB RAM footprint vs ZeroClaw's <5MB, triggering migration discussions (ZeroClaw #88)<br>③ **Review throughput** — 364 PRs pending merge reflect a governance-bandwidth bottleneck | For comparison: IronClaw's test system is more mature (1,724 tests); ZeptoClaw leads on dual-mode MCP transport |
| **Differentiation anchor** | **"Enterprise-grade multi-channel AI operations platform"** — emphasizing deep IM integration, team collaboration, and visual control | Not direct competitors: ZeroClaw (personal lightweight), NanoBot (academic/native Windows), IronClaw (WASM security sandbox) |

---

## 4. Commonly Shared Technical Directions

| Technical direction | Projects involved | Specific needs and progress |
|:---|:---|:---|
| **MCP protocol integration** | ZeptoClaw ✅, PicoClaw (#282), NanoBot, OpenClaw | ZeptoClaw completed the stdio transport milestone today; PicoClaw PR #282 awaits review; community consensus: MCP is the key infrastructure for standardizing the tool ecosystem |
| **Deep enterprise IM adaptation** | OpenClaw, LobsterAI, NanoBot, PicoClaw, ZeroClaw, NanoClaw | **Feishu**: reaction events (OpenClaw #28529), streaming cards (NanoBot #1080), multi-account isolation (OpenClaw #16284)<br>**DingTalk/WeCom**: strong demand for low-barrier access (LobsterAI #102, PicoClaw #872)<br>**Telegram**: voice transcription (ZeroClaw #1469), topics support (NanoClaw #564), endpoint hot-switching (ZeptoClaw #193) |
| **Security architecture hardening** | OpenClaw, IronClaw, TinyClaw, PicoClaw | **Key encryption** (OpenClaw #7916; IronClaw already supports environment-variable isolation)<br>**Security scanning for skill installation** (OpenClaw #18677, #25480 Guardian layer)<br>**Plugin sandbox/timeout control** (TinyClaw #149, #150) |
| **Native Windows support** | ZeroClaw, NanoBot, LobsterAI, OpenClaw | ZeroClaw/NanoBot treat Windows compatibility as a core differentiator; OpenClaw is called a "second-class citizen" in comparisons due to its WSL dependency (#1265) |
| **Local model/Ollama optimization** | LobsterAI, IronClaw, PicoClaw, OpenClaw | LobsterAI #149 greatly reduced model-ID ambiguity today; IronClaw #400 model-name truncation awaits a fix; core pain points: configuration barriers, timeout handling, context-window detection |
| **Session isolation/multi-tenancy** | TinyClaw (#144), NanoBot (#1302), OpenClaw | A key requirement for evolving from personal tool to team deployment: per-thread context isolation, workspace sandboxes, hot config reload |

---

## 5. Differentiation Analysis

| Project | Core feature focus | Target user profile | Technical architecture traits |
|:---|:---|:---|:---|
| **OpenClaw** | Enterprise multi-channel collaboration, skill marketplace, visual control | Technical teams, DevOps, enterprises needing deep IM integration | Node/TS, plugin-based, Control UI, heavyweight all-in-one platform |
| **ZeroClaw** | Ultimate resource efficiency, Rust performance, fast startup | Edge computing, resource-constrained environments, users sensitive to 1.5GB→5MB | Rust, zero runtime dependencies, lightweight binary, review bottleneck unresolved |
| **LobsterAI** | Chinese model adaptation (Tongyi/Volcengine/MiniMax), scheduled tasks, personal automation | Chinese developers, Alibaba Cloud ecosystem users, people wanting an IFTTT alternative | Electron desktop app, prioritizes Chinese cloud vendors, extremely fast iteration |
| **NanoBot** | Native Windows, academic research, multi-agent orchestration | Windows developers, university research teams, individual users wanting out-of-the-box setups | Python, HKUDS academic background, Windows compatibility as the core selling point |
| **IronClaw** | WASM security sandbox, programmable tool calls (PTC), NEAR AI ecosystem | Security-sensitive scenarios, blockchain/Web3 developers, enterprises needing audit trails | Rust, WASM channel isolation, libSQL persistence, test-driven |
| **PicoClaw** | Multi-channel coverage (chasing quantity), SOUL.md memory system, self-hosting | Geek users, privacy-first users (Signal demand #41), heavy multi-IM users | Go, channel system being refactored (#621), tackling memory/context compression |
| **ZeptoClaw** | MCP infrastructure, transport-layer abstraction, developer toolchain | AI infrastructure developers, engineers needing custom tool integration | Rust, McpTransport trait architecture, HTTP/stdio dual mode |
| **TinyClaw** | Plugin system (Events+Hooks), 3D avatar visualization, rapid prototyping | Creative developers, interactive scenarios needing visual feedback | Early-stage TypeScript, plugin ecosystem taking shape, transitioning to a monorepo |
| **NanoClaw** | WhatsApp-centric (transitioning to multi-channel), voice security, religious/cultural modes | Heavy WhatsApp users, people with specific cultural-scenario needs | TypeScript, critical period of the #500 architecture refactor, Signal as the privacy alternative |
| **EasyClaw** | Simplified configuration, Bailian/Alibaba Cloud Coding Plan integration | Beginner developers in China, users seeking a lightweight OpenClaw alternative | Low activity, insufficient version transparency, unclear ecosystem niche |

---

## 6. Community Activity and Maturity Tiers

```
[Rapid iteration phase] Feature expansion first, high merge rate, new features landing in quick succession
├── LobsterAI (v0.1.22, 76% merge rate, aggressive Chinese model adaptation)
├── ZeroClaw (82% Issue close rate, PR review bottleneck, CJK stability push)
└── TinyClaw (plugin system milestone, enterprise needs surfacing)

[Feature expansion phase] Highly active but heavily backlogged, architectural debt accumulating
├── PicoClaw (91 PRs/day, 57 pending merge, channel-count race)
└── NanoBot (72 PRs/day, 40 pending merge, multi-agent architecture awaiting an official response)

[Quality consolidation phase] Healthy review cadence, tests/stability first
├── IronClaw (48% merge rate, 1,724-test milestone, PTC performance optimization)
└── OpenClaw (27% merge rate, pnpm regression fix, security-verification walk-back)

[Architecture transition phase] Core refactor in progress, ecosystem expansion blocked
└── NanoClaw (#500 pluggable-channels refactor, Signal/WhatsApp in parallel, 29 PRs awaiting review)

[Infrastructure deepening phase] Focused on a single technical point, steady progress
└── ZeptoClaw (MCP stdio milestone, low activity but high completeness)

[Stable observation phase] Maintenance mode, functional stagnation
└── EasyClaw (consecutive documentation releases, no code commits, transparency risk)
```

---

## 7. Trend Signals Worth Watching

| Trend signal | Supporting data | Reference value for developers |
|:---|:---|:---|
| **"Memory efficiency" becomes a new competitive dimension** | ZeroClaw #88 got 20 👍; "1.5GB→5MB" is the core migration driver; OpenClaw is called "too heavy" in comparisons | Resource-constrained scenarios (edge, IoT, multi-instance deployments) should prioritize Rust/Go stacks; Electron/Node architectures need to justify their necessity |
| **The MCP protocol becomes the de facto standard for the tool ecosystem** | 5+ projects working on it; ZeptoClaw finished dual-mode transport; PicoClaw #282 awaits review | New tool integrations should implement MCP server/client first rather than custom protocols; stdio mode is critical for the local CLI tool ecosystem |
| **Native Windows support upgrades from "compatibility" to "differentiation"** | NanoBot #1265 explicitly contrasts against OpenClaw's WSL dependency; ZeroClaw is shipping dense Windows fixes | Enterprise Windows deployments are a large unserved market; the WSL dependency has become a negative-experience label |
| **"Real-time model switching" exposes an ops-experience gap** | ZeptoClaw #193 and NanoBot #1292 emerged in the same period, explicitly benchmarking OpenClaw's `/models` design | Production environments need runtime elasticity rather than static configuration; degradation strategies for rate-limit/failure scenarios become hard requirements |
| **Session isolation demand marks the "personal→team" leap** | TinyClaw #144 and NanoBot #1302 surface enterprise-grade needs | Multi-tenant architecture must be designed up front: thread/topic-level context isolation, workspace sandboxes, hot config reload |
| **CJK/Chinese-language scenarios become the stability litmus test** | ZeroClaw's UTF-8 truncation panic, PowerShell encoding, and agent intent-recognition failures form a problem cluster | Internationalization testing cannot rely on ASCII data alone; tool calls and intent recognition in Chinese contexts need dedicated optimization |
| **Security architecture shifts from "feature" to "entry requirement"** | OpenClaw #18677 skill scanning, IronClaw PTC security audits, TinyClaw plugin gating stack up in PRs | Enterprise procurement will demand provable security models: key encryption, skill signing, sandbox timeouts, operation auditing |

---

**Report generated at**: 2026-02-28 \
**Analysis coverage**: 10 active open source projects, 2,847 GitHub activity records

---

## Detailed Reports on Same-Track Projects

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Report | 2026-02-28

## 1. Today at a Glance

ZeroClaw showed **high activity and high throughput** today: 41 Issues closed within 24 hours (an 82% close rate), but a PR merge rate of only 6% (3/50), indicating the team is focused on Issue cleanup while code review is backlogged. Community discussion centers on three themes: **multi-user TOTP security architecture**, **Windows build fixes**, and **Chinese/CJK scenario stability**. Notably, robotics/developer needs such as ROS2 integration and a native GitHub channel keep emerging, and the project is evolving from a "single-operator tool" toward an "enterprise-grade multi-tenant platform".

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### Key merged/closed PRs

| PR | Author | Core contribution | Significance for the project |
|:---|:---|:---|:---|
| [#2145](https://github.com/zeroclaw-labs/zeroclaw/pull/2145) | @theonlyhennygod | **GitHub Copilot onboarding interactive setup wizard** | Rounds out mainstream AI provider coverage and lowers the configuration barrier for new users |
| [#2143](https://github.com/zeroclaw-labs/zeroclaw/pull/2143) | @theonlyhennygod | Hardware positioning copy update: "$10 hardware" → "any hardware" | Removes market misunderstanding and reinforces the cross-platform lightweight positioning |
| [#2140](https://github.com/zeroclaw-labs/zeroclaw/pull/2140) | @theonlyhennygod | README slimmed down; docs migrated to a dedicated system | Improves the first-visit experience and establishes a maintainable documentation architecture |

**Overall progress assessment**: today's merges were mostly **user-experience improvements**; core features (such as the Matrix channel, the economic agent system, WASM plugins) are still sitting in the PR queue awaiting review, and code-review bandwidth is the main bottleneck.

---

## 4. Community Hotspots

### 🔥 Most-discussed Issues

| Issue | Comments | Core request | Underlying signal |
|:---|:---:|:---|:---|
| [#1856](https://github.com/zeroclaw-labs/zeroclaw/issues/1856) | 7 | Multi-user TOTP registration and RBAC permissions | **Surging demand for enterprise shared environments**: evolving from a "single operator" to a "team-level" security model |
| [#2055](https://github.com/zeroclaw-labs/zeroclaw/issues/2055) | 6 | `channel-matrix` feature fails to compile | Matrix protocol support hit stability issues right after landing; the feature-flag system needs hardening |
| [#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88) | 6 | OpenClaw→ZeroClaw migration feature checklist | **Production-grade users arriving**: the RAM footprint gain (1.5GB→<5MB) is the core migration driver, but feature completeness is in doubt |
| [#1469](https://github.com/zeroclaw-labs/zeroclaw/issues/1469) | 6 | Telegram voice transcription not triggering | Async event reliability problems in multimedia-processing channels |

### 👍 Strongest community reactions

- [#527](https://github.com/zeroclaw-labs/zeroclaw/issues/527) **25👍** - Official security statement and anti-fraud advisory (posted by @chumyin)
- [#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88) **20👍** - Migration blocker checklist (continuously drawing production-user attention)

---

## 5. Bugs and Stability

### Sorted by severity

| Level | Issue | Description | Status | Fix PR |
|:---:|:---|:---|:---:|:---:|
| **S0** | [#2055](https://github.com/zeroclaw-labs/zeroclaw/issues/2055) | `channel-matrix` feature fails to compile | ✅ Closed | Fixed |
| **S0** | [#2066](https://github.com/zeroclaw-labs/zeroclaw/issues/2066) | Docker build failure: template file missing | ✅ Closed | Fixed |
| **S0** | [#2083](https://github.com/zeroclaw-labs/zeroclaw/issues/2083) | Debian 12 glibc version incompatibility | ✅ Closed | Needs verification |
| **S1** | [#2072](https://github.com/zeroclaw-labs/zeroclaw/issues/2072) | Windows web agent only returns labels without performing actions | ✅ Closed | [#2056](https://github.com/zeroclaw-labs/zeroclaw/pull/2056) awaiting review |
| **S1** | [#2060](https://github.com/zeroclaw-labs/zeroclaw/issues/2060) | UTF-8 multibyte character truncation panic | ✅ Closed | [#2075](https://github.com/zeroclaw-labs/zeroclaw/pull/2075) awaiting review |
| **S1** | [#2062](https://github.com/zeroclaw-labs/zeroclaw/issues/2062) | Docker `--locked` flag conflicts with custom features | ✅ Closed | Fixed |
| **S1** | [#2105](https://github.com/zeroclaw-labs/zeroclaw/issues/2105) | Agent promises to act but actually stops | ✅ Closed | [#2146](https://github.com/zeroclaw-labs/zeroclaw/pull/2146) awaiting review |
| **S2** | [#2107](https://github.com/zeroclaw-labs/zeroclaw/issues/2107) | Anthropic model vision detection not working | ✅ Closed | Fixed |
| **S2** | [#2041](https://github.com/zeroclaw-labs/zeroclaw/issues/2041) / [#2032](https://github.com/zeroclaw-labs/zeroclaw/issues/2032) | Windows compile failure (duplicate reports) | ✅ Closed | [#2056](https://github.com/zeroclaw-labs/zeroclaw/pull/2056) awaiting review |
| **S2** | [#2048](https://github.com/zeroclaw-labs/zeroclaw/issues/2048) | Feishu WebSocket connects fine but messages get no response | ✅ Closed | Fixed |

**Key pattern**: **CJK/Chinese-language scenario stability** became today's focus — the UTF-8 truncation panic, PowerShell Chinese encoding, and agent intent-recognition failures ("promises to act but stops" in Chinese contexts) form a problem cluster, reflecting insufficient internationalization test coverage.

---

## 6. Feature Requests and Roadmap Signals

| Need | Issue/PR | Maturity | Likelihood of inclusion |
|:---|:---|:---:|:---:|
| **GitHub native channel** | [#2079](https://github.com/zeroclaw-labs/zeroclaw/issues/2079) | Requirement stage | ⭐⭐⭐⭐⭐ High (highly aligned with the project's positioning) |
| **ROS2 integration architecture** | [#1835](https://github.com/zeroclaw-labs/zeroclaw/issues/1835) | Discussion stage | ⭐⭐⭐⭐☆ High (clear robotics scenario) |
| **Economic agent system (Phase 1)** | [#2134](https://github.com/zeroclaw-labs/zeroclaw/pull/2134) | PR awaiting review | ⭐⭐⭐⭐☆ High (architecture-level feature) |
| **WASM plugin foundation** | [#1363](https://github.com/zeroclaw-labs/zeroclaw/pull/1363) | PR awaiting review (Feb 22) | ⭐⭐⭐⭐☆ High (extensibility infrastructure) |
| **Matrix channel Cron delivery** | [#2035](https://github.com/zeroclaw-labs/zeroclaw/pull/2035) | PR awaiting review | ⭐⭐⭐⭐☆ High (completes the channel matrix) |
| **Feishu native Cron delivery** | [#1715](https://github.com/zeroclaw-labs/zeroclaw/issues/1715) | Requirement stage | ⭐⭐⭐☆☆ Medium (enterprise-user demand) |
| **Perplexity filtering (GCG attack detection)** | [#1811](https://github.com/zeroclaw-labs/zeroclaw/issues/1811) | Requirement stage | ⭐⭐⭐☆☆ Medium (security enhancement) |
| **Slack rate-limit optimization** | [#1839](https://github.com/zeroclaw-labs/zeroclaw/issues/1839) | Requirement stage | ⭐⭐⭐☆☆ Medium (reliability optimization) |

**Roadmap signals**: enterprise-grade features (RBAC, auditing, economic tracking) and developer experience (GitHub channel, Copilot support) form a twin-engine drive, and the **"AI-native DevOps assistant"** positioning is clear.

---

## 7. User Feedback Summary

### ✅ Satisfaction points
- **Resource efficiency**: "[OpenClaw] 1.5GB RAM → ZeroClaw <5MB" ([#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88)) — the core differentiated value is validated
- **Responsiveness**: high Issue close rate; active community response

### ❌ Pain points
| Pain point | Source | Impact |
|:---|:---|:---|
| **Windows "second-class citizen" experience** | [#2041](https://github.com/zeroclaw-labs/zeroclaw/issues/2041), [#2032](https://github.com/zeroclaw-labs/zeroclaw/issues/2032), [#2072](https://github.com/zeroclaw-labs/zeroclaw/issues/2072) | Blocks enterprise Windows deployments |
| **Aggressive glibc version** | [#2084](https://github.com/zeroclaw-labs/zeroclaw/issues/2084), [#2083](https://github.com/zeroclaw-labs/zeroclaw/issues/2083) | Cannot run on Ubuntu 22.04/Debian 12, contradicting the "lightweight" positioning |
| **Chinese-language scenario reliability** | [#2060](https://github.com/zeroclaw-labs/zeroclaw/issues/2060), [#2105](https://github.com/zeroclaw-labs/zeroclaw/issues/2105), [#2146](https://github.com/zeroclaw-labs/zeroclaw/pull/2146) | Blocks production environments for CJK users |
| **Activation-system confusion** | [#2022](https://github.com/zeroclaw-labs/zeroclaw/issues/2022) | "Activation" prompts in an open source project raise trust doubts |

### 🎯 Use cases
- **Robotics/ROS2 integration** ([#1835](https://github.com/zeroclaw-labs/zeroclaw/issues/1835)): resource-constrained edge computing environments
- **Multi-AI sub-agent orchestration** ([#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88)): Claude Code session management
- **Enterprise IM integration**: Feishu, DingTalk, QQ group chats (notable demand in the Chinese market)

---

## 8. Pending Backlog

### ⚠️ Needs maintainer attention

| Type | Item | Age | Risk |
|:---|:---|:---:|:---|
| **PR** | [#1363](https://github.com/zeroclaw-labs/zeroclaw/pull/1363) WASM plugin foundation | 6 days | Architecture-level feature; blocks the extension ecosystem |
| **PR** | [#2134](https://github.com/zeroclaw-labs/zeroclaw/pull/2134) Economic agent system | 1 day | XL-sized; needs deep architectural review |
| **PR** | [#2139](https://github.com/zeroclaw-labs/zeroclaw/pull/2139) Codex transport-layer optimization | 1 day | High risk; affects core stability |
| **Issue** | [#88](https://github.com/zeroclaw-labs/zeroclaw/issues/88) Migration blocker checklist | 13 days | 20👍 production users; needs an official roadmap response |
| **Issue** | [#2079](https://github.com/zeroclaw-labs/zeroclaw/issues/2079) GitHub native channel | 1 day | High-value feature; a quick feasibility assessment is recommended |

**Suggested actions**: prioritize reviewing [#2056](https://github.com/zeroclaw-labs/zeroclaw/pull/2056) (Windows fix, unblocks S1-level issues) → [#2075](https://github.com/zeroclaw-labs/zeroclaw/pull/2075) (UTF-8 safe truncation) → [#1363](https://github.com/zeroclaw-labs/zeroclaw/pull/1363) (plugin infrastructure).

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw Project Report | 2026-02-28

> **Project**: [gaoyangz77/easyclaw](https://github.com/gaoyangz77/easyclaw) \
> **Positioning**: AI agent and personal AI assistant tool

---

## 1. Today at a Glance

EasyClaw's activity today was **low-to-medium**. The core movement was two patch releases in a row (v1.5.11, v1.5.12), showing the maintainer iterating quickly on fixes. On the community side there was only 1 Issue closed and no new PR activity; the project is overall in a **post-release stable observation period**. Notably, two consecutive small releases may hint at an urgent problem in v1.5.10 requiring a hotfix, so it is worth watching the differences between versions.

---

## 2. Releases

### 🔖 v1.5.12 & v1.5.11 released back-to-back

| Version | Released at | Notes |
|:---|:---|:---|
| [v1.5.12](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.5.12) | 2026-02-27 | Installation docs update (macOS Gatekeeper guidance) |
| [v1.5.11](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.5.11) | 2026-02-27 | Same as above |

**Update content analysis**:
- The two releases' notes are **completely identical**, both covering macOS installation troubleshooting documentation
- No concrete code changelog was provided (CHANGELOG missing)
- **Speculation**: v1.5.11 may have had a release problem (e.g. binary upload failure), hence the rushed push of v1.5.12

**⚠️ Key gap**: the actual code differences between versions are not public, so users cannot decide whether to upgrade. Suggested additions from the maintainer:
- A list of the specific bugs fixed
- Checksums (SHA256) for each version's binaries

---

## 3. Project Progress

**No code merge activity today** (PRs: 0 merged / 0 closed)

| Metric | Value | Status |
|:---|:---|:---|
| PRs pending merge | 0 | 🟢 No backlog |
| Merged today | 0 | ⚪ No progress |
| Code commit activity | Low | Only version tag pushes |

**Assessment**: the project produced **no functional progress** today and is in a documentation-maintenance and version-management phase.

---

## 4. Community Hotspots

### 🔥 The only active Issue: [#2](https://github.com/gaoyangz77/easyclaw/issues/2) model list sync problem

| Attribute | Details |
|:---|:---|
| Status | ✅ **Closed** |
| Author | @slowayear |
| Comments | 3 |
| Affected version | v1.5.10 (Windows) |
| Core request | After connecting the Bailian Coding Plan, the client model list does not match the officially supported list |

**Nature of the problem**: model availability data from the third-party AI platform (Bailian/Alibaba Cloud) has sync delays or filtering-logic differences versus the EasyClaw client's cached/hardcoded list.

**Community signals**:
- Users expect **real-time sync** of the official model list rather than manually updating the client
- In enterprise/developer scenarios, model availability directly affects workflows (the Coding Plan is a paid feature)

---

## 5. Bugs and Stability

| Severity | Issue | Status | Tracking |
|:---|:---|:---|:---|
| 🔶 **Medium** | Bailian Coding Plan model list mismatch | ✅ **Fixed** (v1.5.11+) | [#2](https://github.com/gaoyangz77/easyclaw/issues/2) |
| 🔷 **Low** | macOS Gatekeeper false "file is damaged" report | 📝 **Mitigated via documentation** | [v1.5.12 release notes](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.5.12) |

**Stability assessment**:
- No crash or data-loss reports
- The macOS signing issue is a **long-standing known limitation**; doc-based mitigation is not a root fix, and moving to Apple Developer signing is recommended

---

## 6. Feature Requests and Roadmap Signals

**No new feature requests today** (Issues: 0 opened)

**Potential needs derived from #2**:
| Need | User scenario | Implementation difficulty | Priority signal |
|:---|:---|:---|:---|
| Dynamic model list refresh | Auto-sync when switching API keys across platforms | Medium | ⭐⭐⭐ High (pain point for paying users) |
| Official platform model status indicator | Distinguish "available/rate-limited/deprecated" | Low | ⭐⭐⭐ High |
| Enterprise model allowlist | Teams centrally manage available models | Medium | ⭐⭐ Medium (B2B demand) |

---

## 7. User Feedback Summary

### Pain points distilled (from the [#2](https://github.com/gaoyangz77/easyclaw/issues/2) discussion)

| Dimension | Details |
|:---|:---|
| **Feature expectation gap** | After subscribing to the Bailian Coding Plan, users expect to immediately see all officially supported models; the missing entries create a "paid feature unusable" perception |
| **Opaque information** | Users cannot tell whether it is a client cache problem, a platform API restriction, or a configuration error |
| **Version-iteration awareness** | Users proactively followed up to v1.5.10 and still hit the problem, showing insufficient patch-version communication |

### Satisfaction signals
- ✅ Maintainer response was fairly fast (closed within 24 hours)
- ❌ The closed Issue did not state the fixing version, so users must verify on their own

---

## 8. Pending Backlog

| Type | Description | Risk | Suggested action |
|:---|:---|:---|:---|
| **Technical debt** | No public CHANGELOG | Hard upgrade decisions for users; eroding trust | Set up automated changelog generation |
| **Platform adaptation** | The unsigned macOS app keeps generating support burden | New-user churn; reputational impact | Apply for an Apple Developer account ($99/year) |
| **Documentation gap** | Missing explanation of differences between versions (v1.5.11 vs v1.5.12) | Community confusion | Add release notes or withdraw the redundant version |

---

## Health Score

| Dimension | Score | Notes |
|:---|:---|:---|
| Release cadence | ⭐⭐⭐⭐☆ | Fast iteration, but transparency needs improvement |
| Community response | ⭐⭐⭐⭐☆ | Timely Issue closure; communication details need work |
| Code activity | ⭐⭐☆☆☆ | No functional commits today |
| Documentation completeness | ⭐⭐⭐☆☆ | Install guidance improved; changelog missing |
| **Overall** | **3.0/5** | Stable maintenance phase; watch out for "release fatigue" |

---

*Daily report generated at: 2026-02-28* \
*Data source: GitHub API / public Releases / Issue tracking*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Report | 2026-02-28

---

## 1. Today at a Glance

LobsterAI kept up **a high iteration pace** today, handling **28 Issues** (7 closed) and **21 PRs** (16 merged) within 24 hours and releasing **v0.1.22**. Community activity is very high, with core pain points concentrated in three areas: **Ollama local model compatibility**, **Windows adaptation**, and **IM bot integration experience**. The dev team responded quickly, merging several key fixes the same day, but issues like Ollama connection problems, the enterprise-authentication barrier for Feishu/DingTalk, and Mac M1 install failures remain to be fully solved. The project is overall in a **rapid feature-expansion phase**, with stability fixes and multi-platform adaptation as the recent main themes.

---

## 2. Releases

### v0.1.22 released
| Attribute | Details |
|:---|:---|
| **Version** | v0.1.22 |
| **Release date** | 2026-02-27 |
| **Release link** | https://github.com/netease-youdao/LobsterAI/releases/tag/v0.1.22 |

#### Core updates
| Feature | Description | Related PRs |
|:---|:---|:---|
| **App auto-update** | The client can detect and install new versions, solving the previous pain point of "having to manually uninstall the old version" | [#154](https://github.com/netease-youdao/LobsterAI/pull/154), [#155](https://github.com/netease-youdao/LobsterAI/pull/155) |
| **Scheduled-task IM notification enhancements** | Supports rich-media sending (images/files, etc.) and persistent storage of notification targets | [#147](https://github.com/netease-youdao/LobsterAI/pull/147) |
| **About page** | New page displaying app information | [#159](https://github.com/netease-youdao/LobsterAI/pull/159) |

#### Migration notes
- **Overwrite-install problem**: [#169](https://github.com/netease-youdao/LobsterAI/issues/169) shows some users still need to uninstall the old version first; the auto-update mechanism may have edge cases
- **Config loss risk**: [#163](https://github.com/netease-youdao/LobsterAI/issues/163) reports Feishu binding info wiped after the update; users are advised to back up their configuration before upgrading

---

## 3. Project Progress

### Key PRs merged today (16)

| PR | Author | Core contribution | Impact assessment |
|:---|:---|:---|:---|
| [#149](https://github.com/netease-youdao/LobsterAI/pull/149) | @btc69m979y-dotcom | **Major Ollama experience improvements**: fixed the model edit form ambiguity ("model name" → actual model ID such as `qwen3:8b`); default baseUrl changed to `/v1` for OpenAI-format compatibility | ⭐⭐⭐ Solves the community's most painful issue |
| [#172](https://github.com/netease-youdao/LobsterAI/pull/172) | @sysusugan | **Antigravity OAuth integration**: new OAuth subsystem supporting third-party login and model sync | ⭐⭐⭐ Extends ecosystem connectivity |
| [#162](https://github.com/netease-youdao/LobsterAI/pull/162) | @Doge2077 | **Multiple custom model configurations**: supports configuring multiple Custom providers, avoiding same-name model conflicts | ⭐⭐⭐ Friendly to enterprise self-hosted deployments |
| [#158](https://github.com/netease-youdao/LobsterAI/pull/158) | @renhongchao | **NetEase Xiaomifeng integration**: new XiaomifengGateway supporting interaction with the NetEase Xiaomifeng personal digital assistant | ⭐⭐⭐ Connects within the NetEase ecosystem |
| [#152](https://github.com/netease-youdao/LobsterAI/pull/152) | @liugang519 | **Scheduled-task chat management**: new HTTP APIs and Skill scripts to view/modify/delete/start-stop tasks | ⭐⭐ Improves task-management flexibility |
| [#128](https://github.com/netease-youdao/LobsterAI/pull/128) | @Aoxiang-001 | **YUNXIN NIM enhancements**: rich-media messages (images/audio/video/files), hot config reload, account allowlist | ⭐⭐ Comprehensive IM capability upgrade |
| [#160](https://github.com/netease-youdao/LobsterAI/pull/160) | @fisherdaddy | **Fixed garbled Chinese text in WebSearch** | ⭐⭐ Stability fix |
| [#167](https://github.com/netease-youdao/LobsterAI/pull/167) | @fisherdaddy | **Fixed custom mailbox advanced-settings bug** | ⭐⭐ Improves mailbox feature usability |
| [#132](https://github.com/netease-youdao/LobsterAI/pull/132) | @btc69m979y-dotcom | **Moonshot Coding Plan + Zhipu fixes**: supports Kimi coding mode; fixed Zhipu Anthropic-format compatibility | ⭐⭐ Multi-provider support |
| [#107](https://github.com/netease-youdao/LobsterAI/pull/107) | @btc69m979y-dotcom | **Volcengine integration**: supports both Anthropic/OpenAI protocols, including a Coding Plan mode | ⭐⭐ Chinese cloud vendor coverage |
| [#115](https://github.com/netease-youdao/LobsterAI/pull/115) | @btc69m979y-dotcom | **Fixed Windows system commands not found**: ensures the System32 directory and environment variable passing | ⭐⭐ Key Windows compatibility fix |
| [#104](https://github.com/netease-youdao/LobsterAI/pull/104) | @btc69m979y-dotcom | **Fixed MiniMax API compatibility**: merges multiple system messages; fixed model identification | ⭐⭐ Third-party API stability |
| [#157](https://github.com/netease-youdao/LobsterAI/pull/157) | @btc69m979y-dotcom | **Fixed Moonshot Coding Plan endpoint switching** | ⭐⭐ Feature completeness |
| [#103](https://github.com/netease-youdao/LobsterAI/pull/103) | @btc69m979y-dotcom | **Fixed Windows file picker z-order issue** | ⭐ UX improvement |
| [#154](https://github.com/netease-youdao/LobsterAI/pull/154), [#155](https://github.com/netease-youdao/LobsterAI/pull/155) | @liuzhq1986 | **App auto-update feature** | ⭐⭐⭐ Version-management infrastructure |

**Overall progress assessment**: today's merged PRs span **6 major dimensions** — local model experience (Ollama), enterprise ecosystem integration (Xiaomifeng, Antigravity), multiple model providers (Volcengine, MiniMax, Moonshot, Zhipu), IM capabilities (NIM rich media), scheduled-task management, and Windows compatibility. The project is rapidly evolving from "features work" to "polished experience".

---

## 4. Community Hotspots

### Most-discussed Issues (sorted by comment count)

| Rank | Issue | Comments | Core request | Status |
|:---|:---|:---:|:---|:---|
| 1 | [#30](https://github.com/netease-youdao/LobsterAI/issues/30) Misleading Ollama model ID | 6 | **Docs/UX issue**: users are confused that the "model name" must exactly match the actual Ollama model name (e.g. `qwen3:8b`) to connect | ✅ Closed |
| 2 | [#89](https://github.com/netease-youdao/LobsterAI/issues/89) Adding a mailbox fails | 5 | **Feature usability**: 163/QQ mailbox IMAP/SMTP tests fail after configuration, and the feature's purpose is unclear (for skills vs. for IM chat) | 🔴 Open |
| 3 | [#102](https://github.com/netease-youdao/LobsterAI/issues/102) Feishu/DingTalk require enterprise review; asking for a low-barrier IM option | 3 | **Entry barrier**: individual developers cannot quickly onboard Feishu/DingTalk bots; calling for alternatives such as QQ bots | 🔴 Open |
| 4 | [#13](https://github.com/netease-youdao/LobsterAI/issues/13) Ollama unusable | 4 | **Basic feature blocked**: the configuration test succeeds but after saving it reports no API | ✅ Closed |
| 5 | [#18](https://github.com/netease-youdao/LobsterAI/issues/18) SiliconCloud API crash | 3 | **Third-party API compatibility**: the Cowork engine process exits | ✅ Closed |

### Analysis of underlying needs
- **Ollama local deployment is the core scenario**: 3 of the highly active Issues involve Ollama; users strongly want to cut token costs, but configuration barriers and stability issues keep tripping them up
- **The "last mile" of IM access**: enterprise IM requires organization review, leaving individual developers locked out; the community wants a more open onboarding path
- **Config-and-go expectations**: users expect it to "work once the parameters are filled in", not a deep understanding of model IDs, API formats, and other low-level concepts

---

## 5. Bugs and Stability

### Bugs reported today (sorted by severity)

| Severity | Issue | Description | Reproduction environment | Fix PR |
|:---|:---|:---|:---|:---:|
| 🔴 **P0-blocker** | [#153](https://github.com/netease-youdao/LobsterAI/issues/153) | **MacBook Pro M1 cannot open the app after installing the ARM64 build** | MacBook Pro (13-inch, M1, 2020) | ❌ None |
| 🔴 **P0-blocker** | [#144](https://github.com/netease-youdao/LobsterAI/issues/144) | **Win11 errors with 404 Not found, completely unusable** | Windows 11 | ❌ None |
| 🟡 **P1-severe** | [#164](https://github.com/netease-youdao/LobsterAI/issues/164) | **bash command output garbled via GBK encoding on Windows, so the AI cannot get any work done** | Windows + Chinese-language system | ❌ None (PowerShell suggested) |
| 🟡 **P1-severe** | [#150](https://github.com/netease-youdao/LobsterAI/issues/150) | **Ollama local deployment unusable** (still broken in v0.1.22) | General | [#149](https://github.com/netease-youdao/LobsterAI/pull/149) partial fix |
| 🟡 **P1-severe** | [#174](https://github.com/netease-youdao/LobsterAI/issues/174) | **Ollama unresponsive for long stretches / Request timed out** (unsuccessful from 0.1.17 to 0.1.22) | General | ❌ None |
| 🟡 **P1-severe** | [#175](https://github.com/netease-youdao/LobsterAI/issues/175) | **Private-cloud model Max_tokens parameter error** | DeepSeek/Qwen3 self-hosted deployments | ❌ None |
| 🟡 **P1-severe** | [#173](https://github.com/netease-youdao/LobsterAI/issues/173) | **Feishu IM messages stall and pile up; a restart is needed to recover** | Feishu integration | ❌ None |
| 🟡 **P1-severe** | [#163](https://github.com/netease-youdao/LobsterAI/issues/163) | **Feishu binding info lost after the update** | v0.1.22 upgrade | ❌ None |
| 🟡 **P1-severe** | [#165](https://github.com/netease-youdao/LobsterAI/issues/165) | **Feishu voice messages cannot be received** | Feishu integration | ❌ None |
| 🟡 **P1-severe** | [#166](https://github.com/netease-youdao/LobsterAI/issues/166) | **Lobster cannot tell where the user is coming from (client vs. Feishu)** | Multi-channel scenarios | ❌ None |
| 🟢 **P2-general** | [#169](https://github.com/netease-youdao/LobsterAI/issues/169) | **Overwrite install not possible; must uninstall first** | Windows | ✅ [#154](https://github.com/netease-youdao/LobsterAI/pull/154), [#155](https://github.com/netease-youdao/LobsterAI/pull/155) |
| 🟢 **P2-general** | [#146](https://github.com/netease-youdao/LobsterAI/issues/146) | **Windows built-in mail skill invocation fails** | Windows 11, v0.1.21 | ❌ None |
| 🟢 **P2-general** | [#148](https://github.com/netease-youdao/LobsterAI/issues/148) | **Midscene skill execution error (screenshot failure)** | Windows + local sandbox | ❌ None |
| 🟢 **P2-general** | [#151](https://github.com/netease-youdao/LobsterAI/issues/151) | **Cannot send images/files to the Telegram bot** | Telegram integration | ❌ None |
| 🟢 **P2-general** | [#156](https://github.com/netease-youdao/LobsterAI/issues/156) | **No typing indicator while chatting over Telegram** | Telegram integration | ❌ None |
| 🟢 **P2-general** | [#161](https://github.com/netease-youdao/LobsterAI/issues/161) | **Cannot change the working directory from a conversation** | Telegram bot | ❌ None |

### Regression risk warnings
- **Recurring Ollama issues**: after [#30](https://github.com/netease-youdao/LobsterAI/issues/30) and [#13](https://github.com/netease-youdao/LobsterAI/issues/13) were closed, [#150](https://github.com/netease-youdao/LobsterAI/issues/150) and [#174](https://github.com/netease-youdao/LobsterAI/issues/174) report new problems, showing the fixes did not cover every scenario
- **Feishu integration stability**: problems exposed at multiple points — message stalling, unsupported voice, context-source recognition failures — so IM channel robustness needs strengthening

---

## 6. Feature Requests and Roadmap Signals

### New feature requests today

| Issue | Request | User scenario | Feasibility assessment |
|:---|:---|:---|:---|
| [#176](https://github.com/netease-youdao/LobsterAI/issues/176) | **Task record grouping, notes feature, built-in Skill editing, TODO list** | Task management, knowledge accumulation, closed-loop workflows | ⭐⭐⭐ High priority; fits the product positioning |
| [#168](https://github.com/netease-youdao/LobsterAI/issues/168) | **Built-in strong-math Skill** | Research and engineering computation scenarios | ⭐⭐ Medium; can rely on external model capabilities |
| [#102](https://github.com/netease-youdao/LobsterAI/issues/102) | **Low-barrier IM access such as QQ bots** | Individual developers bypassing enterprise review | ⭐⭐⭐ High priority; strong community demand |
| [#161](https://github.com/netease-youdao/LobsterAI/issues/161) | **Dynamically change the working directory within a conversation** | Flexible operation in Telegram and other IM scenarios | ⭐⭐ Medium; technically simple |

### Roadmap signals
- **Likely to land soon** (PR exists or strongly related):
  - Multiple custom model configurations → [#162](https://github.com/netease-youdao/LobsterAI/pull/162) submitted
  - Task management enhancements → [#152](https://github.com/netease-youdao/LobsterAI/pull/152) base capability merged
  - Xiaomifeng integration → [#158](https://github.com/netease-youdao/LobsterAI/pull/158) submitted
 \
- **Mid-term planning signals**:
  - Notes feature, TODO list: strong synergy potential with the Youdao Cloud Notes ecosystem
  - Math Skill: consider integrating WolframAlpha or a dedicated math model

---

## 7. User Feedback Summary

### Real pain points (verbatim quotes)

| Scenario | User quote | Sentiment |
|:---|:---|:---:|
| **Repeated Ollama failures** | "From v0.1.17 all the way to v0.1.22, not a single successful run" | 😠 Frustrated |
| **Update wipes config** | "I tuned seven or eight scheduled tasks, and all that tuning was wasted" | 😠 Angry |
| **Windows garbled text** | "The bash command line returns tons of garbled text, so on Windows the AI model cannot get any work done" | 😠 Blocked |
| **Enterprise IM barrier** | "Both Feishu bots and DingTalk bots require enterprise organization review" | 😕 Confused |
| **Config ambiguity** | "This ID has to match the model name exactly to get anything back" | 😕 Confused |

### Satisfaction points
- **Recognition of iteration speed**: "Lobster has been shipping a version every day lately; you can tell they are fixing issues very quickly"
- **Interest in feature potential**: users express interest in scheduled tasks, multi-IM access, and other capabilities

### Key usage scenarios
1. **Low-cost local deployment**: Ollama + open source models is a frequent request, used to cut agent token consumption
2. **Personal automation**: scheduled tasks + IM notifications, replacing IFTTT/Shortcuts
3. **Cross-platform workflows**: Windows dev environment + collaboration with Feishu/DingTalk mobile

---

## 8. Pending Backlog

### Important Issues needing maintainer attention

| Issue | Created | Problem | Priority | Suggested action |
|:---|:---:|:---|:---:|:---|
| [#153](https://github.com/netease-youdao/LobsterAI/issues/153) | 02-27 | Mac M1 install failure | 🔴 P0 | Verify ARM64 build signing/notarization |
| [#144](https://github.com/netease-youdao/LobsterAI/issues/144) | 02-27 | Win11 404 error | 🔴 P0 | Investigate the Claude Code process startup failure |
| [#174](https://github.com/netease-youdao/LobsterAI/issues/174) | 02-28 | Ollama unresponsive for long stretches | 🟡 P1 | Reproduce and add timeout/retry mechanisms |
| [#102](

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Report | 2026-02-28

## 1. Today at a Glance

ZeptoClaw maintained moderate activity today. Core maintainer @qhkm pushed forward a key MCP (Model Context Protocol) infrastructure milestone — the stdio transport implementation has been merged. Community contributor @superhero75 raised the need for dynamic LLM endpoint switching in Telegram scenarios, reflecting a real pain point in multi-model deployments. The dependency-maintenance PR is still waiting to be merged, and supply chain security hardening remains pending. Overall the project is in a feature-iteration phase, with MCP ecosystem integration steadily strengthening.

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### ✅ Merged/closed PRs

| PR | Author | Core contribution | Value for the project |
|:---|:---|:---|:---|
| [#192](https://github.com/qhkm/zeptoclaw/pull/192) | @qhkm | **Complete MCP stdio transport implementation** | Milestone-level progress: completed the full chain of transport abstraction (McpTransport trait), dual-mode support (HTTP/stdio), client refactor, and service discovery registration |

**Technical details:**
- Introduced the `McpTransport` trait to decouple the transport layer
- Added `StdioTransport` for local process communication scenarios
- `McpClient` refactored into a transport-agnostic architecture, supporting `new_stdio()` construction and graceful shutdown
- Extended the MCP service discovery mechanism to support explicit transport-type annotation

**Significance:** This PR fully implements the [2026-02-27 technical plan document](https://github.com/qhkm/zeptoclaw/blob/main/docs/plans/2026-02-27-mcp-stdio-transport.md), making ZeptoClaw one of the few AI assistant frameworks supporting both HTTP and stdio dual-mode MCP, laying the foundation for plugging into local tool ecosystems (such as Claude Desktop and various CLI tools).

---

## 4. Community Hotspots

### 🔥 Most active discussion: dynamic LLM endpoint switching

| Issue | Author | Activity metric | Core request |
|:---|:---|:---|:---|
| [#193](https://github.com/qhkm/zeptoclaw/issues/193) | @superhero75 | 1 new comment | **Hot-switching of models/endpoints in mobile scenarios** |

**In-depth analysis:**

This request exposes a typical production pain point:
- **Scenario:** users hit LLM provider rate limits while using ZeptoClaw over Telegram
- **Pain point:** the current architecture lacks a runtime endpoint-switching mechanism, forcing conversations to be interrupted or quota recovery to be awaited
- **Request:** follow OpenClaw's design — `/models` lists available endpoints and `/model <name>` switches instantly

**Anticipated technical challenges:**
- State management: consistency guarantees when migrating conversation context across endpoints
- Hot config reload: dynamic configuration updates without restarting the service
- Failover: designing automatic degradation and retry strategies

**Roadmap signal:** this feature fits closely with ZeptoClaw's multi-modal, multi-provider architectural direction; it is recommended for inclusion in v0.x prioritization.

---

## 5. Bugs and Stability

**No new bug reports or crash Issues today**

| Category | Count | Status |
|:---|:---|:---|
| Crashes/severe defects | 0 | - |
| Feature regressions | 0 | - |
| Performance issues | 0 | - |

> Note: dependency update PR #183 includes clippy warning fixes, a preventive code-quality improvement.

---

## 6. Feature Requests and Roadmap Signals

| Issue | Type | Likelihood assessment | Key dependencies |
|:---|:---|:---|:---|
| [#193](https://github.com/qhkm/zeptoclaw/issues/193) Telegram LLM endpoint hot-switching | Interaction enhancement | ⭐⭐⭐⭐☆ High | Config system refactor, session state management |
| [#191](https://github.com/qhkm/zeptoclaw/issues/191) MCP stdio transport | Infrastructure | ✅ **Completed** | - |

**Inferred next-release candidate features:**

Based on the MCP stdio capability merged today, the project may extend in the following directions:
1. **MCP tool marketplace/registry:** standardized tool discovery and distribution mechanisms
2. **Multi-LLM routing layer:** intelligent load balancing and failover (echoing the #193 request)
3. **Local-first deployment:** offline/privacy-sensitive scenario support built on stdio transport

---

## 7. User Feedback Summary

### Real pain points distilled from #193

> *"Most llm endpoints have rate limit, it is difficult to switch to another model/endpoint on the road"*

| Dimension | Feedback |
|:---|:---|
| **Usage scenario** | Mobile scenarios (Telegram), multi-provider deployments, rate-limit avoidance |
| **Satisfaction** | ZeptoClaw's Telegram integration already covers basic interaction needs |
| **Dissatisfaction** | Insufficient ops flexibility: endpoint switching requires a restart or editing config files |
| **Competitor reference** | Explicitly cites OpenClaw's `/models` + `/model` command design as the expected benchmark |

**Product insight:** users position ZeptoClaw as a "portable AI assistant"; elasticity and resilience in mobile scenarios become a differentiating competitive point.

---

## 8. Pending Backlog

### ⏳ Long-term items needing maintainer attention

| PR/Issue | Created | Status | Risk/suggested action |
|:---|:---|:---|:---|
| [#183](https://github.com/qhkm/zeptoclaw/pull/183) Update dependencies | 2026-02-26 | **Open, pending merge** | 🔶 **Supply chain security priority**<br>Includes: full-chain updates for cargo/npm/Docker/Actions, Dependabot configuration, supply chain hardening (pinning + cooldown). Review within 48h recommended to avoid dependency drift. |

---

## Appendix: Data Quick Reference

| Metric | Value |
|:---|:---|
| 24h Issue updates | 2 (1 opened / 1 closed) |
| 24h PR updates | 2 (1 pending merge / 1 merged) |
| Releases | 0 |
| Active contributors | 2 (@qhkm, @superhero75, @reneleonhardt) |

---

*Report generated at: 2026-02-28* \
*Data source: GitHub API / ZeptoClaw official repository*

</details>

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Report | 2026-02-28

## 1. Today at a Glance

NanoBot maintained **high activity** today: 32 Issue updates (25 active/7 closed) and 72 PR updates (40 pending merge/32 processed) within 24 hours, with no new release. The community focused on **stability fixes** (empty-message crashes, context duplication) and **multi-platform adaptation** (Feishu streaming output, QQ message replies, Discord voice), while security PRs (sensitive data masking) and developer-experience improvements (token usage statistics, CI image builds) advanced in parallel. Overall the project is in a **feature expansion phase**, but with 40 backlogged PRs, merge pressure is significant.

---

## 2. Releases

**None** — no new version released today.

---

## 3. Project Progress

### Key merged/closed PRs

| PR | Author | Core contribution | Impact |
|:---|:---|:---|:---|
| [#1239](https://github.com/HKUDS/nanobot/pull/1239) | @tanishra | **Fixed Matrix channel initialization** — completed ChannelManager configuration and instantiation logic | Resolved the Matrix channel being completely unusable; corresponds to Issue #1300 |
| [#1293](https://github.com/HKUDS/nanobot/pull/1293) | @Re-bin | **Mistral API compatibility fix** — generates 9-character alphanumeric tool_call_ids | Fixed multi-turn conversation failures with Mistral models |
| [#1200](https://github.com/HKUDS/nanobot/pull/1200) | @intelliot | **Heartbeat test architecture update** — adapted to the two-phase tool-call architecture; removed the deprecated HEARTBEAT_OK_TOKEN | Resolved test code drifting from the main architecture (corresponds to Issue #1221) |
| [#1242](https://github.com/HKUDS/nanobot/issues/1242) | @rcolomina | **Telegram multi-image message fix** — correctly handles media_group_id grouped messages | Fixed the bug where only the last image was saved |

**Overall progress**: infrastructure (tests, CI, channel adaptation) is solid, and the core agent architecture is evolving toward **observability** (token statistics) and **security** (data masking).

---

## 4. Community Hotspots

### Highly discussed Issues

| Rank | Issue | Comments | Core request | Analysis |
|:---|:---|:---:|:---|:---|
| 1 | [#215 Feishu cannot establish a long connection](https://github.com/HKUDS/nanobot/issues/215) | 20 | Feishu still shows "long connection not established" after event subscription configuration | **A blocking problem for enterprise users**; there is a gap between configuration docs and runtime behavior, and the difference between long-connection and callback modes needs clarifying |
| 2 | [#1240 llama3.3-70b-instruct infinite response loop](https://github.com/HKUDS/nanobot/issues/1240) | 13 | Model responses never stop; keeps repeating prompts in the background | **A serious stability problem**; possibly a flaw in stop tokens or tool-loop termination logic |
| 3 | [#222 Multi-agent setup support](https://github.com/HKUDS/nanobot/issues/222) | 6 👍5 | Asking about multi-agent architecture support status and documentation | **An architecture-level need**; the community clearly expects complex workflow orchestration and needs an official Roadmap response |
| 4 | [#1265 Real-world Windows comparison with OpenClaw and suggestions](https://github.com/HKUDS/nanobot/issues/1265) | 4 | Affirms NanoBot's native Windows support advantage; suggests strengthening the differentiation | **A strategic signal** — the Windows user experience is a core competitive advantage and should be protected first |

### High-value PR discussions

| PR | Highlight | Status |
|:---|:---|:---|
| [#1080 Feishu CardKit streaming output](https://github.com/HKUDS/nanobot/pull/1080) | Real-time streaming cards + media embedding; a step change for enterprise UX | Pending merge (related to the #215 problem) |
| [#1238 AgentSkills.io standard compatibility](https://github.com/HKUDS/nanobot/pull/1238) | Ecosystem interoperability breakthrough; can reuse HuggingFace/Anthropic skill libraries | Pending merge |
| [#1305 Automatic sensitive-data masking](https://github.com/HKUDS/nanobot/pull/1305) | A key security/compliance capability with a three-layer defense design | Pending merge (duplicates #1249; needs coordination) |

---

## 5. Bugs and Stability

| Severity | Issue | Description | Fix PR | Status |
|:---|:---|:---|:---|:---|
| 🔴 **Critical** | [#1240](https://github.com/HKUDS/nanobot/issues/1240) | llama3.3-70b infinite loop; forced interruption required | None | **Pending investigation** — suspected failure of the tool-loop termination condition |
| 🔴 **Critical** | [#1309](https://github.com/HKUDS/nanobot/pull/1309) | Empty Telegram messages cause crash loops + context duplication | [#1309](https://github.com/HKUDS/nanobot/pull/1309) | **Pending merge** — isolated to Moonshot/Kimi K2.5 large-context scenarios |
| 🟡 **High** | [#1267](https://github.com/HKUDS/nanobot/issues/1267) | Zhipu AI (zhipu) provider does not work; reports insufficient balance | None | Pending verification — possibly a config format or API change |
| 🟡 **High** | [#1225](https://github.com/HKUDS/nanobot/issues/1225) | deepseek-reasoner request format error; missing reasoning_content | None | Pending fix — incomplete reasoning-model adaptation |
| 🟡 **High** | [#1274](https://github.com/HKUDS/nanobot/issues/1274) | Windows absolute-path regex truncation; legitimate commands falsely intercepted | None | Pending fix — workspace isolation security policy flaw |
| 🟡 **High** | [#1303](https://github.com/HKUDS/nanobot/issues/1303) | `content: null` messages pollute session history and cause subsequent requests to fail | None | **Newly reported** — missing edge-case handling |
| 🟢 **Medium** | [#1192](https://github.com/HKUDS/nanobot/issues/1192) | Bifrost MCP Gateway Code Mode 400 error | None | External compatibility problem |
| 🟢 **Medium** | [#1174](https://github.com/HKUDS/nanobot/issues/1174) | Local model in-memory merging takes too long or fails | None | Architectural performance issue; needs async processing or a degradation strategy |

---

## 6. Feature Requests and Roadmap Signals

| Need | Issue/PR | Technical direction | Likelihood of inclusion |
|:---|:---|:---|:---|
| **OpenAI-compatible API endpoint** | [#1268](https://github.com/HKUDS/nanobot/issues/1268) | Expose NanoBot as a service downstream tools can connect to | ⭐⭐⭐ High — key to expanding its ecosystem niche |
| **Per-session workspace isolation** | [#1302](https://github.com/HKUDS/nanobot/issues/1302) | Multi-user/multi-task filesystem sandbox | ⭐⭐⭐ High — foundation for security and multi-tenancy |
| **Telegram real-time model switching** | [#1292](https://github.com/HKUDS/nanobot/issues/1292) | Runtime LLM endpoint switching to handle rate limits | ⭐⭐⭐ High — a hard requirement for the ops experience |
| **Web chat UI** | [#1297](https://github.com/HKUDS/nanobot/pull/1297) | Flask + SSE multi-session Web UI | ⭐⭐⭐ High — PR submitted, awaiting review |
| **Discord voice/TTS** | [#1306](https://github.com/HKUDS/nanobot/pull/1306) | Audio input transcription + voice replies | ⭐⭐⭐ High — PR submitted |
| **Cursor/GH CLI integration** | [#1299](https://github.com/HKUDS/nanobot/pull/1299) | Configurable integration with the Cursor coding workflow | ⭐⭐ Medium — depends on external tool installation |
| **Model-initiated turn ending** | [#1246](https://github.com/HKUDS/nanobot/pull/1246) | Explicit `end_turn` tool to improve task completion | ⭐⭐ Medium — behavior design needs validation |
| **Multi-model provider failover** | [#1201](https://github.com/HKUDS/nanobot/pull/1201) | Automatic fallback to a backup model when the primary fails | ⭐⭐ Medium — reliability enhancement |

---

## 7. User Feedback Summary

### ✅ Satisfaction points
- **Native Windows support** ([#1265](https://github.com/HKUDS/nanobot/issues/1265)): unlike OpenClaw, which needs WSL, NanoBot works out of the box, with better install success rates and responsiveness
- **Skill installation flexibility**: the `nanobot` skill system, once tuned, is more usable than competitors'

### ❌ Pain points
- **Insufficient enterprise IM adaptation docs**: problems like Feishu long-connection configuration ([#215](https://github.com/HKUDS/nanobot/issues/215)) and DingTalk group-chat replies going out as private messages ([#1045](https://github.com/HKUDS/nanobot/issues/1045)) lack clear guidance
- **Windows edge-case experience**: "sometimes there are issues" ([#1251](https://github.com/HKUDS/nanobot/issues/1251)); details like path handling and permissions need polish
- **Fragmented model adaptation**: Zhipu, DeepSeek reasoning models, Mistral, and others all have compatibility issues; maintaining the provider ecosystem is costly
- **Session/memory management**: merge failures in large-context scenarios ([#1174](https://github.com/HKUDS/nanobot/issues/1174)) and history pollution ([#1176](https://github.com/HKUDS/nanobot/issues/1176)) hurt long-term use

### 💡 Scenario insights
- **Mobile ops needs**: users want to switch models in real time via Telegram ([#1292](https://github.com/HKUDS/nanobot/issues/1292)) instead of SSH-ing in to edit config — hinting at the need for a **more complete mobile management interface**

---

## 8. Pending Backlog

| Type | Item | Created | Risk | Suggested action |
|:---|:---|:---:|:---|:---|
| Issue | [#215 Feishu long connection](https://github.com/HKUDS/nanobot/issues/215) | 2026-02-06 (22 days) | Enterprise-user churn | Assign an owner; verify and close together with PR #1080 |
| Issue | [#222 Multi-agent support](https://github.com/HKUDS/nanobot/issues/222) | 2026-02-06 (22 days) | Unclear Roadmap | Respond officially with architecture plans; convert community contributions |
| Issue | [#1131 CI Test Coverage](https://github.com/HKUDS/nanobot/issues/1131) | 2026-02-24 (4 days) | Missing quality infrastructure | Clarify the CI strategy; add documentation |
| PR | [#126 Automated Docker image builds](https://github.com/HKUDS/nanobot/pull/126) | 2026-02-05 (23 days) | Release efficiency bottleneck | Review and merge; establish an official image channel |
| PR | [#1080 Feishu streaming output](https://github.com/HKUDS/nanobot/pull/1080) | 2026-02-24 (4 days) | Enterprise UX improvements blocked | Prioritize review; resolve the issue related to #215 |
| PR | [#1238 AgentSkills.io compatibility](https://github.com/HKUDS/nanobot/pull/1238) | 2026-02-26 (2 days) | Ecosystem expansion window | Review quickly; seize a voice in the skill standard |

---

**Daily report generated at**: 2026-02-28 \
**Data source**: HKUDS/nanobot public GitHub activity

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Report | 2026-02-28

## 1. Today at a Glance

PicoClaw kept up **an intense development pace** today, with **29 Issue updates** (16 active/newly opened, 13 closed) and **91 PR updates** (57 pending merge, 34 merged/closed) within 24 hours, and no new release. The project's core concerns concentrate on **multi-channel expansion** (WhatsApp, WeCom, Google Chat, HTTP), **MCP protocol integration**, and **stability fixes** (memory leaks, tool-call context loss). Community demand for Model Context Protocol (#290) and the Signal channel (#41) is strong, reflecting users' hopes for an open ecosystem and a privacy-first platform.

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### Notable merged/closed PRs

| PR | Author | Core contribution | Project progress |
|:---|:---|:---|:---|
| [#860](https://github.com/sipeed/picoclaw/pull/860) | @jayzen33 | **Enhanced system prompt**: explicitly instructs the Agent to update SOUL.md and USER.md | Resolves the long-standing pain point of "the Agent not remembering user information"; improves personalization |
| [#476](https://github.com/sipeed/picoclaw/pull/476) | @harshbansal7 | **Telegram message chunking**: implements safe 4096-character truncation while preserving Markdown structure | Fixes long-message crashes on Discord/Telegram; a channel stability milestone |
| [#840](https://github.com/sipeed/picoclaw/pull/840) | @omrikiei | **Fixed Telegram username allowlist regression**: restores passing senderID with the username | Fixes the security feature breakage introduced by #164 |
| [#622](https://github.com/sipeed/picoclaw/pull/622) | @JaviLib | **HTTP channel** (continuing iteration): web interface with built-in Goldmark rendering | Lowers the entry barrier for new users, achieving "install and access" |

**Overall assessment**: today's merges focused on **user-experience fixes** (memory, message length, allowlist) and **infrastructure** (web interface), a solid step toward production readiness.

---

## 4. Community Hotspots

### Most-discussed Issues

| Issue | Comments | Core request | Deeper signal |
|:---|:---|:---|:---|
| [#88](https://github.com/sipeed/picoclaw/issues/88) Chromebook installation guide | 10 | Docs missing; Chromebook users cannot get started | **Emerging-market user groups** are being overlooked; installation doc coverage needs expanding |
| [#680](https://github.com/sipeed/picoclaw/issues/680) GLM default api_base hardcoded | 9 | Insufficient configuration flexibility; hard to switch between providers | Configuration-system architectural debt; the provider resolution logic needs refactoring |
| [#100](https://github.com/sipeed/picoclaw/issues/100) Troubled by "no response" messages | 9 | OpenRouter models return empty content; poor user experience | Needs better **model output quality detection** and **graceful degradation** mechanisms |
| [#545](https://github.com/sipeed/picoclaw/issues/545) Multiple replies after task delegation | 8 | Message storms during multi-agent collaboration | Side effects of the **multi-agent architecture** are showing; coordination mechanisms needed |

### High-priority roadmap topics

| Issue | 👍 | Strategic significance |
|:---|:---|:---|
| [#290](https://github.com/sipeed/picoclaw/issues/290) **MCP protocol support** | 4 | Core to ecosystem expansion; PR #282 already in progress |
| [#41](https://github.com/sipeed/picoclaw/issues/41) **Signal channel** | 4 | A key need for privacy-first users; no implementation yet |
| [#621](https://github.com/sipeed/picoclaw/issues/621) Channel system refactor | 4 | Solves channel scalability at the architecture level; 83% complete |

---

## 5. Bugs and Stability

| Severity | Issue/PR | Problem description | Status |
|:---|:---|:---|:---|
| 🔴 **High** | [#870](https://github.com/sipeed/picoclaw/issues/870) | `forceCompression` breaks tool call/response pairing, causing 400 errors | **Pending fix**; affects long-conversation scenarios |
| 🔴 **High** | [#884](https://github.com/sipeed/picoclaw/pull/884) | WhatsApp Native channel memory leak (QR loop blocking, goroutine leaks) | **PR submitted**, pending merge |
| 🔴 **High** | [#781](https://github.com/sipeed/picoclaw/pull/781) | ExecTool regex error causes a "Fail-Open" security vulnerability | **PR open**; security-critical |
| 🟡 **Medium** | [#794](https://github.com/sipeed/picoclaw/issues/794) | Codex API 400 Bad Request (Device Auth mode) | Pending investigation; possibly a headers issue |
| 🟡 **Medium** | [#778](https://github.com/sipeed/picoclaw/issues/778) | Summarization loses tool-call context | **Being fixed in PR #829** |
| 🟡 **Medium** | [#888](https://github.com/sipeed/picoclaw/issues/888) | `picoclaw cron` CLI does not save tasks to jobs.json | **Closed**; fix needs verification |
| 🟢 **Low** | [#565](https://github.com/sipeed/picoclaw/issues/565) | Telegram `/list models` prompts to update config.yaml (actually .json) | **Closed** |

**Stability trend**: memory management and context compression are today's focus, reflecting the project entering a **long-session stability** push.

---

## 6. Feature Requests and Roadmap Signals

### Strong user demand (no existing PR)

| Issue | Need | Likelihood of inclusion | Blocker |
|:---|:---|:---|:---|
| [#41](https://github.com/sipeed/picoclaw/issues/41) Signal channel | Privacy-first messaging platform | ⭐⭐⭐⭐⭐ | Requires signal-cli integration; moderate effort |
| [#99](https://github.com/sipeed/picoclaw/issues/99) WhatsApp channel | Closed, but demand persists | ⭐⭐⭐⭐☆ | Official API restrictions; community solutions exist |
| [#850](https://github.com/sipeed/picoclaw/issues/850) Webhook messages | Event notifications from external systems | ⭐⭐⭐⭐☆ | Requires designing an authentication mechanism |
| [#869](https://github.com/sipeed/picoclaw/issues/869) Service start/stop commands | Ops convenience | ⭐⭐⭐☆☆ | Overlaps with the existing systemd PR #879 |

### Features backed by existing PRs (high probability for the next version)

| PR | Feature | Status |
|:---|:---|:---|
| [#282](https://github.com/sipeed/picoclaw/pull/282) | **MCP tool support** + Docker deployment | Open, active comments |
| [#879](https://github.com/sipeed/picoclaw/pull/879) | **Self-debugging skill** + Systemd service | Open, stability-oriented |
| [#872](https://github.com/sipeed/picoclaw/pull/872) | **WeCom AIBot channel** | Open, thoroughly tested |
| [#830](https://github.com/sipeed/picoclaw/pull/830) | **Google Chat channel** | Open |
| [#822](https://github.com/sipeed/picoclaw/pull/822) | **Tongyi Qianwen OAuth + QR code login** | Open; lowers the barrier for users in China |

---

## 7. User Feedback Summary

### 😊 Satisfaction points
- **Multi-channel coverage**: users are highly satisfied with the Telegram and Discord integrations; the "tiny beast" nickname shows affection (#99)
- **CLI interaction**: smooth single-task execution; the config-and-go experience is well received

### 😤 Pain points
| Pain point | Typical feedback | Source |
|:---|:---|:---|
| **Complex configuration** | "Tweaked it back and forth and nothing works anywhere" — MiniMax/GLM and other Chinese models are hard to configure | #878, #795, #680 |
| **Long-conversation crashes** | Length limits frequently triggered before message chunking; Discord/Telegram errors | #285, #545 |
| **Missing memory** | The Agent does not proactively update SOUL.md/USER.md; users must repeatedly state preferences | Before the #860 fix |
| **Docs lag** | No Chromebook installation guide; config examples do not match the actual file format | #88, #565 |
| **Poor summarization quality** | "Summary contains no relevant context" — tool-call history is lost | #778 |

### 💡 Usage scenario insights
- **Enterprise users**: need enterprise IM integrations such as WeCom (#872) and Google Chat (#830)
- **Privacy-sensitive users**: strong demand for Signal (#41); they reject Telegram/WhatsApp
- **Developers in China**: adaptation of Tongyi Qianwen, MiniMax, GLM, and other Chinese models is a hard requirement
- **Ops scenarios**: Systemd service support (#879) and Webhook event notifications (#850) are emerging needs

---

## 8. Pending Backlog

### Important topics long awaiting a response

| Issue | Created | Last updated | Risk | Suggested action |
|:---|:---|:---|:---|:---|
| [#290](https://github.com/sipeed/picoclaw/issues/290) MCP protocol support | 2026-02-16 | Today | ⭐⭐⭐⭐⭐ Ecosystem strategy | Coordinate the PR #282 review; set a clear merge timeline |
| [#41](https://github.com/sipeed/picoclaw/issues/41) Signal channel | 2026-02-11 | Today | ⭐⭐⭐⭐☆ Privacy-user churn | Label `help wanted` or add it to the roadmap |
| [#348](https://github.com/sipeed/picoclaw/issues/348) General attachment support | 2026-02-17 | Today | ⭐⭐⭐⭐☆ Feature completeness | Coordinate the design with the channel refactor #621 |
| [#868](https://github.com/sipeed/picoclaw/issues/868) Two-layer architecture proposal | Today | Today | ⭐⭐⭐⭐☆ Architecture evolution | Technical review; respond to the nanobot reference |
| [#297](https://github.com/sipeed/picoclaw/issues/297) Mantis shrimp logo design | 2026-02-16 | Today | ⭐⭐☆☆☆ Branding | Community design call or outsourcing |

### PR review bottleneck

- Among the **57 PRs pending merge**, priority attention should go to:
  - Security fixes: #781 (Fail-Open vulnerability)
  - Stability: #884 (memory leak), #829 (context loss)
  - Ecosystem expansion: #282 (MCP), #872 (WeCom)

---

**Report generated at**: 2026-02-28 \
**Data source**: GitHub API /sipeed/picoclaw \
**Next to watch**: MCP PR merge progress, community response to the Signal channel, and better docs for configuring Chinese models

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Report | 2026-02-28

## 1. Today at a Glance

NanoClaw showed **intense development activity** today: 37 PR updates (29 pending merge, 8 processed) point to explosive growth in community contributions. The core architecture refactor #500 (pluggable multi-channel architecture) keeps evolving, driving dense iteration on channel skills such as Signal, Discord, and Telegram. On stability, issues like WhatsApp connection recovery and container execution failures received targeted fixes, but the security hazard of lacking a user-level task cancellation mechanism was exposed for the first time. Overall project health is good, with technical-debt cleanup and feature expansion advancing in parallel.

---

## 2. Releases

**No new release**

---

## 3. Project Progress

### Notable PRs merged/closed today

| PR | Author | Core contribution | Significance for the project |
|:---|:---|:---|:---|
| [#568](https://github.com/qwibitai/nanoclaw/pull/568) | @nickpourazima | **Channel-agnostic interaction abstraction layer** (closed, superseded by #569) | Lays the interface foundation for unified cross-channel interactions (reactions, replies, votes, etc.) |
| [#339](https://github.com/qwibitai/nanoclaw/pull/339) | @tglowaski | **iMessage channel** (closed) | An attempt at Apple ecosystem integration; though closed, it accumulated experience containerizing iMessage |
| [#547](https://github.com/qwibitai/nanoclaw/pull/547) | @jonazri | **Shabbat Mode** 🕯️ (closed) | Cultural-inclusion innovation, showing the project's responsiveness to special-scenario needs |
| [#511](https://github.com/qwibitai/nanoclaw/pull/511) | @jonazri | **Voice recognition skill** (PyAnnote speaker identification) (closed) | Security-layer enhancement preventing voice commands from being abused by third parties |
| [#515](https://github.com/qwibitai/nanoclaw/pull/515) | @jonazri | **Perplexity Research skill** (closed) | Integrates deep-research capability, expanding the agent's information-gathering dimensions |
| [#509](https://github.com/qwibitai/nanoclaw/pull/509) | @jonazri | **WhatsApp emoji reaction skill** (closed) | A non-verbal feedback channel improving perceived UX during long tasks |
| [#563](https://github.com/qwibitai/nanoclaw/pull/563) | @antonlobanovskiy | **Discord skill invite flow fix** (closed) | Fixed the broken OAuth2 flow, lowering the onboarding barrier for new users |

**Overall progress assessment**: the 7 PRs closed today concentrate on three dimensions — **user-experience optimization** (Discord invite flow), **security hardening** (voice recognition), and **feature expansion** (research capability, emoji reactions). Notably, several innovative features (Shabbat Mode, the voice security layer) were closed, but their code may have been absorbed or may be awaiting resubmission after a refactor, showing the community's commitment to code quality.

---

## 4. Community Hotspots

### Analysis of high-attention PRs

| PR | Activity metric | Core request analysis |
|:---|:---|:---|
| [#500](https://github.com/qwibitai/nanoclaw/pull/500) | Core architecture refactor, driving 4+ derivative PRs | **Technical-debt cleanup**: decoupling the hardcoded WhatsApp-centric architecture into a pluggable channel system — the pivotal leap for the project evolving from a "WhatsApp bot framework" into a "multi-channel AI agent platform" |
| [#569](https://github.com/qwibitai/nanoclaw/pull/569) | Replaces #568, newly opened today | **Unified cross-channel interactions**: answering community member @Fritzzzz1's request in #499 to "solve interaction features for all channels in a generic way"; #569 implements reactions, quoted replies, votes, and more as a skill pack |
| [#499](https://github.com/qwibitai/nanoclaw/pull/499) | Signal channel implementation | **Privacy-first alternative**: provides a TCP JSON-RPC interface via the signal-cli daemon, meeting the needs of users wary of WhatsApp's privacy policy; can run alongside WhatsApp |
| [#566](https://github.com/qwibitai/nanoclaw/pull/566) | WhatsApp stability special project | **Production resilience**: implements exponential backoff for 405 rate-limit errors and downgrades auth failures from fatal errors to recoverable states, directly answering the scenario reported in #553 |

**Community dynamics insight**: today's PR flow shows a clear **"architecture-refactor driven"** character — the #500 pluggable-channels refactor has become the center of gravity, with Signal (#499) and channel interactions (#569) both unfolding around this architecture. This shows the community has formed a technical consensus of "unify the abstraction first, then expand the implementations", and the project is moving from rapid prototyping into engineering maturity.

---

## 5. Bugs and Stability

| Problem | Source | Severity | Status | Impact scope |
|:---|:---|:---|:---|:---|
| **Container execution fails after WhatsApp connection recovery** | [#553](https://github.com/qwibitai/nanoclaw/issues/553) | 🔴 **High** | Pending fix, no PR | Core workflow broken in VPN-switching scenarios: start without VPN → WhatsApp connection fails → enable VPN to restore the connection → container execution misbehaves |
| **No user-level task cancellation mechanism** | [#554](https://github.com/qwibitai/nanoclaw/issues/554) | 🔴 **High (security)** | Pending fix, no PR | Once a destructive instruction (e.g. "delete all emails") starts it cannot be interrupted, posing irreversible-operation risk |
| Discord state/code mismatch causes silent failures | [#488](https://github.com/qwibitai/nanoclaw/pull/488) | 🟡 Medium | **Fix PR pending merge** | Missing state validation in the OAuth flow |
| Telegram state/code mismatch | [#424](https://github.com/qwibitai/nanoclaw/pull/424) | 🟡 Medium | **Fix PR pending merge** | Channel-specific issue similar to #488 |
| Missing Docker permission detection | [#512](https://github.com/qwibitai/nanoclaw/pull/512) | 🟡 Medium | **Fix PR pending merge** | Hard to diagnose when the user is not in the docker group |

**Stability trend**: WhatsApp-related stability issues received dense attention (#566 backoff strategy, #565 PID lock preventing duplicate instances), but the **lifecycle coupling between connection state and container execution** exposed by #553 has no targeted fix yet. The **security architecture flaw** exposed by #554 (no cancellation mechanism) needs a priority response from the core team.

---

## 6. Feature Requests and Roadmap Signals

| Demand signal | Source | Feasibility assessment | Signal strength for the next version |
|:---|:---|:---|:---|
| **Channel-agnostic interaction abstraction** | #499 comments → #568 → #569 | ⭐⭐⭐⭐⭐ High | **Strong** - already implemented as a skill pack, with #500 providing architectural support |
| **Signal as a privacy-alternative channel** | #499 | ⭐⭐⭐⭐☆ High | **Strong** - PR submitted; compatible with the #500 architecture |
| **Avian LLM provider support** | [#549](https://github.com/qwibitai/nanoclaw/pull/549) | ⭐⭐⭐⭐☆ High | **Strong** - skill-pack form; OpenAI-compatible API lowers integration cost |
| **Telegram Topics support** | [#564](https://github.com/qwibitai/nanoclaw/pull/564) | ⭐⭐⭐☆☆ Medium | Medium - enterprise/community scenario need; coupling with the core architecture to be assessed |
| **Shabbat/religious mode** | #547 (closed) | ⭐⭐☆☆☆ Low-medium | Weak - highly innovative but narrow audience; may live on as a community skill |
| **Voice security layer** | #511 (closed) | ⭐⭐⭐⭐☆ High | **Strong** - security-critical feature; the closure may mean a resubmission after refactoring |

**Roadmap inference**: the core narrative of the next version (if based on the #500 refactor) will be a **"multi-channel AI agent platform"**, with Signal integration and unified channel interactions as flagship features. LLM provider diversification (Avian, etc.) keeps expanding through the skill-pack mechanism. Security features (voice verification, task cancellation) need core architectural support and may become post-refactor priorities.

---

## 7. User Feedback Summary

### Real pain points (from Issues)

| Pain point | Source | Scenario reconstruction |
|:---|:---|:---|
| **Service unusable after network environment switches** | #553 | Users in network-restricted regions such as China must frequently switch VPNs, but NanoClaw handles connection interruptions poorly on recovery, leading to "container execution still failing after the connection is restored" |
| **No brakes on destructive operations** | #554 | Users realize the agent may misread instructions and perform dangerous operations (e.g. bulk deletes), but the system offers no "emergency stop" button, creating anxiety about losing control |

### Usage scenario insights

- **Strong multi-channel demand**: users are not satisfied with WhatsApp alone; the parallel development of Signal (#499), Discord (#562), and Telegram (#564) shows the user base spreads across different messaging ecosystems
- **Self-hosting complexity**: Docker permission problems (#512) and OAuth flow confusion (#562, #563) recur, showing the target users (tech enthusiasts) still hit friction during deployment
- **Cultural/religious scenario customization**: #547 Shabbat Mode was closed, but it demonstrated users' interest in "programmable constraints on agent behavior" (policy control over time, location, identity, and other dimensions)

### Satisfaction/dissatisfaction

| Dimension | Assessment |
|:---|:---|
| ✅ Feature richness | High - research capability, voice processing, multi-channel, and more expanding quickly |
| ⚠️ Stability | Medium - connection recovery, state-sync, and similar issues hurt production confidence |
| ❌ Sense of safety and control | Low - the lack of a cancellation mechanism makes users uneasy about agent autonomy |

---

## 8. Pending Backlog

### High-value PRs needing maintainer attention

| PR | Created | Backlog risk | Why it matters |
|:---|:---|:---|:---|
| [#500](https://github.com/qwibitai/nanoclaw/pull/500) | 2026-02-25 | ⚠️ Medium | Core architecture refactor; many of the 29 pending PRs depend on this foundation, and delays will block ecosystem expansion across the board |
| [#412](https://github.com/qwibitai/nanoclaw/pull/412) | 2026-02-23 | 🔴 **High** | Host authorization pass-through, improving the first-setup experience; already backlogged 5 days |
| [#424](https://github.com/qwibitai/nanoclaw/pull/424) | 2026-02-23 | 🔴 **High** | Telegram state fix; same class of issue as #488 and should be merged for consistency |

### Security Issue needing a response

| Issue | Risk | Suggested action |
|:---|:---|:---|
| [#554](https://github.com/qwibitai/nanoclaw/issues/554) | Users cannot interrupt dangerous operations | The core team should reserve a cancellation signal channel in the #500 refactor or design an emergency-stop protocol |

---

**Daily report generated at**: 2026-02-28 \
**Data source**: GitHub API / qwibitai/nanoclaw \
**Analyst**: AI agent and open source project analysis system

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Report | 2026-02-28

## 1. Today at a Glance

IronClaw maintained **high activity** today, with **27 PR updates** (13 merged/closed, 14 awaiting review) and **6 Issue updates** (5 active, 1 closed) within 24 hours. Core progress concentrates on three directions: **WASM channel capability expansion** (file attachments, broadcast messages), landing the **programmable tool call (PTC) infrastructure**, and **developer-experience optimization** (automatic configuration detection, custom data directory). The project is transitioning from a "feature-building phase" to a "stability and ecosystem-expansion phase", and the 48% PR merge rate shows a healthy code-review cadence.

---

## 2. Releases

**No new release**

The v0.13.0 release PR #385 is still open, contains an API breaking change (`constructible_struct_adds_field`), and is expected to merge soon.

---

## 3. Project Progress

### Key PRs merged/closed today (13)

| PR | Author | Core contribution | Significance for the project |
|:---|:---|:---|:---|
| [#404](https://github.com/nearai/ironclaw/pull/404) | @henrypark133 | Web slash-command autocomplete + `/status` `/list` command fixes + chat input lock fix | **A step change in interaction experience**: 18 commands support Tab completion, solving the long-standing "commands visible but unusable" problem |
| [#398](https://github.com/nearai/ironclaw/pull/398) | @henrypark133 | Routine notification delivery fix across all channels | **A critical reliability fix**: WASM channel (Telegram/Slack) notifications went from "silently lost" to "reliably delivered" |
| [#353](https://github.com/nearai/ironclaw/pull/353) | @zmanian | Automated QA system: 424 new tests, CI matrix, Docker builds, schema validators | **An engineering-infrastructure milestone**: test coverage grew from 1,300 → 1,724, systematically preventing regressions |
| [#382](https://github.com/nearai/ironclaw/pull/382) | @henrypark133 | Tool-call persistence, pending-approval state recovery, UTF-8 truncation crash fix | **Data integrity**: context no longer lost when switching threads; production panics eliminated |
| [#397](https://github.com/nearai/ironclaw/pull/397) | @ibhagwan | `IRONCLAW_BASE_DIR` environment variable support (LazyLock caching) | **Deployment flexibility**: supports isolated multi-agent deployments, breaking the hardcoded `~/.ironclaw` limit |
| [#399](https://github.com/nearai/ironclaw/pull/399) | @henrypark133 | libSQL auto-detection (when `ironclaw.db` exists) | **Cloud-native adaptation**: solves the chicken-and-egg configuration problem on NEAR AI cloud instances |
| [#391](https://github.com/nearai/ironclaw/pull/391) | @henrypark133 | Web UI Routine cross-channel visibility fix | **A consistency fix**: Routines created on Telegram can be managed in the Web UI |
| [#146](https://github.com/nearai/ironclaw/pull/146) | @ztsalexey | rig-core backend model auto-discovery | **Usability**: OpenAI/Ollama backends no longer show empty model lists |
| [#128](https://github.com/nearai/ironclaw/pull/128) | @panosAthDBX | Unified configuration diagnostics (responding to @ilblackdragon's feedback) | **Maintainability**: eliminates ad-hoc default logic in configuration parsing |
| [#371](https://github.com/nearai/ironclaw/pull/371) | @BroccoliFin | `--help` enhancements (color output, examples, snapshot tests) | **Developer experience**: closes #285 |
| [#66](https://github.com/nearai/ironclaw/pull/66) | @dj-ryan | Architecture diagram update | **Documentation clarity** |
| [#405](https://github.com/nearai/ironclaw/pull/405) | @jmhdevbot-hue | Word tool (closed, not merged) | — |

**Overall progress assessment**: today's merged PRs cover three dimensions — **user experience** (Web autocomplete), **reliability** (notification delivery, data persistence), and **engineering maturity** (test system, configuration flexibility) — and project health has improved markedly.

---

## 4. Community Hotspots

### Most active discussions

| Topic | Activity metric | Core request analysis |
|:---|:---|:---|
| [#407 Ideas from Hermes Agent worth adopting](https://github.com/nearai/ironclaw/issues/407) | 👍 0, 💬 2, spawned PR #408 | **Benchmarking anxiety**: the community proactively studies the competitor Hermes Agent and proposes adoptable patterns — tool metadata registration, LLM-driven skill discovery, memory tiering. Already directly converted into the PTC (programmable tool calls) implementation |
| [#409 WASM channel file/image attachment support](https://github.com/nearai/ironclaw/pull/409) | XL-sized, new contributor | **Multimedia capability gap**: sending images and transferring documents on Telegram are high-frequency user needs; the PR implements the full chain of HTTP tool download → WASM channel attachments |
| [#408 Programmable tool calls (PTC)](https://github.com/nearai/ironclaw/pull/408) | XL-sized, veteran contributor | **Performance-optimization demand**: chained tool calls without LLM round trips cut response latency from seconds to milliseconds, critical for automated workflows |

**Community signal**: users are no longer satisfied with "it runs"; they now pursue **response speed** (PTC), **multimedia capability** (attachments), and **feature parity with competitors** (the Hermes study), showing the user base expanding from early adopters to broader developers.

---

## 5. Bugs and Stability

| Severity | Issue | Status | Impact scope | Fix PR |
|:---|:---|:---|:---|:---|
| 🔴 **High** | [#400 openai_compatible backend truncates model names](https://github.com/nearai/ironclaw/issues/400) | **Open** | Ollama users cannot use dotted-version models like `llama3.2` | None |
| 🟡 **Medium** | [#406 Discord/WhatsApp missing build.sh, hidden from the install wizard](https://github.com/nearai/ironclaw/issues/406) | **Open** | New users cannot enable the Discord/WhatsApp channels through the wizard | None |
| 🟡 **Medium** | [#148 Discord signature verification missing + Capabilities header mismatch](https://github.com/nearai/ironclaw/issues/148) | **Closed** | Discord interaction endpoints cannot be verified; discovery broken | Fixed (closed today) |

**Stability assessment**: both open bugs affect the **new-user onboarding path** (model selection, channel enablement) and should be handled first. The model-name parsing problem in #400 likely stems from a simple string-split logic; the fix is cheap but the impact is broad.

---

## 6. Feature Requests and Roadmap Signals

| Need | Issue/PR | Implementation status | Probability of making the next version |
|:---|:---|:---|:---|
| **Programmable tool calls (PTC)** | #408 | PR submitted, XL-sized | ⭐⭐⭐⭐⭐ **Very high** — architecture-level feature, fully implemented |
| **WASM channel file attachments** | #409 | PR submitted, XL-sized | ⭐⭐⭐⭐⭐ **Very high** — code complete, awaiting review |
| **SimpleX Chat channel** | [#402](https://github.com/nearai/ironclaw/issues/402) | Requirement stage, with a technical proposal | ⭐⭐⭐⭐☆ **High** — fits the "security-first" positioning; the community is willing to implement |
| **Avian LLM provider** | [#396](https://github.com/nearai/ironclaw/pull/396) | PR submitted, M-sized | ⭐⭐⭐⭐☆ **High** — follows the Tinfoil pattern, low risk |
| **Slack Socket Mode** | #333 | PR open, XL-sized, Feb 23 | ⭐⭐⭐☆☆ **Medium** — clear NAT-friendly connection need, but large in scope |
| **Claude Code CLI login** | [#386](https://github.com/nearai/ironclaw/issues/386) | Requirement stage | ⭐⭐☆☆☆ **Low** — requires Anthropic's cooperation; not technically controllable |
| **OpenTelemetry observability** | #334 | PR open, XL-sized, Feb 23 | ⭐⭐⭐☆☆ **Medium** — tool-call auditing removed; scope shrinking |

---

## 7. User Feedback Summary

### Real pain points

| Source | Pain point | Scenario |
|:---|:---|:---|
| #400 @RikaGoldberg | Ollama local model names truncated | Using `llama3.2`, the backend becomes `llama3`, 404 errors |
| #406 @KemonoNeco | "Invisible" channels — code exists but no build script | The install wizard does not show Discord/WhatsApp, so users assume they are unimplemented |
| #398 fix background | Routine notifications "silently lost" | Users create scheduled tasks but receive no Telegram notification and assume they never fired |
| #397 @ibhagwan | Hardcoded `~/.ironclaw` limits multi-agent deployment | Needs to isolate data/config across multiple agents |

### Satisfaction points

- **Improved configuration flexibility**: #399's libSQL auto-detection fixes cloud-instance startup failures
- **Better Web interaction**: slash autocomplete and command fixes improve efficiency

### Dissatisfaction/confusion

- Awakening of competitor-parity awareness (#407 Hermes study), hinting at "is IronClaw falling behind"
- The Claude Code CLI integration request (#386) shows users' preference for the official toolchain

---

## 8. Pending Backlog

| Item | Created | Risk | Reminder |
|:---|:---|:---|:---|
| [#333 Slack Socket Mode](https://github.com/nearai/ironclaw/pull/333) | 2026-02-23 | A hard requirement for enterprise firewall/NAT scenarios | No updates for 5 days; needs a maintainer review decision |
| [#334 OpenTelemetry](https://github.com/nearai/ironclaw/pull/334) | 2026-02-23 | Observability infrastructure | Scope has shrunk; needs confirmation whether to keep pushing |
| [#400 Model-name truncation](https://github.com/nearai/ironclaw/issues/400) | Yesterday | Affects the core Ollama user base | No assignee; suggest labeling `good first issue` |
| [#386 Claude Code CLI](https://github.com/nearai/ironclaw/issues/386) | 2 days ago | Needs a product decision | Suggest an official response on feasibility |

---

**Daily report generated at**: 2026-02-28 \
**Data range**: GitHub activity over the past 24 hours

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Report | 2026-02-28

---

## 1. Today at a Glance

TinyClaw showed **high development activity** today: **8 PRs** (4 opened, 4 closed) and **1 new Issue** within 24 hours, with no release. Core progress concentrated on **the plugin system officially landing** (PR #127 merged), **multi-platform thread support fixes** (Discord/Telegram), and an **architecture-level refactor** (monorepo proposal). The community has started paying attention to **session isolation**, an enterprise-grade need, marking the project's evolution from basic features toward production readiness.

---

## 2. Releases

**No new release**

> Note: PR #148, which bumped the version to 0.0.7, was closed; presumably the maintainer chose to postpone the release or to consolidate more changes into one release.

---

## 3. Project Progress

### ✅ Key merged/closed PRs

| PR | Author | Core contribution | Significance for the project |
|:---|:---|:---|:---|
| [#127](https://github.com/TinyAGI/tinyclaw/pull/127) | @steven1522 | **Plugin system officially landed**: Events (state broadcasting) + Hooks (message transformation) | An architecture milestone: TinyClaw evolves from a single tool into an **extensible platform**, supporting ecosystem extensions such as 3D avatar visualization and channel format conversion |
| [#146](https://github.com/TinyAGI/tinyclaw/pull/146) | @jlia0 | Rebase-conflict-resolved version of #127 (closed; #127 merged first) | Ensured the plugin system merged cleanly into the mainline |
| [#145](https://github.com/TinyAGI/tinyclaw/pull/145) | @jlia0 | **Skill file management fix**: copy instead of symlink, unified `TINYCLAW_HOME` behavior | Solves cross-environment deployment pain (container/CI scenarios) and eliminates skill-file drift risk |
| [#148](https://github.com/TinyAGI/tinyclaw/pull/148) | @jlia0 | Version bump to 0.0.7 (closed) | — |

**A maturity leap today**: the plugin system + the skill management fix make up **the core deliverables of v0.0.7**, and multi-platform adaptation has entered a refinement stage.

---

## 4. Community Hotspots

| Activity metric | Item | Analysis |
|:---|:---|:---|
| **Architecture-level discussion** | [#147 Monorepo refactor](https://github.com/TinyAGI/tinyclaw/pull/147) | @jlia0 proposes restructuring the codebase, hinting at growing project scale and emerging modularity needs, possibly paving the way for a future plugin marketplace/multi-package management |
| **Enterprise-grade needs surfacing** | [#144 Session isolation](https://github.com/TinyAGI/tinyclaw/issues/144) | A core pain point of multi-tenant scenarios: Telegram Topics and Discord Threads cross-contaminate contexts; needs a `--session-id` + `--resume` mechanism |
| **Plugin security hardening** | [#149](https://github.com/TinyAGI/tinyclaw/pull/149) + [#150](https://github.com/TinyAGI/tinyclaw/pull/150) | @mczabca-boop's stacked PRs: timeout control, metadata scrubbing, plugin gating — reflecting production environments' hard requirements for **sandbox security** |

**Needs insight**: the community is shifting from "works" to "works well and securely"; enterprise deployment scenarios (isolation, auditing, timeout control) are the new focus.

---

## 5. Bugs and Stability

| Severity | Problem | Status | Fix PR |
|:---|:---|:---|:---|
| 🔴 **High** | Discord/Telegram thread reply mix-ups, queue PATH resolution failures | **Pending merge** | [#142](https://github.com/TinyAGI/tinyclaw/pull/142) |
| 🟡 **Medium** | Plugin hooks have no timeout mechanism → may block the main process | **Pending merge** | [#149](https://github.com/TinyAGI/tinyclaw/pull/149) |
| 🟡 **Medium** | Skill file symlinks fail in container environments | **Fixed** | [#145](https://github.com/TinyAGI/tinyclaw/pull/145) ✅ |

> **Risk warning**: #142 involves core cross-platform interaction logic; prioritizing its review and merge is recommended to safeguard the user experience.

---

## 6. Feature Requests and Roadmap Signals

| Source | Feature | Feasibility assessment | Version prediction |
|:---|:---|:---|:---|
| [#144](https://github.com/TinyAGI/tinyclaw/issues/144) | **Per-thread session isolation** | ⭐⭐⭐⭐⭐ High: architecturally needs extending the `-c` parameter; moderate coupling with existing session management | v0.0.8 |
| [#147](https://github.com/TinyAGI/tinyclaw/pull/147) | **Monorepo refactor** | ⭐⭐⭐⭐☆ High: an infrastructure change; timing is ripe after #127 merged | v0.1.0 (breaking change) |
| [#149](https://github.com/TinyAGI/tinyclaw/pull/149) + [#150](https://github.com/TinyAGI/tinyclaw/pull/150) | **OpenViking plugin + security hardening** | ⭐⭐⭐⭐⭐ High: stacked PRs are ready, with #149 as the base | v0.0.7 or v0.0.8 |

**Roadmap signals**: the project is evolving from MVP toward **platformization + enterprise grade**, with security, isolation, and extensibility as the three pillars of the next stage.

---

## 7. User Feedback Summary

> Distilled from the original request in Issue #144

| Dimension | Feedback |
|:---|:---|
| **Pain point** | "Telegram topics and Discord threads hit the same agent, and the contexts pollute each other" — **missing session isolation** in multi-channel deployments |
| **Usage scenario** | Team-level deployment: different projects/topics need independent memory while sharing the same backend resources |
| **Expected behavior** | `--session-id <uuid>` to explicitly specify a session + `--resume` to restore a specific context |
| **Satisfaction hint** | The user proactively proposed a detailed plan (including CLI design), showing strong willingness to invest in the project long term |

---

## 8. Pending Backlog

| Item | Created | Status | Reminder |
|:---|:---|:---|:---|
| [#142](https://github.com/TinyAGI/tinyclaw/pull/142) Discord/Telegram/queue fixes | Today | 🔴 **Pending merge** | Affects the core user experience; review within 48h recommended |
| [#147](https://github.com/TinyAGI/tinyclaw/pull/147) Monorepo refactor | Today | 🟡 **Decision pending** | Maintainers need to confirm the architectural direction; consider opening an RFC discussion |
| [#144](https://github.com/TinyAGI/tinyclaw/issues/144) Session isolation | Today | 🟡 **Response pending** | An enterprise-grade need; suggest labeling `enhancement` + `help wanted` or adding it to a milestone |

---

**Project health score: 🟢 Good** \
- Activity: High (8 PRs/day) \
- Code flow: Healthy (core features merging continuously) \
- Community participation: Rising (enterprise-scenario needs emerging) \
- Risk points: #142 multi-platform fix pending merge; the monorepo decision needs clarity

</details>

---
*This daily report was generated automatically by [agents-radar](https://github.com/duanyytop/agents-radar).*