# AI CLI Community Report 2026-03-02

> Generated at: 2026-03-02 00:07 UTC | Tools covered: 6

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Tools Ecosystem Comparison Report | 2026-03-02

## 1. Ecosystem Overview

The AI CLI tool market currently shows a "one leader, many strong challengers" pattern. Claude Code holds the dominant ecosystem position on the strength of Anthropic's models, while fast followers such as OpenAI Codex and Google Gemini CLI iterate quickly through differentiated features. The community contribution model has shifted from "filing requests" to "implementing directly", and the plugin/MCP ecosystem has become the focal point of competition among platforms. The Chinese-market tools (Kimi, Qwen) are catching up fast but still trail on international standards and remote deployment capability. The industry as a whole is evolving from "features that work" toward "enterprise-ready", with stability, billing transparency, and multi-environment adaptation as the shared bottlenecks.

---

## 2. Activity Comparison by Tool

| Tool | Issues Today | PRs Today | Version Releases | Community Activity Rating |
|:---|:---:|:---:|:---:|:---|
| **Claude Code** | 10+ hot | 10+ open | None | ⭐⭐⭐⭐⭐ Extremely high |
| **OpenAI Codex** | 10+ hot | 10+ open | None | ⭐⭐⭐⭐⭐ Extremely high |
| **Gemini CLI** | 10+ hot | 10+ open | None | ⭐⭐⭐⭐⭐ Extremely high |
| **Kimi Code CLI** | 4 | 4 | None | ⭐⭐⭐☆☆ Medium |
| **OpenCode** | 10+ hot | 10+ open | None | ⭐⭐⭐⭐☆ High |
| **Qwen Code** | 7 | 10 | v0.11.0-nightly | ⭐⭐⭐⭐☆ High |

> **How to read this**: Claude Code/Codex/Gemini form the first tier with 20+ community contributions per day; OpenCode is heating up as the open-source alternative; Kimi's activity is lower but its issues are focused; Qwen iterates intensively for Chinese-language scenarios.

---

## 3. Shared Functional Priorities

