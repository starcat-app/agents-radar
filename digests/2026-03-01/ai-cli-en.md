# AI CLI Community Report 2026-03-01

> Generated at: 2026-03-01 00:08 UTC | Tools covered: 6

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Tools Ecosystem Comparison Report 2026-03-01

---

## 1. Ecosystem Overview

The current AI CLI tool ecosystem shows a **"six-way contest"** pattern: Claude Code holds the feature lead on the strength of Anthropic's models, but cost controversy is intensifying; OpenAI Codex pursues an extreme security sandbox with its Rust rewrite, yet is hampered by connection-layer stability; Google Gemini CLI is betting on a Remote Agents distributed architecture; in the domestic camp, Kimi, Qwen, and OpenCode are catching up fast, differentiating through IDE integration and localized model support. The overall trend is evolving from "single-tool intelligence" toward "multi-agent collaboration", with MCP/ACP protocols becoming the key interoperability layer, but the tools still show significant experience gaps in permission models, memory systems, and enterprise-grade security.

---

## 2. Activity Comparison by Tool

| Tool | Issues Today | PRs Today | Release | Community Heat Rating |
|:---|:---:|:---:|:---|:---:|
| **Claude Code** | 10 hot issues | 10 active PRs | v2.1.63 | 🔥🔥🔥🔥🔥 |
| **OpenAI Codex** | 10 hot issues | 10 active PRs | rust-v0.107.0-alpha.7/8 | 🔥🔥🔥🔥🔥 |
| **Gemini CLI** | 10 hot issues | 10 active PRs | v0.33.0-nightly | 🔥🔥🔥🔥 |
| **Kimi CLI** | 7 hot issues | 4 active PRs | None | 🔥🔥🔥 |
| **OpenCode** | 10 hot issues | 10 active PRs | None | 🔥🔥🔥🔥 |
| **Qwen Code** | 10 hot issues | 10 active PRs | **v0.11.0 stable release** | 🔥🔥🔥🔥🔥 |

> **Note**: Qwen Code added 30 issues + 27 PRs within 24 hours, making it the most active in practice; Claude Code and OpenAI Codex maintain steady high activity; Kimi CLI is relatively low-key but focused on key experience fixes.

---

## 3. Shared Functional Directions

