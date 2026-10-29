# OpenClaw 生态日报 2026-10-30

> Issues: 170 | PRs: 500 | 覆盖项目: 5 个 | 生成时间: 2026-10-29 18:48 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [IronClaw](https://github.com/nearai/ironclaw)
- [QwenPaw](https://github.com/agentscope-ai/QwenPaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目摘要 — 2026-10-30

**数据窗口：** 过去 24 小时，截至 2026-10-29。  
**数据说明：** Issue 为按评论数排序的前 50 个；PR 为前 30 个样本。提供的数据中没有 PR 评论数，因此 PR 排名基于提供的排序和标签。

## 1. 今日概览

OpenClaw 正处于发布与分诊的极高活跃阶段：过去 24 小时有 170 个 Issue 和 500 个 PR 得到更新，其中 131 个活跃 Issue 和 291 个开放 PR，同时还有一个补丁版本发布。新版本 [v2026.10.9](https://github.com/openclaw/openclaw/releases/tag/v2026.10.9) 是安全与依赖加固补丁，而不是功能版本。Issue 队列主要由核心可靠性主题主导——会话状态生命周期、崩溃/唤醒恢复、记忆提升、消息丢失和提供商认证——而不是外观类请求。项目正在快速交付安全修复，但多个 P0/P1 可靠性 Issue 仍未关闭且没有关联修复 PR，因此整体健康度可概括为 **高速推进但可靠性风险升高**。

## 2. 发布

### v2026.10.9 — 安全/依赖补丁

发布说明重点介绍了正在修补的运行时依赖漏洞：

- **MCP schema 校验：** `fast-uri 4.2.3` 会拒绝格式错误的 URI scheme 和 host。
- **输入边界：** 过大的 Zod 集合会在 A2UI 和 Discord 嵌入式应用 SDK 中被提前拒绝。
- **IMAP 发件人解析：** 迁移到 `nodemailer 10.1.4`，加强伪造发件人处理。

**破坏性变更：** 发布说明未提及。  
**迁移说明：** 未提及。这似乎是一个可直接替换的补丁版本。  
**建议：** 由于该版本明确以安全为重点，建议升级。

一个发布流程信号：[Issue #187490](https://github.com/openclaw/openclaw/issues/187490) 跟踪 2026.10.9 验证期间观察到的 flaky 测试。发布将其归类为 flaky，但政策要求在 `main` 上并行修复。

## 3. 项目进展

数据集报告过去 24 小时有 **209 个已合并/已关闭 PR 更新**。可见样本只识别出一个已关闭 PR：

- [PR #187819](https://github.com/openclaw/openclaw/pull/187819) — **CLOSED**：“fix: prevent shared-state hangs after service installation drift.” 这解决了服务安装策略变更或被复制时共享状态 worker 准入挂起的问题，包括 Linux 上运行中的系统 Gateway 可能选中一个无关的陈旧用户服务安装的情况。

多个开放 PR 显示在重要领域有活跃工作：

- **模型目录 / thinking profiles：** [PR #187730](https://github.com/openclaw/openclaw/pull/187730)、[PR #187754](https://github.com/openclaw/openclaw/pull/187754)、[PR #187716](https://github.com/openclaw/openclaw/pull/187716) — 堆叠工作，使目录行拥有 thinking profiles，并改进 Kimi、DeepSeek、Mistral 和 Moonshot 模型的推理重放。
- **Discord / Codex 持久化：** [PR #177691](https://github.com/openclaw/openclaw/pull/177691) — 修复 Gateway 重启后 `/codex detach` 和 `/codex bind` 丢失的问题。它带有 P1、兼容性和安全边界合并风险标签，并且仍需要证据。
- **记忆索引韧性：** [PR #187539](https://github.com/openclaw/openclaw/pull/187539) 修复通过同主机 OpenAI 兼容嵌入服务器时 `memory_search` 超时的问题；[PR #187797](https://github.com/openclaw/openclaw/pull/187797) 处理嵌入批处理上限被截断的错误。
- **Codex 恢复：** [PR #187776](https://github.com/openclaw/openclaw/pull/187776) 在后台清理稳定后恢复 Codex 会话。
- **Agent/会话正确性：** [PR #180214](https://github.com/openclaw/openclaw/pull/180214) 在压缩期间保留活动请求来源；[PR #180247](https://github.com/openclaw/openclaw/pull/180247) 保留工具超时结果；[PR #182553](https://github.com/openclaw/openclaw/pull/182553) 和 [PR #187833](https://github.com/openclaw/openclaw/pull/187833) 处理排队消息上下文与溢出摘要；[PR #187527](https://github.com/openclaw/openclaw/pull/187527) 修复子代理完成后父仪表板发布的问题。
- **安全/沙箱：** [PR #187825](https://github.com/openclaw/openclaw/pull/187825) 修复远程 shell 沙箱路径裁剪问题，该问题可能将 `" x.txt"` 解析为 `x.txt`。
- **UI/CLI 打磨：** [PR #187831](https://github.com/openclaw/openclaw/pull/187831) 在原生状态检查期间保留已保存的选择；[PR #187522](https://github.com/openclaw/openclaw/pull/187522) 处理 stdin 读取时的环境取消；[PR #187830](https://github.com/openclaw/openclaw/pull/187830) 将工作区冲突恢复保持在聊天启动之外；[PR #187823](https://github.com/openclaw/openclaw/pull/187823) 允许操作员关闭只读 Gateway 横幅。

## 4. 社区热门话题

### 最活跃的 Issue

| 主题 | 条目 | 信号 |
|---|---|---|
| 记忆召回 / 提升 | [#150635](https://github.com/openclaw/openclaw/issues/150635) — 22 条评论 | 短期召回保留会每晚驱逐已召回条目，因此“dreaming deep phase”永远不会提升。 |
| 记忆提升不一致 | [#164923](https://github.com/openclaw/openclaw/issues/164923) — 19 条评论 | 一个工作区提升 0/512 个候选，而兄弟工作区提升 50–90%。 |
| 崩溃恢复 / 会话状态 | [#166634](https://github.com/openclaw/openclaw/issues/166634) — 18 条评论 | 延迟回收检查点失败会导致 Agent 在崩溃恢复后永久不可用。 |
| 原生主机执行 / 共享状态 | [#177656](https://github.com/openclaw/openclaw/issues/177656) — 17 条评论 | 2026.10.5 上至少有 28 次失败，伴随共享状态完整性准入错误且没有子结果。 |
| 状态生命周期租约争用 | [#159094](https://github.com/openclaw/openclaw/issues/159094) — 14 条评论 | Gateway 拥有租约，但内部 worker 报告另一个进程拥有状态生命周期。 |
| 控制 UI WebChat 抖动 | [#164394](https://github.com/openclaw/openclaw/issues/164394) — 13 条评论 | 滚动长记录时出现连续的微小上下颤动。 |
| 唤醒恢复运行时失败 | [#158592](https://github.com/openclaw/openclaw/issues/158592) — 11 条评论 | 主机睡眠/唤醒后，一个 Agent 的模型运行时发布超时，并且直到重启才恢复。 |

### 最活跃的 PR 主题

PR 评论数不可用，但提供的头部 PR 样本主要由以下内容主导：

- **Discord/Codex 状态持久性：** [PR #177691](https://github.com/openclaw/openclaw/pull/177691)，P1，存在兼容性和安全边界风险。
- **模型目录重构：** [PR #187730](https://github.com/openclaw/openclaw/pull/187730)、[PR #187754](https://github.com/openclaw/openclaw/pull/187754)、[PR #187716](https://github.com/openclaw/openclaw/pull/187716)。
- **记忆索引可靠性：** [PR #187539](https://github.com/openclaw/openclaw/pull/187539)、[PR #187797](https://github.com/openclaw/openclaw/pull/187797)。
- **会话/Agent 正确性与 UX：** [PR #180214](https://github.com/openclaw/openclaw/pull/180214)、[PR #180247](https://github.com/openclaw/openclaw/pull/180247)、[PR #187527](https://github.com/openclaw/openclaw/pull/187527)、[PR #187831](https://github.com/openclaw/openclaw/pull/187831)。

**底层需求：** 用户正在将 OpenClaw 作为持久化、多通道、多 Agent 运行时来运行。社区参与度最高的问题不是功能愿望清单项；它们是对可预测的记忆提升、持久会话状态、可恢复的 Gateway 进程，以及当运行时所有权或提供商认证失效时更清晰诊断的诉求。

## 5. Bug 与稳定性

以下严重性标签来自 Issue 元数据。许多条目并非在过去 24 小时内首次报告，但在该窗口内有活动并得到更新。

### P0 / 发布阻断类

- [Issue #166634](https://github.com/openclaw/openclaw/issues/166634) — **P0**：延迟回收提交检查点失败会导致 Agent 在崩溃恢复后不可用。Agent 会以 `UNAVAILABLE` 永久拒绝 `chat.history`、`chat.metadata`、`models.list` 和进度卡片请求。**未看到关联修复 PR。**
- [Issue #158592](https://github.com/openclaw/openclaw/issues/158592) — **P0**：在 macOS 主机睡眠/唤醒后，准备好的模型运行时发布对一个 Agent 超时；在 Gateway 重启前，每条入站消息都以“runtime owner was not published”失败。**未看到关联修复 PR。**
- [Issue #160762](https://github.com/openclaw/openclaw/issues/160762) — **P0**：`claude-cli` + Telegram 会丢弃在一轮对话中途发送的消息；被排空的提示携带上一条消息的正文。造成消息/数据丢失影响。**未看到关联修复 PR。**
- [Issue #161341](https://github.com/openclaw/openclaw/issues/161341) — **P0**：Codex 认证导入在 Windows 上总是失败，报“The Codex credential reader could not stop”，即使原生 Codex 登录有效。**未看到关联修复 PR。**

### P1 / 高影响稳定性

- [Issue #177656](https://github.com/openclaw/openclaw/issues/177656) — **P1**：原生主机执行返回共享状态完整性准入错误，且没有子结果；在稳定版 2026.10.5 上至少有 28 次失败。**未看到关联修复 PR。**
- [Issue #159094](https://github.com/openclaw/openclaw/issues/159094) — **P1**：Gateway 拥有状态生命周期租约，但内部 worker 报告另一个 OpenClaw 进程拥有它，从而关闭数据库执行准入。**未看到关联修复 PR。**
- [Issue #155396](https://github.com/openclaw/openclaw/issues/155396) — **P1**：普通 Codex 工具轮次可能在最终答案恢复期间因 `provenance_rejected` 而故障关闭，丢失实质性最终答案。**未看到关联修复 PR。**
- [Issue #187579](https://github.com/openclaw/openclaw/issues/187579) — **P1**：Pi500 重启会因重新复制已安装插件依赖而产生约 1.5 GB 的不必要写入，并过早报告就绪。**未看到关联修复 PR。**
- [Issue #187099](https://github.com/openclaw/openclaw/issues/187099) — **P1**：在恢复切换通道上，排队回复从未被回收；诊断以 `keep_lane/active_reply_work` 拒绝，导致仪表板主会话不可用。**未看到关联修复 PR。**

### 安全 / 数据完整性

- [Issue #173058](https://github.com/openclaw/openclaw/issues/173058) — **安全，P2**：`tools.fs.workspaceOnly` 未限制文件工具，因为 Agent 运行时还将 OpenClaw 状态根作为允许的工作目录接收。**未看到关联修复 PR。**
- [Issue #155457](https://github.com/openclaw/openclaw/issues/155457) — **P2**：Anthropic 工具调用在大型编辑时偶尔因格式错误的流式 JSON 参数失败。**未看到关联修复 PR。**
- [Issue #187588](https://github.com/openclaw/openclaw/issues/187588) — **P2**：针对现有本地 PDF 的 Telegram `MEDIA:` 行从未被派发；文本到达，但不发送文档，也不记录错误。**未看到关联修复 PR。**

### 稳定性 / 运维质量

- [Issue #187490](https://github.com/openclaw/openclaw/issues/187490) — **P2**：2026.10.9 发布验证中出现的 flaky 测试；跟踪在 `main` 上并行修复。
- [Issue #164690](https://github.com/openclaw/openclaw/issues/164690) — **P2**：`claude-cli` 运行会为每个 stdio MCP 服务器启动两次；relay/anchor 包装器每个 stdio 子进程消耗约 144 MB，且不可配置。
- [Issue #185092](https://github.com/openclaw/openclaw/issues/185092) — **P2**：Windows 节点已配对，但浏览器控制因监听器所有权/认证错误失败。

**评估：** 多个 P0 Issue 自 9 月底或 10 月初以来一直开放，且仍缺少可见的关联修复 PR。这是主要的项目健康度担忧。相邻领域有有用的修复 PR——共享状态挂起、状态检查、记忆索引、沙箱路径处理和 Codex 恢复——但它们尚未覆盖最高严重性的会话状态和唤醒恢复故障。

## 6. 功能请求与路线图信号

- **长生命周期会话：** [Issue #154482](https://github.com/openclaw/openclaw/issues/154482) 请求为永久 MAIN 会话历史提供受支持的生命周期——按范围导出/裁剪或滚动——因为以连续性为重点的部署无法限制 `transcript_events`。相关：[Issue #112638](https://github.com/openclaw/openclaw/issues/112638) 关于 `session.maintenance` 未能限制存储。
- **团队/多 Agent 组织：** [Issue #153686](https://github.com/openclaw/openclaw/issues/153686) 请求在团队模式下保留每个 Agent 下的命名会话组，而不是扁平化为 pinned/recent。相关的路由隔离问题出现在 [Issue #126533](https://github.com/openclaw/openclaw/issues/126533) 和 [Issue #154739](https://github.com/openclaw/openclaw/issues/154739)。
- **无障碍与 UI 打磨：** [Issue #154524](https://github.com/openclaw/openclaw/issues/154524) 请求将聊天消息暴露为标题以便屏幕阅读器导航；[Issue #167415](https://github.com/openclaw/openclaw/issues/167415) 报告侧边栏行在悬停状态间展开/打开与一键 Archive 交换位置，存在误归档风险。
- **技能学习 / 评估：** [Issue #150250](https://github.com/openclaw/openclaw/issues/150250) 提出一种 Skill Workshop 能力，用于验证普通工作中的学习覆盖率和行为复用。
- **运维 UX：** [PR #187823](https://github.com/openclaw/openclaw/pull/187823) 为只读 Gateway 横幅添加关闭按钮；[Issue #167316](https://github.com/openclaw/openclaw/issues/167316) 报告 Android 反复为未知 Agent `"openclaw"` 查询 `chat.history`。

**对下一版本的预测：** 最强的近期信号是安全/依赖补丁、模型目录和 thinking profile 工作、记忆索引韧性，以及有针对性的状态/UI 修复。更广泛的架构请求——永久 MAIN 会话生命周期、团队模式命名组，以及深度的会话状态租约重设计——除非维护者将其优先作为发布阻断项，否则不太可能在下一个补丁中落地。

## 7. 用户反馈摘要

- **用户依赖连续性。** 长生命周期 MAIN 会话、记忆提升和记录保留是反复出现的关切。当短期召回上限或提升过滤器行为异常时，用户会失去持久个人 Agent 的核心价值（[#150635](https://github.com/openclaw/openclaw/issues/150635)、[#164923](https://github.com/openclaw/openclaw/issues/164923)、[#154482](https://github.com/openclaw/openclaw/issues/154482)）。
- **多 Agent Gateway 是生产工作负载。** 用户报告租约争用、跨会话信封、多 Agent 扇出和工作区特定的提升失败。他们需要隔离和清晰的所有权语义，而不仅仅是配置选项（[#159094](https://github.com/openclaw/openclaw/issues/159094)、[#126533](https://github.com/openclaw/openclaw/issues/126533)、[#154739](https://github.com/openclaw/openclaw/issues/154739)）。
- **通道可靠性很重要。** Telegram、Discord、Matrix 和 Tlon 的 Issue 涵盖消息丢失、媒体未送达、提及门控、引用边界和重启后绑定丢失。这些是生产集成 Bug，而不是边缘场景功能请求（[#160762](https://github.com/openclaw/openclaw/issues/160762)、[#187588](https://github.com/openclaw/openclaw/issues/187588)、[#164065](https://github.com/openclaw/openclaw/issues/164065)、[PR #177691](https://github.com/openclaw/openclaw/pull/177691)、[PR #187778](https://github.com/openclaw/openclaw/pull/187778)）。
- **CLI 支持的提供商路径仍然脆弱。** Codex 和 `claude-cli` 的 Issue 涉及认证导入、OAuth 刷新锁、来源拒绝、格式错误的流式参数、重复 MCP 服务器和模型目录不匹配。用户希望重试、清晰的原因码和平台一致性（[#161341](https://github.com/openclaw/openclaw/issues/161341)、[#156442](https://github.com/openclaw/openclaw/issues/156442)、[#155396](https://github.com/openclaw/openclaw/issues/155396)、[#155457](https://github.com/openclaw/openclaw/issues/155457)、[#164690](https://github.com/openclaw/openclaw/issues/164690)）。
- **满意信号：** 安全补丁活跃，社区参与度高，维护者正在跨模型目录、记忆索引和 UI 进行合并/重构。**不满意信号：** 多个 P0 已开放数周，许多高价值 Issue 带有 `stale` 或 `needs-product-decision` 标签，发布验证仍会遇到 flaky 测试。

## 8. 积压关注

### 长期未响应 / 高影响 Issue

- [Issue #112638](https://github.com/openclaw/openclaw/issues/112638) — 创建于 2026-07-22，P2，stale。`session.maintenance enforce` 模式未限制存储，因为 thread/channel 条目豁免回收。长期数据增长风险。
- [Issue #126533](https://github.com/openclaw/openclaw/issues/126533) — 创建于 2026-08-20，P2，stale。当默认 bot 账户和更具体的绑定同时匹配时，多 Agent 扇出会丢弃或错误路由 `MESSAGE_CREATE`。消息丢失风险。
- [Issue #127195](https://github.com/openclaw/openclaw/issues/127195) — 创建于 2026-08-21，P2，stale。十六个调用点发出相同的“changed while starting work”错误且没有原因码，使生产诊断困难。
- [Issue #150250](https://github.com/openclaw/openclaw/issues/150250) — 创建于 2026-09-16，P3 功能。Skill Workshop 学习覆盖率和行为复用仍是路线图级请求。
- [Issue #153604](https://github.com/openclaw/openclaw/issues/153604) — 创建于 2026-09-20，P2，stale。移除 `config.loadConfig` 会破坏 `wecom-openclaw-plugin` 等第三方插件；没有 shim 或加载时检测。
- [Issue #153706](https://github.com/openclaw/openclaw/issues/153706) — 创建于 2026-09-20，P2，stale。已关闭的 ACP 会话将 `agentRuntime` 投影为 `{id:"codex", source:"implicit"}`，断言它们从未使用的运行时。
- [Issue #154524](https://github.com/openclaw/openclaw/issues/154524) — 创建于 2026-09-21，P2，stale。关于聊天消息屏幕阅读器导航的无障碍请求。
- [Issue #154482](https://github.com/openclaw/openclaw/issues/154482) — 创建于 2026-09-21，P2，stale。永久 MAIN 会话历史生命周期没有受支持的导出/裁剪/滚动路径。

### 需要维护者关注的 PR

- [PR #177691](https://github.com/openclaw/openclaw/pull/177691) — P1，兼容性和安全边界风险，仍为“needs proof”。重要的 Discord/Codex 状态持久性修复。
- [PR #180200](https://github.com/openclaw/openclaw/pull/180200)、[PR #180214](https://github.com/openclaw/openclaw/pull/180214)、[PR #180247](https://github.com/openclaw/openclaw/pull/180247) — 创建于 2026-10-22，标记为可供维护者查看；涵盖 GitHub 重连流程、压缩来源和工具超时结果。
- [PR #182553](https://github.com/openclaw/openclaw/pull/182553) — 创建于 2026-10-24，P1，需要证据。排队消息运行时上下文标记；更窄的后续拆分到 [PR #187833](https://github.com/openclaw/openclaw/pull/187833)。
- [PR #187542](https://github.com/openclaw/openclaw/pull/187542) — dependabot actions-group 更新，等待维护者。低风险维护，但会增加审查队列负载。

**结论：** OpenClaw 高度活跃且对安全响应迅速，在模型目录、记忆索引和 UI 正确性方面有强劲的持续工作。主要风险是未解决的 P0/P1 会话状态、Gateway 恢复和消息投递故障集中出现，其中多个已开放数周且没有关联修复 PR。

---

## 横向生态对比

# 跨项目对比报告 —— 个人 AI 助手 / Agent 开源生态
**日期：** 2026-10-30  
**项目：** OpenClaw、Hermes Agent、IronClaw、QwenPaw、ZeroClaw  
**数据说明：** 各摘要使用的采样窗口以及评论/反应数据的可得性不同。下文的健康评分为分析师定性评分（0–10），并非直接基准测试。IronClaw 在本窗口内无活动。

---

## 1. 生态概览

个人 AI 助手 / Agent 开源生态正处于**高活跃度但高度关注可靠性的阶段**。各项目已不再主要围绕功能新颖性竞争；它们正趋同于持久化多通道运行、会话状态持久化、记忆正确性、提供商/认证韧性以及运行安全。OpenClaw 按吞吐量是规模最大、最活跃的参考点，而 Hermes Agent、QwenPaw 和 ZeroClaw 则占据更窄但技术上各具特色的细分领域。发布节奏并不均衡：只有 OpenClaw 交付了一个补丁，其他项目则在积累修复，等待后续版本切出。生态的主要风险并非贡献量，而是**合并/评审能力以及尚未解决的高严重度可靠性欠账**。

---

## 2. 活跃度对比

| 项目 | Issues（近 24 小时） | PRs（近 24 小时） | 发布状态 | 健康评分 |
|---|---:|---:|---|---:|
| **OpenClaw** | 170 个更新；131 个活跃/开放 | 500 个更新；291 个开放；209 个已合并/关闭 | **v2026.10.9** 安全/依赖补丁；无破坏性变更 | **7.2/10** —— 迭代速度快、安全响应及时，但 P0/P1 可靠性风险偏高 |
| **Hermes Agent** | 17 个更新；17 个开放；0 个关闭 | 50 个更新；37 个开放；13 个已合并/关闭 | 无发布；发布前稳定期低迷 | **6.4/10** —— 吞吐量强，但发布停滞且积压增长 |
| **IronClaw** | 0 | 0 | 无 | **不适用** —— 本窗口内休眠 |
| **QwenPaw** | 13 个更新；9 个关闭 | 41 个更新；27 个开放；14 个已合并/关闭 | 无发布；正在稳定 **2.3.0-beta.1** | **6.8/10** —— 活跃且响应及时，但 beta 版脆弱，且大型 PR 评审受限 |
| **ZeroClaw** | 1 个更新；1 个关闭；0 个活跃开放 | 50 个更新；49 个开放；1 个已合并/关闭 | 无发布；**v0.9.0** 前筹备中 | **5.5/10** —— 管线较深，但合并速度低，作者行动项积压 |

**解读：** OpenClaw 的 PR 更新量约为同类的 **10×**，并且是本窗口内唯一交付发布版本的项目。QwenPaw 在活跃同类中拥有最健康的合并比例，而 ZeroClaw 的评审瓶颈最为明显。

---

## 3. OpenClaw 的定位

**相较同类的优势**
- **规模：** 24 小时内 500 个 PR 更新、209 个已合并/关闭 PR、170 个 Issue 更新 —— 远高于 Hermes、QwenPaw 和 ZeroClaw。
- **发布响应能力：** 在其他项目未发布任何版本时，交付了一个安全/依赖补丁。
- **广度：** 覆盖多 Agent 网关运行、会话状态生命周期、记忆提升、模型目录/思考配置、Discord/Codex 持久化、记忆索引韧性、沙箱以及多种通道适配器。
- **社区引力：** 在此集合中拥有最大的可见贡献者和 Issue 管线；很可能成为持久化 Agent 运行时的实际参考实现。

**技术路线差异**
OpenClaw 是**以网关为中心、运行时较重**的架构。其 Issue 集中在状态生命周期租约、崩溃/唤醒恢复、记忆提升、消息丢失防护以及提供商认证上——也就是持久化多 Agent 运行时最艰难的操作核心。相比之下：
- **Hermes** 更偏向桌面端/消息能力对齐以及安装/更新。
- **QwenPaw** 更偏向控制台/插件/PawApp。
- **ZeroClaw** 更偏向系统层面，围绕事件溯源持久化、Goal Mode 和 ZeroCode TUI。
- **IronClaw** 在本窗口内不活跃。

**社区规模对比**
OpenClaw 的活跃度比同类高一个数量级：PR 更新为 500，而 Hermes/QwenPaw/ZeroClaw 为 41–50；Issue 更新为 170，而后者为 1–17。然而，OpenClaw 也集中了最多未解决的 P0/P1 可靠性 Issue，因此规模并不等同于全面更优的健康度。

---

## 4. 共同技术重点领域

| 需求 | 项目 | 具体需求 |
|---|---|---|
| **持久化会话/状态恢复** | OpenClaw、Hermes、QwenPaw、ZeroClaw | 崩溃/唤醒恢复、租约归属、仅追加事件历史、迁移安全恢复、回滚/回退、重启后持久化绑定 |
| **记忆正确性与可信度** | OpenClaw、QwenPaw、ZeroClaw | 提升/召回淘汰、静默记忆丢失、并发存储安全、召回泄漏、检查点语义、可见遥测 |
| **静默失败可观测性** | Hermes、QwenPaw、ZeroClaw、OpenClaw | 原因码、可见警告、更新回执、超时反馈、仅调试级可见的失败、“success=True”掩盖数据丢失 |
| **通道一致性与可靠性** | OpenClaw、Hermes、QwenPaw、ZeroClaw | Telegram/Slack/Discord/Matrix 一致性、媒体投递、富消息、输入中/状态指示器、提及门控、重启持久化 |
| **提供商/认证/模型路由韧性** | OpenClaw、Hermes、QwenPaw、ZeroClaw | Codex/claude-cli 认证、OAuth 刷新锁、OpenRouter 定价/密钥轮换、思考控制、本地模型发现、模型目录一致性 |
| **安全/沙箱/密钥** | OpenClaw、Hermes、QwenPaw、ZeroClaw | 工作区作用域、密钥脱敏、审批路由、提示注入误报、CLI 密钥掩码、Code Mode 安全 |
| **安装/更新/打包可靠性** | Hermes、QwenPaw、ZeroClaw、OpenClaw | 大小写不敏感文件系统上的 PM 修复、部分克隆处理、更新回执、PyInstaller 资源、插件加载、依赖打补丁 |
| **Agent 循环与成本控制** | QwenPaw、ZeroClaw、Hermes、OpenClaw | 死循环防护、可配置循环中断、成本覆盖、负定价、计费正确性、用量可见性 |

**共同信号：** 用户正把这些系统当作**生产基础设施**，而不是演示项目。最高价值的工作越来越集中在可预测的状态、可观测的失败和安全自动化上，而非新的 UI 界面。

---

## 5. 差异化分析

| 项目 | 功能重点 | 目标用户 | 架构信号 |
|---|---|---|---|
| **OpenClaw** | 持久化多通道、多 Agent 运行时；会话生命周期；记忆提升；模型目录；沙箱 | 高级用户、运维人员、多通道 Agent 部署 | 以网关为中心的运行时，具备状态租约、记忆管线、通道适配器、安全边界 |
| **Hermes Agent** | 桌面端/消息能力对齐、安装/更新可靠性、Slack/Telegram/Discord 命令、技能目录 | 桌面端与无头/远程用户；多配置网关运维人员；Slack 团队 | 桌面客户端 + 网关 + 包/安装管理器 + 技能/插件 |
| **QwenPaw** | 插件生态、Web 控制台、PawApp SDK/控制平面、JEV 安全模式、Auto-Dream 记忆 | 开发者、控制台/中枢管理员、beta 测试者、插件作者 | 插件隔离架构、Console/PawApp 分层、记忆召回管线、提供商集成 |
| **ZeroClaw** | 持久化事件溯源会话、Goal Mode、ZeroCode TUI、成本控制、通道丰富度 | 需要持久性、可审计性、TUI 工作流的运维人员和开发者 | 面向系统的运行时，具备仅追加会话历史、目标生命周期、MCP/服务健壮性 |
| **IronClaw** | 本窗口内无活动 | 未知 | 无法评估 |

**关键差异：** OpenClaw 最广、最“平台化”；Hermes 最偏桌面端/安装运维；QwenPaw 最偏插件/控制台；ZeroClaw 最偏持久性/事件历史。OpenClaw 以广度和规模竞争，而不是单一狭窄工作流。

---

## 6. 社区动能与成熟度

**第一梯队 —— 规模领先者，快速迭代 + 持续交付**
- **OpenClaw：** 活跃度极高，贡献者基础庞大，已交付安全补丁。按规模看成熟度高，但由于未解决的 P0/P1 会话状态与恢复故障，可靠性风险也最高。

**第二梯队 —— 快速迭代者，正在稳定**
- **Hermes Agent：** PR 吞吐量和贡献者多样性较强，但 Issue 关闭数为零且无发布。积压压力以及安装/更新回归是主要拖累。
- **QwenPaw：** 合并速度快，分诊响应及时，但存在 2.3.0-beta.1 回归和大型 PR 评审瓶颈。首次贡献者信号良好。
- **ZeroClaw：** 管线深、路线图阶段划分清晰，但 1 个合并对 49 个开放 PR。评审吞吐量和作者跟进是瓶颈；处于 v0.9.0 前。

**第三梯队 —— 休眠**
- **IronClaw：** 报告窗口内无活动。

**动能解读：** OpenClaw 正以生态领先的规模迭代并交付。QwenPaw 相对其体量迭代最快。Hermes 在积累修复但未发布。ZeroClaw 有架构雄心，但受合并能力制约。

---

## 7. 趋势信号

1. **持久、可回放的状态正在成为基本要求。**  
   OpenClaw 的会话状态故障、ZeroClaw 的仅追加事件历史、Hermes 的迁移/会话恢复缺陷，以及 QwenPaw 的回退/决策持久化需求，都指向同一项要求：Agent 必须能在崩溃、重启、迁移和压缩后继续存活，且不丢失工作。

2. **记忆是信任面，而不是功能勾选项。**  
   静默记忆丢失、提升不一致、召回泄漏和并发写入数据丢失在 OpenClaw、QwenPaw 和 ZeroClaw 中均有出现。开发者应把记忆视为事务性、可观测的子系统，并具备明确的成功/失败语义。

3. **静默失败比显性失败更糟。**  
   Hermes 的 Slack 状态回归、QwenPaw 的“success=True”记忆丢失，以及 ZeroClaw 的 600s 静默等待，都表明用户对 bug 的容忍度高于不可见 bug。原因码、警告和遥测现在已成为产品需求。

4. **多通道一致性是竞争基线。**  
   Telegram、Slack、Discord、Matrix 和 Web 控制台都需要一致的媒体处理、富消息、输入中/状态指示器，以及重启后持久的绑定。通道特定回归是生产阻塞项。

5. **提供商抽象仍然脆弱。**  
   Codex/claude-cli 认证、OAuth 锁、OpenRouter 定价/密钥轮换、思考控制、本地模型发现和模型目录不匹配反复出现。稳健的提供商层需要重试、认证恢复、成本正确性和清晰诊断。

6. **安全控制必须精准，而不是表演式。**  
   沙箱路径逃逸、密钥暴露、审批路由和提示注入误报在所有活跃项目中都有出现。过度拦截普通文本会带来满意度风险；拦截不足则是安全风险。开发者需要经过校准、决策可解释的护栏。

7. **安装/更新/打包是 Agent 产品的一部分。**  
   PM 修复失败、部分克隆、PyInstaller 资源遗漏、插件加载失败，以及更新回执卡在“running”都不是次要问题——它们决定用户能否可靠地运行 Agent。

8. **评审/设计能力是生态瓶颈。**  
   ZeroClaw 单日 49 个开放/1 个关闭 PR，以及 QwenPaw 的 XXXL PR 队列表明，贡献量可能超过维护者带宽。拥有清晰架构决策记录和更小可评审 PR 的项目，将更快把社区动能转化为已交付的可靠性。

**对 AI agent 开发者的结论：** 应围绕**持久状态、可观测记忆、通道一致性、提供商韧性、精准安全以及可靠的安装/更新路径**来构建。功能广度很重要，但在本窗口内，生态的稀缺资源是在持久化、多通道运行下的可信度。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent — 项目摘要
**日期：** 2026-10-30 · **仓库：** [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. 今日概览

Hermes Agent 正处于高吞吐的维护阶段：过去 24 小时内有 50 个 PR 被触及（37 个开放，13 个已合并/关闭），同期有 17 条 Issue 更新——且全部仍处于开放状态。未切发布，因此已合并的工作正在累积，等待下一个版本，而不是已经交付。Issue 流入明显偏向新报告：17 条中有 6 条创建于 2026-10-29，其中若干引用了 v0.22.5 和当前 `main`，这表明近期构建上存在活跃的内部试用。活动量**高**，但信号几乎完全是 bug 修复与加固工作——没有新功能随版本落地，且开放 Issue 积压的增长速度快于关闭速度（今日关闭 0 条）。整体健康度表现为*稳定但承压于积压*，回归明显集中在 Slack 集成、安装/更新路径和 Desktop 会话状态附近。

---

## 2. 发布

**无。** 报告窗口内没有新标签或发布，也没有发布说明可供总结。这是连续第二次表明项目正处于发布前稳定期；13 个已合并/关闭的 PR 已排队进入下一次发布。维护者应预期下一个版本主要由以下内容构成：
- Slack 适配器兼容性修复（slack-sdk ≥ 3.44）
- 安装/更新回执与部分克隆处理
- Desktop 会话恢复与启动路径修正

今日没有破坏性变更或迁移说明需要报告。

---

## 3. 项目进展

窗口内有 13 个 PR 被合并或关闭。可见样本中明确确认关闭的有三个：

| PR | 标题 | 状态 | 信号 |
|---|---|---|---|
| [#110626](https://github.com/NousResearch/hermes-agent/pull/110626) | `fix(redact): mask assignments in secret-bearing file reads` | **已关闭** | 安全加固已交付——`read_file`/`search_files` 现在会对凭据形态路径执行 ENV/JSON/YAML 赋值扫描。完成 #110228 门禁中文件读取这一半。 |
| [#69563](https://github.com/NousResearch/hermes-agent/pull/69563) | `skills(gaming): game 3D asset pipeline — TRELLIS.2 + SkinTokens` | **已关闭** | 已被取代——同一作者以更广泛的三技能布局重新开启为 [#146590](https://github.com/NousResearch/hermes-agent/pull/146590)。表明合并前有意进行了重新设计。 |
| [#146583](https://github.com/NousResearch/hermes-agent/pull/146583) | `docs: official search titles on docs home and install page` | **已关闭** | 仅 SEO/文档润色；无功能影响。 |

**推进中的功能（开放，尚未合并）：**
- **消息平台功能对齐：** [#145831](https://github.com/NousResearch/hermes-agent/pull/145831) 为 Slack/Telegram/Discord 增加 `/project` 斜杠命令，补齐与 Desktop“Move to project”之间的差距。
- **Skills 目录扩展：** 来自 `Jpalmer95` 的三个并行游戏/歌曲创作 Skill PR——[#146590](https://github.com/NousResearch/hermes-agent/pull/146590)（TRELLIS.2 图像转 3D + SkinTokens 绑定）、[#146593](https://github.com/NousResearch/hermes-agent/pull/146593)（puppeteer-animation、视频引导动作）、[#146592](https://github.com/NousResearch/hermes-agent/pull/146592)（歌曲创作套曲弧线）。
- **Gateway 健壮性：** [#146261](https://github.com/NousResearch/hermes-agent/pull/146261) 通过漂移检查将重启风暴制动机制扩展到已安装的 Scheduled Tasks；[#132665](https://github.com/NousResearch/hermes-agent/pull/132665) 为由流水线管理 systemd unit 的部署场景增加 `HERMES_DISABLE_SERVICE_UNIT_REFRESH`。

---

## 4. 社区热点

| 条目 | 互动 | 潜在需求 |
|---|---|---|
| **[#38519](https://github.com/NousResearch/hermes-agent/issues/38519)** — Desktop 仅前端安装（Windows） | **31 👍，22 条评论**，自 2026-06-03 起开放 | 本窗口内点赞数最高的单项。用户在无头/远程机器上运行 agent，希望 Desktop 作为瘦客户端。已开放 5 个月仍无解决，是项目中最明确未满足的架构请求。 |
| **[#110374](https://github.com/NousResearch/hermes-agent/issues/110374)** — Slack 状态在 slack-sdk ≥ 3.44 下静默损坏 | **16 👍，10 条评论** | 核心痛点是静默失败：`invalid_arguments` 按设计只写入 debug 日志，用户看到的是一个失效指示器却没有任何诊断信息。 |
| **Slack 三重复报告集群** — [#112866](https://github.com/NousResearch/hermes-agent/issues/112866)（6 条评论）、[#132594](https://github.com/NousResearch/hermes-agent/issues/132594)（4 条评论，已标记 `duplicate`） | 合计约 10 条评论 | 三名独立报告者在 v0.21.5 Docker 及之后版本中撞上同一个 `agents.sessions.setStatus` 自由文本回归。强证据表明 bug 广泛存在，且修复尚未对用户可见。 |
| **[#143150](https://github.com/NousResearch/hermes-agent/issues/143150)** — Desktop 在多路复用迁移后出现 `storage_unavailable` | 5 条评论 | 多 profile → 单 gateway 迁移后，`state_meta` 中有一条路由未迁移，导致会话恢复失败。需求是迁移路径的可靠性。 |
| **[#135910](https://github.com/NousResearch/hermes-agent/issues/135910)** — `pm repair` 在大小写不敏感文件系统上失败 | P1，4 条评论 | macOS/APFS + Docker bind mount 是主流开发配置；捆绑 terminfo 上的 `Errno 17` 会阻塞*所有*经 PM 路由的操作。 |

**分析：** 社区的注意力分成一个战略诉求（Desktop 仅前端）和一个运维回归集群（Slack）。Slack 集群的处理方式值得注意：它产生了三个独立 Issue 和一个 `duplicate` 标签，而不是单一标准主线程，这分散了 👍 信号，也让优先级判断更难。

---

## 5. Bug 与稳定性

按严重程度与影响范围排序：

**P1 — 安装阻塞项**
- **[#135910](https://github.com/NousResearch/hermes-agent/issues/135910)** · `pm repair` 无法在大小写不敏感文件系统上提交依赖环境。`shutil.copytree` 在捆绑的 CPython terminfo 上因 `Errno 17` 失败；随后所有经 PM 路由的操作都会失败。标记 `sweeper:risk-compatibility`、`os/macos`。**未见修复 PR。**

**P2 — 崩溃与数据访问回归**
- **[#146537](https://github.com/NousResearch/hermes-agent/issues/146537)** · TUI 会话切换器（`Ctrl+X` / `/sessions`）会通过 `shortModel` 中的 `Cannot read properties of null (reading 'replace')` **杀死整个 TUI**，触发条件是某个活动会话行的 model 为 NULL。硬崩溃，提交于 2026-10-29。**未见修复 PR。**
- **[#143150](https://github.com/NousResearch/hermes-agent/issues/143150)** · Desktop 在 `gateway.multiplex_profiles: true` 迁移后无法恢复先前会话 → `storage_unavailable`。阻塞对历史聊天数据的访问。**未见修复 PR。**
- **[#110374](https://github.com/NousResearch/hermes-agent/issues/110374) / [#112866](https://github.com/NousResearch/hermes-agent/issues/112866) / [#132594](https://github.com/NousResearch/hermes-agent/issues/132594)** · Slack 状态/输入指示器在 slack-sdk ≥ 3.44 上静默失效。功能上只是表面问题，但会影响每一轮 Slack 交互。相关开放 PR [#145832](https://github.com/NousResearch/hermes-agent/pull/145832) 修复的是 Slack `display_name` 处理，**并非**此回归。
- **[#137098](https://github.com/NousResearch/hermes-agent/issues/137098)** · 对于 OpenRouter 的路由/可变价格 slug，成本估算会变成**负数**（负价格哨兵值被按面值计价）。这会侵蚀计费信任。相邻 PR [#55855](https://github.com/NousResearch/hermes-agent/pull/55855) 处理的是上游 429 时的 OpenRouter 密钥轮换，而非定价。
- **[#146502](https://github.com/NousResearch/hermes-agent/issues/146502)** · `auxiliary.compression.model` 被忽略——`summary_model_override` 硬编码为 `None`，因此压缩始终使用主模型，并在该模型变慢时卡住。
- **[#146584](https://github.com/NousResearch/hermes-agent/issues/146584)** · Windows Desktop 启动时运行 `hermes gateway ensure` 两次；这次冗余的 2.5 秒调用在 5.0 秒启动中占主导。

**P3 — 正确性与防护行为**
- **[#146586](https://github.com/NousResearch/hermes-agent/issues/146586)** · 当循环前已有 ≥5 个不同行时，`is_runaway_repetition()` 无法截断不含换行的循环——**已有修复 PR：[#146587](https://github.com/NousResearch/hermes-agent/pull/146587)**。
- **[#146582](https://github.com/NousResearch/hermes-agent/issues/146582)** · `execute_code` 生命周期防护会对仅仅*提及* gateway 重启的文档产生误报——而且很容易被拼接绕过。既存在过度拦截，也存在拦截不足。
- **[#146577](https://github.com/NousResearch/hermes-agent/issues/146577)** / **[#146578](https://github.com/NousResearch/hermes-agent/issues/146578)** · 更新成功后，更新回执卡在 `outcome: "running"`（下一次运行会将其视为中断）；部分克隆安装中 `git merge-base` 10 秒超时。两者均属 `area/install-update`，且由同一报告者提交。
- **[#146495](https://github.com/NousResearch/hermes-agent/issues/146495)** · Linux Desktop：新建项目在 Projects 过滤器中默认未勾选。

**安全标记项**
- **[#146564](https://github.com/NousResearch/hermes-agent/issues/146564)** · Kanban worker 必须将受保护写入的审批转交给**已认证的 owner 响应方**；worker 会话对常规审批界面不可见，因此 `AGENTS.md` 一类写入可能卡住，或在 owner 不可见的情况下继续执行。

---

## 6. 功能请求与路线图信号

| 请求 | 下一版本中的可能性 | 理由 |
|---|---|---|
| **Desktop 仅前端安装**（[#38519](https://github.com/NousResearch/hermes-agent/issues/38519)） | **中等** | 需求最高（31 👍），但属架构级改动——需要连接优先的设置流程。已开放五个月、22 条评论，说明是设计讨论，而非忽视。标记 `needs-decision`。 |
| **消息平台上的 `/project`**（[#145831](https://github.com/NousResearch/hermes-agent/pull/145831)） | **高** | PR 已开放、体量小，并填补了 Desktop 与消息平台之间明确的功能对等缺口。 |
| **游戏与创意 Skills 包**（[#146590](https://github.com/NousResearch/hermes-agent/pull/146590)、[#146593](https://github.com/NousResearch/hermes-agent/pull/146593)、[#146592](https://github.com/NousResearch/hermes-agent/pull/146592)） | **高** | 一天内出现三个 PR，其中一个已由关闭的前身重构而来。Skills 为可选启用，合并风险低。 |
| **模型用量插件 / 计费仪表**（[#146581](https://github.com/NousResearch/hermes-agent/pull/146581)） | **中等** | 仅目录新增（固定到 `9962d96`，v1.1.0），合并成本低——但外部插件依赖审查可能拖慢进度。 |
| **`HERMES_DISABLE_SERVICE_UNIT_REFRESH`**（[#132665](https://github.com/NousResearch/hermes-agent/pull/132665)） | **中等** | 标记 `risk-compatibility`；环境变量退出开关通常会被接受，但需要文档。 |
| **成本可见性与计费正确性**（[#137098](https://github.com/NousResearch/hermes-agent/issues/137098)） | **中等** | 负估算问题，加上用量仪表插件，表明用户对支出追踪的关注正在增长。 |

**方向性判断：** 路线图正被拉向两个方向——*深度*（Skills/创意工具、插件目录）与*运营成熟度*（安装/更新可靠性、多 profile 迁移、服务管理）。后者拥有远更多的开放 bug，却没有同等规模的 PR，这是当前队列中的主要失衡。

---

## 7. 用户反馈摘要

**痛点，以用户自己的表述：**
- *“Windows 上的仅前端安装”* — 用户已经手动解决了分布式 agent 问题，希望 Desktop 不再假设自己与 agent 同机部署。这是工作流请求，不是 bug。
- *“静默损坏”* / *“静默消失”* / *“静默失败”* — “静默”一词出现在全部三份 Slack 报告中。用户对故障的容忍度远高于对没有错误暴露面的故障；具体抱怨是协议失败只写入 debug 日志。
- *“任何依赖环境都无法提交”* — 在受影响的文件系统上，P1 的 PM 故障被描述为绝对失败，而非间歇性失败。
- *“更新成功后，更新回执仍停留在 'running'”* — 信任问题：日志说成功，状态却说中断。用户无法判断自己的安装是否可靠。

**满意信号：** 重复贡献者参与度高（`Jpalmer95` 提交了多个 PR，`thisisnotajokee` 在一天内提交了三份精确的安装-更新报告，附带版本哈希与耗时），且 bug 报告详细、可复现——这表明用户群体投入度高、技术能力强，而不是充满挫败感。

**不满意信号：** Slack 回归已持续至少三个版本（v0.21.5 → v0.21.6 → v0.22.5 时代），并产生了重复报告而非解决方案。#38519 请求自六月起开放，有 31 个赞，却无可见决策。两者都在累积善意负债。

**本窗口可见的使用场景画像：** 无头/远程 agent 托管、多 profile gateway、Slack 作为主要界面、macOS/Docker Desktop 开发、Windows Desktop 作为客户端、本地模型（LM Studio/loopback）推理（见 [#135291](https://github.com/NousResearch/hermes-agent/pull/135291)），以及通过 Hugging Face Spaces 进行无需 GPU 的创作工作。

---

## 8. 积压关注

需要维护者关注的条目，按陈旧度 × 影响排序：

1. **[#38519](https://github.com/NousResearch/hermes-agent/issues/38519)** — *已开放 149 天*，22 条评论，31 👍，标记 `needs-decision`。项目内需求最高的条目却没有可见的决策记录。哪怕一条“不做 / 原因如下”的评论，也能把热度转化为信息。
2. **[#135910](https://github.com/NousResearch/hermes-agent/issues/135910)** — *已开放 20 天*，**P1**，`risk-compatibility`，无关联修复 PR。这是本窗口内唯一的 P1，且会在主流的 macOS/Docker 配置上阻塞所有经 PM 路由的操作。
3. **[#99500](https://github.com/NousResearch/hermes-agent/issues/99500)** — *已开放 60 天*，Exa 无密钥轮换环在被掩盖的 429 上始终不前进（“Unrecognized MCP response shape”）。相邻 PR [#146585](https://github.com/NousResearch/hermes-agent/pull/146585) 修复的是*另一处*无密钥 Exa 缺陷（3,000 字符上限），因此轮换环逻辑仍未修复。
4. **[#110374](https://github.com/NousResearch/hermes-agent/issues/110374)** — *已开放 47 天*，16 👍，也是三重复报告集群的标准主线程。需要要么给出修复，要么明确将 [#112866](https://github.com/NousResearch/hermes-agent/issues/112866) 与 [#132594](https://github.com/NousResearch/hermes-agent/issues/132594) 合并到其中。
5. **[#55855](https://github.com/NousResearch/hermes-agent/pull/55855)** — *已开放 122 天*，阻止在上游 429 时轮换健康的 OpenRouter 密钥。分类器逻辑已经存在；这是与 bug #137098 同一 OpenRouter 领域内长期停滞的正确性修复。
6. **[#143150](https://github.com/NousResearch/hermes-agent/issues/143150)** — *已开放 8 天*，`area/sessions` + `area/profiles`。存在时间短但后果严重：用户升级到多路复用网关后会失去对现有会话的访问。随着更多安装升级，迁移 bug 会随时间恶化。
7. **[#69563](https://github.com/NousResearch/hermes-agent/pull/69563)** — 在 99 天后关闭，并立即重新提交为 [#146590](https://github.com/NousResearch/hermes-agent/pull/146590)。值得维护者说明重设计标准是什么，以免替代 PR 重复这一循环。

---

### 健康快照

| 维度 | 读数 |
|---|---|
| 吞吐量 | **强劲** — 每日 50 次 PR 更新，13 个关闭 |
| 发布节奏 | **停滞** — 0 个发布；修复积压持续累积 |
| Issue 关闭率 | **偏弱** — 关闭 0 个，对比 17 个更新 |
| 严重程度分布 | 可见 issue 中 1× P1、约 8× P2、约 6× P3 |
| 贡献者多样性 | **健康** — 作者众多且不同，有重复提交者 |
| 最高风险主题 | 安装/更新与迁移路径（P1 + 4 个 P2/P3 项，修复 PR 很少） |
| 最高需求且未满足的请求 | 仅前端 Desktop（#38519） |

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>QwenPaw</strong> — <a href="https://github.com/agentscope-ai/QwenPaw">agentscope-ai/QwenPaw</a></summary>

# QwenPaw 项目摘要 — 2026-10-30

## 1. 今日概览

QwenPaw 展现出**高频维护活动**：过去 24 小时内更新了 13 个 issue 和 41 个 PR，其中 9 个 issue 关闭、14 个 PR 合并/关闭，仍有 27 个处于开启状态。本周期无新版本发布，但活动高度集中在稳定 **2.3.0-beta.1** 分支上，该版本产生了多份回归报告（插件加载、桌面打包、可选依赖内存占用）。项目还关闭了一个长期悬而未决的 wontfix 决策——关于 agent 死循环（#6116），并落地了安全/CLI 加固（#8492、#8501）。整体健康状况为**活跃但 beta 脆弱**：贡献者吞吐量强劲、问题分诊响应及时，但待审的大型（XL–XXXL）PR 队列持续增长。首次贡献者（#8291、#8400）的出现表明新人上手通道健康。

## 2. 版本发布

本周期无。

## 3. 项目进展

可见窗口内有五个 PR 进入关闭/合并状态，涵盖安全、provider、控制台 UX 和网站基础设施：

- **[#8492](https://github.com/agentscope-ai/QwenPaw/pull/8492)** `fix(security): prevent false-positive approvals for Code Mode in JEV mode` — 收紧工具审查门控，避免 Code Mode 操作被错误地自动批准；与 agent 安全直接相关。
- **[#8497](https://github.com/agentscope-ai/QwenPaw/pull/8497)** `fix(plugins): tolerate import cache refresh failures during plugin loading` — 针对 2.3.0-beta.1 启动失败（#8473）的修复；恢复插件入口点加载。
- **[#8358](https://github.com/agentscope-ai/QwenPaw/pull/8358)** `fix(providers): honor thinking defaults and declared wire controls` — 解决了 Console/后端不一致的问题：`thinking_enabled=off` 未被传递给 OpenAI 兼容 provider。
- **[#5490](https://github.com/agentscope-ai/QwenPaw/pull/5490)** `feat(console): navigable fullscreen image gallery for chat media` — 长期功能（6 月开启）终于关闭；将工具卡片图片包裹在单个 `Image.PreviewGroup` 中以支持画廊导航。
- **[#8253](https://github.com/agentscope-ai/QwenPaw/pull/8253)** `feat(website): add JSON-driven evaluation index` — 双语评估排行榜，含 Pareto 前沿和 SDK 历史。

其他推进中的工作：记忆召回加固（[#8457](https://github.com/agentscope-ai/QwenPaw/pull/8457)、[#7835](https://github.com/agentscope-ai/QwenPaw/pull/7835)）、CLI 密钥掩码（[#8501](https://github.com/agentscope-ai/QwenPaw/pull/8501)）以及 Ollama 模型发现（[#8309](https://github.com/agentscope-ai/QwenPaw/pull/8309)）。

## 4. 社区热点

| 条目 | 活动 | 链接 |
|---|---|---|
| **#6116** 死循环：agent 在单轮中重复相同工具调用 | 9 条评论，**关闭 wontfix** | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/6116) |
| **#8464** 手动 `/compact` 忽略会话级模型切换 | 4 条评论，已关闭 | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/8464) |
| **#8500** Auto-Dream 静默丢弃记忆，仍照常 checkpoint | 2 条评论，**开启** | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/8500) |
| **#8473** 2.3.0-beta.1 中所有后端插件加载失败 | 2 条评论，已关闭（修复：#8497） | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/8473) |

**底层需求分析：**
- **Agent 循环控制**是情绪最激烈的话题（9 条评论）。用户记录了系统介入前约 6 次重复的相同工具调用，浪费 token 和 API 预算。**wontfix** 的处置值得注意——它很可能表明一种设计立场（例如 6 次重复保护被视为“按预期工作”），而非敷衍了事。这可能会以“可配置/更早的循环中断”请求的形式再次出现。
- **会话状态一致性**（#8464）：用户在会话中途切换模型后，期望*所有*操作——包括 compaction——都遵循当前活动模型。根因是 `active_model` 解析读取的是 agent 级配置而非会话上下文。
- **静默数据丢失**（#8500）是信任风险最高的开放议题：`success=True` 的报告掩盖了记忆丢弃，正是这类 bug 会侵蚀用户对自主记忆功能的信心。

## 5. Bug 与稳定性

按严重程度排序（均为 2026-10-29 报告/更新）：

1. **严重 — [#8473](https://github.com/agentscope-ai/QwenPaw/issues/8473)** *2.3.0-beta.1：所有后端插件在启动时加载失败*（报告者主机上 12/12 插件）。根因：`module_isolation.py:220` 中未加保护的 `importlib.invalidate_caches()`，与此前 #8265 根因相同，为新调用点。**已有修复：** [#8497](https://github.com/agentscope-ai/QwenPaw/pull/8497)（已关闭）。
2. **高 — [#8488](https://github.com/agentscope-ai/QwenPaw/issues/8488)** *桌面/PyInstaller 构建遗漏 `visual_compression` 资源* → `FileNotFoundError: atlas-gray-native.ts`；Visual Compact 静默失效，无用户可见警告。2.3.0-beta.1 打包回归。**开启，无关联修复 PR。**
3. **高 — [#8500](https://github.com/agentscope-ai/QwenPaw/issues/8500)** *Auto-Dream 在提取步骤无法解析 agent 回复时静默丢弃整天的记忆*，却仍然 checkpoint 文件导致永不重试。报告 `success=True` 且无遥测。**开启，无关联修复 PR。**
4. **中 — [#8464](https://github.com/agentscope-ai/QwenPaw/issues/8464)** *手动 `/compact` 总是使用 agent 级 `active_model`*，当该模型严格校验 compaction 参数时返回 400 失败。已关闭。
5. **中 — [#8490](https://github.com/agentscope-ai/QwenPaw/issues/8490)** *打开语音转录设置仅仅为了检查可用性，就把 `whisper` 导入服务器进程*（约 690 MB RSS，永不释放）。**开启。**
6. **低 — [#8486](https://github.com/agentscope-ai/QwenPaw/issues/8486)** 工具调用 `<>` 图标左边缘被裁切——容器缺少水平内边距。外观问题。**开启。**

**回归簇：** 四个开放 bug 中有三个（#8488、#8490、#8486）来自 2.3.0-beta.1 时期的构建，表明该 beta 在 GA 前需要一次集中的稳定化冲刺。一个安全相关的加固 PR，[#8501](https://github.com/agentscope-ai/QwenPaw/pull/8501)（在 `env list`/`env set` 中掩码环境变量值），也解决了 CLI 中的明文密钥暴露问题。

## 6. 功能请求与路线图信号

今日关闭的增强类 issue 涵盖 agent 控制和长会话 UX 面：

- **[#6189](https://github.com/agentscope-ai/QwenPaw/issues/6189)** `save_decision()` API — 结构化决策持久化，以在上下文压缩后存活。强烈的框架级诉求（先有鸡还是先有蛋问题：agent 忘记决策*然后*无法归档它们）。
- **[#4356](https://github.com/agentscope-ai/QwenPaw/issues/4356)** 更细粒度的文件/工具守卫 — 只读路径、项目目录白名单，而非仅黑名单。
- **[#4129](https://github.com/agentscope-ai/QwenPaw/issues/4129)** `/rewind` — 回滚文件/上下文以尝试替代提示或撤销 agent 造成的破坏（直接对标 Claude Code 的请求）。
- **[#7740](https://github.com/agentscope-ai/QwenPaw/issues/7740)** Hub 模式管理员密码重置。
- **[#8459](https://github.com/agentscope-ai/QwenPaw/issues/8459)** Web Console 中更便捷地访问未读推送消息。

**对下个版本的预测：** 鉴于 beta 回归负载，下一个即时版本很可能是 **2.3.0-beta.2/GA 稳定化**，而非功能交付。`save_decision` 式**上下文持久性**和 **rewind** 可能在 2.3.x 或 2.4 落地的信号：两者都针对与开放 bug #8500 相同的压缩丢失痛点类别，且项目已在投资相关记忆管道（#8457、#7835）。文件守卫粒度（#4356）与 #8492 中的 JEV/工具审查安全工作天然配对。

## 7. 用户反馈摘要

**今日表达的痛点：**
- *成本/效率：* 死循环（#6116）浪费的 token 和 API 调用——用户希望更早或可配置的循环中断。
- *可预测性：* 会话中途切换模型不被 `/compact` 遵循（#8464），打破了“你选什么就跑什么”的基本心智模型。
- *对自主性的信任：* 静默记忆丢失（#8500）和静默失效（#8488）比 loudly failure 更糟——用户反复要求可见的状态/警告。
- *资源卫生：* 仅仅访问设置页面就产生 690 MB RSS（#8490），在桌面/笔记本部署上很重要。
- *运维基础：* Hub 管理员仍无法重置用户密码（#7740）；密钥在 `env list` 中明文打印（已由 #8501 解决）。

**满意度信号：** 高质量、可复现的 bug 报告（尤其是来自 `feng183043996`，提交了 #6116、#6189、#8500 并撰写了 #8501）以及首次贡献者（#8291、#8400）表明社区参与度高。不满是**beta 质量的摩擦**，而非根本方向问题——若干抱怨是打包/生命周期回归而非架构性反对。

## 8. 待办关注

需要维护者带宽的大型 PR 和长期审查：

| 条目 | 时长 | 规模 | 关注点 |
|---|---|---|---|
| [#7874](https://github.com/agentscope-ai/QwenPaw/pull/7874) `feat(pawapp): redesign SDK and app control plane` | 自 2026-09-19（约 6 周） | **XXXL** | 架构分岔路口；阻塞下游 PawApp 工作。 |
| [#8034](https://github.com/agentscope-ai/QwenPaw/pull/8034) `fix(providers): bound inline media per request` | 自 2026-09-29（约 1 个月） | XL | 真实的网关故障缓解；仍处于 `Under Review`。 |
| [#7835](https://github.com/agentscope-ai/QwenPaw/pull/7835) `fix(memory): stop leaking auto-memory-recall payload to channels` | 自 2026-09-17（约 6 周） | M | 与 #8457 问题空间重复；需要合并决策。 |
| [#8231](https://github.com/agentscope-ai/QwenPaw/pull/8231) `fix(console): persist market install provenance` | 自 2026-10-13 | M | 阻塞第三方插件的可靠“全部更新”。 |
| [#8499](https://github.com/agentscope-ai/QwenPaw/pull/8499) `(WIP) feat(providers): extract local model management into plugin` | 新增 | **XXXL** | WIP；需在设计进一步膨胀前进行设计审查。 |

**建议：** 开放 PR 队列（27 个）偏向超大 diff——#7874、#8489、#8499、#8463、#8034。当前瓶颈是审查吞吐量，而非贡献量。两个记忆召回 PR（#7835、#8457）应协调为单一方向以避免冲突合并。开放 bug #8500（静默记忆丢失）目前**无关联修复 PR**，鉴于其信任影响应优先分诊。

---
*数据窗口：2026-10-29 → 2026-10-30。来源：[agentscope-ai/QwenPaw](https://github.com/agentscope-ai/QwenPaw)。*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目摘要 — 2026-10-30

**仓库：** [github.com/zeroclaw-labs/zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
**数据窗口：** 活动更新于 2026-10-29（过去 24 小时）

> **数据说明：** 所提供数据集将所有条目的每 PR 评论数报告为 `undefined`，且 👍 = 0，因此无法计算“评论最多”/“反应最多”排名。下文各节按*可观察信号*（更新时间、标签权重、严重性、存续时间）排序，并在相关处加以标注。今天唯一已合并/关闭的 PR **不在**所提供的 20 个条目中，因此无法点名。

---

## 1. 今日概览

ZeroClaw 今日呈现明显的**评审受限、合并速度低**态势：24 小时内共 51 次 issue/PR 更新，但仅有 **1 个 PR 已合并/关闭**，而 49 个仍开放——关闭与更新之比约为 1:50。Issue 队列基本清空（1 个更新，0 个仍开放/活跃），当日唯一关闭项是一个文档翻译清理 issue（[#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076)），并非代码变更。PR 构成偏重：**前 20 个中有 11 个（55%）为 `size:XL`**，**3 个带有 `risk:high`**；而 **20 个中有 9 个（45%）处于 `needs-author-action`**，这表明存在作者跟进积压，而不仅仅是维护者评审积压。没有发布版本，且在可见窗口内没有 PR 被标记为已合并——这与 **v0.9.0** 前后的预发布筹备期一致，该版本已作为 release 标签出现在关闭的 issue 上。贡献者集中度显著：**20 个可见 PR 中有 8 个是来自单一作者（Audacity88）的 `zerocode` 范围工作**，其中若干被标记为 `distinguished contributor`。

**活动评估：** 分诊/更新活动高，吞吐量低；流水线深度健康，合并延迟处于警告水平。

---

## 2. 发布

**过去 24 小时没有新发布。** 最新发布列表为空。

仅有前瞻信号：已关闭 issue [#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076) 带有标签 `release:v0.9.0`，同时描述的是对 **v0.8.7** 中引入的目录内容进行修复。这意味着 **v0.9.0 是下一个计划版本**，并且至少部分 v0.8.7 之后的文档修正正被并入其中，而不是进入 v0.8.x 补丁。该数据集未提供破坏性变更或迁移说明。

---

## 3. 项目进展

**今日已合并/关闭：** 1 个 PR（身份未出现在所提供的 top-20 切片中）+ 1 个 issue。

- **[#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076) — 已关闭（docs，release:v0.9.0）** — “发布由完整通读目录发现的 v0.8.7 翻译修复。”范围：`docs/book/po` 目录（`fr`、`ja`、`es`、`zh-CN`），大多数修正在 v0.8.7 新增页面，尤其是 `plugin-release-acceptance.md`。报告为**信息不正确**，1 条评论，提交后约 1 天内关闭（创建于 2026-10-28，更新于 2026-10-29）。仅文档条目，处理迅速。

**可见的进行中功能推进（未合并）：**
- **目标执行生命周期** — [#11881](https://github.com/zeroclaw-labs/zeroclaw/pull/11881)（Goal Mode V1，提案 4/12）已明确分阶段推进，正在等待运行时放置审批。
- **仅追加的会话事件历史** — [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921)，该集合中影响面最大的变更（`risk:high`、`size:XL`，数十个领域标签）。
- **渠道对齐** — Telegram 富消息（[#11862](https://github.com/zeroclaw-labs/zeroclaw/pull/11862)）以及 Telegram/Slack 的推理流式输出（[#11744](https://github.com/zeroclaw-labs/zeroclaw/pull/11744)）继续推进 Matrix → Telegram/Slack 功能迁移。

小结：当日*已完成*的工作是文档维护；当日*活跃*的工作是一个大型、未合并的功能栈。

---

## 4. 社区热点

由于评论/反应数不可用，以下按更新时间 + 标签权重 + 范围列出**信号最强的活跃讨论串**。值得注意的是，**全部 20 个可见 PR 都在 2026-10-29 更新**，这看起来像一次批量分诊/标签清理，而不是各讨论串的自然讨论。

| 条目 | 为何重要 |
|---|---|
| [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921) `feat(session): append-only session event history` | 影响面最大的开放 PR（`risk:high`、`size:XL`，约 60 个领域标签）。重新定义规范会话/执行历史与重放语义——触及每个渠道、提供商和工具。 |
| [#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301) `fix(agents): durable committed-rename recovery across CLI, gateway, RPC` | `priority:p1`、`risk:high`、`size:XL`，已开放 29 天。许多子系统依赖的跨领域持久性修复。 |
| [#11881](https://github.com/zeroclaw-labs/zeroclaw/pull/11881) `feat(goal): accounted Goal execution lifecycle [4/12]` | 编号式多 PR 设计系列——数据集中最清晰的路标产物。受阻于核心运行时放置审批。 |
| [#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004) `fix(memory): markdown store() append-only` | `priority:p1` 数据完整性修复；规模小（`size:M`），但用户影响大。 |
| [#11744](https://github.com/zeroclaw-labs/zeroclaw/pull/11744) / [#11862](https://github.com/zeroclaw-labs/zeroclaw/pull/11862) | 相邻渠道功能（推理流式输出 vs. 富消息），很可能需要在 Telegram/Slack 消息渲染上做共享设计决策。 |

**底层需求：** 热点集合聚为两类需求——(a) **agent 状态的持久性/一致性**（会话、重命名、记忆）以及 (b) **渠道 UX 对齐**，使 Telegram/Slack 与 Matrix 一致。二者都是“让它在规模化时可信”的需求，而不是新增功能面。

---

## 5. 缺陷与稳定性

按严重性/影响排序。注意：这些都不是今天*报告*的；它们是今天更新过的开放修复。

| 严重性 | 条目 | Issue | 是否已有修复 PR？ |
|---|---|---|---|
| **P1 — 数据丢失** | 并发 `MarkdownMemory::store()` 写入执行读-改-重写，可能丢失更新 | `memory:backend` | **是** — [#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004)，`priority:p1`，`needs-maintainer-review` |
| **P1 — 状态滞留** | Agent 重命名在 workspace/memory/cron/ACP/session 状态之前提交配置；部分失败会使状态留在旧别名下，且 CLI 无法恢复 | `release-gate`、`domain:security` | **是** — [#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301)，`priority:p1`，已开放 29 天，`needs-author-action` |
| **P1/P2 — 安全误报** | 提示防护将任何裸 `;` 或 `\|` 标记为命令注入 → 普通文本、表格和工具输出返回 `Suspicious`/`Blocked` | `security`、`runtime` | **是** — [#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068)，`size:XS` |
| **P2 — 挂起/超时** | 已清除的 `ask_user`/`poll` 引导请求会让守护进程等待完整工具超时（`ask_user` 为 600 秒），且没有用户可见信号 | `zerocode` | **是** — [#11624](https://github.com/zeroclaw-labs/zeroclaw/pull/11624) |
| **P2 — 工具损坏** | 在 Android 上，`canonicalize("/system/bin/sh")` 在 SELinux 下失败并返回 `EPERM`，尽管 `execve` 可用 → **每次原生 `shell` 工具调用都失败** | `config` | **是** — [#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/12080)，`size:S` |
| **P2 — 稳定性** | 一次失败的 MCP 恢复会永久毒化连接（`RecoveryBarrier::poison()` 没有清除路径；`health_check()` 仅探测传输层） | `tool:mcp` | **是** — [#12061](https://github.com/zeroclaw-labs/zeroclaw/pull/12061)，`size:S` |
| **P3 — 性能/成本** | 人格文件（`AGENTS.md`、`SOUL.md` 等）在提示重建时重新渲染 → 编辑会击穿提示缓存 | `agent`、`runtime` | **是** — [#11698](https://github.com/zeroclaw-labs/zeroclaw/pull/11698)，`size:XL` |

**解读：** 每个已识别缺陷都已经有开放的修复 PR。约束是评审/合并能力，而不是诊断。三个 `size:XS`/`S` 修复（[#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068)、[#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/12080)、[#12061](https://github.com/zeroclaw-labs/zeroclaw/pull/12061)）是今天可用的成本最低的稳定性收益。

---

## 6. 功能请求与路线图信号

**明确分阶段推进的路线图：**
- **Goal Mode V1** — [#11881](https://github.com/zeroclaw-labs/zeroclaw/pull/11881) 是 12 个提案中的第 4 个，即一个正式计划。其自述为“分阶段基础，而非启用或合并请求”，并以**核心运行时放置审批**为前置门槛。属于多季度工作。
- **仅追加的会话事件历史** — [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921)：重放可重建状态而不重复外部副作用。这是持久化恢复/撤销的架构前提。

**进行中的面向用户请求：**
- **渠道丰富度与透明度：** Telegram 富消息（标题/列表/引用/表格，通过 `channels.telegram.<alias>.rich_messages` 选择启用，默认 **false**）— [#11862](https://github.com/zeroclaw-labs/zeroclaw/pull/11862)；Telegram/Slack 的推理流式输出对齐（`stream_reasoning = off|status|full`）— [#11744](https://github.com/zeroclaw-labs/zeroclaw/pull/11744)。
- **运维控制：** `cost.allow_override` 已有文档，但此前未接入任何逻辑；[#11589](https://github.com/zeroclaw-labs/zeroclaw/pull/11589) 允许运维人员覆盖已超出的成本限制，而无需重启守护进程。
- **ZeroCode UX 集群：** 转录中的消息时间戳（[#11622](https://github.com/zeroclaw-labs/zeroclaw/pull/11622)）、用每窗格会话上限替代硬编码的 8（[#11731](https://github.com/zeroclaw-labs/zeroclaw/pull/11731)）、非取消式刷新（F5）（[#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457)）、会话列表跨重启持久化（[#11727](https://github.com/zeroclaw-labs/zeroclaw/pull/11727)）、可搜索的键位绑定（[#11505](https://github.com/zeroclaw-labs/zeroclaw/pull/11505)）。
- **记忆：** 可选启用的外部重排（[#12036](https://github.com/zeroclaw-labs/zeroclaw/pull/12036)，由例外请求 PR [#12037](https://github.com/zeroclaw-labs/zeroclaw/pull/12037) 引用）。

**对 v0.9.0 的预测：** 很可能发布**小型、范围受控的修复**——文档/翻译修正、命令注入误报修复、Android shell 路径修复、MCP 连接驱逐、webhook 长时间运行超时（[#11931](https://github.com/zeroclaw-labs/zeroclaw/pull/11931)），并可能包括 Markdown 记忆仅追加修复。考虑到今日 0 次合并、`risk:high` 标签以及明确的审批门槛，XL 条目（Goal Mode、会话事件历史、渠道流式输出、提示缓存稳定性）不太可能进入该版本。

---

## 7. 用户反馈摘要

该数据集中没有直接的用户评论（评论数不可用；唯一 issue 有 1 条评论）。痛点只能从 PR/问题陈述中推断，而这些陈述异常明确：

- **对持久化状态的信任**是主导主题。用户遇到的是*静默*失败：并发下记忆写入丢失（[#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004)）、重命名后 CLI“无法恢复”（[#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301)）、每次启动都会忘记已打开会话的侧边栏（[#11727](https://github.com/zeroclaw-labs/zeroclaw/pull/11727)）。
- **静默等待**是反复出现的不满点：已清除的引导请求会导致 600 秒挂起且无 UI 反馈（[#11624](https://github.com/zeroclaw-labs/zeroclaw/pull/11624)）；没有转录时间戳就无法判断事件顺序或持续时间（[#11622](https://github.com/zeroclaw-labs/zeroclaw/pull/11622)）。
- **误报的安全控制**降低日常使用体验——普通文本和工具输出因注入被拦截（[#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068)）。这是满意度风险：误触发的安全功能被报告为阻碍，而非保护。
- **文档漂移**是真实抱怨：v0.8.7 发布的翻译目录包含不正确信息，只有通过完整人工通读才发现（[#12076](https://github.com/zeroclaw-labs/zeroclaw/issues/12076)）。这表明 i18n 发布流程缺少验证关卡。
- **平台广度摩擦：** Android 用户被完全阻断在 shell 工具之外（[#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/11880) → #12080）。
- **满意度信号：** 无可量化信号（所有 👍 = 0）。没有证据表明用户对方向不满；有证据表明用户对可靠性边界情况不满。

---

## 8. 积压观察

存在停滞风险、需要维护者关注的条目：

| 存续时间（截至 2026-10-30） | 条目 | 阻塞因素 |
|---|---|---|
| **29 天** | [#11301](https://github.com/zeroclaw-labs/zeroclaw/pull/11301) — 持久化已提交重命名恢复 | `priority:p1` + `needs-author-action` + `risk:high`；价值最高但未推进的修复。 |
| **28 天** | [#11457](https://github.com/zeroclaw-labs/zeroclaw/pull/11457) — 非取消式会话刷新 | `distinguished contributor`，小型行为修复，没有可见评审者。 |
| **27 天** | [#11505](https://github.com/zeroclaw-labs/zeroclaw/pull/11505) — 设置操作 + 键位绑定过滤器 | `needs-author-action` |
| **23 天** | [#11589](https://github.com/zeroclaw-labs/zeroclaw/pull/11589) — 运维成本限制覆盖 | 有文档但未实现的配置；中等用户价值，XL 范围。 |
| **9 天** | [#11921](https://github.com/zeroclaw-labs/zeroclaw/pull/11921) — 仅追加的会话事件历史 | `risk:high` + `size:XL`；需要架构决策，而不仅仅是评审。 |
| **7 天** | [#12004](https://github.com/zeroclaw-labs/zeroclaw/pull/12004) — 记忆仅追加 | `priority:p1`、`needs-maintainer-review`；廉价修复，P1 影响。 |

**给维护者的流程观察：**
1. **合并吞吐量是瓶颈。** 49 个开放对 1 个关闭，且 45% 为 `needs-author-action`，这表明分诊惯例把 PR 停在作者身上，却没有清晰的重新进入路径。
2. **两个 `docs(runtime)` 例外请求 PR**——[#12063](https://github.com/zeroclaw-labs/zeroclaw/pull/12063)（agent 自有状态退役，引用 #9745/#9647）和 [#12037](https://github.com/zeroclaw-labs/zeroclaw/pull/12037)（外部记忆重排）——表明贡献者在寻求*架构许可*，而不是代码评审。这些是只有维护者才能解除阻塞的治理决策。
3. **ZeroCode 上的单一作者集中度**（8/20 个 PR）是 bus-factor 风险；其中四个带有 `needs-author-action`，如果该贡献者带宽受限，问题可能加剧。
4. **快速修复现已可用：** [#12068](https://github.com/zeroclaw-labs/zeroclaw/pull/12068)、[#12080](https://github.com/zeroclaw-labs/zeroclaw/pull/12080)、[#12061](https://github.com/zeroclaw-labs/zeroclaw/pull/12061) 为 `size:XS`/`S`——一次评审即可清理三个稳定性条目，并把合并速度从谷底拉起来。

</details>