# OpenClaw Project Report 2026-02-24

> Data source: [openclaw/openclaw](https://github.com/openclaw/openclaw) | Issues: 500 | PRs: 500 | Generated at: 2026-02-24 04:45 UTC

# OpenClaw Project Report | 2026-02-24

---

## 1. Today at a Glance

OpenClaw showed **extremely high community activity** today, with 500 issue updates in the past 24 hours (197 new/active, 303 closed) and 500 PR updates (442 pending merge, 58 merged/closed). **No new version was released**, but the code merge cadence was intense, mainly focused on stability fixes, security hardening, and channel adaptation (Telegram/Feishu/WhatsApp). Notably, 303 issues were closed today, showing that the maintenance team is actively clearing the backlog; meanwhile, 442 pending PRs indicate strong community contribution enthusiasm, though review pressure is heavy. Overall project health is good, and the project is in a stage of **transitioning from feature refinement to stabilization**.

---

## 2. Version Releases

**No new version released** (the latest version remains 2026.2.22-2)

---

## 3. Project Progress

### Important PRs merged/closed today

| PR | Author | Core improvement | Project impact |
|:---|:---|:---|:---|
| [#25008](https://github.com/openclaw/openclaw/pull/25008) | @zerone0x | **Skip reasoning injection for OpenRouter `auto` models** | Fixes a regression introduced in 2026.2.22-2, restoring OpenRouter compatibility |
| [#25025](https://github.com/openclaw/openclaw/pull/25025) | @hclsys | **Fix browser cookies set --url option conflict** | Resolves a CLI argument parsing bug, improving the developer experience |
| [#25035](https://github.com/openclaw/openclaw/pull/25035) | @bmendonca3 | **Deny cron tool invocation on /tools/invoke by default** | Security hardening that prevents unauthorized access to the scheduler |
| [#24686](https://github.com/openclaw/openclaw/pull/24686) | @mujiannan | **Feishu topic session binding inheritance fix** | Resolves session isolation issues in Feishu topic groups, a critical fix for enterprise users |
| [#24785](https://github.com/openclaw/openclaw/pull/24785) | @chilu18 | **Improved dmPolicy configuration error messages** | Makes configuration errors easier to fix and lowers support costs |
| [#24527](https://github.com/openclaw/openclaw/pull/24527) | @easternbloc | **Fix tool results after OpenAI history truncation** | Fixes session corruption in multi-tool-call scenarios |
| [#24733](https://github.com/openclaw/openclaw/pull/24733) | @Glucksberg | **Normalize resolveAgentRoute input peer.kind** | Fixes `dm` vs `direct` matching failures, improving routing reliability |
| [#25044](https://github.com/openclaw/openclaw/pull/25044) | @bmendonca3 | **Deny nodes tool on /tools/invoke by default** | Security hardening that prevents exposure of the node management interface |

**Overall progress assessment**: Today's merged PRs center on **security hardening** (3 items), **channel stability** (Feishu/Telegram/WhatsApp), and **configuration experience improvements**, reflecting the project's shift from feature expansion toward production readiness. In particular, the OpenRouter and Feishu fixes directly address blocking issues for enterprise users.

---

## 4. Community Hotspots

### Most actively discussed issues

| Issue | Comments | 👍 | Core request | Analysis |
|:---|:---:|:---:|:---|:---|
| [#8576](https://github.com/openclaw/openclaw/issues/8576) | 30 | 7 | **@openclaw/feishu installation failure** | Feishu plugin installation problems became today's focus, reflecting growth among Chinese enterprise users; the plugin distribution infrastructure needs attention |
| [#25050](https://github.com/openclaw/openclaw/issues/25050) | 0 | 0 | **webchat sessions incorrectly tagged as whatsapp** | Newly reported configuration drift issue affecting session routing accuracy for multi-channel users |
| [#24870](https://github.com/openclaw/openclaw/issues/24870) | 3 | 3 | **Minimax 2.5 reasoning cannot be disabled** | Model provider compatibility issue; strong user demand for control |
| [#23307](https://github.com/openclaw/openclaw/issues/23307) | 5 | 0 | **${ENV_VAR} resolved to plaintext during configuration migration** | Security-sensitive issue: environment variable references leak during upgrades; PR [#10258](https://github.com/openclaw/openclaw/pull/10258) already fixes it |
| [#14596](https://github.com/openclaw/openclaw/issues/14596) | 4 | 0 | **Sub-agent write tool missing content parameter** | Sub-agent tool call stability, affecting the reliability of automated workflows |

**Hotspot trends**: Feishu ecosystem integration issues are surging (#8576, #10549, #9246), showing that the Chinese market is a growth focus; configuration security and environment variable handling have become trust-sensitive areas; sub-agent stability problems keep being reported and are a core pain point for advanced users.

---

## 5. Bugs and Stability

### Ranked by severity

| Severity | Issue | Description | Status |
|:---|:---|:---|:---|
| 🔴 **Critical** | [#6413](https://github.com/openclaw/openclaw/issues/6413) | Gateway process virtual memory leak (22GB+), reproduces after restart | Open, no fix PR |
| 🔴 **Critical** | [#16323](https://github.com/openclaw/openclaw/issues/16323) | Security audit: unsafe default tool policy, privilege escalation, Windows command injection | Open, security initiative |
| 🟠 **High** | [#25050](https://github.com/openclaw/openclaw/issues/25050) | webchat sessions incorrectly tagged as the whatsapp channel | Open, newly reported today |
| 🟠 **High** | [#23307](https://github.com/openclaw/openclaw/issues/23307) | ${ENV_VAR} resolved to plaintext values during upgrades, leaking credentials | **Fix PR [#10258](https://github.com/openclaw/openclaw/pull/10258) already exists** |
| 🟠 **High** | [#10294](https://github.com/openclaw/openclaw/issues/10294) | Ed25519 private keys stored in plaintext in browser localStorage | **Fix PR [#10296](https://github.com/openclaw/openclaw/pull/10296) already exists** |
| 🟡 **Medium** | [#24870](https://github.com/openclaw/openclaw/issues/24870) | Minimax 2.5 reasoning still displayed after being disabled | Open |
| 🟡 **Medium** | [#25042](https://github.com/openclaw/openclaw/issues/25042) | Sub-agent completion does not automatically trigger a main session response | Open |
| 🟡 **Medium** | [#24995](https://github.com/openclaw/openclaw/issues/24995) | memory_search causes Node.js heap OOM crashes | Open |

**Stability assessment**: The memory leak (#6413) is the most severe production risk but lacks reproduction details; the security issues have community-contributed fix PRs that should be reviewed first; configuration drift and channel tagging errors are newly emerging stability threats.

---

## 6. Feature Requests and Roadmap Signals

### Key feature requests from users

| Request | Issue/PR | Status | Likelihood of inclusion |
|:---|:---|:---|:---|
| **Dynamic tool discovery** (reduce context tokens) | [#6651](https://github.com/openclaw/openclaw/issues/6651) | Open, 11 comments | ⭐⭐⭐ High, a core performance optimization request |
| **Discord semantic search** | [#17875](https://github.com/openclaw/openclaw/issues/17875) | Open, 4 comments | ⭐⭐ Medium, has a clear implementation plan |
| **Linux desktop voice dictation** (hotkey → local STT → auto-paste) | [#16933](https://github.com/openclaw/openclaw/issues/16933) | Open, 2 comments | ⭐⭐ Medium, the community has provided an implementation |
| **Agent lifecycle hooks** | [#17707](https://github.com/openclaw/openclaw/issues/17707) | Open, 3 comments | ⭐⭐⭐ High, an architectural extensibility need |
| **Per-session/per-channel reasoning level overrides** | [#17781](https://github.com/openclaw/openclaw/issues/17781) | Open, 1 comment | ⭐⭐ Medium, a fine-grained control request |
| **Configurable tool-call narration mode** | [#17915](https://github.com/openclaw/openclaw/issues/17915) | Open, 1 comment | ⭐⭐ Medium, a UX improvement |

**Roadmap signals**: Performance optimization (dynamic tool discovery, context budgets) and observability (hooks, tracing) are core requests from advanced users; voice interaction and multimodal capabilities are expanding from macOS to Linux/Windows; enterprise scenarios require finer-grained policy control (per-channel configuration, security hardening).

---

## 7. User Feedback Summary

### Real pain points

> *"Every request includes all tools not needed... makes responses less accurate, especially on smaller models"* — [#6651](https://github.com/openclaw/openclaw/issues/6651)

**Context bloat** is a core pain point for local model users, directly affecting cost and accuracy.

> *"Feishu channel health check every 60 seconds exhausts API quota on free tier"* — [#10549](https://github.com/openclaw/openclaw/issues/10549)

**Quota management for enterprise IM channels** lacks fine-grained control, causing unexpected production outages.

> *"Sub-agent completion announce not delivered to main session"* — multiple related issues

**Sub-agent reliability** is a blocking issue for automated workflow users, undermining trust in task orchestration.

### Satisfaction points

- Broad multi-channel support (Telegram/WhatsApp/Discord/Feishu)
- Local model (Ollama) integration lowers usage costs
- Active security response (multiple security hardening PRs today)

### Dissatisfaction points

- Credential leak risk during configuration migration (#23307)
- Documentation inconsistent with the implementation (AGENTS.md template section name mismatch, #25029)
- Persistent path and permission issues on Windows

---

## 8. Pending Backlog

### Important issues/PRs left unanswered for a long time

| Item | Created | Last activity | Risk | Suggested action |
|:---|:---|:---|:---|:---|
| [#6413](https://github.com/openclaw/openclaw/issues/6413) Gateway memory leak | 2026-02-01 | 2026-02-24 | 🔴 Production stability | Tag as `priority:critical` and assign core developers to investigate |
| [#3092](https://github.com/openclaw/openclaw/issues/3092) Session lock timeouts causing channel handler failures | 2026-01-28 | 2026-02-24 | 🟠 Concurrency reliability | Possibly related to #6413, investigate together |
| [#3344](https://github.com/openclaw/openclaw/issues/3344) Gemini phantom tool calls | 2026-01-28 | 2026-02-24 | 🟡 Model compatibility | Multiple related PRs exist; a unified solution is needed |
| [#16323](https://github.com/openclaw/openclaw/issues/16323) Consolidated security audit issues | 2026-02-14 | 2026-02-24 | 🔴 Security compliance | Set up a security-focused milestone and fix in phases |
| [#17299](https://github.com/openclaw/openclaw/issues/17299) Agents Plane (multi-tenant) | 2026-02-15 | 2026-02-24 | 🟡 Enterprise feature | Evaluate compatibility with the existing architecture, tag as `roadmap` |

**Maintainer reminder**: Among today's 442 pending PRs, security contributions (#10258, #10296, #10174) and channel stability contributions (Feishu/Telegram related) should be reviewed first, to balance accepting community contributions with safeguarding core stability.

---

*Report generated at: 2026-02-24 | Data source: OpenClaw GitHub repository*

---
*This report was automatically generated by [agents-radar](https://github.com/duanyytop/agents-radar).*