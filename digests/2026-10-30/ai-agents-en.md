# OpenClaw Ecosystem Digest 2026-10-30

> Issues: 170 | PRs: 500 | Projects covered: 5 | Generated: 2026-10-29 18:48 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [IronClaw](https://github.com/nearai/ironclaw)
- [QwenPaw](https://github.com/agentscope-ai/QwenPaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-10-30

**Data window:** last 24 hours, through 2026-10-29.  
**Data caveat:** Issues are the top 50 by comment count; PRs are the top 30 sample. PR comment counts are unavailable in the provided data, so PR ranking is based on the supplied ordering and labels.

## 1. Today's Overview

OpenClaw is in a very high-activity release-and-triage phase: 170 issues and 500 PRs were updated in 24 hours, with 131 active issues and 291 open PRs, alongside one patch release. The new release, [v2026.10.9](https://github.com/openclaw/openclaw/releases/tag/v2026.10.9), is a security and dependency-hardening patch rather than a feature release. The issue queue is dominated by core reliability themes—session-state lifecycle, crash/wake recovery, memory promotion, message loss, and provider authentication—rather than cosmetic requests. The project is shipping security fixes quickly, but several P0/P1 reliability issues remain open without linked fix PRs, so overall health reads as **high velocity with elevated reliability risk**.

## 2. Releases

### v2026.10.9 — security/dependency patch

Release notes highlight runtime dependency vulnerabilities being patched:

- **MCP schema validation:** `fast-uri 4.2.3` rejects malformed URI schemes and hosts.
- **Input bounds:** oversized Zod collections are rejected early in A2UI and the Discord embedded app SDK.
- **IMAP sender parsing:** moves to `nodemailer 10.1.4`, hardening spoofed-sender handling.

**Breaking changes:** none stated in the release notes.  
**Migration notes:** none stated. This appears to be a drop-in patch release.  
**Recommendation:** upgrade is advisable because the release is explicitly security-focused.

One release-process signal: [Issue #187490](https://github.com/openclaw/openclaw/issues/187490) tracks flaky tests observed during 2026.10.9 validation. The release classified them as flakes, but policy requires parallel fixes on `main`.

## 3. Project Progress

The dataset reports **209 merged/closed PR updates** in the last 24 hours. The visible sample only identifies one closed PR:

- [PR #187819](https://github.com/openclaw/openclaw/pull/187819) — **CLOSED**: “fix: prevent shared-state hangs after service installation drift.” This addresses shared-state worker admission hangs when service-installation policy changes or is copied, including a Linux case where a running system Gateway could select an unrelated stale user-service installation.

Several open PRs show active work on important areas:

- **Model catalog / thinking profiles:** [PR #187730](https://github.com/openclaw/openclaw/pull/187730), [PR #187754](https://github.com/openclaw/openclaw/pull/187754), [PR #187716](https://github.com/openclaw/openclaw/pull/187716) — stacked work to let catalog rows own thinking profiles and improve reasoning replay for Kimi, DeepSeek, Mistral, and Moonshot models.
- **Discord / Codex persistence:** [PR #177691](https://github.com/openclaw/openclaw/pull/177691) — fixes `/codex detach` and `/codex bind` being lost after Gateway restart. It carries P1, compatibility, and security-boundary merge-risk labels and still needs proof.
- **Memory indexing resilience:** [PR #187539](https://github.com/openclaw/openclaw/pull/187539) fixes `memory_search` timeouts through same-host OpenAI-compatible embedding servers; [PR #187797](https://github.com/openclaw/openclaw/pull/187797) addresses truncated embedding batch-limit errors.
- **Codex recovery:** [PR #187776](https://github.com/openclaw/openclaw/pull/187776) resumes Codex conversations after background cleanup settles.
- **Agent/session correctness:** [PR #180214](https://github.com/openclaw/openclaw/pull/180214) preserves active request provenance during compaction; [PR #180247](https://github.com/openclaw/openclaw/pull/180247) preserves tool timeout outcomes; [PR #182553](https://github.com/openclaw/openclaw/pull/182553) and [PR #187833](https://github.com/openclaw/openclaw/pull/187833) address queued-message context and overflow summaries; [PR #187527](https://github.com/openclaw/openclaw/pull/187527) fixes parent dashboard publishing after subagent completion.
- **Security/sandboxing:** [PR #187825](https://github.com/openclaw/openclaw/pull/187825) fixes remote-shell sandbox path trimming that could resolve `" x.txt"` to `x.txt`.
- **UI/CLI polish:** [PR #187831](https://github.com/openclaw/openclaw/pull/187831) preserves saved selections during native status inspection; [PR #187522](https://github.com/openclaw/openclaw/pull/187522) handles ambient cancellation on stdin reads; [PR #187830](https://github.com/openclaw/openclaw/pull/187830) keeps workspace conflict recovery outside chat boot; [PR #187823](https://github.com/openclaw/openclaw/pull/187823) lets operators dismiss the read-only Gateway banner.

## 4. Community Hot Topics

### Most active issues

| Topic | Item | Signal |
|---|---|---|
| Memory recall / promotion | [#150635](https://github.com/openclaw/openclaw/issues/150635) — 22 comments | Short-term recall retention evicts recalled entries nightly, so the “dreaming deep phase” never promotes. |
| Memory promotion inconsistency | [#164923](https://github.com/openclaw/openclaw/issues/164923) — 19 comments | One workspace promotes 0/512 candidates while sibling workspaces promote 50–90%. |
| Crash recovery / session state | [#166634](https://github.com/openclaw/openclaw/issues/166634) — 18 comments | Late reclamation checkpoint failure leaves an agent permanently unavailable after crash recovery. |
| Native host exec / shared state | [#177656](https://github.com/openclaw/openclaw/issues/177656) — 17 comments | At least 28 failures on 2026.10.5 with shared-state integrity-admission errors and no child result. |
| State-lifecycle lease contention | [#159094](https://github.com/openclaw/openclaw/issues/159094) — 14 comments | Gateway owns the lease, but internal workers report another process owns state-lifecycle. |
| Control UI WebChat jitter | [#164394](https://github.com/openclaw/openclaw/issues/164394) — 13 comments | Continuous micro up/down tremble when scrolling long transcripts. |
| Wake-recovery runtime failure | [#158592](https://github.com/openclaw/openclaw/issues/158592) — 11 comments | After host sleep/wake, one agent’s model runtime publication times out and never recovers until restart. |

### Most active PR themes

PR comment counts are unavailable, but the supplied top PR sample is dominated by:

- **Discord/Codex state durability:** [PR #177691](https://github.com/openclaw/openclaw/pull/177691), P1 with compatibility and security-boundary risks.
- **Model catalog refactor:** [PR #187730](https://github.com/openclaw/openclaw/pull/187730), [PR #187754](https://github.com/openclaw/openclaw/pull/187754), [PR #187716](https://github.com/openclaw/openclaw/pull/187716).
- **Memory indexing reliability:** [PR #187539](https://github.com/openclaw/openclaw/pull/187539), [PR #187797](https://github.com/openclaw/openclaw/pull/187797).
- **Session/agent correctness and UX:** [PR #180214](https://github.com/openclaw/openclaw/pull/180214), [PR #180247](https://github.com/openclaw/openclaw/pull/180247), [PR #187527](https://github.com/openclaw/openclaw/pull/187527), [PR #187831](https://github.com/openclaw/openclaw/pull/187831).

**Underlying need:** users are running OpenClaw as a persistent, multi-channel, multi-agent runtime. The community’s highest-engagement issues are not feature wishlist items; they are requests for predictable memory promotion, durable session state, recoverable gateway processes, and clearer diagnostics when runtime ownership or provider auth breaks.

## 5. Bugs & Stability

Severity labels below come from the issue metadata. Many items were not first reported in the last 24 hours but were active and updated in the window.

### P0 / release-blocking class

- [Issue #166634](https://github.com/openclaw/openclaw/issues/166634) — **P0**: Late reclamation commit checkpoint failure leaves an agent unavailable after crash recovery. Agent permanently refuses `chat.history`, `chat.metadata`, `models.list`, and progress-card requests with `UNAVAILABLE`. **No linked fix PR visible.**
- [Issue #158592](https://github.com/openclaw/openclaw/issues/158592) — **P0**: After macOS host sleep/wake, prepared model runtime publication times out for one agent; every inbound message fails with “runtime owner was not published” until Gateway restart. **No linked fix PR visible.**
- [Issue #160762](https://github.com/openclaw/openclaw/issues/160762) — **P0**: `claude-cli` + Telegram drops a message sent mid-turn; the drained prompt carries the previous message’s body. Message/data-loss impact. **No linked fix PR visible.**
- [Issue #161341](https://github.com/openclaw/openclaw/issues/161341) — **P0**: Codex auth import always fails on Windows with “The Codex credential reader could not stop,” even when native Codex login is valid. **No linked fix PR visible.**

### P1 / high-impact stability

- [Issue #177656](https://github.com/openclaw/openclaw/issues/177656) — **P1**: Native host exec returns shared-state integrity-admission errors without a child result; at least 28 failures on stable 2026.10.5. **No linked fix PR visible.**
- [Issue #159094](https://github.com/openclaw/openclaw/issues/159094) — **P1**: Gateway owns the state-lifecycle lease, but internal workers report another OpenClaw process owns it, closing database execution admission. **No linked fix PR visible.**
- [Issue #155396](https://github.com/openclaw/openclaw/issues/155396) — **P1**: Ordinary Codex tool turns can fail closed on `provenance_rejected` during final-answer recovery, losing the substantive final answer. **No linked fix PR visible.**
- [Issue #187579](https://github.com/openclaw/openclaw/issues/187579) — **P1**: Pi500 restart generates ~1.5 GB of unnecessary writes recopying installed plugin dependencies and reports ready too early. **No linked fix PR visible.**
- [Issue #187099](https://github.com/openclaw/openclaw/issues/187099) — **P1**: Queued reply never reclaimed on a recovery-rollover lane; diagnostic declines with `keep_lane/active_reply_work`, making the dashboard main session unusable. **No linked fix PR visible.**

### Security / data-integrity

- [Issue #173058](https://github.com/openclaw/openclaw/issues/173058) — **Security, P2**: `tools.fs.workspaceOnly` does not restrict file tools because the agent runtime also receives the OpenClaw state root as an allowed working directory. **No linked fix PR visible.**
- [Issue #155457](https://github.com/openclaw/openclaw/issues/155457) — **P2**: Anthropic tool calls intermittently fail with malformed streamed JSON arguments on large edits. **No linked fix PR visible.**
- [Issue #187588](https://github.com/openclaw/openclaw/issues/187588) — **P2**: Telegram `MEDIA:` line for an existing local PDF is never dispatched; text arrives, no document send, no error logged. **No linked fix PR visible.**

### Stability / operational quality

- [Issue #187490](https://github.com/openclaw/openclaw/issues/187490) — **P2**: Flaky tests seen in 2026.10.9 release validation; tracked for parallel fixes on `main`.
- [Issue #164690](https://github.com/openclaw/openclaw/issues/164690) — **P2**: `claude-cli` runs spawn every stdio MCP server twice; relay/anchor wrapper costs ~144 MB per stdio child and is not configurable.
- [Issue #185092](https://github.com/openclaw/openclaw/issues/185092) — **P2**: Windows node paired but browser control fails with listener ownership/authentication error.

**Assessment:** several P0 issues have been open since late September or early October and still lack visible linked fix PRs. This is the main project-health concern. There are useful fix PRs in adjacent areas—shared-state hangs, status inspection, memory indexing, sandbox path handling, and Codex resume—but they do not yet cover the highest-severity session-state and wake-recovery failures.

## 6. Feature Requests & Roadmap Signals

- **Long-lived session lifecycle:** [Issue #154482](https://github.com/openclaw/openclaw/issues/154482) asks for a supported lifecycle for a permanent MAIN session’s history—export/trim by range or rollover—because continuity-focused deployments have no way to bound `transcript_events`. Related: [Issue #112638](https://github.com/openclaw/openclaw/issues/112638) on `session.maintenance` failing to bound the store.
- **Team/multi-agent organization:** [Issue #153686](https://github.com/openclaw/openclaw/issues/153686) requests preserving named session groups under each agent in team mode instead of flattening into pinned/recent. Related routing isolation concerns appear in [Issue #126533](https://github.com/openclaw/openclaw/issues/126533) and [Issue #154739](https://github.com/openclaw/openclaw/issues/154739).
- **Accessibility and UI polish:** [Issue #154524](https://github.com/openclaw/openclaw/issues/154524) asks for chat messages to be exposed as headings for screen-reader navigation; [Issue #167415](https://github.com/openclaw/openclaw/issues/167415) reports sidebar rows where expand/open and one-click Archive swap positions across hover states, risking accidental archival.
- **Skill learning / evaluation:** [Issue #150250](https://github.com/openclaw/openclaw/issues/150250) proposes a Skill Workshop capability to verify learning coverage and behavioral reuse from ordinary work.
- **Operational UX:** [PR #187823](https://github.com/openclaw/openclaw/pull/187823) adds a dismiss button for the read-only Gateway banner; [Issue #167316](https://github.com/openclaw/openclaw/issues/167316) reports Android repeatedly querying `chat.history` for unknown agent `"openclaw"`.

**Prediction for the next version:** the strongest near-term signals are security/dependency patches, model-catalog and thinking-profile work, memory-indexing resilience, and targeted status/UI fixes. Broader architectural requests—permanent MAIN session lifecycle, team-mode named groups, and deep session-state lease redesign—are less likely to land in the next patch unless maintainers prioritize them as release blockers.

## 7. User Feedback Summary

- **Users depend on continuity.** Long-lived MAIN sessions, memory promotion, and transcript retention are recurring concerns. When short-term recall caps or promotion filters misbehave, users lose the core value of a persistent personal agent ([#150635](https://github.com/openclaw/openclaw/issues/150635), [#164923](https://github.com/openclaw/openclaw/issues/164923), [#154482](https://github.com/openclaw/openclaw/issues/154482)).
- **Multi-agent gateways are production workloads.** Users report lease contention, cross-session envelopes, multi-agent fanout, and workspace-specific promotion failures. They need isolation and clear ownership semantics, not just configuration options ([#159094](https://github.com/openclaw/openclaw/issues/159094), [#126533](https://github.com/openclaw/openclaw/issues/126533), [#154739](https://github.com/openclaw/openclaw/issues/154739)).
- **Channel reliability matters.** Telegram, Discord, Matrix, and Tlon issues cover dropped messages, undelivered media, mention gating, citation boundaries, and restart-lost bindings. These are production integration bugs, not edge-case feature requests ([#160762](https://github.com/openclaw/openclaw/issues/160762), [#187588](https://github.com/openclaw/openclaw/issues/187588), [#164065](https://github.com/openclaw/openclaw/issues/164065), [PR #177691](https://github.com/openclaw/openclaw/pull/177691), [PR #187778](https://github.com/openclaw/openclaw/pull/187778)).
- **CLI-backed provider paths remain fragile.** Codex and `claude-cli` issues involve auth import, OAuth refresh locks, provenance rejection, malformed streamed arguments, duplicate MCP servers, and model catalog mismatch. Users want retries, clear reason codes, and platform parity ([#161341](https://github.com/openclaw/openclaw/issues/161341), [#156442](https://github.com/openclaw/openclaw/issues/156442), [#155396](https://github.com/openclaw/openclaw/issues/155396), [#155457](https://github.com/openclaw/openclaw/issues/155457), [#164690](https://github.com/openclaw/openclaw/issues/164690)).
- **Satisfaction signals:** security patching is active, the community is highly engaged, and maintainers are merging/refactoring across model catalog, memory indexing, and UI. **Dissatisfaction signals:** multiple P0s remain open for weeks, many high-value issues carry `stale` or `needs-product-decision` labels, and release validation still encounters flaky tests.

## 8. Backlog Watch

### Long-unanswered / high-impact issues

- [Issue #112638](https://github.com/openclaw/openclaw/issues/112638) — Created 2026-07-22, P2, stale. `session.maintenance enforce` mode does not bound the store because thread/channel entries are exempt from reclaim. Long-standing data-growth risk.
- [Issue #126533](https://github.com/openclaw/openclaw/issues/126533) — Created 2026-08-20, P2, stale. Multi-agent fanout drops or misroutes `MESSAGE_CREATE` when a default bot account and a more-specific binding both match. Message-loss risk.
- [Issue #127195](https://github.com/openclaw/openclaw/issues/127195) — Created 2026-08-21, P2, stale. Sixteen call sites emit the identical “changed while starting work” error with no reason code, making production diagnosis difficult.
- [Issue #150250](https://github.com/openclaw/openclaw/issues/150250) — Created 2026-09-16, P3 feature. Skill Workshop learning coverage and behavioral reuse remains a roadmap-level request.
- [Issue #153604](https://github.com/openclaw/openclaw/issues/153604) — Created 2026-09-20, P2, stale. Removal of `config.loadConfig` breaks third-party plugins such as `wecom-openclaw-plugin`; no shim or load-time detection.
- [Issue #153706](https://github.com/openclaw/openclaw/issues/153706) — Created 2026-09-20, P2, stale. Closed ACP sessions project `agentRuntime` as `{id:"codex", source:"implicit"}`, asserting a runtime they never use.
- [Issue #154524](https://github.com/openclaw/openclaw/issues/154524) — Created 2026-09-21, P2, stale. Accessibility request for screen-reader navigation of chat messages.
- [Issue #154482](https://github.com/openclaw/openclaw/issues/154482) — Created 2026-09-21, P2, stale. Permanent MAIN session history lifecycle has no supported export/trim/rollover path.

### PRs needing maintainer attention

- [PR #177691](https://github.com/openclaw/openclaw/pull/177691) — P1, compatibility and security-boundary risks, still “needs proof.” Important Discord/Codex state durability fix.
- [PR #180200](https://github.com/openclaw/openclaw/pull/180200), [PR #180214](https://github.com/openclaw/openclaw/pull/180214), [PR #180247](https://github.com/openclaw/openclaw/pull/180247) — created 2026-10-22, marked ready for maintainer look; cover GitHub reconnect flow, compaction provenance, and tool timeout outcomes.
- [PR #182553](https://github.com/openclaw/openclaw/pull/182553) — created 2026-10-24, P1, needs proof. Queued-message runtime context labeling; narrower follow-up split into [PR #187833](https://github.com/openclaw/openclaw/pull/187833).
- [PR #187542](https://github.com/openclaw/openclaw/pull/187542) — dependabot actions-group update, waiting on maintainer. Low-risk maintenance but contributes to review queue load.

**Bottom line:** OpenClaw is highly active and security-responsive, with strong ongoing work in model catalog, memory indexing, and UI correctness. The main risk is the concentration of unresolved P0/P1 session-state, gateway-recovery, and message-delivery failures, several of which have been open for weeks without linked fix PRs.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — Personal AI Assistant / Agent OSS Ecosystem
**Date:** 2026-10-30  
**Projects:** OpenClaw, Hermes Agent, IronClaw, QwenPaw, ZeroClaw  
**Data caveat:** Digests use different sampling windows and comment/reaction availability. Health scores below are qualitative analyst ratings (0–10), not direct benchmarks. IronClaw had no activity.

---

## 1. Ecosystem Overview

The personal AI assistant / agent OSS landscape is in a **high-activity but reliability-heavy phase**. Projects are no longer competing mainly on feature novelty; they are converging on persistent multi-channel operation, durable session state, memory correctness, provider/auth resilience, and operational safety. OpenClaw is the largest and most active reference point by throughput, while Hermes Agent, QwenPaw, and ZeroClaw occupy narrower but technically distinct niches. Release cadence is uneven: only OpenClaw shipped a patch, while peers are accumulating fixes toward future cuts. The dominant ecosystem risk is not contribution volume but **merge/review capacity and unresolved high-severity reliability debt**.

---

## 2. Activity Comparison

| Project | Issues (last 24h) | PRs (last 24h) | Release status | Health score |
|---|---:|---:|---|---:|
| **OpenClaw** | 170 updated; 131 active/open | 500 updated; 291 open; 209 merged/closed | **v2026.10.9** security/dependency patch; no breaking changes | **7.2/10** — high velocity and security-responsive, but elevated P0/P1 reliability risk |
| **Hermes Agent** | 17 updated; 17 open; 0 closed | 50 updated; 37 open; 13 merged/closed | No release; pre-release stabilization lull | **6.4/10** — strong throughput, but release stalled and backlog growing |
| **IronClaw** | 0 | 0 | None | **N/A** — dormant in window |
| **QwenPaw** | 13 updated; 9 closed | 41 updated; 27 open; 14 merged/closed | No release; stabilizing **2.3.0-beta.1** | **6.8/10** — active and responsive, but beta-fragile and review-bound on large PRs |
| **ZeroClaw** | 1 updated; 1 closed; 0 active open | 50 updated; 49 open; 1 merged/closed | No release; pre-**v0.9.0** staging | **5.5/10** — deep pipeline, but low merge velocity and author-action backlog |

**Readout:** OpenClaw operates at roughly **10× the PR update volume** of peers and is the only project shipping a release in-window. QwenPaw has the healthiest merge ratio among active peers, while ZeroClaw shows the clearest review bottleneck.

---

## 3. OpenClaw’s Position

**Advantages vs peers**
- **Scale:** 500 PR updates, 209 merged/closed PRs, and 170 issue updates in 24h — far above Hermes, QwenPaw, and ZeroClaw.
- **Release responsiveness:** shipped a security/dependency patch while peers shipped nothing.
- **Breadth:** covers multi-agent gateway operation, session-state lifecycle, memory promotion, model catalog/thinking profiles, Discord/Codex persistence, memory-indexing resilience, sandboxing, and multiple channel adapters.
- **Community gravity:** the largest visible contributor and issue pipeline in this set; likely the de facto reference implementation for persistent agent runtimes.

**Technical approach differences**
OpenClaw is **gateway-centric and runtime-heavy**. Its issues cluster around state-lifecycle leases, crash/wake recovery, memory promotion, message-loss prevention, and provider authentication — i.e., the hard operational core of a persistent multi-agent runtime. By contrast:
- **Hermes** is more Desktop/messaging-parity and install/update oriented.
- **QwenPaw** is console/plugin/PawApp oriented.
- **ZeroClaw** is systems-oriented around event-sourced durability, Goal Mode, and ZeroCode TUI.
- **IronClaw** is inactive in this window.

**Community size comparison**
OpenClaw’s activity is an order of magnitude larger than peers: 500 PR updates vs 41–50 for Hermes/QwenPaw/ZeroClaw, and 170 issue updates vs 1–17. However, OpenClaw also carries the highest concentration of unresolved P0/P1 reliability issues, so scale does not equal uniformly superior health.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects | Specific needs |
|---|---|---|
| **Durable session/state recovery** | OpenClaw, Hermes, QwenPaw, ZeroClaw | Crash/wake recovery, lease ownership, append-only event history, migration-safe resume, rollback/rewind, restart-durable bindings |
| **Memory correctness and trust** | OpenClaw, QwenPaw, ZeroClaw | Promotion/recall eviction, silent memory loss, concurrent store safety, recall leakage, checkpoint semantics, visible telemetry |
| **Silent-failure observability** | Hermes, QwenPaw, ZeroClaw, OpenClaw | Reason codes, visible warnings, update receipts, timeout feedback, debug-level-only failures, “success=True” masking data loss |
| **Channel parity and reliability** | OpenClaw, Hermes, QwenPaw, ZeroClaw | Telegram/Slack/Discord/Matrix parity, media delivery, rich messages, typing/status indicators, mention gating, restart persistence |
| **Provider/auth/model-routing resilience** | OpenClaw, Hermes, QwenPaw, ZeroClaw | Codex/claude-cli auth, OAuth refresh locks, OpenRouter pricing/key rotation, thinking controls, local model discovery, model-catalog consistency |
| **Security/sandbox/secrets** | OpenClaw, Hermes, QwenPaw, ZeroClaw | Workspace scoping, secret redaction, approval routing, prompt-injection false positives, CLI secret masking, Code Mode safety |
| **Install/update/packaging reliability** | Hermes, QwenPaw, ZeroClaw, OpenClaw | PM repair on case-insensitive FS, partial-clone handling, update receipts, PyInstaller assets, plugin loading, dependency patching |
| **Agent-loop and cost control** | QwenPaw, ZeroClaw, Hermes, OpenClaw | Doom-loop guards, configurable loop-breaking, cost overrides, negative pricing, billing correctness, usage visibility |

**Common signal:** users are treating these systems as **production infrastructure**, not demos. The highest-value work is increasingly about predictable state, observable failure, and safe automation rather than new UI surfaces.

---

## 5. Differentiation Analysis

| Project | Feature focus | Target users | Architecture signal |
|---|---|---|---|
| **OpenClaw** | Persistent multi-channel, multi-agent runtime; session lifecycle; memory promotion; model catalog; sandboxing | Power users, operators, multi-channel agent deployments | Gateway-centric runtime with state leases, memory pipeline, channel adapters, security boundaries |
| **Hermes Agent** | Desktop/messaging parity, install/update reliability, Slack/Telegram/Discord commands, skills catalog | Desktop and headless/remote users; multi-profile gateway operators; Slack teams | Desktop client + gateway + package/install manager + skills/plugins |
| **QwenPaw** | Plugin ecosystem, web Console, PawApp SDK/control plane, JEV security mode, Auto-Dream memory | Developers, console/hub admins, beta testers, plugin authors | Plugin-isolated architecture, Console/PawApp layers, memory recall plumbing, provider integrations |
| **ZeroClaw** | Durable event-sourced sessions, Goal Mode, ZeroCode TUI, cost controls, channel richness | Operators and developers needing durability, auditability, TUI workflows | Systems-oriented runtime with append-only session history, goal lifecycle, MCP/service robustness |
| **IronClaw** | No activity in window | Unknown | Cannot assess |

**Key difference:** OpenClaw is broadest and most “platform-like”; Hermes is most Desktop/install-operational; QwenPaw is most plugin/Console-oriented; ZeroClaw is most durability/event-history-oriented. OpenClaw competes on breadth and scale, not on a single narrow workflow.

---

## 6. Community Momentum & Maturity

**Tier 1 — Scale leader, rapid + shipping**
- **OpenClaw:** Very high activity, large contributor base, security patch shipped. Maturity is high by scale, but reliability risk is also highest due to unresolved P0/P1 session-state and recovery failures.

**Tier 2 — Fast iterators, stabilizing**
- **Hermes Agent:** Strong PR throughput and contributor diversity, but zero issue closures and no release. Backlog pressure and install/update regressions are the main drags.
- **QwenPaw:** High merge velocity and responsive triage, but 2.3.0-beta.1 regressions and large-PR review bottleneck. Good first-time-contributor signals.
- **ZeroClaw:** Deep pipeline and clear roadmap staging, but 1 merge vs 49 open PRs. Review throughput and author follow-up are the bottleneck; pre-v0.9.0.

**Tier 3 — Dormant**
- **IronClaw:** No activity in the reporting window.

**Momentum read:** OpenClaw is iterating and shipping at ecosystem-leading scale. QwenPaw is iterating fastest relative to its size. Hermes is accumulating fixes without a release. ZeroClaw has architectural ambition but is merge-constrained.

---

## 7. Trend Signals

1. **Durable, replayable state is becoming table stakes.**  
   OpenClaw’s session-state failures, ZeroClaw’s append-only event history, Hermes’ migration/session-resume bugs, and QwenPaw’s rewind/decision-persistence asks all point to the same requirement: agents must survive crashes, restarts, migrations, and compaction without losing work.

2. **Memory is a trust surface, not a feature checkbox.**  
   Silent memory loss, promotion inconsistency, recall leakage, and concurrent-write data loss appear across OpenClaw, QwenPaw, and ZeroClaw. Developers should treat memory as a transactional, observable subsystem with explicit success/failure semantics.

3. **Silent failure is worse than loud failure.**  
   Hermes’ Slack status regression, QwenPaw’s “success=True” memory drop, and ZeroClaw’s 600s silent waits show users will tolerate bugs better than invisible bugs. Reason codes, warnings, and telemetry are now product requirements.

4. **Multi-channel parity is a competitive baseline.**  
   Telegram, Slack, Discord, Matrix, and web consoles all need consistent media handling, rich messages, typing/status, and restart-durable bindings. Channel-specific regressions are production blockers.

5. **Provider abstraction remains fragile.**  
   Codex/claude-cli auth, OAuth locks, OpenRouter pricing/key rotation, thinking controls, local model discovery, and model-catalog mismatches are recurring. A robust provider layer needs retries, auth recovery, cost correctness, and clear diagnostics.

6. **Security controls must be precise, not theatrical.**  
   Sandbox path escapes, secret exposure, approval routing, and prompt-injection false positives appear across all active projects. Over-blocking ordinary prose is a satisfaction risk; under-blocking is a safety risk. Developers need calibrated guardrails with explainable decisions.

7. **Install/update/packaging is part of the agent product.**  
   PM repair failures, partial clones, PyInstaller asset omissions, plugin-load failures, and update receipts stuck in “running” are not side issues — they determine whether users can operate agents reliably.

8. **Review/design capacity is the ecosystem bottleneck.**  
   ZeroClaw’s 49-open/1-closed PR day and QwenPaw’s XXXL PR queue show contribution volume can outpace maintainer bandwidth. Projects with clear architectural decision records and smaller reviewable PRs will convert community energy into shipped reliability faster.

**Bottom line for AI agent developers:** build for **durable state, observable memory, channel parity, provider resilience, precise security, and reliable install/update paths**. Feature breadth matters, but in this window the ecosystem’s scarce resource is trustworthiness under persistent, multi-channel operation.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — Project Digest
**Date:** 2026-10-30 · **Repo:** [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. Today's Overview

Hermes Agent is in a high-throughput maintenance phase: 50 PRs were touched in the last 24 hours (37 open, 13 merged/closed), against 17 issue updates — all of which remain open. No release was cut, so the merged work is accumulating toward the next version rather than shipping. The issue pipeline skewed heavily toward fresh reports: 6 of the 17 items were created on 2026-10-29, several referencing v0.22.5 and current `main`, which indicates active dogfooding on recent builds. Activity is **high**, but the signal is almost entirely bug-fix and hardening work — there is no new feature landing in a release, and the open-issue backlog is growing faster than it is being closed (0 closes today). Overall health reads as *stable but backlog-pressured*, with a notable concentration of regressions around Slack integration, install/update paths, and Desktop session state.

---

## 2. Releases

**None.** No new tags or releases in the reporting window, and no release notes to summarize. This is the second consecutive signal that the project is in a pre-release stabilization lull; 13 merged/closed PRs are queued for the next cut. Maintainers should expect the next release to be dominated by:
- Slack adapter compatibility fixes (slack-sdk ≥ 3.44)
- Install/update receipt and partial-clone handling
- Desktop session-resume and boot-path corrections

No breaking changes or migration notes to report today.

---

## 3. Project Progress

13 PRs were merged or closed in the window. Three are explicitly confirmed closed in the visible sample:

| PR | Title | Status | Signal |
|---|---|---|---|
| [#110626](https://github.com/NousResearch/hermes-agent/pull/110626) | `fix(redact): mask assignments in secret-bearing file reads` | **CLOSED** | Security hardening shipped — `read_file`/`search_files` now run ENV/JSON/YAML assignment passes on credential-shaped paths. Completes the file-read half of the #110228 gate. |
| [#69563](https://github.com/NousResearch/hermes-agent/pull/69563) | `skills(gaming): game 3D asset pipeline — TRELLIS.2 + SkinTokens` | **CLOSED** | Superseded — the same author re-opened the work as [#146590](https://github.com/NousResearch/hermes-agent/pull/146590) with a broader three-skill layout. Indicates a deliberate redesign before merge. |
| [#146583](https://github.com/NousResearch/hermes-agent/pull/146583) | `docs: official search titles on docs home and install page` | **CLOSED** | SEO/docs polish only; no functional impact. |

**Features advancing (open, not yet merged):**
- **Messaging parity:** [#145831](https://github.com/NousResearch/hermes-agent/pull/145831) adds a `/project` slash command to Slack/Telegram/Discord, closing the gap with Desktop's "Move to project."
- **Skills catalog expansion:** three parallel gaming/songwriting skill PRs from `Jpalmer95` — [#146590](https://github.com/NousResearch/hermes-agent/pull/146590) (TRELLIS.2 image-to-3D + SkinTokens rigging), [#146593](https://github.com/NousResearch/hermes-agent/pull/146593) (puppeteer-animation, video-guided motion), [#146592](https://github.com/NousResearch/hermes-agent/pull/146592) (songwriting set arcs).
- **Gateway robustness:** [#146261](https://github.com/NousResearch/hermes-agent/pull/146261) extends the respawn-storm brake to already-installed Scheduled Tasks via drift check; [#132665](https://github.com/NousResearch/hermes-agent/pull/132665) adds `HERMES_DISABLE_SERVICE_UNIT_REFRESH` for deployments where a pipeline owns systemd units.

---

## 4. Community Hot Topics

| Item | Engagement | Underlying need |
|---|---|---|
| **[#38519](https://github.com/NousResearch/hermes-agent/issues/38519)** — Desktop frontend-only install (Windows) | **31 👍, 22 comments**, open since 2026-06-03 | The single most-upvoted item in the window. Users run the agent on a headless/remote machine and want Desktop as a thin client. The 5-month lifetime with no resolution is the clearest unmet architectural request in the project. |
| **[#110374](https://github.com/NousResearch/hermes-agent/issues/110374)** — Slack status silently broken with slack-sdk ≥ 3.44 | **16 👍, 10 comments** | Silent failure is the core grievance: `invalid_arguments` is debug-logged by design, so users see a dead indicator with no diagnostic. |
| **Slack triplicate cluster** — [#112866](https://github.com/NousResearch/hermes-agent/issues/112866) (6c), [#132594](https://github.com/NousResearch/hermes-agent/issues/132594) (4c, already tagged `duplicate`) | ~10 comments combined | Three independent reporters hit the same `agents.sessions.setStatus` free-text regression across v0.21.5 Docker and later. Strong evidence the bug is widespread and the fix is not yet visible to users. |
| **[#143150](https://github.com/NousResearch/hermes-agent/issues/143150)** — Desktop `storage_unavailable` after multiplex migration | 5 comments | Multi-profile → one-gateway migration leaves a route unmigrated in `state_meta`, breaking session resume. Migration-path reliability is the need. |
| **[#135910](https://github.com/NousResearch/hermes-agent/issues/135910)** — `pm repair` fails on case-insensitive FS | P1, 4 comments | macOS/APFS + Docker bind mounts are a mainstream dev configuration; `Errno 17` on the bundled terminfo blocks *every* PM-routed action. |

**Analysis:** the community's attention is split between one strategic ask (frontend-only Desktop) and one operational regression cluster (Slack). The Slack cluster is notable for how it is being handled: it has generated three separate issues and a `duplicate` tag rather than a single canonical thread, which fragments the 👍 signal and makes prioritization harder.

---

## 5. Bugs & Stability

Ranked by severity and blast radius:

**P1 — Install blocker**
- **[#135910](https://github.com/NousResearch/hermes-agent/issues/135910)** · `pm repair` cannot commit a dependency environment on case-insensitive filesystems. `shutil.copytree` dies with `Errno 17` on bundled CPython terminfo; every PM-routed action then fails. Tagged `sweeper:risk-compatibility`, `os/macos`. **No fix PR visible.**

**P2 — Crashes & data-access regressions**
- **[#146537](https://github.com/NousResearch/hermes-agent/issues/146537)** · TUI session switcher (`Ctrl+X` / `/sessions`) **kills the entire TUI** via `Cannot read properties of null (reading 'replace')` in `shortModel` when a live session row has a NULL model. Hard crash, filed 2026-10-29. **No fix PR visible.**
- **[#143150](https://github.com/NousResearch/hermes-agent/issues/143150)** · Desktop cannot resume prior sessions after `gateway.multiplex_profiles: true` migration → `storage_unavailable`. Blocks access to historical chat data. **No fix PR visible.**
- **[#110374](https://github.com/NousResearch/hermes-agent/issues/110374) / [#112866](https://github.com/NousResearch/hermes-agent/issues/112866) / [#132594](https://github.com/NousResearch/hermes-agent/issues/132594)** · Slack status/typing indicators silently dead on slack-sdk ≥ 3.44. Functionally cosmetic but affects every Slack turn. Related open PR [#145832](https://github.com/NousResearch/hermes-agent/pull/145832) fixes Slack `display_name` handling, **not** this regression.
- **[#137098](https://github.com/NousResearch/hermes-agent/issues/137098)** · Cost estimates go **negative** for OpenRouter routed/variable-price slugs (negative pricing sentinel priced at face value). Trust-eroding for billing. Adjacent PR [#55855](https://github.com/NousResearch/hermes-agent/pull/55855) addresses OpenRouter key rotation on upstream 429s, not pricing.
- **[#146502](https://github.com/NousResearch/hermes-agent/issues/146502)** · `auxiliary.compression.model` is ignored — `summary_model_override` hardcoded to `None`, so compression always uses the main model and stalls when that model is slow.
- **[#146584](https://github.com/NousResearch/hermes-agent/issues/146584)** · Windows Desktop boot runs `hermes gateway ensure` twice; the redundant 2.5 s call dominates a 5.0 s boot.

**P3 — Correctness & guard behavior**
- **[#146586](https://github.com/NousResearch/hermes-agent/issues/146586)** · `is_runaway_repetition()` fails to cut a newline-free loop when ≥5 distinct lines precede it — **fix PR exists: [#146587](https://github.com/NousResearch/hermes-agent/pull/146587)**.
- **[#146582](https://github.com/NousResearch/hermes-agent/issues/146582)** · `execute_code` lifecycle guard false-positives on documentation that merely *mentions* a gateway restart — and is trivially bypassed by a splice. Both over- and under-blocking.
- **[#146577](https://github.com/NousResearch/hermes-agent/issues/146577)** / **[#146578](https://github.com/NousResearch/hermes-agent/issues/146578)** · Update receipts stuck at `outcome: "running"` after success (next run treats it as interrupted); `git merge-base` 10 s timeout on partial-clone installs. Both `area/install-update`, both filed by the same reporter.
- **[#146495](https://github.com/NousResearch/hermes-agent/issues/146495)** · Linux Desktop: newly created projects are unchecked in the Projects filter by default.

**Security-flagged**
- **[#146564](https://github.com/NousResearch/hermes-agent/issues/146564)** · Kanban workers must relay protected-write approvals to an **authenticated owner responder**; worker sessions are hidden from normal approval surfaces, so `AGENTS.md`-class writes can stall or proceed without owner visibility.

---

## 6. Feature Requests & Roadmap Signals

| Request | Likelihood in next version | Rationale |
|---|---|---|
| **Frontend-only Desktop install** ([#38519](https://github.com/NousResearch/hermes-agent/issues/38519)) | **Medium** | Highest demand (31 👍) but architectural — requires a connection-first setup flow. Five months open with 22 comments suggests design debate, not neglect. Tagged `needs-decision`. |
| **`/project` for messaging surfaces** ([#145831](https://github.com/NousResearch/hermes-agent/pull/145831)) | **High** | PR is open, small, and closes a clear Desktop/messaging parity gap. |
| **Gaming & creative skills pack** ([#146590](https://github.com/NousResearch/hermes-agent/pull/146590), [#146593](https://github.com/NousResearch/hermes-agent/pull/146593), [#146592](https://github.com/NousResearch/hermes-agent/pull/146592)) | **High** | Three PRs in one day, one already reworked from a closed predecessor. Skills are opt-in and low-risk to merge. |
| **Model-usage plugin / billing gauge** ([#146581](https://github.com/NousResearch/hermes-agent/pull/146581)) | **Medium** | Catalog-only addition (pinned to `9962d96`, v1.1.0), low merge cost — but external-plugin dependency review may slow it. |
| **`HERMES_DISABLE_SERVICE_UNIT_REFRESH`** ([#132665](https://github.com/NousResearch/hermes-agent/pull/132665)) | **Medium** | Tagged `risk-compatibility`; environment opt-outs are usually accepted but need docs. |
| **Cost-visibility & billing correctness** ([#137098](https://github.com/NousResearch/hermes-agent/issues/137098)) | **Medium** | Negative estimates plus the usage-gauge plugin signal growing user attention to spend tracking. |

**Directional read:** the roadmap is being pulled in two directions — *depth* (skills/creative tooling, plugin catalog) and *operational maturity* (install/update reliability, multi-profile migration, service management). The second has far more open bugs and no equivalent PR volume, which is the main imbalance in the current queue.

---

## 7. User Feedback Summary

**Pain points, in users' own framing:**
- *"Frontend only installation for windows"* — users have already solved the distributed-agent problem manually and want Desktop to stop assuming co-location. This is a workflow request, not a bug.
- *"silently broken"* / *"silently disappears"* / *"silently fails"* — the word "silently" appears in all three Slack reports. Users tolerate breakage far better than breakage with no error surface; debug-level logging of protocol failures is the specific complaint.
- *"no dependency environment can ever be committed"* — the P1 PM failure is described as absolute, not intermittent, on affected filesystems.
- *"update receipt stays 'running' after a successful update"* — a trust problem: the log says success, the state says interrupted. Users cannot tell whether their install is sound.

**Satisfaction signals:** high engagement from repeat contributors (multiple PRs from `Jpalmer95`, `thisisnotajokee` filing three precise install-update reports in one day with version hashes and timings), and detailed, reproducible bug reports — a sign of an invested, technically capable user base rather than a frustrated one.

**Dissatisfaction signals:** the Slack regression has persisted across at least three releases (v0.21.5 → v0.21.6 → v0.22.5 era) and produced duplicate reports instead of a resolution. The #38519 request has been open since June with 31 upvotes and no visible decision. Both are accumulating goodwill debt.

**Use-case profile visible in this window:** headless/remote agent hosting, multi-profile gateways, Slack as a primary surface, macOS/Docker Desktop development, Windows Desktop as a client, local-model (LM Studio/loopback) inference (per [#135291](https://github.com/NousResearch/hermes-agent/pull/135291)), and GPU-free creative work via Hugging Face Spaces.

---

## 8. Backlog Watch

Items needing maintainer attention, ordered by staleness × impact:

1. **[#38519](https://github.com/NousResearch/hermes-agent/issues/38519)** — *Open 149 days*, 22 comments, 31 👍, tagged `needs-decision`. The highest-demand item in the project has no visible decision record. Even a "won't do / here's why" comment would convert heat into information.
2. **[#135910](https://github.com/NousResearch/hermes-agent/issues/135910)** — *Open 20 days*, **P1**, `risk-compatibility`, no linked fix PR. This is the only P1 in the window and it blocks all PM-routed actions on a mainstream macOS/Docker configuration.
3. **[#99500](https://github.com/NousResearch/hermes-agent/issues/99500)** — *Open 60 days*, Exa keyless ring never advances on masked 429s ("Unrecognized MCP response shape"). Adjacent PR [#146585](https://github.com/NousResearch/hermes-agent/pull/146585) fixes a *different* keyless-Exa defect (3,000-char cap), so the ring logic remains unfixed.
4. **[#110374](https://github.com/NousResearch/hermes-agent/issues/110374)** — *Open 47 days*, 16 👍, and the canonical thread for a triplicate cluster. Needs either a fix or an explicit consolidation of [#112866](https://github.com/NousResearch/hermes-agent/issues/112866) and [#132594](https://github.com/NousResearch/hermes-agent/issues/132594) into it.
5. **[#55855](https://github.com/NousResearch/hermes-agent/pull/55855)** — *Open 122 days*, stops rotation of healthy OpenRouter keys on upstream 429s. The classifier logic already exists; this is a long-stalled correctness fix in the same OpenRouter area as bug #137098.
6. **[#143150](https://github.com/NousResearch/hermes-agent/issues/143150)** — *Open 8 days*, `area/sessions` + `area/profiles`. Small age but high consequence: users upgrading to multiplexed gateways lose access to existing sessions. Migration bugs worsen with time as more installs upgrade.
7. **[#69563](https://github.com/NousResearch/hermes-agent/pull/69563)** — Closed after 99 days and immediately re-filed as [#146590](https://github.com/NousResearch/hermes-agent/pull/146590). Worth a maintainer note on what the redesign criteria were, so the replacement doesn't repeat the cycle.

---

### Health Snapshot

| Dimension | Reading |
|---|---|
| Throughput | **Strong** — 50 PR updates/day, 13 closed |
| Release cadence | **Stalled** — 0 releases; fix backlog accumulating |
| Issue closure rate | **Weak** — 0 closed against 17 updated |
| Severity distribution | 1× P1, ~8× P2, ~6× P3 among visible issues |
| Contributor diversity | **Healthy** — many distinct authors, repeat filers |
| Highest-risk theme | Install/update & migration paths (P1 + 4 P2/P3 items, few fix PRs) |
| Highest-demand unmet ask | Frontend-only Desktop (#38519) |

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/QwenPaw">agentscope-ai/QwenPaw</a></summary>

# QwenPaw Project Digest — 2026-10-30

## 1. Today's Overview

QwenPaw shows **high-velocity maintenance activity**: 13 issues and 41 PRs were updated in the last 24 hours, with 9 issues closed and 14 PRs merged/closed against 27 still open. No new release shipped, but the activity is heavily concentrated on stabilizing the **2.3.0-beta.1** line, which generated several regression reports (plugin loading, desktop packaging, optional-dependency memory use). The project also closed a long-running wontfix decision on agent doom loops (#6116) and landed security/CLI hardening (#8492, #8501). Overall health is **active but beta-fragile**: strong contributor throughput and responsive triage, offset by a growing queue of large (XL–XXXL) PRs awaiting review. First-time contributors (#8291, #8400) indicate a healthy on-ramp.

## 2. Releases

None in this cycle.

## 3. Project Progress

Five PRs moved to closed/merged in the visible window, spanning security, providers, console UX, and website infrastructure:

- **[#8492](https://github.com/agentscope-ai/QwenPaw/pull/8492)** `fix(security): prevent false-positive approvals for Code Mode in JEV mode` — tightens the tool-review gate so Code Mode operations aren't auto-approved incorrectly; directly relevant to agent safety.
- **[#8497](https://github.com/agentscope-ai/QwenPaw/pull/8497)** `fix(plugins): tolerate import cache refresh failures during plugin loading` — the fix for the 2.3.0-beta.1 startup failure (#8473); restores plugin entry-point loading.
- **[#8358](https://github.com/agentscope-ai/QwenPaw/pull/8358)** `fix(providers): honor thinking defaults and declared wire controls` — resolves a Console/backend mismatch where `thinking_enabled=off` was not transmitted to OpenAI-compatible providers.
- **[#5490](https://github.com/agentscope-ai/QwenPaw/pull/5490)** `feat(console): navigable fullscreen image gallery for chat media` — long-lived feature (opened June) finally closed; wraps tool-card images in a single `Image.PreviewGroup` for gallery navigation.
- **[#8253](https://github.com/agentscope-ai/QwenPaw/pull/8253)** `feat(website): add JSON-driven evaluation index` — bilingual evaluation leaderboard with Pareto frontier and SDK history.

Additional in-flight work advancing: memory-recall hardening ([#8457](https://github.com/agentscope-ai/QwenPaw/pull/8457), [#7835](https://github.com/agentscope-ai/QwenPaw/pull/7835)), CLI secret masking ([#8501](https://github.com/agentscope-ai/QwenPaw/pull/8501)), and Ollama model discovery ([#8309](https://github.com/agentscope-ai/QwenPaw/pull/8309)).

## 4. Community Hot Topics

| Item | Activity | Link |
|---|---|---|
| **#6116** Doom loop: agent repeats same tool call in one turn | 9 comments, **closed wontfix** | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/6116) |
| **#8464** Manual `/compact` ignores session-level model switch | 4 comments, closed | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/8464) |
| **#8500** Auto-Dream silently drops memory, checkpoints anyway | 2 comments, **open** | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/8500) |
| **#8473** All backend plugins fail to load in 2.3.0-beta.1 | 2 comments, closed (fix: #8497) | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/8473) |

**Analysis of underlying needs:**
- **Agent loop control** is the most emotionally charged topic (9 comments). The user documented ~6 repeated identical tool calls before the system intervened, wasting tokens and API budget. The **wontfix** resolution is notable — it likely signals a design stance (e.g., the 6-repetition guard is considered "working as intended") rather than dismissal. This may resurface as a request for configurable/earlier loop-breaking.
- **Session state consistency** (#8464): users switching models mid-session expect *all* operations — including compaction — to honor the active model. The root cause is `active_model` resolution reading agent-level config instead of session context.
- **Silent data loss** (#8500) is the highest-trust-risk open thread: a "success=True" report masking dropped memory is exactly the class of bug that erodes user confidence in autonomous memory features.

## 5. Bugs & Stability

Ranked by severity (all reported/updated 2026-10-29):

1. **CRITICAL — [#8473](https://github.com/agentscope-ai/QwenPaw/issues/8473)** *2.3.0-beta.1: all backend plugins fail to load at startup* (12/12 plugins on reporter's host). Root cause: unguarded `importlib.invalidate_caches()` in `module_isolation.py:220`, same root cause as prior #8265, new call site. **Fix exists:** [#8497](https://github.com/agentscope-ai/QwenPaw/pull/8497) (closed).
2. **HIGH — [#8488](https://github.com/agentscope-ai/QwenPaw/issues/8488)** *Desktop/PyInstaller build omits `visual_compression` assets* → `FileNotFoundError: atlas-gray-native.ts`; Visual Compact silently no-ops with no user-visible warning. Packaging regression in 2.3.0-beta.1. **Open, no fix PR referenced.**
3. **HIGH — [#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500)** *Auto-Dream silently drops a full day of memory* when the extract step can't parse the agent reply, yet still checkpoints the files so they are never retried. Reports `success=True` with no telemetry. **Open, no fix PR referenced.**
4. **MEDIUM — [#8464](https://github.com/agentscope-ai/QwenPaw/issues/8464)** *Manual `/compact` always uses agent-level `active_model`*, failing with 400 when that model strictly validates compaction params. Closed.
5. **MEDIUM — [#8490](https://github.com/agentscope-ai/QwenPaw/issues/8490)** *Opening Voice Transcription settings imports `whisper` into the server process* (~690 MB RSS, never released) just to check availability. **Open.**
6. **LOW — [#8486](https://github.com/agentscope-ai/QwenPaw/issues/8486)** Tool-call `<>` icon clipped on left edge — container lacks horizontal padding. Cosmetic. **Open.**

**Regression cluster:** three of the four open bugs (#8488, #8490, #8486) are from 2.3.0-beta.1-era builds, suggesting the beta needs a focused stabilization pass before GA. A security-adjacent hardening PR, [#8501](https://github.com/agentscope-ai/QwenPaw/pull/8501) (mask env var values in `env list`/`env set`), also addresses plaintext secret exposure in the CLI.

## 6. Feature Requests & Roadmap Signals

Today's closed enhancement issues span the agent-control and long-session UX surface:

- **[#6189](https://github.com/agentscope-ai/QwenPaw/issues/6189)** `save_decision()` API — structured decision persistence to survive context compaction. Strong framework-level ask (chicken-and-egg problem: agent forgets decisions *then* can't archive them).
- **[#4356](https://github.com/agentscope-ai/QwenPaw/issues/4356)** Finer-grained file/tool guard — read-only paths, project-directory whitelists rather than blacklist-only.
- **[#4129](https://github.com/agentscope-ai/QwenPaw/issues/4129)** `/rewind` — rollback files/context to try alternate prompts or undo agent damage (direct Claude Code parity request).
- **[#7740](https://github.com/agentscope-ai/QwenPaw/issues/7740)** Hub-mode admin password reset.
- **[#8459](https://github.com/agentscope-ai/QwenPaw/issues/8459)** Easier access to unread push messages in the web Console.

**Prediction for next versions:** Given the beta-regression load, the immediate next release is likely a **2.3.0-beta.2/GA stabilization** rather than feature delivery. Signals that `save_decision`-style **context durability** and **rewind** could land in 2.3.x or 2.4: both address the same compaction-loss pain class as open bug #8500, and the project is already investing in related memory plumbing (#8457, #7835). File-guard granularity (#4356) is a natural pairing with the JEV/tool-review security work in #8492.

## 7. User Feedback Summary

**Pain points expressed today:**
- *Cost/efficiency:* Wasted tokens and API calls from doom loops (#6116) — users want earlier or configurable loop-breaking.
- *Predictability:* Mid-session model switches not honored by `/compact` (#8464) breaks a basic mental model of "what you select is what runs."
- *Trust in autonomy:* Silent memory loss (#8500) and silent no-ops (#8488) are worse than loud failures — users repeatedly ask for visible status/warnings.
- *Resource hygiene:* 690 MB RSS from a mere settings-page visit (#8490) matters on desktop/laptop deployments.
- *Operational basics:* Hub admins still can't reset user passwords (#7740); secrets print in plaintext in `env list` (addressed by #8501).

**Satisfaction signals:** high-quality, reproducible bug reports (notably from `feng183043996`, who filed #6116, #6189, #8500 and authored #8501) and first-time contributors (#8291, #8400) show an engaged community. Dissatisfaction is **beta-quality friction**, not fundamental direction — several complaints are packaging/lifecycle regressions rather than architectural objections.

## 8. Backlog Watch

Large PRs and long-running reviews that need maintainer bandwidth:

| Item | Age | Size | Concern |
|---|---|---|---|
| [#7874](https://github.com/agentscope-ai/QwenPaw/pull/7874) `feat(pawapp): redesign SDK and app control plane` | Since 2026-09-19 (~6 wks) | **XXXL** | Architectural fork in the road; blocks downstream PawApp work. |
| [#8034](https://github.com/agentscope-ai/QwenPaw/pull/8034) `fix(providers): bound inline media per request` | Since 2026-09-29 (~1 mo) | XL | Real gateway-failure mitigation; still `Under Review`. |
| [#7835](https://github.com/agentscope-ai/QwenPaw/pull/7835) `fix(memory): stop leaking auto-memory-recall payload to channels` | Since 2026-09-17 (~6 wks) | M | Duplicates problem space with #8457; needs consolidation decision. |
| [#8231](https://github.com/agentscope-ai/QwenPaw/pull/8231) `fix(console): persist market install provenance` | Since 2026-10-13 | M | Blocks reliable "Update All" for third-party plugins. |
| [#8499](https://github.com/agentscope-ai/QwenPaw/pull/8499) `(WIP) feat(providers): extract local model management into plugin` | New | **XXXL** | WIP; needs design review before it grows further. |

**Recommendation:** The open-PR queue (27) is skewed toward very large diffs — #7874, #8489, #8499, #8463, #8034. Review throughput, not contribution volume, is the current bottleneck. Two memory-recall PRs (#7835, #8457) should be reconciled into a single direction to avoid conflicting merges. Open bug #8500 (silent memory loss) currently has **no linked fix PR** and deserves triage priority given its trust impact.

---
*Data window: 2026-10-29 → 2026-10-30. Sources: [agentscope-ai/QwenPaw](https://github.com/agentscope-ai/QwenPaw).*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-10-30

**Repo:** [github.com/zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
**Data window:** activity updated 2026-10-29 (last 24h)

> **Data caveat:** the supplied dataset reports per-PR comment counts as `undefined` and 👍 = 0 across all items, so "most commented" / "most reacted" rankings cannot be computed. Sections below rank by *observable signal* (update recency, label weight, severity, age) and this is flagged where relevant. The single merged/closed PR today is **not** among the 20 items provided, so it cannot be named.

---

## 1. Today's Overview

ZeroClaw shows a strongly **review-bound, low-merge-velocity** day: 51 total issue/PR updates in 24h, but only **1 PR merged/closed** against **49 still open** — roughly a 1:50 close-to-update ratio. The issue queue was effectively cleared (1 updated, 0 open/active remaining), and the day's only closure was a documentation-translation cleanup issue ([#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076)), not a code change. PR composition skews heavy: **11 of the top 20 (55%) are `size:XL`** and **3 carry `risk:high`**, while **9 of 20 (45%) sit under `needs-author-action`**, pointing to an author-follow-up backlog rather than a maintainer-review backlog alone. No releases shipped, and no PR is labelled as merged in the visible window — consistent with a pre-release staging period around **v0.9.0**, which already appears as a release label on the closed issue. Contributor concentration is notable: **8 of the 20 visible PRs are `zerocode`-scoped work from a single author (Audacity88)**, several flagged `distinguished contributor`.

**Activity assessment:** high triage/update activity, low throughput; healthy pipeline depth, warning-level merge latency.

---

## 2. Releases

**No new releases in the last 24h.** Latest Releases list is empty.

Forward-looking signal only: the closed issue [#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076) carries the label `release:v0.9.0` while describing fixes for catalogue content introduced in **v0.8.7**. This implies **v0.9.0 is the next planned cut** and that at least some post-v0.8.7 documentation corrections are being rolled into it rather than a v0.8.x patch. No breaking-change or migration notes are available from this dataset.

---

## 3. Project Progress

**Merged/closed today:** 1 PR (identity not present in the provided top-20 slice) + 1 issue.

- **[#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076) — CLOSED (docs, release:v0.9.0)** — "Ship the v0.8.7 translation fixes found by a full read of the catalogues." Scope: `docs/book/po` catalogues (`fr`, `ja`, `es`, `zh-CN`), with most corrections on pages new in v0.8.7, especially `plugin-release-acceptance.md`. Reported as **incorrect information**, 1 comment, closed within ~1 day of filing (created 2026-10-28, updated 2026-10-29). Fast turnaround on a docs-only item.

**Feature advancement visible in-flight (unmerged):**
- **Goal execution lifecycle** — [#11881](https://github.com/zeroclaw-labs/zeroclaw/pull/11881) (Goal Mode V1, proposal 4/12) is explicitly staged and awaiting runtime-placement approval.
- **Append-only session event history** — [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921), the broadest-blast-radius change in the set (`risk:high`, `size:XL`, dozens of area labels).
- **Channel parity** — Telegram rich messages ([#11862](https://github.com/zeroclaw-labs/zeroclaw/pull/11862)) and reasoning streaming for Telegram/Slack ([#11744](https://github.com/zeroclaw-labs/zeroclaw/pull/11744)) continue the Matrix → Telegram/Slack feature migration.

Net: the day's *completed* work was documentation hygiene; the day's *active* work is a large, unmerged feature stack.

---

## 4. Community Hot Topics

Because comment/reaction counts are unavailable, the following are the **highest-signal active threads** by recency + label weight + scope. Notably, **all 20 visible PRs were updated on 2026-10-29**, which looks like a bulk triage/label sweep rather than organic per-thread discussion.

| Item | Why it matters |
|---|---|
| [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921) `feat(session): append-only session event history` | Highest-blast-radius PR open (`risk:high`, `size:XL`, ~60 area labels). Redefines the canonical conversation/execution history and replay semantics — touches every channel, provider and tool. |
| [#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301) `fix(agents): durable committed-rename recovery across CLI, gateway, RPC` | `priority:p1`, `risk:high`, `size:XL`, open 29 days. Cross-cutting durability fix that many subsystems depend on. |
| [#11881](https://github.com/zeroclaw-labs/zeroclaw/pull/11881) `feat(goal): accounted Goal execution lifecycle [4/12]` | A numbered multi-PR design series — the clearest roadmap artefact in the dataset. Blocked on core runtime-placement approval. |
| [#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004) `fix(memory): markdown store() append-only` | `priority:p1` data-integrity fix; small (`size:M`) but high user impact. |
| [#11744](https://github.com/zeroclaw-labs/zeroclaw/pull/11744) / [#11862](https://github.com/zeroclaw-labs/zeroclaw/pull/11862) | Adjacent channel features (reasoning streaming vs. rich messages) that likely need a shared design decision on Telegram/Slack message rendering. |

**Underlying need:** the hot set clusters into two demands — (a) **durability/consistency of agent state** (sessions, renames, memory) and (b) **channel UX parity** so Telegram/Slack match Matrix. Both are "make it trustworthy at scale" needs rather than new surface area.

---

## 5. Bugs & Stability

Ranked by severity/impact. Note: none of these were *reported* today; they are open fixes updated today.

| Sev | Item | Issue | Fix PR exists? |
|---|---|---|---|
| **P1 — data loss** | Concurrent `MarkdownMemory::store()` writes do read-modify-rewrite and can drop updates | `memory:backend` | **Yes** — [#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004), `priority:p1`, `needs-maintainer-review` |
| **P1 — stranded state** | Agent rename commits config before workspace/memory/cron/ACP/session state; partial failure leaves state under old alias and CLI cannot resume | `release-gate`, `domain:security` | **Yes** — [#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301), `priority:p1`, open 29d, `needs-author-action` |
| **P1/P2 — security FP** | Prompt guard flags any bare `;` or `\|` as command injection → ordinary prose, tables and tool output return `Suspicious`/`Blocked` | `security`, `runtime` | **Yes** — [#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068), `size:XS` |
| **P2 — hang/timeout** | Cleared `ask_user`/`poll` elicitations leave the daemon waiting the full tool timeout (600s for `ask_user`) with no user-visible signal | `zerocode` | **Yes** — [#11624](https://github.com/zeroclaw-labs/zeroclaw/pull/11624) |
| **P2 — broken tooling** | On Android, `canonicalize("/system/bin/sh")` fails `EPERM` under SELinux though `execve` works → **every native `shell` tool call fails** | `config` | **Yes** — [#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/12080), `size:S` |
| **P2 — stability** | One failed MCP recovery permanently poisons a connection (`RecoveryBarrier::poison()` has no clear path; `health_check()` only probes the transport) | `tool:mcp` | **Yes** — [#12061](https://github.com/zeroclaw-labs/zeroclaw/pull/12061), `size:S` |
| **P3 — perf/cost** | Personality files (`AGENTS.md`, `SOUL.md`, etc.) re-rendered on prompt rebuild → edits bust the prompt cache | `agent`, `runtime` | **Yes** — [#11698](https://github.com/zeroclaw-labs/zeroclaw/pull/11698), `size:XL` |

**Read:** every identified bug already has an open fix PR. The constraint is review/merge capacity, not diagnosis. The three `size:XS`/`S` fixes ([#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068), [#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/12080), [#12061](https://github.com/zeroclaw-labs/zeroclaw/pull/12061)) are the cheapest stability wins available today.

---

## 6. Feature Requests & Roadmap Signals

**Explicitly staged roadmap:**
- **Goal Mode V1** — [#11881](https://github.com/zeroclaw-labs/zeroclaw/pull/11881) is proposal **4 of 12**, i.e. a formal programme. Self-described as "a staged foundation, not an enablement or merge request," gated on **core runtime-placement approval**. Multi-quarter work.
- **Append-only session event history** — [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921): replay rebuilds state without repeating external effects. This is the architectural prerequisite for durable resume/undo.

**User-facing requests in flight:**
- **Channel richness & transparency:** Telegram rich messages (headings/lists/quotes/tables, opt-in via `channels.telegram.<alias>.rich_messages`, default **false**) — [#11862](https://github.com/zeroclaw-labs/zeroclaw/pull/11862); reasoning streaming parity for Telegram/Slack (`stream_reasoning = off|status|full`) — [#11744](https://github.com/zeroclaw-labs/zeroclaw/pull/11744).
- **Operator control:** `cost.allow_override` documented but previously wired to nothing; [#11589](https://github.com/zeroclaw-labs/zeroclaw/pull/11589) lets an operator override an exceeded cost limit instead of restarting the daemon.
- **ZeroCode UX cluster:** message timestamps in transcript ([#11622](https://github.com/zeroclaw-labs/zeroclaw/pull/11622)), per-pane session cap replacing a hard-coded 8 ([#11731](https://github.com/zeroclaw-labs/zeroclaw/pull/11731)), non-cancelling refresh (F5) ([#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457)), session-list persistence across restarts ([#11727](https://github.com/zeroclaw-labs/zeroclaw/pull/11727)), searchable keybindings ([#11505](https://github.com/zeroclaw-labs/zeroclaw/pull/11505)).
- **Memory:** opt-in external rerank ([#12036](https://github.com/zeroclaw-labs/zeroclaw/pull/12036), referenced by exception PR [#12037](https://github.com/zeroclaw-labs/zeroclaw/pull/12037)).

**Prediction for v0.9.0:** likely to ship the **small, contained fixes** — docs/translation corrections, the command-injection false-positive fix, the Android shell path fix, MCP connection eviction, webhook long-running timeout ([#11931](https://github.com/zeroclaw-labs/zeroclaw/pull/11931)), and possibly the Markdown memory append-only fix. The XL items (Goal Mode, session event history, channel streaming, prompt-cache stability) are unlikely to make it given 0 merges today, `risk:high` labels, and explicit approval gates.

---

## 7. User Feedback Summary

No direct user commentary is present in this dataset (comment counts unavailable; 1 comment on the sole issue). Pain points must be inferred from the PR/problem statements, which are unusually explicit:

- **Trust in persisted state** is the dominant theme. Users hit *silent* failures: lost memory writes under concurrency ([#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004)), a CLI that "could not resume" after a rename ([#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301)), a sidebar that forgets open sessions each launch ([#11727](https://github.com/zeroclaw-labs/zeroclaw/pull/11727)).
- **Silent waiting** is a recurring irritant: cleared elicitations that leave a 600s hang with no UI feedback ([#11624](https://github.com/zeroclaw-labs/zeroclaw/pull/11624)); no way to tell event ordering or durations without transcript timestamps ([#11622](https://github.com/zeroclaw-labs/zeroclaw/pull/11622)).
- **False-positive safety controls** degrade ordinary use — prose and tool output blocked as injection ([#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068)). This is a satisfaction risk: security features that misfire are reported as blocking, not protective.
- **Documentation drift** is a real complaint: v0.8.7 shipped translation catalogues with incorrect information, found only by a full manual read ([#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076)). Suggests the i18n release process lacks a verification gate.
- **Platform breadth friction:** Android users are fully blocked from shell tooling ([#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/11880) → #12080).
- **Satisfaction signal:** none quantifiable (all 👍 = 0). No evidence of dissatisfaction with direction; evidence of dissatisfaction with *reliability edge cases*.

---

## 8. Backlog Watch

Items at risk of stalling, needing maintainer attention:

| Age (as of 2026-10-30) | Item | Blocking factor |
|---|---|---|
| **29 days** | [#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301) — durable committed-rename recovery | `priority:p1` + `needs-author-action` + `risk:high`; the highest-value fix that is not moving. |
| **28 days** | [#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457) — non-cancelling session refresh | `distinguished contributor`, small behavioural fix, no visible reviewer. |
| **27 days** | [#11505](https://github.com/zeroclaw-labs/zeroclaw/pull/11505) — settings actions + keybinding filter | `needs-author-action` |
| **23 days** | [#11589](https://github.com/zeroclaw-labs/zeroclaw/pull/11589) — operator cost-limit override | Documented-but-unimplemented config; moderate user value, XL scope. |
| **9 days** | [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921) — append-only session event history | `risk:high` + `size:XL`; needs an architectural decision, not just review. |
| **7 days** | [#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004) — memory append-only | `priority:p1`, `needs-maintainer-review`; cheap fix, P1 impact. |

**Process observations for maintainers:**
1. **Merge throughput is the bottleneck.** 49 open vs 1 closed with 45% `needs-author-action` suggests a triage convention that parks PRs on authors without a clear re-entry path.
2. **Two `docs(runtime)` exception-request PRs** — [#12063](https://github.com/zeroclaw-labs/zeroclaw/pull/12063) (agent owned-state retirement, refs #9745/#9647) and [#12037](https://github.com/zeroclaw-labs/zeroclaw/pull/12037) (external memory rerank) — indicate contributors are seeking *architectural permission*, not code review. These are governance decisions that only maintainers can unblock.
3. **Single-author concentration on ZeroCode** (8/20 PRs) is a bus-factor risk; four carry `needs-author-action`, which may compound if that contributor is bandwidth-limited.
4. **Fast fixes are available now:** [#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068), [#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/12080), [#12061](https://github.com/zeroclaw-labs/zeroclaw/pull/12061) are `size:XS`/`S` — a single review pass could clear three stability items and lift merge velocity off the floor.

</details>