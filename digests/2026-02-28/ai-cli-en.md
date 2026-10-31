# AI CLI Community Report 2026-02-28

> Generated at: 2026-02-28 03:32 UTC | Tools covered: 6

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Side-by-side comparison

# AI CLI Tools Ecosystem Comparison Report | 2026-02-28

---

## 1. Ecosystem overview

AI CLI tools have entered a dual-track competition phase of **"refined experience + enterprise-grade stability."** Claude Code commands the high end of the market with its plugin ecosystem and remote control features, but Windows compatibility is a clear weakness; OpenAI Codex is accelerating its Rust core rewrite and leads in MCP toolchain maturity; Chinese tools (Kimi, Qwen) are catching up fast, differentiating through IDE integration and localization. The overall landscape shows "converging fundamentals, diverging vertical scenarios," with memory management, long-session stability, and cross-platform consistency emerging as shared technical bottlenecks.

---

## 2. Activity comparison by tool

| Tool | Issues (today) | PRs (today) | Version releases | Key updates |
|:---|:---:|:---:|:---|:---|
| **Claude Code** | 50 | 14 | None | Pro plan feature controversy, Windows Bun crashes, MCP pipeline conflicts |
| **OpenAI Codex** | 50 | ~15 | Rust α.4-α.8 ×4 | Accelerated low-level architecture iteration, MCP transport self-healing, OAuth race fix |
| **Gemini CLI** | ~15 | ~10 | v0.33.0-nightly / v0.32.0-preview | Plan mode documentation improvements, A2A streaming response robustness |
| **Kimi Code CLI** | 13 | 14 | **v1.16.0** | Session management enhancements, multi-directory workspaces, external editor integration |
| **OpenCode** | 50 | ~12 | None | Memory leak fixes, 1M context support, paste collapsing interaction |
| **Qwen Code** | 29 | 22 | v0.11.0-preview.1 / nightly | MCP server start/stop management, VSCode experience parity, Hooks system |

> **Activity ranking**: Claude Code ≈ OpenAI Codex ≈ OpenCode > Qwen Code > Kimi CLI > Gemini CLI

---

## 3. Shared feature directions

| Feature direction | Tools involved | Specific demands |
|:---|:---|:---|
| **MCP ecosystem maturation** | Claude Code, OpenAI Codex, Kimi, Qwen, Gemini | Server lifecycle management (start/stop/isolation), separation of config from session state, OAuth synchronization, transport self-healing |
| **Deep IDE integration** | Kimi, Qwen, OpenAI Codex, Claude Code | VSCode/JetBrains/Zed feature parity, file references, ACP protocol compatibility, autocompletion improvements |
| **Long-session / large-context stability** | Claude Code, OpenCode, Kimi, Gemini | Memory leak fixes, context compaction accuracy, 1M token support, cross-session persistence |
| **Windows platform experience** | Claude Code, OpenAI Codex, Kimi, Qwen, Gemini | Bun/Node runtime compatibility, path handling, TUI rendering, authentication persistence |
| **Interaction refinement** | OpenCode, Kimi, Gemini, Claude Code | Paste content control, history search, external editors, voice input improvements |

---

## 4. Differentiation analysis

| Tool | Core focus | Target users | Technical trajectory |
|:---|:---|:---|:---|
| **Claude Code** | Enterprise-grade agent orchestration, remote collaboration | Large teams, multi-device developers | Bun runtime, plugin architecture, Pro plan feature tiering |
| **OpenAI Codex** | Low-level performance and toolchain reliability | Professional developers who prioritize stability | Rust core rewrite, OpenTelemetry observability, MCP engineering depth |
| **Gemini CLI** | Remote agent architecture, Plan mode | Cloud-native / distributed development scenarios | A2A protocol, ACP authentication, sprint-style architecture iteration |
| **Kimi Code CLI** | Localized IDE integration, session management | Chinese developers, multi-IDE users | Python implementation, rapid feature iteration, memory system exploration |
| **OpenCode** | Open-source customizability, TUI refinement | Open-source contributors, users with personalization needs | TypeScript, highly configurable, community-driven features |
| **Qwen Code** | Domestic full-stack, multi-agent collaboration | Alibaba Cloud ecosystem users, Chinese enterprises | Deep optimization for in-house models, Hooks extension architecture, specialized Modes |

---

## 5. Community heat and maturity

### 🔥 High activity + rapid iteration
| Tool | Characteristics | Risk signals |
|:---|:---|:---|
| **Qwen Code** | 22 PRs/29 Issues, dense feature delivery | Insufficient internationalization test coverage, bugs concentrated in Chinese-language scenarios |
| **Kimi CLI** | Fast v1.16.0 release cadence, aggressive IDE integration | Network-layer fragility unresolved, frequent connection errors |
| **OpenCode** | Fast community Issue response, intensive interaction polish | Memory management architectural debt surfacing, production stability unverified |

### 🏗️ Architecture rework phase
| Tool | Characteristics | Key observations |
|:---|:---|:---|
| **OpenAI Codex** | 4 Rust alpha releases per day, generational replacement underneath | Leading MCP toolchain maturity, but a JetBrains extension has long been missing |
| **Gemini CLI** | Remote agent infrastructure sprint | A2A/ACP protocols first, but TUI rendering issues piling up |

### ⚠️ Stability crisis
| Tool | Core problems | Impact on user trust |
|:---|:---|:---|
| **Claude Code** | Windows crashes, silent usage-policy changes, inconsistent auth state | Pro users dispute paid feature availability; #28817 with 37👍 reveals a trust rift |

---

## 6. Trend signals worth watching