| Functional Direction | Tools Involved | Specific Demands |
|:---|:---|:---|
| **Deep IDE integration** | Claude Code, OpenAI Codex, Gemini CLI, Kimi CLI, OpenCode, Qwen Code | **Consensus across all tools**. Remote Control/ACP protocol standardization (Claude #28471, Codex #12161, Qwen #1151/#1985/#2015), VS Code/Zed/JetBrains feature parity, consistent cross-platform Plan Mode |
| **Cost and rate control** | Claude Code, OpenAI Codex | **Claude #28537/#4464** report abnormally accelerating token consumption, with Max subscriptions still hitting hard limits; **Codex #12728** burned 22% of the weekly quota in a single day. Needs: real-time usage dashboards, budget alerts, model fallback strategies |
| **TUI stability and performance** | Claude Code, Gemini CLI, OpenCode | **Claude #22906** Windows keyboard failure, **Gemini #18896** scroll flickering, **OpenCode #6209** iTerm2 unable to scroll. Terminal rendering engines have become shared technical debt |
| **MCP/tool ecosystem governance** | Claude Code, OpenAI Codex, OpenCode, Qwen Code | **Claude #22264** cascading parallel tool failures, **OpenCode #7399** tool filtering, **Qwen #2012** bash invocation failures. Shifting from "tool quantity" to "invocation reliability" |
| **Enterprise security and compliance** | Claude Code, OpenAI Codex, OpenCode, Qwen Code | **OpenCode #14982/#15163** macOS permission-scanning boundaries, **Qwen #2010** sensitive-information redaction, **Codex #8361** Copilot identity integration. Data privacy and audit trails are becoming key procurement decision factors |
| **Windows platform experience** | Claude Code, OpenAI Codex, OpenCode | **Claude #22906** keyboard input failure, **Codex** voice 403/IDE extension blocking, **OpenCode #13282** Bun AVX crash. Windows remains stuck in a "second-class citizen" predicament |

---

## 4. Differentiated Positioning Analysis

| Tool | Core Functional Focus | Target User Profile | Technical Route Characteristics |
|:---|:---|:---|:---|
| **Claude Code** | End-to-end code generation, Cowork collaboration mode, Skills ecosystem | Advanced developers pursuing "full automation", Max subscribers | Node.js-dominant, deeply bound to Claude 3.7 Sonnet; aggressively pushing agent autonomy, but the cost model is under fire |
| **OpenAI Codex** | Secure sandbox execution, sub-agent parallelism, Rust performance | Enterprise security-sensitive teams, multi-language projects | Full-stack Rust rewrite with the execpolicy sandbox as the core differentiator; WebSocket transport layer under optimization, connection stability yet to be verified |
| **Gemini CLI** | Remote Agents distributed architecture, plan-mode workflows | Teams needing cross-device/cloud collaboration, Google ecosystem users | Node.js/npm distribution, betting on a three-Sprint "remote agent" strategy; sub-agents about to be enabled by default |
| **Kimi CLI** | Web UI experience, JetBrains ecosystem, file context passing | Heavy IDE users, Chinese developers | Relatively lightweight, focused on the ACP protocol and deep JetBrains integration; interaction-detail polish (todo visualization, multi-tab) |
| **OpenCode** | Multi-provider model support, native VS Code integration, memory efficiency | Model "nomad" users, multi-account enterprise scenarios | Bun runtime chasing top speed, but compatibility costs are showing (Windows AVX crash); actively onboarding domestic models such as Alibaba Cloud Bailian |
| **Qwen Code** | Multi-agent arena, AGENTS.md standard, Hooks extensions | Open-source contributors, advanced users comparing models for selection | The most aggressive community-driven innovation (Modes Layer, agent arena, Hooks system); IDE integration catching up |

---

## 5. Community Heat and Maturity

### 🔥 High activity + rapid iteration
| Tool | Key Signals | Maturity Assessment |
|:---|:---|:---|
| **Qwen Code** | 30 issues/27 PRs within 24h, v0.11.0 released, dense delivery of innovative features such as Modes/arena/Hooks | **Feature-rich but stability unproven**, suited to technology leaders willing to experiment |
| **Claude Code** | The cost-controversy issue has the highest heat (#28537, 29💬), but the release cadence is steady (v2.1.63) and the Skills ecosystem is mature | **The most mature features, the most controversial cost model**, suited to well-funded professional developers |
| **OpenAI Codex** | Two alpha releases on the same day, fast Rust rewrite progress, but 401/WebSocket issues block production use | **The most advanced architecture, the least stable availability**, suited to early adopters with extremely high security requirements |

### 🌱 Medium activity + targeted breakthroughs
| Tool | Key Signals | Maturity Assessment |
|:---|:---|:---|
| **Gemini CLI** | Three Remote Agents sprints in parallel, but community issue response speed is mediocre | **Clear strategic direction, execution details yet to be seen**, suited to Google Cloud ecosystem users positioning early |
| **OpenCode** | The critical memory-leak issue (#13230) has a key fix PR, and Alibaba Cloud Bailian support has landed | **Enterprise features catching up, technical debt needing cleanup**, suited to users with hard requirements for domestic models |

### 🎯 Low activity + precise positioning
| Tool | Key Signals | Maturity Assessment |
|:---|:---|:---|
| **Kimi CLI** | The fewest issues but focused on IDE integration pain points, dense Web UI experience optimization | **Scenario-focused, thin ecosystem**, suited to heavy JetBrains users as a backup tool |

---

## 6. Trend Signals Worth Watching

### 🚨 Industry-level pain point: the cost transparency crisis
- **Signal**: Claude Code #28537, #4464, and OpenAI Codex #12728 jointly expose "black-box billing" anxiety
- **Reference value**: Enterprise procurement decisions will shift from "feature comparison" to "TCO predictability"; real-time usage dashboards, hard budget caps, and automatic model fallback will become standard requirements

### 🔧 Protocol-layer divergence: the first signs of MCP vs ACP camps
- **Signal**: OpenCode/Qwen bet on ACP (Agent Client Protocol), Claude Code pushes Remote Control, Codex/Gemini stay relatively closed
- **Reference value**: Developers should prefer tools supporting open protocols to avoid ecosystem lock-in; toolchain builders should watch for protocol adaptation-layer opportunities

### 🏗️ Architectural paradigm shift: from "single agent" to "multi-agent collaboration"
- **Signal**: Gemini Remote Agents, Qwen arena mode, Codex sub-agent parallel optimization
- **Reference value**: The ability to decompose complex tasks and merge results will become the core competitiveness of next-generation tools; "orchestration layer" design capability matters more than single-model capability

### 🌍 Geopolitical mapping: the domestic model ecosystem is closing the loop faster
- **Signal**: OpenCode integrates Alibaba Cloud Bailian (Qwen/Kimi/GLM/MiniMax), Qwen Code natively supports multiple domestic models, Kimi focuses on Chinese scenarios
- **Reference value**: Domestic developers get an "out-of-the-box" localized experience, but should mind the compliance and availability risks of international tools (Claude/Codex)

### ⚠️ Technical debt becoming visible: TUI engines and cross-platform runtimes
- **Signal**: Windows experience problems are erupting across all tools, and each of the Bun/Node/Rust runtimes pays its own compatibility cost
- **Reference value**: When evaluating tools, fold "target platform test coverage" into selection criteria instead of looking only at feature checklists

---

*This report is generated from each tool's public GitHub data as of 2026-03-01; technology decision-makers are advised to weigh their team's platform preferences, budget models, and security and compliance requirements holistically.*

---

## Detailed Reports by Tool

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Community Highlights

> Data source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (2026-03-01)

---

## 1. Popular Skills Ranking (by attention)

| Rank | Skill | Overview | Status | Link |
|:---|:---|:---|:---|:---|
| 1 | **skill-quality-analyzer / skill-security-analyzer** | Meta-skill: five-dimension quality assessment (structure/docs/tests/security/performance) + security vulnerability scanning | 🟡 Open | [#83](https://github.com/anthropics/skills/pull/83) |
| 2 | **Improved frontend-design** | Improves the executability of the frontend-design skill, ensuring instructions can be completed within a single conversation turn | 🟡 Open | [#210](https://github.com/anthropics/skills/pull/210) |
| 3 | **codebase-inventory-audit** | A 10-step workflow for cleaning up a codebase: identify orphaned code, unused files, and documentation gaps | 🟡 Open | [#147](https://github.com/anthropics/skills/pull/147) |
| 4 | **masonry-generate-image-and-videos** | Masonry CLI integration: Imagen 3.0 image generation + Veo 3.1 video generation | 🟡 Open | [#335](https://github.com/anthropics/skills/pull/335) |
| 5 | **SAP-RPT-1-OSS predictor** | Integration of SAP's open-source tabular foundation model for enterprise data predictive analytics | 🟡 Open | [#181](https://github.com/anthropics/skills/pull/181) |
| 6 | **AURELION skill suite** | Four-layer cognitive framework: structured thinking templates, advisor mode, agent orchestration, persistent memory | 🟡 Open | [#444](https://github.com/anthropics/skills/pull/444) |
| 7 | **Buildr** | Telegram bridge: mirror messages on mobile, forwarding permissions, remote-control coding sessions | 🟡 Open | [#419](https://github.com/anthropics/skills/pull/419) |
| 8 | **ShieldCortex** | Persistent memory system + built-in security layer, supporting agent state encryption and auditing | 🟡 Open | [#386](https://github.com/anthropics/skills/pull/386) |

---

## 2. Community Demand Trends (distilled from issues)

| Direction | Representative Issue | Core Demands |
|:---|:---|:---|
| **Agent governance and security** | [#412](https://github.com/anthropics/skills/issues/412) | A governance model covering policy enforcement, threat detection, trust scoring, and audit trails |
| **MCP protocol integration** | [#16](https://github.com/anthropics/skills/issues/16), [#369](https://github.com/anthropics/skills/issues/369) | Expose Skills as MCP endpoints and standardize AI software APIs |
| **Skill package manager** | [#185](https://github.com/anthropics/skills/issues/185) | npm/cargo-style dependency management with cross-agent sharing |
| **AWS Bedrock compatibility** | [#29](https://github.com/anthropics/skills/issues/29) | Platform compatibility for enterprise deployment scenarios |
| **Skill creation toolchain** | [#202](https://github.com/anthropics/skills/issues/202) | Optimize `skill-creator` for token efficiency and execution orientation |
| **More permissive licensing** | [#100](https://github.com/anthropics/skills/issues/100) | Example code should adopt more open licenses (currently the highest at 11 👍) |

---

## 3. High-Potential Skills Awaiting Merge

| Skill | Key Value | Blocking Risk | Link |
|:---|:---|:---|:---|
| **skill-quality-analyzer** | The first official meta-skill, filling the gap in skill quality assessment | Needs Anthropic review of the security scanner's permissions | [#83](https://github.com/anthropics/skills/pull/83) |
| **frontend-design improvements** | Directly answers the design pain points mentioned in the official blog | Under iteration (updated February 27) | [#210](https://github.com/anthropics/skills/pull/210) |
| **AURELION suite** | Systematically addresses agent memory and cognitive architecture | Bundles 4 skills, a heavy review load | [#444](https://github.com/anthropics/skills/pull/444) |
| **user-preferences configuration** | Multilingual/personalized skill templates (including a Dutch example) | Niche need, priority to be confirmed | [#246](https://github.com/anthropics/skills/pull/246) |

---

## 4. Skills Ecosystem Insights

> **Core demand: evolving from a "tool library" into a "governable agent operating system"** — the community is pushing Skills beyond single-task automation toward enterprise-grade agent infrastructure with persistent memory, security auditing, MCP standardization, and cross-platform deployment.

---

*Data as of: 2026-03-01 | Source: anthropics/skills GitHub repository*

---

# Claude Code Community Report | 2026-03-01

## Today's Overview

Community activity was extremely high today. The v2.1.63 release brought the two practical commands `/simplify` and `/batch`, but **cost and API limit issues** took center stage — multiple high-heat issues reported abnormally accelerating token consumption and overly aggressive rate limits. Meanwhile, Windows platform stability and IDE integration (especially the Remote Control feature) remain developer pain points.

---

## Releases

### v2.1.63 Released
| Item | Details |
|:---|:---|
| **New features** | The two built-in slash commands `/simplify` and `/batch` |
| **Experience improvements** | Output from local slash commands (such as `/cost`) now correctly displays as system messages rather than user messages |
| **Workflow improvements** | Project configuration and automatic memory can now be shared across git worktrees of the same repository |
| **Partial features** | Updates related to the `ENABLE_CLAUDE` environment variable (docs truncated, full description pending) |

🔗 [Release page](https://github.com/anthropics/claude-code/releases/tag/v2.1.63)

---

## Hot Community Issues (Top 10)

| # | Title | Status | Heat | Key Takeaways |
|---|:---|:---|:---:|:---|
| [#28537](https://github.com/anthropics/claude-code/issues/28537) | Rate limits more aggressive than expected | 🔴 OPEN | 29💬 11👍 | **The hottest cost issue**. Users report being throttled far before reaching the documented caps, disrupting normal use for Max subscribers. Reproduced across platforms; official clarification of the throttling policy is needed. |
| [#22543](https://github.com/anthropics/claude-code/issues/22543) | Cowork feature generates 10GB VM packages and severely degrades performance | 🔴 OPEN | 22💬 41👍 | **High-priority oncall issue**. On macOS, VM packages created by the cowork feature balloon out of control, causing slow startup and UI stuttering. Strong community feedback; resource management urgently needs optimization. |
| [#4464](https://github.com/anthropics/claude-code/issues/4464) | "System reminder" content injection consumes excessive context tokens | 🔴 OPEN | 22💬 9👍 | **A long-standing cost pain point**. The mechanism that automatically injects large file contents into context burns through sessions quickly and sends bills soaring. Users want finer-grained control. |
| [#22906](https://github.com/anthropics/claude-code/issues/22906) | Windows v2.1.30+ keyboard input failure | 🔴 OPEN | 20💬 6👍 | **Critical Windows platform bug**. The TUI cannot receive keyboard input at all, severely affecting Windows developers; this regression needs priority fixing. |
| [#10065](https://github.com/anthropics/claude-code/issues/10065) | Long multi-step tasks dropped/rolled back without cause | 🔴 OPEN | 16💬 7👍 | **Reliability issue**. Claude Desktop abruptly abandons progress during long task execution without warning, causing workflow disruption and data-loss risk. |
| [#22264](https://github.com/anthropics/claude-code/issues/22264) | Cascading failures in parallel tool calls | 🔴 OPEN | 14💬 30👍 | **Architecture design issue**. One failed tool call forcibly cancels the other calls in the same batch, requiring a full retry and badly hurting efficiency. The community is calling for an independent-failure mode. |
| [#23601](https://github.com/anthropics/claude-code/issues/23601) | Infinite hang when launching in non-git directories (2.1.31 regression) | 🔴 OPEN | 11💬 2👍 | **Regression bug**. Introduced after 2.1.29; Linux users cannot launch at all in non-git directories, blocking basic usage scenarios. |
| [#23462](https://github.com/anthropics/claude-code/issues/23462) | Skill frontmatter support for model selection | 🔴 OPEN | 4💬 4👍 | **Feature request**. Let skills declare fields such as `model: haiku` to switch models automatically — significant for cost reduction on lightweight tasks; related to #21679 where docs don't match reality. |
| [#28471](https://github.com/anthropics/claude-code/issues/28471) | Pro accounts cannot use the remote-control command | 🔴 OPEN | 9💬 1👍 | **Feature permission confusion**. The docs don't spell out remote-control's subscription-tier requirements; Pro users hit an unusable feature, fragmenting the experience. |
| [#29695](https://github.com/anthropics/claude-code/issues/29695) | TUI screen width grows without bound and crashes | 🔴 OPEN | 3💬 0👍 | **Newly reported severe bug**. In v2.1.63 under the Ghostty terminal, screen width spirals upward to a 100% write ratio, completely blocking usage; an urgent fix is needed. |

---

## Notable PR Progress (Top 10)

| # | Title | Status | Core Contribution |
|---|:---|:---|:---|
| [#29656](https://github.com/anthropics/claude-code/pull/29656) | Fix GitHub Actions shell injection vulnerability | 🟡 OPEN | **Security hardening**. Moves GitHub context variables into the `env:` section to prevent `workflow_dispatch` input injection, fixing the high-severity issue detected by Semgrep. |
| [#29522](https://github.com/anthropics/claude-code/pull/29522) | Fix three major hookify plugin bugs | 🟡 OPEN | **Key fix for the plugin ecosystem**. Resolves the Python import path error, the rule discovery path error, and the Write/Edit field mapping issues, making the plugin genuinely usable. |
| [#29470](https://github.com/anthropics/claude-code/pull/29470) | Add stash plugin: multi-slot message storage | 🟡 OPEN | **Productivity tool**. Provides git-stash-style multi-slot message storage (push/pop/apply/list), addresses the single-slot limit of built-in Ctrl+S, and supports persistence to disk. |
| [#29462](https://github.com/anthropics/claude-code/pull/29462) | Remove the oncall triage workflow and commands | 🔴 CLOSED | **Process streamlining**. Removes the previously implemented automated oncall issue triage system, likely due to noise issues or a policy change. |
| [#29461](https://github.com/anthropics/claude-code/pull/29461) | Restrict duplicate candidates to canonical open issues | 🟡 OPEN | **Community governance**. Improves the duplicate-detection bot so it stops pointing at closed issues or forming circular duplicate networks, raising triage quality. |
| [#29460](https://github.com/anthropics/claude-code/pull/29460) | Improve recency and participation criteria for oncall triage | 🟡 OPEN | **Process optimization**. Fixes the `gh issue list` sorting assumptions so high-participation issues are not missed. |
| [#29459](https://github.com/anthropics/claude-code/pull/29459) | Fix commit-commands tool permission mismatch | 🟡 OPEN | **Plugin fix**. The `/commit` command failed by running unauthorized git commands through dynamic context injection; this completes the `allowed-tools` declaration. |
| [#29457](https://github.com/anthropics/claude-code/pull/29457) | Harden duplicate auto-close safety checks | 🟡 OPEN | **Mistake prevention**. Prevents marking an issue as a duplicate of a closed issue, and avoids two issues pointing at each other and both getting closed. |
| [#29668](https://github.com/anthropics/claude-code/pull/29668) | Fix unbound array crash in ralph-wiggum | 🟡 OPEN | **Stability fix**. `setup-ralph-loop.sh` crashed on empty arrays under `set -u`; fixed with safe expansion syntax. |
| [#28065](https://github.com/anthropics/claude-code/pull/28065) | Batch-fix several small open PRs | 🟡 OPEN | **Maintenance merge**. Consolidates fixes such as hookify field mapping, Python 3.8 type compatibility, and TUI width calculation, reducing merge costs. |

---

## Feature Demand Trends

Based on an analysis of 50 active issues today, community attention centers on the following directions:

| Rank | Direction | Representative Issues | Demand Intensity |
|:---:|:---|:---|:---:|
| 1 | **Cost optimization and transparency** | #28537, #4464, #28899, #29518, #29704 | 🔥🔥🔥🔥🔥 |
| 2 | **Windows platform stability** | #22906, #10065, #23095, #29705, #29702 | 🔥🔥🔥🔥🔥 |
| 3 | **Deep IDE integration** | #28951, #28471, #29682, #29687 (Remote Control/VS Code/JetBrains) | 🔥🔥🔥🔥 |
| 4 | **Performance and resource management** | #22543, #22264, #23601 (Cowork/parallel calls/startup performance) | 🔥🔥🔥🔥 |
| 5 | **Flexible model dispatching** | #23462, #21679 (skill-level model selection) | 🔥🔥🔥 |
| 6 | **Session and state management** | #15631, #21731, #29470 (history isolation/multi-terminal/message storage) | 🔥🔥🔥 |

---

## Developer Focus Points

### 🔴 High-frequency pain points

1. **Anxiety over runaway API costs**
   - Multiple issues report abnormally accelerating token consumption; prompt caching appears to have stopped working
   - The rate-limit policy is opaque; Max subscribers still hit "hard limits"
   - Needs: **real-time usage dashboards, finer-grained budget control, cost anomaly alerts**

2. **Windows second-class citizen experience**
   - Keyboard input, multi-drive configuration, temp file leaks, and other problems are erupting together
   - The native binary and the Node version behave inconsistently
   - Needs: **dedicated Windows test coverage, native installer optimization**

3. **Remote Control feature confusion**
   - Unclear subscription-tier requirements (Pro vs Max), no VS Code support, crashes after connecting
   - Needs: **a unified feature matrix document, IDE plugin feature parity**

### 🟡 Emerging needs

- **Skill ecosystem maturation**: model selection, permission control, debugging tools
- **MCP toolchain stability**: Chrome extension disconnects, tool registration persistence
- **Non-git workflow support**: plain-directory startup, projects outside monorepos

---

*This report is generated from public GitHub data and does not represent Anthropic's official position.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Report | 2026-03-01

---

## Today's Overview

Today the community zeroed in on **WebSocket connection stability** and **authorization issues**, with multiple high-frequency issues involving 401 Unauthorized errors and WebSocket 1008 policy closures. Meanwhile, the team has been busily fixing the memory system, sandbox permissions, and sub-agent startup performance, and shipped two Rust-side alpha versions.

---

## Releases

| Version | Notes |
|:---|:---|
| **rust-v0.107.0-alpha.8** | The latest Rust-side alpha, still iterating |
| **rust-v0.107.0-alpha.7** | The previous alpha released the same day |

> Note: the release cadence is tight right now; production users should watch for stable updates.

---

## Hot Community Issues (Top 10)

| # | Title | Status | Comments | Key Takeaways |
|:---|:---|:---|:---|:---|
| [#12764](https://github.com/openai/codex/issues/12764) | CLI 401 Unauthorized error | 🔴 OPEN | 27 | **Highest heat**. Codex CLI keeps returning 401 Unauthorized, breaking chatgpt.com backend calls; users report "stream disconnected before completion". Suspected auth token refresh or regional CDN issue (cf-ray: SIN node). |
| [#13041](https://github.com/openai/codex/issues/13041) | WebSocket closed by the server with policy 1008 after a successful upgrade | 🔴 OPEN | 23 | **Key infrastructure issue**. WebSocket connections fall into an "upgrade-close-fall back to HTTPS" loop; reported on Arch Linux, with 12 👍. Hurts the real-time response experience; a server-side policy adjustment is needed. |
| [#1980](https://github.com/openai/codex/issues/1980) | Follow the XDG spec on Linux | 🔴 OPEN | 16 | **A long-standing community demand** (created 2025-08). Asks to migrate `~/.codex` to standard XDG paths (`~/.config/codex`, `~/.local/share/codex`); 65 👍, a key cross-platform compatibility topic. |
| [#13106](https://github.com/openai/codex/issues/13106) | App v26.227.1448 streaming UI shows no updates while focused | 🟢 CLOSED | 15 | **Quickly fixed**. While focused, the macOS app does not render streaming responses and only shows them after losing focus; reported by a Pro user, 18 👍. Shows the team reacts fast to app experience issues. |
| [#12241](https://github.com/openai/codex/issues/12241) | Patch application keeps failing | 🔴 OPEN | 11 | A core tool-call pain point. Codex repeatedly hits "Failed to apply patch", hurting code-editing reliability; reported on Linux and present across versions. |
| [#12161](https://github.com/openai/codex/issues/12161) | IDE extension stuck on "Thinking" | 🔴 OPEN | 11 | VS Code/Cursor/Windsurf extensions hang on Windows, affecting ChatGPT Business subscribers; IDE integration stability needs improvement. |
| [#13103](https://github.com/openai/codex/issues/13103) | Cannot disable WebSocket transport | 🔴 OPEN | 11 | The `supports_websockets = false` setting has no effect, and `model_providers.openai` cannot be overridden. Users urgently need an escape hatch to downgrade to HTTPS. |
| [#12728](https://github.com/openai/codex/issues/12728) | Rate-limit consumption abnormally accelerated | 🔴 OPEN | 10 | Users report burning 22% of the weekly quota in a single day with unchanged usage patterns. Might involve background retries, sub-agent billing policy changes, or adjusted model token accounting. |
| [#8361](https://github.com/openai/codex/issues/8361) | Support GitHub Copilot subscription sign-in | 🟢 CLOSED | 10 | **A key enterprise need**. Lets enterprise users access Codex CLI with their existing Copilot subscriptions; 16 👍, part of the identity-system consolidation trend. |
| [#10741](https://github.com/openai/codex/issues/10741) | Xcode MCP integration issues | 🔴 OPEN | 10 | Core to macOS developer workflows. Xcode MCP tool calls misbehave; 31 👍, strong demand for deep Apple ecosystem integration. |

---

## Notable PR Progress (Top 10)

| # | Title | Status | Feature/Fix Highlights |
|:---|:---|:---|:---|
| [#13122](https://github.com/openai/codex/pull/13122) | Restrict memory stage-1 ingestion to exec sources | 🟢 CLOSED | Memory system refinement: configurable `stage_1_sources`, supporting exec-only workflows and preventing CLI/VSCode memories from polluting the execution context |
| [#13130](https://github.com/openai/codex/pull/13130) | Fix `/status` in sub-agent scenarios | 🔴 OPEN | Fixes abnormal status display in sub-agent scenarios; related to #13066 |
| [#13134](https://github.com/openai/codex/pull/13134) | Improve the tool-call approval footer UI | 🔴 OPEN | TUI experience improvement: clarifies MCP tool-call approval indicators, improves input layout and word wrapping |
| [#13100](https://github.com/openai/codex/pull/13100) | Fix browser MCP transport failure recovery | 🟢 CLOSED | **Key reliability fix**. Automatically recovers after macOS browser MCP transport interruptions (Broken pipe/Transport closed); resolves #13138 |
| [#13137](https://github.com/openai/codex/pull/13137) | Add host_executable integration coverage | 🔴 OPEN | Sandbox security hardening: ensures `host_executable()` takes effect end to end in execpolicy preflight and zsh-fork |
| [#13053](https://github.com/openai/codex/pull/13053) | Merge skill permissions with the current sandbox | 🔴 OPEN | **Permission model correction**. Skill scripts now layer permissions instead of replacing them, ending the counterintuitive behavior where "adding a skill reduces capabilities" |
| [#13136](https://github.com/openai/codex/pull/13136) | Limit ChatGPT user ID metrics to the App | 🔴 OPEN | Privacy compliance: user ID metrics become opt-in and App-environment only, with no change to the OSS CLI; finer-grained OTLP metadata |
| [#12989](https://github.com/openai/codex/pull/12989) | Fix macOS automation permission BundleIDs | 🔴 OPEN | Sandbox extension: allows talking to `launchservicesd` to launch target apps, fixing a spec-document omission |
| [#13065](https://github.com/openai/codex/pull/13065) | Resolve host_executable rules in the preflight phase | 🟢 CLOSED | Security policy loop closed: `host_executable()` rule resolution now happens in `core/src/exec_policy` preflight |
| [#12935](https://github.com/openai/codex/pull/12935) | Speed up sub-agent startup | 🟢 CLOSED | **Performance optimization**. Skips the online model refresh for sub-agents and avoids a rollout flush at startup, significantly cutting sub-agent cold-start latency |

---

## Feature Demand Trends

Based on an analysis of 50 active issues, community attention centers on five directions:

| Direction | Representative Issues | Heat Indicators |
|:---|:---|:---|
| **🔐 Authentication and authorization** | #12764, #8361, #10989 | 401 errors, Copilot integration, Safari HTTPS interception |
| **🌐 Transport layer stability** | #13041, #13103, #12804 | WebSocket 1008 policy, forced HTTPS fallback, voice 403 |
| **🖥️ Deep IDE integration** | #12161, #10741, #13071, #10099 | VS Code/Cursor/Xcode/PyCharm, frequent permission prompts |
| **⚡ Performance and resource efficiency** | #12728, #12935, #9211 | Rate-limit anomalies, slow sub-agent startup, remote compression timeouts |
| **🛡️ Sandbox and permission model** | #13053, #12888, #10187 | Skill permission merging, in-sandbox edit failures, repeated Windows authorization |

**Emerging trend**: MCP (Model Context Protocol) ecosystem expansion (#2680 environment variables, #10741 Xcode MCP) is becoming a key demand for connecting external tools.

---

## Developer Focus Points

### 🔴 High-frequency pain points
1. **Connection-layer fragility**: the WebSocket/HTTPS downgrade logic is opaque, and 401/403/1008 errors lack diagnostic information
2. **Windows experience gap**: voice transcription 403, IDE extension permission prompt loops, and TUI rendering problems erupting together
3. **Patch reliability**: "Failed to apply patch" persists across versions, hurting the core editing workflow

### 🟡 Capability boundary demands
- **Model visibility**: unclear usage rights for Spark models (#12992, #13126)
- **Memory system controllability**: filtering polluted memories (#13008), XDG spec compliance (#1980)
- **Enterprise identity**: Copilot/SSO integration, team subscription management

### 🟢 Positive signals
- The team responds quickly to App UI regressions (#13106 closed the same day)
- Sub-agent performance optimization landed (#12935)
- The sandbox permission model is being corrected toward "layering instead of replacing" (#13053)

---

> 📌 **Worth watching**: follow-ups on #12764 (root cause of the 401 errors), #13041 (WebSocket policy), and #13053 (permission model change), which respectively affect the core availability, performance, and security experience.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Report | 2026-03-01

---

## 1. Today's Overview

Today the community focused on **agent architecture upgrades** and **core experience optimization**: the three big Remote Agents sprints are advancing in sync, and sub-agent functionality is about to be enabled by default; meanwhile, the team has been busily fixing long-standing pain points such as TUI flickering and loop-detection false positives. The v0.33.0-nightly version is out, including documentation updates for plan-file editing and test stability improvements.

---

## 2. Releases

### v0.33.0-nightly.20260228.1ca5c05d0
| Item | Details |
|:---|:---|
| **Release date** | 2026-02-28 |
| **Updates** | • Docs: updated the note that plan files can be edited during the approval stage ([#20452](https://github.com/google-gemini/gemini-cli/pull/20452))<br>• Tests: fixed a flaky ToolResultDisplay overflow test ([#jwhelangoog](https://github.com/google-gemini/gemini-cli)) |
| **How to get it** | `npm install -g @google/gemini-cli@nightly` |

---

## 3. Hot Community Issues

| # | Title | Status | Key Info | Community Reaction |
|:---|:---|:---|:---|:---|
| [#20142](https://github.com/google-gemini/gemini-cli/issues/20142) | AskUser open questions should support Ctrl+R history search | 🔴 Open | 8 comments, high-frequency demand | Users strongly want the interaction aligned with regular terminals to cut repeated typing |
| [#18896](https://github.com/google-gemini/gemini-cli/issues/18896) | Windows screen flickering/tearing while scrolling | 🔴 Open | P2 priority, 5 comments | A long-standing Windows user pain point that hurts browsing large files |
| [#20302](https://github.com/google-gemini/gemini-cli/issues/20302) | [Epic] Remote Agents Sprint 1 - Foundation | 🔴 Open | Core epic, 3 comments | Major team investment, laying the foundation for remote agent capabilities |
| [#20181](https://github.com/google-gemini/gemini-cli/issues/20181) | AskUser should support answering open questions in an external editor | 🔴 Open | 3 comments | Part of the same interaction upgrade as #20142, essential for long-text input scenarios |
| [#19514](https://github.com/google-gemini/gemini-cli/issues/19514) | AskUser outputs raw tags in plan mode | 🔴 Open | 3 comments, 1 👍 | A plan-mode UX flaw exposing rendering-logic problems |
| [#18953](https://github.com/google-gemini/gemini-cli/issues/18953) | Complex shell commands execute extremely slowly | 🔴 Open | 3 comments | A performance bottleneck for progress-bar/animation CLI tools, hurting real workflows |
| [#20461](https://github.com/google-gemini/gemini-cli/issues/20461) | Support iterating on plans with feedback annotations | 🔴 Open | 2 comments | A key capability for closing the plan workflow loop, connecting to editor integration |
| [#20550](https://github.com/google-gemini/gemini-cli/issues/20550) | JS Heap out of memory | 🔴 Open | 1 comment, severe | A long-session stability issue needing urgent attention |
| [#19519](https://github.com/google-gemini/gemini-cli/issues/19519) | Long-running shell commands falsely trigger loop detection | 🔴 Open | 1 comment, 2 👍 | The balance between smart detection and user experience |
| [#20721](https://github.com/google-gemini/gemini-cli/issues/20721) | Repeated error "params must have required property 'file_path'" | 🔴 Open | Filed today | A tool-call parameter validation flaw that traps the agent in an infinite loop |

---

## 4. Notable PR Progress

| # | Title | Status | Core Contribution | Impact Scope |
|:---|:---|:---|:---|:---|
| [#20701](https://github.com/google-gemini/gemini-cli/pull/20701) | Reduce LLM loop-detection false positives | 🟡 Open | Provide task context, tighten system prompts, adjust detection frequency thresholds | Solves legitimate operations like bulk refactoring being misjudged as loops |
| [#20439](https://github.com/google-gemini/gemini-cli/pull/20439) | Fix stopHookActive propagation on the AfterAgent hook retry path | 🟡 Open | Stops hooks that depend on this field from entering infinite rejection loops | Hook system stability |
| [#20709](https://github.com/google-gemini/gemini-cli/pull/20709) | Add the github-issue-creator skill | ✅ Merged | Standardizes the workflow for AI-generated GitHub issues | Automated workflow enhancement |
| [#20706](https://github.com/google-gemini/gemini-cli/pull/20706) | Fix the autoThemeSwitching theme mismatch | ✅ Merged | Fixes switching failures when the background color is unchanged but the theme is wrong | Terminal visual experience |
| [#20717](https://github.com/google-gemini/gemini-cli/pull/20717) | Add the `/mcp remove` UI subcommand | 🟡 Open | Interactively remove MCP server configurations | MCP ecosystem usability |
| [#17978](https://github.com/google-gemini/gemini-cli/pull/17978) | Strip trailing punctuation from inline Markdown URLs | 🟡 Open | Fixes links broken by Chinese and English punctuation | Internationalization experience |
| [#19855](https://github.com/google-gemini/gemini-cli/pull/19855) | Decode byte-array-encoded API error messages | 🟡 Open | Turns raw bytes like `91,123,10...` into readable UTF-8 text | Error diagnosis experience |
| [#18499](https://github.com/google-gemini/gemini-cli/pull/18499) | Pluggable voice input architecture | 🟡 Open | Gemini zero-install transcription + optional local Whisper | Accessibility and efficiency gains |
| [#20673](https://github.com/google-gemini/gemini-cli/pull/20673) | Stabilized footer architecture and UX improvements | 🟡 Open | Fixes footer flickering, improves information hierarchy and security visibility | Core TUI experience |
| [#20662](https://github.com/google-gemini/gemini-cli/pull/20662) | Fix the YOLO-mode plan exit bug | 🟡 Open | Ensures the correct payload is sent when `Ctrl+Y` auto-approves | Plan-mode workflow |

---

## 5. Feature Demand Trends

Based on an analysis of 50 active issues, community attention centers on five directions:

| Trend Direction | Representative Issues | Heat Indicators |
|:---|:---|:---|
| **🤖 Agent architecture expansion** | #20302, #20303, #20304, #20195, #20312 | 3 epics + sub-agents enabled by default |
| **🖥️ TUI stability and performance** | #18896, #20217, #20673, #20550 | Flickering, memory, and rendering problems erupting together |
| **📝 Plan-mode workflow** | #20461, #20452, #19514, #20662 | Editor integration, feedback iteration, approval experience |
| **🔧 Interaction experience refinement** | #20142, #20181, #18953, #19519 | History search, external editors, long-command optimization |
| **🔐 Enterprise-grade and extension capabilities** | #20058, #20344, #20060 | Headless-mode policy engine, extension configuration |

---

## 6. Developer Focus Points

### 🔴 High-frequency pain points
| Problem | Typical Feedback | Progress Status |
|:---|:---|:---|
| **Windows TUI flickering** | "Screen tearing and poor refresh while scrolling long lists" | #18896 being tracked, #20673 attempting a root fix |
| **Overly sensitive loop detection** | "Heavy grep searches misjudged as infinite loops" | #20701 is optimizing the algorithm, #19519 still pending |
| **Memory leaks/Heap exhaustion** | JS Heap crash after long sessions | #20550 newly filed, needs an urgent response |

### 🟡 Experience expectations
- **Native terminal feel**: loud calls for Ctrl+R history search (#20142) and external editor support (#20181)
- **Plan-mode loop**: a complete workflow spanning generate → edit → feedback → approve (#20461)
- **Voice and accessibility**: the pluggable voice solution in #18499 is drawing attention

### 🟢 Ecosystem building
- **Remote Agents** running three sprints in parallel, marking the architecture's move toward distribution
- **MCP ecosystem**: commands like `/mcp remove` (#20717) round out server lifecycle management
- **Skill system**: `github-issue-creator` (#20709) points the way toward standardized AI-assisted workflows

---

> 📌 **Subscription tip**: watch the `area/agent` and `area/core` labels — Remote Agents and sub-agent functionality will see notable progress soon.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Report | 2026-03-01

---

## Today's Overview

Community activity was steady today, with no new release. The focus is on **Web UI experience optimization** (2 related PRs) and **file recognition/autocomplete stability** (3 related issues). Developer feedback shows file context passing in IDE integration scenarios is still a pain point, while the concurrent-task interaction experience is starting to draw attention.

---

## Hot Community Issues

| # | Title | Type | Importance | Community Activity |
|---|------|------|--------|---------|
| [#1285](https://github.com/MoonshotAI/kimi-cli/issues/1285) | LLM provider error: Connection error | 🐛 Bug | **High** | Connection stability issues on Linux; 4 comments with ongoing follow-up; affects version 1.15.0 |
| [#1276](https://github.com/MoonshotAI/kimi-cli/issues/1276) | `@` file autocomplete misses files | 🐛 Bug | **High** | Users report incomplete file completion under the `kimi-k2.5` model; PR #1286 attempts a fix |
| [#1291](https://github.com/MoonshotAI/kimi-cli/issues/1291) | Crash when stdin input contains invalid Markdown | 🐛 Bug | **Medium-High** | An edge-case stability issue on version 1.11.0; input validation needs hardening |
| [#1289](https://github.com/MoonshotAI/kimi-cli/issues/1289) | `uname` version with a trailing space produces an invalid HTTP header | 🐛 Bug | **Medium** | A platform compatibility flaw affecting the login flow; zero comments, awaiting triage |
| [#1272](https://github.com/MoonshotAI/kimi-cli/issues/1272) | JetBrains AI Assistant cannot recognize files when invoked over ACP | ✨ Enhancement | **High** | **Core IDE integration pain point**: after files are dragged in, Kimi cannot recognize them automatically and requires typing the full path by hand |
| [#1287](https://github.com/MoonshotAI/kimi-cli/issues/1287) | Cannot pre-draft the next prompt while a task is running | ✨ Enhancement | **Medium** | A concurrent-workflow experience optimization need, reflecting developers' demand for multitasking efficiency |

---

## Notable PR Progress

| # | Title | Author | Feature/Fix Content |
|---|------|------|---------------|
| [#1286](https://github.com/MoonshotAI/kimi-cli/pull/1286) | Prioritize scanning shallow subdirectories to optimize the completer | @hongquan | Fixes the missed-file completion issue in #1276 and improves the directory traversal strategy |
| [#1290](https://github.com/MoonshotAI/kimi-cli/pull/1290) | Prompt toolbar now displays the todo list | @YoungY620 | Web UI enhancement: shows `SetTodoList` status in real time on the prompt toolbar, improving task visibility |
| [#1288](https://github.com/MoonshotAI/kimi-cli/pull/1288) | New-session button supports Cmd+Click to open a new tab | @YoungY620 | Interaction optimization: modifier+click creates a session in a new tab across Mac/Win/Linux |
| [#1127](https://github.com/MoonshotAI/kimi-cli/pull/1127) | Web UI detail style adjustments | @anxndsgn | Continues polishing the web interface visuals; created February 13 and still iterating |

---

## Feature Demand Trends

Community focus directions distilled from today's issues:

```
┌─────────────────────────────────────────────────────────┐
│  1. IDE ecosystem integration  ████████████████████  Highest priority │
│     → File context passing in JetBrains/VS Code plugins │
│                                                         │
│  2. Interaction efficiency  ████████████████░░░░░        │
│     → Concurrent task input, todo visualization, multi-tab workflows │
│                                                         │
│  3. Cross-platform stability  ██████████████░░░░░░░      │
│     → Linux connection issues, HTTP header compatibility, input validation │
│                                                         │
│  4. File system intelligence  ████████████░░░░░░░░░      │
│     → Autocomplete reliability, deep-directory handling │
└─────────────────────────────────────────────────────────┘
```

---

## Developer Focus Points

| Pain Point Category | Specific Symptoms | Impact Scope |
|---------|---------|---------|
| **MCP/ACP protocol file recognition** | When the JetBrains plugin calls over ACP, Kimi cannot sense the context after files are dragged in | Heavy IDE users |
| **Autocomplete reliability** | Deep-directory files missed when triggered by `@`; occasionally no files listed | Users of large codebases |
| **Network layer robustness** | Occasional connection errors on Linux, with no retry or diagnostic mechanism | Enterprise intranet/proxy environments |
| **Concurrent workflow blocking** | Cannot prepare the next instruction during long tasks, breaking the development rhythm | High-frequency interaction users |
| **Input boundary handling** | Invalid Markdown/special characters cause crashes, with no graceful degradation | Automated script scenarios |

---

> 📊 Data source: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) | Statistics window: 2026-02-28 to 2026-03-01

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Report | 2026-03-01

## Today's Overview

OpenCode community activity was high today: **memory leak fixes** and **VS Code integration** are the development priorities, while long-standing issues such as the **TUI scrolling experience** and **macOS permission scanning** keep stirring discussion. Demand for new model providers such as the Alibaba Cloud Bailian coding plan is growing markedly.

---

## Hot Community Issues

| # | Title | Status | Key Takeaways |
|---|------|------|---------|
| [#6209](https://github.com/anomalyco/opencode/issues/6209) | Cannot scroll TUI output in iTerm2 | 🔴 OPEN | **High-upvote pain point** (12👍): abnormal terminal scrolling behavior hurts the basic experience for iTerm2 users; 17 comments show urgent community demand for a workaround |
| [#14982](https://github.com/anomalyco/opencode/issues/14982) | Unexpectedly requests iCloud/Photos permissions | 🔴 OPEN | **Privacy sensitive**: the macOS build triggers system permission popups in unrelated directories; users worry about the scope of data scanning and want official clarification |
| [#13230](https://github.com/anomalyco/opencode/issues/13230) | Memory leak crashes the system (21GB RSS/116GB virt) | 🔴 OPEN | **Critical severity**: a single process exhausts 20GB of memory, triggers OOM and soft-locks the kernel; extremely risky in production |
| [#15163](https://github.com/anomalyco/opencode/issues/15163) | CLI scanning beyond the workspace triggers security alerts | 🔴 OPEN | **Enterprise security**: scanning sensitive directories such as `~/Library` trips internal security systems; indexing boundaries need to be restricted |
| [#6231](https://github.com/anomalyco/opencode/issues/6231) | Auto-discover OpenAI-compatible endpoint models | 🔴 OPEN | **High-upvote request** (40👍): manual configuration is tedious for LM Studio/Ollama users; auto-discovery would greatly lower the barrier to local AI |
| [#14819](https://github.com/anomalyco/opencode/issues/14819) | Support the Alibaba Cloud Bailian coding plan | 🔴 OPEN | **New model ecosystem**: covers domestic models such as Qwen 3.5, Kimi K2.5, and GLM 4.7; loud calls from Chinese developers |
| [#1905](https://github.com/anomalyco/opencode/issues/1905) | Terminal cursor forced to blink | 🔴 OPEN | **Accessibility**: overrides the terminal's native settings and disturbs light-sensitive users; 19👍 reflects attention to experience details |
| [#7399](https://github.com/anomalyco/opencode/issues/7399) | MCP tool filtering (includeTools/excludeTools) | 🔴 OPEN | **MCP governance**: loading every tool when a server has too many hurts performance; fine-grained control is a production-grade must |
| [#14391](https://github.com/anomalyco/opencode/issues/14391) | Stop changing the response design so frequently | 🔴 OPEN | **UX stability**: overly fast UI iteration piles cognitive load on users, reflecting the hard balance between product pace and user experience |
| [#13282](https://github.com/anomalyco/opencode/issues/13282) | Windows 1.1.59 crashes on startup (Bun AVX) | 🔴 OPEN | **Compatibility**: Skylake-architecture CPUs hit Bun runtime AVX instruction crashes, affecting Windows enterprise users |

---

## Notable PR Progress

| # | Title | Type | Key Value |
|---|------|------|---------|
| [#15504](https://github.com/anomalyco/opencode/pull/15504) | VS Code extension: configurable TUI location | 🆕 Feature | Supports dual `editor`/`panel` modes, solving TUI layout inflexibility inside the IDE |
| [#15501](https://github.com/anomalyco/opencode/pull/15501) | VS Code ACP Chat Participant | 🆕 Feature | Native VS Code Chat integration via the Agent Client Protocol, a key step for the IDE ecosystem |
| [#13514](https://github.com/anomalyco/opencode/pull/13514) | Fix multiple memory leaks | 🔧 Fix | Addresses root causes such as unreleased bus subscriptions and uncleaned compaction data, mapping to the #13230 critical issue |
| [#15505](https://github.com/anomalyco/opencode/pull/15505) | Error messages show skill names instead of array indices | 🔧 Fix | Fixes the `[object Promise]` display issue (#7080), improving the debugging experience |
| [#15502](https://github.com/anomalyco/opencode/pull/15502) | Fix MCP OAuth first-connection failure | 🔧 Fix | Solves 401 authentication problems in dynamic client registration scenarios, improving MCP ecosystem stability |
| [#11303](https://github.com/anomalyco/opencode/pull/11303) | ACP client correctly exposes input/output | 🔧 Fix | The tool-call panel in the Zed integration shows the actual command instead of the description, improving debugging transparency |
| [#15102](https://github.com/anomalyco/opencode/pull/15102) | Native support for the Alibaba Cloud Bailian coding plan | 🆕 Feature | Covers 6+ models including Qwen/Kimi/GLM/MiniMax, out of the box for Chinese developers |
| [#14955](https://github.com/anomalyco/opencode/pull/14955) | Desktop project sidebar working-status indicator | 🆕 Feature | Resolves #14430/#12077 by visualizing the AI-processing state and easing "is it frozen" anxiety |
| [#15414](https://github.com/anomalyco/opencode/pull/15414) | Add ClamAV/Trivy security scanning workflows | 🆕 Feature | Responds to the #15189 false-positive antivirus incident by building trustworthy supply-chain security |
| [#15487](https://github.com/anomalyco/opencode/pull/15487) | Multi-account workspace auth + device-flow login | 🆕 Feature | Supports switching across multiple organization accounts and managing credentials in the CLI without editing config, a must for enterprise scenarios |

---

## Feature Demand Trends

Based on an analysis of 50 active issues, community attention falls into four directions:

| Trend Direction | Representative Issues | Heat Indicators |
|---------|-----------|---------|
| **Deep IDE integration** | VS Code/ACP/Zed multi-platform adaptation | PRs #15501/#11303 advancing in sync |
| **Performance and stability** | Memory leaks, Bun crashes, large-file handling | 2 Critical + 3 High Priority |
| **Model ecosystem expansion** | Alibaba Cloud Bailian, OpenRouter, local auto-discovery | #6231 (40👍) is the highest-upvote pending item |
| **Privacy and security boundaries** | Permission scanning scope, MCP tool filtering, security auditing | Rising compliance demands from enterprise users |

---

## Developer Focus Points

### 🔴 High-frequency pain points
1. **TUI experience debt**: terminal rendering problems accumulating over time — scrolling behavior (#6209/#2500), cursor blinking (#1905), CJK table alignment (#14927)
2. **macOS permission anxiety**: iCloud/Photos popups (#14982) and scanning outside the workspace (#15163) raise questions about the scope of data collection
3. **Windows compatibility**: ecosystem adaptation issues such as the Bun AVX instruction set (#13282), antivirus false positives (#15189), and reserved device-name files (#15480)

### 🟡 Emerging needs
- **Fine-grained MCP governance**: tool filtering (#7399) and OAuth stability (#15502) mark MCP's transition from "usable" to "pleasant to use"
- **Multi-account/multi-workspace**: identity management for enterprise team collaboration scenarios (#15487)

### 🟢 Positive signals
- A concrete fix PR exists for the memory leaks (#13514)
- Domestic model ecosystem integration is accelerating (#15102)
- Security scanning mechanisms are being built proactively (#15414)

---

*Data source: github.com/anomalyco/opencode | Statistics window: 2026-02-28 to 2026-03-01*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Report | 2026-03-01

---

## 1. Today's Overview

**v0.11.0 stable release published**, bringing comprehensive model-provider documentation enhancements and a permissions fix for the Arch Linux install script. Community activity surged, with **30 issues** and **27 PRs** added within 24 hours. IDE integration (especially Zed/VSCode) and ACP protocol compatibility dominated the discussion, and a key fix is already in for the session-crash problem caused by PDF handling.

---

## 2. Releases

### v0.11.0 Stable Release
| Version | Type | Core Changes |
|:---|:---|:---|
| [v0.11.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.11.0) | Stable | Model-provider documentation enhancements + Arch install permissions fix |
| [v0.11.0-preview.1](https://github.com/QwenLM/qwen-code/releases/tag/v0.11.0-preview.1) | Preview | Same as above |
| [v0.11.0-nightly.20260228](https://github.com/QwenLM/qwen-code/releases/tag/v0.11.0-nightly.20260228.e93b2873) | Nightly build | Same as above |

**Update details**: [@Mingholy](https://github.com/Mingholy) improved the `modelProviders` documentation, adding comprehensive examples and behavior notes; [@DennisYu07](https://github.com/DennisYu07) fixed the permission check in the Arch Linux install script and added sudo detection.

---

## 3. Hot Community Issues

| # | Status | Title | Author | Key Takeaways |
|:---|:---|:---|:---|:---|
| [#2012](https://github.com/QwenLM/qwen-code/issues/2012) | 🔴 Open | Massive bash tool-call failures | @useribs | **Stability issue**: users report frequent bash tool-call failures across multiple projects, hurting core workflows; needs priority investigation |
| [#2020](https://github.com/QwenLM/qwen-code/issues/2020) | 🔴 Open | Reading PDFs triggers API 400 errors and permanently corrupts sessions | @LeslieZhang1314 | **Severe bug**: reading a PDF sets off an unrecoverable "API Error: 400" that takes down the whole model service; [PR #2024](https://github.com/QwenLM/qwen-code/pull/2024) already fixes it |
| [#1151](https://github.com/QwenLM/qwen-code/issues/1151) | 🔴 Open | Plan Mode doesn't work as expected in ACP mode | @tanzhenxin | **Long-standing open case**: in the Zed editor, `--approval-mode plan` still demands item-by-item confirmation, defeating the design intent and hurting the ACP experience |
| [#1985](https://github.com/QwenLM/qwen-code/issues/1985) | 🔴 Open | VSCode Companion should support Plan Mode switching | @tanzhenxin | **Feature gap**: the CLI supports `Shift+Tab` to cycle the four approval modes, but the VSCode plugin lacks it, fragmenting the experience |
| [#1706](https://github.com/QwenLM/qwen-code/issues/1706) | 🔴 Open | Abnormal file diff display in JetBrains IDEs | @yezhoujie | **IDE integration pain point**: after a file is modified, the diff view cannot fetch the original content, every change shows as an addition, and individual changes cannot be accepted/rejected |
| [#1567](https://github.com/QwenLM/qwen-code/issues/1567) | 🔴 Open | Cannot link VSCode in code-server/WebIDE environments | @yiliang114 | **Cloud development blocker**: `host.docker.internal` resolution failure stops the CLI from connecting to VSCode, hurting containerized development |
| [#2004](https://github.com/QwenLM/qwen-code/issues/2004) | 🔴 Open | OOM crashes | @wenhuiwang93 | **Performance issue**: out-of-memory exits the CLI abnormally; the resource management mechanism needs attention |
| [#2015](https://github.com/QwenLM/qwen-code/issues/2015) | 🔴 Open | ACP Zed integration: mode switching and session management broken | @Mingholy | **Protocol compatibility**: incompatible with the `@zed-industries/claude-agent-acp` protocol format, leaving core features unusable |
| [#2025](https://github.com/QwenLM/qwen-code/issues/2025) | 🔴 Open | Skill invocation auto-inserts spaces, causing infinite loops | @yuffo | **Chinese support flaw**: skills named in Chinese get spaces inserted incorrectly, the invocation fails and loops forever — an internationalization experience problem |
| [#2010](https://github.com/QwenLM/qwen-code/issues/2010) | 🔴 Open | Client-side sensitive-information redaction | @inkdust2021 | **Security need**: automatically replace secrets with placeholders before sending requests and restore them for local display, an enterprise-security must |

---

## 4. Notable PR Progress

| # | Status | Title | Author | Technical Value |
|:---|:---|:---|:---|:---|
| [#1980](https://github.com/QwenLM/qwen-code/pull/1980) | 🟡 Open | Implement the Modes Layer professional agent configuration system | @impulse22-ru | **Architecture upgrade**: adds the `@qwen-code/modes` package with 6 built-in modes (Architect/Code/Ask/Debug/Review/Orchestrator), supporting custom modes and a `/mode` switching command |
| [#2024](https://github.com/QwenLM/qwen-code/pull/2024) | 🟡 Open | Reject PDF files to prevent session corruption | @drewd789 | **Key fix**: intercepts PDFs at the source instead of base64-embedding them, curing the API 400 errors and session crashes caused by [#2020](https://github.com/QwenLM/qwen-code/issues/2020) |
| [#1912](https://github.com/QwenLM/qwen-code/pull/1912) | 🟡 Open | Agent collaboration arena: multi-model competitive execution | @tanzhenxin | **Innovative feature**: runs multiple models in parallel isolated by git worktrees, compares results side by side, and supports merging the best solution |
| [#2017](https://github.com/QwenLM/qwen-code/pull/2017) | 🟡 Open | Fix ACP protocol compatibility with the Zed editor | @Mingholy | **Ecosystem expansion**: aligns with the `@zed-industries/claude-agent-acp` response format, enabling mode switching, session listing, and recovery |
| [#1988](https://github.com/QwenLM/qwen-code/pull/1988) | 🟡 Open | Hooks system infrastructure | @DennisYu07 | **Extensibility boost**: 12 lifecycle event hooks (PreToolUse/PostToolUse etc.), with custom commands manageable from both the CLI and the UI |
| [#2018](https://github.com/QwenLM/qwen-code/pull/2018) | 🟡 Open | Support the AGENTS.md context file by default | @LaZzyMan | **Standards compatibility**: seamlessly matches the [agents.md](https://agents.md/) standard, recognizing project-level agent instructions with no manual configuration |
| [#2021](https://github.com/QwenLM/qwen-code/pull/2021) | 🟡 Open | Detect and guard against truncated tool-call output | @sundapeng | **Reliability improvement**: addresses the hazard where `max_tokens` truncates JSON while some providers wrongly return `finish_reason: "stop"` |
| [#2008](https://github.com/QwenLM/qwen-code/pull/2008) | 🟡 Open | Interactive extension-management TUI | @LaZzyMan | **Experience optimization**: unifies list/update/disable/enable/uninstall/details operations with keyboard navigation (↑↓/Enter/Esc) |
| [#2007](https://github.com/QwenLM/qwen-code/pull/2007) | 🟡 Open | Clean control characters from terminal output | @tengfeiwang1 | **UI fix**: resolves the layout misalignment caused by `\r\n` ([#1950](https://github.com/QwenLM/qwen-code/issues/1950)) |
| [#2005](https://github.com/QwenLM/qwen-code/pull/2005) | 🟡 Open | Strengthen the output-language.md template to enforce language compliance | @zhangxy-zju | **Internationalization improvement**: changes "Prefer" to "You MUST", fixing inconsistent LLM output language across multi-turn conversations |

---

## 5. Feature Demand Trends

Cluster analysis based on 30 active issues:

| Trend Direction | Heat | Typical Demands |
|:---|:---|:---|
| **Deep IDE integration** | 🔥🔥🔥🔥🔥 | VSCode/Zed/JetBrains feature parity (Plan Mode, /insight, /export, diff fixes) |
| **ACP protocol ecosystem** | 🔥🔥🔥🔥🔥 | Mode switching, session management, OAuth/API-KEY auth expansion |
| **Enterprise security** | 🔥🔥🔥🔥 | Sensitive-information redaction, structured error logs, audit trails |
| **Multi-agent parallelism** | 🔥🔥🔥🔥 | Sub-agent parallel execution, arena comparison mode |
| **Chinese/internationalization** | 🔥🔥🔥 | Enforced output-language consistency, Chinese-named skill support, localized reports |
| **Cloud/container support** | 🔥🔥🔥 | code-server, WebIDE, WSL, Docker environment adaptation |
| **Observability** | 🔥🔥🔥 | Real-time token display, performance monitoring, OOM troubleshooting |

---

## 6. Developer Focus Points

### 🔴 High-frequency pain points
1. **Fragmented IDE experience**: the CLI and the VSCode/Zed plugins are not feature-equal (missing commands such as Plan Mode, /insight, /export)
2. **ACP protocol friction**: mode switching and session recovery are broken in the Zed integration, and auth methods are limited
3. **File-handling traps**: PDFs permanently corrupt sessions, and the diff view is broken in JetBrains

### 🟡 Performance and stability
- OOM crash reports are rising; memory management for large projects needs attention
- The bash tool-call failure rate is on the high side, hurting automated workflows

### 🟢 Positive signals
- The community is proactively contributing innovative features such as the Hooks system, arena mode, and AGENTS.md support
- Internationalization improvements (language enforcement, Chinese skill fixes) are getting quick responses

---

> 📊 Data source: [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) | Statistics window: 2026-02-28 to 2026-03-01

</details>

---
*This report was auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*