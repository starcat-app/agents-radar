# AI CLI Tools Community Digest 2026-10-31

> Generated: 2026-10-31 00:15 UTC | Tools covered: 7

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/earendil-works/pi)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report — AI CLI Ecosystem (2026-10-31)

## 1. Ecosystem Overview

The 2026-10-31 digests show a market that has moved from basic code generation toward **production hardening**: permissions, sandboxing, session durability, plugin/MCP reliability, and platform parity. Vendor-backed tools—Claude Code, OpenAI Codex, Gemini CLI, and GitHub Copilot CLI—are investing in enterprise controls, desktop/web integration, and agent orchestration, while community/open-source tools—OpenCode, Pi, and Qwen Code—iterate quickly on provider breadth, extensibility, diagnostics, and remote/headless use. Release cadence is uneven: OpenCode shipped three releases in 24 hours, Claude Code and Gemini shipped one, and Codex, Copilot CLI, and Pi shipped none, yet issue traffic remained high across the board. The dominant friction is no longer model quality but **reliability at boundaries**: Windows/WSL behavior, MCP/plugin lifecycle, auth/quota clarity, context/cost management, and trustworthy agent status. Integration surfaces such as `app-server`, ACP, hooks, plugin manifests, and session stores are becoming the real ecosystem battleground.

---

## 2. Activity Comparison

Counts are for updates in the last 24 hours as disclosed by each digest. **N/D** = total not disclosed; digest lists only selected/highlighted items. **N/A** = no discussion activity/data provided or not a primary channel in the digest—not evidence of inactivity.

| Tool | Issues updated | PRs updated | Discussions | Release status |
|---|---:|---:|---:|---|
| **Claude Code** | N/D | 0 | N/A | 1 stable release: v2.1.314 |
| **OpenAI Codex** | 43 | 50 | N/D | None |
| **Gemini CLI** | N/D | N/D | N/A | 1 nightly: v0.67.0-nightly.20261030 |
| **GitHub Copilot CLI** | 33 | 2 | N/A | None |
| **OpenCode** | N/D | N/D | N/A | 3 stable releases: v2.2.5, v2.2.4, v2.2.3 |
| **Pi** | 36 | 20 | 2 | None |
| **Qwen Code** | 4 | 50 | N/A | 1 driver release: `cua-driver-rs v0.27.0` |

**Data caveats:** Codex’s 50 PRs were all bot-authored and closed; Qwen’s 50 PRs include a large autofix/bot queue. Raw PR counts therefore measure automation/landing cadence more than community review volume.

---

## 3. Shared Feature Directions

| Direction | Communities | Specific needs |
|---|---|---|
| **Permissioned execution and sandboxing** | Claude Code, Codex, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | Write boundaries outside working directories; OS-level sandboxing; repo-level allow/ask/deny policy; explicit approval recovery; fewer spurious permission prompts. Examples: Claude v2.1.314 write boundary, Gemini #19873 OS sandboxing, Copilot #5297 repo-level permissions, OpenCode #2242 sandboxing. |
| **Windows/WSL and terminal parity** | Claude Code, Codex, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | Native Windows packaging; WSL2 CPU/sleep behavior; terminal capability negotiation; no visible `cmd.exe` storms; scrollable long output; Wayland/mintty correctness. Examples: Codex Windows Desktop issues, Copilot #3700/#5304, Pi #10256/#11592, Qwen #15949. |
| **Session portability and continuity** | Claude Code, Codex, Gemini CLI, OpenCode, Pi, Qwen Code | Cross-surface resume/share; cross-backend switching; thread handoff between accounts; remote `serve` access; documented resume-directory semantics. Examples: Claude #15881, Codex #58457/#22356, Qwen #15887. |
| **Agent orchestration reliability** | Claude Code, Codex, Gemini CLI, Copilot CLI, OpenCode, Pi | Trustworthy termination reasons; background subagent control; retry/backoff; queued input after interrupt; no false “success” on truncation. Examples: Gemini #22323, Claude #105928, Codex #58421, OpenCode #59758. |
| **MCP/plugin/extensibility correctness** | Claude Code, Codex, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | MCP reconnect/backoff; plugin auth lifecycle; schema validation that degrades gracefully; permission UI naming tool/input; extension reload safety. Examples: Claude #106087, OpenCode #60583, Copilot #1996, Gemini #24246. |
| **Observability and diagnostics** | Codex, Claude Code, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | Visible command execution; running/finished indicators; explicit LSP/tool errors; credential redaction; doctor commands; actionable quota/auth errors. Examples: Codex #37213, OpenCode #60750/#60748, Qwen #15946. |
| **Context, cost, and quota management** | Codex, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | Rate-limit header preservation; cache-aware compaction; token accounting; AST-aware context; quota reset visibility. Examples: Codex #58413, Copilot #4724/#5292, Qwen #15433. |
| **TUI/editor-grade ergonomics** | Codex, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | Undo/redo; remappable keybindings; long-output preview; transcript virtualization; terminal-width-safe rendering. Examples: Codex #2379, Pi #11598, OpenCode #60741, Qwen #15949. |

---

## 4. Differentiation Analysis

| Tool | Primary focus and target users | Technical approach / differentiators |
|---|---|---|
| **Claude Code** | Enterprise/team security, Claude ecosystem, cross-surface workflows | Permission modes, working-directory write boundaries, IdP-group-scoped gateway upstreams, connectors/MCP, Claude Code + Desktop + web continuity. Strongest on enterprise policy and identity controls. |
| **OpenAI Codex** | OpenAI/ChatGPT users, Windows Desktop, platform integrators | Rust-based CLI/app-server, fullscreen TUI, plugin/app settings, Guardian context budgeting, computer-use, bot-driven high PR throughput. Strong desktop and app-server integration story. |
| **Gemini CLI** | Gemini/Vertex developers, CLI-first agent workflows | Nightly cadence, subagents/skills, AST-aware tooling proposals, OS-sandboxing design, large MCP/tool-set handling. Strong on Google-native context efficiency and agent orchestration experiments. |
| **GitHub Copilot CLI** | GitHub teams, CI/automation, Copilot SDK/headless clients | Containerized server image, ACP/headless integration, hooks, plugin marketplace, repo-level permission policy. Strong GitHub-centric automation and packaging direction. |
| **OpenCode** | Multi-provider individual developers, self-hosted/cost-sensitive users | Client/server architecture, desktop terminals, worktrees, MCP/ACP support, Claude Agent integration, fast release cadence, diagnostics/log redaction. Strong open, multi-model positioning. |
| **Pi** | Provider-agnostic terminal power users and wrapper/package-manager users | Coding-agent + durable runtime, extension hooks, virtual-model routing, self-update contracts, broad provider matrix, terminal correctness. Strong on extensibility and non-npm installation ownership. |
| **Qwen Code** | Qwen ecosystem, managed agents, enterprise/computer-use deployments | Managed Agent, remote `qwen serve`, CUA driver binaries, LSP readiness, shell permission checks, autofix/CI automation. Strong on managed-agent reliability and computer-use infrastructure. |

---

## 5. Community Momentum & Maturity

**Raw activity:** Codex (43 issues / 50 PRs), Pi (36 / 20 / 2 discussions), and Copilot CLI (33 issues / 2 PRs) had the highest disclosed issue/PR traffic. Codex’s PR volume is bot-authored, so it signals automated landing cadence rather than open community review. Qwen’s 50 PRs are similarly automation-heavy and include an `autofix/needs-human` backlog.

**Release velocity:** OpenCode is the fastest shipper in the window with three releases in 24 hours, followed by Claude Code, Gemini CLI, and Qwen’s CUA driver. Codex, Copilot CLI, and Pi shipped no releases but remained active on fixes and issue triage.

**Community engagement:** The strongest single signals were Claude Code #27302 (291 comments / 441 👍), OpenCode #59387 (147 comments) and #2242 (106 comments / 81 👍), Pi #7547 (93 comments), and Codex #37213 (40 👍). These indicate durable demand around account multiplexing, sandboxing, Windows usability, and command visibility.

**Maturity read:** Claude Code, Codex, Copilot CLI, and Gemini CLI are vendor-backed and furthest along on enterprise controls, but still show platform regressions and opaque failure modes. OpenCode, Pi, and Qwen Code are iterating faster and closer to community feedback, with more visible rough edges: OpenCode’s quota/billing threads, Pi’s Windows/WSL issues, and Qwen’s CI/triage load. Codex shows high automation maturity but Windows Desktop remains its top reliability funnel. Copilot’s container-image work is strategically important but currently stalled in review.

---

## 6. Trend Signals

1. **Security is becoming a product surface, not a config detail.** Path boundaries, OS sandboxing, repo-level permissions, IdP scoping, and auditability appear across Claude Code, Gemini, Copilot, OpenCode, and Qwen. Developers building on these tools should expose workspace-scoped policy and clear approval recovery.

2. **Trustworthy agent state is a differentiator.** False `GOAL` success on turn limits, invisible command execution, silent LSP empties, and missing diagnostics are recurring complaints. Structured events, explicit termination reasons, health checks, and redacted logs will matter more than marginal model gains.

3. **MCP/plugin lifecycle is the new integration risk.** Reconnect storms, plugin auth gaps, strict schema rejection, missing custom tools, and permission prompts that do not name the tool/input are common. Build for graceful degradation, backoff, and observable plugin state.

4. **Platform parity remains unsolved.** Windows Desktop, WSL2, mintty/ConPTY, Wayland, and path/registry virtualization generate a disproportionate share of high-severity issues. Containerized distribution and terminal-capability negotiation are practical mitigations.

5. **Sessions must become portable and remote-ready.** Cross-backend resume, thread handoff, CLI/Desktop sharing, remote `serve`, and host-inherited instructions all point to sessions as first-class, transferable artifacts. Stable `app-server`/ACP contracts will be key integration points.

6. **Cost and context observability is rising.** Rate-limit headers, cache-write token accounting, TTL-aware compaction, and quota-reset visibility are now feature requests, not edge cases. Expect users to demand predictable context economics.

7. **TUI quality is a retention factor.** Undo/redo, keybinding consistency, long-output previews, transcript virtualization, and scroll/copy behavior are repeatedly requested. The terminal is being treated as an editor, not a prompt box.

8. **Automation needs human review gates.** Bot-generated PRs are outpacing review in Qwen and dominating Codex’s landing cadence. Teams adopting agent-generated fixes should invest in triage, attribution, and review hygiene to avoid queue stagnation.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

**Data note:** The PR feed reports comment counts as `undefined`. Because the feed states it is sorted by comments, I use feed order as the ranking proxy. All listed PRs are **OPEN** as of 2026-10-31.

## 1) Top Skills Ranking