| Trend | Signal sources | Reference value for developers |
|:---|:---|:---|
| **"Memory systems" as the next differentiator** | Kimi #1283, Claude Code plugin ecosystem | Cross-session context persistence will be the key leap in agent capability; invest in the related architecture early |
| **Standardized MCP config governance** | Shared demand for config separation across all 6 tools | Recommend putting MCP config under version control to avoid `~/.claude.json`-style single points of failure |
| **Cross-platform abstraction layer for TUI engines** | Windows flicker/tearing/performance issues are widespread | Evaluate terminal detection and degradation capabilities when choosing (see Gemini #20565) |
| **Elastic model scheduling becomes a hard requirement** | OpenCode #7602 (44👍), Claude Code usage controversy | Production environments need built-in multi-model fallback strategies to avoid single-point dependency |
| **Voice/multimodal input moves to the front** | OpenCode's 4 paste-optimization Issues, Kimi external editor | The AI-native interaction paradigm is evolving; long-text input experience is the new battleground |
| **Consensus around Rust as the performance foundation** | OpenAI Codex full rewrite, Claude Code's Bun predicament | High-performance CLI runtime selection: the Rust vs Bun/Node trade-off |

---

> **Recommendation**: For enterprise scenarios, evaluate OpenAI Codex (stability) and Claude Code (feature depth) first and watch their Windows fix progress; Chinese developers should focus on the IDE-integration maturity of Kimi/Qwen; choose OpenCode for open-source customization needs, but budget for memory-issue troubleshooting costs.

---

## Detailed reports by tool

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills community highlights

> Data source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (2026-02-28)

---

## 1. Top Skills ranking

| Rank | Skill | Overview | Community buzz | Status |
|:---|:---|:---|:---|:---|
| 1 | **[skill-quality-analyzer](https://github.com/anthropics/skills/pull/83)** + **[skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** | Meta-skill: a five-dimension analysis tool for evaluating Skill quality + security scanning | The first official-grade "Skill for Skills," solving the ecosystem's self-improvement problem | 🟡 Open |
| 2 | **[frontend-design](https://github.com/anthropics/skills/pull/210)** | Front-end design optimization, improving instruction executability | Tied to an Anthropic official blog post, discussing how to make Skill instructions more "Claude-executable" | 🟡 Open |
| 3 | **[codebase-inventory-audit](https://github.com/anthropics/skills/pull/147)** | Codebase cleanup and documentation audit, identifying orphan code and unused files | Strong enterprise code-governance demand; outputs CODEBASE-STATUS.md as a single source of truth | 🟡 Open |
| 4 | **[SAP-RPT-1-OSS](https://github.com/anthropics/skills/pull/181)** | Integrates SAP's open-source tabular foundation model for business data forecasting | First enterprise ERP vendor (SAP) + open-source model integration, expanding B2B scenarios | 🟡 Open |
| 5 | **[masonry-generate-image-and-videos](https://github.com/anthropics/skills/pull/335)** | Masonry CLI wrapper: Imagen 3.0 image + Veo 3.1 video generation | Multimodal generation capability gap, workflow integration demand | 🟡 Open |
| 6 | **[ShieldCortex](https://github.com/anthropics/skills/pull/386)** | AI agent persistent memory + built-in security system | npm package already at 6,200+ downloads; a community-validated standalone project seeking official integration | 🟡 Open |
| 7 | **[AURELION](https://github.com/anthropics/skills/pull/444)** | Four-piece suite: structured thinking templates, professional advisors, autonomous agents, memory system | A complete methodology of cognitive frameworks + memory management, for knowledge-management scenarios | 🟡 Open |
| 8 | **[Buildr](https://github.com/anthropics/skills/pull/419)** | Telegram bridge for controlling Claude Code sessions remotely from a phone | Mobile/asynchronous collaboration scenarios, one-line deployment | 🟡 Open |

---

## 2. Community demand trends

Four directions distilled from the Issues:

| Direction | Representative Issue | Core demand |
|:---|:---|:---|
| **Agent governance and security** | [#412](https://github.com/anthropics/skills/issues/412) Agent Governance Skill | Policy enforcement, threat detection, trust scoring, audit trails — the "brake pads" of AI agent systems |
| **MCP protocol integration** | [#16](https://github.com/anthropics/skills/issues/16) Expose Skills as MCPs<br>[#185](https://github.com/anthropics/skills/issues/185) Skills MCP package manager | Package Skills as MCP tools for reuse across AI clients (Claude/Cursor/Windsurf) |
| **Bedrock/enterprise deployment** | [#29](https://github.com/anthropics/skills/issues/29) Usage with Bedrock | AWS enterprise customers want Skills compatible with Bedrock, outside the Claude.ai ecosystem |
| **Skill quality infrastructure** | [#202](https://github.com/anthropics/skills/issues/202) skill-creator best practices<br>[#189](https://github.com/anthropics/skills/issues/189) duplicate skills problem | The official team needs clearer Skill design specs, validation tooling, and deduplication mechanisms |

---

## 3. High-potential Skills awaiting merge

| PR | Key value | Recent activity | Merge outlook |
|:---|:---|:---|:---|
| [#83](https://github.com/anthropics/skills/pull/83) skill-quality-analyzer | Ecosystem bootstrapping: use Skills to evaluate Skills, solving uneven quality | Updated 2026-01-07; the five-dimension scoring system is complete | 🔴 High (needs official review) |
| [#210](https://github.com/anthropics/skills/pull/210) frontend-design | Endorsed by the official blog; an instruction-engineering methodology | Just updated 2026-02-27, responding to official feedback | 🟢 Very high |
| [#362](https://github.com/anthropics/skills/pull/362) + [#284](https://github.com/anthropics/skills/pull/284) UTF-8 fixes | Internationalization/multibyte character support, Windows compatibility | Dense commits in February, fixing underlying bugs such as #199 | 🟢 Very high (maintenance) |
| [#356](https://github.com/anthropics/skills/pull/356) SKILL.md case-sensitivity docs | Saves users hours of debugging; a UX pain point | Submitted 2026-02-09, directly addressing the high-frequency #314 | 🟢 Very high |
| [#386](https://github.com/anthropics/skills/pull/386) ShieldCortex | Already npm community-validated; hits the twin pain points of security + memory | 6,200+ downloads prove PMF; conflicts with the official roadmap need evaluation | 🟡 Medium |
| [#444](https://github.com/anthropics/skills/pull/444) AURELION | Systematized cognitive framework, a knowledge-management vertical | Just submitted 2-21; the four-skill bundle needs split review | 🟡 Medium |

---

## 4. Skills ecosystem insights

> **Core demand: evolving from "feature tools" to "governable, composable, cross-platform agent infrastructure"** — the community is no longer satisfied with point solutions; it wants officials to solve systemic problems such as Skill quality standards (#83), MCP interoperability (#16), enterprise-grade security governance (#412), and multi-cloud deployment (#29).

---

*Report based on public data from github.com/anthropics/skills, as of 2026-02-28*

---

# Claude Code Community Report | 2026-02-28

## Today at a glance

Community activity is extremely high today, with **50 Issues and 14 PRs** updated in the past 24 hours. The core tensions center on the **Pro plan Remote Control availability controversy** (37 👍) and **Windows platform stability issues** (Bun crashes, MCP connection failures). Community contributors filed multiple plugin-ecosystem PRs, including stash message persistence and duplicate-Issue governance tooling improvements.

---

## Community hotspot Issues

| Priority | Issue | Core problem | Community response |
|:---|:---|:---|:---|
| 🔥 **P0** | [#28817](https://github.com/anthropics/claude-code/issues/28817) Pro users unable to use Remote Control | Auth state does not match feature availability; many Pro users report the feature being incorrectly restricted | **37 👍, 24 comments**; users tried multiple re-auth workarounds, all unsuccessful |
| 🔥 **P0** | [#21875](https://github.com/anthropics/claude-code/issues/21875) Bun v1.3.5 persistent crashes (Windows/WSL) | **78 crash reports**; root cause traced to Bun runtime vs Windows compatibility | 18 comments, thorough user documentation, labeled `high-priority` `oncall` |
| 🔥 **P0** | [#28848](https://github.com/anthropics/claude-code/issues/28848) Max plan usage limits silently reduced | Usage policy changed without notice after the Claude 4.6 launch, triggering a trust crisis | 18 comments, 12 👍; the `invalid` label sparked controversy |
| 🔴 **P1** | [#21791](https://github.com/anthropics/claude-code/issues/21791) Chrome extension MCP pipeline conflict | On Windows, Native Host and MCP Server compete for the same named pipe | 19 comments; a blocking issue for the Windows MCP ecosystem |
| 🔴 **P1** | [#24593](https://github.com/anthropics/claude-code/issues/24593) Claude-in-Chrome extension connection failures | Persistent connection failures between the browser extension and the CLI, disrupting remote development workflows | 17 comments, 11 👍, mostly macOS users |
| 🔴 **P1** | [#13480](https://github.com/anthropics/claude-code/issues/13480) Oversized images permanently break conversations | No recovery mechanism; users must start a new session, with data-loss risk | 13 comments, 22 👍, long unfixed |
| 🟡 **P2** | [#13517](https://github.com/anthropics/claude-code/issues/13517) Custom statusLine command not executed | A config parsing issue affecting advanced users' customization needs | 16 comments, 9 👍 |
| 🟡 **P2** | [#22632](https://github.com/anthropics/claude-code/issues/22632) Bun segfaults after long sessions | Linux/macOS also affected; a memory management issue | 11 comments; possibly shares a root cause with #21875 |
| 🟡 **P2** | [#28322](https://github.com/anthropics/claude-code/issues/28322) `/remote-control` command unrecognized in existing sessions | A skill-system load-timing issue; CLI startup arguments behave inconsistently with in-session commands | 10 comments |
| 🟡 **P2** | [#29217](https://github.com/anthropics/claude-code/issues/29217) `.claude.json` concurrent-write corruption | A multi-session race condition; 165 corrupted backups within 40 minutes | 3 comments; data-integrity risk |

---

## Notable PR progress

| PR | Author | Feature/fix | Status |
|:---|:---|:---|:---|
| [#29470](https://github.com/anthropics/claude-code/pull/29470) | @leonardocardoso | **Stash plugin**: multi-slot message persistence (push/pop/apply/list), overcoming the single-slot Ctrl+S limitation | 🟢 Open |
| [#29461](https://github.com/anthropics/claude-code/pull/29461) | @vishnukannaujia | **Duplicate Issue governance**: restricts dedupe candidates to open Issues, avoiding circular references | 🟢 Open |
| [#29460](https://github.com/anthropics/claude-code/pull/29460) | @vishnukannaujia | **Oncall triage improvements**: fixes `gh issue list` sorting assumptions, improving discovery of high-engagement Issues | 🟢 Open |
| [#29457](https://github.com/anthropics/claude-code/pull/29457) | @vishnukannaujia | **Auto-close hardening**: prevents closing an Issue that points at an already-closed target, avoiding mutual mis-closure | 🟢 Open |
| [#29459](https://github.com/anthropics/claude-code/pull/29459) | @vishnukannaujia | **Commit command fix**: dynamic git command injection matching `allowed-tools` permissions | 🟢 Open |
| [#27687](https://github.com/anthropics/claude-code/pull/27687) | @samuelarogbonlo | **Cloud-synced CLAUDE.md**: cross-device user-level instruction persistence (CLI/VS Code/mobile) | 🟢 Open |
| [#29363](https://github.com/anthropics/claude-code/pull/29363) | @xml | **Repository navigation docs**: clarifies this repository's scope (plugin ecosystem, not CLI source), lowering the contributor barrier | 🟢 Open |
| [#25879](https://github.com/anthropics/claude-code/pull/25879) | @hrishikeshs | **Persistent identity plugin**: multi-instance naming and memory files, supporting parallel orchestrators like Magnus | 🟢 Open |
| [#23853](https://github.com/anthropics/claude-code/pull/23853) | @jaycoolslm | **Dockerfile modernization**: replaces the deprecated npm install with the official native install script | 🟢 Open |
| [#29462](https://github.com/anthropics/claude-code/pull/29462) | @bogini | Removes the Oncall triage workflow (conflicts with the direction of #29460; possibly a policy change) | 🔴 Closed |

---

## Feature demand trends

Based on an analysis of today's 50 Issues, community focus falls into the following tiers:

```
┌─────────────────────────────────────────────────────────┐
│  🔥 Tier 1: platform stability and core feature availability │
│     • Windows compatibility (Bun crashes, MCP pipes, Git Bash) │
│     • Plan/billing transparency (Remote Control, usage-limit change notices) │
├─────────────────────────────────────────────────────────┤
│  ⚡ Tier 2: developer experience and toolchain integration │
│     • MCP ecosystem completeness (config separation, slow-startup handling, cross-session persistence) │
│     • Deeper IDE integration (VS Code context visualization, dynamic terminal titles) │
├─────────────────────────────────────────────────────────┤
│  📈 Tier 3: advanced workflows and extensibility │
│     • Session management (history migration, concurrency safety, cloud sync) │
│     • Plugin system (persistent identity, message stash, permission granularity) │
└─────────────────────────────────────────────────────────┘
```

**Emerging signal**: More Issues tagged `area:memory` (#29175 context compaction corruption) suggest long-session reliability is becoming a new pain point.

---

## Developer concerns

| Pain point category | Manifestations | Representative Issues |
|:---|:---|:---|
| **Windows second-class experience** | Bun crashes, MCP connection failures, Git Bash compatibility, path handling | #21875, #21791, #26547 |
| **Config system fragility** | `.claude.json` race corruption, MCP config mixed with session state, migration data loss | #29217, #29132, #29373 |
| **Opaque feature availability** | Unclear plan feature rollout policies, silent usage-limit changes, inconsistent Remote Control auth state | #28817, #28848 |
| **Long-session reliability** | Memory leaks, context compaction losing content, autosave failures | #22632, #29175 |
| **MCP ecosystem friction** | Slow-starting servers not detected, single config location, cross-platform pipe conflicts | #29033, #29498, #21791 |

**Community call**: Multiple Issues ask for MCP config to be separated from `~/.claude.json` (#29498), to support version control and clearer configuration management.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Report | 2026-02-28

---

## 1. Today at a glance

Community activity is extremely high today, with **4 alpha versions of the Rust core components released in rapid succession** (v0.107.0-alpha.4 through alpha.8), signaling accelerated low-level architecture iteration. Meanwhile, **MCP toolchain stability** is the engineering focus, with multiple PRs proposing fixes for production-grade problems such as transport self-healing and OAuth race conditions.

---

## 2. Version releases

| Version | Notes |
|:---|:---|
| **rust-v0.107.0-alpha.8** | Latest preview of the Rust core components |
| rust-v0.107.0-alpha.7 | Same as above |
| rust-v0.107.0-alpha.5 | Same as above |
| rust-v0.107.0-alpha.4 | Same as above |

> Note: Release notes are brief; watch for a detailed changelog later. The dense iteration suggests the Rust migration/rewrite has entered a critical phase.

---

## 3. Community hotspot Issues (10 selected)

| # | Title | Status | Reactions | Key takeaways |
|:---|:---|:---|:---:|:---|
| [#4313](https://github.com/openai/codex/issues/4313) | Official JetBrains IDEs extension request | 🔴 CLOSED | 👍314 / 💬70 | **One of the highest-voted Issues in the repository's history**; overwhelming community demand for PyCharm/IntelliJ support; closed, but it exposes an IDE ecosystem gap |
| [#10571](https://github.com/openai/codex/issues/10571) | "Bad request" error (gpt-5.2 xhigh) | 🟢 OPEN | 👍3 / 💬16 | Pro users hitting model-layer errors, possibly pointing at new-model compatibility issues |
| [#9153](https://github.com/openai/codex/issues/9153) | Windows 401 unauthorized errors | 🟢 OPEN | 👍1 / 💬16 | A persistent Windows authentication ailment affecting the basic Plus user experience |
| [#12836](https://github.com/openai/codex/issues/12836) | `/copy` command X11 clipboard timeout | 🟢 OPEN | 💬10 | Clipboard integration problem on Linux desktops, common in remote/container scenarios |
| [#13041](https://github.com/openai/codex/issues/13041) | Falls back to HTTPS after WebSocket 1008 Policy close | 🟢 OPEN | 👍5 / 💬10 | **A key network transport issue** affecting the real-time response experience |
| [#13007](https://github.com/openai/codex/issues/13007) | VS Code extension on ARM64 Windows requires re-login on every restart | 🔴 CLOSED | 💬9 | Root cause identified: JWT missing `chatgpt_plan_type`; fix merged |
| [#10715](https://github.com/openai/codex/issues/10715) | Codex App support for LaTeX math rendering | 🔴 CLOSED | 👍8 / 💬9 | Strong demand from academic/research users; being closed may mean it is scheduled or already implemented |
| [#12728](https://github.com/openai/codex/issues/12728) | Rate limit consumption unusually fast | 🟢 OPEN | 💬9 | Users report exhausting 22% of the weekly quota in a single day; billing transparency concerns |
| [#13040](https://github.com/openai/codex/issues/13040) | Pasted content replaced with `[Pasted Content N chars]` placeholder | 🟢 OPEN | 💬7 | **A severe context-loss bug**; the model never actually sees the pasted content |
| [#12852](https://github.com/openai/codex/issues/12852) | Desktop thread stuck on "Thinking" and cannot be stopped | 🟢 OPEN | 💬4 | Requires force-killing the process; a stability problem affecting production use |

---

## 4. Notable PR progress (10 selected)

| # | Title | Status | Core improvements |
|:---|:---|:---|:---|
| [#13098](https://github.com/openai/codex/pull/13098) | MCP tool transport self-healing after close | 🔴 CLOSED | Fixes Playwright/Chrome DevTools MCP `Transport closed` hangs without restarting the app |
| [#12815](https://github.com/openai/codex/pull/12815) | Fix MCP OAuth refresh-token race condition | 🟢 OPEN | Token-refresh synchronization across multiple processes, benchmarked against ChatGPT auth's mature approach |
| [#13058](https://github.com/openai/codex/pull/13058) | Record close markers when live sessions are replaced | 🟢 OPEN | Better live-session lifecycle tracking for debugging and state management |
| [#13096](https://github.com/openai/codex/pull/13096) | Support resumable rollout rebuilds for backtracking | 🟢 OPEN | Improves long-conversation backtracking and fault-tolerant recovery for complex agent workflows |
| [#13083](https://github.com/openai/codex/pull/13083) | Enable analytics for `codex exec` and `codex mcp-server` | 🔴 CLOSED | Completes OpenTelemetry metric collection, closing the observability gap from #12913 |
| [#13092](https://github.com/openai/codex/pull/13092) | Add `request_permissions` built-in tool | 🟢 OPEN | **An architecture-level improvement**: request permissions dynamically at runtime, replacing static session policy |
| [#13090](https://github.com/openai/codex/pull/13090) | Fix project trust config parsing so CLI overrides take effect | 🟢 OPEN | Fixes CLI overrides for MCP sub-table config not taking effect |
| [#13053](https://github.com/openai/codex/pull/13053) | Merge skill permissions with the current sandbox by default | 🟢 OPEN | Fixes the counterintuitive behavior where approving a skill script actually reduced permissions |
| [#13085](https://github.com/openai/codex/pull/13085) | Add `debug clear-memories` command | 🔴 CLOSED | Hard-clears memory state for easier testing and privacy compliance |
| [#13033](https://github.com/openai/codex/pull/13033) | Make `thread/start` non-blocking | 🔴 CLOSED | Slow paths such as MCP auth checks no longer block other requests, improving concurrency |

---

## 5. Feature demand trends

Based on an analysis of today's 50 Issues, community focus forms a **"three horizontal, two vertical"** pattern:

| Direction | Heat | Typical demands |
|:---|:---:|:---|
| **IDE ecosystem expansion** | 🔥🔥🔥 | Official JetBrains extension (#4313 314👍), continued VS Code stability polish |
| **Enterprise-grade stability** | 🔥🔥🔥 | Authentication persistence, WebSocket reliability, stuck threads, rate-limit transparency |
| **Interaction refinement** | 🔥🔥 | TUI keybinding customization (Enter/Ctrl+Enter behavior #12129), side-by-side chat display (#13036) |
| **MCP toolchain maturity** | 🔥🔥 | Transport self-healing, OAuth synchronization, dynamic permission requests, project-level config management |
| **Model and context** | 🔥 | Pasted content loss (#13040), LaTeX rendering, multimodal support |

> **Emerging signal**: "Fork conversation from a message" (#13087) reflects users' exploration of **non-linear conversation management**, possibly foreshadowing more complex agent collaboration patterns.

---

## 6. Developer concerns

### 🔴 High-frequency pain points
| Problem | Impact | Representative Issues |
|:---|:---|:---|
| **Easily lost auth state** | Widely reported on Windows ARM64 and Linux | #13007, #12170, #9153 |
| **Context truncation/loss** | Paste placeholders, memory read drift | #13040, #13088 |
| **Network-layer degradation experience** | WebSocket forced fallback to HTTPS | #13041, #13039 |
| **Opaque resource consumption** | Sudden rate-limit spikes, stuck threads | #12728, #12852 |

### 🟡 Architectural expectations
- **Permission model**: shift from static policy to runtime dynamic requests (#13092 responds to this trend)
- **Observability**: exec/mcp-server metrics filled in (#13083), but the community still calls for finer-grained usage transparency
- **Cross-platform consistency**: the Windows experience clearly lags macOS/Linux

### 🟢 Positive signals
- Rust core iteration accelerating; the performance and security foundation should strengthen
- Significant engineering investment in the MCP ecosystem; toolchain reliability keeps improving

---

*This report is generated from public GitHub data and is for reference only. For key decisions, defer to official releases.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Report | 2026-02-28

---

## 1. Today at a glance

Gemini CLI shipped two notable releases today, **v0.33.0-nightly** and **v0.32.0-preview.0**, focused on completing Plan mode documentation and a robust A2A streaming response implementation. The community is hotly debating remote agent architecture design, while developers keep reporting TUI rendering performance and interaction issues.

---

## 2. Version releases

### v0.33.0-nightly.20260228.1ca5c05d0
| Attribute | Content |
|:---|:---|
| Release type | Nightly |
| Core changes | ① Plan mode docs update: support editing plan files during approval ([#20452](https://github.com/google-gemini/gemini-cli/pull/20452)); ② fix flaky ToolResultDisplay overflow tests ([#20452](https://github.com/google-gemini/gemini-cli/pull/20452)) |

### v0.32.0-preview.0
| Attribute | Content |
|:---|:---|
| Release type | Preview |
| Core changes | ① **Plan mode integration tests** ([#20214](https://github.com/google-gemini/gemini-cli/pull/20214)); ② **ACP authentication handshake aligned with the spec** ([#19725](https://github.com/google-gemini/gemini-cli/pull/19725)); ③ **A2A streaming response robustness implementation** (a key infrastructure upgrade) |

### v0.31.0 (stable)
| Attribute | Content |
|:---|:---|
| Core changes | Scoped-read and limited-search optimizations, fuzzy-edit improvements; bottom border color fix; release notes generator fix |

---

## 3. Community hotspot Issues

| # | Issue | Importance | Community response |
|:---|:---|:---|:---|
| [#20142](https://github.com/google-gemini/gemini-cli/issues/20142) | Open-ended AskUser questions don't support Ctrl+R history search | ⭐⭐⭐⭐⭐ **High** | 8 comments; a frequent interaction pain point for developers; WitJakuczun keeps filing similar UX Issues |
| [#18896](https://github.com/google-gemini/gemini-cli/issues/18896) | Windows screen flickers/tears while scrolling | ⭐⭐⭐⭐⭐ **High** | 5 comments; P2 priority; a long-standing cross-platform TUI rendering issue |
| [#20302](https://github.com/google-gemini/gemini-cli/issues/20302) | [Epic] Remote Agent Sprint 1 - infrastructure and core UX | ⭐⭐⭐⭐⭐ **Strategic** | 3 comments; foundational remote agent architecture work led by adamfweidman |
| [#20181](https://github.com/google-gemini/gemini-cli/issues/20181) | AskUser support for answering open-ended questions in an external editor | ⭐⭐⭐⭐ **Medium-high** | 3 comments; pairs with #20142 as UX improvements; essential for long-text input |
| [#19514](https://github.com/google-gemini/gemini-cli/issues/19514) | AskUser tool outputs raw tags in Plan mode | ⭐⭐⭐⭐ **Bug** | 3 comments; a Plan mode UX defect where model output is not rendered correctly |
| [#18953](https://github.com/google-gemini/gemini-cli/issues/18953) | Complex shell commands execute extremely slowly | ⭐⭐⭐⭐ **Performance** | 3 comments; progress-bar "magic" causes a 100x slowdown; reported by kevmoo |
| [#20017](https://github.com/google-gemini/gemini-cli/issues/20017) | OAuth authentication failure: resource origin mismatch | ⭐⭐⭐⭐ **Blocker** | 2 comments; an obstacle for third-party MCP server integration; a security-policy conflict |
| [#20461](https://github.com/google-gemini/gemini-cli/issues/20461) | Support iterative feedback on plan annotations | ⭐⭐⭐⭐ **Workflow** | 2 comments; a Plan mode evolution direction, adding a review step before approval |
| [#20550](https://github.com/google-gemini/gemini-cli/issues/20550) | JS heap out of memory | ⭐⭐⭐⭐ **Stability** | 1 comment; a severe crash issue in long-running scenarios |
| [#19519](https://github.com/google-gemini/gemini-cli/issues/19519) | Long-running shell commands falsely trigger loop detection | ⭐⭐⭐⭐ **False positive** | 1 comment, 👍2; disrupts the user experience; needs smarter threshold tuning |

---

## 4. Notable PR progress

| # | PR | Status | Feature/fix |
|:---|:---|:---|:---|
| [#20627](https://github.com/google-gemini/gemini-cli/pull/20627) | Changelog for v0.32.0-preview.0 | 🟡 Open | Automated release log; preview release process |
| [#20604](https://github.com/google-gemini/gemini-cli/pull/20604) | Add missing tests for prompts/utils.ts | 🟡 Open | Improves test coverage of a core module; community contribution |
| [#20643](https://github.com/google-gemini/gemini-cli/pull/20643) | Defer startup paths to reduce CLI startup latency | 🟡 Open | **P1 priority**; `--version` fast path; resolves #10726 |
| [#20565](https://github.com/google-gemini/gemini-cli/pull/20645) | Terminal detection and capability downgrade | 🟡 Open | **P1 priority**; adapts to JetBrains/tmux/Win10 environments to avoid rendering issues |
| [#20071](https://github.com/google-gemini/gemini-cli/pull/20071) | Invert context window display to usage rate | 🟡 Open | UX improvement: show used% instead of remaining%, matching competitors |
| [#20460](https://github.com/google-gemini/gemini-cli/pull/20460) | Extract tool argument names into constants | 🟡 Open | A maintainability refactor; reduces typo risk |
| [#20638](https://github.com/google-gemini/gemini-cli/pull/20638) | v0.31.0 & v0.32.0-preview.0 documentation updates | 🟡 Open | Release docs sync |
| [#20553](https://github.com/google-gemini/gemini-cli/pull/20553) | Fix duplicate Accept header in MCP Streamable HTTP | ✅ Closed | Fixes connection failures with strict servers like Firecrawl (#20018) |
| [#20566](https://github.com/google-gemini/gemini-cli/pull/20566) | SVG snapshots include bold styles | ✅ Closed | Test infrastructure polish; more stable snapshots |
| [#20542](https://github.com/google-gemini/gemini-cli/pull/20542) | Audio/video token estimation | ✅ Closed | Accurate billing for multimodal content, replacing base64-length estimation |

---

## 5. Feature demand trends

```
┌─────────────────────────────────────────────────────────┐
│  🔥 Remote agent architecture  ████████████████████  Strategic focus │
│     → Infrastructure Sprints 1-3 (#20302, #20303, #20304) │
│     → Local/remote agent separation (#20233) │
│                                                         │
│  🎨 TUI/interaction polish     ██████████████████   Frequent pain points │
│     → History search/external editor (#20142, #20181) │
│     → Scroll rendering/flicker (#18896, #20217) │
│     → Terminal environment adaptation (#20565) │
│                                                         │
│  ⚡ Performance and stability   ████████████████     Continuous optimization │
│     → Startup latency (#20643, #10726) │
│     → Memory/heap exhaustion (#20550) │
│     → Shell execution performance (#18953) │
│                                                         │
│  🔐 Auth and MCP ecosystem      ██████████████      Ecosystem expansion │
│     → OAuth spec alignment (#19725, #20017) │
│     → Third-party server compatibility (#20553) │
│                                                         │
│  📋 Plan mode evolution         ████████████        Product deepening │
│     → Integration test coverage (#20214) │
│     → Pre-approval review (#20461) │
│     → Plan file editing (#20452) │
└─────────────────────────────────────────────────────────┘
```

---

## 6. Developer concerns

| Pain point category | Manifestations | Representative Issues |
|:---|:---|:---|
| **TUI reliability** | Flicker, tearing, and input lag on Windows/certain terminals | #18896, #20217 |
| **Interaction efficiency** | No quick history recall; limited long-text input | #20142, #20181 |
| **Perceived performance** | Slow startup, slow complex-command execution, memory leaks | #20643, #18953, #20550 |
| **Agent controllability** | Loop-detection false positives, remote agent isolation needs | #19519, #20233 |
| **MCP compatibility** | OAuth policy conflicts, strict header handling | #20017, #20553 |
| **Plan mode maturity** | Tag rendering errors, rigid approval flow | #19514, #20461 |

> **Trend insight**: The community is evolving from "basic features work" toward "enterprise-grade stability and efficient interaction"; remote agent architecture and TUI experience polish are the two parallel mainlines.

---

*Data source: [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) | Generated at: 2026-02-28*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Report | 2026-02-28

---

## 1. Today at a glance

**v1.16.0 is officially released**, bringing session management enhancements (quick switching to a new session with `/new`), workspace expansion (`--add-dir` multi-directory support), and external editor integration (`Ctrl-O`). Community activity surged, with **13 Issues** and **14 PRs** added in a single day; IDE integration (Zed/JetBrains/VSCode) and connection stability are the focus of developer feedback.

---

## 2. Version releases

### v1.16.0 released

| Feature | Notes |
|:---|:---|
| **Session management** | New `/new` command to quickly create and switch to a brand-new session without exiting and re-entering |
| **Workspace expansion** | Supports the `--add-dir` CLI argument and `/add-dir` command to dynamically add extra directories to the workspace |
| **External editor** | `Ctrl-O` shortcut opens the current input in an external editor; `/editor` configures the default editor |
| **Toolset optimization** | Automatically hides the `AskUserQuestion` tool when the client does not support questions |
| **Visual update** | Newly designed ASCII logo banner |

📎 [Release 1.16.0](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.16.0)

---

## 3. Community hotspot Issues

| # | Title | Type | Criticality | Community activity |
|:---|:---|:---|:---|:---|
| [#1234](https://github.com/MoonshotAI/kimi-cli/issues/1234) | Environment-variable proxies broken by aiohttp defaults | 🐛 Bug | 🔴 High | 7 comments; widely affects Linux users; involves the `kimi login` network layer |
| [#1285](https://github.com/MoonshotAI/kimi-cli/issues/1285) | LLM provider Connection error | 🐛 Bug | 🔴 High | Newly reported; likely shares a root cause with #1266 (HTTP header whitespace issue) |
| [#1266](https://github.com/MoonshotAI/kimi-cli/issues/1266) | Trailing whitespace in `platform.version()` fails HTTP header validation | 🐛 Bug | 🔴 High | Root cause identified; triggered by a specific kernel version on Ubuntu 22.04; a fix PR exists |
| [#1276](https://github.com/MoonshotAI/kimi-cli/issues/1276) | `@` file autocompletion misses files | 🐛 Bug | 🟡 Medium | Feedback on a new v1.16.0 feature; the completion algorithm needs work |
| [#1284](https://github.com/MoonshotAI/kimi-cli/issues/1284) | Zed IDE ACP panel fails to start on Windows | 🐛 Bug | 🟡 Medium | An IDE integration compatibility issue, specific to the Windows platform |
| [#1272](https://github.com/MoonshotAI/kimi-cli/issues/1272) | Files not recognized when JetBrains AI Assistant calls over ACP | ✨ Enhancement | 🟡 Medium | ACP protocol file-reference capability needs strengthening; related to PR #1264 |
| [#1211](https://github.com/MoonshotAI/kimi-cli/issues/1211) | Notion Remote MCP credentials do not persist across sessions | 🐛 Bug | 🟡 Medium | 3 comments; a key MCP ecosystem experience issue |
| [#1283](https://github.com/MoonshotAI/kimi-cli/issues/1283) | Memory system: persisting context across sessions | ✨ Enhancement | 🟢 Trend | Proposed by @CatKang; a core differentiation direction for AI-native development tools |
| [#1282](https://github.com/MoonshotAI/kimi-cli/issues/1282) | Remote control: resume local sessions across devices | ✨ Enhancement | 🟢 Trend | Pairs with #1283 to build a seamless development experience |
| [#1279](https://github.com/MoonshotAI/kimi-cli/issues/1279) | Native git-ai integration support | ✨ Enhancement | 🟢 Trend | A code-provenance standard; the auditability need for AI-generated code |

---

## 4. Notable PR progress

| # | Title | Status | Core contribution | Impact scope |
|:---|:---|:---|:---|:---|
| [#1286](https://github.com/MoonshotAI/kimi-cli/pull/1286) | Autocompletion prioritizes scanning shallow subdirectories | 🟢 Open | Optimizes the directory-traversal strategy for `@` file completion, speeding up responses on large repositories | File-reference experience |
| [#1264](https://github.com/MoonshotAI/kimi-cli/pull/1264) | ACP mode supports embedded context for Zed `@` file references | 🟢 Open | Fixes `embedded_context=False` breaking Zed file references | Zed IDE integration |
| [#1265](https://github.com/MoonshotAI/kimi-cli/pull/1265) | Strip whitespace from custom headers to prevent illegal-value errors | 🟢 Open | Resolves the `APIConnectionError` caused by trailing whitespace in `platform.version()` | Connection stability |
| [#1277](https://github.com/MoonshotAI/kimi-cli/pull/1277) | Lazily load CHANGELOG.md to fix PyInstaller packaging startup failure | 🟢 Open | Fixes a fatal error where packaged binaries cannot find the CHANGELOG on first launch | Distribution and deployment |
| [#1223](https://github.com/MoonshotAI/kimi-cli/pull/1223) | Azure Kimi support for default_query/custom_headers | 🟢 Open | Configuration capability for enterprise OpenAI-compatible endpoints | Enterprise deployment |
| [#1268](https://github.com/MoonshotAI/kimi-cli/pull/1268) | Add `/new` command to create and switch to a new session | ✅ Merged | Core v1.16.0 feature; more efficient session management | Daily workflow |
| [#1271](https://github.com/MoonshotAI/kimi-cli/pull/1271) | `--add-dir` and `/add-dir` support extra workspace directories | ✅ Merged | Breaks the single-directory limitation and supports multi-module projects | Large-project support |
| [#1273](https://github.com/MoonshotAI/kimi-cli/pull/1273) | `Ctrl-O` external editor and `/editor` configuration | ✅ Merged | Better long-text editing; friendly to Vim/Emacs users | Input experience |
| [#1267](https://github.com/MoonshotAI/kimi-cli/pull/1267) | Hide `AskUserQuestion` when the client cannot ask questions | ✅ Merged | Dynamic toolset visibility, preventing the LLM from misusing unavailable capabilities | Protocol compatibility |
| [#1269](https://github.com/MoonshotAI/kimi-cli/pull/1269) | Post-compaction context usage estimate precision improved to 0.1% | ✅ Merged | Fixes abnormal token-count display after compaction | Context management |

---

## 5. Feature demand trends

```
🔥 Deeper IDE integration (35%)
   └── File references in Zed/JetBrains/VSCode, ACP protocol compatibility, autocompletion improvements

🔥 Connection and proxy stability (25%)
   └── HTTP header handling, environment-variable proxies, aiohttp configuration, corporate networks

🚀 Agent capability expansion (20%)
   └── Memory system (#1283), remote session handoff (#1282), MCP ecosystem completeness

⚙️ Enterprise-grade and configurability (15%)
   └── Azure support, custom shells, git-ai provenance, Windows compatibility

💡 Interaction polish (5%)
   └── Command skip options (#729), context precision, editor integration
```

---

## 6. Developer concerns

| Pain point category | Manifestations | Community voice |
|:---|:---|:---|
| **Network-layer fragility** | Proxy configuration, header formatting, frequent connection errors | "Connection error" is a high-frequency keyword spanning 3+ separate Issues |
| **Fragmented IDE integration** | ACP implementations differ widely across editors; file-reference behavior is inconsistent | Zed/JetBrains/VSCode each have dedicated issues; high protocol-adaptation cost |
| **Session and context management** | No cross-device handoff, no persistent history, large-project directory limits | #1282/#1283 propose systematic solutions that the community endorses |
| **Enterprise environment adaptation** | Azure support, custom headers, Windows shell configuration | Enterprise developers urgently need configuration flexibility |
| **Auditability of AI-generated code** | Requests to integrate the git-ai standard | Code-provenance compliance needs are emerging |

---

> 📊 Data source: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) | Statistics window: 2026-02-27 to 2026-02-28

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Report | 2026-02-28

## Today at a glance

Today the community focused on **TUI interaction polish** and **memory/performance fixes**, with several highly upvoted Issues centered on basic interactions like pasted-text collapsing and clipboard copying. Meanwhile, key PRs such as Anthropic 1M context-window support and memory-leak fixes have entered active development, and community attention to production-environment stability is rising markedly.

---

## Community hotspot Issues

| Priority | Issue | Description | Community response |
|:---|:---|:---|:---|
| 🔥 **P0** | [#4283](https://github.com/anomalyco/opencode/issues/4283) TUI clipboard copy broken | Users cannot copy selected response text to the clipboard, disrupting a core workflow; 58 comments and 42 👍, today's hottest | Widely reproduced; the cross-terminal compatibility issue remains to be pinpointed |
| 🔥 **P0** | [#12338](https://github.com/anomalyco/opencode/issues/12338) Opus 4.6 1M token limit not in effect | The UI claims 1M context support, but errors occur past 200k; the config toggle does not work | 22 👍; blocks enterprise users |
| 🔥 **P0** | [#13230](https://github.com/anomalyco/opencode/issues/13230) Memory leak crashes the system | On Linux a single process ballooned to 116GB virtual memory / 21GB RSS, triggering OOM and kernel soft lockups | 10 👍; labeled Critical; high risk in production |
| 🔥 **P1** | [#7602](https://github.com/anomalyco/opencode/issues/7602) Native model fallback/failover support | Today only same-model-ID provider fallback is supported; cannot configure "if model A fails, switch to model B" | 44 👍; essential for long-running agent scenarios |
| 🔥 **P1** | [#8501](https://github.com/anomalyco/opencode/issues/8501) Pasted text should support expand-to-edit | `[Pasted ~N lines]` content cannot be viewed or edited once collapsed; poor experience for voice input | 84 👍; today's most-upvoted feature request |
| 🔥 **P1** | [#10563](https://github.com/anomalyco/opencode/issues/10563) Processes orphaned after the terminal closes | MCP child processes keep holding memory when not explicitly exited | 6 comments; a DevOps concern |
| 🔥 **P1** | [#14965](https://github.com/anomalyco/opencode/issues/14965) Slow startup in the Ghostty terminal | Startup latency in Ghostty with 1.2.1+; other terminals are fine | A terminal-compatibility regression |
| 🔥 **P2** | [#2720](https://github.com/anomalyco/opencode/issues/2720) Error when a tool_use block lacks tool_result | AI_APICallError; tool-call and result blocks mismatched | 15 comments; toolchain stability |
| 🔥 **P2** | [#14935](https://github.com/anomalyco/opencode/issues/14935) Assistant responses rendered twice | The UI layer displays the same response twice | 5 comments; a front-end rendering bug |
| 🔥 **P2** | [#15388](https://github.com/anomalyco/opencode/issues/15388) TUI garbled after long sessions | Overlapping characters and broken layout, while the underlying model output is correct | 3 comments; a terminal rendering engine issue |

---

## Notable PR progress

| Status | PR | Core content | Impact |
|:---|:---|:---|:---|
| 🆕 **New** | [#14375](https://github.com/anomalyco/opencode/pull/14375) Anthropic 1M context support | Enables the 1M token window for Opus 4.6/Sonnet 4.6/4.5/4.0, resolving #12323 | Long-document processing, repository-scale agents |
| 🆕 **New** | [#13514](https://github.com/anomalyco/opencode/pull/13514) Memory leak fixes | Fixes unsubscribed share/plugin/format/bootstrap, compaction data not released, FileTime without dispose, and similar issues | Directly answers the Critical #13230 |
| 🆕 **New** | [#15411](https://github.com/anomalyco/opencode/pull/15411) Collapse large pasted input | Makes `[Pasted ~N lines]` expandable/collapsible, resolving #8501, #15405, #14670, #15421 | Voice input and long-text paste experience |
| 🆕 **New** | [#13637](https://github.com/anomalyco/opencode/pull/13637) Ctrl+Enter send option | New setting allowing Ctrl+Enter to send and Enter for a newline, resolving #11898 | Compatibility with multi-line input habits |
| 🔄 **Updated** | [#13854](https://github.com/anomalyco/opencode/pull/13854) Fix streaming Markdown rendering | Messages still flagged as streaming after completion caused the last table row to be skipped | Rich-text rendering accuracy |
| 🔄 **Updated** | [#14647](https://github.com/anomalyco/opencode/pull/14647) Copilot empty-description fix | An empty tool description caused 400 errors | MCP/OpenAI-compatible toolchain |
| 🔄 **Updated** | [#15250](https://github.com/anomalyco/opencode/pull/15250) View and restore archived sessions | New "Archived Sessions" management in Settings, resolving #6680 and #12393 | Session lifecycle management |
| 🔄 **Updated** | [#13261](https://github.com/anomalyco/opencode/pull/13261) Background sub-agent support | Fire-and-forget async tasks, matching Claude Code behavior, resolving #5887 | Parallelizing complex workflows |
| 🔄 **Updated** | [#14969](https://github.com/anomalyco/opencode/pull/14969) Bedrock IAM auth flow | Replaces the API key form with IAM credentials + environment variable options, resolving #14967 | AWS enterprise users |
| 🔄 **Updated** | [#15418](https://github.com/anomalyco/opencode/pull/15418) S3 virtual-hosted/path-style endpoints | The enterprise /share API storage works with more S3 implementations, resolving #7808 | Self-hosted deployments |

---

## Feature demand trends

Based on an analysis of today's 50 Issues, community focus is shifting generations:

| Trend | Representative Issues | Heat indicators |
|:---|:---|:---|
| **TUI interaction refinement** | #4283 clipboard, #8501 paste collapsing, #7320 double-ESC to clear input | High upvotes + high comments; the basic experience becomes the differentiator |
| **Large-model context engineering** | #12338 1M tokens, #7602 model fallback, #10601 Responses API | Enterprise long-context demand exploding |
| **Production stability** | #13230 memory leak, #10563 orphaned processes, #14965 startup performance | More Critical labels; from "works" to "reliable" |
| **Open ecosystem compatibility** | #6231 model auto-discovery, #12062 custom Providers, #14972 OpenAI-compatible layer | Strong demand for decentralized model access |
| **Multimodal/voice input** | #8501, #14670, #15421 speech-to-text paste improvements | Exploring AI-native interaction paradigms |

---

## Developer concerns

### 🔴 Blocking pain points
1. **System-level clipboard reliability** — #4283 shows copy behavior diverging across terminal emulators (macOS/Windows/Linux); a unified abstraction layer is needed
2. **Memory management out of control** — #13230 reveals cumulative leaks from LSP diagnostics, tool output, and event subscriptions in long-running scenarios; architectural rework is needed

### 🟡 High-frequency experience demands
3. **Control over pasted content** — 4 related Issues around expanding/editing/previewing `[Pasted X lines]`, reflecting growth in voice-input tool (Typeless etc.) integration scenarios
4. **Elastic model scheduling** — 44 👍 on #7602 shows developers need intelligent fallback strategies for rate limits and errors

### 🟢 Ecosystem expansion expectations
5. **Open protocol adaptation** — Auto-discovery, validation, and failure handling for OpenAI-compatible endpoints is becoming table stakes for users of self-hosted model infrastructure

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Report | 2026-02-28

## Today at a glance

Community activity is high today, with **29 Issues** and **22 PRs** updated. Highlights include: MCP server management got a major upgrade (enable/disable commands), the VSCode extension experience keeps improving (Plan Mode switching, the /export command, image pasting), and the SubAgent context-inheritance bug was fixed. Meanwhile, documentation corrections and internationalization issues (Chinese filename handling) remain community focal points.

---

## Version releases

### v0.11.0-preview.1 & v0.11.0-nightly.20260228
- **Documentation enhancements**: the `modelProviders` configuration docs add complete examples and behavior notes
- **Install script fix**: refined permission checks for Arch Linux, with a sudo detection mechanism added

> 🔗 https://github.com/QwenLM/qwen-code/releases

---

## Community hotspot Issues (Top 10)

| # | Title | Status | Importance | Community activity |
|---|------|------|--------|----------|
| [#1985](https://github.com/QwenLM/qwen-code/issues/1985) | VSCode Companion support for Plan Mode switching | 🔴 Open | **High** | A feature-parity need: the CLI supports cycling four approval modes with `Shift+Tab`, but the VSCode extension lacks Plan Mode; users call for a consistent experience |
| [#1965](https://github.com/QwenLM/qwen-code/issues/1965) / [#1971](https://github.com/QwenLM/qwen-code/issues/1971) | MCP server enable/disable management | 🔴 Open | **High** | A frequent request: users need flexible control over MCP server lifecycles, avoiding connectivity checks against every server during `mcp list` |
| [#1977](https://github.com/QwenLM/qwen-code/issues/1977) | Windows automatically inserts spaces into Chinese filenames | 🔴 Open | **Medium** | An i18n bug: paths are split incorrectly when reading Chinese files, e.g. `多 agent 交流文档.md` → `多 agent 交流文档.m`, hurting the core experience for Chinese users |
| [#1986](https://github.com/QwenLM/qwen-code/issues/1986) | SubAgent does not inherit output-language.md and QWEN.md | 🔴 Open | **High** | An architecture issue: sub-agents ignore project conventions and language preferences, with no project-level language config; fix PR [#1993](https://github.com/QwenLM/qwen-code/pull/1993) already filed |
| [#1991](https://github.com/QwenLM/qwen-code/issues/1991) | VSCode Companion support for the /export command | 🔴 Open | **Medium** | A data-export need: the CLI exports chat history as HTML/Markdown/JSON/JSONL; IDE users want the same capability |
| [#1990](https://github.com/QwenLM/qwen-code/issues/1990) | Improve VSCode slash-command behavior | 🔴 Open | **Medium** | Interaction: picking a command like `/model` sends immediately and causes misfires; suggest filling the input box instead of executing directly |
| [#1984](https://github.com/QwenLM/qwen-code/issues/1984) | Free-tier limits and reset-time clarifications | 🔴 Open | **Medium** | Commercialization inquiries: users ask about the qwen3.5-plus free quota, whether the 1000/day limit is accurate, and the UTC reset time |
| [#1996](https://github.com/QwenLM/qwen-code/issues/1996) | JetBrains IDE errors in WSL environments | 🔴 Open | **Medium** | A cross-platform issue: path or environment compatibility problems when code lives in WSL; screenshots attached, awaiting further diagnosis |
| [#1964](https://github.com/QwenLM/qwen-code/issues/1964) | Abnormal space handling in mixed Chinese-English text | 🔴 Open | **Medium** | A semantic bug: the AI claims to have removed spaces but never does; seen with mixed text like `WEEKLY 快楽天` |
| [#1970](https://github.com/QwenLM/qwen-code/issues/1970) | Skills not detected correctly | 🔴 Open | **Medium** | A configuration issue: users confirmed the `~/.qwen/skills/` directory structure is correct, yet the system says "No skills"; the scanning logic needs investigation |

---

## Notable PR progress (Top 10)

| # | Title | Status | Core content |
|---|------|------|----------|
| [#1995](https://github.com/QwenLM/qwen-code/pull/1995) | Add error code 1305 support and custom retry configuration | 🟢 Open | Rate-limit resilience: supports provider-specific error codes and adds a `retryErrorCodes` config option |
| [#1993](https://github.com/QwenLM/qwen-code/pull/1993) | SubAgent inherits global context + project-level language config | 🟢 Open | Fixes [#1986](https://github.com/QwenLM/qwen-code/issues/1986): appends `output-language.md` to the system prompt and prefers project-level config |
| [#1988](https://github.com/QwenLM/qwen-code/pull/1988) | Hooks system infrastructure implementation | 🟢 Open | Extension architecture: 12 lifecycle events (PreToolUse/PostToolUse etc.) with support for custom command injection |
| [#1975](https://github.com/QwenLM/qwen-code/pull/1975) / [#1976](https://github.com/QwenLM/qwen-code/pull/1976) | MCP enable/disable commands + list improvements | 🟢 Open | Fully implements [#1965](https://github.com/QwenLM/qwen-code/issues/1965)/[#1971](https://github.com/QwenLM/qwen-code/issues/1971): supports scope control (user/project); disabled servers skip connectivity checks |
| [#1954](https://github.com/QwenLM/qwen-code/pull/1954) | VSCode auxiliary sidebar support | 🟢 Open | Layout: the Qwen Code panel can move to the secondary sidebar, improving multi-screen workflows |
| [#1982](https://github.com/QwenLM/qwen-code/pull/1982) | Fix PDF/media read API 400 errors | 🟢 Open | A key fix: adds default modality capabilities to the model, resolving the `Invalid value: file` error |
| [#1980](https://github.com/QwenLM/qwen-code/pull/1980) | Modes layer for specialized agent configuration | 🟢 Open | A new architecture: 6 built-in modes (Architect/Code/Ask/Debug/Review/Orchestrator), with `/mode` switching and custom modes |
| [#1978](https://github.com/QwenLM/qwen-code/pull/1978) | VSCode image paste support | 🟢 Open | A multimodal UX: paste images directly in the IDE, closing the gap with the CLI |
| [#1782](https://github.com/QwenLM/qwen-code/pull/1782) | SubAgent Skills visibility configuration | 🟢 Open | Performance: trims sub-agent context to cut inference cost and sharpen domain focus |
| [#1709](https://github.com/QwenLM/qwen-code/pull/1709) | qwen3-coder-next set as the default model | 🔴 Closed | Model upgrade: unifies coder-model with qwen3.5-plus and removes the automatic vision-switching logic |

---

## Feature demand trends

```
📊 Category distribution across the 29 Issues:

IDE integration experience ████████████████████  35%  (VSCode/JetBrains feature parity, sidebar, image pasting)
MCP ecosystem management ██████████████        24%  (server start/stop, list improvements, config flexibility)
Internationalization/localization ████████             14%  (Chinese filenames, space handling, language config inheritance)
Model/service configuration  ██████              10%  (free quotas, error codes, rate-limit handling)
Docs and developer experience █████              10%  (doc errors, install scripts, settings backup)
Agent architecture optimization  ███                 7%  (SubAgent context, multi-agent parallelism)
```

**Key trend takeaways**:
1. **IDE experience consistency** is the top demand — feature parity between the CLI and the VSCode/JetBrains extensions is key to user migration
2. **MCP ecosystem maturity** — from "usable" to "pleasant"; server lifecycle management is entering the refinement stage
3. **Enterprise/Chinese-scenario adaptation** — i18n issues are surfacing intensively; test coverage for Chinese paths on Windows and mixed-text handling must improve

---

## Developer concerns

| Pain point category | Manifestations | Related Issues |
|----------|----------|-----------|
| **Messy configuration management** | State variables leaking into settings.json create Git noise; Skills scan paths unclear | [#1750](https://github.com/QwenLM/qwen-code/issues/1750), [#1970](https://github.com/QwenLM/qwen-code/issues/1970) |
| **Proxy/network environments** | The `no_proxy` environment variable is ignored, blocking access to intranet LLM services | [#756](https://github.com/QwenLM/qwen-code/issues/756) |
| **Task state persistence** | A task stops after an edit failure, and a session restart auto-resumes execution, causing loops | [#1967](https://github.com/QwenLM/qwen-code/issues/1967) |
| **Context length limits** | Long conversations hit the 258048 token cap, and `/compress` times out | [#1969](https://github.com/QwenLM/qwen-code/issues/1969) |
| **Input focus management** | Switching input methods on Ubuntu (Ctrl+Space) defocuses the chat window | [#1879](https://github.com/QwenLM/qwen-code/issues/1879) |

> 💡 **Suggested priorities**: Several PRs already advance MCP management — merge them soon; Chinese i18n issues need dedicated testing; for IDE parity, build a CLI-to-IDE capability-mapping checklist.

---

*This report is generated from public GitHub data. Contact the community maintenance team if you need deep analysis of a specific module.*

</details>

---
*This report is auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*