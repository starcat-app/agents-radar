# AI CLI Community Report 2026-02-26

> Generated at: 2026-02-26 12:50 UTC | Tools covered: 6

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-tool Comparison

# 2026-02-26 AI CLI Tools Ecosystem Comparison Report

---

## 1. Ecosystem Overview

The AI CLI tool market currently shows a "three giants, two newcomers" pattern: Claude Code, OpenAI Codex, and Gemini CLI lead as the big three, while Kimi CLI and OpenCode are catching up fast. MCP (Model Context Protocol) has become the de facto standard extension mechanism, but the tools clearly diverge in engineering maturity such as fault tolerance and tool isolation. Remote/multi-agent collaboration is becoming the next competitive battleground, with Claude Code's Remote Control, Gemini's Remote Agents Sprint, and OpenCode's Agent Teams rolling out in parallel. The Windows platform experience remains an industry-wide weakness, with issues like Bun runtime stability and terminal rendering differences recurring repeatedly.

---

## 2. Activity Comparison by Tool

| Tool | Today's issues | Today's PRs | Releases | Key developments |
|:---|:---|:---|:---|:---|
| **Claude Code** | 9 active (3 erupted in a cluster today) | 10 (4 closed) | v2.1.58/59 dual releases | Auto-Memory and the widened Remote Control rollout; permission problems drawing clustered complaints |
| **OpenAI Codex** | 10 hot (from a 50-issue active pool) | 10 (2 closed) | v0.105.0 stable | TUI syntax highlighting, voice input, theme selector; MCP handshake failure is the number-one blocker |
| **Gemini CLI** | 10 hot (including 3 Epics) | 10 (7 closed) | v0.30.0-nightly | Remote Agents Sprints 1/2/3 released in succession, subagents nearing GA |
| **Kimi CLI** | 15 active (8 new today) | 11 (6 closed) | v1.14.0 | Wire mode Steer support; MCP stability is the top ask |
| **OpenCode** | 10 hot (50 new) | 10 (dense merging) | v1.2.14/15 dual releases | Emergency fix for Windows Bun crashes; Agent Teams is an architecture-level breakthrough |
| **Qwen Code** | — | — | — | Data missing |

> **Activity ranking**: OpenCode (issue surge) > Kimi CLI (dense PR output) > Gemini CLI (Epic-level planning) > Claude Code/Codex (steady iteration)

---

## 3. Commonly Shared Feature Directions

