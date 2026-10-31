# OpenClaw Ecosystem Digest 2026-10-31

> Issues: 86 | PRs: 500 | Projects covered: 5 | Generated: 2026-10-31 00:15 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [IronClaw](https://github.com/nearai/ironclaw)
- [QwenPaw](https://github.com/agentscope-ai/QwenPaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-10-31

## 1. Today's Overview

OpenClaw remains a high-velocity project: **86 issues** and **500 PRs** were updated in the last 24 hours, with **264 PRs merged/closed** against **236 still open**. One beta release shipped, narrowly focused on restoring Node compatibility for installs and updates. The issue queue is dominated by **P0/P1 reliability reports** around Windows service lifecycle, macOS authentication, session-state ownership, and transcript redaction. Throughput is healthy, but the concentration of release-blocker bugs and the large open PR backlog suggest **maintainer review bandwidth, not contributor supply**, is the main constraint. Overall health is active and productive, with stability risk concentrated in platform-specific update/auth paths and shared-state coordination.

## 2. Releases

### v2026.10.10-beta.5

**Highlights**
- Node compatibility restored: installs and updates work again on Node `>=24.16.0 <25 || >=26.1.0`.
- Node **24.22.1 or 26.12.1** is now a **security recommendation** rather than a hard requirement.
- Node 26 workers no longer abort when stdin is a file.
- References: [#186589](https://github.com/openclaw/openclaw/pull/186589), [#187516](https://github.com/openclaw/openclaw/pull/187516).

**Breaking changes:** None documented.

**Migration notes:** No mandatory action. Operators on Node 24/26 should upgrade to the recommended patch versions for security hardening; older supported Node ranges are no longer blocked at install/update time.

## 3. Project Progress

With **264 PRs merged/closed**, visible progress in the sample includes:

**Merged/closed PRs**
- [#188719](https://github.com/openclaw/openclaw/pull/188719) — aligned bundled plugin `fs-safe` pins with the root package, fixing ref-sourced package builds that failed before any lane ran.
- [#188810](https://github.com/openclaw/openclaw/pull/188810) — stabilized composer model/effort pickers during mobile layout transitions.
- [#188735](https://github.com/openclaw/openclaw/pull/188735) — exposed plugin source-preparation work in startup diagnostics.
- [#188852](https://github.com/openclaw/openclaw/pull/188852) — repaired release proxy lifecycle module exports.
- [#188853](https://github.com/openclaw/openclaw/pull/188853) — sped up large-buffer test assertions.
- [#127309](https://github.com/openclaw/openclaw/pull/127309) — WhatsApp group gating now honors `implicitMentions`.

**Closed issues indicating fixes or resolution**
- [#167270](https://github.com/openclaw/openclaw/issues/167270) — Feishu cross-session send attaching internal reply anchor / 400 on first send.
- [#178291](https://github.com/openclaw/openclaw/issues/178291) — 2026.10.4→10.5 update failing post-activation Doctor.
- [#187248](https://github.com/openclaw/openclaw/issues/187248) — dead “Refresh” button on reply-failure banner.
- [#186565](https://github.com/openclaw/openclaw/issues/186565) — `read` failing above ~512 MB with V8 string-limit error.
- [#176027](https://github.com/openclaw/openclaw/issues/176027) — sub-second `timeoutSeconds` treated as no timeout.
- [#183699](https://github.com/openclaw/openclaw/issues/183699) — broker workers >2 stalling writers.
- [#156666](https://github.com/openclaw/openclaw/issues/156666) — orphaned dreaming cron job after third-party slot owner disables dreaming.
- [#153498](https://github.com/openclaw/openclaw/issues/153498) — delivery-queue media-spool cleanup failures.
- [#90587](https://github.com/openclaw/openclaw/issues/90587) — RISC-V64 Codex app-server exit.
- [#163824](https://github.com/openclaw/openclaw/issues/163824) — applied Workshop skill invisible under skills allowlist.
- [#185191](https://github.com/openclaw/openclaw/issues/185191) — workspace file-mode opt-out request.
- [#188112](https://github.com/openclaw/openclaw/issues/188112) — Goal Resume button rejecting local Codex.

**In-flight notable PRs**
- [#188397](https://github.com/openclaw/openclaw/pull/188397) — open cold session history without restoring archives (schema 39), XL performance change.
- [#188832](https://github.com/openclaw/openclaw/pull/188832) — keep unchanged sandbox workspaces warm between turns.
- [#188835](https://github.com/openclaw/openclaw/pull/188835) — reuse prepared context during Gateway restart verification.
- [#188850](https://github.com/openclaw/openclaw/pull/188850) — preview automation impact before changing default models.
- [#188865](https://github.com/openclaw/openclaw/pull/188865) — update `fs-safe` to 0.27.0 and remove directory-mode workarounds.
- [#188870](https://github.com/openclaw/openclaw/pull/188870) — restore cold TTS summary selection and plugin preparation.

## 4. Community Hot Topics

PR comment counts are not exposed in this dataset; the issue ranking below is by comment count. Reactions remain low overall, indicating discussion-driven rather than reaction-driven engagement.

| Item | Signal | Underlying need |
|---|---|---|
| [#170956](https://github.com/openclaw/openclaw/issues/170956) Windows slow startup, unclean plugin shutdown, `schtasks` permission error | 27 comments, P0, crash-loop, UX release blocker | Reliable Windows managed-service lifecycle: restarts and updates must not require repeated retries or cause client disconnects. |
| [#150635](https://github.com/openclaw/openclaw/issues/150635) Short-term recall retention evicts recalled entries nightly, dreaming deep phase never promotes | 23 comments, P2, session-state | Memory/dreaming pipeline correctness at the 512-entry cap; users expect learned recall to survive and promote. |
| [#177656](https://github.com/openclaw/openclaw/issues/177656) Native host exec returns shared-state integrity-admission error | 21 comments, P1, ≥28 failures on stable 2026.10.5 | Shared-state admission must be robust across child processes; failures currently leave child effects unproved. |
| [#159094](https://github.com/openclaw/openclaw/issues/159094) Gateway owns state-lifecycle lease but workers report another process owns it | 16 comments, P1, message-loss/session-state | Multi-process state ownership must be coherent; contention currently closes execution admission. |
| [#142821](https://github.com/openclaw/openclaw/issues/142821) Default transcript redaction poisons replayed context | 9 comments, 1 👍, P0, data-loss/security | Security defaults must not corrupt commands, files, or replies when masked content is replayed. |
| [#172969](https://github.com/openclaw/openclaw/issues/172969) `registerCliBackend` without `modelProvider` silently dropped, surfaces as “Invalid URL” | 8 comments, P2 | Better diagnostics for plugin/runtime misconfiguration instead of misleading downstream errors. |
| [#141413](https://github.com/openclaw/openclaw/issues/141413) macOS app omits token for local Gateway using `SecretRef` | 8 comments, 2 👍, P0, security review | Correct credential resolution for protected secrets; the embedded dashboard and app disagree on auth. |
| [#188761](https://github.com/openclaw/openclaw/issues/188761) Preflight automation compatibility when changing default agent model | 6 comments, P2 | Prevent silent automation breakage when model defaults change; users want impact preview before applying. |

**Analysis:** The hottest discussions cluster around **platform reliability** (Windows services, macOS auth), **state ownership** (leases, shared-state admission), and **memory correctness** (dreaming/recall). These are not feature debates; they are trust-and-reliability issues affecting production operators.

## 5. Bugs & Stability

### Critical — P0

| Issue | State | Summary | Fix PR? |
|---|---|---|---|
| [#170956](https://github.com/openclaw/openclaw/issues/170956) | OPEN, 27 comments | Windows slow startup, unclean plugin shutdown, `schtasks` permission error; restarts/updates unreliable, occasional 1006 disconnects | No new fix PR; needs maintainer review |
| [#142821](https://github.com/openclaw/openclaw/issues/142821) | OPEN, 9 comments | Default-on model-visible transcript redaction poisons replayed agent context; masks propagate into commands/files/replies | No new fix PR; needs product + security review |
| [#169844](https://github.com/openclaw/openclaw/issues/169844) | OPEN, 6 comments | Control UI update on Windows hangs at “Activating”; Scheduled Task left disabled and gateway stopped | No new fix PR |
| [#141413](https://github.com/openclaw/openclaw/issues/141413) | OPEN, 8 comments, 2 👍 | macOS app omits token for local Gateway using `SecretRef`; embedded dashboard can authenticate while app cannot | No new fix PR; security review |
| [#163628](https://github.com/openclaw/openclaw/issues/163628) | OPEN, 2 comments | macOS app local connection always presents shared token, never falls back to password when `auth.mode=password` | No linked fix PR in sample |
| [#178291](https://github.com/openclaw/openclaw/issues/178291) | CLOSED | 2026.10.4→10.5 update failed post-activation Doctor on offline-maintenance authority | Closed — verify in release notes |

### High — P1

| Issue | State | Summary | Fix PR? |
|---|---|---|---|
| [#177656](https://github.com/openclaw/openclaw/issues/177656) | OPEN, 21 comments | Native host exec returns shared-state integrity-admission error without child result | No new fix PR |
| [#159094](https://github.com/openclaw/openclaw/issues/159094) | OPEN, 16 comments | Gateway owns state-lifecycle lease but internal workers report another process owns it | No new fix PR |
| [#162941](https://github.com/openclaw/openclaw/issues/162941) | OPEN, 4 comments | Plugin LLM completions from `agent_end` fail with “agent tool caller authority is no longer active” | No new fix PR; security review |
| [#188647](https://github.com/openclaw/openclaw/issues/188647) | OPEN, 2 comments | Model fallback can select backup but finish silently before dispatching provider request | No linked fix PR |
| [#167270](https://github.com/openclaw/openclaw/issues/167270) | CLOSED | Feishu cross-session send attaches internal reply anchor; first send fails with 400 | Closed |

### New / notable today

- [#188867](https://github.com/openclaw/openclaw/issues/188867) — Telegram isolated polling against a local Bot API re-fetches the same completed update in a tight loop, pegging CPU at 120–170%. Filed 2026-10-31; intake needs repro.
- [#188829](https://github.com/openclaw/openclaw/issues/188829) — update failure “validating” on 2026.10.9 (darwin/arm64, Node 26.13.0); needs info.
- [#188694](https://github.com/openclaw/openclaw/issues/188694) — update failure “invalid-config” on 2026.10.9; needs info.
- [#188858](https://github.com/openclaw/openclaw/issues/188858) — Automations editor hides a rearmed one-shot’s effective next run. Fix PR: [#188864](https://github.com/openclaw/openclaw/pull/188864).
- [#188845](https://github.com/openclaw/openclaw/issues/188845) — `doctor --fix` re-enables a plugin with a mixed-case ID after `plugins disable`.
- [#188737](https://github.com/openclaw/openclaw/issues/188737) — Scheduled pinned-only `show_widget` unavailable when target session uses an OpenAI model.

### P2 stability bugs with active fixes

- [#150401](https://github.com/openclaw/openclaw/issues/150401) — provider errors without HTTP status are not failover-eligible, so configured fallbacks are never attempted. Tagged queueable fix.
- [#147637](https://github.com/openclaw/openclaw/issues/147637) — `openclaw memory index --force` fails with “unable to open database file” on a fresh writable agent DB.
- [#180858](https://github.com/openclaw/openclaw/issues/180858) — Codex GPT-Live WebRTC startup discards actionable provider error.
- [#188760](https://github.com/openclaw/openclaw/pull/188760) — Doctor provider checks prepared asynchronously; related to blocking plugin callbacks.
- [#179893](https://github.com/openclaw/openclaw/pull/179893) — Codex saved user turn reported as failed write when prompt annotation is refused.
- [#179891](https://github.com/openclaw/openclaw/pull/179891) — exec text using `$<digit>` in double quotes corrupts dollar amounts.

**Assessment:** The P0 set is small but heavily concentrated in **Windows update/service reliability** and **macOS credential handling** — both directly affect operators’ ability to install, restart, and authenticate. Several P0s have no linked fix PR, which is the main stability risk for the 2026.10.10 stable line.

## 6. Feature Requests & Roadmap Signals

**Active user-requested features**
- [#188761](https://github.com/openclaw/openclaw/issues/188761) — preflight automation compatibility check before changing default agent model. PR [#188850](https://github.com/openclaw/openclaw/pull/188850) already implements impact preview.
- [#150238](https://github.com/openclaw/openclaw/issues/150238) — supported context budget / skip policy for Skill Workshop Experience Review on oversized sessions.
- [#150250](https://github.com/openclaw/openclaw/issues/150250) — verify Skill Workshop learning coverage and behavioral reuse.
- [#169401](https://github.com/openclaw/openclaw/issues/169401) — let owned automations keep explicit failure alerts without owner-conversation repair.
- [#166156](https://github.com/openclaw/openclaw/issues/166156) — opt-out for extra spoken confirmation in Talk (`talk.voiceConfirmation: "off"`).
- [#150029](https://github.com/openclaw/openclaw/issues/150029) — make automation “Inspect” link configurable (`always | errors | never`).
- [#148480](https://github.com/openclaw/openclaw/issues/148480) — reuse restricted Codex completion context to avoid repeated cold history bootstraps.
- [#168624](https://github.com/openclaw/openclaw/issues/168624) — safety-first Android Auto support for explicit-turn assistant messaging.
- [#187774](https://github.com/openclaw/openclaw/issues/187774) — optional Cua Spaces worker provider.
- [#184709](https://github.com/openclaw/openclaw/issues/184709) — ElevenLabs batch transcription keyterm prompting.
- [#183537](https://github.com/openclaw/openclaw/issues/183537) — consider ShieldCortex and multi-clawd for official plugin catalog / verified publisher listing.
- [#184523](https://github.com/openclaw/openclaw/issues/184523) — diagnose embedding entitlement separately from working Codex OAuth inference.

**Prediction for next version (2026.10.10 stable or subsequent beta)**
1. **Automation model-change preflight** — [#188761](https://github.com/openclaw/openclaw/issues/188761) + [#188850](https://github.com/openclaw/openclaw/pull/188850) is already implementation-ready.
2. **One-shot automation effective next-run display** — [#188858](https://github.com/openclaw/openclaw/issues/188858) + [#188864](https://github.com/openclaw/openclaw/pull/188864).
3. **Update robustness** — shallow-clone hang ([#188857](https://github.com/openclaw/openclaw/pull/188857)), build-lock recovery ([#188859](https://github.com/openclaw/openclaw/pull/188859)), leftover runtime/snapshot reclamation ([#188868](https://github.com/openclaw/openclaw/pull/188868)).
4. **Plugin/Doctor diagnostics and security hardening** — async Doctor provider checks ([#188760](https://github.com/openclaw/openclaw/pull/188760)), plugin archive review ceiling ([#188866](https://github.com/openclaw/openclaw/pull/188866)), memory-lancedb certificate-chain rejection ([#188801](https://github.com/openclaw/openclaw/pull/188801)).
5. **Performance** — cold session history without archive restore ([#188397](https://github.com/openclaw/openclaw/pull/188397)) and warm sandbox reuse ([#188832](https://github.com/openclaw/openclaw/pull/188832)) are larger XL changes likely landing in a minor/beta after stability fixes.

Lower likelihood near-term: Android Auto, Cua Spaces, ElevenLabs keyterms, and plugin catalog changes — all still need product/security decisions.

## 7. User Feedback Summary

**Main pain points**
- **Windows operators face repeated update/restart failures.** Slow startup, `schtasks` permission errors, hangs at “Activating,” and disabled Scheduled Tasks ([#170956](https://github.com/openclaw/openclaw/issues/170956), [#169844](https://github.com/openclaw/openclaw/issues/169844)) are the strongest dissatisfaction signal in the dataset.
- **macOS authentication is inconsistent.** The app fails to present a `SecretRef` token ([#141413](https://github.com/openclaw/openclaw/issues/141413)) or always uses the shared token instead of password fallback ([#163628](https://github.com/openclaw/openclaw/issues/163628)).
- **Session-state and memory behavior erodes trust.** State-lifecycle lease contention ([#159094](https://github.com/openclaw/openclaw/issues/159094)), dreaming/recall eviction ([#150635](https://github.com/openclaw/openclaw/issues/150635)), and memory-index failures ([#147637](https://github.com/openclaw/openclaw/issues/147637)) affect long-running agents.
- **Security defaults can cause data loss.** Transcript redaction poisoning replayed context ([#142821](https://github.com/openclaw/openclaw/issues/142821)) is a P0 tension between security and usability.
- **Silent failures and UX friction.** Examples: `registerCliBackend` silently dropping providers ([#172969](https://github.com/openclaw/openclaw/issues/172969)), dead reply-failure Refresh button ([#187248](https://github.com/openclaw/openclaw/issues/187248)), and automations editor hiding effective next run ([#188858](https://github.com/openclaw/openclaw/issues/188858)).
- **Update failure reports on 2026.10.9** ([#188829](https://github.com/openclaw/openclaw/issues/188829), [#188694](https://github.com/openclaw/openclaw/issues/188694)) suggest config/validation edge cases remain; both need reproduction details.

**Satisfaction signals**
- Users are actively filing detailed, reproducible reports with environment and version data.
- Maintainers are closing meaningful bugs and landing fixes quickly — 264 PRs merged/closed in 24h.
- Reaction counts are low, but comment depth on P0/P1 issues shows sustained operator investment.

**Dissatisfaction signal:** Repeated release-blocker bugs in update/auth paths create a “can’t reliably upgrade or reconnect” perception, which is more damaging than isolated feature gaps.

## 8. Backlog Watch

Important items needing maintainer attention, especially older high-severity issues and security-sensitive PRs.

| Item | Age / State | Why it matters |
|---|---|---|
| [#141413](https://github.com/openclaw/openclaw/issues/141413) macOS app omits token for local Gateway using `SecretRef` | Created 2026-09-07, P0, 8 comments, 2 👍, security review needed | Oldest open P0 in the sample; no fix PR. Auth correctness on macOS remains unresolved. |
| [#150635](https://github.com/openclaw/openclaw/issues/150635) Short-term recall retention evicts recalled entries nightly | Created 2026-09-17, P2, 23 comments, product decision | High-discussion memory correctness issue; dreaming promotion never happens at cap. |
| [#159094](https://github.com/openclaw/openclaw/issues/159094) State-lifecycle lease ownership mismatch | Created 2026-09-26, P1, 16 comments | Multi-process state contention can cause message loss; still open. |
| [#143375](https://github.com/openclaw/openclaw/issues/143375) PDF tool gated on vision model before opening document | Created 2026-09-09, P2, 5 comments | Scanned PDFs unreachable without a vision model; extraction signal runs too late. |
| [#147637](https://github.com/openclaw/openclaw/issues/147637) `memory index --force` fails on fresh writable DB | Created 2026-09-14, P2, 5 comments | Blocks memory reindexing; `memory status` works, indicating a path-specific bug. |
| [#151173](https://github.com/openclaw/openclaw/issues/151173) Memory-core recall rehydration anchors on fragments | Created 2026-09-17, P2, 5 comments | Ambiguous range selection by line distance can misattribute recalled content. |
| [#148480](https://github.com/openclaw/openclaw/issues/148480) Reuse restricted Codex completion context | Created 2026-09-14, P2, 5 comments | Repeated cold history bootstraps waste latency/context on Codex handoffs. |
| [#150238](https://github.com/openclaw/openclaw/issues/150238) Context budget/skip policy for Skill Workshop | Created 2026-09-16, P2, 6 comments | Oversized sessions can overrun model context during Experience Review. |
| [#150250](https://github.com/openclaw/openclaw/issues/150250) Skill Workshop learning coverage verification | Created 2026-09-16, P3, 5 comments | Needed to prove workshop revisions actually improve later tasks. |
| [#169401](https://github.com/openclaw/openclaw/issues/169401) Automation failure alert opt-out | Created 2026-10-11, P2, 5 comments | Owner-conversation repair replaces explicit failure alerts; needs product decision. |
| [#179965](https://github.com/openclaw/openclaw/pull/179965) `ask_user` from another agent’s turn reaches that agent instead of owner | Open since 2026-10-21, XL, security-sensitive | Routing/privacy boundary issue; needs maintainer review. |
| [#179959](https://github.com/openclaw/openclaw/pull/179959) Allow write access without personal credential enrollment | Open since 2026-10-21, XL, security-boundary | Shared Gateway operators need managed credential policy; high review risk. |
| [#179893](https://github.com/openclaw/openclaw/pull/179893) Codex saved user turn reported as failed write | Open since 2026-10-21, P2 | False persistence errors and skipped notifications; fix is small but waiting. |
| [#179891](https://github.com/openclaw/openclaw/pull/179891) Exec dollar amounts corrupted by `$<digit>` | Open since 2026-10-21, P2 | Data corruption in agent-sent messages; fix refuses corrupted output but needs proof. |
| [#178033](https://github.com/openclaw/openclaw/pull/178033) Heartbeat status for cadence and activeHours | Open since 2026-10-20, P3 | Operator visibility gap; waiting on maintainer review. |

**Bottom line:** OpenClaw’s contributor throughput is strong, but its **review and product-decision queue** is the bottleneck for P0/P1 reliability work. The highest-leverage maintainer actions this week are: land or assign fixes for Windows update/service lifecycle ([#170956](https://github.com/openclaw/openclaw/issues/170956), [#169844](https://github.com/openclaw/openclaw/issues/169844)), resolve macOS auth ([#141413](https://github.com/openclaw/openclaw/issues/141413), [#163628](https://github.com/openclaw/openclaw/issues/163628)), and decide the security/usability trade-off in transcript redaction ([#142821](https://github.com/openclaw/openclaw/issues/142821)).

---

## Cross-Ecosystem Comparison

## Cross-Project Comparison Report — 2026-10-31

*Scope: OpenClaw, Hermes Agent, IronClaw, QwenPaw, ZeroClaw. Counts are 24-hour digest snapshots unless noted. Health scores are directional 0–10 composites of merge throughput, backlog balance, release cadence, and severity risk; they are not security certifications.*

---

### 1. Ecosystem Overview

The personal AI assistant / agent open-source landscape on 2026-10-31 is characterized by high contribution volume and tighter review bandwidth rather than broad feature launches. OpenClaw remains the reference-scale project, while Hermes Agent, QwenPaw, and ZeroClaw show active mid-stage iteration; IronClaw is in a maintenance-only window. The dominant work is reliability hardening: session/state ownership, platform-specific update and authentication paths, channel adapter semantics, security defaults, and cost/cache control. Silent degradation and lost work are recurring user complaints, especially where subsystems report success while failing to act. No project except OpenClaw shipped a release in the window, so much visible work is queued for future beta/stable cuts.

---

### 2. Activity Comparison

| Project | Issues count | PR count | Merged/closed PRs | Open PRs | Release status | Health score |
|---|---:|---:|---:|---:|---|---:|
| **OpenClaw** | 86 updated | 500 updated | 264 | 236 | **v2026.10.10-beta.5 shipped** | **7.5/10** |
| **Hermes Agent** | 15 updated (4 new, 2 closed) | 50 updated | 8 | 42 | No new release | **7.0/10** |
| **IronClaw** | 0 updated | 1 updated | 0 | 1 | No release | **5.0/10 neutral** |
| **QwenPaw** | 8 updated | 32 updated | 11 | 21 | No new; latest **v2.3.0-beta.1** (10/27) | **7.5/10** |
| **ZeroClaw** | 6 active/open | 50 updated | 0 | 50 | No releases | **5.5/10** |

**Reading the table:** OpenClaw is the only project with substantial merge throughput and a release in the window. QwenPaw has the healthiest merge-to-open ratio among the mid-stage projects. Hermes has responsive triage but a 42:8 open-to-closed PR ratio. ZeroClaw has strong contributor supply but zero merges in 24h. IronClaw has no user-facing activity signal.

---

### 3. OpenClaw’s Position

**Advantages vs peers**
- **Largest activity footprint by an order of magnitude:** 86 issue updates and 500 PR updates vs 15/50 for Hermes, 8/32 for QwenPaw, 6/50 for ZeroClaw, and 0/1 for IronClaw.
- **Only project shipping a release in the window:** `v2026.10.10-beta.5`, focused on Node compatibility and install/update reliability.
- **Highest delivery throughput:** 264 merged/closed PRs vs 11 for QwenPaw, 8 for Hermes, and 0 for ZeroClaw.
- **Broadest operational surface:** Windows service lifecycle, macOS auth, transcript redaction, plugin source preparation, sandbox warm reuse, cold session history, and multi-channel integrations.

**Technical approach differences**
- OpenClaw is a **core gateway/runtime + plugin ecosystem** with explicit state-lifecycle ownership, sandbox/workspace management, transcript redaction, and release-channel discipline.
- Peers are more narrowly focused: Hermes on desktop/dashboard + Kanban/cron workflows; QwenPaw on desktop packaging, channels, and governance; ZeroClaw on Rust-based security/autonomy and context economics.

**Community size comparison**
- By 24h activity proxy, OpenClaw’s issue queue is ~5.7× Hermes, ~10.8× QwenPaw, and ~14.3× ZeroClaw. Its PR update volume is ~10× Hermes/QwenPaw/ZeroClaw.
- The main weakness is not contributor supply but **review and product-decision bandwidth**: P0 Windows update/service issues and macOS auth issues remain open without linked fix PRs, and 236 PRs remain open.

---

### 4. Shared Technical Focus Areas

| Emerging requirement | Projects with evidence | Specific need |
|---|---|---|
| **Session/state durability** | OpenClaw #159094, #177656; Hermes #145022; ZeroClaw #11457, #11727; QwenPaw #8511 | Coherent multi-process state ownership, lease fencing, resumable work, and recovery from gateway stalls without losing in-progress tasks. |
| **Silent-failure observability** | QwenPaw #8488, #8500, #8505; OpenClaw #172969, #188647, #188858; Hermes #147025, #147020; ZeroClaw #11589, #11624 | Visible degradation warnings, structured error classification, non-zero exit semantics, and preflight diagnostics instead of “success” while doing nothing. |
| **Platform parity and packaging** | OpenClaw #170956, #169844, #141413, #163628; QwenPaw #8488, #8502; ZeroClaw #12133, #12134; Hermes #142741, #144616, #146657 | Windows/macOS/WSL CI coverage, frozen-build asset validation, native service lifecycle, env allowlists, and CJK path handling. |
| **Security defaults and governance** | OpenClaw #142821, #141413, #179965, #179959; QwenPaw #8513; ZeroClaw #12134, #12131; Hermes #147019 | Safe-by-default policy without corrupting context or blocking legitimate flows; approval gates, allow-lists, secret resolution, and auditability. |
| **Cost/cache/context economics** | ZeroClaw #11703, #11698, #12044; OpenClaw #188397, #188832; Hermes #127647; QwenPaw #8496 | Stable prompt prefixes, warm sandbox reuse, context budgets, cache-aware tool activation, and operator cost controls. |
| **Channel/adapter semantics** | Hermes #30989, #139875, #140202; OpenClaw #188867, #167270, #127309; QwenPaw #8511; ZeroClaw #10926 | Per-channel debounce/merge/retry, destination addressing correctness, and conformance tests so message handling is consistent across platforms. |
| **Review/merge bandwidth** | OpenClaw 236 open vs 264 merged; Hermes 42 vs 8; QwenPaw 21 vs 11; ZeroClaw 50 vs 0 | Maintainer review rotation, named owners, smaller PRs, and CI gates—contributor supply is outpacing landing capacity in several projects. |

---

### 5. Differentiation Analysis

| Project | Feature focus | Target users | Technical architecture signal |
|---|---|---|---|
| **OpenClaw** | Core assistant gateway, multi-channel integrations, plugins, sandbox/workspace lifecycle, transcript security, Windows/macOS operability | Production operators, plugin developers, power users | Gateway/runtime + plugin source preparation + sandbox + state lifecycle; mature beta release process |
| **Hermes Agent** | Desktop/dashboard, Kanban worker orchestration, cron agents, SSH/mobile terminal, session search, plugin catalog | Multi-worker orchestrators, desktop and remote-terminal users | Gateway/session ownership, SQLite cron ledger, Git tooling, desktop renderer, channel adapters |
| **IronClaw** | Minimal signal in this window; WebUI dependency maintenance only | Not assessable from data | Rust crates + WebUI frontend; Dependabot update for `happy-dom` |
| **QwenPaw** | Desktop/PyInstaller builds, channel reliability, provider compatibility, `tool_guard`/governance, plugin system, local inference direction | Desktop users, zh-CN/CJK users, self-hosted/proxy inference operators, plugin ecosystem | Desktop packaging, plugin system, approval levels, channel adapters, local Piccolo model work |
| **ZeroClaw** | Security/autonomy, ZeroCode UX, Matrix/XMPP channels, cost/context economics, agent-to-agent session messaging | Security-conscious autonomous-agent operators, Rust ecosystem | Rust config/policy, channels/providers, subprocess watchdog, staged Goal V1 epic |

---

### 6. Community Momentum & Maturity

| Tier | Projects | Evidence | Momentum read |
|---|---|---|---|
| **High-throughput + release cadence** | **OpenClaw** | 264 merged/closed, 236 open, beta release shipped | Rapid iteration and reliability hardening; review bandwidth is the constraint |
| **Active stabilization** | **QwenPaw, Hermes Agent** | QwenPaw: 11 merged / 21 open post-beta; Hermes: 8 merged / 42 open, salvage PRs | QwenPaw is converging on beta infrastructure; Hermes is consolidating but review-constrained |
| **Contributor-heavy, merge-constrained** | **ZeroClaw** | 50 open PRs, 0 merged; same-day fix PRs for new S1/S2 bugs | Strong contributor supply, weak landing throughput; fatigue risk |
| **Maintenance-only / no user-facing signal** | **IronClaw** | 1 Dependabot PR, 0 issue updates | No momentum signal from this window |

**Maturity assessment:** OpenClaw is the most mature in release and operational process, but carries concentrated P0 platform risk. Hermes and QwenPaw have functioning external-contributor pipelines and active triage. ZeroClaw has the clearest contributor-supply/landing-capacity imbalance. IronClaw cannot be assessed for maturity from this data slice.

---

### 7. Trend Signals

1. **Reliability is the product.** Platform-specific update/auth failures and session-state contention dominate operator complaints. Developers should invest in cross-platform service lifecycle, auth fallback, and state-ownership fencing before adding features.
2. **Silent failure is more damaging than loud failure.** QwenPaw’s Visual Compact no-op and Auto-Dream memory loss, OpenClaw’s silent provider drop and model fallback, and ZeroClaw’s dead `cost.allow_override` all report success while failing. Observable degradation, structured errors, and non-zero exits are becoming baseline requirements.
3. **Security defaults need policy, not blanket blocking.** OpenClaw’s transcript redaction poisons replayed context; QwenPaw’s shell-wrapped outbound actions bypass approval; ZeroClaw’s forbidden-path defaults miss WSL/Windows volumes. The trend is toward allow-lists, approval workflows, audit trails, and secret resolution that preserve usability.
4. **Cost/cache/context economics matter.** Prompt-cache invalidation, idle resource burn, cold-history bootstraps, and context budgets are now first-class user complaints. Stable prompt prefixes, warm sandbox reuse, and cache-aware tool activation are high-value engineering directions.
5. **Channel adapters need conformance semantics.** BlueBubbles split events, Telegram polling loops, Matrix peer-vs-room addressing, and Feishu mid-processing errors point to the same need: per-channel debounce/merge/retry and explicit destination semantics, backed by tests.
6. **Provider-agnostic inference is a first-class deployment mode.** OpenAI-compatible relays, local Whisper endpoints, and self-hosted gateways require robust status-code extraction, fallback classification, and compatibility shims rather than assuming OpenAI’s exact error shape.
7. **Desktop/frozen-build parity is an emerging weak spot.** PyInstaller asset omission, Windows env allowlists, CJK paths, launchd/Nix versioning, and Windows arm64 test gaps all signal that CI matrices and packaging checks are becoming differentiators.
8. **Review bandwidth is the ecosystem bottleneck.** OpenClaw, Hermes, QwenPaw, and ZeroClaw all show contributor volume at or above maintainer landing capacity. For developers, this favors smaller, fix-linked, well-tested PRs; for maintainers, it favors named reviewers and explicit accept/defer decisions on large PRs.

---

## Peer Project Reports

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — Project Digest
**Date:** 2026-10-31 · **Repo:** [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. Today's Overview

Activity is high but skewed toward intake rather than closure: 65 combined issue/PR updates in the last 24 hours, of which 50 were PRs — yet only 8 PRs were merged or closed against 42 still open. Four new issues arrived on 2026-10-30/31, and two issues closed, including a same-window fix for a browser-extension permission bug. There were **no new releases**, so all of this work is queued for a future tag. The work itself is heavily concentrated in reliability engineering — gateway/session state, cron ledger contention, Git index locking, and supply-chain dependency bumps — with two P1-class items active (#145022 open bug, #145615 open fix PR). Overall health reads as **active and responsive, but review-constrained**: maintainers are visibly in consolidation mode (two "salvage" PRs from `teknium1`), while a tail of May-2026 bug reports and September PRs remains unresolved.

---

## 2. Releases

No new releases in this window. No migration or breaking-change notes to report.

---

## 3. Project Progress

**Closed/merged in the last 24h (8 total; 6 visible in the top-20 PR sample):**

| Item | Area | What landed |
|---|---|---|
| [PR #118111](https://github.com/NousResearch/hermes-agent/pull/118111) | Git / agent tooling | Disabled optional Git locks in bounded internal probes to stop stray `.git/index.lock` files. Superseded and extended by [PR #147031](https://github.com/NousResearch/hermes-agent/pull/147031) (opened today by `teknium1`), which removes lock acquisition from all background `git status` reads — session-start probes, dashboard coding rail, Review pane, subagent worktree checks. |
| [PR #143888](https://github.com/NousResearch/hermes-agent/pull/143888) | Dashboard / mobile | Android IME edits now handled at `beforeinput`, fixing taps that never reached the PTY (#137986). |
| [PR #143102](https://github.com/NousResearch/hermes-agent/pull/143102) | Dashboard / mobile | Overscroll containment for the mobile drawer menu (iOS Safari scroll-chaining). |
| [PR #138954](https://github.com/NousResearch/hermes-agent/pull/138954) | Gateway / storage | Idle scratch directories are now re-swept on the housekeeping tick, fixing retention on hosts whose only long-lived process is the gateway. |
| [PR #127163](https://github.com/NousResearch/hermes-agent/pull/127163) | Desktop / SSH | SSH tunnel flap budget switched from retry-count to time-window; keepalive half already upstreamed. |
| [PR #117126](https://github.com/NousResearch/hermes-agent/pull/117126) | Tools / sessions | `session_search` now reports matched-set coverage instead of the truncated returned slice. |
| [Issue #147013](https://github.com/NousResearch/hermes-agent/issues/147013) | Gateway / browser ext. | Closed — `source=hermes_browser` sessions were rejected by three admission gates. |
| [Issue #142962](https://github.com/NousResearch/hermes-agent/issues/142962) | Plugin catalog | Closed — `limbic` catalog entry bumped to 0.9.0. |

**New fix work opened today:** [PR #147030](https://github.com/NousResearch/hermes-agent/pull/147030) serializes `cron/executions.py` ledger writes so SQLite contention waits rather than killing workers (fixes #135487; deployment measured 12 concurrent writers and 50 jobs sharing minute 0). Security/maintenance: [PR #147028](https://github.com/NousResearch/hermes-agent/pull/147028) (undici, zod, fast-uri advisories) and [PR #147029](https://github.com/NousResearch/hermes-agent/pull/147029) (body-parser 1.20.9, GHSA-27r3-jxmh-p828).

---

## 4. Community Hot Topics

Comment counts for PRs were not populated in this dataset; issue engagement below is complete.

1. **[Issue #127647](https://github.com/NousResearch/hermes-agent/issues/127647) — 34 comments** · *Tracker: Desktop idle resource burn* (P2, comp/desktop). By far the most-discussed item, open since 2026-09-29 with an indexed triage plan, a PR cross-reference index, and a causal analysis of "which changes introduced each mechanism." **Underlying need:** an always-on assistant must be cheap when idle — laptop battery, fan noise, and background CPU/GPU are now first-class product concerns, not edge cases. The tracker format signals the maintainers expect a multi-PR campaign rather than a single fix.
2. **[Issue #145022](https://github.com/NousResearch/hermes-agent/issues/145022) — 12 comments** · *Kanban workers crash with "Kanban execution unknown; retained by owner"* (P1, comp/gateway, area/sessions). One gateway stall killed 4 workers simultaneously and discarded in-progress work. **Need:** durable, resumable session ownership under gateway backpressure — the retry recovers the card but not the work.
3. **[Issue #30989](https://github.com/NousResearch/hermes-agent/issues/30989) — 6 comments** · *BlueBubbles text+attachment arrives as two events and interrupts the turn* (P2). **Need:** adapter parity — Telegram has debounce/merge, BlueBubbles does not, so iMessage users get spurious `⚡ Interrupting current turn` events.
4. **[Issue #142741](https://github.com/NousResearch/hermes-agent/issues/142741) — 6 comments** · *launchd bootstrap retry never kickstarts a registered-but-not-running job* (P2, os/macos). **Need:** reliable service supervision; `launchctl list` showing a PID is treated as proof of liveness when it isn't.
5. **[Issue #131433](https://github.com/NousResearch/hermes-agent/issues/131433) — 5 comments, 1 👍** · *Closed cron run goes read-only after first reply* (P2). A regression from #124945's write-restriction logic. **Need:** clear, documented session-write semantics that survive refactors.

**Pattern:** three of the top five are session-state or adapter-delivery issues, and several carry `sweeper:risk-session-state` / `risk-message-delivery` labels — an automated risk-tagging system is flagging the same subsystem repeatedly.

---

## 5. Bugs & Stability

Ranked by severity and blast radius:

| Severity | Item | Impact | Fix PR? |
|---|---|---|---|
| **P1** | [#145022](https://github.com/NousResearch/hermes-agent/issues/145022) Kanban worker crash on gateway stall | Work-in-progress loss, multi-worker fleet failure | None visible |
| **P1** | [PR #145615](https://github.com/NousResearch/hermes-agent/pull/145615) (open) — owner-forward rejects `session.resume` answers >1 MiB | TUI gateway resume failure; socket-level test added | This *is* the fix (for #145215) |
| **P2** | [#147026](https://github.com/NousResearch/hermes-agent/issues/147026) (new) — reasoning replay double-stuffs `reasoning` + `reasoning_content` on bare-`custom` routes | Every multi-turn chat 400s from turn 2 on strict hosts (SenseNova) | None |
| **P2** | [#145182](https://github.com/NousResearch/hermes-agent/issues/145182) — `auxiliary.vision` fallback carries aux model name to auto-detected provider | Vision requests 400 (`<local model> is not a valid model ID`) | None |
| **P2** | [#30989](https://github.com/NousResearch/hermes-agent/issues/30989) BlueBubbles split-event interrupt | Mid-turn interruption, duplicated context | None (open ~5 months) |
| **P2** | [#142741](https://github.com/NousResearch/hermes-agent/issues/142741) launchd restart failure on macOS | Gateway cannot be restarted via CLI | None |
| **P2** | [#131433](https://github.com/NousResearch/hermes-agent/issues/131433) cron run read-only after first reply | Feature regression in desktop Cron | None |
| **P2** | [#144616](https://github.com/NousResearch/hermes-agent/issues/144616) Nix builds report `0.0.0` | Home Assistant plugin never loads (requires ≥0.21.5); misleading update warning | None |
| **P2** | [#147020](https://github.com/NousResearch/hermes-agent/issues/147020) (new) — lifecycle guard treats dotted `server.kill()` as shell `kill` | False-positive command blocking in serialized source; operational risk | None |
| **P2** | [#147025](https://github.com/NousResearch/hermes-agent/issues/147025) (new) — `platform_toolsets.<platform>: []` still loads all MCP servers | Config semantics silently inverted; `no_mcp` undocumented | None |
| **P2** | [#30323](https://github.com/NousResearch/hermes-agent/issues/30323) leftover `/steer` applied after queued follow-up | Guidance delivered late or appears dropped | None |
| **P2** | [#26451](https://github.com/NousResearch/hermes-agent/issues/26451) skill discovery recurses hidden workspace dirs | Vendored/generated skills surfaced as installed | None |

**Stability note:** [PR #146657](https://github.com/NousResearch/hermes-agent/pull/146657) (open) reports 30 Windows arm64 test fixes, **six of which were real product bugs** — a sign that non-POSIX CI coverage is thin. A same-day closure on #147013 shows fast turnaround when the root cause is localized.

---

## 6. Feature Requests & Roadmap Signals

Only one explicit feature request in this window:

- **[Issue #147019](https://github.com/NousResearch/hermes-agent/issues/147019) — Override for hardline checks** (new, 0 comments). Users running automated test/setup flows need reboots and currently "sneak a reboot command into a shell script" to bypass the guard. **Prediction:** plausible for the next minor release as a scoped config gate, but because it touches a safety boundary (`hardline`), expect maintainers to demand an allow-list/confirmation design rather than a blanket toggle — likely slower than typical config fixes.

**Likely contents of the next version**, based on what is actually near-ready:
- Security/dependency patch set: [#147028](https://github.com/NousResearch/hermes-agent/pull/147028), [#147029](https://github.com/NousResearch/hermes-agent/pull/147029).
- Git lock fix [#147031](https://github.com/NousResearch/hermes-agent/pull/147031) and cron ledger serialization [#147030](https://github.com/NousResearch/hermes-agent/pull/147030) — both small, targeted, and tagged `ci-reviewed`/linked to issues.
- Plugin catalog hygiene [#147027](https://github.com/NousResearch/hermes-agent/pull/147027), plus the just-closed limbic 0.9.0 entry.
- Desktop/dashboard polish (#146642 inline-code currency escaping, #146657 Windows test matrix).

**Unlikely next version:** the idle-resource-burn campaign (#127647) spans multiple mechanisms and will land incrementally; large session-prune PR [#108582](https://github.com/NousResearch/hermes-agent/pull/108582) (open since 2026-09-11) has already been split once (#125807) and looks at risk of slipping again.

---

## 7. User Feedback Summary

**Pain points, in order of recurrence:**
1. **Cost of idleness** — desktop renderer CPU/GPU, backend serve CPU, and memory growth (#127647) dominate discussion volume; users treat this as a daily-use blocker.
2. **Lost work on failure** — Kanban worker crashes (#145022) and cron read-only regression (#131433) both destroy or block in-progress state. Users emphasize retries recover the *card*, not the *work*.
3. **Platform adapter inconsistency** — BlueBubbles (#30989), Telegram forum topics (#139875), WeCom/WeChat rate-limit push loss (#140202) are all the same complaint in different wrappers: message semantics differ per platform and failures are silent.
4. **Install/update friction** — Nix `0.0.0` version (#144616), stale PEP 660 editable-install maps after `hermes update` (#134458), and misleading migration prompts.
5. **Configuration surprises** — an empty list meaning "all MCP servers" (#147025) and provider/model mismatch on fallback (#145182) both violate user mental models rather than failing loudly.

**Use cases visible in reports:** multi-worker Kanban orchestration, cron-driven scheduled agents, desktop + remote SSH sessions, macOS launchd service deployment, mobile web terminal use, and a real plugin ecosystem (limbic memory, hermes-finance, Home Assistant).

**Satisfaction signals:** unusually high report quality — commit SHAs, source-inspection reproductions on `origin/main`, socket-level tests, and inline diffs from users who cannot open PRs (e.g., #142962, #145615's credited upstream branch). Same-window closure of #147013 shows responsiveness. **Dissatisfaction signals:** a five-month-old adapter bug, repeated `sweeper:risk-session-state` tagging, and 42 open PRs against 8 closed — contributors are producing faster than reviews complete.

---

## 8. Backlog Watch

Items needing maintainer attention, ordered by staleness × importance:

| Item | Age | Why it matters |
|---|---|---|
| [#30989](https://github.com/NousResearch/hermes-agent/issues/30989) BlueBubbles split events | Open since **2026-05-23** (~5 months), 6 comments | Every iMessage text+attachment turn is interrupted; Telegram already solved this — likely a port, not a design problem. |
| [#30323](https://github.com/NousResearch/hermes-agent/issues/30323) leftover `/steer` ordering | Since **2026-05-22**, 3 comments | CLI guidance silently dropped; affects trust in steering. |
| [#26451](https://github.com/NousResearch/hermes-agent/issues/26451) hidden dirs in skill discovery | Since **2026-05-15**, 2 comments | Cheap fix, correctness issue for anyone with editor-generated directories. |
| [PR #108582](https://github.com/NousResearch/hermes-agent/pull/108582) exact-selection session prune | Since **2026-09-11** | Large feature, already split once; needs a decision (merge, re-scope, or close) rather than continued drift. |
| [PR #134458](https://github.com/NousResearch/hermes-agent/pull/134458) / [PR #134460](https://github.com/NousResearch/hermes-agent/pull/134460) | Since **2026-10-07** | Update-flow and CLI regex fixes tagged `risk-compatibility`; both small and unblocked. |
| [#127647](https://github.com/NousResearch/hermes-agent/issues/127647) idle-burn tracker | Since **2026-09-29**, 34 comments | Highest-engagement item in the repo and still a tracker — assign an owner and a milestone so the 34-comment analysis converts into shipped PRs. |

**Bottom line:** the project is healthy on contribution and triage velocity but has a measurable **review-and-merge bottleneck** (42:8 open-to-closed PR ratio) and a persistent session-state/adapter bug cluster. Clearing the five-month-old adapter issues and the September PR queue would do more for perceived reliability than any new feature work this cycle.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-10-31

## Today's Overview
IronClaw showed very low activity on 2026-10-31: 0 issue updates, 1 open PR update, and 0 new releases or merged/closed PRs. The only activity was Dependabot PR [#8164](https://github.com/nearai/ironclaw/pull/8164), a dev-dependency bump for `happy-dom` in the WebUI frontend. No user-facing bugs, feature requests, or community discussions were recorded in the supplied data. Overall, this was a maintenance-only window with no evidence of regressions or release momentum.

## Project Progress
- No PRs were merged or closed today.
- No features advanced and no fixes were shipped.
- [#8164](https://github.com/nearai/ironclaw/pull/8164) remains open and appears to be awaiting review/CI validation.

## Community Hot Topics
- No Issues were updated, so there were no active issue discussions.
- The only PR in the window is [#8164](https://github.com/nearai/ironclaw/pull/8164): `chore(deps-dev): bump happy-dom from 20.11.1 to 21.0.4` in `/crates/product/ironclaw_webui/frontend`.
- Comment count was not supplied in the dataset; reactions were 0. This is an automated dependency-maintenance item, not a community discussion.
- Underlying need: keep frontend test/tooling dependencies current and compatible.

## Bugs & Stability
- No bugs, crashes, or regressions were reported today.
- No bug-fix PRs exist in the supplied data.
- Potential low-to-moderate review risk: [#8164](https://github.com/nearai/ironclaw/pull/8164) bumps `happy-dom` across a major version boundary (20 → 21), so maintainers should verify upstream release notes and CI results for frontend test compatibility.

## Feature Requests & Roadmap Signals
- No feature requests or roadmap signals were present in the last 24 hours.
- No next-version feature prediction can be derived from this data window.

## User Feedback Summary
- No real user feedback was recorded today.
- User pain points, use cases, and satisfaction/dissatisfaction cannot be assessed from the supplied data.
- The only activity is automated dependency maintenance, not user-facing product feedback.

## Backlog Watch
- No long-unanswered important Issues or PRs appear in the supplied data.
- The sole open item is [#8164](https://github.com/nearai/ironclaw/pull/8164), created and updated on 2026-10-30. It is not yet long-unanswered, but it is the only maintainer action item in this window and should receive normal dependency-review attention.

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/QwenPaw">agentscope-ai/QwenPaw</a></summary>

# QwenPaw Project Digest — 2026-10-31

*Data window: activity updated 2026-10-30 → 2026-10-31 · Source: github.com/agentscope-ai/QwenPaw*

---

## 1. Today's Overview

QwenPaw is in a post-beta stabilization push: four days after the **v2.3.0-beta.1** cut (2026-10-27), the tracker saw **40 issue/PR updates in 24h** (8 issues, 32 PRs) with **11 PRs merged or closed** against 21 still open — a healthy merge-to-open ratio for a pre-release window. The release-duty installation verification issue (#8456) was closed today, indicating beta install checks have concluded, and no new release shipped. Activity is concentrated on **desktop/PyInstaller packaging gaps, provider error classification, and channel reliability**, with same-day fix PRs filed for the two most-commented bugs (#8488 → #8514, #8505 → #8512). The main health concern is a cluster of **silent-failure defects** (Visual Compact no-op, Auto-Dream memory loss reporting `success=True`) plus one **unfixed governance/security gap** (#8513) with no remediation PR yet. Overall: **high velocity, good contributor throughput, elevated trust-risk from silent failures.**

---

## 2. Releases

**No new releases today.** Latest published version remains **v2.3.0-beta.1 (Beta, 2026-10-27)**; release-duty verification issue [#8456](https://github.com/agentscope-ai/QwenPaw/issues/8456) was closed on 2026-10-30, signaling completion of the beta installation checkpoint pass. All defects in today's digest target this beta line, so the next 2.3.0 pre-release/stable cut will carry a meaningful batch of desktop and provider fixes (see §3).

---

## 3. Project Progress

**Merged/closed today (visible in top-20 sample):**

| PR | Title | Impact |
|---|---|---|
| [#8483](https://github.com/agentscope-ai/QwenPaw/pull/8483) | fix(plugins): keep a failing import-cache refresh from taking out the plugin system | **High** — Debian 12 / CPython 3.11.9+ hosts had *all* backend plugins fail to load due to `importlib.metadata` mismatch |
| [#8508](https://github.com/agentscope-ai/QwenPaw/pull/8508) | fix(workspace): remove legacy workspace ZIP APIs | **High** — eliminates ZIP merge path that could overwrite live SQLite files and broke on Windows after #8482 |
| [#7896](https://github.com/agentscope-ai/QwenPaw/pull/7896) | fix(channels): recheck idle queues after awaiting consumer shutdown | **High** — fixes message-drop race in idle channel cleanup (first-time contributor) |
| [#6041](https://github.com/agentscope-ai/QwenPaw/pull/6041) | fix(loop): exempt read-only tools from doom loop detection | **Medium** — ends false-positive terminations on repeated memory reads (closes #5906); open since July |
| [#8507](https://github.com/agentscope-ai/QwenPaw/pull/8507) | fix(console): remove shared memory tag test fixture dependency | **Medium** — unblocks Docker frontend build (TS2307 chain) |
| [#8379](https://github.com/agentscope-ai/QwenPaw/pull/8379) | fix(tests): let full pytest collect both `test_backup` modules | **Low** — restores green `pytest` gate from CONTRIBUTING.md |

**Net effect:** the beta blockers closed today are infrastructure-level (plugin bootstrap, workspace ZIP, test collection, Docker build) rather than user-facing features — consistent with hardening before stable. Three of the six closures came from first-time/returning external contributors, a positive ecosystem signal.

---

## 4. Community Hot Topics

Reaction data is flat across the board (all items at 👍 0), so discussion volume is the only heat proxy.

1. **[#8488](https://github.com/agentscope-ai/QwenPaw/issues/8488) — Desktop build omits `visual_compression` assets (3 comments)** — Most-discussed issue of the day. Users on the Windows PyInstaller build get a `FileNotFoundError` on `atlas-gray-native.ts`, so **Visual Compact silently no-ops on every eligible model call**. Underlying need: *feature-parity guarantees between dev and frozen builds*; users tolerate a missing optimization far less than a missing optimization that pretends to run. Fix PR [#8514](https://github.com/agentscope-ai/QwenPaw/pull/8514) is already open (adds the data dir to `qwenpaw.spec`).
2. **[#8505](https://github.com/agentscope-ai/QwenPaw/issues/8505) — Gateway 502 misclassified as `unknown` (2 comments)** — Users behind OpenAI-compatible relays get **no retry and no model fallback** because the status code lives only in message text (`status_code=502, 请联系管理员处理！`). Underlying need: resilience for self-hosted/proxied inference, where relays are the norm in this user base. Fix PR [#8512](https://github.com/agentscope-ai/QwenPaw/pull/8512) open.
3. **[#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500) — Auto-Dream silently drops memory (2 comments)** — An unparseable extract receipt is still checkpointed, so a full day of memory is discarded and never retried, while the run reports `success=True`. Underlying need: **observable failure semantics** in long-running memory pipelines.
4. **[#8513](https://github.com/agentscope-ai/QwenPaw/issues/8513) — Shell-wrapped outbound actions bypass approval (1 comment)** — A security-focused user reports that SMTP send / HTTP POST / `@file-to-network` shell commands produce no findings and no approval prompt at `AUTO` or `SMART`, in both `tool_guard` and governance lanes.

---

## 5. Bugs & Stability

Ranked by severity (correctness/security → UX):

| Sev | Item | Symptom | Fix PR? |
|---|---|---|---|
| **Critical** | [#8513](https://github.com/agentscope-ai/QwenPaw/issues/8513) | Outbound-capable shell commands (email exfil, HTTP POST, file-to-network) execute with **no findings or approval** under `approval_level: AUTO`/SMART — dual detector gap | ❌ None yet |
| **High** | [#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500) | Auto-Dream checkpoints failed extracts; a day of memory is lost with `success=True` and no retry or user-visible warning | ❌ None yet |
| **High** | [#8488](https://github.com/agentscope-ai/QwenPaw/issues/8488) | Desktop/PyInstaller 2.3.0-beta.1 (Windows): Visual Compact never runs, glyph atlases unshipped, `FileNotFoundError` per model call | ✅ [#8514](https://github.com/agentscope-ai/QwenPaw/pull/8514) |
| **High** | [#8511](https://github.com/agentscope-ai/QwenPaw/issues/8511) | Feishu channel intermittently raises `ProviderError: No active model configured` when a message arrives mid-processing; **reproduces on v2.2.2, not a beta regression** | ❌ None yet |
| **Medium** | [#8505](https://github.com/agentscope-ai/QwenPaw/issues/8505) | Bare `openai.APIError` with status only in text → classified `unknown`, kills retry/fallback | ✅ [#8512](https://github.com/agentscope-ai/QwenPaw/pull/8512) |
| **Medium** | [#8502](https://github.com/agentscope-ai/QwenPaw/issues/8502) | Desktop HTML preview "open in browser": CJK workspace paths → "file not found"; files outside workspace → click does nothing (Win11, zh-CN, 2.3.0b1) | ❌ None yet |
| **Low** | [#8486](https://github.com/agentscope-ai/QwenPaw/issues/8486) | Tool-call `< >` icon clipped at container's left edge (missing horizontal padding) | ✅ Closed today |

**Pattern:** two of the three highest-impact open bugs are *silent* — the feature degrades or data disappears without surfacing an error. Windows + CJK locale is an emerging weak spot (3 of 7 items). No crashes or data corruption in the core engine were reported today.

---

## 6. Feature Requests & Roadmap Signals

- **Desktop approval notifications** — [#8504](https://github.com/agentscope-ai/QwenPaw/pull/8504) (XXXL, from #8460): system notifications for pending approvals when running in background, deliberately *without* tool-call parameters in the payload. Strong candidate for **2.3.x**; approval workflows are a recurring theme and the privacy-conscious design suggests it's close to review-ready.
- **Third-party agent plugins** — [#8426](https://github.com/agentscope-ai/QwenPaw/pull/8426) (XXXL): architectural extraction of the third-party agent into the plugin system. Larger blast radius; likely **2.4**. Pairs with [#8483](https://github.com/agentscope-ai/QwenPaw/pull/8483) plugin-loading hardening merged today.
- **Local Piccolo model with bidirectional candidate scoring** — [#8463](https://github.com/agentscope-ai/QwenPaw/pull/8463): offline replacement for native Jev decisions (tool review, ReMe compaction). Signals a **local-first inference** direction; needs model-owner review before landing.
- **Community feed + inbox** — [#7903](https://github.com/agentscope-ai/QwenPaw/pull/7903) (XXXL, `ready-for-human-review`): embedded feed, category sync, Platform PKCE account linking. Either a marquee 2.4 feature or gated behind a flag.
- **Configurable Whisper model name** — [#8052](https://github.com/agentscope-ai/QwenPaw/pull/8052): unblocks non-OpenAI Whisper endpoints (SiliconFlow, local). Small, low-risk; should ship soon.
- Smaller UX asks: extension-app "Install app" button ([#8485](https://github.com/agentscope-ai/QwenPaw/pull/8485)).

**Prediction for next 2.3.x:** #8514, #8512, #8504, #8052, #8496. **For 2.4:** #8426, #7903, #8463.

---

## 7. User Feedback Summary

**Pain points, ranked by repetition and severity:**

1. **Silent degradation erodes trust.** #8488 (Visual Compact no-ops), #8500 (memory discarded with `success=True`), and #8505 (retry silently skipped) are the same complaint in three subsystems: *the product reports success while doing nothing.* Users are explicitly reading logs to discover this — the beta needs visible warnings and non-zero exit semantics for degraded paths.
2. **Frozen desktop builds lag the dev build.** Missing PyInstaller data dirs (#8488), broken plugin installation/repair ([#8509](https://github.com/agentscope-ai/QwenPaw/pull/8509)), and CJK-path handling in HTML preview (#8502) all point at insufficient packaging/locale coverage in the Windows beta. Desktop is where dissatisfaction is concentrated.
3. **Proxy/relay inference is a first-class deployment mode.** #8505 and #8496 (slow summary models, duplicate `max_tokens`/`max_completion_tokens`) show users running OpenAI-compatible gateways that don't match OpenAI's exact error shape — compatibility shims matter more than new providers.
4. **Governance is trusted but not yet sufficient.** The #8513 reporter is auditing rather than complaining, and is finding real gaps in `tool_guard` for outbound shell actions — this is a *security-confidence* signal to take seriously pre-stable.
5. **Positive signals:** 11 PRs merged/closed in 24h, multiple first-time contributors (#7896, #6041, #8400), and users filing precise, environment-complete repros (versions, OS, locale, workspace shape) — a mature reporting culture.

---

## 8. Backlog Watch

Items needing maintainer attention (age and/or lack of response):

- **[#7903](https://github.com/agentscope-ai/QwenPaw/pull/7903) — feat(community): integrate community and inbox** · `size/XXXL` · `ready-for-human-review` since 2026-09-20 (**~6 weeks**). The single largest stalled PR; a community-feed surface touching auth, sync, and console. Needs a named reviewer or an explicit "not before 2.4" decision so the contributor isn't left hanging.
- **[#8052](https://github.com/agentscope-ai/QwenPaw/pull/8052) — configurable Whisper model name** · open since 2026-09-30 (**~1 month**) with no visible review activity. Small, useful, low-risk — an easy merge that would shorten the "unreviewed small PR" queue.
- **[#8067](https://github.com/agentscope-ai/QwenPaw/pull/8067) — CJK emphasis boundaries in rendered Markdown** · `Under Review` since 2026-10-01. Directly relevant to the zh-CN user base that is also reporting desktop locale bugs; worth pairing with the CJK-path work in #8502.
- **[#8066](https://github.com/agentscope-ai/QwenPaw/pull/8066) — drop empty media blocks before formatting** · since 2026-10-01. Prevents hard provider rejections from zero-byte tool images; complements today's provider-compatibility theme.
- **[#8513](https://github.com/agentscope-ai/QwenPaw/issues/8513) — outbound shell action detector gap** · **no fix PR and only 1 comment.** Highest-severity open issue in the tracker; needs a security owner assigned before 2.3.0 stable.
- **[#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500) — Auto-Dream memory loss** · no fix PR. At minimum needs a "Surface failure instead of checkpointing" mitigation for the stable cut.
- **Process nit:** [#8509](https://github.com/agentscope-ai/QwenPaw/pull/8509) and [#8485](https://github.com/agentscope-ai/QwenPaw/pull/8485) were submitted with the PR template unfilled (`[Describe what this PR does and why]`), and PR comment counts are unreported in this data slice — both increase triage cost on an already busy 21-open-PR queue.

---

**Health verdict:** Strong throughput and a functioning external-contributor pipeline; the beta is converging on infrastructure stability rather than scope. The two things to watch before 2.3.0 stable are (a) **silent-failure semantics** across Visual Compact, Auto-Dream, and provider retries, and (b) **the unassigned `tool_guard`/governance gap in #8513** — the only item today with both critical severity and zero movement.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-10-31

## 1. Today's Overview

ZeroClaw closed the 2026-10-30 → 10-31 window with **zero integration throughput**: 50 pull requests were updated in the last 24 hours but **none were merged or closed**, and all 6 active issues remain open with no closures. Activity is therefore high in volume but entirely upstream of the merge button — review, rebase, and CI churn rather than delivery. The day's genuinely new work is a pair of Windows/WSL security-and-environment defects (#12133, #12134) filed on 2026-10-30, each with a matching fix PR (#12135, #12136) already open — an encouraging fast-turnaround signal. Meanwhile a large ZeroCode UX and runtime-stability queue from a single distinguished contributor continues to age, with items opened on 2026-10-02 still unmerged. **Health read:** strong contributor supply and disciplined triage labeling, but a visible landing bottleneck that converts into contributor fatigue if unaddressed.

## 2. Releases

No releases exist in the dataset (0 new releases; no "Latest Releases" entries at all). This appears to be a pre-release / continuous-development phase, so there is no changelog, breaking-change, or migration surface to report.

## 3. Project Progress

**Merged/closed today: 0 PRs, 0 issues.** No feature or fix was formally delivered in this window, so "progress" is measurable only as in-review advancement:

- **ZeroCode UX batch (Audacity88)** — a large, coherent set of UI/session work staged but unmerged: F5 focused-session refresh without cancel-first recovery (#11457), transcript file-path linking (#11633), mid-turn steering (#11621), config delete/reset confirmation (#11510), multi-select alias-reference editors (#11502), file-write diff previews (#11463), session reopen on restart (#11727).
- **Runtime/context economics** — #11698 (pin personality files per session to stop prompt-cache busts), #12044 (deferred bootstrap sections), #11589 (operator override for exceeded cost limits), #11456 (opt-in subprocess memory watchdog).
- **Channels & providers** — #11847 (native Rust XMPP with optional legacy OMEMO), #11871 (MiniMax M3.1-Flash catalog refresh).
- **Security hardening** — #12136 (widen default forbidden paths to `/mnt`, `/media`, `/run/media`, Windows drives/UNC) and #12135 (forward `APPDATA`/`LOCALAPPDATA`), both filed the same day as their issues.
- **Explicitly not progress:** #11882 ("Goal V1 proposal 5/12") self-describes as a draft slice that is "not independently enableable or merge-ready," with failed local validation and Core approval still open — part of a 12-PR dependent epic.

**Assessment:** the pipeline is full and thematically organized, but a 50:0 open-to-merged ratio on a single day is a review-capacity signal, not a velocity signal.

## 4. Community Hot Topics

| Item | Type | Comments | Signal |
|---|---|---|---|
| [#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926) Matrix `send_via` treats peer identities as room destinations | Bug (S2) | 6 | Highest-comment issue; discussion-heavy because it touches identity/destination semantics |
| [#11703](https://github.com/zeroclaw-labs/zeroclaw/issues/11703) Deferred `tool_search` activation busts the prompt cache | Bug (S3) | 3 | Cost/economics debate; only active on `mcp.deferred_loading = true` |
| [#11119](https://github.com/zeroclaw-labs/zeroclaw/issues/11119) Receiver-discretionary session messaging tracker | Tracker (risk:high) | 0 | Big architectural surface, no public discussion yet |
| [#12134](https://github.com/zeroclaw-labs/zeroclaw/issues/12134) Default `forbidden_paths` gaps | Bug (S1) | 0 | Fresh, security-critical, already has a fix PR |
| [#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457) ZeroCode focused-session refresh | PR (size:XL) | n/a | Most prominent in the ZeroCode queue |
| [#11882](https://github.com/zeroclaw-labs/zeroclaw/pull/11882) Goal V1 supervision slice | PR (draft) | n/a | Largest architectural PR in flight |

**Note on ranking:** the feed lists PRs "by comment count" but returns `Comments: undefined` for all 20 shown, so PR comment/reaction ranking is not verifiable from this data; the figures above reflect the 20 most recently updated PRs. All Issues show 👍: 0.

**Underlying needs:**
1. **Semantic correctness at channel boundaries** — #10926 is really about ambiguous addressing (peer vs. room) in a multi-channel abstraction; the 6-comment thread suggests the group is still negotiating the right model rather than patching a typo.
2. **Token/cost determinism** — #11703 and #11698 both stem from the same root concern: any mutable content in the system prompt silently invalidates provider caches. Users are optimizing real money, not just latency.
3. **Security defaults that assume a single-OS, single-filesystem world** — #12134 exposes a Linux/Windows/WSL assumption gap in the only denylist consulted under full autonomy.

## 5. Bugs & Stability

No crashes, panic reports, or explicit regressions were filed today. Ranked by severity:

| Severity | Issue | Impact | Fix PR exists? |
|---|---|---|---|
| **S1 — workflow blocked** | [#12134](https://github.com/zeroclaw-labs/zeroclaw/issues/12134) `default_forbidden_paths()` misses `/mnt` (WSL drive mounts), system drive root, `C:\Users`, other drives, UNC paths | Under `workspace_only = false`, file tools can reach host-mounted and non-system volumes that equivalent Linux/Windows homes would refuse — a sandbox escape by configuration default | ✅ [#12136](https://github.com/zeroclaw-labs/zeroclaw/pull/12136) (size:S) |
| **S2 — degraded** | [#12133](https://github.com/zeroclaw-labs/zeroclaw/issues/12133) Three Windows env allowlists disagree; shell/skill/hardware children omit `APPDATA`, `LOCALAPPDATA` | `gh`, `npm` and similar CLIs behave as logged-out/misconfigured inside agent child processes | ✅ [#12135](https://github.com/zeroclaw-labs/zeroclaw/pull/12135) (size:XS) |
| **S2 — degraded** | [#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926) `SendViaTool::resolve_target` uses the first `external_peers` entry as recipient | Matrix messages can be routed to a peer identity where a room was intended — potential misdelivery | ❌ none in this dataset |
| **S3 — minor (cost)** | [#11703](https://github.com/zeroclaw-labs/zeroclaw/issues/11703) Activating a deferred tool rewrites the system prompt and busts the prompt cache | Recurring token cost on every activation when deferred MCP loading is on | ⚠️ adjacent fix only ([#11698](https://github.com/zeroclaw-labs/zeroclaw/pull/11698) pins personality files, a different cache-busting source) |

**Stability work in flight (not yet landed):** [#11624](https://github.com/zeroclaw-labs/zeroclaw/pull/11624) (answer dropped elicitations instead of letting `ask_user` silently time out at 600 s), [#11815](https://github.com/zeroclaw-labs/zeroclaw/pull/11815) (dismissed choice reported as an answer, not a tool failure), [#11911](https://github.com/zeroclaw-labs/zeroclaw/pull/11911) (preserve completed tool results across interrupted channel turns), [#11456](https://github.com/zeroclaw-labs/zeroclaw/pull/11456) (subprocess memory watchdog).

**Stability read:** the two S1/S2 items filed yesterday are the only ones with same-day fixes, which is healthy. #10926 has been open since 2026-09-17 (44 days) with no linked fix and is the most concerning unresolved correctness bug.

## 6. Feature Requests & Roadmap Signals

**Explicit requests / RFCs**
- [#11119](https://github.com/zeroclaw-labs/zeroclaw/issues/11119) — implementation tracker for **receiver-discretionary agent-to-agent session messaging** (RFC #11027): runtime-owned messaging between enrolled same-alias sessions. Labeled `risk:high`, `topic:identity-access`, `topic:agent-loop`. This is the project's clearest multi-session architecture bet.
- [#12131](https://github.com/zeroclaw-labs/zeroclaw/issues/12131) — **RFC: shared execution permissions and same-identity credential renewal**, motivated by tasks that accept input from multiple authenticated contributors and spawn children outliving the initiating connection. Meets the "new security layer" RFC trigger.

**Feature-bearing PRs signaling near-term scope**
- **Goal V1 epic** — #11882 is slice 5 of 12, with explicit dependent-slice sequencing. Expect a multi-week landing arc, not a point release.
- **Context budget** — #12044 (addressable/deferred bootstrap sections) + #11698 (stable personality block) form a coherent "cheaper resident context" theme.
- **Channel breadth** — #11847 (native Rust XMPP + optional legacy OMEMO), #11871 (MiniMax model catalog refresh).
- **Operator control** — #11589 (`cost.allow_override` actually implemented rather than documented-but-dead), #11456 (memory caps for shell subprocesses).

**Prediction (data-grounded):**
1. **Highest probability next to land:** #12135 and #12136 — small (`XS`/`S`), fix-linked to S2/S1 bugs, single-author end-to-end, no architectural debate.
2. **Likely bundle:** the ZeroCode UX set (#11457, #11621, #11633, #11510, #11502, #11727) is thematically one review; expect grouped merges, but `risk:high`/`size:XL` members (#11463) will lag.
3. **Least likely soon:** #11882 (draft, dependent, failed local validation) and #11847 (XL, `risk:high`, cross-cutting channels/secrets/CI).
4. **Watch item:** #11119 has 0 comments despite `risk:high` — a tracker that large usually needs maintainer design sign-off before slices appear.

## 7. User Feedback Summary

**Pain points, by theme**

| Theme | Evidence | User impact |
|---|---|---|
| **Security defaults are OS-naive** | #12134 (S1) | Full-autonomy users on WSL or Windows are exposed by *default*, not by misconfiguration. Strong dissatisfaction signal in the framing ("cover neither… nor…"). |
| **Windows is a second-class runtime** | #12133, #12135 | Three divergent env allowlists mean agent-run CLIs (`gh`, `npm`) look logged out. A parity/consistency complaint, not a request for new features. |
| **Cost opacity from context churn** | #11703, #11698, #12044, #11589 | Users are paying for prompt-cache invalidation they cannot see or prevent; `cost.allow_override` was documented but wired to nothing — a trust hit. |
| **ZeroCode session state is fragile** | #11457, #11727, #11624, #11815 | Lost open sessions on restart, cancel-first refresh destroying drafts/queues, dropped prompts silently burning a 600 s timeout. |
| **Multi-channel addressing ambiguity** | #10926 | Users cannot predict whether a target resolves to a peer or a room. |

**Satisfaction signals:** same-day issue→fix pairs (#12133/#12135, #12134/#12136) from the same reporter show contributors who trust the process enough to write the patch themselves; detailed reproduction templates (file/line references such as `crates/zeroclaw-config/src/policy.rs:479-517`, commit `1c1cd118ac`) indicate a technically invested user base; the `distinguished contributor` label is actively used.

**Dissatisfaction risk:** the dominant frustration vector is not bug count but **review latency**. Several PRs carry `needs-author-action` and `needs-maintainer-review` simultaneously, and the oldest are 29 days old with zero merges. For a project with 50 concurrently open PRs, a 0-merge day reads to contributors as "work goes in, nothing comes out."

## 8. Backlog Watch

| Item | Age (as of 2026-10-31) | Why it needs attention |
|---|---|---|
| [#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926) Matrix peer/room confusion | 44 days, 6 comments | Oldest active bug, S2 correctness (misdelivery risk), no linked fix PR in dataset — discussion without convergence |
| [#11119](https://github.com/zeroclaw-labs/zeroclaw/issues/11119) Session messaging tracker | 36 days, 0 comments | `risk:high` architecture tracker with no visible maintainer engagement; downstream slices may be blocked on an unratified contract |
| [#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457) ZeroCode session refresh | 29 days, size:XL | Longest-lived prominent UX PR; staleness invites conflicts against the rest of the ZeroCode batch |
| [#11463](https://github.com/zeroclaw-labs/zeroclaw/pull/11463) File-write diff previews | 29 days, `risk:high`, `needs-maintainer-review` | Security-adjacent (renders file contents) and explicitly awaiting maintainer review |
| [#11456](https://github.com/zeroclaw-labs/zeroclaw/pull/11456) Subprocess memory watchdog | 29 days, `size:XL`, `needs-maintainer-review` | Resource-safety feature; blocking on review, not author |
| [#11882](https://github.com/zeroclaw-labs/zeroclaw/pull/11882) Goal V1 slice 5/12 | 12 days, draft | Author states failed local validation + Core approval outstanding; needs a sequencing decision for the epic |
| [#11871](https://github.com/zeroclaw-labs/zeroclaw/pull/11871) MiniMax catalog refresh | 12 days, `stale-candidate` | Trivial `size:M` provider fix at risk of rotting; cheapest possible merge to demonstrate throughput |
| [#11703](https://github.com/zeroclaw-labs/zeroclaw/issues/11703) Prompt-cache busting | 18 days, 3 comments | Cost bug with only an adjacent fix; needs a decision on whether #11698 closes it or a separate prompt-stability fix is required |

**Maintainer-attention priority:** (1) merge the two fix-linked S1/S2 PRs (#12136, #12135) to prove the queue moves; (2) assign an owner to #10926 before it reaches 60 days; (3) give #11119 an explicit accept/defer decision so the Goal V1 and session-messaging tracks are not built on an unratified contract.

---

**Data notes:** "Updated in last 24h" reflects modification, not creation — several items listed were opened weeks earlier. All issues in scope are open (0 closed), all 50 PRs are open (0 merged/closed), and PR comment counts were returned as `undefined`, so PR engagement ranking is inferred from recency and scope rather than verified comment volume. All reaction counts are 0. Only 20 of the 50 updated PRs were included in the feed.

</details>