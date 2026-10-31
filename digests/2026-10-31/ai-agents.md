# OpenClaw 生态日报 2026-10-31

> Issues: 86 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-10-31 00:15 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [IronClaw](https://github.com/nearai/ironclaw)
- [QwenPaw](https://github.com/agentscope-ai/QwenPaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目摘要 — 2026-10-31

## 1. 今日概览

OpenClaw 仍是一个高速推进的项目：过去 24 小时内更新了 **86 个 issue** 和 **500 个 PR**，其中 **264 个 PR 已合并/关闭**，**236 个仍处于打开状态**。发布了一个 beta 版本，重点很窄，仅用于恢复安装和更新时的 Node 兼容性。Issue 队列主要由 **P0/P1 可靠性报告**占据，涉及 Windows 服务生命周期、macOS 身份认证、会话状态归属以及转录脱敏。吞吐量健康，但发布阻断类 bug 集中出现，且开放 PR 积压量大，说明主要瓶颈是 **维护者的评审带宽，而非贡献者供给**。整体健康度活跃且富有产出，稳定性风险集中在平台特定的更新/认证路径和共享状态协调上。

## 2. 发布

### v2026.10.10-beta.5

**亮点**
- Node 兼容性已恢复：在 Node `>=24.16.0 <25 || >=26.1.0` 上，安装和更新再次可用。
- Node **24.22.1 或 26.12.1** 现在是**安全建议**，而非硬性要求。
- 当 stdin 为文件时，Node 26 worker 不再中止。
- 参考：[#186589](https://github.com/openclaw/openclaw/pull/186589)、[#187516](https://github.com/openclaw/openclaw/pull/187516)。

**破坏性变更：** 未记录任何破坏性变更。

**迁移说明：** 无强制操作。使用 Node 24/26 的运维人员应升级到推荐补丁版本以进行安全加固；较旧的受支持 Node 范围不再在安装/更新时被阻止。

## 3. 项目进展

在 **264 个 PR 已合并/关闭**的情况下，样本中可见的进展包括：

**已合并/关闭的 PR**
- [#188719](https://github.com/openclaw/openclaw/pull/188719) — 将捆绑插件 `fs-safe` 的版本固定与根包对齐，修复了在任何 lane 运行前就失败的 ref 来源包构建。
- [#188810](https://github.com/openclaw/openclaw/pull/188810) — 稳定了移动端布局切换期间 composer 的模型/effort 选择器。
- [#188735](https://github.com/openclaw/openclaw/pull/188735) — 在启动诊断中暴露插件源准备工作。
- [#188852](https://github.com/openclaw/openclaw/pull/188852) — 修复了发布代理生命周期模块导出。
- [#188853](https://github.com/openclaw/openclaw/pull/188853) — 加快了大缓冲区测试断言。
- [#127309](https://github.com/openclaw/openclaw/pull/127309) — WhatsApp 群组门控现在遵循 `implicitMentions`。

**表明已修复或已解决的关闭 issue**
- [#167270](https://github.com/openclaw/openclaw/issues/167270) — 飞书跨会话发送附带内部回复锚点 / 首次发送返回 400。
- [#178291](https://github.com/openclaw/openclaw/issues/178291) — 2026.10.4→10.5 更新在激活后 Doctor 阶段失败。
- [#187248](https://github.com/openclaw/openclaw/issues/187248) — 回复失败横幅上的“刷新”按钮失效。
- [#186565](https://github.com/openclaw/openclaw/issues/186565) — `read` 在超过约 512 MB 时因 V8 字符串限制错误而失败。
- [#176027](https://github.com/openclaw/openclaw/issues/176027) — 亚秒级 `timeoutSeconds` 被当作无超时。
- [#183699](https://github.com/openclaw/openclaw/issues/183699) — broker worker 超过 2 个时阻塞 writer。
- [#156666](https://github.com/openclaw/openclaw/issues/156666) — 第三方 slot 所有者禁用 dreaming 后，dreaming cron 任务成为孤儿。
- [#153498](https://github.com/openclaw/openclaw/issues/153498) — 投递队列 media-spool 清理失败。
- [#90587](https://github.com/openclaw/openclaw/issues/90587) — RISC-V64 Codex app-server 退出。
- [#163824](https://github.com/openclaw/openclaw/issues/163824) — 已应用的 Workshop 技能在技能允许列表中不可见。
- [#185191](https://github.com/openclaw/openclaw/issues/185191) — 工作区文件模式退出请求。
- [#188112](https://github.com/openclaw/openclaw/issues/188112) — Goal Resume 按钮拒绝本地 Codex。

**进行中的重要 PR**
- [#188397](https://github.com/openclaw/openclaw/pull/188397) — 在不恢复归档的情况下打开冷会话历史（schema 39），XL 性能变更。
- [#188832](https://github.com/openclaw/openclaw/pull/188832) — 在轮次之间保持未变更的沙箱工作区处于热状态。
- [#188835](https://github.com/openclaw/openclaw/pull/188835) — 在 Gateway 重启验证期间复用已准备的上下文。
- [#188850](https://github.com/openclaw/openclaw/pull/188850) — 在更改默认模型前预览自动化影响。
- [#188865](https://github.com/openclaw/openclaw/pull/188865) — 将 `fs-safe` 更新到 0.27.0，并移除 directory-mode workaround。
- [#188870](https://github.com/openclaw/openclaw/pull/188870) — 恢复冷 TTS 摘要选择和插件准备。

## 4. 社区热点

本数据集未暴露 PR 评论数；下面的 issue 排名按评论数排序。总体反应数仍然较低，表明参与主要由讨论驱动，而非表情回应驱动。

| 条目 | 信号 | 潜在需求 |
|---|---|---|
| [#170956](https://github.com/openclaw/openclaw/issues/170956) Windows 启动缓慢、插件关闭不干净、`schtasks` 权限错误 | 27 条评论，P0，崩溃循环，UX 发布阻断项 | 可靠的 Windows 托管服务生命周期：重启和更新不应需要反复重试，也不应导致客户端断连。 |
| [#150635](https://github.com/openclaw/openclaw/issues/150635) 短期回忆保留每晚驱逐已召回条目，dreaming 深度阶段从不晋升 | 23 条评论，P2，session-state | 在 512 条目上限下记忆/dreaming 管道的正确性；用户期望已学习到的回忆能够留存并晋升。 |
| [#177656](https://github.com/openclaw/openclaw/issues/177656) 原生主机 exec 返回共享状态完整性准入错误 | 21 条评论，P1，稳定版 2026.10.5 上 ≥28 次失败 | 共享状态准入必须跨子进程保持健壮；当前失败会导致子进程产生的效果无法得到证明。 |
| [#159094](https://github.com/openclaw/openclaw/issues/159094) Gateway 持有状态生命周期租约，但 worker 报告另一个进程持有该租约 | 16 条评论，P1，消息丢失/session-state | 多进程状态归属必须一致；当前争用会关闭执行准入。 |
| [#142821](https://github.com/openclaw/openclaw/issues/142821) 默认转录脱敏污染重放的上下文 | 9 条评论，1 👍，P0，数据丢失/安全 | 当被掩码的内容被重放时，安全默认值不得破坏命令、文件或回复。 |
| [#172969](https://github.com/openclaw/openclaw/issues/172969) 不带 `modelProvider` 的 `registerCliBackend` 被静默丢弃，表现为“Invalid URL” | 8 条评论，P2 | 针对插件/运行时配置错误提供更好的诊断，而不是误导性的下游错误。 |
| [#141413](https://github.com/openclaw/openclaw/issues/141413) macOS 应用对使用 `SecretRef` 的本地 Gateway 省略 token | 8 条评论，2 👍，P0，安全评审 | 正确解析受保护密钥的凭据；嵌入式 dashboard 与应用在认证上不一致。 |
| [#188761](https://github.com/openclaw/openclaw/issues/188761) 更改默认 agent 模型时预检自动化兼容性 | 6 条评论，P2 | 防止模型默认值更改时自动化静默损坏；用户希望在应用前预览影响。 |

**分析：** 最热门的讨论集中在**平台可靠性**（Windows 服务、macOS 认证）、**状态归属**（租约、共享状态准入）和**记忆正确性**（dreaming/recall）。这些不是功能争论，而是影响生产运维人员的信任与可靠性问题。

## 5. Bug 与稳定性

### 严重 — P0

| Issue | 状态 | 摘要 | 修复 PR？ |
|---|---|---|---|
| [#170956](https://github.com/openclaw/openclaw/issues/170956) | OPEN，27 条评论 | Windows 启动缓慢、插件关闭不干净、`schtasks` 权限错误；重启/更新不可靠，偶发 1006 断连 | 无新修复 PR；需要维护者评审 |
| [#142821](https://github.com/openclaw/openclaw/issues/142821) | OPEN，9 条评论 | 默认开启的模型可见转录脱敏会污染重放的 agent 上下文；掩码会传播到命令/文件/回复中 | 无新修复 PR；需要产品 + 安全评审 |
| [#169844](https://github.com/openclaw/openclaw/issues/169844) | OPEN，6 条评论 | Windows 上的 Control UI 更新卡在“Activating”；计划任务被留在禁用状态且 gateway 已停止 | 无新修复 PR |
| [#141413](https://github.com/openclaw/openclaw/issues/141413) | OPEN，8 条评论，2 👍 | macOS 应用对使用 `SecretRef` 的本地 Gateway 省略 token；嵌入式 dashboard 可以认证，而应用无法认证 | 无新修复 PR；安全评审 |
| [#163628](https://github.com/openclaw/openclaw/issues/163628) | OPEN，2 条评论 | macOS 应用本地连接始终提供共享 token，当 `auth.mode=password` 时从不回退到密码 | 样本中无关联修复 PR |
| [#178291](https://github.com/openclaw/openclaw/issues/178291) | CLOSED | 2026.10.4→10.5 更新在离线维护权限下激活后 Doctor 失败 | 已关闭 — 请在发布说明中核实 |

### 高 — P1

| Issue | 状态 | 摘要 | 修复 PR？ |
|---|---|---|---|
| [#177656](https://github.com/openclaw/openclaw/issues/177656) | OPEN，21 条评论 | 原生主机 exec 返回共享状态完整性准入错误，且没有子进程结果 | 无新修复 PR |
| [#159094](https://github.com/openclaw/openclaw/issues/159094) | OPEN，16 条评论 | Gateway 持有状态生命周期租约，但内部 worker 报告另一个进程持有该租约 | 无新修复 PR |
| [#162941](https://github.com/openclaw/openclaw/issues/162941) | OPEN，4 条评论 | 来自 `agent_end` 的插件 LLM 补全失败，报错“agent tool caller authority is no longer active” | 无新修复 PR；安全评审 |
| [#188647](https://github.com/openclaw/openclaw/issues/188647) | OPEN，2 条评论 | 模型回退可以选择备用模型，但在派发 provider 请求前静默结束 | 无关联修复 PR |
| [#167270](https://github.com/openclaw/openclaw/issues/167270) | CLOSED | 飞书跨会话发送附带内部回复锚点；首次发送失败并返回 400 | 已关闭 |

### 今日新增/值得注意

- [#188867](https://github.com/openclaw/openclaw/issues/188867) — 针对本地 Bot API 的 Telegram 隔离轮询在紧循环中反复拉取同一个已完成的 update，CPU 占用稳定在 120–170%。提交于 2026-10-31；受理需要复现。
- [#188829](https://github.com/openclaw/openclaw/issues/188829) — 2026.10.9 上更新失败并卡在“validating”（darwin/arm64，Node 26.13.0）；需要补充信息。
- [#188694](https://github.com/openclaw/openclaw/issues/188694) — 2026.10.9 上更新失败并报“invalid-config”；需要补充信息。
- [#188858](https://github.com/openclaw/openclaw/issues/188858) — Automations 编辑器隐藏了重新启用的一次性任务的有效下次运行时间。修复 PR：[#188864](https://github.com/openclaw/openclaw/pull/188864)。
- [#188845](https://github.com/openclaw/openclaw/issues/188845) — 执行 `plugins disable` 后，`doctor --fix` 会重新启用 ID 大小写混合的插件。
- [#188737](https://github.com/openclaw/openclaw/issues/188737) — 当目标会话使用 OpenAI 模型时，计划且仅固定调用的 `show_widget` 不可用。

### 有活跃修复的 P2 稳定性 bug

- [#150401](https://github.com/openclaw/openclaw/issues/150401) — 不带 HTTP 状态的 provider 错误不符合故障转移条件，因此配置的回退从不会尝试。已标记为可排队修复。
- [#147637](https://github.com/openclaw/openclaw/issues/147637) — 在全新的可写 agent DB 上，`openclaw memory index --force` 失败并报“unable to open database file”。
- [#180858](https://github.com/openclaw/openclaw/issues/180858) — Codex GPT-Live WebRTC 启动时丢弃可操作的 provider 错误。
- [#188760](https://github.com/openclaw/openclaw/pull/188760) — Doctor 的 provider 检查改为异步准备；与阻塞插件回调有关。
- [#179893](https://github.com/openclaw/openclaw/pull/179893) — 当提示词注解被拒绝时，Codex 已保存的用户轮次被报告为写入失败。
- [#179891](https://github.com/openclaw/openclaw/pull/179891) — 双引号中使用 `$<digit>` 的 exec 文本会破坏美元金额。

**评估：** P0 集合不大，但高度集中在 **Windows 更新/服务可靠性** 和 **macOS 凭据处理** 上——两者都直接影响运维人员安装、重启和认证的能力。若干 P0 没有关联修复 PR，这是 2026.10.10 稳定版线路的主要稳定性风险。

## 6. 功能请求与路线图信号

**用户积极请求的功能**
- [#188761](https://github.com/openclaw/openclaw/issues/188761) — 更改默认 agent 模型前预检自动化兼容性。PR [#188850](https://github.com/openclaw/openclaw/pull/188850) 已实现影响预览。
- [#150238](https://github.com/openclaw/openclaw/issues/150238) — 针对超大会话中的 Skill Workshop Experience Review，支持上下文预算/跳过策略。
- [#150250](https://github.com/openclaw/openclaw/issues/150250) — 验证 Skill Workshop 的学习覆盖率和行为复用。
- [#169401](https://github.com/openclaw/openclaw/issues/169401) — 允许自有自动化保留显式失败告警，而无需通过所有者会话修复。
- [#166156](https://github.com/openclaw/openclaw/issues/166156) — Talk 中额外语音确认的退出选项（`talk.voiceConfirmation: "off"`）。
- [#150029](https://github.com/openclaw/openclaw/issues/150029) — 使自动化“Inspect”链接可配置（`always | errors | never`）。
- [#148480](https://github.com/openclaw/openclaw/issues/148480) — 复用受限的 Codex 补全上下文，以避免重复的冷历史引导。
- [#168624](https://github.com/openclaw/openclaw/issues/168624) — 面向显式轮次助手消息的安全优先 Android Auto 支持。
- [#187774](https://github.com/openclaw/openclaw/issues/187774) — 可选的 Cua Spaces worker provider。
- [#184709](https://github.com/openclaw/openclaw/issues/184709) — ElevenLabs 批量转录关键词提示。
- [#183537](https://github.com/openclaw/openclaw/issues/183537) — 考虑将 ShieldCortex 和 multi-clawd 纳入官方插件目录/已验证发布者列表。
- [#184523](https://github.com/openclaw/openclaw/issues/184523) — 将 embedding 授权诊断与正常工作的 Codex OAuth 推理分开诊断。

**对下一版本（2026.10.10 稳定版或后续 beta）的预测**
1. **自动化模型变更预检** — [#188761](https://github.com/openclaw/openclaw/issues/188761) + [#188850](https://github.com/openclaw/openclaw/pull/188850) 已具备实现条件。
2. **一次性自动化的有效下次运行时间显示** — [#188858](https://github.com/openclaw/openclaw/issues/188858) + [#188864](https://github.com/openclaw/openclaw/pull/188864)。
3. **更新健壮性** — shallow-clone 挂起（[#188857](https://github.com/openclaw/openclaw/pull/188857)）、构建锁恢复（[#188859](https://github.com/openclaw/openclaw/pull/188859)）、残留 runtime/snapshot 回收（[#188868](https://github.com/openclaw/openclaw/pull/188868)）。
4. **插件/Doctor 诊断与安全加固** — 异步 Doctor provider 检查（[#188760](https://github.com/openclaw/openclaw/pull/188760)）、插件归档审查上限（[#188866](https://github.com/openclaw/openclaw/pull/188866)）、memory-lancedb 证书链拒绝（[#188801](https://github.com/openclaw/openclaw/pull/188801)）。
5. **性能** — 不恢复归档的冷会话历史（[#188397](https://github.com/openclaw/openclaw/pull/188397)）和热沙箱复用（[#188832](https://github.com/openclaw/openclaw/pull/188832)）是较大的 XL 变更，可能在稳定性修复后进入 minor/beta。

近期可能性较低：Android Auto、Cua Spaces、ElevenLabs 关键词和插件目录变更——都仍需要产品/安全决策。

## 7. 用户反馈摘要

**主要痛点**
- **Windows 运维人员反复遇到更新/重启失败。** 启动缓慢、`schtasks` 权限错误、卡在“Activating”以及计划任务被禁用（[#170956](https://github.com/openclaw/openclaw/issues/170956)、[#169844](https://github.com/openclaw/openclaw/issues/169844)）是数据集中最强烈的不满信号。
- **macOS 认证不一致。** 应用无法提供 `SecretRef` token（[#141413](https://github.com/openclaw/openclaw/issues/141413)），或始终使用共享 token 而不回退到密码（[#163628](https://github.com/openclaw/openclaw/issues/163628)）。
- **会话状态和记忆行为削弱信任。** 状态生命周期租约争用（[#159094](https://github.com/openclaw/openclaw/issues/159094)）、dreaming/recall 驱逐（[#150635](https://github.com/openclaw/openclaw/issues/150635)）以及 memory-index 失败（[#147637](https://github.com/openclaw/openclaw/issues/147637)）会影响长期运行的 agent。
- **安全默认值可能导致数据丢失。** 转录脱敏污染重放上下文（[#142821](https://github.com/openclaw/openclaw/issues/142821)）是安全与可用性之间的 P0 矛盾。
- **静默失败和 UX 摩擦。** 例如：`registerCliBackend` 静默丢弃 provider（[#172969](https://github.com/openclaw/openclaw/issues/172969)）、回复失败刷新按钮失效（[#187248](https://github.com/openclaw/openclaw/issues/187248)），以及自动化编辑器隐藏有效下次运行时间（[#188858](https://github.com/openclaw/openclaw/issues/188858)）。
- **2026.10.9 上的更新失败报告**（[#188829](https://github.com/openclaw/openclaw/issues/188829)、[#188694](https://github.com/openclaw/openclaw/issues/188694)）表明配置/验证边界情况仍然存在；两者都需要复现细节。

**满意信号**
- 用户正在积极提交包含环境和版本数据的详细、可复现报告。
- 维护者正在快速关闭有意义的 bug 并合入修复——24 小时内合并/关闭 264 个 PR。
- 表情回应数较低，但 P0/P1 issue 的评论深度显示出运维人员持续投入。

**不满信号：** 更新/认证路径中反复出现的发布阻断 bug 造成“无法可靠升级或重新连接”的观感，这比孤立的功能缺口更具破坏性。

## 8. 待办积压观察

需要维护者关注的重要事项，尤其是较早的高严重度 issue 和对安全敏感的 PR。

| 条目 | 年龄/状态 | 为何重要 |
|---|---|---|
| [#141413](https://github.com/openclaw/openclaw/issues/141413) macOS 应用对使用 `SecretRef` 的本地 Gateway 省略 token | 创建于 2026-09-07，P0，8 条评论，2 👍，需要安全评审 | 样本中最早的开放 P0；无修复 PR。macOS 上的认证正确性仍未解决。 |
| [#150635](https://github.com/openclaw/openclaw/issues/150635) 短期回忆保留每晚驱逐已召回条目 | 创建于 2026-09-17，P2，23 条评论，产品决策 | 讨论热烈的记忆正确性问题；达到上限时 dreaming 晋升从不发生。 |
| [#159094](https://github.com/openclaw/openclaw/issues/159094) 状态生命周期租约归属不匹配 | 创建于 2026-09-26，P1，16 条评论 | 多进程状态争用可能导致消息丢失；仍未关闭。 |
| [#143375](https://github.com/openclaw/openclaw/issues/143375) PDF 工具在打开文档前受 vision 模型门控 | 创建于 2026-09-09，P2，5 条评论 | 没有 vision 模型时无法处理扫描版 PDF；提取信号运行得太晚。 |
| [#147637](https://github.com/openclaw/openclaw/issues/147637) `memory index --force` 在全新的可写 DB 上失败 | 创建于 2026-09-14，P2，5 条评论 | 阻塞记忆重建索引；`memory status` 正常，表明是路径特定 bug。 |
| [#151173](https://github.com/openclaw/openclaw/issues/151173) Memory-core recall rehydration 锚定在片段上 | 创建于 2026-09-17，P2，5 条评论 | 按行距离进行的模糊范围选择可能错误归因已召回内容。 |
| [#148480](https://github.com/openclaw/openclaw/issues/148480) 复用受限的 Codex 补全上下文 | 创建于 2026-09-14，P2，5 条评论 | 重复的冷历史引导在 Codex 交接中浪费延迟/上下文。 |
| [#150238](https://github.com/openclaw/openclaw/issues/150238) Skill Workshop 的上下文预算/跳过策略 | 创建于 2026-09-16，P2，6 条评论 | 超大会话在 Experience Review 期间可能超出模型上下文。 |
| [#150250](https://github.com/openclaw/openclaw/issues/150250) Skill Workshop 学习覆盖率验证 | 创建于 2026-09-16，P3，5 条评论 | 需要证明 workshop 修订确实能改善后续任务。 |
| [#169401](https://github.com/openclaw/openclaw/issues/169401) 自动化失败告警退出选项 | 创建于 2026-10-11，P2，5 条评论 | 所有者会话修复替代了显式失败告警；需要产品决策。 |
| [#179965](https://github.com/openclaw/openclaw/pull/179965) 来自另一个 agent 轮次的 `ask_user` 到达该 agent 而不是所有者 | 自 2026-10-21 起开放，XL，安全敏感 | 路由/隐私边界问题；需要维护者评审。 |
| [#179959](https://github.com/openclaw/openclaw/pull/179959) 允许在未注册个人凭据的情况下获得写访问权限 | 自 2026-10-21 起开放，XL，安全边界 | 共享 Gateway 运维人员需要受管凭据策略；评审风险高。 |
| [#179893](https://github.com/openclaw/openclaw/pull/179893) Codex 已保存的用户轮次被报告为写入失败 | 自 2026-10-21 起开放，P2 | 错误的持久化错误和跳过的通知；修复很小但仍在等待。 |
| [#179891](https://github.com/openclaw/openclaw/pull/179891) Exec 美元金额被 `$<digit>` 破坏 | 自 2026-10-21 起开放，P2 | agent 发送的消息中的数据损坏；修复会拒绝损坏输出，但需要证明。 |
| [#178033](https://github.com/openclaw/openclaw/pull/178033) 针对 cadence 和 activeHours 的心跳状态 | 自 2026-10-20 起开放，P3 | 运维可见性缺口；等待维护者评审。 |

**底线：** OpenClaw 的贡献者吞吐量很强，但其**评审与产品决策队列**是 P0/P1 可靠性工作的瓶颈。本周维护者最高杠杆的行动是：合入或指派 Windows 更新/服务生命周期修复（[#170956](https://github.com/openclaw/openclaw/issues/170956)、[#169844](https://github.com/openclaw/openclaw/issues/169844)），解决 macOS 认证（[#141413](https://github.com/openclaw/openclaw/issues/141413)、[#163628](https://github.com/openclaw/openclaw/issues/163628)），并决定转录脱敏中的安全/可用性权衡（[#142821](https://github.com/openclaw/openclaw/issues/142821)）。

---

## 横向生态对比

## 跨项目对比报告 — 2026-10-31

*范围：OpenClaw、Hermes Agent、IronClaw、QwenPaw、ZeroClaw。除特别说明外，计数均为 24 小时摘要快照。健康分为 0–10 的方向性综合评分，由合并吞吐量、积压平衡度、发布节奏和严重性风险构成；它们不是安全认证。*

---

### 1. 生态概览

2026-10-31 的个人 AI 助手/智能体开源格局，特征是高贡献量与更紧张的评审带宽，而非广泛的功能发布。OpenClaw 仍是参考级规模项目，Hermes Agent、QwenPaw 和 ZeroClaw 则处于活跃的中期迭代；IronClaw 处于仅维护窗口。主要工作是可靠性加固：会话/状态所有权、平台特定的更新与认证路径、通道适配器语义、安全默认值以及成本/缓存控制。静默降级和工作丢失是反复出现的用户抱怨，尤其是子系统报告成功却未能执行操作时。该窗口内除 OpenClaw 外没有项目发布版本，因此大量可见工作排入未来的 beta/stable 版本。

---

### 2. 活动对比

| 项目 | Issue 数量 | PR 数量 | 已合并/已关闭 PR | 开放 PR | 发布状态 | 健康分 |
|---|---:|---:|---:|---:|---|---:|
| **OpenClaw** | 86 个更新 | 500 个更新 | 264 | 236 | **v2026.10.10-beta.5 已发布** | **7.5/10** |
| **Hermes Agent** | 15 个更新（4 个新增，2 个关闭） | 50 个更新 | 8 | 42 | 无新版本发布 | **7.0/10** |
| **IronClaw** | 0 个更新 | 1 个更新 | 0 | 1 | 无发布 | **5.0/10 中性** |
| **QwenPaw** | 8 个更新 | 32 个更新 | 11 | 21 | 无新版本；最新 **v2.3.0-beta.1**（10/27） | **7.5/10** |
| **ZeroClaw** | 6 个活跃/开放 | 50 个更新 | 0 | 50 | 无发布 | **5.5/10** |

**解读表格：** OpenClaw 是唯一在本窗口内既有可观合并吞吐量又发布版本的项目。QwenPaw 在中阶段项目中拥有最健康的合并/开放比例。Hermes 的分诊响应及时，但 PR 开放/关闭比为 42:8。ZeroClaw 贡献者供给强劲，但 24 小时内零合并。IronClaw 没有面向用户的活动信号。

---

### 3. OpenClaw 的定位

**相较同行的优势**
- **活动足迹领先一个数量级：** 86 个 Issue 更新和 500 个 PR 更新，而 Hermes 为 15/50，QwenPaw 为 8/32，ZeroClaw 为 6/50，IronClaw 为 0/1。
- **唯一在本窗口内发布版本的项目：** `v2026.10.10-beta.5`，聚焦 Node 兼容性与安装/更新可靠性。
- **最高交付吞吐量：** 已合并/关闭 264 个 PR，而 QwenPaw 为 11，Hermes 为 8，ZeroClaw 为 0。
- **最广泛的运行面：** Windows 服务生命周期、macOS 认证、转录内容脱敏、插件源准备、沙箱热复用、冷会话历史以及多渠道集成。

**技术路线差异**
- OpenClaw 是**核心网关/运行时 + 插件生态**，具备显式的状态生命周期所有权、沙箱/工作区管理、转录内容脱敏和发布通道纪律。
- 同行则更聚焦：Hermes 聚焦桌面/仪表盘 + Kanban/cron 工作流；QwenPaw 聚焦桌面打包、通道和治理；ZeroClaw 聚焦基于 Rust 的安全/自主性和上下文经济学。

**社区规模对比**
- 以 24 小时活动量作为代理指标，OpenClaw 的 Issue 队列约为 Hermes 的 5.7 倍、QwenPaw 的 10.8 倍、ZeroClaw 的 14.3 倍。其 PR 更新量约为 Hermes/QwenPaw/ZeroClaw 的 10 倍。
- 主要弱点不是贡献者供给，而是**评审与产品决策带宽**：P0 级 Windows 更新/服务问题和 macOS 认证问题仍未关闭，且没有关联修复 PR；同时仍有 236 个 PR 处于开放状态。

---

### 4. 共同技术重点领域

| 新兴需求 | 有证据的项目 | 具体需求 |
|---|---|---|
| **会话/状态持久性** | OpenClaw #159094、#177656；Hermes #145022；ZeroClaw #11457、#11727；QwenPaw #8511 | 一致的多进程状态所有权、租约围栏（lease fencing）、可恢复工作，以及在不丢失进行中任务的情况下从网关停滞中恢复。 |
| **静默失败可观测性** | QwenPaw #8488、#8500、#8505；OpenClaw #172969、#188647、#188858；Hermes #147025、#147020；ZeroClaw #11589、#11624 | 可见的降级警告、结构化错误分类、非零退出语义，以及预检诊断，而不是“成功”却什么都没做。 |
| **平台一致性与打包** | OpenClaw #170956、#169844、#141413、#163628；QwenPaw #8488、#8502；ZeroClaw #12133、#12134；Hermes #142741、#144616、#146657 | Windows/macOS/WSL CI 覆盖、冻结构建产物校验、原生服务生命周期、环境变量允许列表以及 CJK 路径处理。 |
| **安全默认值与治理** | OpenClaw #142821、#141413、#179965、#179959；QwenPaw #8513；ZeroClaw #12134、#12131；Hermes #147019 | 默认安全策略，同时不破坏上下文或不阻塞合法流程；审批门禁、允许列表、密钥解析和可审计性。 |
| **成本/缓存/上下文经济学** | ZeroClaw #11703、#11698、#12044；OpenClaw #188397、#188832；Hermes #127647；QwenPaw #8496 | 稳定的提示前缀、沙箱热复用、上下文预算、缓存感知的工具激活以及运营方成本控制。 |
| **通道/适配器语义** | Hermes #30989、#139875、#140202；OpenClaw #188867、#167270、#127309；QwenPaw #8511；ZeroClaw #10926 | 按通道进行防抖/合并/重试、目标寻址正确性，以及一致性测试，以确保跨平台消息处理一致。 |
| **评审/合并带宽** | OpenClaw 236 个开放 vs 264 个已合并；Hermes 42 vs 8；QwenPaw 21 vs 11；ZeroClaw 50 vs 0 | 维护者评审轮换、明确负责人、更小的 PR 和 CI 门禁——在多个项目中，贡献者供给正超过落地能力。 |

---

### 5. 差异化分析

| 项目 | 功能重点 | 目标用户 | 技术架构信号 |
|---|---|---|---|
| **OpenClaw** | 核心助手网关、多渠道集成、插件、沙箱/工作区生命周期、转录内容安全、Windows/macOS 可操作性 | 生产环境运营者、插件开发者、高级用户 | 网关/运行时 + 插件源准备 + 沙箱 + 状态生命周期；成熟的 beta 发布流程 |
| **Hermes Agent** | 桌面/仪表盘、Kanban 工作器编排、cron 智能体、SSH/移动终端、会话搜索、插件目录 | 多工作器编排者、桌面与远程终端用户 | 网关/会话所有权、SQLite cron 账本、Git 工具、桌面渲染器、通道适配器 |
| **IronClaw** | 本窗口信号极少；仅 WebUI 依赖维护 | 无法从数据评估 | Rust crate + WebUI 前端；针对 `happy-dom` 的 Dependabot 更新 |
| **QwenPaw** | 桌面/PyInstaller 构建、通道可靠性、提供方兼容性、`tool_guard`/治理、插件系统、本地推理方向 | 桌面用户、zh-CN/CJK 用户、自托管/代理推理运营者、插件生态 | 桌面打包、插件系统、审批级别、通道适配器、本地 Piccolo 模型工作 |
| **ZeroClaw** | 安全/自主性、ZeroCode 用户体验、Matrix/XMPP 通道、成本/上下文经济学、智能体到智能体会话消息 | 注重安全的自主智能体运营者、Rust 生态 | Rust 配置/策略、通道/提供方、子进程看门狗、分阶段的 Goal V1 epic |

---

### 6. 社区动能与成熟度

| 层级 | 项目 | 证据 | 动能解读 |
|---|---|---|---|
| **高吞吐 + 发布节奏** | **OpenClaw** | 已合并/关闭 264，开放 236，beta 版本已发布 | 快速迭代与可靠性加固；评审带宽是约束 |
| **活跃稳定化** | **QwenPaw、Hermes Agent** | QwenPaw：beta 后已合并 11/开放 21；Hermes：已合并 8/开放 42，有挽救性 PR | QwenPaw 正收敛于 beta 基础设施；Hermes 正在整合但受评审制约 |
| **贡献者众多、合并受限** | **ZeroClaw** | 50 个开放 PR，0 个已合并；针对新 S1/S2 bug 的当日修复 PR | 贡献者供给强劲，落地吞吐量弱；存在疲劳风险 |
| **仅维护 / 无面向用户信号** | **IronClaw** | 1 个 Dependabot PR，0 个 Issue 更新 | 本窗口无动能信号 |

**成熟度评估：** OpenClaw 在发布与运营流程上最成熟，但承载集中的 P0 平台风险。Hermes 和 QwenPaw 拥有可运转的外部贡献者流水线和活跃分诊。ZeroClaw 的贡献者供给/落地能力失衡最为明显。IronClaw 无法基于这一数据切片评估成熟度。

---

### 7. 趋势信号

1. **可靠性就是产品。** 平台特定的更新/认证失败和会话状态争用主导了运营者抱怨。开发者应在添加功能之前，投资于跨平台服务生命周期、认证回退和状态所有权围栏。
2. **静默失败比显性失败更具破坏性。** QwenPaw 的 Visual Compact 空操作和 Auto-Dream 记忆丢失、OpenClaw 的静默提供方掉线和模型回退，以及 ZeroClaw 失效的 `cost.allow_override`，都在失败时报告成功。可观测的降级、结构化错误和非零退出正成为基线要求。
3. **安全默认值需要策略，而不是一刀切阻断。** OpenClaw 的转录内容脱敏会污染重放的上下文；QwenPaw 的 shell 包装出站操作会绕过审批；ZeroClaw 的禁止路径默认值会漏掉 WSL/Windows 卷。趋势是采用允许列表、审批工作流、审计轨迹和密钥解析，同时保持可用性。
4. **成本/缓存/上下文经济学很重要。** 提示缓存失效、空闲资源消耗、冷历史引导和上下文预算现在都是首要用户抱怨。稳定的提示前缀、沙箱热复用和缓存感知的工具激活是高价值工程方向。
5. **通道适配器需要一致性语义。** BlueBubbles 拆分事件、Telegram 轮询循环、Matrix 对等端 vs 房间寻址，以及 Feishu 处理中途错误，都指向同一需求：按通道进行防抖/合并/重试，以及明确的目标语义，并由测试保障。
6. **提供方无关推理是一等部署模式。** OpenAI 兼容中继、本地 Whisper 端点和自托管网关需要稳健的状态码提取、回退分类和兼容性垫片，而不是假设 OpenAI 的精确错误形态。
7. **桌面/冻结构建一致性是新兴薄弱点。** PyInstaller 产物遗漏、Windows 环境变量允许列表、CJK 路径、launchd/Nix 版本管理，以及 Windows arm64 测试缺口，都表明 CI 矩阵和打包检查正成为差异化因素。
8. **评审带宽是生态瓶颈。** OpenClaw、Hermes、QwenPaw 和 ZeroClaw 都表现出贡献者数量达到或超过维护者落地能力。对开发者而言，这更有利于更小、关联修复且测试充分的 PR；对维护者而言，这更有利于指定评审人，并对大型 PR 做出明确的接受/推迟决定。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — 项目摘要
**日期：** 2026-10-31 · **仓库：** [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. 今日概览

活动量很高，但偏向接收新事项而非收尾：过去 24 小时共有 65 条 issue/PR 更新，其中 50 条是 PR——然而只有 8 个 PR 被合并或关闭，仍有 42 个处于打开状态。2026-10-30/31 新增 4 个 issue，关闭 2 个 issue，其中包括同一窗口内对一个浏览器扩展权限 bug 的修复。**没有新发布**，因此所有工作都排队等待未来的 tag。工作本身高度集中在可靠性工程——gateway/session 状态、cron ledger 争用、Git index 锁定以及供应链依赖升级——其中有两个 P1 级事项活跃（#145022 打开的 bug，#145615 打开的修复 PR）。整体健康状况可解读为**活跃且响应及时，但受评审制约**：维护者明显处于整合模式（来自 `teknium1` 的两个“salvage”PR），而 2026 年 5 月的一串 bug 报告和 9 月的 PR 仍未解决。

---

## 2. 发布

本窗口没有新发布。没有需要报告的迁移或破坏性变更说明。

---

## 3. 项目进展

**过去 24 小时关闭/合并（共 8 个；在 PR 前 20 样本中可见 6 个）：**

| 条目 | 领域 | 落地内容 |
|---|---|---|
| [PR #118111](https://github.com/NousResearch/hermes-agent/pull/118111) | Git / agent 工具 | 在受限内部探测中禁用可选 Git 锁，以阻止产生游离的 `.git/index.lock` 文件。该改动已被 [PR #147031](https://github.com/NousResearch/hermes-agent/pull/147031) 取代并扩展；后者由 `teknium1` 今日打开，从所有后台 `git status` 读取中移除锁获取——包括会话启动探测、dashboard 编码栏、Review 面板、子代理 worktree 检查。 |
| [PR #143888](https://github.com/NousResearch/hermes-agent/pull/143888) | Dashboard / 移动端 | Android IME 编辑现在在 `beforeinput` 处理，修复了从未到达 PTY 的点击（#137986）。 |
| [PR #143102](https://github.com/NousResearch/hermes-agent/pull/143102) | Dashboard / 移动端 | 移动端抽屉菜单的过度滚动遏制（iOS Safari 滚动链）。 |
| [PR #138954](https://github.com/NousResearch/hermes-agent/pull/138954) | Gateway / 存储 | 空闲临时目录现在会在 housekeeping tick 上重新清扫，修复了仅以 gateway 作为唯一长期进程的主机上的保留问题。 |
| [PR #127163](https://github.com/NousResearch/hermes-agent/pull/127163) | Desktop / SSH | SSH 隧道抖动预算从重试次数改为时间窗口；keepalive 部分已合入上游。 |
| [PR #117126](https://github.com/NousResearch/hermes-agent/pull/117126) | Tools / 会话 | `session_search` 现在报告匹配集覆盖率，而不是截断后的返回切片。 |
| [Issue #147013](https://github.com/NousResearch/hermes-agent/issues/147013) | Gateway / 浏览器扩展 | 已关闭——`source=hermes_browser` 会话被三个准入闸门拒绝。 |
| [Issue #142962](https://github.com/NousResearch/hermes-agent/issues/142962) | 插件目录 | 已关闭——`limbic` 目录条目升级到 0.9.0。 |

**今日新开的修复工作：** [PR #147030](https://github.com/NousResearch/hermes-agent/pull/147030) 串行化 `cron/executions.py` 的 ledger 写入，使 SQLite 争用时等待而不是杀死 worker（修复 #135487；部署实测有 12 个并发写入者和 50 个作业共享第 0 分钟）。安全/维护：[PR #147028](https://github.com/NousResearch/hermes-agent/pull/147028)（undici、zod、fast-uri 安全公告）和 [PR #147029](https://github.com/NousResearch/hermes-agent/pull/147029)（body-parser 1.20.9，GHSA-27r3-jxmh-p828）。

---

## 4. 社区热点

本数据集中未填充 PR 的评论数；以下 issue 互动数据是完整的。

1. **[Issue #127647](https://github.com/NousResearch/hermes-agent/issues/127647) — 34 条评论** · *Tracker：桌面端空闲资源消耗*（P2，comp/desktop）。这是讨论量最高的条目，自 2026-09-29 打开，包含索引化分诊计划、PR 交叉引用索引，以及对“哪些改动引入了各机制”的因果分析。**底层需求：** 常开助手在空闲时必须低成本——笔记本电池、风扇噪音和后台 CPU/GPU 现在是一等产品问题，而非边缘情况。该 tracker 形式表明维护者预期这是一场多 PR 行动，而不是单个修复。
2. **[Issue #145022](https://github.com/NousResearch/hermes-agent/issues/145022) — 12 条评论** · *Kanban worker 崩溃，报“Kanban execution unknown; retained by owner”*（P1，comp/gateway，area/sessions）。一次 gateway 停顿同时杀死了 4 个 worker，并丢弃了进行中的工作。**需求：** 在 gateway 背压下实现持久、可恢复的会话所有权——重试能恢复卡片，但无法恢复工作。
3. **[Issue #30989](https://github.com/NousResearch/hermes-agent/issues/30989) — 6 条评论** · *BlueBubbles 文本+附件以两个事件到达并打断当前轮次*（P2）。**需求：** 适配器一致性——Telegram 有去抖/合并，BlueBubbles 没有，因此 iMessage 用户会遇到虚假的 `⚡ Interrupting current turn` 事件。
4. **[Issue #142741](https://github.com/NousResearch/hermes-agent/issues/142741) — 6 条评论** · *launchd bootstrap 重试从不 kickstart 已注册但未运行的作业*（P2，os/macos）。**需求：** 可靠的服务监督；`launchctl list` 显示 PID 时会被当作存活证明，但事实并非如此。
5. **[Issue #131433](https://github.com/NousResearch/hermes-agent/issues/131433) — 5 条评论，1 👍** · *已关闭的 cron 运行在首次回复后变为只读*（P2）。这是 #124945 写入限制逻辑引入的回归。**需求：** 清晰、有文档的会话写入语义，且能在重构后保持。

**模式：** 前五名中有三个是会话状态或适配器投递问题，且其中几个带有 `sweeper:risk-session-state` / `risk-message-delivery` 标签——一个自动化风险打标系统反复标记同一子系统。

---

## 5. Bug 与稳定性

按严重性和影响范围排序：

| 严重性 | 条目 | 影响 | 修复 PR？ |
|---|---|---|---|
| **P1** | [#145022](https://github.com/NousResearch/hermes-agent/issues/145022) gateway 停顿时 Kanban worker 崩溃 | 进行中工作丢失，多 worker 集群故障 | 未见 |
| **P1** | [PR #145615](https://github.com/NousResearch/hermes-agent/pull/145615)（打开）——owner-forward 拒绝大于 1 MiB 的 `session.resume` 应答 | TUI gateway 恢复失败；已添加 socket 级测试 | 这*就是*修复（针对 #145215） |
| **P2** | [#147026](https://github.com/NousResearch/hermes-agent/issues/147026)（新）——reasoning 重放会在裸 `custom` 路由上重复填充 `reasoning` + `reasoning_content` | 在严格主机（SenseNova）上，从第 2 轮起每个多轮聊天都返回 400 | 无 |
| **P2** | [#145182](https://github.com/NousResearch/hermes-agent/issues/145182)——`auxiliary.vision` 回退将 aux 模型名带到自动检测的 provider | Vision 请求返回 400（`<local model> is not a valid model ID`） | 无 |
| **P2** | [#30989](https://github.com/NousResearch/hermes-agent/issues/30989) BlueBubbles 拆分事件打断 | 轮次中途打断，上下文重复 | 无（已打开约 5 个月） |
| **P2** | [#142741](https://github.com/NousResearch/hermes-agent/issues/142741) macOS 上 launchd 重启失败 | 无法通过 CLI 重启 gateway | 无 |
| **P2** | [#131433](https://github.com/NousResearch/hermes-agent/issues/131433) cron 运行在首次回复后变为只读 | 桌面端 Cron 功能回归 | 无 |
| **P2** | [#144616](https://github.com/NousResearch/hermes-agent/issues/144616) Nix 构建报告 `0.0.0` | Home Assistant 插件从不加载（要求 ≥0.21.5）；误导性更新警告 | 无 |
| **P2** | [#147020](https://github.com/NousResearch/hermes-agent/issues/147020)（新）——生命周期守卫将带点的 `server.kill()` 视为 shell `kill` | 在序列化源码中误拦截命令；运营风险 | 无 |
| **P2** | [#147025](https://github.com/NousResearch/hermes-agent/issues/147025)（新）——`platform_toolsets.<platform>: []` 仍加载所有 MCP 服务器 | 配置语义被静默反转；`no_mcp` 未记录 | 无 |
| **P2** | [#30323](https://github.com/NousResearch/hermes-agent/issues/30323) 遗留 `/steer` 在排队的后续消息之后生效 | 指导信息延迟送达或看起来被丢弃 | 无 |
| **P2** | [#26451](https://github.com/NousResearch/hermes-agent/issues/26451) 技能发现递归进入隐藏工作区目录 | Vendored/生成的技能被显示为已安装 | 无 |

**稳定性说明：** [PR #146657](https://github.com/NousResearch/hermes-agent/pull/146657)（打开）报告了 30 个 Windows arm64 测试修复，**其中六个是真实产品 bug**——这表明非 POSIX CI 覆盖很薄。同一天关闭 #147013 表明，当根因定位明确时，处理速度很快。

---

## 6. 功能请求与路线图信号

本窗口只有一个明确的功能请求：

- **[Issue #147019](https://github.com/NousResearch/hermes-agent/issues/147019) — hardline 检查的覆盖开关**（新，0 条评论）。运行自动化测试/安装流程的用户需要重启，而当前只能“把重启命令偷偷塞进 shell 脚本”来绕过守卫。**预测：** 作为有作用域的配置门控进入下一个 minor 版本是可能的，但由于触及安全边界（`hardline`），预计维护者会要求白名单/确认设计，而不是一刀切开关——可能比典型配置修复更慢。

**下一版本可能包含的内容**，基于实际接近就绪的工作：
- 安全/依赖补丁集：[#147028](https://github.com/NousResearch/hermes-agent/pull/147028)、[#147029](https://github.com/NousResearch/hermes-agent/pull/147029)。
- Git 锁修复 [#147031](https://github.com/NousResearch/hermes-agent/pull/147031) 和 cron ledger 串行化 [#147030](https://github.com/NousResearch/hermes-agent/pull/147030)——两者都小而聚焦，并带有 `ci-reviewed` 标签/关联到 issue。
- 插件目录清理 [#147027](https://github.com/NousResearch/hermes-agent/pull/147027)，加上刚刚关闭的 limbic 0.9.0 条目。
- 桌面端/dashboard 打磨（#146642 行内代码货币转义，#146657 Windows 测试矩阵）。

**不太可能进入下一版本：** 空闲资源消耗治理行动（#127647）横跨多种机制，将增量落地；大型会话裁剪 PR [#108582](https://github.com/NousResearch/hermes-agent/pull/108582)（自 2026-09-11 打开）已经拆分过一次（#125807），看起来有再次延期的风险。

---

## 7. 用户反馈摘要

**痛点，按出现频率排序：**
1. **空闲成本**——桌面渲染器 CPU/GPU、后端服务 CPU 和内存增长（#127647）主导讨论量；用户将其视为日常使用阻塞项。
2. **失败时丢失工作**——Kanban worker 崩溃（#145022）和 cron 只读回归（#131433）都会破坏或阻塞进行中的状态。用户强调重试恢复的是*卡片*，而不是*工作*。
3. **平台适配器不一致**——BlueBubbles（#30989）、Telegram 论坛主题（#139875）、WeCom/WeChat 限流推送丢失（#140202）都是不同包装下的同一类抱怨：消息语义因平台而异，且失败是静默的。
4. **安装/更新摩擦**——Nix `0.0.0` 版本（#144616）、`hermes update` 后 PEP 660 可编辑安装映射陈旧（#134458），以及误导性的迁移提示。
5. **配置意外**——空列表表示“所有 MCP 服务器”（#147025）以及回退时 provider/model 不匹配（#145182）都违背用户心智模型，而不是显式失败。

**报告中可见的使用场景：** 多 worker Kanban 编排、cron 驱动的定时代理、桌面 + 远程 SSH 会话、macOS launchd 服务部署、移动 Web 终端使用，以及真实插件生态（limbic memory、hermes-finance、Home Assistant）。

**满意度信号：** 报告质量异常高——提交 SHA、基于 `origin/main` 的源码检查复现、socket 级测试，以及无法打开 PR 的用户提供的内联 diff（例如 #142962、#145615 致谢的上游分支）。同一窗口内关闭 #147013 显示了响应性。**不满信号：** 一个五个月之久的适配器 bug、反复出现的 `sweeper:risk-session-state` 标签，以及 42 个打开 PR 对 8 个关闭 PR——贡献者的产出速度快于评审完成速度。

---

## 8. 积压观察

需要维护者关注的事项，按陈旧度 × 重要性排序：

| 条目 | 存在时长 | 为何重要 |
|---|---|---|
| [#30989](https://github.com/NousResearch/hermes-agent/issues/30989) BlueBubbles 拆分事件 | 自 **2026-05-23** 打开（约 5 个月），6 条评论 | 每个 iMessage 文本+附件轮次都会被打断；Telegram 已经解决了这个问题——很可能是移植，而不是设计问题。 |
| [#30323](https://github.com/NousResearch/hermes-agent/issues/30323) 遗留 `/steer` 顺序 | 自 **2026-05-22**，3 条评论 | CLI 指导信息被静默丢弃；影响对 steering 的信任。 |
| [#26451](https://github.com/NousResearch/hermes-agent/issues/26451) 技能发现中的隐藏目录 | 自 **2026-05-15**，2 条评论 | 修复成本低，对任何有编辑器生成目录的人都是正确性问题。 |
| [PR #108582](https://github.com/NousResearch/hermes-agent/pull/108582) 精确选择会话裁剪 | 自 **2026-09-11** | 大型功能，已拆分一次；需要决策（合并、重新划定范围或关闭），而不是继续漂移。 |
| [PR #134458](https://github.com/NousResearch/hermes-agent/pull/134458) / [PR #134460](https://github.com/NousResearch/hermes-agent/pull/134460) | 自 **2026-10-07** | 更新流程和 CLI 正则修复，带有 `risk-compatibility` 标签；两者都很小且无阻塞。 |
| [#127647](https://github.com/NousResearch/hermes-agent/issues/127647) 空闲消耗 tracker | 自 **2026-09-29**，34 条评论 | 仓库中互动量最高的条目，且仍是一个 tracker——分配负责人和里程碑，让 34 条评论的分析转化为已交付的 PR。 |

**结论：** 项目在贡献和分诊速度方面是健康的，但存在可衡量的**评审与合并瓶颈**（打开/关闭 PR 比例 42:8）以及持续存在的会话状态/适配器 bug 集群。清理五个月之久的适配器 issue 和 9 月 PR 队列，对本周期感知可靠性的提升将超过任何新功能工作。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目摘要 — 2026-10-31

## 今日概览
IronClaw 在 2026-10-31 活动量极低：0 条 Issue 更新、1 条开放 PR 更新，以及 0 个新版本或已合并/关闭的 PR。唯一活动是 Dependabot PR [#8164](https://github.com/nearai/ironclaw/pull/8164)，即 WebUI 前端的开发依赖 `happy-dom` 版本升级。在提供的数据中，未记录到面向用户的缺陷、功能请求或社区讨论。总体来看，这是一个仅进行维护的窗口期，没有证据表明存在回归或发布推进势头。

## 项目进展
- 今日没有 PR 被合并或关闭。
- 没有功能推进，也没有修复发布。
- [#8164](https://github.com/nearai/ironclaw/pull/8164) 仍处于开放状态，似乎正在等待审查/CI 验证。

## 社区热点
- 没有 Issue 被更新，因此没有活跃的 Issue 讨论。
- 该窗口内唯一的 PR 是 [#8164](https://github.com/nearai/ironclaw/pull/8164)：`chore(deps-dev): bump happy-dom from 20.11.1 to 21.0.4`，位于 `/crates/product/ironclaw_webui/frontend`。
- 数据集中未提供评论数；反应数为 0。这是一个自动化依赖维护项，而非社区讨论。
- 底层需求：保持前端测试/工具链依赖为最新且兼容。

## 缺陷与稳定性
- 今日未报告缺陷、崩溃或回归。
- 提供的数据中不存在缺陷修复 PR。
- 潜在的低至中等审查风险：[#8164](https://github.com/nearai/ironclaw/pull/8164) 将 `happy-dom` 跨主版本边界升级（20 → 21），因此维护者应核对上游发布说明和 CI 结果，以确认前端测试兼容性。

## 功能请求与路线图信号
- 过去 24 小时内没有功能请求或路线图信号。
- 无法根据该数据窗口推断下一版本的功能预测。

## 用户反馈摘要
- 今日未记录到真实用户反馈。
- 无法根据提供的数据评估用户痛点、使用场景以及满意度/不满意度。
- 唯一活动是自动化依赖维护，而非面向用户的产品反馈。

## 待办积压观察
- 提供的数据中没有出现长期未答复的重要 Issue 或 PR。
- 唯一的开放事项是 [#8164](https://github.com/nearai/ironclaw/pull/8164)，创建并更新于 2026-10-30。它尚未长期未答复，但它是该窗口内唯一的维护者行动项，应获得常规的依赖审查关注。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/QwenPaw">agentscope-ai/QwenPaw</a></summary>

# QwenPaw 项目摘要 — 2026-10-31

*数据窗口：活动更新于 2026-10-30 → 2026-10-31 · 来源：github.com/agentscope-ai/QwenPaw*

---

## 1. 今日概览

QwenPaw 正处于 beta 后的稳定化冲刺阶段：在 **v2.3.0-beta.1** 发布（2026-10-27）四天后，追踪器在 24 小时内记录到 **40 条 issue/PR 更新**（8 个 issue、32 个 PR），其中 **11 个 PR 已合并或关闭**，另有 21 个仍开放——对于预发布窗口而言，这是一个健康的合并/开放比例。发布值班安装验证问题（#8456）今日已关闭，表明 beta 安装检查已结束，且未发布新版本。活动集中在**桌面/PyInstaller 打包缺口、提供商错误分类和渠道可靠性**上，并已为两个评论最多的问题提交当日修复 PR（#8488 → #8514，#8505 → #8512）。主要健康隐患是一组**静默失败缺陷**（Visual Compact 空操作、Auto-Dream 记忆丢失却报告 `success=True`），外加一个**尚未修复的治理/安全缺口**（#8513），目前没有修复 PR。总体：**迭代速度快、贡献者吞吐良好，静默失败带来更高的信任风险。**

---

## 2. 发布

**今日无新版本发布。** 最新已发布版本仍为 **v2.3.0-beta.1（Beta，2026-10-27）**；发布值班验证问题 [#8456](https://github.com/agentscope-ai/QwenPaw/issues/8456) 已于 2026-10-30 关闭，标志着 beta 安装检查关口已通过。今日摘要中的所有缺陷都针对这一 beta 线，因此下一次 2.3.0 预发布/稳定版将包含一批有意义的桌面端和提供商修复（见 §3）。

---

## 3. 项目进展

**今日合并/关闭（在前 20 条样本中可见）：**

| PR | 标题 | 影响 |
|---|---|---|
| [#8483](https://github.com/agentscope-ai/QwenPaw/pull/8483) | fix(plugins)：防止一次失败的导入缓存刷新拖垮整个插件系统 | **高** — 在 Debian 12 / CPython 3.11.9+ 主机上，由于 `importlib.metadata` 不匹配，*所有*后端插件都无法加载 |
| [#8508](https://github.com/agentscope-ai/QwenPaw/pull/8508) | fix(workspace)：移除旧版工作区 ZIP API | **高** — 消除了可能覆盖在线 SQLite 文件的 ZIP 合并路径；该路径在 #8482 之后于 Windows 上失效 |
| [#7896](https://github.com/agentscope-ai/QwenPaw/pull/7896) | fix(channels)：在等待消费者关闭后重新检查空闲队列 | **高** — 修复空闲渠道清理中的消息丢失竞态（首次贡献者） |
| [#6041](https://github.com/agentscope-ai/QwenPaw/pull/6041) | fix(loop)：将只读工具从 doom loop 检测中豁免 | **中** — 终止重复记忆读取导致的误判终止（关闭 #5906）；自 7 月起开放 |
| [#8507](https://github.com/agentscope-ai/QwenPaw/pull/8507) | fix(console)：移除共享内存标签测试夹具依赖 | **中** — 解除 Docker 前端构建阻塞（TS2307 错误链） |
| [#8379](https://github.com/agentscope-ai/QwenPaw/pull/8379) | fix(tests)：让完整 pytest 收集两个 `test_backup` 模块 | **低** — 恢复 CONTRIBUTING.md 中的绿色 `pytest` 门禁 |

**净效果：** 今日关闭的 beta 阻塞项属于基础设施层面（插件启动、工作区 ZIP、测试收集、Docker 构建），而非面向用户的功能——这与稳定版前的加固方向一致。六个关闭项中有三个来自首次/回归的外部贡献者，是积极的生态信号。

---

## 4. 社区热门话题

反应数据全线持平（所有条目均为 👍 0），因此讨论量是唯一的热度代理指标。

1. **[#8488](https://github.com/agentscope-ai/QwenPaw/issues/8488) — 桌面构建遗漏 `visual_compression` 资源（3 条评论）** — 当日讨论最多的问题。Windows PyInstaller 构建的用户在 `atlas-gray-native.ts` 上遇到 `FileNotFoundError`，因此 **Visual Compact 在每次符合条件的模型调用中都会静默空操作**。底层需求：*开发构建与冻结构建之间的功能对等保证*；比起缺失优化，用户更难容忍假装运行的优化。修复 PR [#8514](https://github.com/agentscope-ai/QwenPaw/pull/8514) 已开放（将数据目录加入 `qwenpaw.spec`）。
2. **[#8505](https://github.com/agentscope-ai/QwenPaw/issues/8505) — 网关 502 被误分类为 `unknown`（2 条评论）** — 位于 OpenAI 兼容中转之后的用户**既不会重试，也不会进行模型回退**，因为状态码只存在于消息文本中（`status_code=502, 请联系管理员处理！`）。底层需求：自托管/代理推理的韧性；在该用户群中，中转已是常态。修复 PR [#8512](https://github.com/agentscope-ai/QwenPaw/pull/8512) 已开放。
3. **[#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500) — Auto-Dream 静默丢弃记忆（2 条评论）** — 无法解析的提取回执仍会被写入检查点，导致一整天的记忆被丢弃且永不重试，而运行仍报告 `success=True`。底层需求：长时间运行的记忆流水线中的**可观测失败语义**。
4. **[#8513](https://github.com/agentscope-ai/QwenPaw/issues/8513) — Shell 包装的出站操作绕过审批（1 条评论）** — 一位关注安全的用户报告，SMTP 发送 / HTTP POST / `@file-to-network` shell 命令在 `AUTO` 或 `SMART` 下都不会产生检测发现，也不会弹出审批提示，且在 `tool_guard` 和治理通道中都是如此。

---

## 5. Bug 与稳定性

按严重性排序（正确性/安全性 → 用户体验）：

| 严重性 | 条目 | 症状 | 修复 PR？ |
|---|---|---|---|
| **危急** | [#8513](https://github.com/agentscope-ai/QwenPaw/issues/8513) | 具备出站能力的 shell 命令（邮件外泄、HTTP POST、文件到网络）在 `approval_level: AUTO`/SMART 下执行时**没有任何检测发现或审批**——双检测器缺口 | ❌ 暂无 |
| **高** | [#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500) | Auto-Dream 将失败的提取写入检查点；一天记忆丢失且 `success=True`，没有重试或用户可见警告 | ❌ 暂无 |
| **高** | [#8488](https://github.com/agentscope-ai/QwenPaw/issues/8488) | 桌面/PyInstaller 2.3.0-beta.1（Windows）：Visual Compact 从不运行，字形图集未随包发布，每次模型调用都出现 `FileNotFoundError` | ✅ [#8514](https://github.com/agentscope-ai/QwenPaw/pull/8514) |
| **高** | [#8511](https://github.com/agentscope-ai/QwenPaw/issues/8511) | 飞书渠道在处理中收到消息时偶发抛出 `ProviderError: No active model configured`；**在 v2.2.2 可复现，并非 beta 回归** | ❌ 暂无 |
| **中** | [#8505](https://github.com/agentscope-ai/QwenPaw/issues/8505) | 裸 `openai.APIError` 的状态仅存在于文本中 → 被分类为 `unknown`，导致重试/回退失效 | ✅ [#8512](https://github.com/agentscope-ai/QwenPaw/pull/8512) |
| **中** | [#8502](https://github.com/agentscope-ai/QwenPaw/issues/8502) | 桌面 HTML 预览“在浏览器中打开”：CJK 工作区路径 → “找不到文件”；工作区之外的文件 → 点击无反应（Win11、zh-CN、2.3.0b1） | ❌ 暂无 |
| **低** | [#8486](https://github.com/agentscope-ai/QwenPaw/issues/8486) | 工具调用 `< >` 图标在容器左边缘被裁切（缺少水平内边距） | ✅ 今日已关闭 |

**模式：** 三个影响最大的未关闭 bug 中有两个是*静默*的——功能降级或数据消失却不暴露错误。Windows + CJK 区域设置是正在显现的薄弱点（7 项中有 3 项）。今日未报告核心引擎崩溃或数据损坏。

---

## 6. 功能请求与路线图信号

- **桌面审批通知** — [#8504](https://github.com/agentscope-ai/QwenPaw/pull/8504)（XXXL，来自 #8460）：在后台运行时为待审批项发送系统通知，有意在负载中*不*包含工具调用参数。是 **2.3.x** 的有力候选；审批工作流是反复出现的主题，且注重隐私的设计表明它已接近可审查状态。
- **第三方智能体插件** — [#8426](https://github.com/agentscope-ai/QwenPaw/pull/8426)（XXXL）：将第三方智能体架构性抽离到插件系统中。影响范围更大；很可能在 **2.4**。与今日合并的 [#8483](https://github.com/agentscope-ai/QwenPaw/pull/8483) 插件加载加固配套。
- **带双向候选评分的本地 Piccolo 模型** — [#8463](https://github.com/agentscope-ai/QwenPaw/pull/8463)：用于替代原生 Jev 决策（工具审查、ReMe 压缩）的离线方案。释放出**本地优先推理**方向的信号；落地前需要模型负责人审查。
- **社区信息流 + 收件箱** — [#7903](https://github.com/agentscope-ai/QwenPaw/pull/7903)（XXXL，`ready-for-human-review`）：内嵌信息流、分类同步、Platform PKCE 账号关联。要么成为 2.4 的旗舰功能，要么通过功能开关控制。
- **可配置的 Whisper 模型名称** — [#8052](https://github.com/agentscope-ai/QwenPaw/pull/8052)：解除非 OpenAI Whisper 端点（SiliconFlow、本地）的阻塞。小改动、低风险；应尽快发布。
- 较小的用户体验诉求：扩展应用“安装应用”按钮（[#8485](https://github.com/agentscope-ai/QwenPaw/pull/8485)）。

**对下一个 2.3.x 的预测：** #8514、#8512、#8504、#8052、#8496。**对 2.4：** #8426、#7903、#8463。

---

## 7. 用户反馈摘要

**痛点，按重复频率与严重性排序：**

1. **静默降级侵蚀信任。** #8488（Visual Compact 空操作）、#8500（记忆被丢弃却报 `success=True`）和 #8505（重试被静默跳过）是三个子系统中的同一类抱怨：*产品什么都没做却报告成功。* 用户要专门读日志才能发现这一点——beta 需要为降级路径提供可见警告和非零退出语义。
2. **冻结的桌面构建落后于开发构建。** PyInstaller 数据目录缺失（#8488）、插件安装/修复损坏（#8509），以及 HTML 预览中的 CJK 路径处理（#8502），都指向 Windows beta 中打包/区域设置覆盖不足。桌面端正是不满集中之处。
3. **代理/中转推理是一等部署模式。** #8505 和 #8496（摘要模型缓慢、重复的 `max_tokens`/`max_completion_tokens`）表明用户运行的是错误形态并不完全匹配 OpenAI 的 OpenAI 兼容网关——兼容层比新增提供商更重要。
4. **治理值得信任但尚不充分。** #8513 的报告者是在审计而非抱怨，并且发现了 `tool_guard` 在出站 shell 操作上的真实缺口——这是稳定版前需要认真对待的*安全信心*信号。
5. **积极信号：** 24 小时内合并/关闭 11 个 PR，多位首次贡献者（#7896、#6041、#8400），以及用户提交精确、环境信息完整的复现（版本、操作系统、区域设置、工作区形态）——一种成熟的报告文化。

---

## 8. 积压待办观察

需要维护者关注的事项（存在时长和/或缺乏响应）：

- **[#7903](https://github.com/agentscope-ai/QwenPaw/pull/7903) — feat(community)：集成社区与收件箱** · `size/XXXL` · 自 2026-09-20 起为 `ready-for-human-review`（**约 6 周**）。这是单个最大的停滞 PR；一个涉及认证、同步和控制台的社区信息流界面。需要指定审查者，或给出明确的“不早于 2.4”决定，以免贡献者悬而未决。
- **[#8052](https://github.com/agentscope-ai/QwenPaw/pull/8052) — 可配置的 Whisper 模型名称** · 自 2026-09-30 起开放（**约 1 个月**），未见审查活动。小、有用、低风险——一次轻松合并即可缩短“未审查小 PR”队列。
- **[#8067](https://github.com/agentscope-ai/QwenPaw/pull/8067) — 渲染 Markdown 中的 CJK 强调边界** · 自 2026-10-01 起为 `Under Review`。与同样在报告桌面区域设置 bug 的 zh-CN 用户群直接相关；值得与 #8502 中的 CJK 路径工作配套处理。
- **[#8066](https://github.com/agentscope-ai/QwenPaw/pull/8066) — 在格式化前丢弃空媒体块** · 自 2026-10-01 起。防止零字节工具图像导致提供商硬拒绝；与今日的提供商兼容性主题互补。
- **[#8513](https://github.com/agentscope-ai/QwenPaw/issues/8513) — 出站 shell 操作检测器缺口** · **无修复 PR，仅 1 条评论。** 追踪器中严重性最高的未关闭问题；需要在 2.3.0 稳定版之前指派安全负责人。
- **[#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500) — Auto-Dream 记忆丢失** · 无修复 PR。至少需要为稳定版提供“暴露失败而非写入检查点”的缓解措施。
- **流程小问题：** [#8509](https://github.com/agentscope-ai/QwenPaw/pull/8509) 和 [#8485](https://github.com/agentscope-ai/QwenPaw/pull/8485) 提交时 PR 模板未填写（`[Describe what this PR does and why]`），且本数据切片未报告 PR 评论数——两者都增加了本就繁忙的 21 个待处理 PR 队列的分诊成本。

---

**健康度结论：** 吞吐强劲，外部贡献者流水线运转正常；beta 正收敛于基础设施稳定性而非范围扩张。2.3.0 稳定版前需要关注两件事：(a) Visual Compact、Auto-Dream 和提供商重试中的**静默失败语义**；(b) **#8513 中未指派的 `tool_guard`/治理缺口**——这是今日唯一同时具有危急严重性且毫无进展的事项。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目摘要 — 2026-10-31

## 1. 今日概览

ZeroClaw 在 2026-10-30 → 10-31 窗口内以**零集成吞吐**收官：过去 24 小时有 50 个 PR 被更新，但**没有一个被合并或关闭**，且 6 个活跃 issue 全部保持打开、无关闭。因此活动量很大，但完全停留在合并按钮之前——是评审、变基和 CI 空转，而非交付。当日真正的新工作是 2026-10-30 提交的一对 Windows/WSL 安全与环境缺陷（#12133、#12134），每个都已有一个对应的修复 PR（#12135、#12136）处于打开状态——这是一个令人鼓舞的快速周转信号。与此同时，来自一位杰出贡献者（distinguished contributor）的大量 ZeroCode UX 与运行时稳定性队列持续积压老化，其中 2026-10-02 打开的条目仍未合并。**健康度判断：** 贡献者供给强劲、分诊标签有纪律，但存在明显的落地瓶颈；若不处理，将转化为贡献者疲劳。

## 2. 发布

数据集中不存在任何发布（0 个新发布；完全没有“Latest Releases”条目）。这看起来是预发布/持续开发阶段，因此没有变更日志、破坏性变更或迁移面可报告。

## 3. 项目进展

**今日合并/关闭：0 个 PR，0 个 issue。** 在此窗口内没有正式交付任何功能或修复，因此“进展”只能以评审中的推进来衡量：

- **ZeroCode UX 批次（Audacity88）** — 一组规模大且连贯的 UI/会话工作，已暂存但未合并：F5 刷新聚焦会话，不再先取消再恢复（#11457）、对话记录文件路径链接（#11633）、回合中途引导（#11621）、配置删除/重置确认（#11510）、多选别名引用编辑器（#11502）、文件写入差异预览（#11463）、重启后重新打开会话（#11727）。
- **运行时/上下文成本** — #11698（按会话固定人格文件，以阻止提示缓存击穿）、#12044（延迟启动引导段）、#11589（超出成本限制时的操作员覆盖）、#11456（可选的子进程内存看门狗）。
- **通道与提供商** — #11847（原生 Rust XMPP，可选支持旧版 OMEMO）、#11871（MiniMax M3.1-Flash 目录刷新）。
- **安全加固** — #12136（将默认禁止路径扩展到 `/mnt`、`/media`、`/run/media`、Windows 驱动器/UNC）和 #12135（转发 `APPDATA`/`LOCALAPPDATA`），两者均在与各自 issue 同日提交。
- **明确不算进展：** #11882（“Goal V1 proposal 5/12”）自述为草稿切片，“无法独立启用，也未达到可合并状态”，本地验证失败且 Core 批准仍未完成——属于一个由 12 个 PR 组成的依赖型 epic。

**评估：** 流水线已满且按主题组织良好，但单日 50:0 的打开/合并比是评审容量信号，不是速度信号。

## 4. 社区热点

| 项目 | 类型 | 评论数 | 信号 |
|---|---|---|---|
| [#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926) Matrix `send_via` 将 peer 身份当作房间目标 | 缺陷（S2） | 6 | 评论数最多的 issue；因涉及身份/目标语义而讨论密集 |
| [#11703](https://github.com/zeroclaw-labs/zeroclaw/issues/11703) 延迟激活 `tool_search` 会击穿提示缓存 | 缺陷（S3） | 3 | 成本/经济性讨论；仅在 `mcp.deferred_loading = true` 时触发 |
| [#11119](https://github.com/zeroclaw-labs/zeroclaw/issues/11119) 接收方自主决定的会话消息传递跟踪器 | 跟踪器（risk:high） | 0 | 架构面很大，尚无公开讨论 |
| [#12134](https://github.com/zeroclaw-labs/zeroclaw/issues/12134) 默认 `forbidden_paths` 存在缺口 | 缺陷（S1） | 0 | 新提交、安全关键，且已有修复 PR |
| [#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457) ZeroCode 聚焦会话刷新 | PR（size:XL） | 不适用 | ZeroCode 队列中最突出 |
| [#11882](https://github.com/zeroclaw-labs/zeroclaw/pull/11882) Goal V1 监督切片 | PR（草稿） | 不适用 | 在途最大的架构 PR |

**排名说明：** 信息流按“评论数”列出 PR，但对展示的全部 20 个 PR 都返回 `Comments: undefined`，因此无法从这些数据验证 PR 的评论/反应排名；上表中的数字反映的是最近更新的 20 个 PR。所有 Issue 显示 👍：0。

**底层需求：**
1. **通道边界处的语义正确性** — #10926 实质上是多通道抽象中寻址歧义（peer 与 room）的问题；6 条评论的讨论表明，团队仍在协商正确的模型，而不是在修补拼写错误。
2. **Token/成本确定性** — #11703 和 #11698 都源于同一个根本担忧：系统提示中的任何可变内容都会静默使提供商缓存失效。用户优化的是真金白银，而不仅仅是延迟。
3. **假设单一操作系统、单一文件系统的安全默认值** — #12134 暴露了完全自主模式下唯一被查询的拒绝列表在 Linux/Windows/WSL 假设上的缺口。

## 5. 缺陷与稳定性

今日未提交崩溃、panic 报告或明确的回归。按严重程度排序：

| 严重程度 | Issue | 影响 | 是否有修复 PR？ |
|---|---|---|---|
| **S1 — 工作流受阻** | [#12134](https://github.com/zeroclaw-labs/zeroclaw/issues/12134) `default_forbidden_paths()` 遗漏 `/mnt`（WSL 驱动器挂载）、系统盘根目录、`C:\Users`、其他驱动器、UNC 路径 | 在 `workspace_only = false` 时，文件工具可以触及主机挂载卷和非系统卷，而等效的 Linux/Windows 主目录会拒绝这些位置——这是由配置默认值造成的沙箱逃逸 | ✅ [#12136](https://github.com/zeroclaw-labs/zeroclaw/pull/12136)（size:S） |
| **S2 — 降级** | [#12133](https://github.com/zeroclaw-labs/zeroclaw/issues/12133) 三个 Windows 环境变量允许列表不一致；shell/技能/硬件子进程遗漏 `APPDATA`、`LOCALAPPDATA` | `gh`、`npm` 及类似 CLI 在 agent 子进程内表现为未登录/配置错误 | ✅ [#12135](https://github.com/zeroclaw-labs/zeroclaw/pull/12135)（size:XS） |
| **S2 — 降级** | [#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926) `SendViaTool::resolve_target` 将第一个 `external_peers` 条目用作接收方 | Matrix 消息可能被路由到 peer 身份，而本意是房间——存在误投递风险 | ❌ 本数据集中无 |
| **S3 — 轻微（成本）** | [#11703](https://github.com/zeroclaw-labs/zeroclaw/issues/11703) 激活延迟工具会重写系统提示并击穿提示缓存 | 开启延迟 MCP 加载时，每次激活都会产生重复 token 成本 | ⚠️ 仅有相邻修复（[#11698](https://github.com/zeroclaw-labs/zeroclaw/pull/11698) 固定人格文件，属于另一缓存失效来源） |

**进行中的稳定性工作（尚未落地）：** [#11624](https://github.com/zeroclaw-labs/zeroclaw/pull/11624)（对被丢弃的 elicitation 作出应答，而不是让 `ask_user` 在 600 秒后静默超时）、[#11815](https://github.com/zeroclaw-labs/zeroclaw/pull/11815)（将被忽略的选择报告为回答，而不是工具失败）、[#11911](https://github.com/zeroclaw-labs/zeroclaw/pull/11911)（在通道轮次中断时保留已完成的工具结果）、[#11456](https://github.com/zeroclaw-labs/zeroclaw/pull/11456)（子进程内存看门狗）。

**稳定性判断：** 昨天提交的两个 S1/S2 项是唯一有当日修复的项，这是健康的。#10926 自 2026-09-17 起已开启 44 天，没有关联修复，是最令人担忧的未解决正确性缺陷。

## 6. 功能请求与路线图信号

**明确请求 / RFC**
- [#11119](https://github.com/zeroclaw-labs/zeroclaw/issues/11119) — **接收方自主决定的 agent 间会话消息传递**（RFC #11027）的实现跟踪器：在已注册的同别名会话之间由运行时拥有的消息传递。标记为 `risk:high`、`topic:identity-access`、`topic:agent-loop`。这是该项目最清晰的多会话架构押注。
- [#12131](https://github.com/zeroclaw-labs/zeroclaw/issues/12131) — **RFC：共享执行权限与同身份凭据续期**，其动机是任务会接受来自多个已认证贡献者的输入，并生成生命周期超过发起连接的子进程。满足“新安全层”RFC 触发条件。

**体现近期范围的功能型 PR**
- **Goal V1 epic** — #11882 是 12 个切片中的第 5 个，具有明确的依赖切片顺序。预计会经历数周的落地过程，而不是一个点发布。
- **上下文预算** — #12044（可寻址/延迟启动引导段）+ #11698（稳定人格块）构成一个连贯的“更便宜常驻上下文”主题。
- **通道广度** — #11847（原生 Rust XMPP + 可选旧版 OMEMO）、#11871（MiniMax 模型目录刷新）。
- **操作员控制** — #11589（`cost.allow_override` 真正实现，而不是有文档但无效）、#11456（shell 子进程内存上限）。

**预测（基于数据）：**
1. **最有可能接下来落地：** #12135 和 #12136 — 规模小（`XS`/`S`）、与 S2/S1 缺陷的修复关联、单作者端到端、没有架构争论。
2. **可能的捆绑：** ZeroCode UX 集合（#11457、#11621、#11633、#11510、#11502、#11727）在主题上属于同一次评审；预计会成组合并，但 `risk:high`/`size:XL` 成员（#11463）会滞后。
3. **近期最不可能：** #11882（草稿、有依赖、本地验证未通过）和 #11847（XL、`risk:high`、横切通道/密钥/CI）。
4. **关注项：** #11119 尽管标记为 `risk:high`，却有 0 条评论——如此大的跟踪器通常需要维护者设计签核后才会出现切片。

## 7. 用户反馈摘要

**按主题划分的痛点**

| 主题 | 证据 | 用户影响 |
|---|---|---|
| **安全默认值对操作系统缺乏认知** | #12134（S1） | WSL 或 Windows 上的完全自主模式用户是因*默认值*而暴露，并非因错误配置。其表述（“既不覆盖……也不覆盖……”）中有强烈的不满信号。 |
| **Windows 是二等运行时** | #12133、#12135 | 三个不一致的环境变量允许列表意味着 agent 运行的 CLI（`gh`、`npm`）看起来处于登出状态。这是对等性/一致性投诉，而不是新功能请求。 |
| **上下文变动带来的成本不透明** | #11703、#11698、#12044、#11589 | 用户正在为看不见也无法阻止的提示缓存失效付费；`cost.allow_override` 有文档但未接通任何逻辑——这是一次信任打击。 |
| **ZeroCode 会话状态脆弱** | #11457、#11727、#11624、#11815 | 重启后丢失已打开会话，先取消再刷新破坏草稿/队列，被丢弃的提示静默消耗 600 秒超时。 |
| **多通道寻址歧义** | #10926 | 用户无法预测目标会解析为 peer 还是 room。 |

**满意度信号：** 同一报告者提交的当日 issue→修复配对（#12133/#12135、#12134/#12136）表明，贡献者信任流程，愿意自己编写补丁；详细的复现模板（如 `crates/zeroclaw-config/src/policy.rs:479-517` 的文件/行引用、提交 `1c1cd118ac`）表明用户群体在技术上有投入；`distinguished contributor` 标签被积极使用。

**不满风险：** 主要挫败来源不是缺陷数量，而是**评审延迟**。多个 PR 同时带有 `needs-author-action` 和 `needs-maintainer-review`，最旧的已达 29 天且零合并。对于一个有 50 个并发打开 PR 的项目，零合并日会让贡献者觉得“工作进去了，什么也没出来。”

## 8. 积压观察

| 项目 | 时长（截至 2026-10-31） | 为何需要关注 |
|---|---|---|
| [#10926](https://github.com/zeroclaw-labs/zeroclaw/issues/10926) Matrix peer/room 混淆 | 44 天，6 条评论 | 最古老的活跃缺陷，S2 正确性问题（误投递风险），数据集中无关联修复 PR——讨论未收敛 |
| [#11119](https://github.com/zeroclaw-labs/zeroclaw/issues/11119) 会话消息传递跟踪器 | 36 天，0 条评论 | `risk:high` 架构跟踪器，没有可见的维护者参与；下游切片可能被未批准的契约阻塞 |
| [#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457) ZeroCode 会话刷新 | 29 天，size:XL | 生命周期最长的重要 UX PR；陈旧会招致与 ZeroCode 批次其余部分的冲突 |
| [#11463](https://github.com/zeroclaw-labs/zeroclaw/pull/11463) 文件写入差异预览 | 29 天，`risk:high`、`needs-maintainer-review` | 安全相关（渲染文件内容），且明确等待维护者评审 |
| [#11456](https://github.com/zeroclaw-labs/zeroclaw/pull/11456) 子进程内存看门狗 | 29 天，`size:XL`、`needs-maintainer-review` | 资源安全功能；阻塞在评审，而非作者 |
| [#11882](https://github.com/zeroclaw-labs/zeroclaw/pull/11882) Goal V1 切片 5/12 | 12 天，草稿 | 作者表示本地验证未通过 + Core 批准未完成；需要为 epic 做排序决策 |
| [#11871](https://github.com/zeroclaw-labs/zeroclaw/pull/11871) MiniMax 目录刷新 | 12 天，`stale-candidate` | 微不足道的 `size:M` 提供商修复，有搁置过期风险；最便宜的可合并项，用来展示吞吐 |
| [#11703](https://github.com/zeroclaw-labs/zeroclaw/issues/11703) 提示缓存击穿 | 18 天，3 条评论 | 成本缺陷，仅有相邻修复；需要决定 #11698 是否能关闭它，还是需要单独的提示稳定性修复 |

**维护者关注优先级：**（1）合并两个与修复关联的 S1/S2 PR（#12136、#12135），以证明队列在流动；（2）在 #10926 达到 60 天前为其分配负责人；（3）对 #11119 给出明确的接受/延后决定，以免 Goal V1 和会话消息传递轨道建立在未批准的契约上。

---

**数据说明：**“最近 24 小时更新”反映的是修改，而非创建——列出的若干条目是数周前打开的。范围内所有 issue 均为打开状态（0 个关闭），全部 50 个 PR 均为打开状态（0 个合并/关闭），且 PR 评论数返回为 `undefined`，因此 PR 互动排名是根据新近度和范围推断的，而非经过验证的评论量。所有反应计数均为 0。50 个更新的 PR 中只有 20 个包含在信息流中。

</details>