# AI CLI Community Report 2026-02-24

> Generated at: 2026-02-24 04:45 UTC | Tools covered: 6

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)

---

## Cross-tool Comparison

# AI CLI Tools Ecosystem Comparison Report | 2026-02-24

---

## 1. Ecosystem Overview

The current AI CLI tool ecosystem shows a **"three superpowers plus many strong players" landscape**: Claude Code and OpenAI Codex lead on enterprise-grade features and architectural depth, Gemini CLI is rapidly catching up backed by Google's model resources, while emerging tools such as OpenCode, Qwen Code, and Kimi CLI look for differentiation in vertical scenarios and open source ecosystems. Overall trends show that **fine-grained permission systems, cross-platform stability, and long-session management** have become industry-wide challenges, and tool competition is shifting from "feature availability" to a deeper contest of "engineering maturity" and "enterprise readiness".

---

## 2. Activity Comparison by Tool

| Tool | Issues (today) | PRs (today) | Version releases | Key updates |
|:---|:---:|:---:|:---|:---|
| **Claude Code** | 10+ | 8 | v2.1.51 | 🔴 Windows extension crash incident (CI build contamination) |
| **OpenAI Codex** | 10+ | 10 | rust-v0.105.0-alpha.14~16 | Architecture refactoring (shell-escalation decoupling), permission system upgrades |
| **Gemini CLI** | 10 | 10 | v0.29.7, v0.30.0-preview.6 | Quota detection fix, Plan Mode policy engine refactoring |
| **OpenCode** | 10 | 10 | — | Web UI consistency fixes, session hooks proposal |
| **Qwen Code** | 14 | 13 | v0.10.5-nightly | VS Code layout improvements, multi-model arena experiment |
| **Kimi CLI** | 1 | 3 | — | MCP debug logging fix, Nix/Fish experience improvements |

> **Activity tiers**: Qwen Code and OpenAI Codex had the highest update density today (20+ items); Kimi CLI has entered stable maintenance, with updates slowing noticeably.

---

## 3. Shared Feature Directions