| Feature direction | Tools involved | Specific asks | Urgency |
|:---|:---|:---|:---:|
| **MCP ecosystem stability** | Claude Code, Codex, Kimi CLI | Fault tolerance for connection failures (#769), tool isolation (#6915), handshake reliability (#6020) | 🔴 P0 |
| **Remote/multi-agent collaboration** | Claude Code, Gemini CLI, OpenCode | Remote Control permissions (#28817), Remote Agents Sprint (#20302), Agent Teams (#15205) | 🔴 P0 |
| **Windows platform experience** | All five | Bun runtime crashes (#15015), screen flicker (#18896), voice transcription differences (#12827) | 🟡 P1 |
| **Memory/context management** | Claude Code, Codex, Gemini CLI | Auto-Memory (just released), diff-based memory forgetting (#12900), memory interaction UI (#20429) | 🟡 P1 |
| **Enterprise security and compliance** | Claude Code, Gemini CLI, OpenCode | Data masking hooks (#18653), policy-engine blocking control (#20430), IAM authentication (#14969) | 🟢 P2 |
| **Rate limit transparency** | Claude Code, Codex | Max subscription throttling (#28975), abnormal quota consumption (#12728) | 🟡 P1 |

---

## 4. Differentiation Analysis

| Tool | Core focus | Target users | Technical route traits |
|:---|:---|:---|:---|
| **Claude Code** | Enterprise security, long-context workflows | Large teams, compliance-sensitive enterprises | Deep optimization for its own models (Claude), Remote Control ecosystem integration |
| **OpenAI Codex** | TUI experience, voice interaction, Skill ecosystem | Individual professional developers, creative workers | Rapid feature iteration (alpha channel), ChatGPT ecosystem synergy |
| **Gemini CLI** | Remote agent architecture, subagent orchestration | Distributed teams, cloud-native developers | Official roadmap-driven (Sprint system), deep Google Cloud integration |
| **Kimi CLI** | Domestic Chinese developer experience, multimodal input | Chinese-speaking developers, Moonshot ecosystem users | Unified Wire/Web/Shell across three surfaces, fast response to community feedback |
| **OpenCode** | Open source extensibility, multi-model neutrality | Open source contributors, model-agnostic teams | Bun runtime, Tauri Desktop, community-driven with features first |

**Key differentiation signals**:
- Claude Code is betting on a "remote development hub" positioning, deeply tied to the IDE
- Gemini CLI is the only tool explicitly planning "machine-to-machine authentication" (Sprint 3), aiming at CI/CD scenarios
- OpenCode's Agent Teams implements DB-level parallel sessions, the most aggressive technical route
- Kimi CLI's micro-innovations like "number-key selection" show precise insight into domestic developers' efficiency pain points

---

## 5. Community Activity and Maturity

```
Maturity quadrant (based on today's data)

High maturity ┃ High activity
   ┃
Claude Code ●────────────● OpenCode
(features stable,   │  (fast iteration,
 complaints focus on permissions) │   issues surging but fixed fast)
   ┃
────────────┼────────────
   ┃
Codex ●─────┼────────● Gemini CLI
(TUI polishing phase, │  (clear roadmap,
 heavy MCP debt) │   subagents nearing GA)
   ┃
Low maturity ┃ Low activity
   ┃
         ● Kimi CLI
        (catch-up phase,
         MCP stability unproven)
```

| Assessment dimension | Leader | Notes |
|:---|:---|:---|
| **Community response speed** | OpenCode | v1.2.15 fixed the `.env` crash the same day; @RealKai42 landed 5 PRs in one day |
| **Long-term planning clarity** | Gemini CLI | Sprint 1/2/3 public roadmap, P0-P2 priorities transparent |
| **Enterprise feature completeness** | Claude Code | Most complete audit, masking, and SSO needs, but heavy pricing controversy |
| **Developer experience details** | Kimi CLI | Dense micro-innovations: number keys, Tab navigation, simplified shell prompt |
| **Ecosystem extension health** | Codex | Most complete mechanisms: skill hot-reloading, MCP OAuth resource parameters |

---

## 6. Trend Signals Worth Watching

| Signal | Evidence | Reference value for developers |
|:---|:---|:---|
| **MCP going from "feature" to "infrastructure"** | All five tools integrate it, but missing fault tolerance in Kimi/Claude becomes a production blocker | Test MCP degradation capability first when choosing; avoid single points of failure |
| **Standardization of "agents of agents" architectures** | Agent Teams, Remote Agents, and Subagents emerging in parallel | Divide-and-conquer for complex tasks will become standard; watch session isolation and state synchronization design |
| **Voice/multimodal input inflection point** | Codex's voice debut immediately exposed platform differences, Gemini 3.1 Pro preview lacks capacity | Reserve a 2-3 version stabilization cycle for new interaction modes |
| **Windows developers' "second-class citizen" predicament** | Bun runtime, terminal rendering, and path handling break repeatedly | Cross-platform teams should deploy Linux/macOS first, with Windows as a fallback |
| **Community-driven governance experiments** | Claude Code #28714 uses Haiku 4.5 to auto-triage issues ($0.25/month) | AI-assisted open source governance is already dirt cheap; borrow it for internal tooling maintenance |
| **Rate limits clashing with feature tiers** | Claude Max at $200/month still hits throttling, Codex quota consumption is a "black box" | Watch billing policy details for premium features to avoid budget blowouts |

---

> **Decision advice**: for stable enterprise deployments, Claude Code is the first choice (watch permission-fix progress); for multi-agent architecture pilots, try Gemini CLI or OpenCode; for individual developers who prize experience, Codex; domestic teams evaluating Kimi CLI must verify MCP stability; reassess Qwen Code once data is available.

---

## Detailed Reports by Tool

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Community Highlights

> Data source: [anthropics/skills](https://github.com/anthropics/skills)

⚠️ Skills summary generation failed.

---

# Claude Code Community Report | 2026-02-26

---

## 1. Today at a Glance

Claude Code shipped **v2.1.58/59** back-to-back today, headlined by two features: **Auto-Memory** and the **widened Remote Control rollout**. The community erupted with concentrated feedback around Remote Control permission problems, while multiple compatibility bugs in the Windows Cowork feature continue to trouble users.

---

## 2. Releases

### v2.1.59 (latest)
| Feature | Description |
|:---|:---|
| **Auto-Memory** | Claude automatically saves useful context to memory, manageable via `/memory` |
| **`/copy` interactive copy** | Shows an interactive picker when code blocks are present; supports copying a single block or the full response |
| **"Always allow" prefix improvements** | Better prefix-suggestion experience for the `c` command |

### v2.1.58
- **Remote Control rollout widened**: remote control opened up to more users

📎 [Releases page](https://github.com/anthropics/claude-code/releases)

---

## 3. Hot Community Issues

| # | Title | Status | Comments/👍 | Key takeaways |
|:---|:---|:---|:---|:---|
| [#6915](https://github.com/anthropics/claude-code/issues/6915) | **MCP tool subagent isolation** | 🔴 Open | 82 / 260 | **Hottest request of the year**. MCP tools like Playwright pollute the main conversation context; users want them accessible only to subagents. An architecture-level pain point affecting large-scale workflow design |
| [#24055](https://github.com/anthropics/claude-code/issues/24055) | **Output token limit error (32k)** | 🔴 Open | 68 / 51 | High-frequency Windows bug; Claude responses exceeding the 32000-token limit cause crashes. Reproduced, tagged `oncall` urgent |
| [#17432](https://github.com/anthropics/claude-code/issues/17432) | **India localized pricing (INR)** | 🔴 Open | 40 / 106 | Key emerging-market expansion need. INR pricing on par with ChatGPT/Gemini; the current USD exchange rate creates a 3-4x cost burden |
| [#6836](https://github.com/anthropics/claude-code/issues/6836) | **tool_use/tool_result block mismatch** | 🔴 Open | 38 / 20 | **150+ reports aggregated**. A meta-problem of corrupted conversation state, persisting across versions, flagged as a core stability risk |
| [#28817](https://github.com/anthropics/claude-code/issues/28817) | **Remote Control unavailable to Pro users** | 🔴 Open | 7 / 21 | Erupted in a cluster today. v2.1.58 claims a widened rollout, but many Pro users are still blocked — auth state and feature flags out of sync |
| [#28792](https://github.com/anthropics/claude-code/issues/28792) | **Remote Control WSL permission problems** | 🔴 Open | 6 / 3 | Same as above but specific to WSL environments, showing the rollout has platform differences |
| [#28973](https://github.com/anthropics/claude-code/issues/28973) | **`~/.claude.json` concurrent write corruption** | 🟢 Closed | 3 / 0 | Race conditions truncate the config; closed quickly today but the problem is typical, reflecting a multi-session architecture flaw |
| [#18653](https://github.com/anthropics/claude-code/issues/18653) | **Hooks for masking tool result content** | 🔴 Open | 13 / 12 | An enterprise security must-have. Sensitive data returned by MCP tools needs automatic masking; there is currently no interception mechanism |
| [#28975](https://github.com/anthropics/claude-code/issues/28975) | **Opus 4.6 (1M) Max subscription throttling** | 🔴 Open | 2 / 0 | Users on the $200/month Max plan hit rate limits; long-context premium features clash with billing policy |
| [#27897](https://github.com/anthropics/claude-code/issues/27897) | **Cowork Windows 11 Insider EXDEV rename bug** | 🔴 Open | 4 / 0 | File renames fail inside the MSIX container; a Windows preview compatibility issue blocking VM startup |

---

## 4. Notable PR Progress

| # | Title | Status | Core content |
|:---|:---|:---|:---|
| [#28967](https://github.com/anthropics/claude-code/pull/28967) | **Extend oncall-triage workflow timeouts** | 🟡 Open | Ops response: Job 15→25min, Claude analysis step 10→20min, to handle complex issue processing |
| [#28850](https://github.com/anthropics/claude-code/pull/28850) | **Note PowerShell for the Windows install command** | 🟡 Open | Docs fix: `irm` is unavailable in cmd.exe; an explicit note added to reduce installation failures |
| [#28714](https://github.com/anthropics/claude-code/pull/28714) | **Automated issue triage + weekly report** | 🟡 Open | **Community governance innovation**. Haiku 4.5 classifies individual issues (~$0.001 each), Sonnet 4.6 generates the weekly report (~$0.05/week), about $0.25 per month |
| [#28756](https://github.com/anthropics/claude-code/pull/28756) | **Clean up OIDC permissions + gh.sh migration** | 🟢 Closed | Security hardening: removed unused `id-token: write`, oncall-triage now uses a controlled gh CLI wrapper |
| [#28533](https://github.com/anthropics/claude-code/pull/28533) | **gh.sh CLI wrapper** | 🟢 Closed | Security sandbox: only whitelisted commands like `issue view/list`, `search issues`, `label list` are allowed |
| [#23258](https://github.com/anthropics/claude-code/pull/23258) | **Question optimizer plugin** | 🟡 Open | Performance optimization: 4-condition detection for simple questions (interrogative/subject/verb/question mark), reducing AI thinking time |
| [#23946](https://github.com/anthropics/claude-code/pull/23946) | **Destructive command guard plugin** | 🟡 Open | Security plugin: PreToolUse hooks intercept dangerous operations like `rm -rf /` and `docker system prune` |
| [#23930](https://github.com/anthropics/claude-code/pull/23930) | **Fix AskUserQuestion examples missing description** | 🟡 Open | Developer experience: `skill-creator` crashes on `description.split`; document example fields completed |

---

## 5. Feature Request Trends

Based on an analysis of 50 active issues, the community focuses on five directions:

```
┌─────────────────────────────────────────────────────────┐
│  1. MCP ecosystem governance        ████████████████████  High priority      │
│     → tool isolation, result truncation, permission control, masking hooks │
│                                                         │
│  2. Windows platform stability      ██████████████████    Urgent fixes      │
│     → Cowork VM compatibility, MSIX container, special characters in paths │
│                                                         │
│  3. Enterprise security & compliance ████████████████     Rising fast       │
│     → audit logs, data masking, command interception, SSO/SAML            │
│                                                         │
│  4. Pricing and accessibility       ██████████████        Regional expansion │
│     → India/emerging-market pricing, education discounts, usage transparency │
│                                                         │
│  5. Remote development experience   ████████████          New-feature teething │
│     → Remote Control permission issues, multi-device sync, WSL support    │
└─────────────────────────────────────────────────────────┘
```

---

## 6. Developer Focus Areas

### 🔴 Blocking pain points
| Problem | Impact | Status |
|:---|:---|:---|
| **Remote Control permission chaos** | Feature unavailable to Pro/Max users | Clustered complaints today; the rollout strategy needs clarifying |
| **Cowork crashes across Windows editions** | Differences among Win11 Home/Pro/Insider | Docs updated to require Pro/Enterprise, but the implementation is still unstable |
| **Concurrent config write corruption** | Data loss for multi-session users | The race condition needs file locking or an SQLite migration |

### 🟡 High-frequency experience requests
- **MCP context pollution**: "Playwright tools shouldn't appear in every conversation" — needs a tool-scoping mechanism
- **Token usage anxiety**: weak visibility into cache invalidation, unpredictable long-session costs
- **Vim mode conflicts**: a single ESC in Plan Mode clears input, clashing with Vim muscle memory

### 🟢 Positive signals
- Auto-Memory shipping answers the long-standing memory management need
- The community automation PR (#28714) shows Anthropic exploring AI-driven governance
- The plugin ecosystem is taking shape: security/performance tools like the destructive command guard and question optimizer are emerging

---

> 📊 Data source: [anthropics/claude-code](https://github.com/anthropics/claude-code) | Statistics window: past 24 hours as of 2026-02-26

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Report | 2026-02-26

## Today at a Glance

Codex ships **v0.105.0 stable** today, bringing three headline features: TUI syntax highlighting, a theme selector, and voice input; meanwhile the community is in intense discussion around **MCP connection stability**, **Windows/WSL compatibility**, and **rate limit anomalies** — among 50 active issues, the MCP handshake failure thread with 37 comments is the number-one hotspot.

---

## Releases

### v0.105.0 (stable)
- **TUI visual upgrade**: syntax highlighting for fenced code blocks and diffs, a `/theme` selector with live preview, auto-adapting to terminal light/dark modes
- **Voice input**: hold the space bar to record and transcribe speech into text input

### v0.106.0-alpha.x series (alpha.1 through alpha.8)
- Fast-track iteration channel, mainly aimed at early testers

---

## Hot Community Issues (Top 10)

| # | Status | Title | Key takeaways | Community response |
|---|------|------|---------|---------|
| [#6020](https://github.com/openai/codex/issues/6020) | 🔴 OPEN | MCP client handshake failure: `connection closed` | **The MCP ecosystem's number-one blocker**, affecting all server connections, with clustered feedback from Pro users | 37 comments, 23 👍, unresolved for 4 months |
| [#12764](https://github.com/openai/codex/issues/12764) | 🔴 OPEN | 401 Unauthorized authentication failure | Newly appeared API authentication issue affecting 0.104.0 users | 15 comments, medium urgency |
| [#10939](https://github.com/openai/codex/issues/10939) | 🔴 OPEN | Cannot set gpt-5.3-codex via `/model` | Model access permissions out of sync with API availability, confusing ChatGPT Pro users | 15 comments, official reply: "the API usually opens within a week" |
| [#12827](https://github.com/openai/codex/issues/12827) | ✅ CLOSED | Voice transcription unresponsive (Linux/kitty) | Day-one bug of the new feature, quickly fixed | 12 comments, closed fast |
| [#3550](https://github.com/openai/codex/issues/3550) | 🔴 OPEN | VS Code extension: isolate conversation history per project/workspace | **Long-standing request**; the global conversation list causes multi-project confusion | 11 comments, 34 👍, open since 2025-09 |
| [#9224](https://github.com/openai/codex/issues/9224) | 🔴 OPEN | Remote control for Codex (phone→desktop) | **Highly upvoted creative feature**; users have workarounds but want official support | 10 comments, 47 👍 |
| [#10486](https://github.com/openai/codex/issues/10486) | 🔴 OPEN | Export Plan mode to Markdown | A workflow necessity; manual copying is tedious | 10 comments, 11 👍 |
| [#12728](https://github.com/openai/codex/issues/12728) | 🔴 OPEN | Rate limit consumption abnormally accelerated | Users report "burning 22% of the weekly quota in a day", suspected billing/throttling policy change | 8 comments, confirmed by multiple users |
| [#11179](https://github.com/openai/codex/issues/11179) | 🔴 OPEN | macOS App: diff panel showing 3 million changed lines freezes the app | **A performance disaster**, large-file diff rendering crashes | 7 comments, Plus user |
| [#12754](https://github.com/openai/codex/issues/12754) | 🔴 OPEN | macOS App crash: `Maximum call stack size exceeded` | Multi-Python-project workspaces trigger a routing stack overflow | 6 comments, 12 👍 |

---

## Notable PR Progress (Top 10)

| # | Status | Title | Technical value |
|---|------|------|---------|
| [#12900](https://github.com/openai/codex/pull/12900) | 🟡 OPEN | **Memories forgetting (diff-based memory decay)** | Solves long-session memory bloat, intelligently cleaning stale context |
| [#12727](https://github.com/openai/codex/pull/12727) | 🟡 OPEN | TUI: resolve resume/fork working directory via thread_id | Fixes path-resolution ambiguity in session resume, supports explicit UUID |
| [#12803](https://github.com/openai/codex/pull/12803) | 🟡 OPEN | Live skill refresh notifications | Removes the "restart to see new skills" misconception, supports `.agents/skills` hot-reloading |
| [#12866](https://github.com/openai/codex/pull/12866) | 🟡 OPEN | MCP OAuth resource parameter support | Fixes [#12589](https://github.com/openai/codex/issues/12589), supports RFC 8707 resource identifiers, a key fix for enterprise OAuth scenarios |
| [#12868](https://github.com/openai/codex/pull/12868) | 🟡 OPEN | TUI: submit pending nudges after streaming output | Fixes timing issues where nudge messages interleave with assistant output, improving interaction stability |
| [#12812](https://github.com/openai/codex/pull/12812) | 🟡 OPEN | Fine-grained incremental memory-forgetting prompt | Distinguishes `added_thread_ids` (ingestion queue) from `removed_thread_ids` (cleanup queue), optimizing memory management strategy |
| [#12873](https://github.com/openai/codex/pull/12873) | 🟡 OPEN | Default reasoning summary in the model catalog | Makes `model_reasoning_summary` optional, following model metadata defaults when unset |
| [#12612](https://github.com/openai/codex/pull/12612) | 🟡 OPEN | Unify rollout reconstruction and resume/fork metadata hydration | Technical debt cleanup, unifying history reconstruction logic as groundwork for complex session recovery |
| [#12870](https://github.com/openai/codex/pull/12870) | ✅ CLOSED | Restore visible line numbers for hidden file links | Fixes a TUI markdown link rendering regression, balancing clickability and readability |
| [#12763](https://github.com/openai/codex/pull/12763) | ✅ CLOSED | MCP OAuth resource parameter (community version) | The community contribution was inherited and extended by [#12866](https://github.com/openai/codex/pull/12866), showing open source collaboration |

---

## Feature Request Trends

| Direction | Heat | Typical issues | Insight |
|------|------|-----------|------|
| **MCP ecosystem stability** | 🔥🔥🔥🔥🔥 | #6020, #12869 | Protocol handshakes, streaming HTTP session expiry, OAuth configuration — MCP's growing pains moving from "works" to "works well" |
| **Windows/WSL experience** | 🔥🔥🔥🔥 | #10726, #12804, #12894, #12892 | Multiple platform adaptation issues in voice transcription, scrolling, link opening; Microsoft-ecosystem users are a significant share |
| **Rate limit transparency** | 🔥🔥🔥🔥 | #12728, #12799 | Quota consumption is a "black box"; users need finer-grained usage feedback mechanisms |
| **TUI/editor experience** | 🔥🔥🔥 | #12749, #12840, #10486 | Theme customization, diff readability, Plan export — professional developers' workflow integration needs |
| **Cross-device collaboration** | 🔥🔥🔥 | #9224 | Phone-desktop pairing is becoming a differentiation point |
| **Deep VS Code integration** | 🔥🔥 | #3550, #6403 | Workspace isolation, Codespaces OAuth redirects — the native IDE experience vs CLI trade-off |

---

## Developer Focus Areas

### 🔴 High-frequency pain points

1. **"Connection as a service" MCP reliability**
   - Handshake failures, degradation after session expiry, complex OAuth configuration — as the core extension mechanism, MCP's stability directly affects productivity

2. **Platform consistency gap**
   - macOS features first → Linux/WSL lag → Windows adaptation problems; a gap between cross-platform promises and actual experience

3. **Rate limit "surprises"**
   - Unchanged usage patterns suddenly trigger quota alarms; no real-time usage dashboard

### 🟡 Emerging expectations

4. **Voice interaction maturity**
   - 0.105.0 day one exposed platform differences (Linux unresponsive, Windows 403, WSL not enabled), iterating fast

5. **Refined memory/context management**
   - From "remember everything" to "smart forgetting"; the community expects explainable, controllable long-term memory strategies

6. **Enterprise/team scenarios**
   - OAuth resource parameters, multi-account switching ([#12872](https://github.com/openai/codex/pull/12872)), workspace isolation — evolving from a personal tool to team collaboration

---

*This report is generated from public GitHub data; follow [openai/codex](https://github.com/openai/codex) for the latest updates*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Report | 2026-02-26

## Today at a Glance

Gemini CLI released **v0.30.0-nightly** today, adding 3.1 Pro Preview model support and expandable MCP tool details. Community activity is surging, with **Remote Agents** as the absolute focus — the official team released three Sprint milestone issues in a row, while the local subagent feature is close to being enabled by default. Developers strongly want interaction improvements, with multiple AskUser tool improvement suggestions surfacing in quick succession.

---

## Releases

### [v0.30.0-nightly.20260226.f9f916e1d](https://github.com/google-gemini/gemini-cli/releases/tag/v0.30.0-nightly.20260226.f9f916e1d)

| Update | Description |
|:---|:---|
| **3.1 Pro Preview model** | Added to the behavior evaluation suite; developers can test next-generation model capabilities early |
| **PR rate limit** | Added `feat:PR-rate-limit`, improving GitHub API call frequency control |
| **MCP tool interaction improvements** | Supports expanding full MCP tool details at approval time, improving transparency |

---

## Hot Community Issues (Top 10)

| # | Issue | Key takeaways | Community response |
|:---|:---|:---|:---|
| [#20169](https://github.com/google-gemini/gemini-cli/issues/20169) | API Error: gemini-3-flash-preview insufficient capacity | **Service stability alarm**: the new model preview frequently triggers capacity limit errors, hurting production availability | 🔥 8 comments, urgent triage needed |
| [#20142](https://github.com/google-gemini/gemini-cli/issues/20142) | AskUser open questions don't support Ctrl+R history search | Pain point for repeated-input scenarios; developers strongly want chat history search reused here | 🔥 8 comments, tagged `help wanted` |
| [#20302](https://github.com/google-gemini/gemini-cli/issues/20302) | [Epic] Remote Agents Sprint 1 - infrastructure | **Strategic feature**: remote agent infrastructure and streaming support, core of the official roadmap | 3 comments, P0 priority |
| [#18896](https://github.com/google-gemini/gemini-cli/issues/18896) | Windows screen flicker/tearing while scrolling | Long-standing terminal rendering issue affecting the Windows developer experience | 5 comments, P2 priority |
| [#20177](https://github.com/google-gemini/gemini-cli/issues/20177) | Agent uses AskUser instead of standard tool confirmation | Inconsistent interaction design: simple shell commands still need manual confirmation, breaking flow | 4 comments, needs a product decision |
| [#20304](https://github.com/google-gemini/gemini-cli/issues/20304) | [Epic] Remote Agents Sprint 3 - advanced infrastructure | Remote agent OAuth and machine-to-machine authentication, enterprise-grade needs | 2 comments, P2 priority |
| [#20181](https://github.com/google-gemini/gemini-cli/issues/20181) | AskUser support answering open questions in an external editor | Long-text input scenarios (like Conductor track descriptions) urgently need editor support | 3 comments, experience improvement |
| [#18953](https://github.com/google-gemini/gemini-cli/issues/18953) | Complex shell commands execute extremely slowly | "100x slower than running directly in the CLI"; terminal animations and progress UX drag down performance | 3 comments, performance bottleneck |
| [#20347](https://github.com/google-gemini/gemini-cli/issues/20347) | `/memory add` fails in Plan Mode | User-initiated commands blocked by agent mode; the permission model needs redesign | 2 comments, tool permission boundaries |
| [#20312](https://github.com/google-gemini/gemini-cli/issues/20312) | [Experiment] Subagents enabled by default | **Milestone signal**: the local subagent feature is approaching GA, final acceptance needed | 1 comment, experiment graduating |

---

## Notable PR Progress (Top 10)

| # | PR | Feature/fix | Technical value |
|:---|:---|:---|:---|
| [#20430](https://github.com/google-gemini/gemini-cli/pull/20430) | Native policy file support for blocking Hook execution | Introduces `[[hook_rule]]` configuration, fixing hooks mistakenly going through `run_shell_command` policy checks | Finer-grained enterprise security policies |
| [#20429](https://github.com/google-gemini/gemini-cli/pull/20429) | `/memory list` interactive UI + shortcuts | `Ctrl+X` opens files/folders; memory management upgraded from a text list to a TUI | Major productivity boost |
| [#20416](https://github.com/google-gemini/gemini-cli/pull/20416) | Context-aware escape correction replaces heuristics | Cures Gemini's over-escaping bug (`\n` literal issues), moving from "guessing" to "precise fixes" | Key data-integrity fix |
| [#20403](https://github.com/google-gemini/gemini-cli/pull/20403) | Deferred settings loading prevents closure data loss | Fixes state corruption during `onModelChange` hot-reload/runtime config changes | Runtime stability |
| [#20274](https://github.com/google-gemini/gemini-cli/pull/20274) | Subagents generate unique Session IDs | Fixes log overwriting caused by parent and child agents sharing a Session ID | Observability foundation |
| [#20419](https://github.com/google-gemini/gemini-cli/pull/20419) | Tool-only responses refresh the Transcript | Extends #17996, ensuring `BeforeTool` hooks see complete state | Hook system reliability |
| [#20414](https://github.com/google-gemini/gemini-cli/pull/20414) | Fix Ctrl+O expansion hint flicker | Optimizes message show/hide timing, removing visual noise | Interaction polish |
| [#20422](https://github.com/google-gemini/gemini-cli/pull/20422) | Remove deprecated preview flag docs | Gemini 3 has been enabled by default since v0.29.0; documentation cleanup debt | Documentation accuracy |
| [#20326](https://github.com/google-gemini/gemini-cli/pull/20326) | Windows WSL development environment guide | Solves native dependency and sandbox issues for Windows contributors | Developer experience, lower contribution barrier |
| [#19821](https://github.com/google-gemini/gemini-cli/pull/19821) | Multi-architecture sandbox Docker builds | Fixes ARM64 (Raspberry Pi 5 etc.) `exec format error` crashes | Platform compatibility expansion |

---

## Feature Request Trends

```
┌─────────────────────────────────────────────────────────┐
│  🔥 Remote agent architecture       ████████████████████  │
│     - Sprints 1/2/3 released in sequence, covering P0-P2 priorities │
│                                                         │
│  🧠 Subagent ecosystem              ██████████████████    │
│     - Local subagent Sprint 1 underway, experiment flag about to be removed │
│                                                         │
│  💬 AskUser interaction improvements ████████████████      │
│     - History search, external editor, simplified confirmation - three arrows at once │
│                                                         │
│  ⚡ Performance and stability        ██████████████        │
│     - Screen flicker, slow command execution, API retry strategy │
│                                                         │
│  🔒 Enterprise features             ████████████          │
│     - Policy engine, headless mode, Hook blocking control │
│                                                         │
│  🏠 Local model support             ████████              │
│     - Local inference demand like Gemma 3 emerging (#20427 feature request) │
└─────────────────────────────────────────────────────────┘
```

---

## Developer Focus Areas

| Pain point category | Specific feedback | Representative issue |
|:---|:---|:---|
| **Model availability anxiety** | Frequent "No capacity available" errors, insufficient preview stability | #20169 |
| **Windows as a second-class citizen** | Screen flicker, difficult dev environment setup; a clear gap vs macOS/Linux | #18896, #20326 |
| **Interaction efficiency bottlenecks** | AskUser breaks flow, no history search, limited long-text input | #20142, #20177, #20181 |
| **Performance black box** | Slow complex shell commands, no progress visibility, false-positive loop detection | #18953, #19519 |
| **Tool permission confusion** | Plan Mode blocks user-initiated commands; the security-vs-convenience boundary is blurry | #20347, #20331 |
| **Local privacy demands** | Want support for local models like Gemma to avoid cloud dependency | #20427 |

---

*This report is generated from public data at github.com/google-gemini/gemini-cli*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Report | 2026-02-26

## Today at a Glance

Kimi Code CLI released stable **v1.14.0** today, adding Wire mode Steer support and improving Web/ACP usage docs. Community activity is markedly up, with 8 new open issues in a single day; MCP ecosystem stability and interaction experience are the developer focus.

---

## Releases

### v1.14.0 (2026-02-26)

| Category | Update |
|:---|:---|
| **Docs** | Added getting-started guides for the Kimi Web and Kimi ACP usage modes ([#1225](https://github.com/MoonshotAI/kimi-cli/pull/1225)) |
| **Feature** | Wire mode adds Steer support for finer-grained AI behavior control ([#1228](https://github.com/MoonshotAI/kimi-cli/pull/1228)) |
| **Fix** | Improved shortcut display adaptation on the Web platform |

---

## Hot Community Issues

### 🔴 High priority: MCP ecosystem stability

| # | Title | Status | Criticality | Community response |
|:---|:---|:---|:---|:---|
| [#769](https://github.com/MoonshotAI/kimi-cli/issues/769) | Should not exit automatically when an MCP connection fails | ⭕ OPEN | ⭐⭐⭐⭐⭐ | 👍×3, suggests matching the fault tolerance of Codex/Claude Code |
| [#1253](https://github.com/MoonshotAI/kimi-cli/issues/1253) | MCP server startup conflicts | ⭕ OPEN | ⭐⭐⭐⭐⭐ | New issue; developers building their own MCP hit port/process conflicts |
| [#1248](https://github.com/MoonshotAI/kimi-cli/issues/1248) | kimi code cli conflicts with mcp at runtime | ⭕ OPEN | ⭐⭐⭐⭐⭐ | The `notifications/initialized` message triggers a ValidationError |

> **Analysis**: as Kimi CLI's core extension mechanism, MCP's current "crash on any single point of failure" design severely hurts production availability. The community strongly calls for a degradation strategy like Claude Code's, allowing continued operation when some MCP servers fail.

---

### 🟡 Interaction experience improvements

| # | Title | Status | Criticality | Community response |
|:---|:---|:---|:---|:---|
| [#751](https://github.com/MoonshotAI/kimi-cli/issues/751) | Execute slash commands immediately on selection | ⭕ OPEN | ⭐⭐⭐⭐☆ | Saves one Enter press, improves flow |
| [#1252](https://github.com/MoonshotAI/kimi-cli/issues/1252) | Support number-key selection in CLI permission prompts | ⭕ OPEN | ⭐⭐⭐⭐☆ | Asks for parity with the WebUI; related PR #1256 already closed |
| [#1249](https://github.com/MoonshotAI/kimi-cli/issues/1249) | Check the shell environment on new session | ⭕ OPEN | ⭐⭐⭐⭐☆ | PowerShell users' pain point: the AI mistakenly sends bash commands |

---

### 🟢 Authentication and deployment

| # | Title | Status | Criticality | Community response |
|:---|:---|:---|:---|:---|
| [#1250](https://github.com/MoonshotAI/kimi-cli/issues/1250) | kimi code Failed to get models: 401 | ⭕ OPEN | ⭐⭐⭐⭐☆ | Newly reported on v1.14.0, authentication flow anomaly |
| [#1231](https://github.com/MoonshotAI/kimi-cli/issues/1231) | Kimi Claw cannot log in to Kimi Cli | ✅ CLOSED | ⭐⭐⭐⭐☆ | The OAuth browser flow limits use in server environments |

---

### ✅ Fixed issues (closed within 24h)

| # | Title | Fix |
|:---|:---|:---|
| [#1217](https://github.com/MoonshotAI/kimi-cli/issues/1217) | Image processing hangs | v1.12.0 image processing blocking issue |
| [#1220](https://github.com/MoonshotAI/kimi-cli/issues/1220) | HTTP header polluted by Ubuntu kernel version | Special characters caused connection failures |
| [#1222](https://github.com/MoonshotAI/kimi-cli/issues/1222) | 413 Request Entity Too Large | Oversized request body handling |
| [#1224](https://github.com/MoonshotAI/kimi-cli/issues/1224) | Unusable inside JetBrains IDEA | IDE terminal compatibility issue |
| [#1226](https://github.com/MoonshotAI/kimi-cli/issues/1226) [#1227](https://github.com/MoonshotAI/kimi-cli/issues/1227) | LLM provider connection error | Batch fix for connection errors |

---

## Notable PR Progress

| # | Author | Status | Feature/fix |
|:---|:---|:---|:---|
| [#1257](https://github.com/MoonshotAI/kimi-cli/pull/1257) | @RealKai42 | ⭕ OPEN | **Simplified shell prompt**: removed username/working-directory prefixes; the status bar gains a top separator and adaptive shortcut hints |
| [#1256](https://github.com/MoonshotAI/kimi-cli/pull/1256) | @RealKai42 | ✅ CLOSED | **Number-key selection support**: Q&A and permission panels support quick selection with keys 1-5 (merged in place of #1252) |
| [#1255](https://github.com/MoonshotAI/kimi-cli/pull/1255) | @RealKai42 | ✅ CLOSED | **Tab-style multi-question navigation**: Shell/Web Q&A dialogs support tab switching with automatic state save/restore |
| [#1246](https://github.com/MoonshotAI/kimi-cli/pull/1246) | @RealKai42 | ✅ CLOSED | **End-to-end AskUserQuestion support**: unified structured user-question flow across Wire/Shell/Web |
| [#1254](https://github.com/MoonshotAI/kimi-cli/pull/1254) | @RealKai42 | ✅ CLOSED | **Process title setting**: the CLI main process shows as `Kimi Code` and the Web worker as `kimi-code-worker`, easier to monitor |
| [#1236](https://github.com/MoonshotAI/kimi-cli/pull/1236) | @CyCle1024 | ⭕ OPEN | **Proxy environment trust**: enables `trust_env` on `aiohttp.ClientSession`, supporting system proxy auto-discovery |
| [#1229](https://github.com/MoonshotAI/kimi-cli/pull/1229) | @privatejava | ⭕ OPEN | **HTTP header whitespace fix**: trims leading/trailing spaces from header values, preventing the h11 library from refusing to parse |
| [#1223](https://github.com/MoonshotAI/kimi-cli/pull/1223) | @kingdomseed | ⭕ OPEN | **Azure Kimi support**: allows `default_query` and `custom_headers` to pass through to the OpenAI client |
| [#1131](https://github.com/MoonshotAI/kimi-cli/pull/1131) | @IndenScale | ⭕ OPEN | **AgentHooks framework**: internal testing support with built-in dangerous-command interception and test-enforcement hooks |
| [#1127](https://github.com/MoonshotAI/kimi-cli/pull/1127) | @anxndsgn | ⭕ OPEN | **Web UI polish**: minor interface tweaks (specific changes to be added) |

> **Observation**: @RealKai42 contributed 5 PRs today, concentrating on the interaction experience layer; number-key selection and Tab navigation meaningfully improve CLI efficiency.

---

## Feature Request Trends

Cluster analysis based on 15 active issues:

```
┌─────────────────────────────────────────┐
│  MCP ecosystem stability   ████████████  27% │
│  Interaction improvements  ██████████    23% │
│  Auth/deployment issues    ████████      18% │
│  IDE/editor integration    ██████        14% │
│  Network/proxy support     ████          10% │
│  Other feature requests    ███            8% │
└─────────────────────────────────────────┘
```

**Core trends**:
1. **MCP fault tolerance** is the top ask — developers need production-grade extension stability
2. **Cross-platform consistency** — WebUI and CLI feature parity (number keys, permission panels)
3. **Enterprise environment adaptation** — proxies, reverse proxies, browser-less login and other deployment scenarios

---

## Developer Focus Areas

### 🔥 High-frequency pain points

| Pain point | Typical scenario | Related issues |
|:---|:---|:---|
| **MCP single point of failure** | Any MCP failure crashes the CLI; no degraded operation | #769, #1253, #1248 |
| **No shell environment awareness** | In PowerShell the AI keeps emitting bash commands | #1249 |
| **OAuth limits server deployment** | Remote servers/containers can't complete browser login | #1231 |
| **Header pollution** | System information leaks into HTTP headers and breaks connections | #1220, #1229 |

### 💡 Community expectations

- **Short term**: MCP error isolation + number-key selection merged into mainline soon
- **Mid term**: API key auth replacing OAuth, supporting pure command-line environments
- **Long term**: an MCP marketplace/registry mechanism to lower the barrier for custom extensions

---

*Report generated at: 2026-02-26 | Data source: github.com/MoonshotAI/kimi-cli*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Report | 2026-02-26

## Today at a Glance

OpenCode shipped the v1.2.14/v1.2.15 double release today, focusing on fixing Windows Bun runtime crashes; community issues surged by 50, with `.env` files triggering a ThreadLock panic as the most frequent failure; on the PR side, heavyweight features like Agent Teams multi-session collaboration and Windows code signing are emerging.

---

## Releases

### v1.2.15 (latest)
| Module | Update |
|:---|:---|
| **Core** | Fixed most segfaults on Windows + Bun v1.3.10; separated TUI and server configuration |
| **Desktop** | Removed the sidecar interactive shell flag, fixing the macOS startup hang; fixed sub-session permissions and question handling; improved keyboard navigation |

### v1.2.14
| Module | Update |
|:---|:---|
| **Core** | Added a message deletion endpoint (@shantur) |
| **TUI** | Consumes stdout and process exit concurrently, fixing the auth login block (@Ayushlm10) |

> 💡 Community contributors: @Ayushlm10, @shantur

---

## Hot Community Issues (Top 10)

| # | Title | Status | Comments/👍 | Key takeaways |
|:---|:---|:---|:---|:---|
| [#4283](https://github.com/anomalyco/opencode/issues/4283) | TUI copy-to-clipboard broken | 🔴 OPEN | 56 / 42 | The longest-standing UI ailment, unfixed since v1.0.62, hurting basic interaction |
| [#8829](https://github.com/anomalyco/opencode/issues/8829) | GitHub Copilot gemini3pro model unsupported | 🔴 OPEN | 30 / 8 | Paid model adaptation lags for enterprise users, a gap versus Claude/GPT support |
| [#10221](https://github.com/anomalyco/opencode/issues/10221) | Fresh install shows a black screen, unresponsive | 🔴 OPEN | 25 / 13 | Crashes at startup, blocking new-user conversion; diagnostic tooling needed |
| [#15015](https://github.com/anomalyco/opencode/issues/15015) | `.env` file triggers Bun ThreadLock panic | 🟢 CLOSED | 10 / 5 | **Today's most frequent failure**, introduced in v1.2.11, emergency-fixed in v1.2.15 |
| [#14734](https://github.com/anomalyco/opencode/issues/14734) | Windows multi-agent segfault at startup | 🟢 CLOSED | 8 / 0 | Shares a root cause with #15015; Bun runtime stability is the Windows bottleneck |
| [#15127](https://github.com/anomalyco/opencode/issues/15127) | Crashes whenever `.env` has any content | 🟢 CLOSED | 8 / 0 | Clear reproduction path: empty files are fine, any content guarantees a crash |
| [#14982](https://github.com/anomalyco/opencode/issues/14982) | Unexpectedly requests iCloud/Photos permission | 🔴 OPEN | 7 / 3 | Privacy-sensitive; users question the sandbox mechanism, compliance explanations needed |
| [#14289](https://github.com/anomalyco/opencode/issues/14289) | claude-opus-4.6 vision capability not recognized | 🔴 OPEN | 12 / 1 | New model capability mapping lags; Azure already supports it but OpenCode hasn't caught up |
| [#13230](https://github.com/anomalyco/opencode/issues/13230) | Memory leak freezes the system (111GB/21GB) | 🔴 OPEN | 4 / 10 | **Critical severity**; catastrophic failure in Linux production, OOM killer ineffective |
| [#15195](https://github.com/anomalyco/opencode/issues/15195) | Desktop doesn't inherit the full PATH environment variable | 🔴 OPEN | 5 / 0 | A v1.2.15 regression; the TUI works but Desktop can't find commands |

---

## Notable PR Progress (Top 10)

| # | Title | Author | Type | Value |
|:---|:---|:---|:---|:---|
| [#15205](https://github.com/anomalyco/opencode/pull/15205) | Agent Teams: DB-level parallel multi-session collaboration | @DXM666 | ✨ Feature | Architecture-level breakthrough; the main session can spawn cooperating sub-sessions, enabling divide-and-conquer for complex tasks |
| [#15211](https://github.com/anomalyco/opencode/pull/15211) | Fix Desktop PATH environment variable inheritance | @nexxeln | 🐛 Fix | Emergency fix for #15195; probes the SHELL environment and injects safely |
| [#15201](https://github.com/anomalyco/opencode/pull/15201) | Windows CLI/Desktop code signing | @Hona | 🔧 Infra | Azure Trusted Signing + Tauri signing, resolving antivirus false positives |
| [#15203](https://github.com/anomalyco/opencode/pull/15203) | OpenCode Go provider list improvements | @iamdavidhill | ♻️ Refactor | Distinguishes Zen/Go versions, reducing user confusion |
| [#14969](https://github.com/anomalyco/opencode/pull/14969) | Bedrock IAM credential connection flow | @tristan-stahnke-GPS | 🐛 Fix | Replaces the API key form, supporting AK/SK/Region three-part authentication |
| [#13514](https://github.com/anomalyco/opencode/pull/13514) | Fix multiple memory leaks | @sebishogun | 🐛 Fix | Targets #13230; cleans up Bus subscriptions, compaction data, FileTime state |
| [#14707](https://github.com/anomalyco/opencode/pull/14707) | Automatic compaction recovery on 413 errors | @bentrd | 🐛 Fix | Auto-compacts on context overflow, avoiding request-entity-too-large crashes |
| [#14374](https://github.com/anomalyco/opencode/pull/14374) | Git worktree selector | @swalker326 | 🐛 Fix | Header-level switching for multi-workspace projects, solving the long-standing #13782 pain |
| [#12829](https://github.com/anomalyco/opencode/pull/12829) | Embed the Web UI into the binary | @BlankParticle | ✨ Feature | Works in offline environments, packaged at build time, toggleable via a flag |
| [#14621](https://github.com/anomalyco/opencode/pull/14621) | Improved diff/code comment display | @adamdotdevin | ✨ Feature | Code review experience upgrade, details pending |

---

## Feature Request Trends

```
┌─────────────────────────────────────────┐
│  🔥 Stability and performance (35%)     │
│    · Windows Bun runtime crashes        │
│    · Memory leaks / OOM / system freezes │
│    · Startup black screen / unresponsive │
├─────────────────────────────────────────┤
│  🤖 Model ecosystem expansion (25%)     │
│    · Fast adaptation of new models (gemini3pro/claude-opus-4.6) │
│    · Vision capability recognition      │
│    · Better provider auth options (Bedrock IAM) │
├─────────────────────────────────────────┤
│  🖥️ Desktop experience (20%)            │
│    · PATH/environment variable inheritance │
│    · Transparent permission requests (iCloud/Photos) │
│    · Basic interactions like clipboard/keyboard navigation │
├─────────────────────────────────────────┤
│  🔧 Enterprise features (15%)           │
│    · Intranet deployment / custom Web UI proxy │
│    · Domestic IM integrations like Feishu/DingTalk │
│    · Azure DevOps Pipeline support      │
├─────────────────────────────────────────┤
│  🧩 Developer toolchain (5%)            │
│    · Claude Code hooks compatibility    │
│    · Git worktree / GPG commit support  │
└─────────────────────────────────────────┘
```

---

## Developer Focus Areas

| Pain point tier | Manifestation | Representative issues |
|:---|:---|:---|
| **P0 blocking** | Windows users can't start the app; `.env` files become "landmines" | #15015, #15127, #15159, #15174 |
| **P1 high-frequency failures** | Copy-paste broken, black screens, permission popups startling users | #4283, #10221, #14982 |
| **P2 experience gaps** | Desktop and TUI behave inconsistently; environment isolation is messy | #15195, #14438 |
| **P3 ecosystem lag** | New model support slower than competitors; limited enterprise auth options | #8829, #14289, #2957 |
| **P4 architectural debt** | Memory management and the concurrency model spiral out of control in extreme scenarios | #13230, #14734 |

> **Today's action advice**: Windows users should hold off upgrading to v1.2.11-1.2.14 and jump straight to v1.2.15; Linux production users should track the #13230 memory leak fix progress.

---

*Data source: github.com/anomalyco/opencode | Generated at: 2026-02-26*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

⚠️ Summary generation failed.

</details>

---
*This report was auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*