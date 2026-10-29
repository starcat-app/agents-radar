# AI CLI Tools Community Digest 2026-10-30

> Generated: 2026-10-29 18:48 UTC | Tools covered: 7

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

# Cross-Tool Comparison Report — AI CLI Ecosystem
**Data window:** 2026-10-29/30 · **Sources:** GitHub digests for Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, OpenCode, Pi, Qwen Code

---

## 1. Ecosystem Overview

The AI CLI category has moved past feature announcement into **reliability, governance, and cost-control engineering**. Across all seven tools, the highest-engagement threads are no longer about new capabilities but about silent failures (hangs, masked status, dropped state), opaque permission decisions, and prompt-cache/context economics. Two operating models are visible: **closed, maintainer-driven cores** (Claude Code, Copilot CLI, Codex) where PR throughput is near zero or bot-generated, versus **open contributor pipelines** (Gemini CLI, Qwen Code, OpenCode, Pi) where community PRs carry substantive fixes. Release cadence is decoupled from issue volume — OpenCode and Qwen Code shipping while Claude Code and Gemini CLI ship nothing — suggesting release trains are now gated by internal QA rather than community demand. Meanwhile, Windows and Linux/Wayland regressions dominate platform complaints in five of seven tools, making OS parity the practical adoption ceiling for enterprise rollout.

---

## 2. Activity Comparison

| Tool | Issues updated (24h) | PRs updated (24h) | Discussions | Release status (24h) |
|---|---|---|---|---|
| **Claude Code** | 49 | 2 (1 substantive, open ~7 months) | N/A | None |
| **OpenAI Codex** | n/d | ~50 (essentially all `copyberry[bot]`) | Active — Ideas, Q&A, Show & tell (~10 threads cited) | 2 alpha tags (`0.166.0-alpha.6`, `alpha.5.1.1`), empty changelogs |
| **Gemini CLI** | 46 | 37 | N/A | None |
| **GitHub Copilot CLI** | 38 | 0 | N/A | None |
| **OpenCode** | n/d | n/d (≥10 notable in flight) | N/A | **2 stable** (`v2.2.2`, `v2.2.1`) + `process-daemon v0.3.3` |
| **Pi** | n/d (10 covered) | 10 | 2 threads (1 Show & tell, 1 Q&A) | None |
| **Qwen Code** | 3 | 20+ (top-20 analyzed) | N/A | **CLI `v0.26.4` + SDK `0.1.26` + Desktop `0.26.4` + nightly** |

*N/A = no Discussions channel surfaced in the source data; all seven repos have Issues/PRs enabled, so N/A denotes channel absence, not inactivity. n/d = total not disclosed in digest; hot-issue/PR lists were curated rather than complete.*

**Read the ratios, not the totals:**

| Tool | Issue:PR ratio | Signal |
|---|---|---|
| Gemini CLI | 46 : 37 (1.2:1) | Healthy two-way community; contributors ship |
| Claude Code | 49 : 2 (24.5:1) | Maintainer-triage bottleneck; community PRs effectively not a channel |
| Copilot CLI | 38 : 0 | Fully closed development |
| Codex | PR-heavy, bot-authored | Automated merge train; not a community-contribution surface |

**Engagement depth:** Claude Code #1757 (89 comments / 77 👍) and OpenCode #59387 (104 comments) show the deepest sustained threads. Qwen Code's #14724 (84 comments, zero 👍) is automation noise, not engagement — a distinction worth making when scoring "community health."

---

## 3. Shared Feature Directions

Six requirements recur across three or more communities:

**1. Permission systems with deterministic policy and escape hatches** — *Claude Code, Codex, Gemini CLI, Copilot CLI, OpenCode*
- Codex: `decision = "prompt-user"` managed checkpoints (#58045) forcing human approval independent of saved approvals.
- Copilot CLI: default-deny + explicit allowlist for non-interactive mode (#5275); `--deny-tool` currently always overrides `--allow-tool`.
- Gemini CLI: `security.allowCommandSubstitution` opt-in (#30029); discourage destructive `git reset --force` (#22672).
- Claude Code: non-overridable PowerShell guard false positive (#73524) — the anti-pattern everyone else is fixing.
- OpenCode: `external_directory` enforced for file tools but **bypassed via shell** (#56288), with the tree-sitter removal PR (#60332) as the structural fix.
> **Shared need:** secure defaults *plus* an explicit, documented override — and a machine-readable reason when a command is blocked (Copilot #56722: "blocked by policy" with no rule identified).

**2. Agent/subagent observability and control authority** — *Claude Code, Codex, Gemini CLI, Copilot CLI*
- Claude Code: per-agent token/tool/model metrics removed from the desktop panel (#105831); subagent notification spam polluting parent context (#105928); undocumented Agent-tool suppression (#80988).
- Gemini CLI: surface subagent trajectories via `/chat share` (#22598); subagent context in `/bug` reports (#21763).
- Codex: Guardian review of injected commands (#58119), persisted parent-child relationships (#58129).
- Copilot CLI: `includeCoAuthoredBy: false` not inherited by subagents (#4576).
> **Shared need:** "users want to be the authority on delegation and to see what subagents actually did."

**3. Context budgeting, memory fidelity, and prompt-cache stability** — *Claude Code, Codex, OpenCode, Pi, Qwen Code*
- Claude Code: hardcoded 200-line/25KB memory window (#91188); **measured adherence drop from ~95% → ~72%** when only the index line loads (#105867).
- Pi: dynamic tool ordering re-bills the whole conversation (#10024, #11529); Anthropic server-side message threads to send only new messages (#11545).
- Qwen Code: immutable-context mode for slow-prefill self-hosted models (#14215).
- Codex: `codex.additional_context` count/byte/truncation metrics (#58144); cheaper models for memory maintenance (#58091).
- OpenCode: `/compact` without a context-fit check (#46164).
> **Shared need:** deterministic context assembly, visible truncation cost, prefix-cache preservation.

**4. Windows (and Linux/Wayland) platform parity** — *Claude Code, Codex, Gemini CLI, Copilot CLI, Pi*
- Codex: sandbox cannot spawn commands at all (HRESULT `0x80070020`, #55230) — the most severe single blocker in the dataset.
- Claude Code: Windows prompt-suggestion regression (#102208), plugin path mismatch (#105945), IdP lockouts from headless Chrome (#106003).
- Gemini CLI: Wayland browser subagent fails with `GOAL` success (#21983); Windows `fs.stat dev: 0` broke every secure file read (#30033).
- Copilot CLI: Windows Entra broker token cache (#5236).
- Pi: Windows/Zellij wheel scrolls history instead of transcript (#9656).
> **Shared need:** parity is the enterprise gate; Windows reports cluster on auth and sandbox path resolution specifically.

**5. Credential/secret handling as a first-class primitive** — *Claude Code, Codex, Copilot CLI, Pi*
- Codex #58148: secrets management should be core, not delegated to shell conventions — driven by infra/deploy/production use.
- Copilot CLI: keychain/secret-store failures across Ubuntu (`secret-tool`, 22 👍), macOS (XARA partitioning), Windows (Entra broker).
- Claude Code: `/feedback` submits transcripts by default, leaking secrets (#93138).
- Pi: OAuth credential resolution for summaries (#11556); per-request Bedrock client churn (#11527).

**6. Cost and quota transparency** — *OpenCode, Copilot CLI, Codex, Claude Code*
- OpenCode: hidden title/summary LLM calls billed but absent from session cost (#46371); 104-comment free-tier megathread (#59387).
- Copilot CLI: PRU quota wipeout linked to a feature toggle (#4802); 354K tokens of eagerly injected MCP schemas (+cost, #4613).
- Codex: predictable monthly usage resets (#57967); cheaper memory models (#58091).
- Claude Code: pooled usage across accounts for small teams (#92517).

---

## 4. Differentiation Analysis

| Tool | Focus | Target user | Technical approach |
|---|---|---|---|
| **Claude Code** | Deep interactive dev sessions; memory/prompt-authority transparency | Individual devs & teams on long-lived repos | Closed core, hook/plugin extension, aggressive auto-memory + agent-tool defaults; issue surface far exceeds PR surface |
| **OpenAI Codex** | Policy infrastructure for autonomous execution | Platform/enterprise teams, agent builders | Rust CLI + desktop + IDE; Guardian review, managed approval checkpoints, workspace-routed web search; alpha train with bot-authored PRs |
| **Gemini CLI** | Agent orchestration architecture | OSS contributors, power users w/ many MCP servers | Contributor-heavy; AST-aware code intelligence (tilth/glyph/ast-grep), OS-level sandboxing, subagent evaluation strategy |
| **Copilot CLI** | GitHub/enterprise identity + ACP interoperability | GitHub Enterprise orgs, third-party ACP clients (GitKraken) | Closed; ACP as the integration contract; entitlement-mapping bugs are the recurring failure mode |
| **OpenCode** | Product velocity + automation primitives | Builders, self-hosters, cost-sensitive teams | Fastest cadence; `/goal` objective loops, Code Mode schedule conditions, default image generation, MDM org policies |
| **Pi** | Minimal, provider-agnostic headless core | Extension authors, multi-provider/BYOK users | Small surface (agent loop + 7 tools + JSONL sessions); correctness-obsessed on prompt caching and provider quirks |
| **Qwen Code** | Self-hosted model economics + managed serving | Self-hosted/on-prem deployments, daemon workflows | Managed Agent Server (Maven modules), hybrid `tools.mode` (direct/code_mode), heavy CI investment |

**Notable divergences:**
- **PR throughput** is the sharpest structural divide: Gemini CLI (37) and Qwen Code (20+) treat community code as the delivery mechanism; Claude Code (2) and Copilot CLI (0) do not.
- **Memory strategy**: Claude Code bets on auto-memory with hardcoded budgets (and is being punished for opacity); Pi/Qwen treat context as an accounting problem to be made deterministic.
- **Safety posture**: Codex is *adding* human checkpoints and review infra; Gemini/OpenCode are *adding configurable off-switches* to existing blocks. Both converge on the same conclusion — hardcoded denial without explanation is the failure mode.
- **Monetization friction** is explicit only in OpenCode (free-tier/quota megathread, paid users blocked on "unlimited" models) and Copilot CLI (PRU accounting); the others abstract it behind plan entitlements.

---

## 5. Community Momentum & Maturity

**Tier 1 — High volume, high engagement**
- **Claude Code**: largest absolute debate (49 issues; top thread 89 comments/77 👍) but **structurally bottlenecked** — 2 PRs updated, one substantive fix open ~7 months. Mature product, immature contribution channel. Best signal-to-noise for *what users care about*; worst for *responsiveness*.
- **Gemini CLI**: best-balanced health in the set — 46 issues / 37 PRs, with PRs fixing high-blast-radius bugs (duplicate tool execution on retry #30020, `/restore` deleting ignored files #30034, `$`-pattern prompt corruption #30035). Caveat: the team's own eval layer is still unstable (#23166, #23313), so quality claims are not yet independently verifiable.

**Tier 2 — Strong velocity, narrower community**
- **OpenCode**: fastest shipping cadence — two stable releases in 24h plus a pty daemon. Engineering quality is high (permission scanner refactor, TLS trust, MDM policies), but free-tier/rate-limit opacity is the loudest community complaint. Momentum is high; trust is the open question.
- **OpenAI Codex**: heavy investment, minimal community voice. ~50 PRs in 24h, all bot-authored — this is an internal engineering firehose, not a community. Release hygiene is weak (two alpha tags, no changelog). Treat PR counts here as *maintainer activity*, not ecosystem health.
- **Qwen Code**: coordinated CLI+SDK+Desktop release train. But the top "issue" is bot noise (#14724, 84 comments, 0 👍), 2 autofix runs are wedged in `queued`, and 8+ of the top 20 PRs are CI repairs. **Iterating fast on infrastructure, not product** — only one net-new user feature (theme inheritance) in v0.26.4.

**Tier 3 — Small but high-signal**
- **Pi**: lowest volume, highest per-issue technical quality. Quantified failure reports (14× key latency at 400k entries, p50 1.5ms→21ms; 37.3 GiB-equivalent memory profiles; V8 OOM with 8 MB session files). Community-led Rust port (#11503) signals genuine architectural confidence. Best early-warning system for provider-compatibility issues.

**Tier 4 — Stalled contributor surface**
- **GitHub Copilot CLI**: 38 issues updated, **0 PRs**, and a flagship entitlement bug (#552) open since **November 2025** with 31 comments and no resolution. Enterprise-impacting failures (keychain across three OSes, 37 GiB process growth) suggest regression coverage is lagging release cadence (versions cited span `0.0.355` → `1.0.105`). Highest risk of the set for org-dependent workflows.

---

## 6. Trend Signals

**1. Agent status semantics are becoming a hard requirement.**
Gemini CLI reports `MAX_TURNS` as `GOAL` success (#22323) and browser subagent failure as `GOAL` success on Wayland (#21983); Claude Code's Remote Control 403 has no in-session recovery (#91717); OpenCode sessions hang at "Working" with no error (#58786, #60330). **Implication:** if you branch CI on agent status today, you will ship false positives. Verify status contracts before automating, and treat "success" as unverified until you have independent evidence.

**2. The permission model is now the product surface, not a safety checkbox.**
Codex managed checkpoints, Copilot allowlist requests, Gemini's `allowCommandSubstitution`, OpenCode's shell-bypass fix — all converge. The differentiator is no longer *whether* you block, but whether the block is **explained, overridable, and consistent across surfaces**. Copilot CLI's word-for-word failure ("blocked by policy," no rule, no recovery) is the template to design against.

**3. Prompt caching has become a P&L line item.**
Pi quantifies it: dynamic tool ordering and system-prompt head movement silently re-bill entire conversations (#10024, #11529). Claude Code quantifies the flip side: instruction adherence collapses 95%→72% under truncation (#105867). **Implication:** evaluate context-assembly determinism as a first-class selection criterion; ask vendors for cache-hit and truncation telemetry before committing to long sessions.

**4. ACP and MCP are consolidating into the real integration contracts.**
Copilot CLI's ACP requests are now filed by named third-party integrators (contextTier mid-session, `ask_user`, non-destructive `session/prompt`). MCP maturity issues are universal — Gemini's 128-tool hard ceiling (#24246), Copilot's 354K eager schema tokens (#4613), OpenCode's per-server TLS trust (#60039), Pi's `tool_search` namespacing (#11558). **Implication:** protocol parity is becoming a purchase criterion for teams building on top of these CLIs.

**5. Local resource management is an under-owned problem.**
OpenCode's `event` table reaching 13 GB (#33356), 37 GiB Copilot CLI processes (#5254), V8 OOM in Pi (#11570), orphaned MCP children (#46035, #46253). Every tool treats runaway local state as a bug rather than a bounded subsystem. **Implication:** plan disk/process guardrails and periodic state pruning in any long-running deployment.

**6. Platform parity is the enterprise adoption gate — and Windows is losing.**
Five of seven tools report Windows-first clusters, concentrated in sandbox execution, path resolution, and OS identity integration. Codex's #55230 (sandbox cannot spawn commands) and Claude Code's #106003 (headless Chrome locking IdP accounts) are rollout blockers, not annoyances.

**7. Release and CI automation is generating more noise than signal.**
Qwen Code's 84-comment bot issue, wedged autofix runs, cancelled-run false positives (#15852), placeholder changelogs; Codex's version-string-only alpha notes; Copilot's regression churn across minor versions. **Implication:** do not consume release notes at face value from this cohort — pin versions, bisect deliberately, and track issue trackers directly.

---

### Practical guidance for technical decision-makers

| If your priority is… | Lean toward | Because |
|---|---|---|
| Broadest ecosystem signal & feature discovery | **Claude Code** | Highest-engagement tracker; every major theme surfaces here first |
| Auditable autonomous execution | **OpenAI Codex** | Only tool shipping managed human-approval checkpoints (Guardian, `prompt-user`) |
| Contributing fixes and getting them merged | **Gemini CLI** | 1.2:1 issue:PR ratio; substantive correctness PRs land |
| Fast-moving product capability | **OpenCode** | Two stable releases in 24h; `/goal` loops, Code Mode schedules |
| Multi-provider / BYOK correctness | **Pi** | Only community publishing quantified cache and provider-quirk analysis |
| On-prem / self-hosted model economics | **Qwen Code** | Immutable-context roadmap explicitly targets slow prefill |
| GitHub Enterprise identity integration | **Copilot CLI** — with caution | Native GHE/Entra path, but open entitlement and keychain defects |

**Two caveats to carry into any evaluation:** (1) issues and PRs in Codex and Qwen Code are substantially automation-generated — raw counts are not community-health metrics; (2) in every tool, the most damaging defect class is the *silent* one (masked success, dropped session binding, no-error hangs), so weight observability and error-surfacing higher than feature checklists during trials.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights — as of 2026-10-30

> Note: PR comment counts were not populated in the supplied dataset. The ranking below follows the provided comment-sorted order and uses update recency, scope, and impact as secondary attention signals. All ranked PRs are **OPEN**.

## 1. Top Skills Ranking

1. **mcp-builder: MCP v2 compatibility fix — PR #1742**  
   [github.com/anthropics/skills/pull/1742](https://github.com/anthropics/skills/pull/1742)  
   Updates `mcp-builder` for `mcp>=2.0.0`, including the `streamable_http_client` rename and custom-header handling via `create_mcp_http_client` / `http_client`. High ecosystem-compatibility impact. **Status: OPEN.**

2. **skill-creator: trigger-eval reliability — PR #1298**  
   [github.com/anthropics/skills/pull/1298](https://github.com/anthropics/skills/pull/1298)  
   Isolates trigger evaluations and fixes Windows/runtime failures that can produce false misses or invalid scores. Addresses core Skill-authoring reliability. **Status: OPEN.**

3. **Notion spec-to-implementation + quantitative-resume-auditor — PR #1245**  
   [github.com/anthropics/skills/pull/1245](https://github.com/anthropics/skills/pull/1245)  
   Adds two Skills: one converts product/tech specs into Notion implementation tasks; the other audits quantitative resumes. Long-running submission with recent updates. **Status: OPEN.**

4. **proofcore-contract-auditor — PR #1771**  
   [github.com/anthropics/skills/pull/1771](https://github.com/anthropics/skills/pull/1771)  
   Web3 Skill for static analysis of Solidity/Rust smart contracts and cryptographic audit-proof anchoring on TON. Niche but clearly scoped. **Status: OPEN.**

5. **DOCX orphaned-comment detection — PR #1734**  
   [github.com/anthropics/skills/pull/1734](https://github.com/anthropics/skills/pull/1734)  
   Title indicates detection of orphaned comments in DOCX files; the PR summary is blank, so scope is inferred from the title. Document-quality automation theme. **Status: OPEN.**

6. **md2video-audio — PR #1703**  
   [github.com/anthropics/skills/pull/1703](https://github.com/anthropics/skills/pull/1703)  
   Converts Markdown documents into MP4 videos with voiceovers via Marp and related tooling. Represents demand for media-generation Skills. **Status: OPEN.**

7. **webapp-testing: remove `shell=True` risk — PR #1980**  
   [github.com/anthropics/skills/pull/1980](https://github.com/anthropics/skills/pull/1980)  
   Replaces unsafe `subprocess.Popen(..., shell=True)` usage in `with_server.py`, addressing command-injection risk (CWE-78). Security-relevant and recently updated. **Status: OPEN.**

8. **docx: LibreOffice timeout/error verification — PR #1792**  
   [github.com/anthropics/skills/pull/1792](https://github.com/anthropics/skills/pull/1792)  
   Makes `accept_changes.py` report LibreOffice timeouts as errors and verifies that revision marks are actually removed before claiming success. **Status: OPEN.**

## 2. Community Demand Trends

- **Trust, security, and namespace governance** — Issue [#492](https://github.com/anthropics/skills/issues/492) is the top discussion: community Skills distributed under the `anthropic/` namespace create impersonation and trust-boundary risks.  
- **Organization-wide Skill sharing and distribution** — Issue [#228](https://github.com/anthropics/skills/issues/228) asks for shared Skill libraries or direct sharing links instead of manual `.skill` file exchange.  
- **Reliable Skill triggering and evaluation** — Issue [#556](https://github.com/anthropics/skills/issues/556) reports `run_eval.py` / `claude -p` never triggering Skills, pointing to demand for dependable evaluation infrastructure.  
- **Agent memory and context efficiency** — Issue [#1329](https://github.com/anthropics/skills/issues/1329) proposes `compact-memory`, a symbolic-notation Skill for compact long-running agent state.  
- **Skill authoring quality and metadata** — Issues [#202](https://github.com/anthropics/skills/issues/202) and [#2064](https://github.com/anthropics/skills/issues/2064) focus on best practices, token efficiency, and descriptions that explain when to use a Skill.  
- **Agent governance and quality gates** — Issues [#412](https://github.com/anthropics/skills/issues/412) and [#1385](https://github.com/anthropics/skills/issues/1385) propose governance patterns, adversarial review, and delivery-verification pipelines.  
- **Plugin/package hygiene** — Issue [#189](https://github.com/anthropics/skills/issues/189) highlights duplicate Skills across `document-skills` and `example-skills`, causing context-window duplication.  
- **Document/office automation robustness** — Issues [#2018](https://github.com/anthropics/skills/issues/2018) and [#1868](https://github.com/anthropics/skills/issues/1868) show continued demand for correct DOCX XML handling and graphics utilities.

## 3. High-Potential Pending Skills

All are currently **OPEN**, selected for recent updates and practical impact:

- **PR #1980 — webapp-testing security hardening**  
  [github.com/anthropics/skills/pull/1980](https://github.com/anthropics/skills/pull/1980)  
  Removes a command-injection vector; updated 2026-10-25.

- **PR #1742 — mcp-builder MCP v2 compatibility**  
  [github.com/anthropics/skills/pull/1742](https://github.com/anthropics/skills/pull/1742)  
  Important for users on newer MCP versions; updated 2026-10-08.

- **PR #1245 — Notion spec + resume auditor Skills**  
  [github.com/anthropics/skills/pull/1245](https://github.com/anthropics/skills/pull/1245)  
  Substantive new-Skill submission; updated 2026-10-15.

- **PR #1681 — skill-creator direct execution support**  
  [github.com/anthropics/skills/pull/1681](https://github.com/anthropics/skills/pull/1681)  
  Fixes standalone `package_skill.py` execution and outdated usage paths; updated 2026-10-24.

- **PR #1997 — skill-creator YAML frontmatter parsing**  
  [github.com/anthropics/skills/pull/1997](https://github.com/anthropics/skills/pull/1997)  
  Fixes metadata corruption in evaluation/description optimization; updated 2026-10-19.

- **PR #1975 — pptx `--cols` validation**  
  [github.com/anthropics/skills/pull/1975](https://github.com/anthropics/skills/pull/1975)  
  Small but user-visible CLI fix; updated 2026-10-27.

- **PR #1730 — claude-api dead URL replacement**  
  [github.com/anthropics/skills/pull/1730](https://github.com/anthropics/skills/pull/1730)  
  Documentation reliability fix with verified replacement URLs; updated 2026-10-04.

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is not simply more Skills, but trustworthy, reliable, shareable, and well-governed Skills — especially around namespace security, trigger/eval correctness, authoring quality, and robust document/tooling integrations.**

---

# Claude Code Community Digest — 2026-10-30

## 1. Today's Highlights
No new releases landed in the last 24 hours, but issue traffic stayed high (49 issues updated). The long-running authentication complaint (#1757) remains the most-engaged thread at 89 comments/77 👍, while a freshly filed memory-fidelity report (#105867) and the *heron_brook* Agent-tool suppression bug (#80988) kept prompt/agent-control transparency at the center of discussion. Platform-specific regressions — Windows hook/plugin failures and headless Chrome triggering IdP lockouts — are the fastest-growing category of new reports.

## 2. Releases
None in the last 24 hours.

## 3. Hot Issues

1. **[#1757](https://github.com/anthropics/claude-code/issues/1757) — Claude Code requires users to constantly login** (89 comments, 77 👍)
   Still the highest-engagement open bug on the tracker. Users report being forced through web re-authentication almost daily. The volume and age (open since June 2025) make this the clearest signal that session persistence is a top-tier reliability gap.

2. **[#80988](https://github.com/anthropics/claude-code/issues/80988) — `heron_brook` prompt section disables Agent-tool dispatch for Opus 5 only** (38 comments, 72 👍)
   A versioned system-prompt section silently overrides user-configured delegation policy with no opt-out. High reaction count reflects frustration less about the default itself than about *undocumented, model-specific behavior changes*. Related report #84183 was closed, concentrating discussion here.

3. **[#91188](https://github.com/anthropics/claude-code/issues/91188) — Make the auto-memory `MEMORY.md` compaction reminder threshold configurable** (60 comments)
   The 200-line/25KB auto-load window is hardcoded, and users hitting it get nagged rather than offered control. Sustained comment volume suggests many teams are operating at the boundary of the current memory budget.

4. **[#105867](https://github.com/anthropics/claude-code/issues/105867) — Output-format rule from auto-memory followed only ~72% of the time when just the index line is loaded** (new, 4 comments)
   A quantified reliability finding: instruction adherence drops from ~95% (full memory file in context) to ~72% (index line only). Directly relevant to anyone relying on persistent conventions, and a good complement to #91188.

5. **[#93201](https://github.com/anthropics/claude-code/issues/93201) — Built-in browser ignores Allowed sites for internal hostnames (`*.local`)** (15 comments, 30 👍)
   Site-level permissions are disabled for internal hostnames, so users get a prompt on *every* action against local dev/staging hosts. Notably painful for teams testing on `.local` domains behind an allowlist.

6. **[#73524](https://github.com/anthropics/claude-code/issues/73524) — PowerShell `Remove-Item on system path` guard over-blocks legitimate commands** (10 comments)
   The AST analyzer mis-attributes an unrelated token as the delete target, and the guard is non-overridable. Classic static-analysis false positive with no escape hatch.

7. **[#102208](https://github.com/anthropics/claude-code/issues/102208) — Prompt suggestions never appear (Windows, v2.1.296/v2.1.300)** (8 comments, 8 👍)
   Regression confirmed by multiple users on both TUI and desktop, with `/config` showing the feature enabled and no env var override set. Clean, reproducible regression report.

8. **[#106003](https://github.com/anthropics/claude-code/issues/106003) — Headless `chrome.exe` on Windows triggers failed logons and locks IdP-managed accounts** (new)
   Each headless HTML→PDF/PNG invocation causes a burst of failed logon attempts in JumpCloud-managed environments, escalating to account lockouts. Security/IT-impacting and likely to affect enterprise rollouts.

9. **[#105945](https://github.com/anthropics/claude-code/issues/105945) — `security-guidance` plugin hook blocks all prompts on Windows desktop** (new)
   `claude auth status` returns non-JSON because `claude.exe` is not found under `AppData\Roaming\Claude\claude-code`, so every prompt is blocked. Path-resolution mismatch between plugin expectations and desktop-app install layout.

10. **[#91717](https://github.com/anthropics/claude-code/issues/91717) — Remote Control fails with HTTP 403 after Desktop update; `/remote-control` retry does not recover** (8 comments)
    Cross-platform (Windows/macOS) auth failure with no working recovery path in-session — requires a full restart. Fits the broader auth-reliability theme.

*Also worth watching:* [#92517](https://github.com/anthropics/claude-code/issues/92517) (pool usage across accounts / shared session context), [#105928](https://github.com/anthropics/claude-code/issues/105928) (background subagents waking parent on every tick), [#93138](https://github.com/anthropics/claude-code/issues/93138) (redact secrets from feedback transcripts), [#105831](https://github.com/anthropics/claude-code/issues/105831) (restore per-agent model/token/tool counts in Desktop workflow panel).

## 4. Key PR Progress
Only **2 pull requests** were updated in the last 24 hours, so this section is inherently thin:

1. **[#32751](https://github.com/anthropics/claude-code/pull/32751) [OPEN] — fix(hookify): map stop/prompt events to correct field names**
   Fixes #32153. Hookify rules using the simple `pattern` syntax with `event: stop` or `event: prompt` never fire, because `config_loader.py` maps them to `field='content'`, which `rule_engine._extract_field()` cannot resolve for Stop/UserPromptSubmit events (it only handles `content` for Write-style events). Open since March 2026 — a small but high-leverage fix for anyone authoring hook rules.

2. **[#57333](https://github.com/anthropics/claude-code/pull/57333) [CLOSED] — Update README.md**
   Documentation-only change; closed without further detail.

> Observation: community PR throughput appears very low relative to issue volume (49 issues vs. 2 PRs updated), and the one substantive fix has been open for ~7 months. Worth flagging for maintainer triage capacity.

## 5. Hot Discussions
Omitted — no discussion data was provided in this dataset.

## 6. Feature Request Trends

- **Configurable memory & context budgeting.** #91188 (compaction threshold) and #105867 (index-only adherence) point to demand for explicit control over what auto-memory loads and when it warns — plus visibility into *how much* fidelity is lost by truncation.
- **Agent/subagent control and observability.** #80988 and #84183 (opt-out from Agent-tool suppression), #86089 (resumable agent sessions in workflows), #105928 (notification noise), #105831 (per-agent tokens/tools/model in the desktop panel). The theme: users want to be the authority on delegation policy and to see what subagents actually did.
- **Desktop/UI polish and parity.** #102699 (sidebar theming/user CSS, bolder project headings), #105189 (unread/running status for Chat tab), #105985 (cwd in the status line for multi-session clarity), #26784 (drag-and-drop files without Shift), #91697 (Wayland focus-stealing).
- **Multi-account and team ergonomics.** #92517 asks for pooled usage across subscriptions and shared session context for small teams working one project.
- **Consent and privacy in the feedback pipeline.** #93138 (redact secrets), #103863 (send feedback with no session context), #87955 (structured idea channel with opt-in transcript sharing).
- **Headless/CI configurability and documentation.** #104929 requests a documented way to skip all `CLAUDE.md` files in `claude -p` runs while retaining project skills.
- **Platform/browser coverage.** #90414 (Firefox extension), plus internal-hostname support in #93201.

## 7. Developer Pain Points

1. **Authentication doesn't persist.** #1757 (daily re-login) and #91717 (unrecoverable 403 in Remote Control) are the two most disruptive reliability issues; both require abandoning the session to recover.
2. **Silent system-prompt behavior changes.** #80988/#84183 — model-scoped directives that override user configuration with no changelog entry and no opt-out. This erodes trust more than the behavior itself.
3. **Memory system is opaque and lossy.** Hardcoded thresholds (#91188) plus a measurable adherence drop when only the index line is loaded (#105867) make persistent conventions unpredictable.
4. **Windows is the weakest platform.** Prompt-suggestion regression (#102208), PowerShell guard false positives (#73524), plugin path resolution failure (#105945), missing `mcp__claude-in-chrome__file_upload` in new chats (#105868), and IdP account lockouts from headless Chrome (#106003).
5. **Over-broad safety guards without override.** #73524 — static analysis blocks legitimate commands and offers no escape hatch, pushing users to disable tooling entirely.
6. **Subagent notification spam.** #105928 — background subagents waiting on their own Monitor/background shell wake the parent on every tick with identical "Waiting." messages, polluting the parent's context.
7. **Secrets can leak through `/feedback` defaults.** #93138 — transcripts default to being submitted, and leaked secrets are only avoidable if you notice the toggle.
8. **Docs gaps for headless workflows.** #104929 — no documented flag matrix for selectively loading skills vs. `CLAUDE.md` in `-p` mode.
9. **Desktop regressions with no diagnostic surface.** #105831 — per-agent token/tool metrics were removed from the workflow panel; #105189 — Chat tab lacks running/unread status that Code sessions have.

---
*Data window: issues and PRs updated 2026-10-29. No releases or discussions were available for this period.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-10-30

**Source:** [github.com/openai/codex](https://github.com/openai/codex) · Data window: last 24h (through 2026-10-29)

---

## 1. Today's Highlights

Two Rust alpha releases shipped (0.166.0-alpha.6 and 0.166.0-alpha.5.1) with no published changelog, while the PR queue shows a heavy, bot-authored push around **Guardian review**, **managed command approval checkpoints**, and **web-search/tool-call plumbing**. On the issue side, the day's volume is dominated by **Windows sandbox and command-execution failures**, **browser/extension integration fragility**, and a growing cluster of **safety-guardrail false positives** on legitimate C/C++ and Git work.

---

## 2. Releases

- **[rust-v0.166.0-alpha.6](https://github.com/openai/codex/releases)** — `0.166.0-alpha.6`, release notes contain only the version string (no substantive changelog).
- **[rust-v0.166.0-alpha.5.1](https://github.com/openai/codex/releases)** — `0.166.0-alpha.5.1`, patch-level bump on the 0.166 alpha line; no documented changes.

> Both are pre-release alpha tags. No stable-channel release in the last 24h; treat as CLI/engine iteration rather than user-facing feature announcements.

---

## 3. Hot Issues

1. **[#54532](https://github.com/openai/codex/issues/54532)** — `[Windows][Computer Use] zh-CN document-role URL detection failure on @oai/sky 0.7.8` (12 comments). Highest-engagement issue of the day: on Chinese-language Windows, native Computer Use can enumerate Chrome/Edge windows but fails when acquiring window state with a browser-URL confidence error. A narrowly scoped document-role predicate fix reportedly restores both browsers — a strong signal that locale-dependent role heuristics are the root cause.

2. **[#36319](https://github.com/openai/codex/issues/36319)** — `[macOS] ChatGPT Chrome extension unavailable in Chrome Web Store` (9 comments). The official listing returns "This item cannot be purchased or downloaded" despite a healthy Codex Chrome plugin and native host. Long-running (created July) and unresolved, which is eroding trust in the browser-extension install path.

3. **[#57107](https://github.com/openai/codex/issues/57107)** — `[Windows][Desktop][IAB] Attached tab loses browser-session binding before action` (8 comments). The built-in browser (IAB) attaches a tab successfully, then rejects the next action because the tab is "no longer part of the browser session." Silent state loss in the agent's browser-control loop is a correctness risk for any automation built on IAB.

4. **[#55230](https://github.com/openai/codex/issues/55230)** — `[Windows] Codex App sandbox fails to execute commands (HRESULT 0x80070020)` (7 comments). Windows 11 25H2 + Codex 26.1013.40934, Plus plan: the app sandbox cannot spawn commands. This is the highest-severity Windows blocker reported this window — the app is effectively unusable for local task execution.

5. **[#34455](https://github.com/openai/codex/issues/34455)** — `Make request_user_input timeout duration and behavior configurable` (6 comments, **22 👍**). The most-upvoted issue in the set. `request_user_input` auto-resolves after a fixed 60s grace + 60s countdown and submits an empty answer. Developers want the timer and timeout outcome configurable rather than silently guessing on their behalf.

6. **[#43197](https://github.com/openai/codex/issues/43197)** — `Windows: deleting archived Codex chats fails despite enabled delete button` (6 comments). UI state and backend disagree — the button is active, deletion silently fails. Contributes to the "Windows feature parity and state consistency" theme.

7. **[#57620](https://github.com/openai/codex/issues/57620)** — `[macOS] Worktree icons missing from sidebar after updating to 26.1023.50603` (5 comments, **5 👍**). Fresh regression on the latest desktop build; small surface, but it's a visible workflow break for anyone using multiple git worktrees.

8. **[#34070](https://github.com/openai/codex/issues/34070)** — `Codex Windows App uses hardcoded %USERPROFILE%\.codex — ignores CODEX_DIR / CODEX_HOME` (5 comments). App/CLI config divergence: the CLI honors the env vars, the desktop app does not. A concrete disk-management blocker for constrained Windows machines, and a broader architectural inconsistency between runtimes.

9. **[#57759](https://github.com/openai/codex/issues/57759)** — `[Linux/Wayland] Codex 26.1021.22027 fails to start UI and freezes VS Code 1.143.1` (4 comments, **1 👍**). Reproducible regression with a confirmed working downgrade (26.908.40401). A hard freeze of the host IDE is the worst failure mode for an extension, and the downgrade bisect gives maintainers a clean repro.

10. **[#58148](https://github.com/openai/codex/issues/58148)** — `Credential security and authorization should be a core Codex capability` (1 comment, filed 10-29). Filed by a user running Codex for real DevOps work (infra management, deploys, production debugging, high-value API keys). Argues secrets handling should be a first-class primitive rather than delegated to shell conventions — a directionally important request as usage shifts from codegen to operations.

---

## 4. Key PR Progress

> Note: essentially all 50 PRs updated in this window are authored by `copyberry[bot]`, indicating an automated/agent-authored merge train. Reviewed below are the substantive behavior changes.

1. **[#58147](https://github.com/openai/codex/pull/58147)** — *Return standalone web search failures to the model.* Standalone search errors currently abort the turn as fatal; this converts client setup errors and failed requests into unsuccessful tool outputs the model can reason about and recover from. Meaningfully improves agent resilience.

2. **[#58140](https://github.com/openai/codex/pull/58140)** — *Route standalone web search through the thread's workspace context.* Fixes requests being sent to the bootstrap backend instead of the discovered workspace backend, bypassing workspace routing.

3. **[#58125](https://github.com/openai/codex/pull/58125)** — *Support negotiated server-side truncation in Code Mode clients.* Adds truncation negotiation for stdio and gRPC so oversized output — including script errors — is bounded before crossing the transport instead of being capped host-side.

4. **[#58045](https://github.com/openai/codex/pull/58045)** — *Add managed command checkpoints requiring fresh human approval.* Introduces `decision = "prompt-user"` in managed `requirements.toml` prefix rules, forcing a human decision independent of automatic review, hook allowances, and saved approvals. The clearest policy-control addition in the batch.

5. **[#58119](https://github.com/openai/codex/pull/58119)** — *Add experimental Guardian review for injected thread commands.* Exposes `thread/guardianReview` to assess an idle thread's final injected `exec_command` without executing it, returning the call ID plus assessment (or `null` when exec policy skips approval).

6. **[#58075](https://github.com/openai/codex/pull/58075)** — *Use serving assessments for adaptive Guardian review.* Matches final serving assessments to responses/output items and reuses them instead of asynchronous scoring, so low-risk actions can be fast-pathed.

7. **[#58040](https://github.com/openai/codex/pull/58040)** — *Preserve native tool-call evidence through Guardian review.* Retains original function-call metadata even when the call has aged out of live history — required to review encrypted multi-agent messages correctly.

8. **[#58122](https://github.com/openai/codex/pull/58122)** — *Add an incremental exec tools feature flag.* Registers `incremental_exec_tools` as an under-development, default-off feature exposed in the config schema — the scaffolding for incremental tool exposure.

9. **[#58091](https://github.com/openai/codex/pull/58091)** — *Update default models for memory extraction and consolidation.* Switches to `gpt-6-luna` for extraction and `gpt-6.1-terra` for consolidation when the provider doesn't mandate a backend-specific ID — i.e., cheaper/smaller models for memory maintenance.

10. **[#58129](https://github.com/openai/codex/pull/58129)** — *Persist subagent relationships before creating child storage.* Prevents orphaned child history that parent-subtree deletion can't discover; a relationship-write failure now rejects the spawn.

*Also notable:* [#58144](https://github.com/openai/codex/pull/58144) (new `codex.additional_context` count/byte/truncation metrics), [#58121](https://github.com/openai/codex/pull/58121) (centralized provider request auth checks with retry on credential change), [#58134](https://github.com/openai/codex/pull/58134) (model-migration guidance prefers documented replacements), [#58110](https://github.com/openai/codex/pull/58110) (scoped RUSTSEC-2026-0418 ignore for Windows-only `libz-sys`).

---

## 5. Hot Discussions

### Ideas
- **[#30332](https://github.com/openai/codex/discussions/30332)** — *Background updates for Codex CLI without blocking startup.* Proposes a Claude Code–style flow: check/download in the background, prompt to restart when ready, instead of forcing an update decision at launch. Startup friction is a recurring complaint across CLI tools.
- **[#57967](https://github.com/openai/codex/discussions/57967)** — *1–2 free Codex usage resets per month for ChatGPT Plus.* Asks for the currently promotional resets to become a predictable monthly allowance; framed as retention/plan-value rather than an entitlement demand.

### Q&A
- **[#8582](https://github.com/openai/codex/discussions/8582)** — *Search/Find in the active chat history* (4 👍). `Ctrl-F` always targets the code editor regardless of focus; no search context menu exists in the Codex canvas. Basic navigability gap that grows with conversation length.
- **[#5210](https://github.com/openai/codex/discussions/5210)** — *Any way to clear the text area?* No discovered shortcut for clearing the prompt input after an accidental large paste — small UX papercut, long-lived thread.

### Show and tell
- **[#57746](https://github.com/openai/codex/discussions/57746)** — *Zozo: an inspectable issue-to-PR example and a review checklist for coding-agent work.* Ships a public issue/diff/CI trace plus a checklist for vetting agent output. Useful pattern for teams that need auditable agent runs.
- **[#57591](https://github.com/openai/codex/discussions/57591)** — *toli — let Codex and Claude Code collaborate, even on different machines.* Apache-2.0 tool for direct agent-to-agent communication across developers' machines, motivated by divergent local context during pair debugging.
- **[#58093](https://github.com/openai/codex/discussions/58093)** — *OpenFusion: orchestrator and router for subtask handling.* Routes each subtask to the cheapest capable model with a judge step that escalates on poor results — cost-optimization around Codex/agent workloads.
- **[#58104](https://github.com/openai/codex/discussions/58104)** — *Kilobat: networking for AI agents (and humans).* macOS menu-bar network monitor that tracks Codex, Claude Code and Gemini traffic, with an open-source CLI + MCP so agents can inspect network state themselves.
- **[#56337](https://github.com/openai/codex/discussions/56337)** — *Off the Wall: recall your past corrections before Codex answers.* MIT-licensed, keeps corrections in the user's own words and quotes them back to Codex or Claude Code — a lightweight persistent-preference layer.
- **[#58031](https://github.com/openai/codex/discussions/58031)** — *Using Codex with current Alibaba Cloud documentation and official citations.* Reports that generated cloud config is plausible but needs verification against live endpoints/regions/models — an argument for grounded doc retrieval in domain-specific work.

---

## 6. Feature Request Trends

- **Configurability of agent behavior.** The top-upvoted issue (#34455, 22 👍) wants configurable `request_user_input` timeouts; #34070 wants `CODEX_HOME`/`CODEX_DIR` respected; #58127 (PR) makes tooltips honor a preference. Theme: stop hardcoding policy and UI defaults.
- **Desktop/CLI parity and consistent state.** Env-var handling, cloud-environment discovery (#58145: CLI picker returns `HTTP 200 []` while desktop shows a published env), and archived-chat deletion (#43197) all point at divergent code paths between surfaces.
- **Platform parity, especially Windows.** Computer Use (#54532, #57371), sandbox execution (#55230), policy denial messaging (#56722), `/approve` discoverability (#57350), file/PDF access (#58139) — the largest single cluster in the window.
- **Transparent, actionable safety and policy errors.** #58138 and #58141 (both 10-29) report cybersecurity guardrails blocking ordinary C/C++ and local Git integration work; #56722 asks for the blocking rule and a recovery path instead of "blocked by policy."
- **Credential and secret management as a first-class capability** (#58148) — driven by usage shifting into infra/deploy/production work.
- **Browser and extension integration robustness** — Chrome Web Store availability (#36319), IAB session binding (#57107), unsupported extension sidebars (#58133).
- **IDE ergonomics** — in-chat search (#8582), clear-input shortcut (#5210), respecting the default editor for file links (#47702).
- **Cost/usage flexibility** — predictable usage resets (#57967) and community-built routing to cheaper models (#58093).
- **Non-blocking update flows** for CLI (#30332).

---

## 7. Developer Pain Points

- **Windows is the weakest surface.** Command execution inside the app sandbox fails outright (HRESULT `0x80070020`, #55230); authorized commands are rejected as "blocked by policy" with no rule identified and no recovery action (#56722); `/approve` is undocumented-in-UI and returns "no command found" (#57350). Multiple independent reports converge on the same experience: the permission system says no, and won't say why.
- **Safety guardrails produce false positives on ordinary work.** Two reports in a single day (#58138 C/C++; #58141 local Git integration) describe repeated interruptions of plainly authorized development tasks by cybersecurity filters — a direct productivity tax that also undermines trust in the approval flow.
- **Silent state and cache bugs.** IAB drops the tab's session binding before an action (#57107); PDF refresh keeps stale content because the cache key omits `conversationId` (#56862); archived-chat deletion no-ops (#43197). Silent failures are costly in agent workflows because the agent, not the human, is the one observing them.
- **Regressions land on the stable desktop channel.** Worktree icons vanish in 26.1023.50603 (#57620); the VS Code extension freezes the whole IDE on Linux/Wayland in 26.1021.22027 (#57759, fixed only by downgrading). Users are effectively debugging release gating.
- **Configuration is not honored consistently.** The desktop app ignores `CODEX_DIR`/`CODEX_HOME` (#34070) and, per #58145, disagrees with the CLI about which cloud environments exist — forcing users to duplicate or manually sync setup.
- **Extension distribution is unreliable.** A months-old Chrome Web Store outage (#36319) blocks the documented install path, and unsupported extension sidebars (#58133, OKX Wallet) narrow what the built-in browser can host.
- **Locale-specific breakage.** Incomplete zh-CN localization (#27255) and zh-CN-only Computer Use failures (#54532) suggest locale handling is under-tested outside en-US.
- **Long-conversation navigability and input control remain unaddressed.** No in-chat search (#8582) and no clear-input shortcut (#5210) are small requests with outsized daily cost, and both threads are months old.

---

*Prepared as an analyst digest. Alpha release notes were empty in the source data; PR intent is inferred from titles and descriptions.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-10-30

## Today's Highlights
No new releases shipped in the last 24 hours, but community activity remained heavy: 46 issues and 37 PRs were updated, with the bulk of attention still on agent/subagent reliability. Two P1 agent bugs — misleading `MAX_TURNS` success reporting (#22323) and the generalist agent hanging indefinitely (#21409) — continue to draw the most discussion and reactions. On the PR side, contributors pushed a broad set of hardening fixes around checkpoint/restore correctness, shell-substitution security, retry deduplication, and CI test coverage.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent `MAX_TURNS` reported as `GOAL` success (P1)**
   A `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` despite its own output saying it hit the turn limit before performing analysis. This is a correctness/trust problem for any automation that branches on agent status. 13 comments and 2 👍 make it the most-discussed issue of the window.

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever (P1)**
   Simple operations like folder creation hang indefinitely once the CLI defers to the generalist agent; users report waiting up to an hour. The workaround — instructing the model not to use subagents — is telling, and with 8 👍 it's the highest-reacted issue in this batch.

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Zero-dependency OS sandboxing + post-execution intent routing (P2, effort/large)**
   Proposes leaning into Gemini 3's native bash affinity by letting models chain POSIX tools (`grep`, `sed`, `awk`) inside an OS-level sandbox, then routing on post-execution intent. This is the architectural counterpoint to the safety concerns raised elsewhere. 9 comments, 1 👍.

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini under-uses skills and subagents**
   Anecdotal but widely resonant: the model won't invoke custom skills (`gradle`, `git`) or subagents unless explicitly told, even when highly relevant. Directly undermines the value of the extensibility surface. 7 comments.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — EPIC: assess AST-aware reads, search, and codebase mapping (P2)**
   Parent epic investigating whether AST-aware tooling reduces misaligned reads, cuts turns, and trims token noise. Related investigations (#22746, #22747) are tracking `tilth`/`glyph`/`ast-grep` as candidates. 7 comments.

6. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 400 error when >128 tools are available (P2)**
   The CLI surfaces a 400 once the enabled tool count crosses the threshold, with no graceful scoping. A hard scalability ceiling for users with many MCP servers or extensions. 3 comments.

7. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent should stop/discourage destructive behavior (P2)**
   The model reaches for `git reset` or `--force` when safer alternatives exist, and lacks guardrails around destructive DB/resource operations. Security-adjacent and likely to shape policy work. 3 comments, 1 👍.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland (P1)**
   The browser subagent terminates with `Termination Reason: GOAL` on Wayland sessions, i.e., a failure masked as success — the same reporting pattern as #22323. Linux/Wayland users are effectively blocked from browser automation. 4 comments.

9. **[#22267](https://github.com/google-gemini/gemini-cli/issues/22267) — Browser Agent ignores `settings.json` overrides (P2)**
   `AgentRegistry` merges settings correctly at init, but the Browser Agent bypasses them entirely — including `maxTurns`. Config drift of this kind is especially confusing when combined with the hang/turn-limit issues above. 4 comments.

10. **[#23571](https://github.com/google-gemini/gemini-cli/issues/23571) — Model litters workspace with temp scripts (P2)**
    When restricted to shell execution, the model generates edit scripts across arbitrary directories, creating cleanup overhead before any clean commit. A concrete workflow tax on shell-only configurations. 3 comments.

*Also worth watching:* [#20079](https://github.com/google-gemini/gemini-cli/issues/20079) (symlinked agent files not recognized), [#22598](https://github.com/google-gemini/gemini-cli/issues/22598) (surface subagent trajectories via `/chat share`), [#22741](https://github.com/google-gemini/gemini-cli/issues/22741) (background local agents via Ctrl+B, 2 👍).

---

## Key PR Progress

1. **[#30034](https://github.com/google-gemini/gemini-cli/pull/30034) — Honor `.git/info/exclude` and `core.excludesFile` in shadow repo**
   Fixes a data-loss class of bug where `/restore` reverted or deleted files that should have been ignored under Git config rules. Important for anyone using checkpointing with local-only excludes.

2. **[#30035](https://github.com/google-gemini/gemini-cli/pull/30035) — Prevent `$`-pattern corruption in LLM prompt templates (P2)**
   Migrates `summarizer.ts`, `llm-edit-fixer.ts`, and `sessionSummaryService.ts` from `String.replace(placeholder, value)` to a single-pass `safeTemplateReplace()`, eliminating dynamic-value interpretation bugs in prompt construction.

3. **[#30031](https://github.com/google-gemini/gemini-cli/pull/30031) — Gate background log stream init on execution lifecycle (P2)**
   Addresses a model-config edge case when `gemini-2.5-flash` is explicitly selected alongside `useLatestFlash` and dynamic model configuration. Prevents premature log-stream initialization.

4. **[#30023](https://github.com/google-gemini/gemini-cli/pull/30023) — Run SDK tests in PR CI, fix `AgentLoopContext` mock (P2)**
   Re-enables 6 skipped `GeminiCliSession.sendStream()` tests and adds the SDK package to the `others` CI shard. Meaningful reduction in untested surface area.

5. **[#29918](https://github.com/google-gemini/gemini-cli/pull/29918) — Report working/blocked/idle status via OSC 7501**
   The TUI now emits terminal program-status reports so multiplexer tabs can show which session needs attention. A quality-of-life win for multi-session workflows (size/xl).

6. **[#30020](https://github.com/google-gemini/gemini-cli/pull/30020) — Drop tool calls streamed by failed attempts on retry**
   On mid-stream retries, both the failed and successful attempts' `ToolCallRequest` events were being executed — meaning side-effecting commands could run twice. High-value correctness fix for the agent loop.

7. **[#30029](https://github.com/google-gemini/gemini-cli/pull/30029) — Make command-substitution blocking user-configurable (P3, help wanted)**
   Adds `security.allowCommandSubstitution` (default `false`) to replace the hardcoded block on `$()`, backticks, and process substitution in the shell tool. Fixes #27393; trades convenience against a deliberate safety default.

8. **[#30026](https://github.com/google-gemini/gemini-cli/pull/30026) — Treat project temp paths as local in untrusted-flag checks**
   Stops the CLI from prompting for confirmation on its own helper scripts under `~/.gemini/tmp/<project>/...`, a recurring friction point after shell output leaks script paths into context.

9. **[#30019](https://github.com/google-gemini/gemini-cli/pull/30019) — Preserve session history during tool output masking**
   Prevents the first user prompt from being dropped when resuming sessions whose tool outputs were masked, by not writing the API-shaped `getHistory()` view back into storage.

10. **[#29977](https://github.com/google-gemini/gemini-cli/pull/29977) — Honor cancellation in `read_background_output` (P2, help wanted)**
    The tool previously ignored its abort signal and would sleep out the full `delay_ms` before reading anyway. Complements [#29978](https://github.com/google-gemini/gemini-cli/pull/29978), which fixes dropped boundary/oversized lines in the same tool.

*Also merged/closed this window:* [#30012](https://github.com/google-gemini/gemini-cli/pull/30012) (429 cool-down countdown in the loading indicator), [#30006](https://github.com/google-gemini/gemini-cli/pull/30006) (PowerShell CIM fallback for Windows IDE process lookup), [#29989](https://github.com/google-gemini/gemini-cli/pull/29989) (`\n` escape corruption across core/cli), [#30024](https://github.com/google-gemini/gemini-cli/pull/30024) (undici 7.10.0 → 7.30.1).

---

## Feature Request Trends

- **Agent orchestration maturity.** The largest cluster by far: backgroundable local agents (#22741), shared memory / parallel subagent collaboration (#18287), delegating build-fix loops to the generalist (#22602), and a dedicated subagent eval strategy (#22601). Subagents are clearly the strategic center of gravity.
- **Observability and debuggability.** Requests for subagent trajectories in `/chat share` (#22598), subagent context in `/bug` reports (#21763), and better agent "self-awareness" of its own flags and hotkeys (#21432) all point to the same gap: users can't see what the agent is doing.
- **Token-efficient, structure-aware code intelligence.** The AST epic (#22745) plus #22746/#22747, "Tactful Extraction" (#19561), and persistent file-based task tracking (#18836) form a coherent push to reduce context bloat and context rot.
- **Safety with escape hatches.** Sandboxed native bash (#19873), discouraging destructive git/DB commands (#22672), and configurable command substitution (#30029) suggest the community wants secure defaults *plus* explicit opt-outs.
- **Browser agent resilience.** Session takeover/lock recovery (#22232) and respecting `settings.json` (#22267) are recurring asks from anyone running persistent browser sessions.
- **Policy granularity.** Per-workspace policy autoaddition (#18397) reflects demand for repo-scoped rather than global trust decisions.

---

## Developer Pain Points

- **Silent hangs and masked failures.** The two dominant P1s — the generalist agent hanging (#21409) and `MAX_TURNS` being reported as `GOAL` success (#22323, and the same pattern in #21983) — are the most damaging class of bug because they defeat scripting, CI, and user trust simultaneously.
- **Configuration that isn't honored.** The Browser Agent ignoring `settings.json` (#22267) and symlinked agent files being silently skipped (#20079) both produce "I configured it correctly and nothing happened" experiences with no diagnostic signal.
- **Scale ceilings on tooling.** The 400 error past the tool threshold (#24246) punishes exactly the power users who invest in MCP servers and extensions.
- **Workspace hygiene.** Temp scripts scattered across directories (#23571) and `/restore` touching ignored files (#30034) both turn a clean commit into manual cleanup.
- **Platform-specific breakage.** Wayland browser failures (#21983) and Windows path/process issues (#30033, #30006) recur; Windows `fs.stat` returning `dev: 0` on Node 22.12–22.16/23.x caused *every* secure file read to fail before #30033.
- **Correctness bugs in the agent loop itself.** Double execution of tool calls on retry (#30020), `\n` escape corruption (#29989), and `$`-pattern mangling in prompt templates (#30035) are low-level but high-blast-radius — they silently alter behavior rather than failing loudly.
- **Evaluation infrastructure is not yet trustworthy.** #23166 ("evals bleed") and #23313 (a steering eval had to be commented out) show the team itself is still stabilizing the measurement layer, which slows confidence in agent-quality claims.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI — Community Digest
**Date:** 2026-10-30 · **Source:** [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

## 1. Today's Highlights
No new releases landed in the last 24 hours, but 38 issues were updated, with activity concentrated on authentication/platform bugs and ACP (Agent Client Protocol) parity gaps. The long-running org-entitlement failure [#552](https://github.com/github/copilot-cli/issues/552) remains the most-discussed thread at 31 comments, while several high-severity resource-consumption reports ([#5254](https://github.com/github/copilot-cli/issues/5254), [#4613](https://github.com/github/copilot-cli/issues/4613)) continue to draw attention. Fresh triage items include a broken `copilot --cloud` provisioning path and a `/copy` Markdown→HTML regression.

## 2. Releases
_No new releases in the last 24 hours._

## 3. Hot Issues

1. **[#552](https://github.com/github/copilot-cli/issues/552) — `Failed to list models: 403 unauthorized` (OPEN, 31 comments, 👍4)**
   The highest-traffic thread in the repo. Users in orgs with Copilot CLI enabled still cannot enumerate models, blocking basic usage. The comment volume (spanning from Nov 2025 to now) signals an unresolved entitlement/mapping problem on GitHub's side rather than a simple client bug.

2. **[#2165](https://github.com/github/copilot-cli/issues/2165) — Ubuntu keychain support is broken (OPEN, 5 comments, 👍22)**
   Highest-reaction item in this batch. Two distinct defects: incorrect docs for the keychain workaround, and `secret-tool`-related auth failures. Linux users consider this a first-class platform-support gap.

3. **[#4802](https://github.com/github/copilot-cli/issues/4802) — PRU quota wiped out, likely tied to Assisted Permissions (OPEN, 8 comments)**
   Billing-impacting report from a Pro annual/legacy request-based user. Community reaction is cautious but concerned — quota accounting regressions erode trust quickly, especially with no clear remediation path.

4. **[#4851](https://github.com/github/copilot-cli/issues/4851) — Azure MCP server fails sending HTTP request (CLOSED, 6 comments, 👍10)**
   Rust runtime `BrokenPipe` when validating an Azure API Center MCP registry — a "broke overnight" enterprise regression that was closed, suggesting a fix landed. Notable for the 10 upvotes and enterprise MCP reliance.

5. **[#4275](https://github.com/github/copilot-cli/issues/4275) — ACP: expose `contextTier` as a session config option (OPEN, 7 comments, 👍4)**
   The interactive `/model` picker supports mid-session context-tier changes; ACP clients can only set it at spawn. A clear parity request from a GitKraken integrator — evidence that third-party ACP consumers are now a real constituency.

6. **[#2109](https://github.com/github/copilot-cli/issues/2109) — ACP: support `ask_user` / `ask_question` extension method (OPEN, 4 comments, 👍8)**
   Only `session/request_permission` is exposed today, so custom ACP clients can't surface clarifying questions with structured answers. Well-received (👍8) and architecturally significant for the ACP ecosystem.

7. **[#5254](https://github.com/github/copilot-cli/issues/5254) — 1.0.103: main process grows to 37 GiB during long parallel-agent session (OPEN, 2 comments)**
   37.3 GiB physical footprint after ~6h19m on a 32 GiB Mac, with 133M malloc allocations and 10.7 GiB fragmentation. This is the most alarming stability report in the batch — long-running resumed sessions with parallel sub-agents are effectively unusable.

8. **[#4613](https://github.com/github/copilot-cli/issues/4613) — 1.0.80+ regression: MCP schemas eagerly injected, +354K startup tokens (CLOSED, 3 comments)**
   The CLI apparently stopped deferring MCP tool schemas, injecting the full ambient catalog into the first request even for trivial prompts. A direct cost/latency regression for anyone with a large MCP setup; closed implies triage action.

9. **[#4576](https://github.com/github/copilot-cli/issues/4576) — `includeCoAuthoredBy: false` not inherited by task subagents (OPEN, 2 comments, 👍5)**
   Subagents still add the `Co-authored-by: Copilot` trailer, contradicting an explicit settings.json opt-out. Small surface area, real compliance annoyance for teams with strict commit-attribution policies.

10. **[#5275](https://github.com/github/copilot-cli/issues/5275) — Support default-deny tool permissions with explicit allowlist in non-interactive mode (OPEN, 1 comment)**
    `--deny-tool` always overrides `--allow-tool`, and some tools are allowed by default, so CI pipelines cannot enforce a strict allowlist. A foundational request for anyone running the CLI unattended.

## 4. Key PR Progress
_No pull requests were updated in the last 24 hours._

## 5. Hot Discussions
_No discussion data was provided for this period._

## 6. Feature Request Trends

- **ACP parity with the interactive TUI** is the clearest emerging theme: `contextTier` as a session option ([#4275](https://github.com/github/copilot-cli/issues/4275)), `ask_user` extension methods ([#2109](https://github.com/github/copilot-cli/issues/2109)), correct `session/prompt` semantics that don't kill background sub-agents ([#4555](https://github.com/github/copilot-cli/issues/4555)), and OAuth refresh-token use instead of browser prompts ([#5229](https://github.com/github/copilot-cli/issues/5229)). Integrators want ACP to be a first-class surface, not a subset.
- **Deterministic, policy-driven non-interactive mode**: strict tool allowlists ([#5275](https://github.com/github/copilot-cli/issues/5275)) and settings inheritance into subagents ([#4576](https://github.com/github/copilot-cli/issues/4576)). Headless CI use is outgrowing the current permission model.
- **Configuration discoverability**: publishing a JSON schema for `providers.json` ([#5287](https://github.com/github/copilot-cli/issues/5287)) and adding the documented but missing `--fusion-tier` flag ([#5290](https://github.com/github/copilot-cli/issues/5290)). Users are reverse-engineering BYOK and model-tier settings.
- **Cross-platform identity integration**: Linux secret storage ([#2165](https://github.com/github/copilot-cli/issues/2165)), macOS XARA keychain partitioning ([#4273](https://github.com/github/copilot-cli/issues/4273)), Windows Entra broker token cache ([#5236](https://github.com/github/copilot-cli/issues/5236)), and GHE-aware proxy/token forwarding for `gh` in sandbox mode ([#5286](https://github.com/github/copilot-cli/issues/5286)).
- **MCP lifecycle maturity**: correct Enterprise/Entra scope handling ([#5061](https://github.com/github/copilot-cli/issues/5061)), Datadog OAuth token exchange ([#5058](https://github.com/github/copilot-cli/issues/5058)), and lazy schema loading to control startup token cost ([#4613](https://github.com/github/copilot-cli/issues/4613)).
- **Context-window ergonomics**: reliable rollover/checkpointing ([#5205](https://github.com/github/copilot-cli/issues/5205)) and compaction thresholds that don't fire at 50% on high-effort models ([#4571](https://github.com/github/copilot-cli/issues/4571)).

## 7. Developer Pain Points

- **Authentication and platform integration remain the weakest area.** Keychain/secret-store issues span Ubuntu, macOS, and Windows in this single window, plus Enterprise/data-residency login confusion (`*.ghe.com` mislabeled as Enterprise Cloud, [#5280](https://github.com/github/copilot-cli/issues/5280)). Enterprise users hit this first and hardest.
- **Resource and cost blowups in long sessions.** A 37 GiB process footprint ([#5254](https://github.com/github/copilot-cli/issues/5254)), a runaway `copilot-file-search` thread pinning CPU while idle ([#4710](https://github.com/github/copilot-cli/issues/4710)), and 354K tokens of eager MCP schema injection ([#4613](https://github.com/github/copilot-cli/issues/4613)) all point at insufficient bounds on background work and startup payload.
- **Silent or premature failures in non-interactive/ACP mode.** `session/prompt` unconditionally aborting the session ([#4555](https://github.com/github/copilot-cli/issues/4555)), plugin custom agents activating in `--prompt` but not interactively ([#4592](https://github.com/github/copilot-cli/issues/4592)), and `copilot --cloud` failing instantly with an opaque `internal server error` ([#5289](https://github.com/github/copilot-cli/issues/5289)).
- **Billing/quota opacity.** The PRU wipeout report ([#4802](https://github.com/github/copilot-cli/issues/4802)) is low-volume but high-severity; quota changes tied to feature toggles need clearer accounting and rollback guidance.
- **Regression churn between minor versions.** `/copy` now returning HTML instead of Markdown ([#5288](https://github.com/github/copilot-cli/issues/5288)), an October theme change reducing heatmap/highlight readability ([#5056](https://github.com/github/copilot-cli/issues/5056)), and compaction behavior shifting in 1.0.80 ([#4571](https://github.com/github/copilot-cli/issues/4571)) suggest a fast release cadence outpacing regression coverage. Version numbers cited in this window range from `0.0.355` to `1.0.105`.
- **Long-tail issues without closure.** [#552](https://github.com/github/copilot-cli/issues/552) has been open since November 2025 with 31 comments and no resolution — a visible signal that org-level entitlement bugs fall into a black hole, which discourages further high-quality reporting.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-10-30

## 1. Today's Highlights
Two releases landed within 24 hours: **v2.2.2** enables image generation by default for providers that expose image models, and **v2.2.1** adds `/goal` for goal-driven sessions that keep running until a reviewer confirms completion. The tracker is dominated by free-tier/quota confusion (the megathread has 104 comments) and reports of v2.2.1 sessions hanging at "Working". Meanwhile, maintainers are landing a wave of core work: a tree-sitter-free shell permission scanner, Code Mode schedule checks, and by-reference media blobs in the TUI.

## 2. Releases

- **[v2.2.2](https://github.com/anomalyco/opencode/releases)** — *Image Generation by Default*: when a connected provider supports image models, agents can call `experimental_image_generate` with no extra configuration. Preferred model is configurable via `experimental.image_generate.model` ([#60258](https://github.com/anomalyco/opencode/pull/60258)).
- **[v2.2.1](https://github.com/anomalyco/opencode/releases)** — *Keep Working Toward a Goal*: `/goal <objective>` in TUI/Desktop keeps the session running until a reviewer confirms the objective is met; `/goal pause|resume|clear` control the loop ([#59437](https://github.com/anomalyco/opencode/pull/59437)).
- **[process-daemon v0.3.3](https://github.com/anomalyco/opencode/releases)** — `opencode-pty 0.3.3` (protocol 7) from `packages/process-daemon`, published to npm as `@opencode/pty@0.3.3`.

Release PR: **[#60337 release: v2.2.2](https://github.com/anomalyco/opencode/pull/60337)** brings versions and changelog back to `dev`.

## 3. Hot Issues

1. **[#59387 Free tier issues: read this first](https://github.com/anomalyco/opencode/issues/59387)** — *104 comments, 9 👍*. The canonical funnel for free-tier failures: "Free usage exceeded", resets that never happen, and Desktop version mismatch. Highest-engagement thread in the repo and the clearest signal that quota messaging needs work.
2. **[#33356 Unbounded growth of the `event` table (13GB+ opencode.db)](https://github.com/anomalyco/opencode/issues/33356)** — *45 comments, 12 👍*. Long-lived instances balloon to ~13 GB because `message.updated.1` snapshots are never pruned or compacted, filling volumes to 97–99%. Top-voted issue; a real operational risk for headless deployments.
3. **[#58786 Desktop sessions hang in Working/Thinking after Oct 22 Bun runtime update](https://github.com/anomalyco/opencode/issues/58786)** — Reproduces in brand-new sessions, no error surfaced. Points at the runtime migration rather than session corruption.
4. **[#60330 v2.2.1 stalls at "Working" all day in OpenCode GO](https://github.com/anomalyco/opencode/issues/60330)** — Fresh report on the current release; 15-minute latency on a trivial "Test" message while the Console build works. Suggests a regression worth bisecting against v2.2.2.
5. **[#56288 `external_directory` ask is skipped for `shell`](https://github.com/anomalyco/opencode/issues/56288)** — *reproduced, severity: high*. File tools enforce the rule, shell does not; a path outside the workspace can be written silently. Directly relevant to the tree-sitter removal work in PR #60332.
6. **[#46371 Hidden LLM calls billed but absent from session cost](https://github.com/anomalyco/opencode/issues/46371)** — Title generation and summaries call `LLM.stream()` but never persist token usage; billing-level evidence revives an auto-closed report. Cost transparency is a recurring trust issue.
7. **[#57012 Allow insecure HTTP for authenticated remote MCP servers on internal networks](https://github.com/anomalyco/opencode/issues/57012)** — v2.0 strictly enforces TLS for authenticated MCPs; internal-network users are blocked. PR #60039 (per-server TLS trust) is the upstream response.
8. **[#60320 Active Go subscriber hard-blocked by rate limit on Beam Free](https://github.com/anomalyco/opencode/issues/60320)** — Paid account, but `beam` advertised as unlimited returns an inescapable rate-limit error. Pairs with [#60317](https://github.com/anomalyco/opencode/issues/60317) on the retry-countdown that never resolves.
9. **[#7487 `exec` variable substitution](https://github.com/anomalyco/opencode/issues/7487)** — *8 comments, 5 👍*, open since January. Long-running request to reuse config variables inside `exec`; a small config-ergonomics gap that keeps resurfacing.
10. **[#46378 Unicode `×` (U+00D7) triggers HTTP 400 on GLM-5.3-Flash](https://github.com/anomalyco/opencode/issues/46378)** — Deterministic gateway `[1210] API parameter invalid` on standard characters. A narrow but fully reproducible provider-compatibility bug.

Also worth tracking: [#46035 MCP children accumulate until OOM](https://github.com/anomalyco/opencode/issues/46035) (closed), [#46164 `/compact` lacks a context-fit check](https://github.com/anomalyco/opencode/issues/46164), and [#60328 free usage exceeded with zero usage](https://github.com/anomalyco/opencode/issues/60328).

## 4. Key PR Progress

1. **[#60332 refactor(core): finish moving shell permission checks off tree-sitter](https://github.com/anomalyco/opencode/pull/60332)** — Shell permission checks now run on the built-in scanner across all channels, dropping 2.3 MB of embedded tree-sitter WASM and fixing eight shell-parsing edge cases. Directly addresses the class of bypasses in #56288/#46398.
2. **[#60140 feat(core): Code Mode checks with static tool scanning for schedules](https://github.com/anomalyco/opencode/pull/60140)** — Schedules can run a JavaScript `if`/`until` check before waking a session, with no model call and no allowlist to maintain. Behind `experimental.*`. Builds on merged #60137.
3. **[#60028 feat(core): let a Code Mode check decide when a schedule fires](https://github.com/anomalyco/opencode/pull/60028)** — Closed precursor to #60140: `if: { type: "code", code, allow }` evaluates `state`, `now`, and `runs` and returns `{ wake, state, message? }`.
4. **[#60116 feat(tui): load stored images by reference, like desktop](https://github.com/anomalyco/opencode/pull/60116)** — TUI requests stored images by reference and downloads only on display, matching Desktop. Active only with `experimental.media_blob`; a meaningful step for large-image sessions.
5. **[#60102 fix(core): keep permission reasons and feedback in MCP tool failures](https://github.com/anomalyco/opencode/pull/60102)** — Denials previously collapsed to `Unable to execute <server>_<tool>`, hiding the rule and user feedback from the model. Better self-correction after a deny.
6. **[#60120 fix(core): send execute progress at most every 100 ms](https://github.com/anomalyco/opencode/pull/60120)** — Nested `execute` calls previously emitted 2N ever-growing snapshots; throttling cuts bandwidth and UI churn on large programs.
7. **[#60039 feat(mcp): per-server TLS trust for remote MCP servers](https://github.com/anomalyco/opencode/pull/60039)** — Adds a `tls` config block (`ca_file`, …) per remote server; explicit trust first, trust-on-first-use to follow. The supported answer to #57012.
8. **[#60315 feat(core): integration.connect and integration.use policies](https://github.com/anomalyco/opencode/pull/60315)** — MDM-enforceable org policies for Console workspaces; supersedes `OPENCODE_CONSOLE_REQUIRE_ORG` (#58159). Enterprise deployment is becoming a first-class concern.
9. **[#60084 fix(core): require one-way V1 upgrade acknowledgment](https://github.com/anomalyco/opencode/pull/60084)** — One-time confirmation before startup imports V1 history, clarifying that adopting V2 applies to every project. Reduces migration surprise.
10. **[#60323 refactor(client): share the persistent pty protocol](https://github.com/anomalyco/opencode/pull/60323)** — Moves the persistent PTY socket protocol out of the TUI pane into `@opencode/client/solid` so the Desktop terminal can reuse it (stacked with #60322/#60329).

UI-level fixes moving quickly: [#60335 mobile question options/submit reachable](https://github.com/anomalyco/opencode/pull/60335), [#60336 `#` in file search base](https://github.com/anomalyco/opencode/pull/60336), [#60334 add-menu shortcuts inside bounds](https://github.com/anomalyco/opencode/pull/60334), [#60333 Markdown frontmatter as YAML block](https://github.com/anomalyco/opencode/pull/60333), [#60221 group added projects in settings](https://github.com/anomalyco/opencode/pull/60221).

## 6. Feature Request Trends

- **Provider & transport configurability** — Custom base URL/API key for any LLM ([#59972](https://github.com/anomalyco/opencode/issues/59972)), insecure HTTP for authenticated internal MCPs ([#57012](https://github.com/anomalyco/opencode/issues/57012)), per-server TLS trust ([#60039](https://github.com/anomalyco/opencode/pull/60039)). Users increasingly run OpenCode behind corporate networks and private gateways.
- **Programmable automation primitives** — Code Mode schedule conditions ([#60028](https://github.com/anomalyco/opencode/pull/60028), [#60140](https://github.com/anomalyco/opencode/pull/60140)) and `exec` variable substitution ([#7487](https://github.com/anomalyco/opencode/issues/7487) — the top-voted open feature request) show demand for config-as-code without model round-trips.
- **Long-running/agentic session control** — `/goal` in v2.2.1 formalizes objective-driven loops; schedules plus Code Mode checks extend the same idea to unattended runs.
- **Cost and quota transparency** — Hidden title/summary LLM calls missing from session cost ([#46371](https://github.com/anomalyco/opencode/issues/46371)) and repeated free-tier accounting complaints.
- **Enterprise policy controls** — Org-required Console sign-in ([#58159](https://github.com/anomalyco/opencode/pull/58159)) and integration connect/use policies ([#60315](https://github.com/anomalyco/opencode/pull/60315)).
- **Media efficiency** — By-reference image loading ([#60116](https://github.com/anomalyco/opencode/pull/60116)) plus default image generation in v2.2.2.

## 7. Developer Pain Points

- **Quota and rate-limit opacity** — The single loudest theme: [#59387](https://github.com/anomalyco/opencode/issues/59387) (104 comments), [#60317](https://github.com/anomalyco/opencode/issues/60317), [#60320](https://github.com/anomalyco/opencode/issues/60320), [#60328](https://github.com/anomalyco/opencode/issues/60328), [#59975](https://github.com/anomalyco/opencode/issues/59975). Symptoms include free-tier resets that never fire, paid accounts blocked on "unlimited" models, and retry countdowns that loop indefinitely.
- **Hangs with no diagnostics** — Desktop sessions stuck in Working/Thinking after the Bun runtime switch ([#58786](https://github.com/anomalyco/opencode/issues/58786)) and v2.2.1 stalling for minutes on trivial prompts ([#60330](https://github.com/anomalyco/opencode/issues/60330)). No errors surfaced, which makes triage hard.
- **Local state growth and process leaks** — Unbounded `event` table growth to 13 GB ([#33356](https://github.com/anomalyco/opencode/issues/33356)), MCP child processes accumulating until OOM ([#46035](https://github.com/anomalyco/opencode/issues/46035)), orphaned MCP descendants on disconnect ([#46253](https://github.com/anomalyco/opencode/issues/46253)).
- **Permission enforcement gaps** — `external_directory` bypassed via shell on POSIX and PowerShell ([#56288](https://github.com/anomalyco/opencode/issues/56288), [#46398](https://github.com/anomalyco/opencode/issues/46398)); denials losing their reason in MCP wrappers (#60102) compounded the confusion.
- **Billing and cost accounting** — Real provider charges for title/summary generation that never appear in session cost ([#46371](https://github.com/anomalyco/opencode/issues/46371)).
- **Provider/model edge cases** — Deterministic 400s from a Unicode `×` ([#46378](https://github.com/anomalyco/opencode/issues/46378)) and recursive JSON schemas rejected by some models when an MCP is enabled ([#45823](https://github.com/anomalyco/opencode/issues/45823)).
- **Compaction reliability** — Manual `/compact` streams the full history without a context-fit check, producing upstream request failures ([#46164](https://github.com/anomalyco/opencode/issues/46164)).
- **Migration friction** — V1→V2 imports needed an explicit acknowledgment ([#60084](https://github.com/anomalyco/opencode/pull/60084)); multiple "no way to add a custom URL/API key anymore" reports ([#59972](https://github.com/anomalyco/opencode/issues/59972)) suggest the provider setup path regressed in v2.

*Note: no Discussion data was provided, so the Hot Discussions section is omitted.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi Community Digest — 2026-10-30

**Source:** [github.com/earendil-works/pi](https://github.com/earendil-works/pi)  
**Window:** Last 24 hours (data through 2026-10-29)

## Today's Highlights

No new Pi releases were published in the last 24 hours. Activity was dominated by provider compatibility and prompt-cache correctness: OpenRouter context-limit 400s ([#10497](https://github.com/earendil-works/pi/issues/10497)) are the most-commented issue, while dynamic tool ordering/system-prompt changes ([#10024](https://github.com/earendil-works/pi/issues/10024), [#11529](https://github.com/earendil-works/pi/issues/11529)) and OpenAI-specific fields sent to compatible providers ([#9508](https://github.com/earendil-works/pi/issues/9508)) continue to create cost and error-handling problems. Long-session stability also surfaced strongly, with a V8 OOM crash report ([#11570](https://github.com/earendil-works/pi/issues/11570)) and a render-path performance regression ([#11567](https://github.com/earendil-works/pi/issues/11567)), while the community highlighted a Rust port of Pi’s headless core ([#11503](https://github.com/earendil-works/pi/discussions/11503)).

## Hot Issues

1. **[#10497](https://github.com/earendil-works/pi/issues/10497) — OpenRouter Error: 400** `[OPEN, bug, inprogress]`  
   Context-length overflows on OpenRouter requests surface as raw `400` errors, especially for extensions that inject file contents into context. With 13 comments, it is the most-discussed issue in the window and points to a need for better preflight token accounting and provider-error normalization.

2. **[#9656](https://github.com/earendil-works/pi/issues/9656) — Mouse wheel scrolls prompt history instead of transcript in fullscreen on Windows + Zellij** `[OPEN, bug]`  
   A terminal-input handling inconsistency specific to Windows → Alacritty → Zellij. It has 12 comments and 5 👍, the highest reaction count among open bugs, suggesting multiplexer compatibility is a meaningful UX pain point.

3. **[#9508](https://github.com/earendil-works/pi/issues/9508) — pi-ai sends unsupported OpenAI-specific request fields/roles/auth to compatible providers** `[OPEN, bug]`  
   Third-party OpenAI-compatible providers reject Pi requests with `400/422` because OpenAI-specific fields, roles, or auth headers leak through. Nine comments since September indicate a persistent interoperability gap rather than a one-off provider issue.

4. **[#10024](https://github.com/earendil-works/pi/issues/10024) — Mid-run tool set change moves the head of the system prompt and re-bills the conversation** `[OPEN]`  
   Dynamic tool selection re-derives the rendered tool bullet list from the live set, changing the system prompt during a run and invalidating prompt caching. Five comments and 2 👍 reflect cost-sensitive user concern.

5. **[#11157](https://github.com/earendil-works/pi/issues/11157) — Extensions that `sendMessage` at `session_start` turn every session into a legacy transcript** `[OPEN, inprogress, prio:p0]`  
   Extensions that inject a message before Pi’s system message break transcript assumptions, including Anthropic’s `system` field behavior. The p0 label and three comments signal a core/extension ordering contract that needs to be made explicit.

6. **[#11570](https://github.com/earendil-works/pi/issues/11570) — V8 OOM (SIGABRT) in long sessions** `[CLOSED, no-action]`  
   Long-running sessions (~8 MB session files, 2+ days) crash with `FatalProcessOutOfMemory` from giant `ConsString` flattening/regex replacement inside `flatMap`. With five production crash reports, this is a high-severity stability signal despite being closed as no-action.

7. **[#11527](https://github.com/earendil-works/pi/issues/11527) — Bedrock: a new `BedrockRuntimeClient` is created for every request** `[OPEN]`  
   Each model call creates a fresh client, credential provider, and HTTP/2 session. With SSO profiles this can trigger a `GetRoleCredentials` round trip per request, adding latency and credential churn.

8. **[#11529](https://github.com/earendil-works/pi/issues/11529) — Tool order depends on registration order, so the same tools can bust the prompt cache** `[OPEN]`  
   `getCurrentTools()` returns insertion order, so tools that reconnect or load via `tool_search` move to the end of the map. This breaks prompt-cache stability and connects directly to the cost issues in #10024.

9. **[#11567](https://github.com/earendil-works/pi/issues/11567) — Typing slows down in long sessions: `getSessionName()` scans every entry on each render** `[CLOSED, bug, no-action]`  
   At ~400k entries, key-to-render p50 rises from 1.5 ms to 21 ms, with 94% of busy CPU in `SessionManager.getSessionName()`. The issue was closed no-action, but the profile is concrete and likely to recur.

10. **[#11538](https://github.com/earendil-works/pi/issues/11538) — google-generative-ai: streamed parts with separate thought signatures are merged or dropped** `[OPEN]`  
   The Google stream parser coalesces text/thinking parts and retains only the last `thoughtSignature`, losing replay fidelity for thinking continuity. Two comments, but provider-side correctness issues tend to affect multiple models.

## Key PR Progress

1. **[#11545](https://github.com/earendil-works/pi/pull/11545) — Anthropic message threads** `[OPEN]`  
   Adds support for Anthropic’s server-side message threads: when a session ID is set and caching is on, Pi can send only new messages instead of the full history each turn. This could materially reduce token usage and cost.

2. **[#11562](https://github.com/earendil-works/pi/pull/11562) — Start new sessions in the cwd’s default directory** `[OPEN]`  
   Fixes session storage semantics when a session is opened with a cwd from another project. `/new`, `/fork`, and `/clone` now use the session’s cwd default folder instead of treating the old folder as a custom `--session-dir`.

3. **[#11546](https://github.com/earendil-works/pi/pull/11546) — Cap `pi.exec` output at 256 MiB** `[CLOSED]`  
   Bounds combined stdout/stderr via `ExecOptions.maxBuffer`, terminates oversized commands, and returns `truncated`/`killed` status. A practical safeguard against runaway memory use in agent-executed commands.

4. **[#11577](https://github.com/earendil-works/pi/pull/11577) — Pick the smaller of PNG and JPEG when resizing images** `[CLOSED]`  
   Fixes the resize path always preferring PNG when it fit under the byte limit, even when the JPEG was much smaller. Directly addresses [#11550](https://github.com/earendil-works/pi/issues/11550) and avoids unnecessary payload inflation.

5. **[#11572](https://github.com/earendil-works/pi/pull/11572) — Do not retry Zhipu usage-limit errors (code 1308)** `[CLOSED]`  
   Zhipu/Z.ai plan caps return HTTP 429 with code `1308`; the generic 429 pattern previously made Pi retry futilely. The fix distinguishes a quota cap from transient rate limiting.

6. **[#11565](https://github.com/earendil-works/pi/pull/11565) — Stop writing OSC 133 prompt markers in regular mode** `[CLOSED]`  
   Prevents TUI messages from being interpreted as shell prompts by terminals that display OSC 7501 program status, such as Rex and newer iTerm2. Fixes disappearing “working” indicators.

7. **[#11556](https://github.com/earendil-works/pi/pull/11556) — Let the SDK stream resolve auth for summaries** `[CLOSED]`  
   Fixes compaction, branch summaries, and bug-report summaries in `createAgentSession` sessions by letting `modelRuntime.streamSimple` resolve stored OAuth credentials instead of passing an access token as `apiKey`.

8. **[#11544](https://github.com/earendil-works/pi/pull/11544) — Kill the daemon’s commands when it is terminated** `[CLOSED]`  
   Prevents orphaned commands when a local Unix daemon is closed: the daemon now handles `SIGTERM` so `kill_all` runs instead of dying before cleanup.

9. **[#11543](https://github.com/earendil-works/pi/pull/11543) — Strip private-parameter CSI sequences in `stripAnsi`** `[CLOSED]`  
   Fixes ANSI stripping for sequences with private prefix bytes (`<`, `=`, `>`), so SGR mouse reports and secondary device attributes no longer leak fragments like `35;59;1M` into rendered text.

10. **[#11571](https://github.com/earendil-works/pi/pull/11571) — Warn when an npm package update leaves the installed version unchanged** `[CLOSED]`  
    Addresses a registry-cache mismatch between `npm view` and `npm install <name>@latest` during `pi update --extensions`, making a silent no-op update visible to the user.

## Hot Discussions

**Show and tell**

- **[#11503](https://github.com/earendil-works/pi/discussions/11503) — pi-rs: a Rust port of the headless core**  
  A community Rust port of Pi 0.74.2’s headless core (agent loop, seven built-in tools, session JSONL, CLI surface, system prompt), with behavioral parity verified “atom by atom.” The author also shares a DeepSeek API compatibility finding. One comment and 1 👍.

**Q&A**

- **[#11574](https://github.com/earendil-works/pi/discussions/11574) — How to upload an npmjs package to Pi package source?**  
  A package author asks how to publish and share a Pi package with the community. The lack of an obvious answer highlights a documentation/discovery gap around third-party package distribution.

## Feature Request Trends

- **Provider abstraction hardening:** sanitize OpenAI-specific fields for compatible providers ([#9508](https://github.com/earendil-works/pi/issues/9508)), preserve Google thought signatures ([#11538](https://github.com/earendil-works/pi/issues/11538)), reuse Bedrock clients ([#11527](https://github.com/earendil-works/pi/issues/11527)), and handle provider-specific auth metadata correctly.
- **Prompt-cache stability and cost accounting:** stable system-prompt heads and tool ordering ([#10024](https://github.com/earendil-works/pi/issues/10024), [#11529](https://github.com/earendil-works/pi/issues/11529)), Bedrock cache warming ([#11528](https://github.com/earendil-works/pi/issues/11528)), OpenRouter session IDs ([#10022](https://github.com/earendil-works/pi/issues/10022)), and authoritative OpenRouter cost/BYOK data ([#8940](https://github.com/earendil-works/pi/issues/8940)).
- **Long-session reliability:** OOM crashes ([#11570](https://github.com/earendil-works/pi/issues/11570)), render-time scans ([#11567](https://github.com/earendil-works/pi/issues/11567)), context-usage accounting ([#11534](https://github.com/earendil-works/pi/issues/11534)), and token-estimation clamping ([#10988](https://github.com/earendil-works/pi/issues/10988)).
- **MCP and tool discovery:** namespace-scoped `tool_search` queries ([#11558](https://github.com/earendil-works/pi/issues/11558)), robust `WWW-Authenticate` parsing ([#11539](https://github.com/earendil-works/pi/issues/11539)), and deterministic tool ordering for cache stability.
- **Extension contracts and packaging:** explicit `session_start` message-ordering rules ([#11157](https://github.com/earendil-works/pi/issues/11157)), recoverable unsupported image formats ([#11552](https://github.com/earendil-works/pi/issues/11552)), configurable OAuth/Copilot timeouts ([#11549](https://github.com/earendil-works/pi/issues/11549)), and clearer package publishing guidance ([#11574](https://github.com/earendil-works/pi/discussions/11574)).
- **Terminal UX portability:** Windows/Zellij wheel handling ([#9656](https://github.com/earendil-works/pi/issues/9656)), Apple Terminal `Shift+Enter` behavior ([#11559](https://github.com/earendil-works/pi/issues/11559)), RTL rendering ([#11580](https://github.com/earendil-works/pi/pull/11580)), and cleaner OSC/CSI handling ([#11565](https://github.com/earendil-works/pi/pull/11565), [#11543](https://github.com/earendil-works/pi/pull/11543)).

## Developer Pain Points

- **Provider-specific 400/422 failures remain a recurring tax.** OpenAI-compatible endpoints, OpenRouter context limits, Google thought signatures, Bedrock credentials, and Zhipu quota errors all require provider-aware handling rather than generic request paths.
- **Prompt-cache invalidation is costly and hard to see.** Dynamic tool selection, registration-order changes, and system-prompt head movement can silently re-bill conversations; users are asking for deterministic ordering and better cost visibility.
- **Long sessions degrade or crash.** Large session files trigger V8 OOMs, per-render scans, and context-accounting problems, making multi-day agent sessions risky.
- **Extensions can violate core assumptions.** Injecting messages at `session_start`, using `tools.`-prefixed names with small local models, or emitting unsupported image formats can break transcripts or provider requests.
- **Terminal and multiplexer differences create inconsistent UX.** Windows/Zellij, Apple Terminal, RTL text, and OSC/CSI sequences all produce platform-specific behavior that is difficult for users to diagnose.
- **Session storage and resumption semantics are confusing.** Opening a session from another project can change where `/new`, `/fork`, and `/clone` save, and `--session-dir` detection has been mistaken for custom storage.
- **Community package distribution lacks a clear path.** The npm package publishing question and the Gondolin packaging fix ([#11582](https://github.com/earendil-works/pi/pull/11582)) both point to onboarding/documentation friction for extension authors.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-10-30

**Source:** [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) · Data window: updates through 2026-10-29

---

## 1. Today's Highlights

The CLI shipped **v0.26.4**, a light release whose only user-facing feature is host-theme inheritance for generated UI views; the matching TypeScript SDK **v0.1.26** and **Desktop v0.26.4** were published alongside it. Engineering velocity is concentrated almost entirely in **CI and release reliability**: of the 20 most-commented PRs, more than half are infrastructure hardening (macOS suite partitioning, Web Shell smoke isolation, runner routing, Maven cache correctness, release notifier reconciliation). The most substantive open discussion remains **context immutability for self-hosted models** (#14215), where low prompt-processing speed makes mutable context expensive.

---

## 2. Releases

| Release | Notes |
|---|---|
| **v0.26.4** ([release](https://github.com/QwenLM/qwen-code/releases)) | Primary CLI release. No known breaking changes. Feature: `feat(generated-ui): follow the host theme in generated views` ([#15798](https://github.com/QwenLM/qwen-code/pull/15798)). Release body is a placeholder (`_See the complete change list below._`), so the changelog is effectively the PR list. |
| **sdk-typescript-v0.1.26** | Bundles CLI **0.26.4**, built from the same branch/ref as the SDK. The release body still contains stale text referencing CLI **0.26.3**, suggesting a template/automation artifact worth cleaning up. |
| **desktop-v0.26.4** | Includes `fix(config): report controls that were silently dropped` ([#15794](https://github.com/QwenLM/qwen-code/pull/15794)) by @yiliang114, plus managed-session documentation updates. |
| **v0.26.3-nightly.20261028.ca204559a7** | Nightly cut from `release/v0.26.3-nightly.20261028.ca204559a7`; carries the same `fix(config)` change and managed docs edits. |

**Takeaway:** a coordinated CLI + SDK + Desktop release train at 0.26.4. The only net-new product capability is theme inheritance for generated views; everything else is carried forward from 0.26.3.

---

## 3. Hot Issues

> Only **3 issues** were updated in the 24h window, so all three are covered rather than a top-10 selection.

1. **[#14724](https://github.com/QwenLM/qwen-code/issues/14724) — Main CI failed: Managed Agent gate, no test identified** · `OPEN` · `type/bug`, `autofix/skip` · **84 comments**
   A bot-filed main-branch CI failure that has now been open for 10 days with 84 comments and no 👍. The extreme comment count on an `autofix/skip`-labeled item signals an automation loop or repeated human triage rather than genuine community debate — the single highest-noise item in the tracker.

2. **[#14215](https://github.com/QwenLM/qwen-code/issues/14215) — Context immutability for self-hosted models** · `OPEN` · `P2`, `feature-request`, `performance`, `memory`, `caching`, `context-performance`, `need-discussion` · **7 comments, 1 👍**
   The most substantive community request in the window. The reporter argues that features like memories, dreams, suggestions, and sessions all assume fast prompt processing; on self-hosted hardware with slow prefill, mutable context becomes prohibitively expensive. Requested behavior is an immutable context mode that preserves prefix-cache hits. Labeled `need-discussion`, so maintainer input is the blocker.

3. **[#15251](https://github.com/QwenLM/qwen-code/issues/15251) — Fleet Shepherd Dashboard** · `OPEN` · **0 comments**
   Auto-maintained operational dashboard for the repo's agent fleet. Its current state is notable: the tick reports **2 autofix runs wedged in `queued`** (oldest 2026-10-...), with `syncs: 0 · dispatches: 0 · releases: 0`. This is effectively a public health signal that the autofix pipeline is stalled.

---

## 4. Key PR Progress

1. **[#15871](https://github.com/QwenLM/qwen-code/pull/15871) — refactor(managed-agent): split server into Maven modules** (@doudouOUC)
   Decomposes the Managed Agent Server into six production Maven modules plus one unpublished verification module, with framework-neutral contracts defining boundaries between control-plane orchestration, Runtime Broker orchestration, persistence, and adapters. The largest architectural change in flight.

2. **[#15870](https://github.com/QwenLM/qwen-code/pull/15870) — refactor(managed): remove persisted public message snapshots** (@doudouOUC)
   Removes persisted public message snapshots from the managed server — a data-model simplification that likely reduces storage growth and snapshot/strea
m divergence.

3. **[#11854](https://github.com/QwenLM/qwen-code/pull/11854) — feat: add hybrid code mode** (@DragonnZhang)
   Long-running (since 2026-09-14) feature adding a Codex-aligned `tools.mode` enum: `direct`, `code_mode`, `code_mode_only`. In `code_mode`, ordinary tools stay directly callable while also exposing an isolated `exec` JavaScript tool with nested JS declarations. The most significant capability addition under review.

4. **[#15887](https://github.com/QwenLM/qwen-code/pull/15887) — feat(serve): enable remote access from settings without restarting** (@yiliang114)
   Adds **Settings → Connections → Allow remote connections** to a running `qwen serve`. Remote access defaults off; a local operator can enable it live, then copy the address and a separate bearer token into another Web Shell's connection form. Meaningful UX win for daemon workflows.

5. **[#15634](https://github.com/QwenLM/qwen-code/pull/15634) — feat(channels): deliver injected messages into the running turn** (@Eric-GoodBoy-Tech)
   Adds a fourth channel `dispatchMode`, `inject`: messages arriving mid-turn go to the running turn's mid-turn queue and are read at the next tool-batch boundary instead of being buffered until turn end. Directly addresses agent responsiveness in channel sessions.

6. **[#15888](https://github.com/QwenLM/qwen-code/pull/15888) — fix(ci): partition the complete macOS test suite into bounded jobs** (@yiliang114)
   Splits macOS CI into seven jobs (three CLI shards, two core shards, remaining workspace suites, standalone/runtime scripts) with the original check retained as an aggregate gate. Stacked on #15884/#15883. A direct response to macOS suite timeouts.

7. **[#15886](https://github.com/QwenLM/qwen-code/pull/15886) + [#15884](https://github.com/QwenLM/qwen-code/pull/15884) — Web Shell smoke isolation** (@yiliang114)
   #15886 pins browser smoke to `ubuntu-latest` for every admitted run, decoupled from the shared Linux runner fleet; #15884 moves Chromium profiles and shared-memory temp files onto the runner temp directory. Together these target the recurring smoke failure tracked in #15060.

8. **[#15885](https://github.com/QwenLM/qwen-code/pull/15885) — fix(ci): route the E2E build job through the pool-first runner expression** (@yiliang114)
   Aligns the E2E shared build job with the repo-wide routing convention: prefer self-hosted `ecs-qwen` when enabled, fall back to hosted Ubuntu, plus the standard self-hosted disk setup. Closes a routing inconsistency.

9. **[#15854](https://github.com/QwenLM/qwen-code/pull/15854) — perf(release): reuse verified native audio prebuilds across releases** (@yiliang114)
   Reuses native audio prebuilds from a successful official main release when build inputs match; validated cache hits skip the entire native build matrix, with any lookup/download/validation failure falling back to rebuilding all five targets. A clear release-latency win.

10. **[#15829](https://github.com/QwenLM/qwen-code/pull/15829) — fix(vscode): keep sibling model settings when writing provider config** (@2SinceJuly)
    Fixes a real data-loss bug: configuring a Coding Plan or provider from the VS Code companion rewrote `settings.model` with only `name`, silently deleting sibling keys. Now writes `name` and its paired `baseUrl` key-by-key. **High user impact relative to its small diff.**

**Also worth watching:** [#15852](https://github.com/QwenLM/qwen-code/pull/15852) (release notifiers file issues only on real failures and reconcile stale ones), [#15730](https://github.com/QwenLM/qwen-code/pull/15730) (job token for publish checkout), [#15274](https://github.com/QwenLM/qwen-code/pull/15274) / [#15286](https://github.com/QwenLM/qwen-code/pull/15286) (Maven cache/result-preservation hardening, both `autofix/needs-human`), [#15771](https://github.com/QwenLM/qwen-code/pull/15771) (Actions queue census on the Fleet Shepherd dashboard), [#11486](https://github.com/QwenLM/qwen-code/pull/11486) (`qwen update --target-version`).

---

## 5. Hot Discussions

*Omitted — no Discussion data was provided in this dataset.*

---

## 6. Feature Request Trends

- **Context and cache economics for self-hosted deployments.** #14215 is the clearest signal: prefix-cache preservation, context immutability, and lower prefill cost. The `roadmap/context-performance` + `scope/memory` + `scope/caching` label cluster indicates this is a recognized roadmap axis, not a one-off.
- **Tool-invocation architecture.** #11854 (`tools.mode`: `direct` / `code_mode` / `code_mode_only`) points toward a Codex-aligned model where tools are callable both directly and from an isolated JS `exec` sandbox.
- **Live/remote serving ergonomics.** #15887 seeks zero-restart remote access with token-based auth for `qwen serve` — the daemon is being treated as a first-class deployment target.
- **Mid-turn message injection.** #15634 requests interruptible, tool-boundary-aware message delivery in channel sessions instead of end-of-turn buffering.
- **Deterministic, offline-capable installation.** #11486 (`--target-version` without npm discovery) reflects demand for pinned, reproducible standalone installs, including custom `QWEN_UPDATE_BASE_URL` mirrors.
- **Editor integration fidelity.** #15829 shows VS Code companion config writes must be non-destructive to sibling settings — a "don't lose my config" class of request.

---

## 7. Developer Pain Points

1. **CI instability is the dominant tax.** At least 8 of the top 20 PRs are CI fixes. Recurring themes: shared runner network contention (#15886), Chromium temp/shared-memory behavior in Web Shell smoke (#15884), macOS suite duration (#15888), inconsistent runner routing (#15885), and Maven cache write-back failure modes (#15274, #15286). Contributors are spending review bandwidth on test infrastructure rather than product code.
2. **Autofix automation is stalling, not helping.** Issue #15251 reports **2 autofix runs wedged in `queued`**; #14724 has accumulated **84 comments** on a main-CI failure; two `autofix/needs-human` PRs (#15274, #15286) have sat open since 2026-10-22. The bot produces volume, but a growing share requires human rescue.
3. **Release automation false positives.** #15852 documents that both fan-out release notifiers treat **cancelled** runs as failures and file issues, and that neither can close those issues when a later attempt ships. Combined with the placeholder v0.26.4 notes and the stale "0.26.3" text inside the 0.1.26 SDK release body, release metadata is drifting from reality.
4. **Silent config mutations destroy user state.** Two independent tickets in one window — Desktop's `fix(config): report controls that were silently dropped` (#15794) and VS Code's `settings.model` overwrite (#15829) — indicate a systemic pattern: writers replace config objects rather than merging keys.
5. **Self-hosted users feel like second-class citizens.** #14215 articulates the frustration directly: cutting-edge features (memories, dreams, suggestions, sessions) are designed around fast hosted prompt processing and degrade badly on slower self-hosted hardware.
6. **Opaque or missing release notes.** v0.26.4's changelog ships as `_See the complete change list below._`, forcing users to reconstruct changes from the PR list.

---

*Digest generated from GitHub metadata only. Issue/PR bodies were truncated in the source data; comment counts were unavailable for PRs and are reported as-is for issues.*

</details>