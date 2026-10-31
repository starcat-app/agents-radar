# OpenClaw Project Report 2026-02-23

> Data source: [openclaw/openclaw](https://github.com/openclaw/openclaw) | Issues: 500 | PRs: 500 | Generated at: 2026-02-23 13:19 UTC

# OpenClaw Project Report | 2026-02-23

## 1. Today at a Glance

OpenClaw shows **extremely high activity** today, with 500 issue updates in the past 24 hours (247 new/active, 253 closed), 500 PR updates (366 pending merge, 134 merged/closed), and 1 release. The community is focused on **v2026.2.22 adaptation problems** — large numbers of users report the Chrome extension browser relay authentication change (HMAC-derived tokens), abnormal loading of channel plugins such as Telegram/WhatsApp, and configuration validation issues on Windows. Meanwhile, Mistral provider support has officially launched, and multilingual memory search expansion (Turkish, Danish, etc.) keeps advancing. Overall project health is good, but the efficiency of handling post-release regressions needs attention.

---

## 2. Releases

### v2026.2.22: openclaw 2026.2.22
**Release link**: https://github.com/openclaw/openclaw/releases/tag/v2026.2.22

| Change | Details |
|--------|------|
| **New features** | **Mistral provider support** (#23845) — including memory embeddings and voice support |
| **Core updates** | Added an optional built-in auto-updater (`update.auto.*`), disabled by default, supporting delayed and jittered checks on stable plus hourly checks on beta |
| **Breaking changes** | **Browser extension relay authentication mechanism change** — switched from the raw gateway token to HMAC-SHA256 derived tokens, breaking many users' configurations |
| **Migration notes** | Users need to reconfigure the token in the Chrome extension options page, or wait for follow-up PRs that restore backward compatibility (see #24489, #24436) |

---

## 3. Project Progress

### Important PRs merged/closed today

| PR | Author | Core contribution | Project impact |
|:---|:---|:---|:---|
| [#24479](https://github.com/openclaw/openclaw/pull/24479) | @merc1305 | **Security fix**: redact sensitive keys in dynamic configuration paths (`env.GROQ_API_KEY` etc.) | Resolves `config.get` leaking API keys, raising the security baseline |
| [#24471](https://github.com/openclaw/openclaw/pull/24471) | @gitwithuli | **Internationalization**: added Turkish stopword filtering, extending multilingual memory search support | Memory search language coverage grows to 6 (Spanish/Portuguese/Japanese/Korean/Arabic/Turkish) |
| [#24335](https://github.com/openclaw/openclaw/pull/24335) | @Kay-051 | **Fix**: prevent reasoning content from leaking to WhatsApp/Telegram when `thinking=low` | Resolves the #24290 regression, improving message privacy |
| [#24413](https://github.com/openclaw/openclaw/pull/24413) | @justinhuangcode | **Fix**: stop misidentifying the macOS menu bar app as a competing gateway service | Eliminates the #23846 false positive, improving the macOS experience |
| [#24485](https://github.com/openclaw/openclaw/pull/24485) | @chilu18 | **Fix**: replaced stale doctor/restart command hints | Resolves the misleading CLI hints in #24351 and #24220 |
| [#24431](https://github.com/openclaw/openclaw/pull/24431) | @s1korrrr | **CI fix**: install PyYAML in the skills-python job | Fixes the #24342 test failure, keeping skills system CI stable |
| [#24410](https://github.com/openclaw/openclaw/pull/24410) | @chilu18 | **CI fix**: same as above (duplicate submission, merged) | — |

**Overall progress**: Today's merged PRs concentrate on **security hardening** (key redaction), **internationalization expansion** (Turkish), **release regression fixes** (reasoning leakage, false-positive elimination), and **infrastructure stability** (CI fixes). The project is advancing steadily on multilingual support and security compliance, but the adaptation problems triggered by the v2026.2.22 authentication change still require substantial community resources to absorb.

---

## 4. Community Hotspots

### Most actively discussed Issues

| Issue | Comments | Core ask | Analysis |
|:---|:---|:---|:---|
| [#23861](https://github.com/openclaw/openclaw/issues/23861) | **10** | Raspberry Pi installation failure: `npm install` breaks the system | **Edge device deployment pain point** — a user reports 3 Pi devices broken during installation, reflecting insufficient robustness of the install scripts in ARM/embedded environments |
| [#8576](https://github.com/openclaw/openclaw/issues/8576) | **29** | Feishu plugin installation error `@openclaw/feishu` | **Hard requirement for Chinese enterprise users** — the Feishu integration problem has long gone unfixed; 29 comments show enterprise deployments blocked, with a risk of being replaced by competitors |
| [#17019](https://github.com/openclaw/openclaw/issues/17019) | **27** | `400 Item 'rs_...' of type 'reasoning' was provided without its required following item` | **Reasoning model compatibility** — a high-frequency technical error affecting reasoning features of Claude and other models; users report repeated recurrences |
| [#7309](https://github.com/openclaw/openclaw/issues/7309) | **5** | Support DeepSeek API as a first-class LLM provider | **Domestic model demand** — 12 👍; users want native DeepSeek support instead of manual configuration, reflecting Chinese market demand |
| [#13248](https://github.com/openclaw/openclaw/issues/13248) | **7** | Full MCP (Model Context Protocol) support | **Ecosystem expansion demand** — 12 👍; users note the codebase already has MCP infrastructure but lacks user-level configuration, and want standardized tool calls unlocked |

**Underlying asks**: The community's core tension lies in **"feature breadth vs. stability depth"** — users want quick access to new models (DeepSeek, Gemini 3.1) and protocols (MCP), yet remain stuck with regressions in basic functionality (installation, authentication, channel plugins). The integration experience of enterprise users (Feishu, DingTalk) directly affects adoption decisions.

---

## 5. Bugs and Stability

### Sorted by severity

| Severity | Issue | Description | Status | Fix PR |
|:---|:---|:---|:---|:---|
| **P0 - Blocking** | [#24395](https://github.com/openclaw/openclaw/issues/24395) | **All channel plugins disabled in v2026.2.22** — config writes `channels.<id>.enabled` but the loader reads `plugins.entries.<id>.enabled` | 🔴 Open | [#24428](https://github.com/openclaw/openclaw/pull/24428), [#24231](https://github.com/openclaw/openclaw/pull/24231) |
| **P0 - Blocking** | [#24358](https://github.com/openclaw/openclaw/issues/24358) | **Chrome extension relay authentication broken** — the HMAC token change causes "Gateway token rejected" | 🔴 Open | [#24489](https://github.com/openclaw/openclaw/pull/24489), [#24436](https://github.com/openclaw/openclaw/pull/24436), [#24437](https://github.com/openclaw/openclaw/pull/24437) |
| **P1 - High** | [#24499](https://github.com/openclaw/openclaw/issues/24499) | OpenAI adapter sends `ROLE_UNSPECIFIED`, causing Moonshot/Kimi API 400 errors | 🟡 Open | None |
| **P1 - High** | [#24496](https://github.com/openclaw/openclaw/issues/24496) | Windows 11 ByteString error — character value 1047 > 255 | 🟡 Open | None |
| **P1 - High** | [#24263](https://github.com/openclaw/openclaw/issues/24263) | WhatsApp channel config corrupted on Windows — `Unrecognized key: "enabled"` | 🟡 Open | [#24300](https://github.com/openclaw/openclaw/pull/24300) |
| **P2 - Medium** | [#24494](https://github.com/openclaw/openclaw/issues/24494) | macOS browser control service not listening on port base+2 | 🟡 Open | None |
| **P2 - Medium** | [#24414](https://github.com/openclaw/openclaw/issues/24414) | Desktop app "Check for updates" shows an old version as the new one | 🟡 Open | None |
| **P2 - Medium** | [#24374](https://github.com/openclaw/openclaw/issues/24374) | MS Teams channel `startAccount` resolves immediately, causing a restart loop | 🟡 Open | [#24391](https://github.com/openclaw/openclaw/pull/24391) |

**Stability assessment**: The v2026.2.22 release triggered **2 P0 blocking issues** (channel plugins disabled, extension authentication broken), directly impacting the core user experience. 5+ targeted fix PRs already exist, but the merge pace needs to accelerate. Regression test coverage is insufficient for the Windows platform and third-party API adaptation (Moonshot).

---

## 6. Feature Requests and Roadmap Signals

| Feature request | Heat | Technical feasibility | Signal for next version |
|:---|:---|:---|:---|
| **Native DeepSeek support** (#7309) | 12 👍 | High (OpenAI compatible) | 🔶 Possible — strong community demand; needs official provider registration |
| **Full MCP support** (#13248) | 12 👍 | Medium (infrastructure exists) | 🔶 Possible — the codebase already has `mcporter`; needs a user configuration layer |
| **Task-level smart model routing** (#19166) | 5 comments | Medium | 🔶 Possible — aligned with the existing `model-router` plugin direction |
| **reasoningDefault config key** (#24491, #24161) | 2 duplicates | High | 🟢 High probability — a simple configuration extension, PR ready |
| **GitHub native channel** (#24386) | 0 👍 | Medium | 🔶 Possible — enterprise scenario; needs webhook + API in both directions |
| **Mobile-adapted Web UI** (#22590) | 3 comments | Medium | 🔶 Possible — a demand specific to Chinese users |
| **Agent-level tool permission limits** (#24372) | 0 👍 | Medium | 🔶 Possible — security enhancement, essential for multi-agent scenarios |
| **Session archiving/persistence** (#24066) | 2 comments | Medium | 🔶 Possible — related to the existing compaction/memory system |

**Roadmap signals**: The next version (v2026.2.23 or v2026.3.x) may focus on:
1. **Configuration experience improvements** (`reasoningDefault`, configuration validation)
2. **China ecosystem adaptation** (DeepSeek, mobile Web UI, Feishu stability)
3. **Enterprise security** (tool permissions, session isolation)

---

## 7. User Feedback Summary

### Real pain points

| Scenario | Feedback source | Core complaint |
|:---|:---|:---|
| **Configuration broken after version upgrades** | #24395, #24358, #24414 | "Every update breaks existing settings" — eroding trust |
| **Poor cross-platform consistency** | #24263 (Windows), #24494 (macOS) | "Always more problems on Windows" — doubts about platform fairness |
| **Misleading error messages** | #24220, #24351 | Suggested commands do not exist; debugging time wasted |
| **Fragile enterprise integrations** | #8576 (Feishu), #24374 (MS Teams) | Unstable enterprise IM integrations affecting production deployments |
| **Security vs. convenience trade-off** | #24384 (API key leak) | Status messages leaking sensitive information; security awareness awakening |

### Satisfaction points
- **Active multilingual expansion** (quick turnaround on Turkish and Danish PRs)
- **Auto-updater shipped** (a long-requested feature)
- **Timely Mistral support** (fast follow-up on new models)

---

## 8. Pending Backlog

### Important long-unanswered Issues

| Issue | Created | Last updated | Risk | Suggested action |
|:---|:---|:---|:---|:---|
| [#3460](https://github.com/openclaw/openclaw/issues/3460) Internationalization (i18n) and localization support | 2026-01-28 | Today | 66 comments, 0 👍, officials say "no bandwidth to support" | Set up a community translation program, with officials providing the technical framework |
| [#5380](https://github.com/openclaw/openclaw/pull/5380) Keep recent messages when compaction fails | 2026-01-31 | Today | Experience issue, risk of user data loss | Evaluate for merge, or fold into the compaction refactor |
| [#7175](https://github.com/openclaw/openclaw/issues/7175) pre-compaction hook | 2026-02-02 | Today | Data protection need | Design jointly with #13032 (`session:before_end` hook) |
| [#7598](https://github.com/openclaw/openclaw/issues/7598) Session history backup layer | 2026-02-03 | Today | Core reliability | Raise the priority; linked to #24066 session archiving |
| [#8255](https://github.com/openclaw/openclaw/issues/8255) Workspace file post-write hooks | 2026-02-03 | Today | Workflow automation | Evaluate integration with the skills system |

**Maintainer reminder**: Among the backlog, **#3460 internationalization** and **#7598 session backup** are architecture-level needs; it is recommended to respond to them explicitly in next quarter's roadmap, to avoid losing community contributors over a lack of direction.

---

*Report generated at: 2026-02-23 | Data source: OpenClaw GitHub repository*

---
*This report was automatically generated by [agents-radar](https://github.com/duanyytop/agents-radar).*