| Rank | Skill / PR | What it does | Attention / discussion highlight | Status |
|---:|---|---|---|---|
| 1 | [mcp-builder #1742](https://github.com/anthropics/skills/pull/1742) | Maintains the MCP server-building Skill | Fixes `mcp>=2` compatibility: `streamablehttp_client` → `streamable_http_client`, plus custom-header configuration via `create_mcp_http_client` / `http_client`. Linked to #1668. | OPEN |
| 2 | [skill-creator #1298](https://github.com/anthropics/skills/pull/1298) | Skill trigger evaluation and optimization | Addresses false misses/invalid scores: competing worker probes, Windows `select()` failures, and runtime failures being misclassified as non-triggers. | OPEN |
| 3 | [notion-spec-to-implementation + quantitative-resume-auditor #1245](https://github.com/anthropics/skills/pull/1245) | Two new Skills: Notion spec-to-task planning; quantitative resume auditing | Broad two-Skill submission. Notion Skill decomposes specs into implementation tasks with acceptance criteria and progress tracking. | OPEN |
| 4 | [proofcore-contract-auditor #1771](https://github.com/anthropics/skills/pull/1771) | Smart-contract static analysis and audit-proof notarization | Web3-focused Skill: analyzes Solidity/Rust contracts and anchors audit proofs on TON via a zero-storage Merkle protocol. High-scope/security-sensitive proposal. | OPEN |
| 5 | [Detect orphaned DOCX comments #1734](https://github.com/anthropics/skills/pull/1734) | DOCX cleanup/validation | Title indicates detection of orphaned Word comments; PR summary is blank, so review likely depends on implementation details. | OPEN |
| 6 | [md2video-audio #1703](https://github.com/anthropics/skills/pull/1703) | Markdown-to-MP4 video generation with voiceover | Compiles Markdown into slides via Marp and produces narrated MP4s. Review focus: zero-cost claim, media pipeline reliability, and output quality. | OPEN |
| 7 | [webapp-testing #1980](https://github.com/anthropics/skills/pull/1980) | Browser/web-app testing harness | Removes `subprocess.Popen(..., shell=True)` to mitigate command injection (CWE-78) while preserving `cd && command` support. Security-relevant. | OPEN |
| 8 | [docx timeout/output verification #1792](https://github.com/anthropics/skills/pull/1792) | DOCX revision acceptance workflow | Makes LibreOffice timeout return an error and verifies output no longer contains `w:ins` / `w:del` / move revision marks before claiming success. | OPEN |

## 2) Community Demand Trends

- **Trust, provenance, and namespace security** — [#492](https://github.com/anthropics/skills/issues/492) is the most-commented issue: community Skills distributed under the `anthropic/` namespace can impersonate official Skills and abuse trust boundaries. Demand is rising for provenance, verification, and permission warnings.
- **Org-wide sharing and distribution** — [#228](https://github.com/anthropics/skills/issues/228) asks for shared Skill libraries or direct sharing links instead of manual `.skill` file uploads through Slack/Teams.
- **Skill evaluation and trigger reliability** — [#556](https://github.com/anthropics/skills/issues/556) reports a 0% trigger rate in `run_eval.py`; [#202](https://github.com/anthropics/skills/issues/202) argues `skill-creator` should be more operational and token-efficient; [#2064](https://github.com/anthropics/skills/issues/2064) flags descriptions that explain *what* a Skill does but not *when* to use it.
- **Agent memory, context compression, and reasoning quality** — [#1329](https://github.com/anthropics/skills/issues/1329) proposes `compact-memory`; [#1385](https://github.com/anthropics/skills/issues/1385) proposes a reasoning quality-gate pipeline with calibration, adversarial review, and delivery verification.
- **Governance and safety patterns** — [#412](https://github.com/anthropics/skills/issues/412) proposed `agent-governance` for policy enforcement, threat detection, trust scoring, and audit trails. This overlaps strongly with the namespace-security concern in #492.
- **Packaging, document fidelity, and lifecycle resilience** — [#189](https://github.com/anthropics/skills/issues/189) reports duplicate Skills from overlapping plugins; [#2018](https://github.com/anthropics/skills/issues/2018) reports invalid DOCX XML; [#1868](https://github.com/anthropics/skills/issues/1868) reports a rendering bug; [#62](https://github.com/anthropics/skills/issues/62) reports disappearing Skills and errors.

## 3) High-Potential Pending Skills

- [mcp-builder #1742](https://github.com/anthropics/skills/pull/1742) — core compatibility fix for `mcp>=2`; likely high priority because it affects an official infrastructure Skill.
- [webapp-testing #1980](https://github.com/anthropics/skills/pull/1980) — security hardening against command injection; small, targeted, and issue-relevant.
- [skill-creator #1681](https://github.com/anthropics/skills/pull/1681) — enables direct execution of `package_skill.py` and updates stale usage paths; recent update on 2026-10-24.
- [pyxel #525](https://github.com/anthropics/skills/pull/525) — retro game development Skill with headless run/frame-inspection guidance; long-running but still updated on 2026-10-23.
- [skill-creator #1997](https://github.com/anthropics/skills/pull/1997) — fixes YAML frontmatter parsing so eval metadata matches `SKILL.md`; correctness-focused and likely reviewable.
- [pptx #1975](https://github.com/anthropics/skills/pull/1975) — rejects `--cols` below 1 up front instead of failing after LibreOffice render; latest update on 2026-10-27 and low-risk.
- [notion-spec-to-implementation + quantitative-resume-auditor #1245](https://github.com/anthropics/skills/pull/1245) — broader two-Skill submission; may need scope and quality review before landing.

Small issue-linked fixes [#1976](https://github.com/anthropics/skills/pull/1976) and [#1977](https://github.com/anthropics/skills/pull/1977) are also active and could merge quickly.

## 4) Skills Ecosystem Insight

**The community’s most concentrated demand is making Skills production-ready and trustworthy—secure provenance, reliable triggering/evaluation, correct packaging, and shareable team workflows—more than adding purely novel one-off Skills.**

---

# Claude Code Community Digest — 2026-10-31

## 1. Today's Highlights

Claude Code v2.1.314 shipped a meaningful permissions hardening: write-capable tools now refuse paths outside working directories in every permission mode, and gateway upstreams can optionally be scoped to IdP groups. Community attention remains dominated by long-running connector account management demand (#27302, 291 comments / 441 👍) and a cluster of MCP/plugin reliability regressions. No pull requests were updated in the last 24 hours.

## 2. Releases

### v2.1.314
- **Working-directory write boundary enforced globally** — `permissions.blockWritesOutsideWorkingDirectories` makes `Write`, `Edit`, and `NotebookEdit` refuse paths outside the working directories in every permission mode. This is a notable defense-in-depth change for users running agents in sensitive repositories.
- **IdP-group-scoped Claude apps gateway upstreams** — upstreams now accept an optional `groups` list, allowing only developers in specified identity-provider groups to be routed to the corresponding upstream. Useful for enterprise deployments with segmented access policies.

## 3. Hot Issues

1. **[#27302](https://github.com/anthropics/claude-code/issues/27302) — Support multiple Connector accounts for the same connector**  
   Open enhancement with by far the strongest community signal: 291 comments and 441 👍. Users need multiple accounts per connector in Claude and Claude Code on the web, a common requirement for work/personal separation and multi-tenant workflows. The age of the issue (created February 2026) and continued activity make it a persistent top request.

2. **[#66010](https://github.com/anthropics/claude-code/issues/66010) — Gmail MCP rewrites URLs with Google tracking URLs**  
   Privacy-focused bug reported since June 2026, still active with 23 comments. The MCP integration reportedly mutates Gmail URLs into Google tracking links, which matters for users handling sensitive mail content and for trust in MCP-mediated data paths.

3. **[#15881](https://github.com/anthropics/claude-code/issues/15881) — Seamless session sharing between Claude Code and Claude Desktop**  
   A long-standing cross-surface continuity request with 62 👍. Users currently rely on manual export/copy-paste to move context between CLI and Desktop, which breaks flow for mixed local/desktop workflows.

4. **[#106087](https://github.com/anthropics/claude-code/issues/106087) — Plugin cannot recover its own MCP server after startup failure**  
   Newly filed Windows/plugin bug: `$.mcp.connect` does not retry, and a 15-minute failure cache blocks new sessions. This is important for plugin authors because a transient startup failure can effectively disable a plugin for the whole session window with no self-recovery path.

5. **[#106037](https://github.com/anthropics/claude-code/issues/106037) — Scheduled tasks miss custom connector tools for the entire run**  
   Marked as a regression of #35899. Built-in connectors load, but custom connector tools only appear after a follow-up message. This directly affects automation and routine reliability on web/Windows.

6. **[#105928](https://github.com/anthropics/claude-code/issues/105928) — Background subagents wake parent on every monitor tick**  
   A background subagent waiting on its own Monitor/background shell sends repeated identical “Waiting.” notifications to the parent. This is an agent-orchestration noise issue that can degrade multi-agent sessions and inflate token/event churn.

7. **[#102096](https://github.com/anthropics/claude-code/issues/102096) — Workflow `agent()` silently removes the Agent tool from custom agent types**  
   Has reproduction and affects the official `claude-security` plugin. Silent capability removal is particularly damaging for plugin and agent authors because behavior diverges from declared configuration without an error.

8. **[#104548](https://github.com/anthropics/claude-code/issues/104548) — Desktop sidebar needs running vs. finished session indicator**  
   A small but high-signal UX request: the only running-session cue is a shimmer effect on the title. With multiple concurrent sessions, users cannot quickly distinguish active from completed work. 5 👍 on a relatively new issue.

9. **[#99059](https://github.com/anthropics/claude-code/issues/99059) — Windows MSIX registry writes silently virtualized**  
   The agent can confirm registry changes that never reach the real registry despite `desktop6:RegistryWriteVirtualization=disabled`. This is a serious correctness and trust issue for Windows desktop users performing system-level work.

10. **[#106017](https://github.com/anthropics/claude-code/issues/106017) — Cloud sessions fail GitHub clone auth despite green integration status**  
   Newly reported web/GitHub integration bug: the integration page shows the app installed and repository checks green, but cloud sessions still fail on `git clone`. This blocks cloud-based workflows and points to a mismatch between status reporting and actual credential availability.

## 4. Key PR Progress

No pull requests were updated in the last 24 hours. There is no PR activity to summarize for this digest.

## 5. Feature Request Trends

- **Identity and account multiplexing** — Multiple connector accounts (#27302) and in-place account email changes (#76624) reflect demand for better multi-identity support across personal, team, and organizational contexts.
- **Cross-surface session continuity** — Session sharing between Claude Code and Desktop (#15881), persistent multi-turn sessions (#90474), and session naming behavior across `/clear` and `/new` (#101699) all point to a desire for durable, portable context.
- **Desktop session observability** — Requests for clearer running/finished indicators (#104548) and focus-aware browser pane controls (#97937) show that multi-session desktop usage is stressing current UI affordances.
- **Local development permission ergonomics** — Auto-allowing loopback-resolving `*.test` domains (#92698) is a narrow but practical request to reduce friction in local browser-preview workflows.
- **Configurable rule scoping** — Task-scoped rule loading (#90381) would let teams apply rules by task type rather than only by file path, improving context efficiency.
- **Plugin and agent extensibility correctness** — Issues around MCP server recovery (#106087), silently removed Agent tools (#102096), and plugin auto-update failures (#73673) indicate that the plugin ecosystem is maturing faster than its failure-handling semantics.

## 6. Developer Pain Points

- **MCP reliability and transparency** — Several active issues concern silent data corruption or missing capabilities: dropped parameters after long values (#72228), Gmail URL rewriting (#66010), plugin MCP server recovery failure (#106087), and missing custom connector tools in scheduled runs (#106037).
- **Agent orchestration noise and drift** — Background subagent notifications (#105928) and multi-agent session orphaning/drift reports (#90264) show that multi-agent workflows remain fragile under concurrency.
- **Platform-specific packaging and desktop correctness** — Linux native binary segfaults (#90473, #90482), Windows MSIX registry virtualization (#99059), PowerShell `--` stripping in `claude mcp add` (#90439), and VS Code session deletion problems (#90466) create platform-specific support burden.
- **Permission and account friction** — Users continue to struggle with connector account limits (#27302), desktop connector “Always allow” settings being ignored (#106284), and permission behavior that differs across surfaces.
- **Stale-issue churn** — Many issues updated in the last 24 hours are closed as `stale`, `duplicate`, or `invalid`, suggesting that high-volume bug reporting is outpacing triage and that some regressions recur after prior fixes (#106037 explicitly references a regression of #35899).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-10-31

## 1. Today's Highlights
No new releases shipped in the last 24 hours, but the repo stayed highly active: 43 issues and 50 PRs were touched, with a large batch of bot-authored PRs landing around Guardian context budgeting, TUI session switching, and tool-call tracing. Windows Desktop remains the dominant source of pain — durable chat submission, plugin sync, disappearing projects, and VS Code extension startup all drew sustained attention. On the community side, the top-voted requests are still quality-of-life wins (undo/redo in the TUI, visible command execution), and third-party tooling around Codex sessions continues to proliferate.

## 2. Releases
Omitted — no releases in the last 24h.

## 3. Hot Issues

1. **[#50428](https://github.com/openai/codex/issues/50428)** — *Windows desktop: durable chat `turn/start` and `thread/fork` fail with `AbsolutePathBuf` deserialized without a base path* (38 comments, 👍3). The single most-discussed issue in the window. Windows Desktop can read a durable/cloud chat but cannot submit plain text or fork in the same directory — a hard blocker for durable-thread workflows, reproduced across two desktop builds.
2. **[#37213](https://github.com/openai/codex/issues/37213)** — *Codex Desktop no longer shows running commands* (12 comments, 👍40). The highest-reaction issue in the batch: command visibility vanished from the agent view, which users call a serious loss of trust/observability. Regression from build 26.730.61639 on Apple Silicon.
3. **[#2379](https://github.com/openai/codex/issues/2379)** — *Undo / redo typing in the TUI* (15 comments, 👍38). A year-old enhancement that keeps accruing votes: Cmd-Z / Shift-Cmd-Z in the composer. Signals that TUI editing ergonomics lag behind the feature surface.
4. **[#53898](https://github.com/openai/codex/issues/53898)** — *Cloud command execution fails during sandbox init with read-only filesystem* (12 comments, 👍4). `bwrap: Can't create file /home/agent/.codex/sessions` when using `sandbox_permissions="require_escalated"` — cloud sandbox bootstrapping is racing its own writable mounts.
5. **[#55869](https://github.com/openai/codex/issues/55869)** — *Windows: projects disappear after update while records remain in local SQLite* (8 comments). Data is intact but the sidebar won't render it — a state-migration/render regression that erodes confidence in local project storage.
6. **[#45121](https://github.com/openai/codex/issues/45121)** — *Windows computer-use helper freezes Voidtools Everything while reading large UI Automation lists* (7 comments). Cross-process interference: the computer-use helper's UIA enumeration blocks unrelated desktop tools. Notable as an early signal about computer-use blast radius on Windows.
7. **[#57344](https://github.com/openai/codex/issues/57344)** — *[Windows][VS Code] Codex v26.1021.22027 fails to start UI — v26.1007.21434 works* (6 comments, 👍6). Clean bisect-style report with a working downgrade; classic extension-host breakage that forces users to pin old versions.
8. **[#53016](https://github.com/openai/codex/issues/53016)** — *Dots: inconsistent computer names and no rename option in the Computers sidebar* (10 comments). Naming falls back to hostnames like `*-Mac-Mini.local` with no rename path — small, but it affects the multi-machine "dots" story.
9. **[#58413](https://github.com/openai/codex/issues/58413)** — *Usage-limit 429: `codex-family` rate-limit headers discarded when `x-codex-active-limit` names another limit* (3 comments). Fresh, technically precise: clients can't surface the correct limit state because error mapping drops headers. Matters for anyone building on `app-server`.
10. **[#58209](https://github.com/openai/codex/issues/58209)** — *Suspected cybersecurity false positive repeatedly blocks ordinary engineering work and leaves Goal stalled* (2 comments). A safety-check false positive that stalls a Goal entirely, with no described escape hatch — a recurring class of complaint.

*Also worth watching:* [#45479](https://github.com/openai/codex/issues/45479) (Windows viewport/auto-scroll, 8 comments), [#58421](https://github.com/openai/codex/issues/58421) (app-server queued input not drained after interrupt — closed), [#58306](https://github.com/openai/codex/issues/58306) (hidden follow-up questions on Deepin), [#58453](https://github.com/openai/codex/issues/58453) (97s latency for a one-line response).

## 4. Key PR Progress

All 50 PRs in the window were bot-authored (`copyberry[bot]`) and closed, indicating a fast landed-batch cadence rather than open review traffic.

1. **[#58457](https://github.com/openai/codex/pull/58457)** — *Enable cross-backend session switching in the TUI.* Selecting a conversation owned by another backend is now resumed through that backend instead of being rejected — removes a confusing dead end in the session picker.
2. **[#58410](https://github.com/openai/codex/pull/58410)** — *Enable deferred tool world state by default.* `deferred_tool_world_state` is now stable: deferred tool namespaces move into the developer `<tools>` context rather than the `tool_search` description.
3. **[#58454](https://github.com/openai/codex/pull/58454)** — *Elastic budgeting for Guardian context preparation.* Introduces `ContextBudgeting::Elastic`, removing fixed per-section caps so root conversation and Node REPL evidence can be allocated dynamically.
4. **[#58444](https://github.com/openai/codex/pull/58444)** — *Cap Guardian context entries before elastic allocation.* Companion guardrail: caps required/optional text before allocating whole entries, measuring rendered content including JSON escaping and framing.
5. **[#58456](https://github.com/openai/codex/pull/58456)** — *Preserve incomplete response output in failed inference traces.* Failed traces previously dropped attempted tool calls that only appeared in the terminal payload — direct improvement to debuggability.
6. **[#58404](https://github.com/openai/codex/pull/58404)** — *Fix context token estimates for responses without usable usage.* Tracks the history boundary so retained output from failed responses still counts toward estimates, making auto-compaction trigger on time.
7. **[#58430](https://github.com/openai/codex/pull/58430)** + **[#58434](https://github.com/openai/codex/pull/58434)** — *Audio file references with explicit runtime rejection* and *audio validation failures as non-retryable input errors.* Extends `app-server`/model content with `fileId`/`file_id` audio inputs while mapping size/format/sample-rate problems to `InvalidAudioInput` (HTTP 400) instead of pointless retries.
8. **[#58428](https://github.com/openai/codex/pull/58428)** — *Support app settings in plugin configuration.* Connector-wide settings under `plugins.<plugin>.apps.<connector>`, merged field-by-field with earlier plugin names taking precedence.
9. **[#58411](https://github.com/openai/codex/pull/58411)** — *Expose non-consuming input activity waits to hosts.* Adds `CodexThread::wait_for_input_activity` so host-owned tools can wait on agent messages/steering identically to native `wait_agent`, even with multi-agent support disabled.
10. **[#58403](https://github.com/openai/codex/pull/58403)** — *Run package updates outside the project on non-Windows platforms.* Executes updaters with `/` as CWD so parent-directory package config and hooks can't influence Codex's own updates — a quiet supply-chain hardening.

*Also landed:* [#58446](https://github.com/openai/codex/pull/58446) clickable viewed-image paths in TUI (local workspaces only, disabled over SSH), [#58427](https://github.com/openai/codex/pull/58427) alternative sign-in methods grouped into a submenu, [#58412](https://github.com/openai/codex/pull/58412) leading `!` stays literal when exposed by an edit, [#58406](https://github.com/openai/codex/pull/58406) host-inherited thread instructions/execution policies, [#58459](https://github.com/openai/codex/pull/58459) tighter Bazel CI snapshot handling.

## 5. Hot Discussions

**General**
- **[#3057](https://github.com/openai/codex/discussions/3057)** — *Codex using Python to make edits to files* (22 comments, 👍38). Long-running thread: the agent scripts file changes via Python instead of the File Edit tool. Still the most-engaged discussion and a persistent signal about edit-tool reliability.
- **[#49129](https://github.com/openai/codex/discussions/49129)** — *Codex CLI goes fullscreen* (8 comments, 👍5). OpenAI's own post on the new full-window TUI default: expandable diffs/tool output, pinned composer, copy with formatting preserved.
- **[#41527](https://github.com/openai/codex/discussions/41527)** — *Native ChatGPT Linux app on SteamOS 3.8.16 (Steam Deck)* (7 comments, 👍5). Community-validated install on an officially unsupported Arch-based distro.

**Q&A**
- **[#58396](https://github.com/openai/codex/discussions/58396)** — *Does `plugin add` initiate OAuth for `authentication: ON_INSTALL`?* (3 comments). Installation-only workflow question on Windows for the CapCut × Codex plugin — plugin auth lifecycle is underdocumented.
- **[#58235](https://github.com/openai/codex/discussions/58235)** — *Will Codex be rewritten from Rust to TypeScript?* A downstream fork maintainer asking for public architecture direction before investing further. Worth an official answer.
- **[#57688](https://github.com/openai/codex/discussions/57688)** — *Windows: resuming work with an inaccessible subagent and missing denial entry.* Five-week block, no supported recovery path described.

**Ideas**
- **[#22356](https://github.com/openai/codex/discussions/22356)** — *Thread sharing and hand off with other Codex accounts.* Cross-account collaboration on the same thread; directly echoed by the newly landed cross-backend session switching in the TUI.

**Show and tell**
- **[#58359](https://github.com/openai/codex/discussions/58359)** — *claude-codex-taskbar:* 5-hour and weekly Codex limits rendered on the Windows 10/11 taskbar (<1 MB, open source).
- **[#58220](https://github.com/openai/codex/discussions/58220)** — *recall:* zero-dependency MCP server that exposes Claude Code's `~/.claude/projects/<project>/memory/` Markdown to Codex, so memory survives switching agents.
- **[#58372](https://github.com/openai/codex/discussions/58372)** — *Yardlet:* MIT-licensed native Mac (Swift) app that runs Codex CLI via `app-server` alongside other agents, keeping sessions in your normal `CODEX_HOME`.
- **[#58276](https://github.com/openai/codex/discussions/58276)** — *Vigie:* desktop window that follows `~/.codex/sessions` transcripts live, rendering reasoning, messages, and one row per tool call. Mac/Linux testers wanted.
- **[#58248](https://github.com/openai/codex/discussions/58248)** — */call-me:* remote MCP that phones you when Codex is blocked or finished (no OAuth).

## 6. Feature Request Trends

- **Editor-grade TUI ergonomics.** Undo/redo (#2379, 38👍) plus related composer fixes (leading `!` handling, copyability of agent output, clickable image paths) show demand for the TUI to behave like a real editor, not a prompt box.
- **Desktop UX polish and structure.** Nested local projects (#33304), renameable multi-machine "computers" (#53016), and consistent viewport scrolling (#45479) — the desktop app's information architecture is the limiting factor now, not the model.
- **Session/thread portability and collaboration.** Cross-backend session switching (landed), thread sharing/handoff between accounts (#22356), host-inherited thread instructions (#58406), and persistent `CODEX_HOME` sessions (Yardlet) all point the same direction: sessions should be portable, resumable, and shareable.
- **Explicit, discoverable permission and sandbox semantics.** `/approve` being unavailable after auto-review denial (#57350), phantom `approval_policy: Never` (#58458), Slack-delegation approval ambiguity (#58443), and read-only-FS sandbox bootstrap (#53898) — users want approvals to be legible and recoverable.
- **Extensibility surface growth.** Plugin-level app settings, `authentication: ON_INSTALL` OAuth behavior, `app-server` JSON-RPC contracts, audio/multimodal inputs, and MCP bridges (recall, /call-me) — the ecosystem is building on `app-server` faster than it's documented.
- **Rate-limit and cost observability.** Header-dropping on 429 (#58413) and taskbar limit trackers (#58359) both reflect demand for trustworthy quota visibility.
- **Remote/mobile continuity.** Android Remote failing on permission-pending threads (#40310) and "computer is locked" remote failures (#58452).

## 7. Developer Pain Points

- **Windows Desktop reliability is the top of the funnel.** Roughly a third of the top 30 issues carry `windows-os` + `app`: path deserialization breaking durable turns (#50428), bundled plugin sync `copyfile UNKNOWN` (#55794), projects vanishing post-update (#55869), VS Code extension UI failing to start (#57344), inconsistent auto-scroll (#45479). Multiple reports include downgrade instructions — users are pinning old builds.
- **Version-to-version regressions without migration paths.** "Projects disappear but SQLite is fine," "commands stopped rendering," "extension won't start" all share a shape: the update breaks the surface, data survives, and there's no in-product repair.
- **Opaque safety and approval decisions block real work.** Cyber-safety false positives stall a Goal with no escalation path (#58209), automated review doesn't accept explicitly delegated owner approvals (#58443), and `/approve` isn't discoverable when it's needed (#57350). The complaint is not that checks exist — it's that the recovery path is hidden.
- **Sandbox initialization is fragile at the edges.** `bwrap` writing into a read-only `/home/agent/.codex` (#53898) and config that appears to set `approval_policy: Never` with no visible source (#58458) make escalated flows un-debuggable from the user side.
- **Lost state on interruption.** Queued input not drained after `turn/interrupt` (#58421), broken turn/start on Windows (#50428), and missing failed-trace evidence (fixed in #58456) — the theme is "the session didn't survive, and neither did the diagnostics."
- **Latency outliers in long conversations.** A 97-second first token for a one-line, no-tool response (#58453) undermines the perceived value of long-running sessions; expect this to be tied to context/compaction behavior.
- **Observability gaps when the agent acts.** Hidden command execution (#37213, 👍40), hidden follow-up questions on some Linux desktops (#58306), and unreadable prompt input after theme switches (#58440) — users consistently ask to *see* what Codex is doing before it does it.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-10-31

## 1. Today's Highlights
Tonight's nightly (`v0.67.0-nightly.20261030`) is a small, hygiene-focused release: README scope/limitations documentation and a fix bounding inline history re-renders after terminal width changes. Meanwhile, issue activity is dominated by **agent reliability** — false-success subagent terminations, generalist-agent hangs, browser-agent config/Wayland failures — and by a cluster of filesystem/path-correctness PRs (symlinks, `.gitignore` negation, `~` expansion, Windows `stat` behavior).

## 2. Releases
**v0.67.0-nightly.20261030.gb633c0703**
- `docs(readme)`: clarified Gemini CLI scope, limitations, and the surrounding tool landscape ([#29995](https://github.com/google-gemini/gemini-cli/pull/29995)).
- `fix(cli)`: bounded inline history re-render after terminal width changes ([PR by @jvargassanchez-dot](https://github.com/google-gemini/gemini-cli/pulls)).
- Automated version bump PR: [#30045](https://github.com/google-gemini/gemini-cli/pull/30045).

## 3. Hot Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent MAX_TURNS reported as GOAL success (P1, 13 comments, 👍2)**  
   A subagent that hit its turn cap before doing any analysis still reports `status: "success"` / `Termination Reason: GOAL`. Highest-engagement issue of the day because it silently corrupts agent results — callers cannot distinguish truncation from completion.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs (P1, 8 comments, 👍8)**  
   Delegation to the generalist agent can hang indefinitely on trivial tasks (e.g. folder creation). Highest 👍 in the set; the workaround (forbidding subagent use) effectively disables the feature, signalling broad user impact.

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Zero-dependency OS sandboxing + post-execution intent routing (P2, 9 comments)**  
   Proposes leaning into Gemini 3's native bash fluency while containing risk via OS-level sandboxing rather than restricting shell access. A design-level thread that likely shapes the permission model.

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini rarely invokes skills or subagents on its own (P2, 7 comments)**  
   Anecdotal but resonant: custom skills (e.g. `gradle`, `git`) are only used when explicitly instructed. Directly undermines the value of the skills/subagent surface area.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — EPIC: assess AST-aware file reads, search, and codebase mapping (P2, 7 comments)**  
   Tracks whether AST-aware tools reduce misaligned reads and token noise. Related sub-issues [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) and [#22747](https://github.com/google-gemini/gemini-cli/issues/22747) are also active today.

6. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error with >128 tools (P2, 3 comments)**  
   Agents fail hard when too many tools are in scope; users expect smarter tool-set narrowing. A hard blocker for large MCP/extension installs.

7. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should stop/discourage destructive behavior (P2, 3 comments, 👍1)**  
   Model reaches for `git reset` / `--force` when safer alternatives exist. Safety-adjacent and likely to gain traction alongside the sandboxing discussion.

8. **[#22267](https://github.com/google-gemini/gemini-cli/issues/22267) — Browser agent ignores `settings.json` overrides (P2, 4 comments)**  
   `AgentRegistry` merges settings correctly at init, but the Browser Agent ignores them (e.g. `maxTurns`). A clear config-plumbing regression rather than a design debate.

9. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland (P1, 4 comments)**  
   Fails while still reporting `Termination Reason: GOAL` — reinforcing the theme that termination reasons are unreliable, and highlighting Linux desktop coverage gaps.

10. **[#22741](https://github.com/google-gemini/gemini-cli/issues/22741) — Allow local agents to be backgroundable via Ctrl+B (P3, 👍2)**  
    Subagents are frequently used for non-blocking work (exploration, lint/build), yet block the main session. Small, high-leverage UX request with early community support.

## 4. Key PR Progress

1. **[#30059](https://github.com/google-gemini/gemini-cli/pull/30059) (CLOSED) — Preserve selected model across fallback, cancel, and rewind**  
   Fixes manually selected models (e.g. `gemini-3.1-pro-preview`) silently reverting to `gemini-3-flash-preview` on later turns while the footer and `/model` dialog still show the old choice — a confusing state-divergence bug.

2. **[#30057](https://github.com/google-gemini/gemini-cli/pull/30057) — Preserve explicit `gemini-2.5-flash` in dynamic model resolution**  
   Related follow-up: explicit `--model`/`/model` choices were being overridden when `useLatestFlash` is active (Vertex AI / API-key auth paths).

3. **[#30051](https://github.com/google-gemini/gemini-cli/pull/30051) — Kill active shells and persist tool calls on headless interruption**  
   Fixes `gemini -p ... --yolo` exiting with code 0 on SIGINT/SIGTERM while leaving `run_shell_command` alive in a detached process — important for CI and scripted usage.

4. **[#30042](https://github.com/google-gemini/gemini-cli/pull/30042) (CLOSED) — Canonical symlink resolution in `GlobTool`**  
   Resolves workspace roots and entries to realpaths for filtering, boundary validation, and output. Pairs with [#20079](https://github.com/google-gemini/gemini-cli/issues/20079) (symlinked agent files not recognized).

5. **[#30052](https://github.com/google-gemini/gemini-cli/pull/30052) — Honor nested `.gitignore` negations under `dir/**` patterns**  
   `GitIgnoreParser` disagreed with git on re-included files (`logs/**` + `!keep.txt`). Correctness fix with direct impact on context gathering and `/restore` behavior.

6. **[#30034](https://github.com/google-gemini/gemini-cli/pull/30034) (CLOSED) — Honor `.git/info/exclude` and `core.excludesFile` in the shadow repo**  
   Prevents `/restore` from reverting files that git considers ignored. Notable because it fixes data-loss-adjacent behavior in checkpointing.

7. **[#30039](https://github.com/google-gemini/gemini-cli/pull/30039) (CLOSED) — Serialize concurrent extension installs with a per-extension lock**  
   Closes a TOCTOU race in `installOrUpdateExtension()` where parallel installs of the same extension could interleave file copies and metadata writes.

8. **[#30058](https://github.com/google-gemini/gemini-cli/pull/30058) — Prevent interrupted Whisper downloads from counting as installed**  
   Partial files at the final model path made `isModelInstalled()` return true, permanently breaking voice input until manual cleanup.

9. **[#30055](https://github.com/google-gemini/gemini-cli/pull/30055) — Map Claude `SubagentStop` hooks to `AfterAgent` on migrate**  
   `EVENT_MAPPING` used the wrong key casing (`SubAgentStop`), so migrated hooks passed through unmapped. Eases migration from Claude Code.

10. **[#30050](https://github.com/google-gemini/gemini-cli/pull/30050) (CLOSED) — Flush pending SSE buffer at stream EOF**  
    Drops the final event when a stream closes without a trailing `\n\n` (common behind proxies/gateways) — a subtle source of truncated responses.

*Also worth watching:* [#29978](https://github.com/google-gemini/gemini-cli/pull/29978) (`read_background_output` dropping oversized/boundary lines), [#30054](https://github.com/google-gemini/gemini-cli/pull/30054) (`tildeifyPath` boundary fix, `~bert/proj`), [#30053](https://github.com/google-gemini/gemini-cli/pull/30053) (`Background PIDs: NaN`).

## 5. Hot Discussions
No discussion data was provided for this period; section omitted.

## 6. Feature Request Trends

- **Subagent orchestration & ergonomics** — backgrounding via `Ctrl+B` ([#22741](https://github.com/google-gemini/gemini-cli/issues/22741)), shared memory / parallel collaboration ([#18287](https://github.com/google-gemini/gemini-cli/issues/18287)), discovery via `settings.json` ([#18285](https://github.com/google-gemini/gemini-cli/issues/18285)), and trajectory visibility through `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)).
- **Context efficiency / AST-aware tooling** — the [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) epic plus "tactful extraction" surgical reads ([#19561](https://github.com/google-gemini/gemini-cli/issues/19561)) target the ~36.6k-token baseline and large-file "firehose" reads.
- **Persistent, file-based task tracking** — replacing in-context `WriteToDo` to avoid context rot ([#18836](https://github.com/google-gemini/gemini-cli/issues/18836), experiment in [#21000](https://github.com/google-gemini/gemini-cli/issues/21000)).
- **Safety with capability, not restriction** — OS sandboxing plus intent routing ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)) and discouraging destructive git/DB operations ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Workspace-scoped policy** — per-workspace approval policies rather than a single global policy ([#18397](https://github.com/google-gemini/gemini-cli/issues/18397)).
- **Eval infrastructure maturity** — stabilizing internal project evals ([#23166](https://github.com/google-gemini/gemini-cli/issues/23166)) and making flaky steering evals deterministic ([#23313](https://github.com/google-gemini/gemini-cli/issues/23313)).

## 7. Developer Pain Points

- **Agent termination signals are untrustworthy.** `MAX_TURNS` reported as `GOAL` success ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)), the same pattern in the Wayland browser failure ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)), and indefinite generalist hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)) together make agent output unauditable.
- **Model selection state diverges from model actually used.** Two independent PRs ([#30059](https://github.com/google-gemini/gemini-cli/pull/30059), [#30057](https://github.com/google-gemini/gemini-cli/pull/30057)) address silent reversion to flash models while the UI still advertises the user's choice.
- **Configuration is inconsistently honored.** Browser Agent ignores `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) and settings writes clobbered on-disk edits made after startup ([#29762](https://github.com/google-gemini/gemini-cli/pull/29762)).
- **Filesystem/path edge cases dominate the fix queue.** Symlinked agents ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)), symlinked glob roots ([#30042](https://github.com/google-gemini/gemini-cli/pull/30042)), `.gitignore` negation ([#30052](https://github.com/google-gemini/gemini-cli/pull/30052)), `~` expansion ([#30054](https://github.com/google-gemini/gemini-cli/pull/30054)), and Windows/libuv `dev: 0` ([#30044](https://github.com/google-gemini/gemini-cli/pull/30044)).
- **Tool sprawl breaks sessions.** Hard 400s above ~128 tools ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) penalize users with rich MCP/extension setups.
- **Workspace pollution.** The model scatters temporary edit scripts across directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)), making clean commits laborious.
- **Interactive prompts stall automation.** The agent gets stuck on CLIs that ask questions (e.g. `create-vite`) ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)), and headless runs leave orphaned shells ([#30051](https://github.com/google-gemini/gemini-cli/pull/30051)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI — Community Digest
**Date:** 2026-10-31 · **Repo:** [github/copilot-cli](https://github.com/github/copilot-cli)
**Activity window:** last 24h — 0 releases · 33 issues updated (30 shown) · 2 PRs updated

---

## 1. Today's Highlights

No releases shipped in the last 24 hours, but issue traffic was heavy and concentrated on platform reliability: a high-severity WSL2 CPU spin regression (#3700), repeated 300s auto-compaction timeouts (#5292), and intermittent `web_search` gateway failures (#5301) dominated the queue. On the delivery side, the long-standing request to ship a container image (#55, 23 👍) moved closer to reality with a recreated PR (#5308) that publishes `ghcr.io/github/copilot-cli` on release. A cluster of fresh triage items also points to growing friction in model configuration (Fusion tier flags) and ACP/headless integrations.

---

## 2. Releases

_No new releases in the last 24 hours._

---

## 3. Hot Issues

1. **[#55 — Package copilot-cli in docker image](https://github.com/github/copilot-cli/issues/55)** (OPEN, 6 comments, 23 👍)
   The most-upvoted item in the queue by a wide margin. Developers without Node.js on their machines want a supported, easily upgradable install path. Now directly tied to PR #5307/#5308, so this is finally moving from request to implementation.

2. **[#3700 — 1.0.60 WSL2 regression: ~215% CPU while idle, TUI frozen until restart](https://github.com/github/copilot-cli/issues/3700)** (OPEN, 6 comments, 2 👍, High severity)
   Reproduces on every fresh session after a clean reboot, with live reasoning/streamed text never painting. Marked as a regression of #2208, which makes it a priority-1 platform bug for the Windows/WSL2 user base.

3. **[#3760 — "ctrl+enter enqueue" label vs. actual ctrl+q binding](https://github.com/github/copilot-cli/issues/3760)** (CLOSED, 3 comments, 12 👍)
   A documented-behavior mismatch with video evidence; closed within the window. High 👍 relative to comment count shows broad silent agreement — the kind of small UX papercut that erodes trust in the TUI's discoverability.

4. **[#1996 — Plugin marketplace install fails on `plugins.56.source` validation](https://github.com/github/copilot-cli/issues/1996)** (CLOSED, 6 comments, 1 👍)
   Strict Zod validation of `marketplace.json` rejects an entire marketplace for a single malformed entry. Closed, but part of a pattern (see #4969) where schema strictness blocks plugin adoption rather than degrading gracefully.

5. **[#4724 — Auto-compact on idle, aligned to the model's prompt cache TTL](https://github.com/github/copilot-cli/issues/4724)** (OPEN, 3 comments, 2 👍)
   Makes the cost argument explicitly: after a ~5-minute idle gap, the next turn re-reads full context uncached, and compaction only fires on token thresholds. A well-formed feature request at the intersection of cost, latency, and context management.

6. **[#5298 — `--model fusion` fails unless undocumented `DYNAMIC_AUTO_TIERS` flag is set (1.0.105)](https://github.com/github/copilot-cli/issues/5298)** (OPEN, triage, 0 comments)
   Fusion is documented as GA and enabled for the org, yet fails with "requires dynamic Auto tiers." Freshly filed and closely related to #5290 — together they suggest the model-resolution layer's configuration surface is ahead of its documentation.

7. **[#5301 — `web_search` fails with HTTP 504 at ~120s](https://github.com/github/copilot-cli/issues/5301)** (OPEN, triage, 0 comments)
   Reported as failing on more than half of calls over ~9 days via the remote GitHub MCP server. A reliability regression on a core built-in tool, with a clear transport-level error signature for maintainers to chase.

8. **[#5292 — Automatic compaction repeatedly times out at 300s until sessions hit the hard context limit](https://github.com/github/copilot-cli/issues/5292)** (OPEN, 0 comments, reported on 1.0.91)
   The summarizer timeout becomes a dead end: compaction fails, context keeps growing, then requests are rejected for exceeding the limit, with no recovery path. Pairs with the now-closed #5205 rollover failure to form a real context-memory reliability theme.

9. **[#5304 — `/keep-alive` in WSL2 does not prevent the Windows host from sleeping](https://github.com/github/copilot-cli/issues/5304)** (OPEN, triage, 1 comment)
   The CLI uses `systemd-inhibit` inside WSL, which creates no Windows power request visible to `powercfg -requests`. Breaks long-running sessions — a concrete WSL platform-parity gap from a well-known contributor.

10. **[#5297 — Repository-level, version-controlled command permissions (allow / ask / deny)](https://github.com/github/copilot-cli/issues/5297)** (OPEN, triage, 0 comments)
    Requests committing a shared permission set alongside instructions, skills, and agents so a team cloning a repo inherits the same trust posture. Strong signal for governance/onboarding use cases in team and workshop settings.

---

## 4. Key PR Progress

Only two PRs were updated in the last 24 hours, and they are the same change — #5308 is a faithful recreation of #5307 after the original was closed. Both are now closed.

1. **[#5308 — Publish a Copilot CLI server container image on release](https://github.com/github/copilot-cli/pull/5308)** (CLOSED, by brunoborges)
   Recreated from #5307 with the original two commits unchanged. Outstanding review feedback is substantive: an existing `latest` or `prerelease` manifest lacking a version annotation can be mistaken for a missing tag and overwritten by an older release — a real registry-correctness hazard for the publish workflow.

2. **[#5307 — Publish a Copilot CLI server container image on release](https://github.com/github/copilot-cli/pull/5307)** (CLOSED, by brunoborges)
   Adds a workflow publishing to `ghcr.io/github/copilot-cli` on every release, running the CLI as a headless server so a Copilot SDK client in another container, a CI job, or an integration test can drive it directly. Explicitly framed as the answer to #55.

_Net read: the container-image work is the only active delivery thread, and the version-tag overwrite concern should be resolved before it lands._

---

## 5. Hot Discussions

_No discussion data was provided for this window._

---

## 6. Feature Request Trends

- **Distribution without Node.js** — A supported container image (#55 → PR #5307/#5308) remains the single highest-demand packaging ask, motivated by frictionless onboarding and upgrades.
- **Richer hook/extension surface** — Requests are pushing hooks beyond lifecycle events: an authoritative foreground-session change stream for terminal integrations (#5279), plus a hook for slash-command/skill invocation with name matching and async command hooks (#5305).
- **Configuration as code for trust** — Repo-level, version-controlled allow/ask/deny command permissions (#5297) so teams inherit a shared security posture with the repo.
- **Predictable model configuration** — `--fusion-tier` CLI support (#5290), an undocumented gate blocking `--model fusion` (#5298), and clearer reasoning-effort tier gating (#2990) all point to a demand for documented, self-consistent model controls.
- **Context/cost-aware memory management** — Idle-triggered compaction aligned to prompt-cache TTL (#4724) and reliable automatic compaction (#5292).
- **Input customization** — Remappable `shift+enter` submit-vs-newline behavior (#5291) and correct enqueue keybindings (#3760).
- **Headless/ACP hardening** — Correctness and performance fixes for programmatic clients (#5229, #5293, #5108).
- **WSL2 platform parity** — Host power management (#5304) and TUI rendering/CPU behavior (#3700).

---

## 7. Developer Pain Points

1. **Windows and WSL2 remain the weakest platform.** A ~215% CPU idle spin with a frozen TUI (#3700), `/keep-alive` not preventing host sleep (#5304), recurring invalid PowerShell generation (~2,164 shell calls analyzed, #5302), and an OpenWith dialog firing on every message when the profile path contains a space (#5299). The space-in-path bug in particular suggests unquoted path interpolation.
2. **Context and memory management fails closed, not open.** Auto-compaction hitting a 300s summarizer timeout with no recovery (#5292) and rollover aborting on a missing `checkpoint.md` (#5205, closed) leave users stuck at the hard context limit. `store_memory` also silently fails for non-GitHub origins like Azure DevOps (#3060, closed).
3. **Documentation and implementation drift on flags and keybinds.** `ctrl+enter` advertised but `ctrl+q` required (#3760), `--available-tools=` exposing all 21 tools instead of none (#5306), `--fusion-tier` documented but absent (#5290), and Fusion failing behind an undocumented env var (#5298). Users are repeatedly debugging the CLI against its own docs.
4. **Strict plugin marketplace validation blocks adoption.** A single over-long description (#4969) or one malformed `source` field (#1996) rejects the entire marketplace with no partial load — harsh failure semantics for a discovery surface.
5. **Headless/ACP integrations are brittle.** `session/list` rescanning the entire store per page (#5108), `session/prompt` withheld until async bash shells exit (#5293), and expired MCP OAuth tokens opening a browser instead of using the stored refresh token (#5229). All closed or triaged, but a concentrated cluster for SDK/agent-client authors.
6. **Core tool reliability.** `web_search` 504s on a majority of calls over nine days (#5301) and a misleading `model_not_supported` 400 after content-filter responses (#5309) both cost users debugging time on issues outside their control.
7. **Autopilot quality-of-life.** Empty `assistant.message` content before `task_complete` claiming the answer is "above" (#5303), and random approach selection after a Ctrl+D decline (#5295) undermine confidence in unattended runs.

---

*Digest generated from 30 of 33 issues updated in the last 24h and 2 PRs. No release or discussion activity to report.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-10-31

## 1. Today's Highlights
OpenCode shipped three releases in the last 24 hours, headlined by **v2.2.5** worktree/base-branch shortcuts and shell-mode toggling, following **v2.2.4**'s persistent desktop terminals and **v2.2.3**'s Claude Code login integration. Community attention remains dominated by the free-tier incident mega-thread (#59387, 147 comments) and long-standing sandboxing concerns (#2242, 81 👍). On the engineering side, PRs this cycle focus heavily on reliability hardening: credential redaction in logs, schema-validation guards, MCP reconnect behavior, and a new `opencode doctor` diagnostic command.

## 2. Releases
- **v2.2.5** — New keyboard shortcuts: `⌘⌥O` / `Ctrl+Alt+O` to select a worktree, `⌘⌥B` / `Ctrl+Alt+B` to choose its base branch, and `⌘⇧X` / `Ctrl+Shift+X` to toggle shell mode in the composer. ([#60744 release PR](https://github.com/anomalyco/opencode/pull/60744))
- **v2.2.4** — Desktop terminals are now session-scoped, survive server restarts with scrollback intact, stay synchronized with the TUI and other windows, and preserve renamed terminal names. ([#60346](https://github.com/anomalyco/opencode/pull/60346))
- **v2.2.3** — Claude Code can be used inside OpenCode: install Claude Code, run `claude auth login`, then select **Claude Agent** in `/connect`. Also includes faster long-session streaming in Desktop. ([#58782](https://github.com/anomalyco/opencode/pull/58782))

## 3. Hot Issues

1. **[#59387](https://github.com/anomalyco/opencode/issues/59387) — Free tier issues mega-thread** (147 comments, 12 👍, OPEN)
   The central triage thread for `Free usage exceeded`, non-resetting quotas, and Desktop version gating. High comment volume signals an ongoing billing/quota reliability problem affecting a large user cohort.

2. **[#2242](https://github.com/anomalyco/opencode/issues/2242) — Sandboxing the agent** (106 comments, 81 👍, OPEN since 2025-08)
   Requests filesystem/terminal isolation comparable to macOS Seatbelt in Gemini CLI or Codex CLI. The highest-upvoted issue in this set; a persistent security gap for teams running agents unattended.

3. **[#45278](https://github.com/anomalyco/opencode/issues/45278) — Payment declined after 3 months** (42 comments, 35 👍, CLOSED)
   Renewal failures with previously working cards, bank-confirmed as valid. Strong reaction because it blocks paying subscribers entirely; now closed.

4. **[#53011](https://github.com/anomalyco/opencode/issues/53011) — Numeric replacements duplicate changed values** (9 comments, CLOSED)
   The `edit` tool intermittently emits duplicated tokens (e.g., `900900`) with duplication counts from 2× to 129×. A correctness bug with silent file corruption potential.

5. **[#53146](https://github.com/anomalyco/opencode/issues/53146) — Concurrent servers collide on `session_message.seq`** (9 comments, CLOSED)
   Two server processes sharing one `opencode.db` allocate sequence numbers from independent in-memory counters, causing `UNIQUE(seq)` failures. Important for long-lived `opencode serve --service` deployments.

6. **[#52791](https://github.com/anomalyco/opencode/issues/52791) — `Invalid opencode-go/anthropic-messages stream event`** (4 comments, CLOSED)
   Long sessions begin failing every request after a few hours; retries and restarts don't help. Indicates stream-parsing fragility that breaks unattended workflows.

7. **[#60583](https://github.com/anomalyco/opencode/issues/60583) — Remote MCP 404 triggers infinite reconnect** (2 comments, OPEN, reproduced)
   A `resources/templates/list` 404 is treated as a dead session, producing an endless connected/connecting oscillation with intermittently disappearing tools. Core MCP interoperability issue.

8. **[#60501](https://github.com/anomalyco/opencode/issues/60501) — `webfetch` status fails schema validation** (2 comments, OPEN, reproduced)
   Nonstandard HTTP statuses abort `SessionRunner.drain` with `Schema validation failed`. Shows how strict internal schemas can take down a whole session.

9. **[#60738](https://github.com/anomalyco/opencode/issues/60738) — Windows startup spawns ~15–20 `cmd.exe` windows** (1 comment, OPEN)
   Tool detection runs `cmd.exe /c where <tool>` without `CREATE_NO_WINDOW`, adding ~20 seconds of visible flicker. A clear platform-polish regression with an obvious fix.

10. **[#60752](https://github.com/anomalyco/opencode/issues/60752) — iOS Safari crashes after auth (`undefined e.type`)** (0 comments, OPEN)
    The web UI crashes immediately post-authentication on iPhone, reported on both 2.2.0 and 2.2.5. Mobile web remains a weak surface.

*Also worth watching:* [#60739](https://github.com/anomalyco/opencode/issues/60739) "Not usable" on 2.2.4, [#59759](https://github.com/anomalyco/opencode/issues/59759) invisible TUI question selector, [#53006](https://github.com/anomalyco/opencode/issues/53006) 2.7 MB eagerly bundled entry chunk.

## 4. Key PR Progress

1. **[#60749](https://github.com/anomalyco/opencode/pull/60749) — Decode ACP attachment filenames** (OPEN)
   Fixes `filenameFromUri` leaving percent-encoding intact (`photo%201.png` → `photo 1.png`); closes #59792.

2. **[#60751](https://github.com/anomalyco/opencode/pull/60751) — Report nonstandard provider HTTP statuses** (OPEN)
   Keeps `HttpContext.status` strict while preventing proxies returning codes like 999 from crashing session drain; closes #60501.

3. **[#60604](https://github.com/anomalyco/opencode/pull/60604) — Unencodable tool results no longer kill the session** (OPEN)
   Guards `encodeJson` in `toolResultText` so a single bad tool output doesn't terminate the run; closes #58934.

4. **[#60750](https://github.com/anomalyco/opencode/pull/60750) — `opencode doctor`** (OPEN, needs compliance)
   Read-only diagnostic of the data directory and hard-to-see failure modes, motivated by a real stale-schema incident where v1 CLI and v2 Desktop shared `~/.local/share/opencode`.

5. **[#60748](https://github.com/anomalyco/opencode/pull/60748) — Redact credentials in structured logs** (OPEN, needs compliance)
   Provider errors, request spans, and tool metadata can leak `Authorization` headers or live API keys into `log/opencode.log`; this centralizes redaction in the log formatter.

6. **[#60747](https://github.com/anomalyco/opencode/pull/60747) — Expose `apiVersion` in `/api/info`** (OPEN, needs compliance)
   Lets clients distinguish HTTP API generations instead of gating on semver, since v1 routes were removed in 2.0.

7. **[#60741](https://github.com/anomalyco/opencode/pull/60741) — Preview long writes and diffs in the TUI** (OPEN, contributor)
   A 500-line write currently pushes the rest of the turn off-screen; this adds a collapsed preview, mirroring existing shell-output truncation. Related to #40096.

8. **[#60548](https://github.com/anomalyco/opencode/pull/60548) — Name the MCP tool and input in the permission dock** (OPEN)
   MCP tools request with `resources: ["*"]` and no curated description, so the dock previously showed opaque prompts; closes #51519.

9. **[#60737](https://github.com/anomalyco/opencode/pull/60737) — VS Code emits V2 mention syntax** (OPEN, needs compliance)
   `Cmd+Option+K` currently inserts V1 `@path#L37-42`; V2 expects `@path#37-42`, breaking file references from the extension.

10. **[#60717](https://github.com/anomalyco/opencode/pull/60717) / [#60715](https://github.com/anomalyco/opencode/pull/60715) — ReDoS hardening** (OPEN)
    Replace backtracking-prone regexes in email validation and `data:` URL parsing (used in `ai/src/media.ts`, `core/src/aisdk.ts`, `cli/src/acp/tool.ts`) that can hang on adversarial inputs like 30,000 consecutive dots or semicolons.

## 5. Hot Discussions
*No discussion data was provided in this dataset; section omitted.*

## 6. Feature Request Trends
- **Agent sandboxing and least-privilege execution** — The strongest sustained demand (#2242, 81 👍): OS-level confinement, path restrictions, and clearer permission semantics.
- **Permission-surface usability for plugins/MCP** — Multiple PRs and issues (#60745, #60548, #60740) converge on making the permission dock name the tool, the action, and the input instead of showing generic or duplicated entries.
- **Diagnostics and operability** — `opencode doctor` (#60750), `apiVersion` discovery (#60747), and better startup/tool-detection behavior (#60738) reflect demand for debuggable, inspectable installations.
- **Context and subagent control** — #59758 asks for the ability to disable subagents or fix reasoning settings to prevent rapid context exhaustion on locally served models.
- **Config isolation across worktrees** — #53096 reports that changing an API key in one worktree breaks the other 11 instances with apparent amnesia, pointing to per-worktree config scoping.
- **Frontend/performance budget** — #53006 flags a 2.7 MB entry chunk downloaded on every route, a request for route-level code splitting.

## 7. Developer Pain Points
- **Free-tier quota and billing reliability** is the loudest complaint cluster: quotas that never reset, `Free usage exceeded` loops, unexpected plan gating, and declined renewals on valid cards (#59387, #45278).
- **Regional availability** — Russian users report complete loss of site and model access without a VPN despite an active Go Plus subscription (#60573).
- **Silent correctness and data-integrity failures** are the most damaging class of bug: duplicated numeric edits (#53011), destroyed pending permissions with no revocation event (#52846), and stale sequence counters corrupting shared databases (#53146).
- **Session state instability** — models switching mid-conversation across concurrent sessions (#52805), cached per-session model resolution silently falling back to another provider (#53060), and stream-event parse failures that persist across retries (#52791).
- **Platform rough edges** — visible `cmd.exe` storms on Windows startup (#60738), TUI freezes on large inline images (#60377), and iOS Safari post-auth crashes (#60752).
- **Performance and context economics** — oversized frontend bundles (#53006), long-running sessions exhausting context via subagents (#59758), and compaction retaining unbounded recent-context (#60391).
- **Security hygiene** — credentials found in plaintext in `log/opencode.log` (#60748) and the absence of any agent sandbox (#2242) remain unresolved foundational concerns.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi Community Digest — 2026-10-31

**Scope:** 36 issues, 20 PRs, and 2 discussions updated in the last 24h. No new releases.

---

## 1. Today's Highlights

Activity is dominated by **platform/platform-terminal correctness**: a large Windows experience thread (#7547, 93 comments), mintty/ConPTY escape-sequence leaks (#10256), and WSL interop failures (#11592) all saw movement, with fixes landing for the latter two. A second cluster is **auth and provider plumbing** — OpenAI subscription/entitlement errors (#10480, #10953, #10605) and Anthropic/Gemini request-replay bugs (#10954, #11376, #10157) continue to generate 400s for users. On the feature side, the provider expansion PR (#11370), TUI transcript virtualization (#11598), and a trio of tool-search ranking fixes (#11625/#11631/#11632) represent the most substantive code progress.

---

## 2. Releases

None in the last 24h.

---

## 3. Hot Issues

1. **[#7547](https://github.com/earendil-works/pi/issues/7547) — [Windows] How do you use Pi on Windows? (OPEN, 93 comments, 👍2)**
   The de-facto Windows coordination thread. Maintainers explicitly frame the problem: too many supported execution paths (native, WSL, mintty, Windows Terminal, ConPTY), so effort must be split between core fixes, docs, and delegation to extensions. Highest-engagement issue in the window by a wide margin — treat it as the canonical signal source for Windows priorities.

2. **[#10480](https://github.com/earendil-works/pi/issues/10480) — Direct OpenAI connection ignores manual usage-limit reset (CLOSED, 20 comments, 👍3)**
   A banked reset on a ChatGPT Pro plan wasn't recognized by the `openai` route, while `openai-codex` with the same account worked. Closed with a documented workaround (`/logout` → `/login` via codex). Symptom of the broader auth-path divergence between the two OpenAI routes.

3. **[#10256](https://github.com/earendil-works/pi/issues/10256) — Terminal color-query replies leak into the prompt, BEL opens external editor (OPEN, 15 comments, 👍4)**
   Regression in 0.99.x on mintty/ConPTY: OSC 4 palette replies arrive prefixless after DA1, get echoed into the input buffer, and the BEL byte launches the external editor. Highest-👍 terminal bug; fix PR #11609 is up.

4. **[#10953](https://github.com/earendil-works/pi/issues/10953) — OpenAI login fails on ChatGPT Business, legacy Codex login works (CLOSED, 12 comments, 👍4)**
   `3p_delegated_access_policy_denied` on the standard route for a Business workspace; "OpenAI Codex (legacy)" succeeded with full access. Closed as no-action, which leaves enterprise users on the legacy path without a documented migration story.

5. **[#10605](https://github.com/earendil-works/pi/issues/10605) — ChatGPT/OpenAI OAuth 403 (OPEN, 11 comments, 👍1)**
   Plus-tier users hitting `subscription_sharing_user_not_eligible` after logout/login. Still open and unresolved — the error text gives users no actionable guidance.

6. **[#10157](https://github.com/earendil-works/pi/issues/10157) — Gemini tool-call thought signatures dropped on AI Studio OpenAI-compatible endpoint (OPEN, 9 comments)**
   The endpoint returns `extra_content.google.thought_signature`; Pi does not replay it, so multi-turn tool use degrades. Reproducible on 0.87.1 with Gemini Flash Lite. Matters for anyone using Gemini through the compat layer rather than a native provider.

7. **[#10299](https://github.com/earendil-works/pi/issues/10299) — Empty tool call from OpenRouter/GLM permanently wedges the session (CLOSED, 8 comments)**
   A malformed empty `tool_calls` entry is persisted and replayed, poisoning every subsequent request. Reported with repro *and* a fix, closing out a previously unreproducible report (#4854). Good example of provider-side sloppiness requiring client-side defensive parsing.

8. **[#10954](https://github.com/earendil-works/pi/issues/10954) — [prio:p0] OpenCode Go Claude: 400 on replayed thinking block after tool list change (OPEN, 6 comments)**
   `block_binding` is only sent for `supportsMidConvoEffort` models, so replayed thinking blocks fail validation when the tool list shifts. Related to #10324. P0 and still open.

9. **[#11376](https://github.com/earendil-works/pi/issues/11376) — [prio:p0] Removing an initial tool mid-session breaks all later Anthropic requests (OPEN, 4 comments)**
   After an extension reload stops registering a tool, every request fails with `tool_reference_unresolved`. Needs `needs-info` triage but is a hard blocker for long-lived sessions with reloadable extensions.

10. **[#11331](https://github.com/earendil-works/pi/issues/11331) — `tool_search` returns the wrong tool for an exact name match (CLOSED, 5 comments)**
    An exact tool name could lose to a shorter description containing the same words — a bad failure mode for model-driven tool selection. Closed with a fix available; spawned follow-up ranking work in both coding-agent and durable.

---

## 4. Key PR Progress

1. **[#11370](https://github.com/earendil-works/pi/pull/11370) — feat(ai,coding-agent): add DeepInfra, Nebius, Ollama Cloud, Scaleway, SiliconFlow, StepFun (OPEN)**
   Six hosted providers sourced from models.dev, selected by contributor activity and issue-tracker demand. Stacked on #11369. The largest user-visible capability addition in the window.

2. **[#11598](https://github.com/earendil-works/pi/pull/11598) — perf(tui): virtualize the transcript, lazy fullscreen layout (CLOSED)**
   Fixes framing cost being O(transcript) rather than O(viewport) — every component previously stayed alive for the whole session. Resolves #9549; meaningful for long sessions and slow terminals.

3. **[#7948](https://github.com/earendil-works/pi/pull/7948) — feat(coding-agent): defer extension runtime reloads (CLOSED)**
   Replaces awaited `ctx.reload()` with fire-and-forget `ctx.requestReload()`, coalescing requests and deferring replacement until operations, compaction, or summarization settle. Directly reduces the class of bugs behind #11376 and #4748.

4. **[#11629](https://github.com/earendil-works/pi/pull/11629) — feat: `PI_SELF_UPDATE_COMMAND` / `selfUpdateCommand` (CLOSED)**
   Lets wrapper-managed installs (mise, Nix, `PNPM_HOME` wrappers) declare how `pi update` should work instead of printing "cannot self-update." Refs #7756, #5607.

5. **[#11628](https://github.com/earendil-works/pi/pull/11628) — fix: name the package manager only when it owns the install (CLOSED)**
   `detectInstallMethod()` matched any path containing `/pnpm/`, so `$PNPM_HOME/global-nub/...` installs were misclassified. Fixes #7756.

6. **[#11627](https://github.com/earendil-works/pi/pull/11627) — fix: start WSL interop helpers from `/`, report editor failures (CLOSED)**
   Fixes #11592: deep working directories pushed the translated `\\wsl.localhost\...` path past MAX_PATH, so `powershell.exe` failed to spawn and clipboard image paste silently returned `null`.

7. **[#11609](https://github.com/earendil-works/pi/pull/11609) — fix(tui): consume mintty's prefixless palette replies after DA1 (CLOSED)**
   Targeted fix for #10256 — correctly frames the DA1 reply then drains the trailing OSC 4 payload instead of feeding it to the prompt.

8. **[#11625](https://github.com/earendil-works/pi/pull/11625) — fix: weigh tool names above descriptions in tool search (CLOSED)**
   Addresses #11331. Follow-ups **#11632** (rank tools matching more query terms) and **#11631** (port both fixes to durable's private ranker copy) also closed — closing the coding-agent/durable divergence.

9. **[#11037](https://github.com/earendil-works/pi/pull/11037) — fix: Unicode word segmentation in tool search (CLOSED)**
   The shared tokenizer split on `/[^a-z0-9]+/`, discarding CJK entirely. Fixes #10816 and makes `tool_search` usable for non-Latin tool metadata.

10. **[#11619](https://github.com/earendil-works/pi/pull/11619) — feat(durable): `beforeProviderRequest` generation hook (CLOSED)**
    Durable counterpart to coding-agent's `before_provider_request`, letting extensions rewrite provider request bodies — e.g. enabling Anthropic `thinking.display: "updates"` (#10804).

*Also merged:* **#11630** host keybinding hints to extension renderers (#4748), **#11607** whole-ANSI-sequence stripping in chord output, **#11606** image blocks from `read` in Code Mode, **#11605** env watcher frame-overflow reporting, **#11608** tokenized permission-gate command checks. **#11624** (llama.cpp docs tweaks) remains open.

---

## 5. Hot Discussions

**Q&A**
- **[#11404](https://github.com/earendil-works/pi/discussions/11404) — Is there an official Pi code-agent sandbox by Docker? (1 comment, 👍2)**
  Four `sbx/pi*` images exist on Docker Hub (`pi`, `pi-mixin`, `pi-image`, `pi-kit`) with no clear indication of who maintains them or whether they're sanctioned. Signals demand for an official containerized/sandboxed distribution — a natural complement to the Windows packaging debate in #7547.

**Show and tell**
- **[#11488](https://github.com/earendil-works/pi/discussions/11488) — AY-PI: per-prompt tier routing and tool scoping (2 comments, 👍1)**
  Built on Pi's virtual-model and classifier APIs: classifies each prompt into CHAT/SUGGEST/REVIEW/PLAN/CODE plus a low/medium/high tier, then scopes tools so only CODE retains `edit`/`write`/`bash`. Useful reference implementation for anyone building routing or least-privilege tool policies on top of Pi.

---

## 6. Feature Request Trends

- **Installation ownership and self-update**: wrappers and non-npm package managers (mise, Nix, `PNPM_HOME` shims) need a first-class contract — #7756, #5607, #11629.
- **Provider breadth and auth ergonomics**: six new providers pending (#11370), plus repeated demand for reliable OpenAI Business/Plus entitlement handling and a clearer split between `openai` and `openai-codex` routes.
- **Multilingual and precise tool discovery**: Unicode-aware tokenization (#10816/#11037) and deterministic ranking on exact names (#11331/#11625).
- **Session lifecycle control**: moving an inactive session into the current working directory with a keybinding (#11583), documented resume-directory semantics (#11617/#11532), and correct branch summarization after retries (#11602).
- **Extension runtime safety**: deferred/coalesced reloads (#7948), cross-realm keybinding resolution (#4748/#11630), and request-rewrite hooks for durable (#11619).
- **Terminal UX polish**: focus-aware cursor visibility in inactive panes (#11611), binary token formatting (#11620), and fullscreen/transcript performance (#11598).

---

## 7. Developer Pain Points

- **Windows and WSL remain the roughest surface.** Prefixless mintty palette replies corrupting the prompt (#10256), symbols leaking into input under CPU load (#11086), and MAX_PATH-driven silent failures in WSL clipboard paste (#11592) all point to the same gap: no robust terminal-capability negotiation or error surfacing. The 93-comment #7547 thread confirms the community has no shared expectation of what "supported on Windows" means.
- **Silent failures are worse than errors.** `readClipboardImage()` returns `null` with stderr set to `ignore`; env watcher overflow kills its only writer while the daemon keeps running (#11605); cached models vanish after catalog metadata resets to zero (#11593). Each costs users significant debugging time.
- **Replayed conversation state is a recurring 400 generator.** Dropped Gemini thought signatures (#10157), Anthropic thinking blocks after compaction (#11610) or tool-list changes (#10954), and unresolved tool references (#11376) are all the same underlying problem: request history is not preserved in a provider-valid form across edits, reloads, and retries.
- **OAuth/entitlement errors are opaque.** `3p_delegated_access_policy_denied`, `subscription_sharing_user_not_eligible`, and "usage limit reached" after a banked reset (#10480, #10953, #10605) give users no next step; the working answers live in issue comments, not in the product.
- **Duplicated logic between coding-agent and durable drifts.** Durable keeps its own copies of the tool ranker (#11631, #11632) and needed a separately ported `beforeProviderRequest` hook (#11619) — fixes must be applied twice, and regressions exist in one surface but not the other.
- **Long-lived processes leak or fail to exit.** 182 leaked X11 connections filling Xorg's client table (#7600), and `ctx.shutdown()` not terminating an idle RPC process until another command arrives (#11599) — both hit users running Pi as a persistent service.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-10-31

## 1. Today's Highlights

The most significant activity is on the reliability side: two long-running main-CI failure trackers (Managed Agent gate and E2E Tests) remain open and are absorbing most of the triage bandwidth, with the Managed Agent thread now at 100 comments. Alongside that, a substantial cluster of PRs lands managed-agent fault-injection coverage, remote-access enablement for `qwen serve`, and a batch of core correctness fixes around LSP readiness, shell permissions, and OpenAI cache-token accounting. A new `cua-driver-rs v0.27.0` release ships signed macOS binaries and unsigned Linux/Windows payloads for the CUA driver.

> Note: only **4 Issues** were updated in the last 24h (all covered below). 50 PRs were updated; the top 10 most substantive are summarized. **No Discussion data was provided**, so Section 5 is omitted.

---

## 2. Releases

### `cua-driver-rs v0.27.0` — Qwen CUA Driver prebuilt binaries
Vendored under `packages/cua-driver`, this release distributes prebuilt binaries for the computer-use driver across all three platforms:

- **macOS**: codesigned + notarized universal binary, plus a `QwenCuaDriver.app` bundle — installable without Gatekeeper workarounds.
- **Linux**: unsigned, `x86_64` + `arm64`, with a **glibc 2.31 floor** (RHEL 8 / Ubuntu 20.04-era baseline). Older distros will need to build from source.
- **Windows**: unsigned UIAccess worker + native SDK payload for `x86_64` + `arm64`. UIAccess implies the worker must be placed in a trusted location to interact with elevated windows.

**Takeaway:** macOS is fully production-ready; Linux and Windows artifacts are unsigned, so enterprise deployments will need to add their own signing/allow-listing step.

---

## 3. Hot Issues

Only 4 issues were updated in the window, all listed here.

1. **[#14724](https://github.com/QwenLM/qwen-code/issues/14724) — Main CI failed: Managed Agent gate — no test identified** · `type/bug`, `autofix/skip` · 100 comments
   The single loudest thread in the repo. Open since 2026-10-19, still open, and explicitly tagged `autofix/skip` — meaning the automated remediation path has opted out, so it needs a human. The "no test identified" signature suggests the Managed Agent gate fails without attributing the failure to a specific test, which is exactly the class of opaque failure that generates long comment threads. **Community reaction:** the comment volume (largely bot/CI echoes) signals a triage problem more than a debate — no 👍 recorded.

2. **[#15173](https://github.com/QwenLM/qwen-code/issues/15173) — Main CI failed: E2E Tests — no test identified** · `type/bug`, `autofix/in-progress` · 20 comments
   A `E2E Tests` run failed in `E2E Test (Linux) - sandbox:docker - shard 1/1`, step `Run E2E tests`, with a concrete failing test: `interactive/context-compress-interactive.test.ts`. Unlike #14724 this one *has* a named test and an active autofix, making it the more tractable of the two CI blockers. **Matters because** context-compression is core to long-session UX, and a flaky interactive test undermines confidence in that path.

3. **[#15949](https://github.com/QwenLM/qwen-code/issues/15949) — `/btw` response cannot be scrolled or selected/copied (Windows CLI)** · `priority/P3`, `category/ui`, `scope/interactive`, `scope/rendering`, `scope/windows`, `roadmap/terminal-ux` · 2 comments
   Freshly filed (2026-10-30). On Windows, long `/btw` output overflows the terminal viewport with no scroll affordance, making the head or tail of the answer unreachable. The label set is notable — it's tagged to `roadmap/terminal-ux`, so this is being tracked as part of the broader terminal rendering work rather than a one-off. **Community reaction:** early but concrete; Windows CLI rendering is a recurring sore spot.

4. **[#15251](https://github.com/QwenLM/qwen-code/issues/15251) — Fleet Shepherd Dashboard** · 0 comments
   An auto-maintained operational dashboard (last tick `2026-10-30T23:10:09Z`, scan-signal age 0m) tracking bot fleet PRs, dispatches, releases, and cleanups. No community discussion, but useful signal: this tick recorded `syncs: 0 · dispatches: 0 · releases: 0 · cleanups: 0`, i.e. a quiet fleet cycle — consistent with the CI blockers, not new PRs, being the current bottleneck.

---

## 4. Key PR Progress

1. **[#15945](https://github.com/QwenLM/qwen-code/pull/15945) — test(managed-agent): gate the A3 mixed-sibling approval crash window** *(wenshao)*
   Packages recovery-matrix row A3 as a fault arm in the Hosted failover E2E job: approves a two-call batch one sibling at a time, crashes the replacement Harness in the approval gap, then verifies recovery. This is exactly the kind of deterministic crash-window test the Managed Agent gate failures (#14724) need in order to become diagnosable.

2. **[#15887](https://github.com/QwenLM/qwen-code/pull/15887) — feat(serve): enable remote access from settings without restarting** *(yiliang114)*
   Adds **Settings → Connections → Allow remote connections** to a live `qwen serve` daemon. Remote access defaults off; a local operator can flip it on without a restart, then copy the address and a separate bearer token into another Web Shell's connection form. Removing the restart requirement is a real workflow unlock for remote/headless setups.

3. **[#15684](https://github.com/QwenLM/qwen-code/pull/15684) — feat(managed-agent): materialize inert external workspaces** *(yiliang114)*
   Operator-only path to materialize an already-registered external storage alias as a discoverable Workspace with a delegated owner. Deliberately minimal: metadata + idempotent receipt in one transaction, no storage allocation, no worker start.

4. **[#15946](https://github.com/QwenLM/qwen-code/pull/15946) — fix(core): reject LSP queries when no server is ready** *(404khai)*
   LSP navigation queries now fail with an explicit reason instead of silently returning empty results — covering go-to-definition, find-references, hover, document symbols, implementations, call-hierarchy prep, code actions, and workspace symbols. Fixes a nasty class of "the tool said nothing, so the model guessed" behavior.

5. **[#15681](https://github.com/QwenLM/qwen-code/pull/15681) — fix(core): don't treat fd duplication (`2>&1`) as a file write in shell permission checks** *(Suaroman)*
   `2>&1`, `1>&2`, `>&2`, `2>&-`, `<&0` are no longer classified as file writes by the shell permission checker. This eliminates spurious permission prompts on extremely common shell idioms — a high-frequency papercut.

6. **[#15433](https://github.com/QwenLM/qwen-code/pull/15433) — fix(core): preserve OpenAI cache-write token usage** *(he-yufeng)*
   Threads `prompt_tokens_details.cache_write_tokens` through both Chat Completions usage conversion paths, so GenAI provenance and OTel consumers can report cache-creation tokens for ordinary responses *and* streaming usage-only chunks with `choices: []`. Directly improves cost observability.

7. **[#13725](https://github.com/QwenLM/qwen-code/pull/13725) — fix(core): handle partial ANSI and UTF-8 prefixes in Shell previews** *(PratikWayase)*
   Fixes two low-severity boundary artifacts in the bounded Shell preview ring buffer when the ring starts mid-encoded-sequence: cut ANSI CSI sequences and split UTF-8 prefixes. Long-lived PR (open since 2026-10-09) but still moving.

8. **[#15169](https://github.com/QwenLM/qwen-code/pull/15169) — fix(memory): back off after a failed auto dream** *(harjothkhara)*
   Adds backoff when automatic memory "dreaming" fails, preventing repeated futile attempts. Worth flagging that the PR body leads with the maintainer's reviewer-test-plan requirement — a signal that review latency is currently gated on PR hygiene.

9. **[#15274](https://github.com/QwenLM/qwen-code/pull/15274) — fix(ci): preserve Maven suite results across cache write-back failures** *(qwen-code-dev-bot)* · `autofix/needs-human`
   Hardens the SDK Java Maven cache path: failed MySQL integration suites can still publish artifacts while preserving the original suite status, and cache setup failures preserve the already-known result. Companion to **#15286**, which stops the job-local Maven repo from sharing mutable inodes with the host cache (drops `maven-metadata-local.xml`, `_remote.repositories`, `resolver-status.properties`). Both are stuck awaiting human review.

10. **[#15435](https://github.com/QwenLM/qwen-code/pull/15435) — feat(web-shell): show tool arguments and result in expanded cards** *(BigDaddy1337)*
    Expanding a tool card now shows the actual call — arguments and result — for tools without a built-in detail view, instead of repeating the collapsed row's one-line summary. JSON objects/arrays are pretty-printed. Meaningful transcript debuggability win.

**Also worth watching:** [#14373](https://github.com/QwenLM/qwen-code/pull/14373) inline session rename + `F2`, [#13643](https://github.com/QwenLM/qwen-code/pull/13643) workspace pinning, [#13256](https://github.com/QwenLM/qwen-code/pull/13256) long diff line wrapping, [#15904](https://github.com/QwenLM/qwen-code/pull/15904) opt-in QQ bot message forwarding.

---

## 5. Hot Discussions

*Omitted — no Discussion data was provided in this dataset.*

---

## 6. Feature Request Trends

Distilled from the Issues and PRs above, four directions dominate:

1. **Web Shell information density & navigation** — the largest single cluster. Tool-card argument/result expansion (#15435), workspace pinning (#13643), inline session rename with `F2` (#14373), long-diff wrapping (#13256), and bounded pending-edit diffs (#13771) all point at the same complaint: the transcript and sidebar don't surface enough context at a glance, and long content gets clipped rather than made navigable.

2. **Remote & headless operation of `qwen serve`** — runtime remote-access toggle without restart (#15887), plus relaxed `--local-control-address` validation for enterprise intranets outside RFC 1918/3927 (#14140). Users want to drive a daemon running elsewhere without restart ceremonies.

3. **Managed Agent reliability as a first-class feature** — fault-injection arms (#15945), post-split verification gaps (#15927), and external workspace materialization (#15684). The volume here reads as hardening work driven directly by the CI failures in #14724 / #15173.

4. **Correctness at tool boundaries** — LSP explicit rejection instead of empty results (#15946), fd-duplication not counted as a file write (#15681), and ANSI/UTF-8-safe preview rings (#13725). The theme: tools should fail loudly or stay silent accurately, never emit misleading empties or spurious permission prompts.

Secondary: token/cost observability (#15433) and terminal UX on Windows (#15949).

---

## 7. Developer Pain Points

- **Opaque CI failures with no attributable test.** Both open CI blockers (#14724, #15173) carry the "no test identified" signature. #14724 has 100 comments and is tagged `autofix/skip` — the automation has given up, so a human must attribute the failure by hand. This is the highest-cost recurring frustration in the repo right now.

- **The `autofix/needs-human` queue is stalling.** #15274 and #15286 are infrastructure fixes that unblock Java SDK CI, and both are waiting on human review. Bot-authored PRs are being generated faster than they can be reviewed, so genuine CI improvements age out in the queue.

- **Review latency tied to PR hygiene.** The maintainer note prepended to #15169 makes the expectation explicit: PRs without a clear reviewer test plan get deprioritized. Contributors are being slowed by a documentation requirement rather than a technical one.

- **Windows CLI terminal rendering remains laggy in coverage.** #15949 (`/btw` overflow with no scroll or copy) is tagged across `scope/windows`, `scope/rendering`, and `roadmap/terminal-ux` — a P3 that keeps accumulating scope labels, suggesting the terminal-rendering rework is known but not yet scheduled.

- **Spurious permission prompts on standard shell idioms.** Until #15681 lands, `2>&1` triggers file-write permission checks — a constant interruption for anyone running build or test commands through the agent.

- **Silent empty results from unready tooling.** #15946 exists because LSP queries were returning empty rather than erroring when no language server was ready, causing the model to act on "no results" as if it were ground truth. Same pathology pattern users report in agentic debugging generally.

</details>