| Feature direction | Tools involved | Specific requests |
|:---|:---|:---|
| **Fine-grained permissions and sandboxing** | Claude Code (#28029, #23946), Codex (#11871, #12638), Gemini (#20058) | PreToolUse hooks, dynamic permission requests, policy engine for headless mode |
| **Cross-platform stability** | Claude Code (#28081 Windows crash), Codex (#12542, #12644), Qwen (#1904, #1889) | Windows CI build verification, enterprise security software compatibility, macOS path handling |
| **Long-session/memory management** | Claude Code (#14227, #27140), Codex (#12184, #11984), OpenCode (#14863, #12687) | Cross-session persistent memory, context compaction, memory leak fixes |
| **IDE integration depth** | Qwen (#1308, #1870), Claude Code (VS Code extension), OpenCode (#14864) | Sidebar layout freedom, Web/TUI configuration consistency, Activity Bar integration |
| **Model observability** | Codex (#2109 Event Hooks), Gemini (#18494 diagnostic tooling), OpenCode (#14863 hooks) | Structured logging, real-time stream observation, agent behavior debugging |

---

## 4. Differentiated Positioning Analysis

| Tool | Core focus | Target users | Technical approach characteristics |
|:---|:---|:---|:---|
| **Claude Code** | Enterprise security and compliance | Large teams, regulated industries | **Leading hook/plugin architecture**: mature security mechanisms such as PreToolUse guards and destructive-command-guard; the abrupt OAuth policy change reflects tightening platform control |
| **OpenAI Codex** | Engineering architecture and performance | Professional developers, performance-sensitive scenarios | **Rust core refactoring**: decoupling shell-escalation and removing exec-server in pursuit of maximum execution efficiency; the desktop file I/O crisis exposes architectural debt |
| **Gemini CLI** | Plan Mode workflows | Cost-sensitive users, Google ecosystem | **Policy-driven architecture**: conductor.toml as the configuration hub, automatic model switching (Pro/Flash tiering), though the hardcoded tool visibility issue remains unsolved |
| **OpenCode** | Open source extensibility | Self-hosting users, plugin developers | **Unified dual clients (TUI/Web)**, native hooks proposal catching up with Claude; memory leaks and Gemini compatibility issues constrain production readiness |
| **Qwen Code** | Multi-model ecosystem and localization | Chinese developers, Alibaba Cloud users | **Bailian platform integration**: rapid onboarding of third-party models (Zhipu, Moonshot); the Agent Arena experiment shows evolution toward "model comparison evaluation" |
| **Kimi CLI** | Simplicity and stability | Lightweight users, early MCP adopters | **Minimal viable product**: streamlined features focused on the core experience; the MCP OAuth logging fix reflects prioritizing ecosystem integration over feature expansion |

---

## 5. Community Activity and Maturity

```
Maturity quadrant (estimated from today's data)
─────────────────────────────────────────
High activity │  Codex (architecture refactoring phase) │  Claude Code (enterprise stable phase)
              │  Qwen Code (rapid catch-up phase)      │
              │  OpenCode (feature completion phase)   │
──────────────┼────────────────────────────────────────┼──────────────
Low activity  │                                        │  Gemini CLI (policy adjustment phase)
              │                                        │  Kimi CLI (maintenance stability phase)
              └────────────────────────────────────────┘
                   Low maturity ←————→ High maturity
```

| Assessment dimension | Leaders | Notes |
|:---|:---|:---|
| **Community response speed** | Codex, OpenCode | Key issues get PR follow-ups within 24 hours |
| **Enterprise feature completeness** | Claude Code | Custom npm repositories, team environment variables, etc. already shipped |
| **Architectural foresight** | Codex, Claude Code | Rust refactoring and the hook system lead the technical direction |
| **Production stability risk** | OpenCode, Codex | Blocking issues such as memory leaks and the file I/O crisis remain unresolved |
| **Ecosystem openness** | Qwen Code, Gemini CLI | Active third-party model onboarding and MCP integration |

---

## 6. Trend Signals Worth Watching

| Signal | Industry significance | Recommended developer actions |
|:---|:---|:---|
| **Hook/plugin architecture becoming standard** | Tools are shifting from "closed products" to "programmable platforms" | Prioritize evaluating a tool's extension point design (PreToolUse, Event Hooks, session lifecycle) to avoid vendor lock-in |
| **Windows and enterprise environments as the quality litmus test** | The dividing line between consumer-grade and production-grade tools | Enterprise tool selection should verify: multi-platform CI build coverage, security software compatibility, headless/CI scenario support |
| **Model routing and tiering strategies becoming explicit** | Cost optimization and capability matching become core engineering problems | Pay attention to a tool's model switching mechanisms (Pro/Flash automatic tiering, fallback strategies) and assess token efficiency optimization opportunities |
| **Context management shifting from "capacity competition" to "intelligent compression"** | Long windows ≠ high availability; context quality determines the ceiling | Prefer tools with tiered memory, compaction that preserves key information, and token efficiency monitoring |
| **Accelerating MCP ecosystem integration** | Tool boundaries are blurring and an "AI-native IDE" form is emerging | Evaluate the maturity of the MCP server ecosystem and watch integration details such as OAuth, progress display, and debugging experience |

---

*This report is generated from public community data as of 2026-02-24; PoC validation against specific scenarios is recommended*

---

## Detailed Reports by Tool

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

# Claude Code Community Report | 2026-02-24

---

## Today at a Glance

The community saw a large-scale **Windows VS Code extension crash incident** today — v2.1.51 hardcoded Linux paths during CI builds, leaving Windows users unable to activate the extension, and more than ten related issues flooded in. Meanwhile, an apparent Anthropic OAuth policy adjustment triggered authentication failures for third-party apps, becoming a focus of developer attention.

---

## Version Releases

### v2.1.51 Released
| Item | Details |
|:---|:---|
| **New features** | `claude remote-control` subcommand, supporting externally built local environment services |
| **Configuration improvements** | Plugin marketplace Git timeout raised from 30s to 120s, plus a new `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS` environment variable |
| **Enterprise support** | Added custom npm repository support |

> 🔗 https://github.com/anthropics/claude-code/releases/tag/v2.1.51

---

## Community Hotspot Issues

### 🔴 Severe Failures

| # | Title | Status | Key information |
|:---|:---|:---|:---|
| **#28081** | [Windows VS Code extension activation failure: hardcoded Linux CI paths](https://github.com/anthropics/claude-code/issues/28081) | 🔴 OPEN | **v2.1.51 regression**. `extension.js` contains `file:///home/runner/work/...` paths, causing `createRequire` to crash on Windows. Wide impact, tagged `regression` |
| **#28076** | [command 'claude-vscode.editor.openLast' not found](https://github.com/anthropics/claude-code/issues/28076) | 🔴 OPEN | Same root cause; the Windows extension is completely broken, 👍 3 |
| **#28082** | [Build 2.1.51 hardcodes Linux paths, causing Windows crashes](https://github.com/anthropics/claude-code/issues/28082) | 🔴 OPEN | Detailed reproduction report confirming CI build artifact contamination |
| **#28056** | [VS Code extension Windows activation failure](https://github.com/anthropics/claude-code/issues/28056) | 🔴 OPEN | Duplicate report; the community confirmed multiple cases |
| **#28073** | [v2.1.51 Windows activation failure](https://github.com/anthropics/claude-code/issues/28073) | 🔴 OPEN | Additional technical detail: file URL parsing errors |

### 🔶 Authentication and API Issues

| # | Title | Status | Key information |
|:---|:---|:---|:---|
| **#28091** | [Anthropic disables OAuth tokens for third-party apps](https://github.com/anthropics/claude-code/issues/28091) | 🔴 OPEN | **Sudden policy change**. Third-party app OAuth authentication stopped working, affecting the integration ecosystem |
| **#5893** | [OAuth authentication-unsupported error suddenly appearing mid-run](https://github.com/anthropics/claude-code/issues/5893) | 🔴 OPEN | Long-running issue, 62 comments, 47 👍, updated again today, possibly related to the change above |

### 🔷 High-traction Feature Requests

| # | Title | Status | Key information |
|:---|:---|:---|:---|
| **#21151** | [READ tool does not display file names](https://github.com/anthropics/claude-code/issues/21151) | 🔴 OPEN | **The community's hottest request**, 110 comments, 175 👍. In the TUI, multi-file read targets cannot be told apart, severely disrupting workflows |
| **#12346** | [GitLab integration (repository connection, MRs, mobile)](https://github.com/anthropics/claude-code/issues/12346) | 🔴 OPEN | 25 👍, a must-have for enterprise users, in contrast to the current GitHub-first strategy |
| **#14227** | [Cross-session persistent memory](https://github.com/anthropics/claude-code/issues/14227) | 🔴 OPEN | 10 comments, 6 👍. Every launch starts with zero context; developers are calling for MEMORY.md enhancements |
| **#27298** | [Tiered memory system](https://github.com/anthropics/claude-code/issues/27298) | 🔴 OPEN | Detailed proposal: project-level, user-level, and global-level memory architecture |

---

## Notable PR Progress

| # | Title | Status | What it does/fixes |
|:---|:---|:---|:---|
| **#28088** | [Fix hookify plugin import paths](https://github.com/anthropics/claude-code/pull/28088) | 🟢 OPEN | Resolves the `No module named 'hookify'` error by correcting mixed absolute/relative imports |
| **#28065** | [Batch fixes for small open PRs](https://github.com/anthropics/claude-code/pull/28065) | 🟢 OPEN | Collection: hookify field mapping fix + Python 3.8 type compatibility + documentation updates |
| **#28062** | [Batch community PR fixes](https://github.com/anthropics/claude-code/pull/28062) | 🟢 OPEN | Collection: hookify import fix + skills system improvements + configuration validation enhancements |
| **#28029** | [Bash/Glob tool deny-path guard hook](https://github.com/anthropics/claude-code/pull/28029) | 🟢 OPEN | New PreToolUse hook that closes the loophole where `grep -r` and `Glob` patterns bypass deny rules |
| **#27928** | [Enhanced compound command validation](https://github.com/anthropics/claude-code/pull/27928) | 🟢 OPEN | Resolves ambiguous permission prompts for commands like `sleep 10 && do-something`, improving security |
| **#23946** | [destructive-command-guard plugin](https://github.com/anthropics/claude-code/pull/23946) | 🟢 OPEN | PreToolUse hook: intercepts irreversible operations (rm -rf /, dangerous git operations, policy file modification) |
| **#27140** | [memory-bridge cross-session memory plugin](https://github.com/anthropics/claude-code/pull/27140) | 🟢 OPEN | The `/bridge` command persists session learnings to MEMORY.md/CLAUDE.md/skills, with context compaction warnings |
| **#27911** | [Issue triage workflow improvements](https://github.com/anthropics/claude-code/pull/27911) | 🔴 CLOSED | Merged: extracts the `/triage-issue` command, scripts label operations and validates them |

---

## Feature Request Trends

```
Heat ranking | Direction             | Representative issues
─────────┼───────────────────────┼────────────────────────────────────────
  🔥🔥🔥  | IDE integration stability | #28081 #28076 #28056 and the Windows crash wave
  🔥🔥🔥  | Authentication/authorization | #28091 #5893 #8938 OAuth policy and token management
  🔥🔥    | Context/memory system | #14227 #27298 #21151 persistent memory and TUI information display
  🔥🔥    | Multi-platform support | #12346 GitLab integration, #13738 WSL clipboard
  🔥      | Enterprise/team features | #28087 Agent team environment variables, #28075 multi-agent coordination
  🔥      | Security and permissions | #28086 permission mode matching, #27407 command false positives
```

---

## Developer Concerns

### 🚨 Critical Pain Points

| Problem | Impact | Community voice |
|:---|:---|:---|
| **Windows CI build contamination** | v2.1.51 completely unusable | "This is a regression that should have been caught in CI" — developers question test coverage |
| **Abrupt OAuth policy change** | Third-party integrations broken | No advance notice; production environments suddenly failed |

### 📊 High-frequency Requests

1. **Cross-platform build quality** — Windows/macOS/Linux build artifacts need independent verification to avoid hardcoded paths
2. **Transparent communication of product changes** — Policy adjustments such as OAuth need migration windows and official announcements
3. **TUI information density optimization** — Tool output readability, as reflected in #21151, is a long-standing pain point
4. **Enterprise-grade code hosting support** — The tension between GitLab demand (#12346) and the current GitHub-first strategy

### 💡 Emerging Trends

- **Active hook/plugin ecosystem**: 4 PRs today involve PreToolUse hooks (security guards, path validation, memory bridging)
- **Agent team features need refinement**: multi-session coordination (#28078 #28075) is becoming a bottleneck for advanced users

---

*This report is generated from public GitHub data; follow [anthropics/claude-code](https://github.com/anthropics/claude-code) for the latest updates*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Report | 2026-02-24

## Today at a Glance

The Codex community was extremely active today: the core team pushed forward intensively on the **shell-escalation architecture refactoring** and **permission system upgrades**, while fixing multiple stability issues affecting Windows and macOS users. On the community side, the **desktop file I/O performance crisis** became a new flashpoint, with CPU spikes caused by conflicts with enterprise security software drawing wide attention.

---

## Version Releases

**rust-v0.105.0-alpha.14~16** three releases in a row \
🔗 [v0.105.0-alpha.16](https://github.com/openai/codex/releases/tag/rust-v0.105.0-alpha.16)

> Three consecutive alpha iterations focused on stability fixes in the Rust core layer, paving the way for the upcoming stable release.

---

## Community Hotspot Issues (Top 10)

| # | Title | Status | Criticality | Community response |
|---|------|------|--------|----------|
| [#12644](https://github.com/openai/codex/issues/12644) | **Extreme desktop file I/O drives CPU spikes** (5,500-12,000 openat/sec) | 🔴 OPEN | ⭐⭐⭐⭐⭐ | Enterprise security software conflict, affecting production environments |
| [#12631](https://github.com/openai/codex/issues/12631) | Model performance "falling off a cliff", suspected throttling | 🟢 CLOSED | ⭐⭐⭐⭐⭐ | Users question the routing policy; closed quickly by officials |
| [#12184](https://github.com/openai/codex/issues/12184) | Context loss when switching multi-worker agents | 🔴 OPEN | ⭐⭐⭐⭐☆ | Blocks enterprise user workflows |
| [#10384](https://github.com/openai/codex/issues/10384) | **Expose the `request_user_input` tool in code mode** | 🔴 OPEN | ⭐⭐⭐⭐⭐ | 70 👍, a long-standing highly-voted request |
| [#12108](https://github.com/openai/codex/issues/12108) | Xcode MCP repeatedly prompts for permission on every focus | 🔴 OPEN | ⭐⭐⭐⭐☆ | 5 👍, a macOS developer experience pain point |
| [#12128](https://github.com/openai/codex/issues/12128) | `project_root_markers` not applied to AGENTS.md discovery | 🔴 OPEN | ⭐⭐⭐⭐☆ | Configuration consistency bug, a fix PR already exists |
| [#11984](https://github.com/openai/codex/issues/11984) | Severe UI lag in long sessions | 🔴 OPEN | ⭐⭐⭐⭐☆ | Electron performance bottleneck, feedback from Pro users |
| [#12542](https://github.com/openai/codex/issues/12542) | Windows Terminal TUI input regression (ANSI sequence leakage) | 🟢 CLOSED | ⭐⭐⭐⭐☆ | 9 comments, fixed quickly |
| [#2109](https://github.com/openai/codex/issues/2109) | **Event Hooks system** | 🔴 OPEN | ⭐⭐⭐⭐⭐ | 426 👍, the highest-voted feature request |
| [#12637](https://github.com/openai/codex/issues/12637) | git stash-style experience for branch switching | 🔴 OPEN | ⭐⭐⭐☆☆ | Feedback from Chinese users, workflow optimization |

### Deep Dive

- **#12644 performance crisis**: This is today's most destructive new problem. In enterprise environments equipped with endpoint security software, Codex desktop generates tens of thousands of file system calls per second, driving CPU usage to 100%. This may share the same root cause as the long-session lag in [#11984](https://github.com/openai/codex/issues/11984), both pointing to design flaws in the file monitoring mechanism.

- **#12631 model quality controversy**: Users reported GPT-5.3-codex performance "falling off a cliff" and suspect a silent downgrade to a lower-capability model. It was closed quickly by officials without a technical explanation, which may spark community trust discussions.

---

## Notable PR Progress (Top 10)

| # | Title | Author | Core change |
|---|------|------|----------|
| [#12638](https://github.com/openai/codex/pull/12638) | **Refactor: decouple shell-escalation from codex-core** | @bolinfest | Removes exec-server, paving the way for new shell tools |
| [#12632](https://github.com/openai/codex/pull/12632) | Remove exec-server, move execve wrapper into shell-escalation | @bolinfest | Architectural cleanup, simplifying the privilege escalation path |
| [#11871](https://github.com/openai/codex/pull/11871) | **Introduce Feature::RequestPermissions** | @dylan-hurd-oai | The model can request specific in-sandbox permissions (e.g., writing to a designated directory) |
| [#12639](https://github.com/openai/codex/pull/12639) | Fix `project_root_markers` support for AGENTS.md discovery | @etraut-openai | Resolves #12128, configuration consistency |
| [#12613](https://github.com/openai/codex/pull/12613) | **TUI adds /copy command** | @won-openai | One-keystroke copy of the latest complete reply |
| [#12628](https://github.com/openai/codex/pull/12628) | **Ctrl-L clears the screen (without starting a new session)** | @won-openai | A lightweight action distinct from /clear |
| [#12630](https://github.com/openai/codex/pull/12630) | Fix /review to use runtime configuration | @hdcodedev | Resolves #12495, reasoning effort syncs after model switches |
| [#12636](https://github.com/openai/codex/pull/12636) | Improved js_repl uncaught exception handling | @fjord-oai | Clearer error reporting on kernel crashes |
| [#12635](https://github.com/openai/codex/pull/12635) | Tighter memory lookup and citation rules | @zuxin-oai | Reduces irrelevant memory retrieval and enforces structured citations |
| [#12610](https://github.com/openai/codex/pull/12610) | **TUI /fork branch picker UI** | @yvolovich-cyber | Visual selection of rollback points, complementing #12577 |

### Architecture Trends

The triple PR series led by **bolinfest** today (#12638/#12632/#12614) marks a major refactoring of Codex's execution layer architecture — completely removing the legacy exec-server and consolidating privilege escalation logic into a separate `shell-escalation` module. This lays the foundation for finer-grained permission control later (such as RequestPermissions in #11871).

---

## Feature Request Trends

Semantic clustering based on 50 issues:

```
🔥 High-heat directions 📈 Growth trends
─────────────────────────────────────────
1. Fine-grained permissions and sandboxing ████████████████████  RequestPermissions landing
2. IDE/editor integration █████████████████░░░  VS Code/Cursor stability
3. Performance and resource optimization ███████████████████░  File I/O, memory, long sessions
4. Developer experience (DX) ███████████████░░░░░  Event Hooks, /copy, /fork
5. Voice/multimodal input ██████████░░░░░░░░░░  #3000 voice dictation 66 👍
6. Model observability ██████████░░░░░░░░░░  Reasoning process visualization
7. Windows compatibility ████████████░░░░░░░░  Ongoing regression issues
```

---

## Developer Concerns

### 🔴 Blocking Pain Points

| Problem | Scope of impact | Workaround |
|------|--------|----------|
| 100% CPU in enterprise environments (#12644) | Enterprise/security software users | None yet, needs an official fix |
| Windows TUI input failure (#12542) | Windows Terminal users | Fixed, pending release |
| "Bad Request" batch errors (#12477 etc.) | All platforms | Closed quickly by officials, or already fixed server-side |
| Repeated VS Code logins (#12170) | ChatGPT auth users | Switch to API key authentication |

### 🟡 High-frequency Requests

1. **Human interaction in code mode** (#10384): a long-standing request with 70 👍; developers want to trigger user confirmations in non-Agent mode too
2. **Session management enhancements**: PRs for /fork, /title, and a stash-like branch switching experience are landing in rapid succession
3. **MCP ecosystem maturation**: Xcode MCP permission issues (#12108) and dynamic header refresh (#7318) reflect deep MCP integration needs
4. **Customizability**: Event Hooks (#2109) leads by a wide margin at 426 👍; developers want to weave Codex into custom workflows

### 💡 Ecosystem Signals

- **Claude migration**: PR #12392 is implementing automatic Claude configuration migration, accelerating conversion of competing tools' users
- **Third-party tool integration**: token_count event exposure (#9660), notify payload extensions (#12622), and more show Codex becoming more observable and integrable

---

*This report is generated from public GitHub data and does not represent OpenAI's official position*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Report | 2026-02-24

## Today at a Glance

The Gemini CLI team shipped 6 releases in rapid succession today, including stable v0.29.7 and preview v0.30.0-preview.6, focusing on fixing the model quota access check. The community's top concerns are the **gemini-3.1-pro-preview model support request** (93 👍), plus Plan Mode-related core experience improvements such as tool visibility and context management.

---

## Version Releases

| Version | Type | Core updates |
|:---|:---|:---|
| **v0.29.7** | Stable | Fixed the quota access check, supporting all preview models (not only 3.0) |
| **v0.30.0-preview.6** | Preview | Same as above, a patch release based on preview.5 |
| **v0.30.0-nightly.20260224** | Nightly | Refactored session conversion logic into the core layer; fixed manual model selection not persisting across restarts |

> Key fix: users with only Gemini 3.1 preview model access were previously downgraded to Gemini 2.5 by mistake; this is now resolved. [#19867](https://github.com/google-gemini/gemini-cli/pull/19867)

---

## Community Hotspot Issues

| # | Title | Importance | Community response |
|:---|:---|:---|:---|
| [#19532](https://github.com/google-gemini/gemini-cli/issues/19532) | **Add gemini-3.1-pro-preview support** | ⭐ P1 | **93 👍, 104 comments** — today's hottest request; users are eager to use the latest model |
| [#20076](https://github.com/google-gemini/gemini-cli/issues/20076) | Centralize Plan Mode tool visibility logic | 🔧 Architecture | Resolves the inconsistency between the hardcoded tool list and the policy engine, affecting enterprise-grade extension |
| [#20103](https://github.com/google-gemini/gemini-cli/issues/20103) | Inject tool calls when the user manually exits Plan Mode | 🐛 Bug | The model gets confused by manual exits; interaction state synchronization needs fixing |
| [#20058](https://github.com/google-gemini/gemini-cli/issues/20058) | Policy engine support for headless mode | ⭐ P1 | A must-have for enterprise users; blocks the deprecation of old settings |
| [#19561](https://github.com/google-gemini/gemini-cli/issues/19561) | "Tactful Extraction" precise code reading | 🚀 Performance | Reduces context bloat (targeting a drop from +15k tokens/turn), improving large-file handling efficiency |
| [#19520](https://github.com/google-gemini/gemini-cli/issues/19520) | Smart output handling for high-volume commands | 🚀 Performance | Fixes hang/loop detection issues caused by large-output commands like `grep` |
| [#19454](https://github.com/google-gemini/gemini-cli/issues/19454) | Plan Mode automatic model switching | 🤖 AI | Pro for the planning phase, Flash for the implementation phase, optimizing cost and speed |
| [#18494](https://github.com/google-gemini/gemini-cli/issues/18494) | Diagnostics tooling infrastructure | 🔧 Architecture | Long-standing technical debt addressing the difficulty of debugging agent behavior |
| [#19519](https://github.com/google-gemini/gemini-cli/issues/19519) | Long-running commands falsely triggering loop detection | 🐛 Bug | Affects heavy task execution; needs to distinguish "slow" from "infinite loop" |
| [#18896](https://github.com/google-gemini/gemini-cli/issues/18896) | Screen flicker when scrolling on Windows | 🐛 Bug | 3 comments; a rendering issue commonly hit by Windows users |

---

## Notable PR Progress

| # | Title | Status | What it does/fixes |
|:---|:---|:---|:---|
| [#20116](https://github.com/google-gemini/gemini-cli/pull/20116) | Dynamic policy-driven tool evaluation for Plan Mode | 🟢 Open | **Core fix**: moves hardcoded tool filtering into the policy engine, supporting `conductor.toml` customization |
| [#20108](https://github.com/google-gemini/gemini-cli/pull/20108) | Fix fatal crash caused by loop detection | 🟢 Open | Resolves Node.js process termination caused by a synchronous `AbortError` race condition |
| [#19982](https://github.com/google-gemini/gemini-cli/pull/19982) | Agent/AgentSession v1 and the ReAct loop | 🟢 Open | **Architecture upgrade**: introduces a stateful ReAct interface with event streams, designed for SDK scenarios |
| [#20099](https://github.com/google-gemini/gemini-cli/pull/20099) | Settings refactor toward noun-first naming and positive logic | 🟢 Open | UX consistency improvements, e.g. `disable-auto-accept` → `auto-accept-edits` |
| [#20100](https://github.com/google-gemini/gemini-cli/pull/20100) | Quota wording inversion: "remaining %" → "used %" | 🟢 Open | Aligns with industry conventions such as Claude Code |
| [#20121](https://github.com/google-gemini/gemini-cli/pull/20121) | MCPOAuthProvider OAuth implementation | 🟢 Open | Standard MCP SDK OAuth client support |
| [#20001](https://github.com/google-gemini/gemini-cli/pull/20001) | Redact API keys in proxy URLs from telemetry logs | 🟢 Open | Security hardening: prevents credential leaks in the `http://key@proxy` form |
| [#19920](https://github.com/google-gemini/gemini-cli/pull/19920) | Shared secret authentication for DevTools server endpoints | 🟢 Open | Security fix: WS/SSE endpoints were previously accessible to any local process |
| [#19806](https://github.com/google-gemini/gemini-cli/pull/19806) | Skill creation `--local` rapid iteration flag | 🟢 Open | Developer experience: writes directly to `.gemini/skills/` without packaging |
| [#20042](https://github.com/google-gemini/gemini-cli/pull/20042) | Fix styled table width calculation | 🟢 Open | Long-standing UI issue: Markdown styling characters caused column misalignment |

---

## Feature Request Trends

Analysis of 50 active issues shows the community's focus distributed as follows:

```
🎯 Plan Mode ecosystem polish ████████████████████  28%  (tool visibility, model switching, hook mechanism)
🤖 New model support ██████████████       20%  (strong demand for 3.1 Pro Preview)
⚡ Performance and context optimization ████████████         16%  (token efficiency, large files, output handling)
🔒 Enterprise/security features ██████████           14%  (policy engine, headless, authentication)
🛠️ Developer toolchain ████████             12%  (diagnostics, debugging, DevTools)
🖥️ Cross-platform experience ██████                8%  (Windows rendering, WSL, IDE integration)
```

**Emerging trend**: MCP (Model Context Protocol) ecosystem integration is accelerating, with multiple issues/PRs around MCP tool annotations, OAuth, and progress display.

---

## Developer Concerns

| Pain point category | Specific feedback | Related issues |
|:---|:---|:---|
| **Model availability** | "I have 3.1 access but got downgraded to 2.5" — the permission detection logic is opaque | [#19532](https://github.com/google-gemini/gemini-cli/issues/19532) |
| **Plan Mode cognitive burden** | The model insists on entering Plan Mode too aggressively, even for simple tasks; state gets messy after manual exits | [#19312](https://github.com/google-gemini/gemini-cli/issues/19312), [#20103](https://github.com/google-gemini/gemini-cli/issues/20103) |
| **Context explosion** | Reading large files injects +15k tokens at once; a smarter tiered reading strategy is needed | [#19561](https://github.com/google-gemini/gemini-cli/issues/19561) |
| **Headless/CI scenarios** | No policy engine support and loop detection killing long tasks hinder automated deployment | [#20058](https://github.com/google-gemini/gemini-cli/issues/20058), [#19519](https://github.com/google-gemini/gemini-cli/issues/19519) |
| **Debugging black box** | Agent behavior is hard to reproduce and diagnose; structured logging and DevTools are urgently needed | [#18494](https://github.com/google-gemini/gemini-cli/issues/18494) |

---

*This report is generated from public GitHub data and is for reference only. For complete information, visit [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Report | 2026-02-24

## Today at a Glance

Community activity was steady today. The core focus is the fix for **MCP debug logs polluting the console** (Issue #1214 + PR #1215), plus **Nix dev environment support** and **Fish-style keyboard shortcut** experience improvements contributed by two developers. No new release.

---

## Community Hotspot Issues

| # | Title | Author | Core problem | Importance |
|---|------|------|---------|--------|
| [#1214](https://github.com/MoonshotAI/kimi-cli/issues/1214) | Verbose MCP debug messages printed to console when starting with -C flag and OAuth MCP servers | @mingdaoai | When resuming a session with `-C`, debug logs from OAuth MCP servers (e.g., Todoist) print directly to the console, disrupting the user experience | 🔴 **High** — affects the daily interaction experience; a companion fix PR already exists |

> Note: only 1 issue update today, reflecting the community entering stable maintenance.

---

## Notable PR Progress

| # | Title | Author | Type | What it does/fixes |
|---|------|------|------|--------------|
| [#1215](https://github.com/MoonshotAI/kimi-cli/pull/1215) | fix: redirect stderr before MCP loading | @mingdaoai | 🐛 Bugfix | **Key fix**: moves the `redirect_stderr` call earlier, before MCP server loading, so `mcp-remote` OAuth debug messages (like `[16850] Using existing...`) are redirected to a log file instead of polluting the console. Directly resolves Issue #1214 |
| [#1213](https://github.com/MoonshotAI/kimi-cli/pull/1213) | feat: add nix devShell support | @jetjinser | ✨ Feature | Adds Nix dev environment support, providing a reproducible build environment and lowering the contribution barrier for Nix users |
| [#1212](https://github.com/MoonshotAI/kimi-cli/pull/1212) | feat(shell): add fish-style `Ctrl-L` to clear screen preserving scrollback | @jetjinser | ✨ Feature | Implements Fish shell-style `Ctrl+L` screen clearing: clears the visible area while preserving scrollback history, improving the terminal interaction experience |

---

## Feature Request Trends

Based on recent community activity, current focus areas:

| Trend direction | Notes |
|---------|------|
| **MCP ecosystem polish** | Integration experience improvements for OAuth-based MCP servers (logging, auth flows) |
| **Developer experience (DX)** | Terminal shortcut enhancements (Fish/Zsh style), dev environment standardization (Nix) |
| **Logging and debugging** | Separate user-visible output from internal debug messages to avoid information overload |

---

## Developer Concerns

| Pain point/need | Specific manifestation |
|----------|---------|
| **Console output pollution** | Low-level debug messages from MCP libraries interrupt user workflows; the timing of stderr redirection must be strictly separated |
| **Cross-platform dev environments** | Calls for Nix support reflect demand for declarative, reproducible build environments |
| **Terminal habit migration** | Fish/Zsh users expect familiar shortcut behavior (e.g., `Ctrl+L` preserving history) |

---

*Data source: [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) | Statistics window: 2026-02-23 to 2026-02-24*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Report | 2026-02-24

## Today at a Glance

The OpenCode community was extremely active today, with **Web UI consistency fixes** in the spotlight as multiple PRs iterated quickly on experience issues such as configuration syncing and state cleanup. Meanwhile, improvement proposals for **session lifecycle management** and the **context compaction mechanism** kept landing, reflecting the community's urgent need for long-session stability.

---

## Version Releases

No new release.

---

## Community Hotspot Issues (Top 10)

| # | Issue | Importance | Community response |
|---|-------|--------|---------|
| [#14864](https://github.com/anomalyco/opencode/issues/14864) | Web UI does not honor the `tui.diff_style` configuration | 🔥 High | Configuration consistency is central to the cross-platform experience; a fix PR has been submitted |
| [#14863](https://github.com/anomalyco/opencode/issues/14863) | Native hooks support: session lifecycle events | 🔥 High | A key feature to match Claude Code, essential for enterprise automation scenarios |
| [#14862](https://github.com/anomalyco/opencode/issues/14862) | Big Pickle ignores AGENTS.md instructions, causing code pollution | 🔥 High | A severe reliability issue undermining trust in production environments |
| [#14509](https://github.com/anomalyco/opencode/issues/14509) | Gemini fails all requests due to the `anyOf` schema | 🔥 High | Ongoing for 3 days, 6 comments; Gemini users completely blocked |
| [#8097](https://github.com/anomalyco/opencode/issues/8097) | Interactive terminal input support (sudo/passwords etc.) | 🔥 High | 8 comments, 👍3, a core pain point for infrastructure deployment scenarios |
| [#12687](https://github.com/anomalyco/opencode/issues/12687) | Severe memory leak causing macOS kernel crashes | 🔥 High | 11 comments, a performance crisis; inevitably triggered by extended use |
| [#14848](https://github.com/anomalyco/opencode/issues/14848) | Billing sync delays + TUI session loss | 🔥 High | Paid users' experience harmed; a trust crisis |
| [#5971](https://github.com/anomalyco/opencode/issues/5971) | Plugin API: custom sidebar panels | 🔥 High | 👍16, 5 comments, key infrastructure for ecosystem expansion |
| [#13838](https://github.com/anomalyco/opencode/issues/13838) | Compaction injects fake user messages, causing unexpected summaries | Medium | 3 comments, 👍2, affects the session recovery experience |
| [#13669](https://github.com/anomalyco/opencode/issues/13669) | ReadTool fully loading large files causes RSS bloat | Medium | 4 comments, clear room for performance optimization |

---

## Notable PR Progress (Top 10)

| # | PR | Type | Core content |
|---|-----|------|---------|
| [#14865](https://github.com/anomalyco/opencode/pull/14865) | Web UI honors the `tui.diff_style` configuration | 🐛 Fix | Unifies diff view behavior between TUI and Web UI, resolving #14864 |
| [#14741](https://github.com/anomalyco/opencode/pull/14741) | Add `stream.delta` / `stream.aborted` hooks | ✨ Feature | Real-time stream observation for plugins, laying the groundwork for the hooks system in #14863 |
| [#14861](https://github.com/anomalyco/opencode/pull/14861) | Clean up the changes view after deleting all sessions | 🐛 Fix | Resolves leftover state issues, complementing #14860 |
| [#14859](https://github.com/anomalyco/opencode/pull/14859) | Sidebar adds plugin/formatter panels | ✨ Feature | Resolves #13622 and #9314, plus a status dialog overflow fix |
| [#14832](https://github.com/anomalyco/opencode/pull/14832) | WriteTool force-converts JSON objects to strings | 🐛 Fix | Resolves edit tool failures for quantized models like qwen3-coder (#6918) |
| [#14855](https://github.com/anomalyco/opencode/pull/14855) | Add Stylua Lua formatting support | ✨ Feature | Rounds out Neovim/Lua ecosystem support, closes #14817 |
| [#14846](https://github.com/anomalyco/opencode/pull/14846) | Compaction preserves original user prompts | ✨ Feature | Resolves #3031 and #13838, improving session recovery context |
| [#14845](https://github.com/anomalyco/opencode/pull/14845) | Double-tap Esc to confirm canceling AI responses | ✨ Feature | An accidental-trigger guard, closes #14844 |
| [#14851](https://github.com/anomalyco/opencode/pull/14851) | WriteTool sensitive file permission fix | 🐛 Fix | Sets 0o644 permissions, closes #14853 |
| [#14743](https://github.com/anomalyco/opencode/pull/14743) | Anthropic cache hit rate optimization | 🐛 Fix | System prompt splitting + tool stability, resolving #5416 and #5224 |

---

## Feature Request Trends

Four core directions distilled from today's 50 issues:

| Direction | Representative issues | Heat |
|------|-----------|------|
| **Deep IDE/editor integration** | #14856 (working directory detection), #7769 (Git submodules) | 🔥🔥🔥 |
| **Session lifecycle management** | #14863 (hooks), #13838 (compaction experience), #14848 (session loss) | 🔥🔥🔥 |
| **Performance and resource optimization** | #12687 (memory leak), #13669 (ReadTool optimization), #14065 (cache hit rate) | 🔥🔥🔥 |
| **Enterprise/compliance scenarios** | #8097 (interactive input), #4959 (model fetching disabled in proxy environments), #14853 (file permissions) | 🔥🔥 |

---

## Developer Concerns

### 🔴 High-frequency Pain Points
1. **Cross-platform consistency breakdown** — Web UI and TUI configurations out of sync (#14864), Windows path handling (#14742 series)
2. **Long-session stability** — memory leaks causing system crashes (#12687), context overflow killing sessions (#14824), billing sync delays (#14848)
3. **Model compatibility** — the Gemini schema issue (#14509), qwen3-coder tool call failures (#6918)

### 🟡 Ecosystem Expansion Demands
- **Plugin system deepening**: the sidebar API (#5971, 👍16) and hooks mechanism (#14863) are key infrastructure for ecosystem building
- **Formatter/LSP coverage**: language support keeps filling in with Stylua (#14817), ruff/ty (#14850), and more

### 🟢 Experience Improvements
- **Accidental-trigger protection**: Esc cancel confirmation (#14845), cursor positioning on multi-line paste (#14840)
- **Visual controllability**: theme hot reload (#14847), widescreen mode (#14835), font size settings taking effect (#14823)

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Report | 2026-02-24

## Today at a Glance

Qwen Code released v0.10.5-nightly today, focusing on fixing release workflow standardization issues. Community activity was fairly high, with 14 issue and 13 PR updates, centered on three major themes: **VS Code sidebar interaction experience**, **model configuration flexibility**, and **Windows environment compatibility**.

---

## Version Releases

### v0.10.5-nightly.20260224.a13d88ac
- **Version bump**: routine version bump to 0.10.5
- **Workflow fix**: standardized the Release Notes generation process and added prerelease tag support (contributed by @Mingholy)

[View the full changelog](https://github.com/QwenLM/qwen-code/releases/tag/v0.10.5-nightly.20260224.a13d88ac)

---

## Community Hotspot Issues (10)

| # | Title | Type | Key takeaways |
|---|------|------|---------|
| [#1919](https://github.com/QwenLM/qwen-code/issues/1919) | API Error: 401 invalid access token or token expired | 🐛 Bug | **High-frequency authentication failure**: users hit 401 errors when using OpenAI-compatible APIs (Alibaba Cloud Bailian), affecting basic availability |
| [#1918](https://github.com/QwenLM/qwen-code/issues/1918) | Support more retry scenarios | ⭐ Feature | **Stability enhancement**: no retry mechanism when the model service errors in YOLO mode; @wenshao suggests adding smart retry strategies |
| [#1898](https://github.com/QwenLM/qwen-code/issues/1898) | `contextWindowSize` not respected? | 🐛 Bug | **Configuration override issue**: users who explicitly set a 256k context window still get truncated; involves local vLLM deployment scenarios |
| [#1910](https://github.com/QwenLM/qwen-code/issues/1910) | Agent lacks built-in knowledge of its own config system | 🐛 Bug | **Meta-capability gap**: the agent cannot understand the schema and syntax of its own configuration system, forcing users to consult the source code manually |
| [#1889](https://github.com/QwenLM/qwen-code/issues/1889) | /init doesnt work in Mac | 🐛 Bug | **Cross-platform compatibility**: the `/init` command fails on Mac with ListFiles tool errors |
| [#1916](https://github.com/QwenLM/qwen-code/issues/1916) | VS Code chat button hard to find (feedback from a Russian-speaking user) | ⭐ Feature | **UX onboarding barrier**: international users report the VS Code extension's chat entry point is not intuitive enough |
| [#1870](https://github.com/QwenLM/qwen-code/issues/1870) | Missing Option to Open Qwen Chat in Primary or Secondary Sidebar | ⭐ Feature | **Layout flexibility**: users strongly want to move the chat panel to the primary/secondary sidebar (echoing #1308) |
| [#1308](https://github.com/QwenLM/qwen-code/issues/1308) | Move Qwen Code window to Activity Bar / Secondary Side Bar | ⭐ Feature | **Long-standing highly-upvoted request** (5 👍): Activity Bar integration for the VS Code extension, improving workflow efficiency |
| [#1917](https://github.com/QwenLM/qwen-code/issues/1917) | Add a modular Phrase Pack System for Loading Messages | ⭐ Feature | **Personalized experience**: a user has already built a local "loading phrase pack" system that allows custom witty loading copy |
| [#1883](https://github.com/QwenLM/qwen-code/issues/1883) | Where do I report security issues | 🔒 Security | **Security response process**: the security issue reporting link is dead and the entry point to the Alibaba Cloud vulnerability platform is unclear |

---

## Notable PR Progress (10)

| # | Title | Status | Technical value |
|---|------|------|---------|
| [#1907](https://github.com/QwenLM/qwen-code/pull/1907) | Alibaba Cloud Bailian Coding Plan supports third-party models (glm-4.7, kimi-k2.5, qwen3-coder-next) | ✅ Merged | **Ecosystem expansion**: responding to #1903, the Bailian platform adds Zhipu, Moonshot, and in-house model support, including thinking mode |
| [#1874](https://github.com/QwenLM/qwen-code/pull/1874) | runner supports auth_type model configuration | ✅ Merged | **Authentication flexibility**: the ModelSpec data structure is extended to support per-model authentication types |
| [#1877](https://github.com/QwenLM/qwen-code/pull/1877) | Install script permission checks and sudo detection (Arch Linux support) | 🔄 Open | **Cross-platform installation**: hardens install-qwen-with-source.sh to prevent damage to system directories |
| [#1912](https://github.com/QwenLM/qwen-code/pull/1912) | Agent collaboration arena: multi-model competitive execution | 🔄 Open | **Innovative experiment**: runs multiple models in parallel isolated by git worktrees, supporting result comparison and merging the best solution |
| [#1911](https://github.com/QwenLM/qwen-code/pull/1911) | Fix contextWindowSize priority override issue | 🔄 Open | **Configuration consistency**: preserves user-defined values when the provider does not set them explicitly |
| [#1904](https://github.com/QwenLM/qwen-code/pull/1904) | Normalize Windows PATH-like environment variable keys | 🔄 Open | **Windows compatibility**: resolves command resolution ambiguity caused by `Path`/`PATH` case coexistence |
| [#1858](https://github.com/QwenLM/qwen-code/pull/1858) | Remove redundant non-null assertions, extract timeout constants | ✅ Merged | **Code quality**: TypeScript convention cleanup for the AcpConnection class |
| [#1857](https://github.com/QwenLM/qwen-code/pull/1857) | Improve BOM detection: length checks and codePointAt | ✅ Merged | **Unicode safety**: edge case handling in AcpFileSystemService |
| [#1847](https://github.com/QwenLM/qwen-code/pull/1847) | .gitignore excludes .qwen/commands/ and .qwen/skills/ | ✅ Merged | **Custom workflows**: keeps user-defined commands and skills out of version control |
| [#1836](https://github.com/QwenLM/qwen-code/pull/1836) | OpenAI-compatible API media type support | ✅ Merged | **Multimodal compatibility**: based on a capability declaration system, avoiding 400 errors from unsupported media types |

> Note: #1913-#1915 are devcontainer-related test PRs from the same user, closed and not listed.

---

## Feature Request Trends

Analysis of today's issues shows four major community focus areas:

| Trend direction | Representative issues | Heat |
|---------|-----------|------|
| **VS Code extension layout freedom** | #1308, #1870, #1916 | 🔥🔥🔥 High |
| Users strongly want the chat panel to be draggable to the Activity Bar / secondary sidebar, matching the experience of competitors like Cursor/Copilot |
| **Fine-grained model configuration** | #1898, #1911, #1918, #422 | 🔥🔥🔥 High |
| Production-grade needs such as contextWindowSize enforcement logic, fallback model switching, and retry strategies |
| **Agent self-awareness** | #1910 | 🔥🔥 Medium |
| Agents need built-in knowledge of their own configuration system's schema to reduce user learning costs |
| **Windows environment improvements** | #1724, #1904, #1919 | 🔥🔥 Medium |
| Ongoing fixes for Windows-specific issues such as process termination, environment variables, and path handling |

---

## Developer Concerns

### 🔴 High-frequency Pain Points
1. **Opaque configuration enforcement**: parameters like `contextWindowSize` feel "set but ignored"; in fact provider values override user values (#1898 → fix in progress in #1911)
2. **Poor VS Code entry discoverability**: both new and veteran users report being unable to find the chat button, especially international users (#1916)
3. **Broken security response channel**: the official security report entry link has expired, hindering responsible vulnerability disclosure (#1883)

### 🟡 Experience Improvement Requests
- **CLI history management**: lacks a `/delete` or cleanup command, so sessions pile up (#1902)
- **Loading state personalization**: a community user has already built a "phrase pack" system; the official project could consider adopting it (#1917)

### 🟢 Ecosystem Building Signals
- **Multi-model arena**: the Agent Arena design in #1912 shows the community evolving toward "model-as-a-service" comparative evaluation
- **Third-party model onboarding**: the Bailian platform quickly onboarded Zhipu/Moonshot, reflecting Alibaba Cloud's open ecosystem strategy

---

*This report is generated from public GitHub data and does not represent any official position*

</details>

---
*This report was automatically generated by [agents-radar](https://github.com/duanyytop/agents-radar).*