| Functional direction | Tools involved | Specific demands | Urgency |
|:---|:---|:---|:---:|
| **Remote/headless environment adaptation** | Claude Code (Cowork VM), Codex (SSH), Kimi (SSH), OpenCode (Server) | Full support for containers, CI/CD, SSH bastion hosts, and headless servers | 🔴 P0 |
| **Billing transparency and controllability** | Codex (usage anomalies), OpenCode (Copilot billing errors), Qwen (free-quota guidance) | Real-time dashboards, hard spending caps, correct classification of agent requests, friendly guidance when quota runs out | 🔴 P0 |
| **MCP/plugin ecosystem governance** | Claude Code (subagent permissions), Codex (zombie processes), Gemini (MCP toggle), OpenCode (runtime tool toggle) | Process lifecycle management, permission consistency, tool hot-swapping, protection against context explosion | 🟡 P1 |
| **Plan mode professionalization** | Claude Code, Gemini, OpenCode, Qwen | Shift from "one-shot approval" to "collaborative iteration", with support for annotations, external editors, and state restoration | 🟡 P1 |
| **Stability and memory management** | OpenCode (116GB leak), Gemini (JS heap exhaustion), Codex (MCP leak) | No crashes in long sessions, uninterrupted compaction, orphan process reclamation | 🔴 P0 |
| **AGENTS.md standardization** | Claude Code (#29835), Qwen (#2018) | Parity with CLAUDE.md to lower migration costs for multi-agent projects | 🟢 P2 |

---

## 4. Differentiated Positioning

| Tool | Core functional focus | Target user profile | Technical approach |
|:---|:---|:---|:---|
| **Claude Code** | Cowork VM collaboration, deep IDE integration, plugin ecosystem | Enterprise dev teams, users who need securely isolated environments | Closed source + official plugin marketplace, emphasizing "Agent as a Service" |
| **OpenAI Codex** | Voice interaction, real-time collaboration, parallel Subagents | Pro/Plus paying users, those chasing the latest model capabilities | Tightly bound to the OpenAI model stack, voice-first design |
| **Gemini CLI** | Remote agent infrastructure, Plan mode professionalization | Google Cloud ecosystem users, multimodal use cases | Sprint-based development, deep MCP protocol integration |
| **Kimi Code CLI** | Chinese-language scenario optimization, Alibaba Cloud ecosystem integration | Chinese developers, Alibaba Cloud users | Localization first, international capabilities still to be filled in |
| **OpenCode** | Multi-provider support, open-source customizability, enterprise compliance | Open-source advocates, enterprises with multi-model strategies, security-conscious organizations | Maximum openness, rapid onboarding of new providers |
| **Qwen Code** | Chinese-language stability, Alibaba Cloud Coding Plan commercialization | Chinese-language developers, Alibaba Cloud paying users | Deep optimization for Chinese scenarios, clear business model |

---

## 5. Community Buzz and Maturity

```
Maturity matrix (horizontal axis: feature completeness, vertical axis: community activity)

High activity │
              │    🟢 Claude Code    🟢 Gemini CLI
              │    (mature ecosystem)  (rapid iteration)
              │
              │              🟡 OpenCode
              │         (feature catch-up phase)
              │
              │    🟢 OpenAI Codex    🟡 Qwen Code
              │    (high buzz / stability pain)  (Chinese-market depth)
              │
              │              🔵 Kimi Code CLI
              │              (early stage)
              └─────────────────────────────────────
                   Low completeness            High completeness
```

| Stage | Tools | Key characteristics |
|:---|:---|:---|
| **Mature ecosystem stage** | Claude Code | Active plugin marketplace, but Cowork/VM-layer stability drags down its reputation |
| **Rapid iteration stage** | Gemini CLI, Codex | Feature-dense releases, with remote agents/voice as differentiating bets |
| **Feature catch-up stage** | OpenCode, Qwen | Multi-provider onboarding / Chinese-language optimization, accumulating stability debt |
| **Early build-out stage** | Kimi | Basic features usable, with obvious gaps in enterprise scenario fit |

---

## 6. Trend Signals Worth Watching

| Trend | Signal sources | Reference value for developers |
|:---|:---|:---|
| **"Agents as infrastructure"** | Gemini remote-agent Sprints, Claude Cowork VM | Future CLI tools will ship built-in lightweight runtime environments, and seamless switching between local development and remote execution will become table stakes |
| **The billing-transparency war** | Codex usage anomalies, OpenCode Copilot incident, Qwen paywall guidance | Enterprise procurement will mandate observable token/request-level billing; "black-box billing" tools will be eliminated |
| **MCP becomes the de facto standard** | All 6 tools deeply integrated | Investing in MCP tool development pays off across platforms, but watch the differences in process governance and permission models |
| **Chinese-scenario technical debt becomes visible** | Qwen whitespace issues, Kimi remote adaptation | Chinese-language developers should assess how deep a tool's CJK support goes; tools not internationalization-native carry hidden costs |
| **A window for open-source alternatives** | OpenCode's dense multi-provider PRs, Claude Code's closed-source restrictions | Enterprise wariness of vendor lock-in creates openings for alternatives like OpenCode, at the price of stability risk |
| **"Preventive security" design** | Claude push-guardrails, Qwen VibeGuard, OpenCode portable mode | Security shifts from "post-hoc audit" to "pre-emptive blocking"; pre-push visibility checks and PII masking become compliance must-haves |

---

*This report is generated from each tool's public GitHub data as of 2026-03-02; validate with a POC against your specific business scenarios.*

---

## Detailed Reports by Tool

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Community Hotspots

> Data source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Hotspots Report (2026-03-02)

---

## 1. Top Skills Ranking (by community attention)

| Rank | Skill | Overview | Status | Link |
|:---|:---|:---|:---|:---|
| 1 | **skill-quality-analyzer / skill-security-analyzer** | Meta Skills: automatically assess the quality of other Skills across 5 dimensions (structure, documentation, security, and more) | 🔵 Open | [#83](https://github.com/anthropics/skills/pull/83) |
| 2 | **frontend-design** | An optimized frontend design skill, improving instruction clarity and single-turn executability | 🔵 Open | [#210](https://github.com/anthropics/skills/pull/210) |
| 3 | **codebase-inventory-audit** | Codebase health audit: a 10-step workflow that identifies orphaned code, unused files, documentation gaps, and more | 🔵 Open | [#147](https://github.com/anthropics/skills/pull/147) |
| 4 | **Google Workspace integration suite** | 6 Agent Skills enabling email triage, drafts, calendar, and task management via GOG CLI | 🔵 Open | [#299](https://github.com/anthropics/skills/pull/299) |
| 5 | **ShieldCortex** | Persistent memory system + AI agent security framework (threat detection, trust scoring, audit trails) | 🔵 Open | [#386](https://github.com/anthropics/skills/pull/386) |
| 6 | **masonry-generate-image-and-videos** | Masonry CLI integration: Imagen 3.0 image generation, Veo 3.1 video generation | 🔵 Open | [#335](https://github.com/anthropics/skills/pull/335) |
| 7 | **SAP-RPT-1-OSS predictor** | SAP open-source tabular foundation model integration for enterprise predictive analytics | 🔵 Open | [#181](https://github.com/anthropics/skills/pull/181) |
| 8 | **flutter-theme-factory** | Flutter theme factory: 12 preset themes (including ColorScheme, Google Fonts, light/dark modes) | 🔵 Open | [#368](https://github.com/anthropics/skills/pull/368) |

---

## 2. Community Demand Trends (distilled from Issues)

| Trend | Representative issue | Core demand |
|:---|:---|:---|
| **🔐 Agent governance and security** | [#412](https://github.com/anthropics/skills/issues/412) | Lacking skills for policy enforcement, threat detection, and audit trails for AI agent systems |
| **⚙️ Skills as MCP services** | [#16](https://github.com/anthropics/skills/issues/16) | Expose Skills as standard MCP interfaces for cross-tool reuse |
| **📦 Skills package manager** | [#185](https://github.com/anthropics/skills/issues/185) | The community project [skills-mcp](https://github.com/leezhuuuuu/skills-mcp) is pushing a standardized distribution mechanism |
| **🛠️ Enterprise-grade workflows** | [#202](https://github.com/anthropics/skills/issues/202) | skill-creator needs to evolve from "teaching documentation" into an "efficient execution tool" |
| **☁️ Multi-cloud/Bedrock compatibility** | [#29](https://github.com/anthropics/skills/issues/29) | Support for running Skills in non-Claude-native environments |

---

## 3. High-Potential Skills Pending Merge (active comments + recent updates)

| Skill | Key value | Last updated | Link |
|:---|:---|:---|:---|
| **feature-dev workflow fix** | Fixes the TodoWrite overwrite bug, resolving skipped Phase 6-7 | 2026-02-12 | [#363](https://github.com/anthropics/skills/pull/363) |
| **YAML special-character pre-check** | Adds detection of unquoted special characters in `quick_validate.py` to prevent silent parse errors | 2026-02-12 | [#361](https://github.com/anthropics/skills/pull/361) |
| **skill-creator UTF-8 encoding fix** | A definitive fix for UnicodeDecodeError on Windows | 2026-01-30 | [#284](https://github.com/anthropics/skills/pull/284) |
| **webapp-testing dependency declaration** | Adds `requirements.txt` to pre-declare Playwright dependencies, reducing runtime friction | 2026-02-01 | [#282](https://github.com/anthropics/skills/pull/282) |

---

## 4. Skills Ecosystem Insights

> **Key takeaway**: The community is leaping from "single-point tool skills" to "a meta-capability layer (Meta-Skills) + enterprise governance frameworks" — it needs both quality infrastructure that can audit/generate other Skills (e.g. #83) and, urgently, production-grade capabilities such as agent security, MCP standardization, and multi-cloud deployment, reflecting Claude Code's evolution from a personal productivity tool into a team-level AI engineering platform.

---

*Data as of: 2026-03-02 | Source: github.com/anthropics/skills*

---

# Claude Code Community Report | 2026-03-02

## Today at a Glance

Community activity is extremely high today, and **Cowork is the center of attention** — key problems such as the folder-picker restriction and VM startup failures keep escalating. Meanwhile, **the AskUserQuestion tool has hit a severe regression**, with multiple users reporting that the interactive UI fails to render and an empty answer comes back immediately. Community contributors are actively submitting plugin PRs, including practical features such as AGENTS.md support and code-verification enhancements.

---

## Community Hot Issues

| Rank | Issue | Significance | Community response |
|:---|:---|:---|:---|
| 1 | [#24964](https://github.com/anthropics/claude-code/issues/24964) **Cowork folder picker rejects paths outside the home directory** | 🔴 Severely limits workflows | 60 comments, 75 👍, cross-platform impact (Windows/macOS); symlinks/junctions are also blocked |
| 2 | [#26554](https://github.com/anthropics/claude-code/issues/26554) **Cowork RPC error: virtiofs/Plan9 mount failure** | 🔴 Blocks Cowork usage | 38 comments, 47 👍, a VM file-system-layer problem |
| 3 | [#18170](https://github.com/anthropics/claude-code/issues/18170) **Terminal copy-paste includes extra indentation and trailing spaces** | 🟡 High-frequency pain point | 36 comments, 65 👍, a long-standing UX problem |
| 4 | [#29530](https://github.com/anthropics/claude-code/issues/29530) **AskUserQuestion does not render the interactive UI and returns an empty response immediately** | 🔴 Tool completely broken | 9 comments, 9 👍, erupted today, breaks automation flows |
| 5 | [#27801](https://github.com/anthropics/claude-code/issues/27801) **Cowork workspace fails to start, VM service not running** | 🔴 Fully blocks the feature | 15 comments, 7 👍, persists after restart |
| 6 | [#13605](https://github.com/anthropics/claude-code/issues/13605) **Custom plugin subagents cannot access MCP tools** | 🟡 Plugin ecosystem limitation | 14 comments, 16 👍, built-in agents work but custom agents are restricted |
| 7 | [#13898](https://github.com/anthropics/claude-code/issues/13898) **Custom subagents cannot access project-level MCP servers** | 🟡 Related to #13605 | 9 comments, 7 👍, manifests as hallucination rather than a real call |
| 8 | [#29774](https://github.com/anthropics/claude-code/issues/29774) **AskUserQuestion auto-selects in custom commands** | 🔴 Same root cause as #29530 | 5 comments, 3 👍, new today, the skills system is affected |
| 9 | [#29733](https://github.com/anthropics/claude-code/issues/29733) **AskUserQuestion completes without any user input** | 🔴 Duplicate report of #29530 | 4 comments, 7 👍, confirms how widespread the problem is |
| 10 | [#5186](https://github.com/anthropics/claude-code/issues/5186) **Notification hook delayed by 10 seconds** | 🟡 Performance issue | 21 comments, 24 👍, Linux platform, memory-related |

> **Key insight**: The AskUserQuestion tool saw a **concentrated burst of failure reports** today, with 3 related issues updated at the same time, suggesting a regression introduced in a recent release. File-system/VM-layer stability for Cowork remains the biggest pain point.

---

## Notable PR Progress

| PR | Status | Feature/Fix |
|:---|:---|:---|
| [#29759](https://github.com/anthropics/claude-code/pull/29759) | 🟢 Open | **Fixes the RTL text rendering regression** (Arabic/Hebrew displayed incorrectly in the VSCode webview since v2.1.63); root cause is a global CSS `direction: ltr` override |
| [#29835](https://github.com/anthropics/claude-code/pull/29835) | 🟢 Open | **AGENTS.md plugin support** — automatically loads AGENTS.md when no CLAUDE.md exists, resolving the community's top-voted request |
| [#29755](https://github.com/anthropics/claude-code/pull/29755) | 🟢 Open | **verified-code-answers plugin** — distinguishes Claude's "verified assertions" from "unverified speculation", resolving the confidence-conflation problem in #29753 |
| [#29732](https://github.com/anthropics/claude-code/pull/29732) | 🟢 Open | **push-guardrails plugin** — prevents private code from being pushed to public repositories by accident, a direct response to the security incident in #29225 |
| [#29757](https://github.com/anthropics/claude-code/pull/29757) | 🟢 Open | **Docs fix**: use the lowercase-hyphenated naming convention consistently in the skill development guide (`skill-name` instead of `Skill Name`) |
| [#29731](https://github.com/anthropics/claude-code/pull/29731) | 🟢 Open | **Docs fix**: standardize skill-name example formatting and explain the constraints of the `name` field as a slash-command trigger |
| [#29833](https://github.com/anthropics/claude-code/pull/29833) | 🔴 Closed | AGENTS.md plugin (first version), superseded by #29835 |
| [#28062](https://github.com/anthropics/claude-code/pull/28062) | 🔴 Closed | Batch fixes for community PRs: hookify import paths, Python 3.8 compatibility, subagent MCP access, and more |
| [#28065](https://github.com/anthropics/claude-code/pull/28065) | 🔴 Closed | Batch merge of additional small fixes: Write/Edit field mapping, Python 3.8 typing, subagent tool injection |
| [#26442](https://github.com/anthropics/claude-code/pull/26442) [#26447](https://github.com/anthropics/claude-code/pull/26447) | 🔴 Closed | Sonnet 1M context window disappearing issue (duplicate closures) |

> **Contribution trend**: Community contributions today are **highly concentrated on the plugin ecosystem** — 4 new plugin PRs cover documentation conventions, code security, answer trustworthiness, and multi-format support, showing strong developer demand for extensibility.

---

## Feature Demand Trends

Based on an analysis of 50 active issues, community attention is distributed as follows:

```
┌─────────────────────────────────────────┐
│  🔥 Cowork VM/file-system stability     28%  │
│     (mount failures, path restrictions, VM startup) │
├─────────────────────────────────────────┤
│  🛠️ Tool-system reliability             22%  │
│     (AskUserQuestion failures, MCP access) │
├─────────────────────────────────────────┤
│  🔌 MCP/plugin ecosystem polish         18%  │
│     (subagent permissions, project-level config, tool injection) │
├─────────────────────────────────────────┤
│  🎨 IDE/editor integration experience   15%  │
│     (VSCode extension, remote control, copy-paste) │
├─────────────────────────────────────────┤
│  ⚡ Performance and reliability         12%  │
│     (latency, timeouts, history persistence) │
├─────────────────────────────────────────┤
│  🔐 Security and permission control      5%  │
│     (.claudeignore, repository visibility) │
└─────────────────────────────────────────┘
```

**Emerging trends**:
- **AGENTS.md standardization**: the community is proactively pushing for parity with CLAUDE.md
- **Answer trustworthiness markers**: developers need to distinguish "execution-verified" answers from "speculative" ones
- **Preventive security controls**: repository visibility checks before code pushes

---

## Developer Concerns

### 🔴 Blocking pain points

| Problem | Impact scope | Urgency |
|:---|:---|:---|
| **AskUserQuestion completely broken** | All skills/automation that depend on interactive confirmation | P0 |
| **Cowork path restriction** | Enterprise users with cross-drive/network storage | P0 |
| **Cowork VM startup failure** | VM-dependent workflows | P1 |

### 🟡 High-frequency friction points

1. **Inconsistent MCP tool access permissions**
   - Built-in agents ✓ vs custom subagents ✗
   - Global config ✓ vs project config ✗
   - *Developer expectation: a unified capability model*

2. **Copy-paste experience**
   - Terminal output carries indentation used for visual alignment
   - Needs a "plain-text copy" mode or automatic cleanup

3. **Ambiguous error messages**
   - "API Error: Rate limit" does not distinguish usage limits from throughput limits
   - Leaves paying users confused and debugging in circles

### 🟢 Positive signals

- **Surge in plugin development activity**: the community is shifting from "filing requests" to "implementing directly"
- **Standardizing documentation contributions**: infrastructure improvements such as naming conventions and validation checklists
- **Fast response to security incidents**: the push-guardrails plugin was proposed within 4 days of #29225

---

*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Report | 2026-03-02

---

## 1. Today at a Glance

Community focus today is split between two pain points — **abnormal usage billing** and **connection stability**: multiple Plus/Pro users report that Codex consumption rates suddenly jumped 2-4x, while WebSocket connections on Linux are frequently downgraded to HTTPS. The development team is pushing a steady stream of PRs around cross-platform voice support and authentication fixes.

---

## 2. Releases

**No new releases** (no Releases in the past 24 hours)

---

## 3. Community Hot Issues

| Priority | Issue | Core problem | Community response |
|:---|:---|:---|:---|
| 🔴 **P0** | [#13167](https://github.com/openai/codex/issues/13167) [#13186](https://github.com/openai/codex/issues/13186) | **Abnormal usage billing**: Plus/Pro users report very short tasks burning through large amounts of quota; widely discussed on Reddit | 4+ duplicate reports; users have started tracking their own token consumption |
| 🔴 **P0** | [#13041](https://github.com/openai/codex/issues/13041) | **WebSocket 1008 Policy close**: Linux users are disconnected by the server immediately after the connection upgrade, forcing an HTTPS downgrade | 40 comments, 62 👍, affects many distributions including Arch/Fedora |
| 🟡 **P1** | [#10450](https://github.com/openai/codex/issues/10450) | **Remote development support**: requests SSH/remote-host support, benchmarked against VS Code Remote | 217 👍, the top-voted feature request; a hard requirement for enterprise users |
| 🟡 **P1** | [#13179](https://github.com/openai/codex/issues/13179) | **Subagents consume message quota exponentially**: messages usage explodes when subagents are used | New report; official clarification of the billing logic is needed |
| 🟡 **P1** | [#12491](https://github.com/openai/codex/issues/12491) | **MCP zombie process leak**: Codex.app does not reclaim child processes after tasks complete; 1300+ zombies / 37GB memory leaked | Serious production issue; 4 comments awaiting follow-up |
| 🟡 **P1** | [#3141](https://github.com/openai/codex/issues/3141) | **Sandbox GPU access**: the Linux sandbox blocks NVIDIA GPUs, breaking ML workflows | 28 comments, long unresolved, 32 👍 |
| 🟢 **P2** | [#10760](https://github.com/openai/codex/issues/10760) | **macOS "Awaiting approval" hang**: the approval prompt cannot be interacted with; closed | 59 comments of heavy discussion, 67 👍, proposed fix pending verification |
| 🟢 **P2** | [#2952](https://github.com/openai/codex/issues/2952) | **@-search ignores .gitignore'd files**: the VS Code extension cannot search files ignored by Git | 23 comments, hurts monorepo scenarios |
| 🟢 **P2** | [#11325](https://github.com/openai/codex/issues/11325) | **App is missing the /compact command**: the CLI has manual compaction, the App has no equivalent | 21 comments; a must-have for context management |
| 🟢 **P2** | [#13148](https://github.com/openai/codex/issues/13148) | **Windows EOL corrupted**: Codex keeps replacing CRLF with LF despite explicit instructions | Only 4 comments but strongly worded: "SERIOUS PITA" |

---

## 4. Notable PR Progress

| Status | PR | Feature/Fix | Technical notes |
|:---|:---|:---|:---|
| 🆕 **OPEN** | [#13193](https://github.com/openai/codex/pull/13193) | **Persist voice device ID** | Persists the cpal device ID so the microphone/speaker no longer has to be re-selected after every restart |
| 🆕 **OPEN** | [#13192](https://github.com/openai/codex/pull/13192) | **Cross-platform TUI voice support** | Upgrades cpal to 0.17.3, aligning the Linux voice path with macOS/Windows |
| 🆕 **OPEN** | [#13191](https://github.com/openai/codex/pull/13191) | **Windows auth storage fix** | Stores the OAuth token in binary shards, working around Credential Manager size limits |
| 🆕 **OPEN** | [#13177](https://github.com/openai/codex/pull/13177) | **Hot turn-context refresh** | Reloads context between sampling requests so mid-turn nudges take effect in real time |
| 🆕 **OPEN** | [#13187](https://github.com/openai/codex/pull/13187) | **Plan mode instruction configuration** | Adds the `plan_mode_developer_instructions` config option |
| 🔄 **OPEN** | [#13096](https://github.com/openai/codex/pull/13096) | **Resumable rollout rebuild** | Restores historical state when rewinding, improving long-session stability |
| ✅ **CLOSED** | [#13181](https://github.com/openai/codex/pull/13181) | **Account status sync fix** | Adds plan types to `account/updated`, fixing wrong upgrade prompts for paying users |
| ✅ **CLOSED** | [#12989](https://github.com/openai/codex/pull/12989) | **macOS automation permission fix** | The sandbox extension now allows the `launchservicesd` mach lookup, fixing app launch |
| 🔄 **OPEN** | [#12951](https://github.com/openai/codex/pull/12951) | **OSC-52 clipboard support** | The `/copy` command supports clipboard integration for SSH remote sessions |
| 🔄 **OPEN** | [#13137](https://github.com/openai/codex/pull/13137) | **host_executable integration tests** | Fills in end-to-end test coverage for execpolicy and zsh-fork |

---

## 5. Feature Demand Trends

Based on an analysis of 50 active issues, community priorities:

```
1. Billing transparency and controllability ████████████████████  Usage anomalies, quota-consumption visibility, hard spending caps
2. Connection and transport stability ████████████████░░░░  WebSocket reliability, fallback strategy, reconnection mechanisms
3. Remote/cloud development support ██████████████░░░░░░  SSH, containers, CI/CD integration
4. Sandbox capability expansion ████████████░░░░░░░░  GPU, networking, license-check bypasses
5. Deep IDE integration ██████████░░░░░░░░░░  VS Code extension feature parity, JetBrains support
6. Context management optimization █████████░░░░░░░░░░░  Manual compact, session recovery, long-context strategies
7. Cross-platform consistency ████████░░░░░░░░░░░░  Windows-specific issues, Linux feature parity
```

---

## 6. Developer Concerns

| Pain point category | Specific manifestations | Frequency |
|:---|:---|:---|
| **"Black-box billing" anxiety** | Sudden usage spikes, opaque subagent billing logic, no real-time dashboard | 🔥🔥🔥🔥🔥 |
| **Linux as a second-class citizen** | WebSocket downgrades, missing voice features, GPU sandbox restrictions, auth problems | 🔥🔥🔥🔥🔥 |
| **Windows edge cases** | EOL handling, PowerShell defaults, file paths, update flow | 🔥🔥🔥🔥 |
| **MCP production readiness** | Zombie processes, config hot-reload, error isolation | 🔥🔥🔥🔥 |
| **Context running out of control** | Runaway generation, forgotten plans, no way to force compaction | 🔥🔥🔥 |
| **Enterprise compliance** | Audit logs, data residency, offline/on-premises deployment | 🔥🔥🔥 |

---

*This report is generated from public GitHub data and does not represent OpenAI's official position.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Report | 2026-03-02

## Today at a Glance

Community activity is extremely high today. **Remote Agents** infrastructure is the central focus, with the official team pushing hard on Sprint 1-3 planning and implementation. Meanwhile, **user experience optimization** continues in force, with multiple PRs making deep improvements to pain points such as terminal flicker, startup latency, and interaction details. Notably, community contributor `aishop-lab` submitted 5 high-quality PRs in a single day, focused on test coverage and edge-case fixes.

---

## Releases

No new releases.

---

## Community Hot Issues

| # | Issue | Significance | Community activity |
|---|-------|--------|---------|
| [#20142](https://github.com/google-gemini/gemini-cli/issues/20142) | AskUser open questions do not support Ctrl+R history search | ⭐⭐⭐⭐⭐ | **8 comments**, the most-discussed issue; a high-frequency developer pain point. Users answering complex open questions cannot quickly recall past input, severely hurting multi-turn conversation efficiency. |
| [#18896](https://github.com/google-gemini/gemini-cli/issues/18896) | Screen flicker/tearing when scrolling on Windows | ⭐⭐⭐⭐⭐ | **5 comments**; a long-standing terminal rendering issue affecting the baseline Windows experience, labeled P2 priority. |
| [#20302](https://github.com/google-gemini/gemini-cli/issues/20302) | [Epic] Remote Agents Sprint 1 - foundational architecture | ⭐⭐⭐⭐⭐ | **Core roadmap item**; led by Adam Weidman, it establishes streaming and core infrastructure for remote agents and is the cornerstone of future ecosystem expansion. |
| [#20181](https://github.com/google-gemini/gemini-cli/issues/20181) | AskUser support for answering open questions in an external editor | ⭐⭐⭐⭐⭐ | Same author as #20142, forming an **input-experience improvement pair**. Long-text input scenarios (e.g. Conductor track descriptions) urgently need editor support. |
| [#19514](https://github.com/google-gemini/gemini-cli/issues/19514) | AskUser tool outputs raw tags in Plan mode | ⭐⭐⭐⭐☆ | The model's `<question>` tags are not rendered, exposing a Plan mode UI adaptation flaw that affects professional workflows. |
| [#18953](https://github.com/google-gemini/gemini-cli/issues/18953) | Complex shell commands execute extremely slowly | ⭐⭐⭐⭐☆ | CLI tools with progress animations run up to 100x slower than native, pointing to terminal rendering bottlenecks that need architecture-level optimization. |
| [#20461](https://github.com/google-gemini/gemini-cli/issues/20461) | Support Plan annotation feedback iteration | ⭐⭐⭐⭐☆ | Works in tandem with #17721 editor integration, moving Plan mode from "one-shot approval" toward "collaborative iteration". |
| [#20550](https://github.com/google-gemini/gemini-cli/issues/20550) | JS heap memory exhaustion | ⭐⭐⭐⭐☆ | A production issue: after long runs, GC cannot reclaim memory; stability needs urgent attention. |
| [#19519](https://github.com/google-gemini/gemini-cli/issues/19519) | Long-running shell commands falsely trigger loop detection | ⭐⭐⭐⭐☆ | **2 👍**; a UX annoyance with frequent false positives in scenarios such as `grep` over large directories. |
| [#20795](https://github.com/google-gemini/gemini-cli/issues/20795) | Vim mode setting wrongly modifies user-level config | ⭐⭐⭐⭐☆ | **New today**; a settings scope isolation flaw where Workspace changes unexpectedly pollute User config, affecting multi-project developers. |

---

## Notable PR Progress

| # | PR | Type | Core improvement |
|---|-----|------|---------|
| [#18963](https://github.com/google-gemini/gemini-cli/pull/18963) | SettingsDialog.tsx refactor: remove React anti-patterns | 🔧 Architecture | Eliminates excessive state synchronization, improving type safety and maintainability; continues the technical-debt cleanup from #14915. |
| [#20643](https://github.com/google-gemini/gemini-cli/pull/20643) | Lazy loading to reduce startup latency | ⚡ Performance | **P1 priority**; a `--version` fast path + on-demand initialization, resolving the long-standing pain point #10726. |
| [#20673](https://github.com/google-gemini/gemini-cli/pull/20673) | Stable footer architecture and UX improvements | 🎨 UX | Definitively fixes footer flicker, restructuring the information hierarchy and security-status visibility. |
| [#20774](https://github.com/google-gemini/gemini-cli/pull/20774) | `/directory` renamed to `/workspace` | 🏗️ Terminology unification | **v2**; keeps alias compatibility and standardizes terminology end to end (CWD + trusted directories). |
| [#20745](https://github.com/google-gemini/gemini-cli/pull/20745) | Add `/colors` command and semantic focus colors | 🎨 Theming | A visual theme-debugging tool; standardizes focus/selection colors and improves accessibility. |
| [#20786](https://github.com/google-gemini/gemini-cli/pull/20786) | Compact mode for MCP tool output | 🎨 UX | Toggled globally with `Ctrl+O`; single-line summaries replace verbose output, reducing terminal clutter. |
| [#20793](https://github.com/google-gemini/gemini-cli/pull/20793) | Preserve trailing newlines to support heredocs | 🐛 Fix | Fixes `.trim()` breaking multi-line shell constructs; a critical edge-case fix. |
| [#20788](https://github.com/google-gemini/gemini-cli/pull/20788) | Pass proxy environment variables to sandboxed processes | 🐛 Fix | Resolves #19187, where `HTTP_PROXY` configuration has no effect in corporate network environments. |
| [#20794](https://github.com/google-gemini/gemini-cli/pull/20794) | errorClassification.ts test coverage | 🧪 Quality | Contributed by `aishop-lab`; 8 tests covering 4 core paths, improving error-handling reliability. |
| [#20717](https://github.com/google-gemini/gemini-cli/pull/20717) | `/mcp remove` interactive subcommand | ✨ Feature | Remove MCP servers directly within a session, rounding out MCP lifecycle management. |

---

## Feature Demand Trends

Based on an analysis of 50 active issues, community attention falls into three main threads:

| Trend | Heat | Representative issues | Notes |
|---------|------|-----------|------|
| **Agent ecosystem expansion** | 🔥🔥🔥🔥🔥 | #20302, #20303, #20304, #20195, #20233 | Remote/local subagents advance in parallel; sprint-based development; deep MCP protocol integration |
| **Plan mode professionalization** | 🔥🔥🔥🔥☆ | #20461, #20595, #20344, #19514 | Evolving from basic approval toward "collaborative planning"; needs annotation, iteration, and external editor support |
| **Terminal experience refinement** | 🔥🔥🔥🔥☆ | #20142, #20181, #18896, #20217, #20673 | Input efficiency (history search, external editors), rendering stability (flicker), performance (startup, memory) |

**Emerging signals**: Infrastructure capabilities are accumulating around OAuth/MCP authentication (#20121), token-efficient reading strategies (#19561 "Tactful Extraction"), and session recovery prompts (#19379).

---

## Developer Concerns

### 🔴 High-frequency pain points
1. **Input experience bottleneck** — AskUser history search, editor support, and long-text handling form a complete demand cluster (#20142 + #20181)
2. **Windows terminal rendering** — Flicker spans multiple scenarios (scrolling #18896, input path #20217), hurting adoption among professional users
3. **Performance and stability** — Startup latency (#20643 resolved), memory leaks (#20550), slow long-command execution (#18953)

### 🟡 Workflow improvement requests
- **Plan mode**: needs a more code-review-like collaborative experience rather than one-shot approval
- **Session management**: missing recovery guidance after unexpected exits (#19379)
- **Config isolation**: Workspace/User scope confusion (#20795)

### 🟢 Ecosystem expectations
- An open timeline and third-party integration documentation for remote agents
- Official operation and quality review mechanisms for the MCP marketplace

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Report | 2026-03-02

## Today at a Glance

Community activity is steady today, with no new releases. The core concerns center on two areas — **SSH remote environment compatibility** and **task execution workflow optimization** — while the improvement for file auto-completion has already entered PR review.

---

## Community Hot Issues

> 4 total; all included

| # | Title | Type | Key info | Link |
|:---|:---|:---|:---|:---|
| **#1293** | Cannot communicate over a remote SSH server | 🔴 Bug | The CLI is completely unusable on headless servers where DNS cannot be modified; a blocking issue for enterprise server scenarios | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1293) |
| **#1276** | `@` file auto-completion misses files | 🔴 Bug | Files deep in the directory tree are not offered for completion; directly tied to PR #1286 | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1276) |
| **#1292** | Task subtasks hang during execution | 🔴 Bug | Intermittent hangs in multi-subtask scenarios, destabilizing complex workflows | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1292) |
| **#1287** | Cannot prepare the next task prompt while a task is running | 🟡 Enhancement | The blocking interaction design limits batch-task efficiency; a workflow-continuity pain point | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1287) |

**Community reaction watch**: The SSH environment issue (#1293) and the Task hang (#1292) were both filed on March 1 and have yet to receive an official response, with users growing anxious; a community contributor has already submitted a fix for the file completion issue.

---

## Notable PR Progress

> 4 total; all included

| # | Title | Status | Feature/Fix | Link |
|:---|:---|:---|:---|:---|
| **#1286** | Scan shallow subdirectories first to optimize completion | 🟢 Open | Fix for #1276: adjusts directory scan priority to improve discovery of deeply nested files | [Link](https://github.com/MoonshotAI/kimi-cli/pull/1286) |
| **#1236** | Enable `trust_env` to support proxy environment variables | 🟢 Open | Lets `aiohttp.ClientSession` read system proxy configuration, fixing connectivity in corporate network environments | [Link](https://github.com/MoonshotAI/kimi-cli/pull/1236) |
| **#743** | Update `uv_build` version constraint | 🟢 Open | Build-system dependency maintenance, ensuring compatibility with newer uv toolchains | [Link](https://github.com/MoonshotAI/kimi-cli/pull/743) |
| **#173** | Bump version to 0.50 | 🔴 Closed | Closed as historical PR cleanup; no functional change | [Link](https://github.com/MoonshotAI/kimi-cli/pull/173) |

**Review activity**: #1286 and #1236 are both network/environment adaptation improvements with significant value for server deployment scenarios; worth watching their merge progress.

---

## Feature Demand Trends

Community focus areas distilled from recent issues:

| Priority | Direction | Specific manifestations |
|:---|:---|:---|
| **P0** | **Remote/headless environment adaptation** | A concentrated burst of connection and authentication problems on SSH servers, container environments, and headless scenarios |
| **P1** | **Task execution reliability** | Task subtask hangs, interruption recovery, multi-task queue management |
| **P1** | **Interaction efficiency optimization** | Asynchronous prompt preparation, more flexible interruption and resumption mechanisms |
| **P2** | **File indexing accuracy** | Completion accuracy on large codebases, ignore-rule tuning |

---

## Developer Concerns

### 🔴 High-frequency pain points

1. **Enterprise server deployment barriers**
   - Core conflict: the auth/connection mechanisms Kimi CLI depends on are incompatible with headless, network-restricted environments
   - Typical scenarios: SSH bastion hosts, CI/CD pipelines, containerized dev environments

2. **Complex task-flow stability**
   - Intermittent subtask hangs with no clear reproduction pattern, making debugging hard
   - Lacks observability into task execution state (logs, progress, timeout control)

### 🟡 Experience optimization requests

- **Workflow continuity**: the current single-threaded blocking interaction limits batch-processing efficiency
- **Environment awareness**: automatic adaptation to system-level configuration such as proxies, DNS, and certificates

---

*Data source: github.com/MoonshotAI/kimi-cli | Statistics window: 2026-03-01 to 2026-03-02*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Report | 2026-03-02

## Today at a Glance

Community focus today centers on two serious problems: **Copilot auth billing anomalies** (issue #8030 has drawn 134 comments) and **system crashes caused by memory leaks** (issue #13230). Meanwhile, developers are submitting a dense stream of PRs for new providers (Databricks, Blackbox AI, Jules) and core improvements such as runtime tool toggles, signaling that ecosystem expansion has entered an acceleration phase.

---

## Releases

**No new releases** (no Releases in the past 24 hours)

---

## Community Hot Issues

| # | Title | Status | Comments | Core problem and community response |
|---|------|------|------|------------------|
| [#8030](https://github.com/anomalyco/opencode/issues/8030) | Copilot auth error bills agent requests as user requests, rapidly draining premium quota | 🔴 OPEN | **134** | **Top-priority billing incident**. Users report 60 agent requests in a single session wrongly marked as user-initiated, draining quota instantly. 46 👍 show broad impact; the X-Initiator header logic needs an urgent fix. |
| [#13230](https://github.com/anomalyco/opencode/issues/13230) | Memory leak causes Linux kernel soft lockups, OOM kills, and total system collapse | 🔴 OPEN | 10 | **Critical-severity stability issue**. A single process ballooned to 116GB virtual memory / 21GB RSS, triggering simultaneous soft lockups on 7/8 CPUs for 356 seconds. Users say "the only recovery is a forced shutdown"; severely impacts production use. |
| [#7979](https://github.com/anomalyco/opencode/issues/7979) | Extremely slow startup on Windows | 🔴 OPEN | 10 | A high-frequency pain point with 33 👍. Every startup re-downloads the oh-my-opencode binary and updates plugins; no caching mechanism. |
| [#3523](https://github.com/anomalyco/opencode/issues/3523) | Overly long tool names cause silent crashes | 🔴 OPEN | 9 | When an MCP tool name exceeds 64 characters, the TUI exits without any error message and all subsequent requests fail — a terrible debugging experience. |
| [#13217](https://github.com/anomalyco/opencode/issues/13217) | Tasks stop after compaction | 🔴 OPEN | 7 | Triggered frequently in long-task scenarios; users must type "keep going" to resume. Forms a related issue cluster with #11301, reflecting session state-machine flaws. |
| [#12472](https://github.com/anomalyco/opencode/issues/12472) | Native Claude Code hooks compatibility (PreToolUse/PostToolUse/Stop) | 🔴 OPEN | 5 | 6 👍. An enterprise-migration pain point and a key gap in Claude Code ecosystem compatibility, blocking reuse of existing hooks assets. |
| [#8676](https://github.com/anomalyco/opencode/issues/8676) | Desktop plugin API 401 unauthorized | 🔴 OPEN | 5 | The Desktop's auto-generated UUID password is not passed correctly to the plugin client, blocking plugin ecosystem usage in Desktop scenarios. |
| [#7261](https://github.com/anomalyco/opencode/issues/7261) | v1.1.6 memory bloat unfixed + MCP orphan processes | 🔴 OPEN | 5 | Users still hit this after the official claim of a memory fix, and MCP processes are left behind; trust is eroding. |
| [#15585](https://github.com/anomalyco/opencode/issues/15585) | Free models show "free quota used up" | 🔴 OPEN | 4 | Users question the real billing policy behind free models; triggered after 6-hour long sessions — a policy transparency problem. |
| [#11301](https://github.com/anomalyco/opencode/issues/11301) | On Windows, post-compaction processing stops **every** time | 🔴 OPEN | 6 | Same root as #13217 but emphasized as "100% reproducible"; a Windows-platform-specific issue. |

---

## Notable PR Progress

| # | Title | Status | Type | Description |
|---|------|------|------|---------|
| [#15538](https://github.com/anomalyco/opencode/pull/15538) | Fix normalization of the OpenAI-compatible schema required field | 🟢 OPEN | Bug fix | Fixes gateways such as DeepSeek rejecting requests over an empty `required: []` array, improving stability on third-party compatible gateways. |
| [#7984](https://github.com/anomalyco/opencode/pull/7984) | Add Databricks provider support | 🟢 OPEN | Feature | Supports token-billed LLM endpoints on Databricks Workspaces, with SDK routing for Claude/LLaMA/Mistral and other models. |
| [#15630](https://github.com/anomalyco/opencode/pull/15630) | Prevent memory leaks when the SSE stream client disconnects | 🟢 OPEN | Bug fix | Fixes memory accumulation after multiple reconnects in long sessions; directly related to the #13230 memory crisis. |
| [#15631](https://github.com/anomalyco/opencode/pull/15631) | Add clickable URLs and file paths to TUI tool output | 🟢 OPEN | Feature | Based on the OSC8 hyperlink protocol, supports click-to-open in iTerm2/Ghostty/Kitty and other terminals, improving interaction efficiency. |
| [#15629](https://github.com/anomalyco/opencode/pull/15629) | Add Blackbox AI provider | 🟢 OPEN | Feature | Ships Blackbox AI (OpenAI-compatible) built in, with three model options offering 128K-200K context. |
| [#15625](https://github.com/anomalyco/opencode/pull/15625) | Add Jules (Google) stateless agent routing | 🟢 OPEN | Feature | Integrates Google's coding agent Jules REST API, supporting session/activity/source management; no streaming or chat completions. |
| [#8963](https://github.com/anomalyco/opencode/pull/8963) | Full portable mode and environment isolation support | 🟢 OPEN | Feature | Adds environment variables such as `OPENCODE_DATA_DIR/CACHE_DIR/LOG_DIR/STATE_DIR`, enabling fully configurable deployment for enterprise security compliance. |
| [#15624](https://github.com/anomalyco/opencode/pull/15624) | Runtime tool toggles across API/TUI/Web | 🟢 OPEN | Feature | Dynamically enable/disable tools; resolves #15623 and #13827, easing the context explosion caused by too many tools. |
| [#15619](https://github.com/anomalyco/opencode/pull/15619) | Fix cloudflare-ai-gateway metadata forwarding | 🟢 OPEN | Bug fix | Fills in `options.metadata` pass-through for `createAiGateway()`, fixing the broken configuration in #15621. |
| [#14877](https://github.com/anomalyco/opencode/pull/14877) | Fix authToken option being ignored in getSDK | 🟢 OPEN | Bug fix | Resolves the conflict between `authToken` and `apiKey` in provider configuration, ensuring custom auth takes correct precedence. |

---

## Feature Demand Trends

Based on an analysis of 50 active issues, community priorities:

| Trend | Heat indicators | Typical issues |
|---------|---------|-----------|
| **🔥 Billing and quota transparency** | #8030 (134 comments, 46👍) | Copilot billing errors, unclear free-model quota policy |
| **🔥 Stability and memory management** | #13230, #7261, #7979 | Memory leaks crashing systems, slow startup, orphan processes |
| **🚀 Multi-provider ecosystem expansion** | #7984, #15629, #15625, #10232 | New integrations such as Databricks/Blackbox/Jules/Routstr |
| **⚙️ Enterprise deployment capabilities** | #8963, #8676, #14544 | Portable mode, Desktop plugin auth, server-side config persistence |
| **🎛️ Tool and agent controllability** | #15624, #12472, #13217 | Runtime tool toggles, Claude hooks compatibility, compaction state recovery |
| **🖥️ TUI/IDE experience optimization** | #15631, #4464, #13682 | Clickable links, light mode, SSH remote auth copying |

---

## Developer Concerns

### 🔴 Blocking pain points
1. **Billing accuracy crisis**: the Copilot billing error in #8030 directly undermines commercial users' trust and needs an immediate fix
2. **Production stability**: memory leaks (#13230) and compaction interruptions (#13217/#11301) make OpenCode unfit for long-running tasks
3. **Windows experience gap**: slow startup (#7979), guaranteed compaction stops (#11301), and OAuth flashing errors (#15626) form a platform-specific issue cluster

### 🟡 High-frequency improvement requests
- **Tool ecosystem governance**: tool name length limits (#3523), runtime toggles (#15624), MCP process lifecycle management
- **Config portability**: full environment-variable coverage (#8963), across devices

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Report | 2026-03-02

## Today at a Glance

Today the community is focused on **Chinese-scenario stability fixes** and **authentication experience optimization**: multiple PRs urgently fix Skill invocation failures caused by model-emitted whitespace, plus file-read errors triggered by spaces between digits and Chinese characters — pain points for Chinese-language users. Meanwhile, the auth flow rework has entered intensive development, with a flattened three-option design clarifying the paid conversion path. The v0.11.0-nightly release keeps iterating, paving the way for the stable 0.11.1.

---

## Releases

### v0.11.0-nightly.20260301.14df5a57
- **Type**: Nightly preview
- **Changelog**: [compare v0.11.0](https://github.com/QwenLM/qwen-code/compare/v0.11.0...v0.11.0-nightly.20260301.14df5a57)

> This release is a preview ahead of the stable 0.11.1, carrying pre-release validation of several critical fixes.

---

## Community Hot Issues (10)

| # | Status | Title | Significance analysis | Link |
|---|------|------|-----------|------|
| **2032** | 🔴 OPEN | Model forcibly inserts spaces between digits and Chinese characters, causing file read failures | **A P0 blocking bug for Chinese scenarios**: affects reading files named with "digits + Chinese characters", disrupting workflows for many Chinese-language users; same class of model output formatting problem as #2025, needing a systemic fix | [Link](https://github.com/QwenLM/qwen-code/issues/2032) |
| **2025** | 🔴 OPEN | Invoking a Skill auto-inserts spaces, causing an infinite loop | **High-frequency Chinese-language Skill failure**: Skills named in Chinese (e.g. "comfyui工作流") get spurious spaces added, triggering a fail→retry→fail dead loop; PR #2027 already targets a fix | [Link](https://github.com/QwenLM/qwen-code/issues/2025) |
| **2034** | 🟡 OPEN | Customize/disable the "thinking" spinner quotes | **A high-vote experience-improvement request**: users call the TUI rotating quotes "dated and distracting", exposing a gap in terminal UI personalization | [Link](https://github.com/QwenLM/qwen-code/issues/2034) |
| **2016** | 🟡 OPEN | Refactor the /auth dialog: promote Coding Plan to a top-level option | **A critical commercialization path**: optimizes the free-to-paid conversion funnel and pairs with #1983; PR #2030 is implemented and awaiting merge | [Link](https://github.com/QwenLM/qwen-code/issues/2016) |
| **1983** | 🟡 OPEN | Guide users to upgrade to Coding Plan when free quota runs out | **A user-retention pain point**: the current error message is a "dead end" with no clear upgrade guidance; directly affects paid conversion for Alibaba Cloud Bailian Coding Plan | [Link](https://github.com/QwenLM/qwen-code/issues/1983) |
| **1708** | 🔴 OPEN | Cannot use hooks | **A long-standing configuration system flaw**: hooks configuration in settings.json is not recognized, breaking automation workflow integration; filed nearly a month ago with no response — needs maintainer attention | [Link](https://github.com/QwenLM/qwen-code/issues/1708) |
| **2033** | 🟢 CLOSED | Cannot edit files outside the workspace | **Security policy overreach**: users expect to edit external config files but are blocked by workspace restrictions; closed pending confirmation whether it is by design or needs documentation | [Link](https://github.com/QwenLM/qwen-code/issues/2033) |

> Note: 7 issues total today; the above are all noteworthy entries.

---

## Notable PR Progress (10)

| # | Status | Title | Feature/Fix details | Link |
|---|------|------|-------------|------|
| **2027** | 🟢 OPEN | fix(tools): trim whitespace from Skill names | **Urgent fix for #2025**: adds `trim()` handling in `validateToolParams`, resolving lookup failures caused by extra spaces the model adds to Chinese Skill names; prevents the infinite loop | [Link](https://github.com/QwenLM/qwen-code/pull/2027) |
| **2030** | 🟢 OPEN | [0.11.1] improve the auth dialog UX | **Commercialization experience upgrade**: replaces the nested second-level menu with three flat options (Qwen OAuth/API-KEY/Coding Plan), each showing key decision info such as "free/paid", "request limits", and "available models"; directly addresses #2016 | [Link](https://github.com/QwenLM/qwen-code/pull/2030) |
| **2031** | 🟢 OPEN | feat(security): introduce VibeGuard-style client-side redaction | **An enterprise security must-have**: before requests are sent to the model provider, secrets/PII are redacted into `__VG_<CATEGORY>_<hash>__` placeholders per configured rules and restored locally after the response; supports three matching types: keyword/regex/built-in rules | [Link](https://github.com/QwenLM/qwen-code/pull/2031) |
| **2029** | 🟢 OPEN | fix(tools): add bash/sh aliases for the shell tool | **Model compatibility fix**: resolves "Tool not found" errors caused by the model's habitual `bash`/`sh` aliases not matching the registered tool name `run_shell_command`; migrates legacy tool names in step | [Link](https://github.com/QwenLM/qwen-code/pull/2029) |
| **2021** | 🟢 OPEN | [0.11.1] detect and guard against truncated tool-call output | **Reliability hardening**: when LLM output hits `max_tokens`, tool-call JSON can be truncated; providers such as DashScope/Qwen misreport `finish_reason: "stop"`, silently writing incomplete code; adds truncation detection and guarding | [Link](https://github.com/QwenLM/qwen-code/pull/2021) |
| **1980** | 🟢 OPEN | feat: implement the Modes Layer for professional agent profiles | **An architecture-level feature**: adds the `@qwen-code/modes` package with 6 built-in modes — Architect/Code/Ask/Debug/Review/Orchestrator; supports `/mode` slash-command switching and custom modes in settings.json; separates tool routing from the prompt composer | [Link](https://github.com/QwenLM/qwen-code/pull/1980) |
| **1954** | 🟢 OPEN | Feat: VS Code secondary sidebar support | **Deep IDE integration**: supports placing the Qwen Code panel in the VS Code Secondary Sidebar, optimizing wide-screen workspace layouts; runs alongside the existing sidebar webview provider | [Link](https://github.com/QwenLM/qwen-code/pull/1954) |
| **2018** | 🟢 OPEN | [0.11.1] support AGENTS.md as a default context file | **Ecosystem standard compatibility**: adds automatic `AGENTS.md` recognition alongside `QWEN.md`, compatible with the [agents.md](https://agents.md/) standard with no manual configuration; lowers migration costs for multi-agent projects | [Link](https://github.com/QwenLM/qwen-code/pull/2018) |
| **2007** | 🟢 OPEN | fix: clean control characters from terminal output | **UI stability fix**: fixes misalignment in the Ink-based TUI caused by Windows-style line endings (`\r\n`) or lone `\r`; replaces `\r` with `\n` for cross-platform consistency | [Link](https://github.com/QwenLM/qwen-code/pull/2007) |
| **2005** | 🟢 OPEN | feat(i18n): strengthen output-language.md template constraints | **Multilingual consistency**: changes the soft "Prefer responding" prompt into the mandatory "You MUST always respond" rule, fixing LLMs mirroring the user's input language across turns and ignoring the setting | [Link](https://github.com/QwenLM/qwen-code/pull/2005) |

---

## Feature Demand Trends

Based on an analysis of today's issues and PRs, community focus falls into three main directions:

| Trend | Specific manifestations | Priority |
|---------|---------|--------|
| **Chinese-scenario stability** | Concentrated outbreak of digit-Chinese spacing, Skill-name spacing, and output-language consistency problems, reflecting systemic flaws in Chinese-corpus fine-tuning and post-processing logic | 🔴 Urgent |
| **Commercialization experience optimization** | The auth flow rework (#2016/#2030) and free-quota upgrade guidance (#1983) advance on parallel tracks; Coding Plan paid conversion has become the product's core KPI | 🟡 High priority |
| **Enterprise security compliance** | The introduction of VibeGuard-style redaction (#2031), plus DNS detection for container environments (#1817), signals rising demand from B2B deployment scenarios | 🟡 High priority |
| **Deep IDE ecosystem integration** | The VS Code secondary sidebar (#1954) and AGENTS.md standard compatibility (#2018) mark the leap from "usable" to "delightful" | 🟢 Ongoing |
| **Multi-mode agent architecture** | Modes Layer (#1980) introduces professional role separation; Architect/Orchestrator and other modes point toward evolution into complex project workflows | 🟢 Forward-looking |

---

## Developer Concerns

### 🔥

</details>

---
*This report is auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*