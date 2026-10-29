# AI CLI 工具社区动态日报 2026-10-30

> 生成时间: 2026-10-29 18:48 UTC | 覆盖工具: 7 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/earendil-works/pi)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# 跨工具对比报告 — AI CLI 生态系统
**数据窗口：** 2026-10-29/30 · **来源：** Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、OpenCode、Pi、Qwen Code 的 GitHub 摘要

---

## 1. 生态系统概览

AI CLI 品类已经越过了功能发布阶段，进入**可靠性、治理与成本控制工程**阶段。在全部七款工具中，互动量最高的讨论串不再是关于新能力，而是关于静默失败（挂起、状态被掩盖、状态丢失）、不透明的权限决策，以及提示缓存/上下文经济学。可以看到两种运营模式：**闭源、维护者驱动的内核**（Claude Code、Copilot CLI、Codex），其 PR 吞吐量接近于零或由机器人生成；以及**开放贡献者管道**（Gemini CLI、Qwen Code、OpenCode、Pi），社区 PR 承载了实质性修复。发布节奏与 issue 数量脱钩——OpenCode 和 Qwen Code 在发货，而 Claude Code 和 Gemini CLI 什么都没发——说明发布列车现在由内部 QA 而非社区需求来把关。与此同时，Windows 和 Linux/Wayland 回归问题在七款工具中的五款里主导了平台类投诉，使操作系统间的对等性成为企业推广部署的实际天花板。

---

## 2. 活跃度对比

| 工具 | 24h 内更新的 Issue | 24h 内更新的 PR | Discussions | 发布状态（24h） |
|---|---|---|---|---|
| **Claude Code** | 49 | 2（1 个实质性修复，开放约 7 个月） | 无 | 无 |
| **OpenAI Codex** | n/d | ~50（几乎全部为 `copyberry[bot]`） | 活跃 — Ideas、Q&A、Show & tell（引用约 10 个讨论串） | 2 个 alpha 标签（`0.166.0-alpha.6`、`alpha.5.1.1`），changelog 为空 |
| **Gemini CLI** | 46 | 37 | 无 | 无 |
| **GitHub Copilot CLI** | 38 | 0 | 无 | 无 |
| **OpenCode** | n/d | n/d（≥10 个进行中的显著 PR） | 无 | **2 个稳定版**（`v2.2.2`、`v2.2.1`）+ `process-daemon v0.3.3` |
| **Pi** | n/d（覆盖 10 个） | 10 | 2 个讨论串（1 个 Show & tell，1 个 Q&A） | 无 |
| **Qwen Code** | 3 | 20+（分析了前 20 个） | 无 | **CLI `v0.26.4` + SDK `0.1.26` + Desktop `0.26.4` + nightly** |

*N/A = 源数据中未出现 Discussions 频道；全部七个仓库均启用了 Issues/PR，因此 N/A 表示该频道不存在，而非不活跃。n/d = 摘要中未披露总数；热门 issue/PR 列表是经过筛选的，而非完整列表。*

**看比例，而非总量：**

| 工具 | Issue:PR 比例 | 信号 |
|---|---|---|
| Gemini CLI | 46 : 37（1.2:1） | 健康的双向社区；贡献者在提交代码 |
| Claude Code | 49 : 2（24.5:1） | 维护者分流瓶颈；社区 PR 实际上不构成渠道 |
| Copilot CLI | 38 : 0 | 完全闭源开发 |
| Codex | PR 密集，机器人撰写 | 自动化合并列车；并非社区贡献面 |

**互动深度：** Claude Code #1757（89 条评论 / 77 👍）和 OpenCode #59387（104 条评论）展现了最深的持续性讨论串。Qwen Code 的 #14724（84 条评论，0 👍）是自动化噪音，而非互动——在评估「社区健康度」时值得做出这一区分。

---

## 3. 共同功能方向

六项需求在三个或以上社区中反复出现：

**1. 具有确定性策略和逃生通道的权限系统** — *Claude Code、Codex、Gemini CLI、Copilot CLI、OpenCode*
- Codex：`decision = "prompt-user"` 托管检查点（#58045），强制人工审批，独立于已保存的审批。
- Copilot CLI：非交互模式下的默认拒绝 + 显式允许列表（#5275）；`--deny-tool` 当前始终覆盖 `--allow-tool`。
- Gemini CLI：`security.allowCommandSubstitution` 需显式启用（#30029）；劝阻破坏性 `git reset --force`（#22672）。
- Claude Code：不可覆盖的 PowerShell 防护误报（#73524）——正是其他所有工具都在修复的反模式。
- OpenCode：`external_directory` 对文件工具已强制执行，但**可通过 shell 绕过**（#56288），tree-sitter 移除 PR（#60332）作为结构性修复。
> **共同需求：** 安全默认值*加上*显式、有文档的覆盖机制——以及命令被阻止时的机器可读原因（Copilot #56722：「blocked by policy」但未标识具体规则）。

**2. 智能体/子智能体的可观测性与控制权** — *Claude Code、Codex、Gemini CLI、Copilot CLI*
- Claude Code：桌面面板移除了每智能体的 token/工具/模型指标（#105831）；子智能体通知刷屏污染父上下文（#105928）；未文档化的 Agent 工具抑制（#80988）。
- Gemini CLI：通过 `/chat share` 暴露子智能体轨迹（#22598）；`/bug` 报告中包含子智能体上下文（#21763）。
- Codex：Guardian 对注入命令的审查（#58119），持久化父子关系（#58129）。
- Copilot CLI：`includeCoAuthoredBy: false` 未被子智能体继承（#4576）。
> **共同需求：**「用户希望成为委派行为的权威，并看到子智能体实际做了什么。」

**3. 上下文预算、记忆保真度与提示缓存稳定性** — *Claude Code、Codex、OpenCode、Pi、Qwen Code*
- Claude Code：硬编码的 200 行/25KB 记忆窗口（#91188）；**当仅加载索引行时，测得遵循度从约 95% → 约 72%**（#105867）。
- Pi：动态工具排序重新计费整个对话（#10024、#11529）；Anthropic 服务端消息线程仅发送新消息（#11545）。
- Qwen Code：面向慢预填充自托管模型的不可变上下文模式（#14215）。
- Codex：`codex.additional_context` 计数/字节/截断指标（#58144）；更便宜的模型用于记忆维护（#58091）。
- OpenCode：`/compact` 未做上下文适配检查（#46164）。
> **共同需求：** 确定性上下文组装、可见的截断成本、前缀缓存保持。

**4. Windows（及 Linux/Wayland）平台对等性** — *Claude Code、Codex、Gemini CLI、Copilot CLI、Pi*
- Codex：沙箱完全无法派生命令（HRESULT `0x80070020`，#55230）——数据集中最严重的单一阻塞项。
- Claude Code：Windows 提示建议回归（#102208）、插件路径不匹配（#105945）、无头 Chrome 导致 IdP 锁定（#106003）。
- Gemini CLI：Wayland 浏览器子智能体失败却报告 `GOAL` 成功（#21983）；Windows 上 `fs.stat dev: 0` 破坏了所有安全文件读取（#30033）。
- Copilot CLI：Windows Entra broker 令牌缓存（#5236）。
- Pi：Windows/Zellij 滚轮滚动的是历史而非转录（#9656）。
> **共同需求：** 平台对等性是企业的准入门槛；Windows 报告特别集中在认证和沙箱路径解析上。

**5. 凭据/密钥处理作为一等原语** — *Claude Code、Codex、Copilot CLI、Pi*
- Codex #58148：密钥管理应作为核心能力，而非委托给 shell 约定——由基础设施/部署/生产用例驱动。
- Copilot CLI：keychain/密钥存储故障跨 Ubuntu（`secret-tool`，22 👍）、macOS（XARA 分区）、Windows（Entra broker）。
- Claude Code：`/feedback` 默认提交转录，泄露密钥（#93138）。
- Pi：摘要的 OAuth 凭据解析（#11556）；每请求 Bedrock 客户端抖动（#11527）。

**6. 成本与配额透明度** — *OpenCode、Copilot CLI、Codex、Claude Code*
- OpenCode：隐藏的标题/摘要 LLM 调用被计费但未出现在会话成本中（#46371）；104 条评论的免费层级大讨论串（#59387）。
- Copilot CLI：PRU 配额因功能开关而被耗尽（#4802）；354K token 的急切注入 MCP schema（+成本，#4613）。
- Codex：可预测的月度用量重置（#57967）；更便宜的记忆模型（#58091）。
- Claude Code：小团队的跨账户池化用量（#92517）。

---

## 4. 差异化分析

| 工具 | 侧重点 | 目标用户 | 技术路线 |
|---|---|---|---|
| **Claude Code** | 深度交互式开发会话；记忆/提示权威透明度 | 长期维护仓库的个体开发者与团队 | 闭源内核，hook/插件扩展，激进的自动记忆 + 智能体工具默认值；issue 面远超 PR 面 |
| **OpenAI Codex** | 面向自主执行的政策基础设施 | 平台/企业团队、智能体构建者 | Rust CLI + 桌面 + IDE；Guardian 审查、托管审批检查点、工作区路由的 Web 搜索；alpha 列车由机器人撰写 PR |
| **Gemini CLI** | 智能体编排架构 | OSS 贡献者、拥有大量 MCP 服务器的高级用户 | 贡献者密集；AST 感知代码智能（tilth/glyph/ast-grep）、OS 级沙箱、子智能体评估策略 |
| **Copilot CLI** | GitHub/企业身份 + ACP 互操作性 | GitHub Enterprise 组织、第三方 ACP 客户端（GitKraken） | 闭源；以 ACP 作为集成契约；权益映射 bug 是反复出现的故障模式 |
| **OpenCode** | 产品迭代速度 + 自动化原语 | 构建者、自托管者、成本敏感团队 | 最快的发布节奏；`/goal` 目标循环、Code Mode 调度条件、默认图像生成、MDM 组织策略 |
| **Pi** | 极简、供应商无关的无头内核 | 扩展作者、多供应商/BYOK 用户 | 小表面积（智能体循环 + 7 个工具 + JSONL 会话）；对提示缓存和供应商怪癖极度关注正确性 |
| **Qwen Code** | 自托管模型经济学 + 托管服务 | 自托管/本地部署、守护进程工作流 | 托管 Agent Server（Maven 模块）、混合 `tools.mode`（direct/code_mode）、大量 CI 投入 |

**显著分歧：**
- **PR 吞吐量**是最鲜明的结构性分界线：Gemini CLI（37）和 Qwen Code（20+）将社区代码视为交付机制；Claude Code（2）和 Copilot CLI（0）则不然。
- **记忆策略**：Claude Code 押注自动记忆 + 硬编码预算（并因不透明而受到惩罚）；Pi/Qwen 将上下文视为一个可以变得确定性的会计问题。
- **安全姿态**：Codex 在*增加*人工检查点和审查基础设施；Gemini/OpenCode 在*增加*现有阻断的可配置关闭开关。两者殊途同归——没有解释的硬编码拒绝就是故障模式。
- **变现摩擦**仅在 OpenCode（免费层级/配额大讨论串，付费用户在「无限」模型上被阻止）和 Copilot CLI（PRU 核算）中显性化；其他工具将其抽象为计划权益。

---

## 5. 社区动能与成熟度

**第一梯队 — 高体量、高互动**
- **Claude Code**：绝对讨论量最大（49 个 issue；置顶讨论串 89 条评论/77 👍），但**存在结构性瓶颈**——仅 2 个 PR 更新，其中一个实质性修复开放约 7 个月。成熟产品，不成熟的贡献渠道。对于*用户关心什么*信噪比最好；对于*响应能力*最差。
- **Gemini CLI**：集合中健康度最均衡——46 个 issue / 37 个 PR，PR 修复了高影响面 bug（重试时工具重复执行 #30020、`/restore` 删除被忽略文件 #30034、`$` 模式提示损坏 #30035）。注意：团队自身的评估层仍不稳定（#23166、#23313），因此质量声明尚无法独立验证。

**第二梯队 — 强劲速度、较窄社区**
- **OpenCode**：最快的发货节奏——24 小时内两个稳定版本加一个 pty 守护进程。工程质量高（权限扫描器重构、TLS 信任、MDM 策略），但免费层级/速率限制的不透明是社区最响亮的投诉。动能高；信任是悬而未决的问题。
- **OpenAI Codex**：投入巨大，社区声音极小。24 小时内约 50 个 PR，全部由机器人撰写——这是内部工程消防水管，不是社区。发布卫生薄弱（两个 alpha 标签，无 changelog）。将这里的 PR 计数视为*维护者活跃度*，而非生态系统健康度。
- **Qwen Code**：CLI+SDK+Desktop 协同发布列车。但最高「issue」是机器人噪音（#14724，84 条评论，0 👍），2 个自动修复运行卡在 `queued` 状态，前 20 个 PR 中有 8+ 个是 CI 修复。**在基础设施上快速迭代，而非产品**——v0.26.4 中只有一个净新增用户功能（主题继承）。

**第三梯队 — 小而高信号**
- **Pi**：体量最低，每 issue 技术质量最高。量化的故障报告（40 万条目下密钥延迟 14×，p50 1.5ms→21ms；37.3 GiB 等效内存画像；8 MB 会话文件下 V8 OOM）。社区主导的 Rust 移植（#11503）表明真正的架构信心。供应商兼容性问题的最佳早期预警系统。

**第四梯队 — 停滞的贡献者面**
- **GitHub Copilot CLI**：38 个 issue 更新，**0 个 PR**，旗舰权益 bug（#552）自 **2025 年 11 月**开放至今，31 条评论，未解决。影响企业的故障（三个操作系统上的 keychain、37 GiB 进程增长）表明回归覆盖落后于发布节奏（版本跨度从 `0.0.355` → `1.0.105`）。对于依赖组织的工作流，是本集合中风险最高的。

---

## 6. 趋势信号

**1. 智能体状态语义正在成为硬性要求。**
Gemini CLI 将 `MAX_TURNS` 报告为 `GOAL` 成功（#22323），将 Wayland 上的浏览器子智能体失败报告为 `GOAL` 成功（#21983）；Claude Code 的 Remote Control 403 没有会话内恢复（#91717）；OpenCode 会话挂起在「Working」状态且无错误（#58786、#60330）。**含义：** 如果你今天基于智能体状态做 CI 分支，你会发布假阳性。在自动化之前验证状态契约，并将「成功」视为未经独立证据验证。

**2. 权限模型现在是产品面，而非安全复选框。**
Codex 托管检查点、Copilot 允许列表请求、Gemini 的 `allowCommandSubstitution`、OpenCode 的 shell 绕过修复——殊途同归。差异化因素不再是*是否*阻止，而是阻止是否**被解释、可覆盖、跨界面一致**。Copilot CLI 的逐字故障（「blocked by policy」，无规则、无恢复）是设计时要规避的模板。

**3. 提示缓存已成为损益表项目。**
Pi 将其量化：动态工具排序和系统提示头部移动会静默地重新计费整个对话（#10024、#11529）。Claude Code 量化了另一面：截断下指令遵循度从 95%→72% 崩溃（#105867）。**含义：** 将上下文组装的确定性作为一等选择标准；在承诺长时间会话之前，向供应商索取缓存命中和截断遥测数据。

**4. ACP 和 MCP 正在固化为真正的集成契约。**
Copilot CLI 的 ACP 请求现在由具名第三方集成商提交（会话中期 contextTier、`ask_user`、非破坏性 `session/prompt`）。MCP 成熟度问题是普遍的——Gemini 的 128 工具硬上限（#24246）、Copilot 的 354K 急切 schema token（#4613）、OpenCode 的每服务器 TLS 信任（#60039）、Pi 的 `tool_search` 命名空间（#11558）。**含义：** 协议对等性正在成为构建在这些 CLI 之上的团队的采购标准。

**5. 本地资源管理是一个所有权不足的问题。**
OpenCode 的 `event` 表达到 13 GB（#33356）、37 GiB Copilot CLI 进程（#5254）、Pi 中的 V8 OOM（#11570）、孤儿 MCP 子进程（#46035、#46253）。每个工具都将失控的本地状态视为 bug，而非有界子系统。**含义：** 在任何长时间运行的部署中规划磁盘/进程护栏和定期状态修剪。

**6. 平台对等性是企业采用的门槛——而 Windows 正在失利。**
七款工具中有五款报告 Windows 优先的问题簇，集中在沙箱执行、路径解析和 OS 身份集成。Codex 的 #55230（沙箱无法派生命令）和 Claude Code 的 #106003（无头 Chrome 锁定 IdP 账户）是推广阻塞项，而非小烦恼。

**7. 发布和 CI 自动化正在产生更多噪音而非信号。**
Qwen Code 的 84 条评论机器人 issue、卡住的自动修复运行、取消运行的假阳性（#15852）、占位 changelog；Codex 的仅版本号 alpha 说明；Copilot 跨小版本的回归抖动。**含义：** 不要在这个群体中按字面消费发布说明——固定版本、刻意二分、直接跟踪 issue tracker。

---

### 给技术决策者的实用指南

| 如果你的优先事项是…… | 倾向于 | 因为 |
|---|---|---|
| 最广泛的生态系统信号与功能发现 | **Claude Code** | 互动量最高的 tracker；每个主要主题都首先在这里出现 |
| 可审计的自主执行 | **OpenAI Codex** | 唯一发布托管人工审批检查点的工具（Guardian、`prompt-user`） |
| 贡献修复并使其合并 | **Gemini CLI** | 1.2:1 的 issue:PR 比例；实质性正确性 PR 能落地 |
| 快速演进的产品能力 | **OpenCode** | 24 小时内两个稳定版本；`/goal` 循环、Code Mode 调度 |
| 多供应商 / BYOK 正确性 | **Pi** | 唯一发布量化缓存和供应商怪癖分析的社区 |
| 本地部署 / 自托管模型经济学 | **Qwen Code** | 不可变上下文路线图明确针对慢预填充 |
| GitHub Enterprise 身份集成 | **Copilot CLI** — 需谨慎 | 原生 GHE/Entra 路径，但存在未解决的权益和 keychain 缺陷 |

**在任何评估中都要牢记的两个注意事项：**（1）Codex 和 Qwen Code 中的 issue 和 PR 很大程度上是自动化生成的——原始计数不是社区健康度指标；（2）在每款工具中，最具破坏性的缺陷类别是*静默*的那一类（成功被掩盖、会话绑定丢失、无错误挂起），因此在试用期间，应将可观测性和错误暴露的权重置于功能清单之上。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区亮点 — 截至 2026-10-30

> 注：提供的数据集未包含 PR 评论数。以下排名遵循给定的按评论排序顺序，并将最近更新时间、范围和影响作为次级关注信号。所有上榜 PR 均为 **OPEN**。

## 1. 热门 Skills 排名

1. **mcp-builder：MCP v2 兼容性修复 — PR #1742**  
   [github.com/anthropics/skills/pull/1742](https://github.com/anthropics/skills/pull/1742)  
   为 `mcp>=2.0.0` 更新 `mcp-builder`，包括 `streamable_http_client` 重命名，以及通过 `create_mcp_http_client` / `http_client` 处理自定义请求头。对生态兼容性影响较大。**状态：OPEN。**

2. **skill-creator：trigger-eval 可靠性 — PR #1298**  
   [github.com/anthropics/skills/pull/1298](https://github.com/anthropics/skills/pull/1298)  
   隔离 trigger 评估，并修复可能导致漏判或无效评分的 Windows/运行时故障。解决 Skill 编写可靠性的核心问题。**状态：OPEN。**

3. **Notion spec-to-implementation + quantitative-resume-auditor — PR #1245**  
   [github.com/anthropics/skills/pull/1245](https://github.com/anthropics/skills/pull/1245)  
   新增两个 Skills：一个将产品/技术规格转换为 Notion 实现任务；另一个审计量化简历。提交周期较长，近期有更新。**状态：OPEN。**

4. **proofcore-contract-auditor — PR #1771**  
   [github.com/anthropics/skills/pull/1771](https://github.com/anthropics/skills/pull/1771)  
   用于对 Solidity/Rust 智能合约进行静态分析，并在 TON 上锚定密码学审计证明的 Web3 Skill。领域较窄，但范围清晰。**状态：OPEN。**

5. **DOCX 孤立批注检测 — PR #1734**  
   [github.com/anthropics/skills/pull/1734](https://github.com/anthropics/skills/pull/1734)  
   标题表明要检测 DOCX 文件中的孤立批注；PR 摘要为空，因此范围由标题推断。属于文档质量自动化主题。**状态：OPEN。**

6. **md2video-audio — PR #1703**  
   [github.com/anthropics/skills/pull/1703](https://github.com/anthropics/skills/pull/1703)  
   通过 Marp 及相关工具将 Markdown 文档转换为带配音的 MP4 视频。体现了对媒体生成 Skills 的需求。**状态：OPEN。**

7. **webapp-testing：移除 `shell=True` 风险 — PR #1980**  
   [github.com/anthropics/skills/pull/1980](https://github.com/anthropics/skills/pull/1980)  
   替换 `with_server.py` 中不安全的 `subprocess.Popen(..., shell=True)` 用法，解决命令注入风险（CWE-78）。与安全相关，且近期有更新。**状态：OPEN。**

8. **docx：LibreOffice 超时/错误验证 — PR #1792**  
   [github.com/anthropics/skills/pull/1792](https://github.com/anthropics/skills/pull/1792)  
   使 `accept_changes.py` 将 LibreOffice 超时报告为错误，并在声称成功前验证修订标记确实已移除。**状态：OPEN。**

## 2. 社区需求趋势

- **信任、安全与命名空间治理** — Issue [#492](https://github.com/anthropics/skills/issues/492) 是讨论热度最高的话题：以 `anthropic/` 命名空间分发的社区 Skills 会带来冒充与信任边界风险。  
- **组织范围内的 Skill 共享与分发** — Issue [#228](https://github.com/anthropics/skills/issues/228) 希望提供共享 Skill 库或直接分享链接，而不是手动交换 `.skill` 文件。  
- **可靠的 Skill 触发与评估** — Issue [#556](https://github.com/anthropics/skills/issues/556) 报告 `run_eval.py` / `claude -p` 从未触发 Skills，表明需要可靠的评估基础设施。  
- **Agent 记忆与上下文效率** — Issue [#1329](https://github.com/anthropics/skills/issues/1329) 提出 `compact-memory`，一种用符号记法压缩长时间运行 Agent 状态的 Skill。  
- **Skill 编写质量与元数据** — Issue [#202](https://github.com/anthropics/skills/issues/202) 和 [#2064](https://github.com/anthropics/skills/issues/2064) 关注最佳实践、token 效率，以及说明何时使用某个 Skill 的描述。  
- **Agent 治理与质量门禁** — Issue [#412](https://github.com/anthropics/skills/issues/412) 和 [#1385](https://github.com/anthropics/skills/issues/1385) 提出治理模式、对抗性审查和交付验证流水线。  
- **插件/包整洁性** — Issue [#189](https://github.com/anthropics/skills/issues/189) 指出 `document-skills` 与 `example-skills` 中存在重复 Skills，导致上下文窗口重复。  
- **文档/办公自动化健壮性** — Issue [#2018](https://github.com/anthropics/skills/issues/2018) 和 [#1868](https://github.com/anthropics/skills/issues/1868) 表明，对正确的 DOCX XML 处理和图形工具仍有持续需求。

## 3. 高潜力待处理 Skills

以下均当前为 **OPEN**，因近期更新和实际影响入选：

- **PR #1980 — webapp-testing 安全加固**  
  [github.com/anthropics/skills/pull/1980](https://github.com/anthropics/skills/pull/1980)  
  移除命令注入攻击向量；更新于 2026-10-25。

- **PR #1742 — mcp-builder 的 MCP v2 兼容性**  
  [github.com/anthropics/skills/pull/1742](https://github.com/anthropics/skills/pull/1742)  
  对使用较新 MCP 版本的用户很重要；更新于 2026-10-08。

- **PR #1245 — Notion spec + resume auditor Skills**  
  [github.com/anthropics/skills/pull/1245](https://github.com/anthropics/skills/pull/1245)  
  实质性的新 Skill 提交；更新于 2026-10-15。

- **PR #1681 — skill-creator 直接执行支持**  
  [github.com/anthropics/skills/pull/1681](https://github.com/anthropics/skills/pull/1681)  
  修复 `package_skill.py` 独立执行及过时的使用路径；更新于 2026-10-24。

- **PR #1997 — skill-creator 的 YAML frontmatter 解析**  
  [github.com/anthropics/skills/pull/1997](https://github.com/anthropics/skills/pull/1997)  
  修复评估/描述优化中的元数据损坏；更新于 2026-10-19。

- **PR #1975 — pptx `--cols` 验证**  
  [github.com/anthropics/skills/pull/1975](https://github.com/anthropics/skills/pull/1975)  
  小而用户可见的 CLI 修复；更新于 2026-10-27。

- **PR #1730 — claude-api 失效 URL 替换**  
  [github.com/anthropics/skills/pull/1730](https://github.com/anthropics/skills/pull/1730)  
  文档可靠性修复，替换 URL 已验证；更新于 2026-10-04。

## 4. Skills 生态洞察

**社区最集中的需求并不是简单地要更多 Skills，而是可信、可靠、可共享且治理良好的 Skills — 尤其是在命名空间安全、触发/评估正确性、编写质量，以及稳健的文档/工具集成方面。**

---

# Claude Code 社区简报 — 2026-10-30

## 1. 今日亮点
过去 24 小时内没有新版本发布，但 issue 活跃度依然很高（共 49 个 issue 有更新）。长期存在的认证投诉（#1757）仍是最热讨论帖，共 89 条评论 / 77 个 👍；而新提交的记忆保真度报告（#105867）和 *heron_brook* Agent 工具抑制 bug（#80988）则让提示词/Agent 控制透明度继续成为讨论焦点。平台特定的回归问题——Windows 上 hook/插件失效，以及无头 Chrome 触发 IdP 账户锁定——是增长最快的新报告类别。

## 2. 版本发布
过去 24 小时内无新版本。

## 3. 热门 Issue

1. **[#1757](https://github.com/anthropics/claude-code/issues/1757) — Claude Code 要求用户频繁重新登录**（89 条评论，77 👍）
   仍是追踪器中参与度最高的未修复 bug。用户报告几乎每天都被迫重新进行 Web 身份验证。讨论量和持续时间（自 2025 年 6 月起一直处于打开状态）使其成为最明确的信号：会话持久性是一个顶级的可靠性缺口。

2. **[#80988](https://github.com/anthropics/claude-code/issues/80988) — `heron_brook` 提示词片段仅对 Opus 5 禁用 Agent 工具调度**（38 条评论，72 👍）
   一个带版本号的系统提示词片段会静默覆盖用户配置的委派策略，且无法选择退出。高反应量反映出的不满更多在于*未文档化的、模型特定的行为变更*，而非默认行为本身。相关报告 #84183 已关闭，讨论集中到此处。

3. **[#91188](https://github.com/anthropics/claude-code/issues/91188) — 使自动记忆 `MEMORY.md` 压缩提醒阈值可配置**（60 条评论）
   200 行 / 25KB 的自动加载窗口是硬编码的，触发该限制的用户只会被反复提醒，而无法获得控制权。持续的评论量表明，许多团队正运行在当前记忆预算的边界上。

4. **[#105867](https://github.com/anthropics/claude-code/issues/105867) — 仅加载索引行时，自动记忆中的输出格式规则只有约 72% 的情况被遵循**（新提交，4 条评论）
   一项量化的可靠性发现：指令遵循率从约 95%（完整记忆文件进入上下文）降至约 72%（仅有索引行）。对任何依赖持久化约定的用户都直接相关，也是 #91188 的良好补充。

5. **[#93201](https://github.com/anthropics/claude-code/issues/93201) — 内置浏览器对内部主机名（`*.local`）忽略“允许的站点”设置**（15 条评论，30 👍）
   针对内部主机名的站点级权限被禁用，因此用户对本地开发/预发主机的*每一次*操作都会弹出提示。对于在允许列表后的 `.local` 域名上测试的团队来说尤其痛苦。

6. **[#73524](https://github.com/anthropics/claude-code/issues/73524) — PowerShell `Remove-Item on system path` 防护过度拦截合法命令**（10 条评论）
   AST 分析器将不相关的 token 误判为删除目标，且该防护无法覆盖。典型的静态分析误报，且没有规避途径。

7. **[#102208](https://github.com/anthropics/claude-code/issues/102208) — 提示建议从不出现（Windows，v2.1.296/v2.1.300）**（8 条评论，8 👍）
   多位用户在 TUI 和桌面端均确认了该回归，`/config` 显示该功能已启用，且未设置任何环境变量覆盖。一份清晰、可复现的回归报告。

8. **[#106003](https://github.com/anthropics/claude-code/issues/106003) — Windows 上的无头 `chrome.exe` 触发登录失败并锁定由 IdP 管理的账户**（新提交）
   在 JumpCloud 管理的环境中，每次无头 HTML→PDF/PNG 调用都会引发一阵登录失败尝试，最终升级为账户锁定。影响安全和 IT，并可能影响企业部署。

9. **[#105945](https://github.com/anthropics/claude-code/issues/105945) — `security-guidance` 插件 hook 在 Windows 桌面端阻止所有提示**（新提交）
   由于在 `AppData\Roaming\Claude\claude-code` 下找不到 `claude.exe`，`claude auth status` 返回非 JSON 内容，导致所有提示都被阻止。插件期望的路径与桌面应用安装布局之间存在路径解析不匹配。

10. **[#91717](https://github.com/anthropics/claude-code/issues/91717) — 桌面端更新后 Remote Control 失败并返回 HTTP 403；`/remote-control` 重试无法恢复**（8 条评论）
    跨平台（Windows/macOS）的认证失败，会期内没有可用的恢复路径——需要完全重启。符合更广泛的认证可靠性主题。

*同样值得关注：* [#92517](https://github.com/anthropics/claude-code/issues/92517)（跨账户池化用量 / 共享会话上下文）、[#105928](https://github.com/anthropics/claude-code/issues/105928)（后台子代理每次 tick 都唤醒父代理）、[#93138](https://github.com/anthropics/claude-code/issues/93138)（从反馈记录中抹除密钥）、[#105831](https://github.com/anthropics/claude-code/issues/105831)（在桌面端工作流面板中恢复每个代理的模型/token/工具计数）。

## 4. 关键 PR 进展
过去 24 小时内仅有 **2 个 pull request** 有更新，因此本节内容不可避免地较为单薄：

1. **[#32751](https://github.com/anthropics/claude-code/pull/32751) [OPEN] — fix(hookify)：将 stop/prompt 事件映射到正确的字段名**
   修复 #32153。使用简单 `pattern` 语法并设置 `event: stop` 或 `event: prompt` 的 Hookify 规则永远不会触发，因为 `config_loader.py` 将它们映射为 `field='content'`，而 `rule_engine._extract_field()` 无法为 Stop/UserPromptSubmit 事件解析该字段（它仅对 Write 类事件处理 `content`）。自 2026 年 3 月起处于打开状态——对于任何编写 hook 规则的人来说，这是一个小而高杠杆的修复。

2. **[#57333](https://github.com/anthropics/claude-code/pull/57333) [CLOSED] — 更新 README.md**
   仅文档变更；关闭时未提供更多细节。

> 观察：相对于 issue 数量，社区 PR 吞吐量显得非常低（49 个 issue 对比 2 个 PR 有更新），且唯一一个实质性修复已开放约 7 个月。值得提醒维护者关注分类处理能力。

## 5. 热门讨论
略——本数据集中未提供讨论数据。

## 6. 功能请求趋势

- **可配置的记忆与上下文预算。** #91188（压缩阈值）和 #105867（仅索引时的遵循率）表明，用户要求对自动记忆加载的内容和提醒时机进行显式控制——并希望了解因截断而损失了*多少*保真度。
- **Agent/子代理控制与可观测性。** #80988 与 #84183（可选择退出 Agent 工具抑制）、#86089（工作流中可恢复的代理会话）、#105928（通知噪音）、#105831（桌面面板中每个代理的 token/工具/模型）。主题是：用户希望成为委派策略的权威，并看到子代理实际做了什么。
- **桌面端/UI 打磨与一致性。** #102699（侧边栏主题/用户 CSS、更醒目的项目标题）、#105189（Chat 标签页的未读/运行状态）、#105985（状态栏中的 cwd，以便在多会话中保持清晰）、#26784（无需按 Shift 的拖放文件）、#91697（Wayland 焦点抢占）。
- **多账户与团队易用性。** #92517 请求跨订阅池化用量，以及为共同处理一个项目的小团队提供共享会话上下文。
- **反馈流程中的同意与隐私。** #93138（抹除密钥）、#103863（在不携带会话上下文的情况下发送反馈）、#87955（带有选择加入转录分享的结构化想法通道）。
- **无头/CI 可配置性与文档。** #104929 请求一种有文档说明的方式，在 `claude -p` 运行中跳过所有 `CLAUDE.md` 文件，同时保留项目技能。
- **平台/浏览器覆盖。** #90414（Firefox 扩展），以及 #93201 中的内部主机名支持。

## 7. 开发者痛点

1. **认证无法持久化。** #1757（每天重新登录）和 #91717（Remote Control 中不可恢复的 403）是两个最具破坏性的可靠性问题；两者都需要放弃当前会话来恢复。
2. **系统提示词的静默行为变更。** #80988/#84183——按模型作用域的指令会覆盖用户配置，既没有变更日志条目，也没有退出选项。这比行为本身更侵蚀信任。
3. **记忆系统不透明且有损。** 硬编码阈值（#91188）加上仅加载索引行时可测量的遵循率下降（#105867），使持久化约定变得不可预测。
4. **Windows 是最弱的平台。** 提示建议回归（#102208）、PowerShell 防护误报（#73524）、插件路径解析失败（#105945）、新聊天中缺少 `mcp__claude-in-chrome__file_upload`（#105868），以及无头 Chrome 导致的 IdP 账户锁定（#106003）。
5. **过度宽泛的安全防护且无法覆盖。** #73524——静态分析阻止合法命令且没有规避途径，迫使用户完全禁用工具。
6. **子代理通知轰炸。** #105928——后台子代理在等待自己的 Monitor/后台 shell 时，每次 tick 都用相同的“Waiting.”消息唤醒父代理，污染父代理的上下文。
7. **密钥可能通过 `/feedback` 默认设置泄露。** #93138——转录默认会被提交，只有注意到开关才能避免泄露密钥。
8. **无头工作流的文档缺口。** #104929——在 `-p` 模式下选择性加载技能与 `CLAUDE.md` 的开关矩阵没有文档说明。
9. **桌面端回归且无诊断界面。** #105831——工作流面板中移除了每个代理的 token/工具指标；#105189——Chat 标签页缺少 Code 会话具有的运行/未读状态。

---
*数据窗口：issue 和 PR 更新于 2026-10-29。本时段内没有可用的版本发布或讨论数据。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区摘要 — 2026-10-30

**来源：** [github.com/openai/codex](https://github.com/openai/codex) · 数据窗口：最近 24 小时（截至 2026-10-29）

---

## 1. 今日亮点

发布了两个 Rust alpha 版本（0.166.0-alpha.6 和 0.166.0-alpha.5.1），但均未公布变更日志；同时 PR 队列中出现了大量由机器人提交的推送，集中在 **Guardian review**、**托管命令审批检查点** 和 **网页搜索/工具调用管线**。问题侧，当日讨论量主要由 **Windows 沙箱与命令执行失败**、**浏览器/扩展集成脆弱性**，以及针对合法 C/C++ 与 Git 工作的 **安全护栏误报** 增多所占据。

---

## 2. 版本发布

- **[rust-v0.166.0-alpha.6](https://github.com/openai/codex/releases)** — `0.166.0-alpha.6`，发布说明仅包含版本字符串（无实质性变更日志）。
- **[rust-v0.166.0-alpha.5.1](https://github.com/openai/codex/releases)** — `0.166.0-alpha.5.1`，0.166 alpha 线上的补丁级版本；无已记录变更。

> 两者均为预发布 alpha 标签。最近 24 小时内没有稳定通道版本；应将其视为 CLI/引擎迭代，而非面向用户的功能公告。

---

## 3. 热门 Issue

1. **[#54532](https://github.com/openai/codex/issues/54532)** — `[Windows][Computer Use] zh-CN document-role URL detection failure on @oai/sky 0.7.8`（12 条评论）。当日互动量最高的问题：在中文 Windows 上，原生 Computer Use 可以枚举 Chrome/Edge 窗口，但在获取窗口状态时因浏览器 URL 置信度错误而失败。据称，一个范围很窄的 document-role 谓词修复即可恢复两个浏览器——这强烈表明，依赖区域设置的 role 启发式是根因。

2. **[#36319](https://github.com/openai/codex/issues/36319)** — `[macOS] ChatGPT Chrome extension unavailable in Chrome Web Store`（9 条评论）。官方商店列表返回“此项目无法购买或下载”，尽管 Codex Chrome 插件和原生宿主均正常。该问题已持续很久（7 月创建）且仍未解决，正在削弱用户对浏览器扩展安装路径的信任。

3. **[#57107](https://github.com/openai/codex/issues/57107)** — `[Windows][Desktop][IAB] Attached tab loses browser-session binding before action`（8 条评论）。内置浏览器（IAB）成功附加标签页后，却在下一个操作时拒绝该标签页，理由是它“不再属于浏览器会话”。代理浏览器控制循环中的静默状态丢失，对任何基于 IAB 的自动化来说都是正确性风险。

4. **[#55230](https://github.com/openai/codex/issues/55230)** — `[Windows] Codex App sandbox fails to execute commands (HRESULT 0x80070020)`（7 条评论）。Windows 11 25H2 + Codex 26.1013.40934，Plus 套餐：应用沙箱无法启动命令。这是本时间窗口内报告的最高严重级别 Windows 阻断问题——该应用实际上无法用于本地任务执行。

5. **[#34455](https://github.com/openai/codex/issues/34455)** — `Make request_user_input timeout duration and behavior configurable`（6 条评论，**22 👍**）。本组中获赞最多的问题。`request_user_input` 会在固定的 60 秒宽限 + 60 秒倒计时后自动解决，并提交空答案。开发者希望计时器和超时结果可配置，而不是替他们静默猜测。

6. **[#43197](https://github.com/openai/codex/issues/43197)** — `Windows: deleting archived Codex chats fails despite enabled delete button`（6 条评论）。UI 状态与后端不一致——按钮处于可用状态，删除却静默失败。这加深了“Windows 功能对齐与状态一致性”这一主题。

7. **[#57620](https://github.com/openai/codex/issues/57620)** — `[macOS] Worktree icons missing from sidebar after updating to 26.1023.50603`（5 条评论，**5 👍**）。最新桌面构建上的新回归；影响面不大，但对任何使用多个 git worktree 的人来说，这是可见的工作流中断。

8. **[#34070](https://github.com/openai/codex/issues/34070)** — `Codex Windows App uses hardcoded %USERPROFILE%\.codex — ignores CODEX_DIR / CODEX_HOME`（5 条评论）。应用/CLI 配置分歧：CLI 遵循这些环境变量，桌面应用则不遵循。对于磁盘空间受限的 Windows 机器，这是一个具体的磁盘管理阻断问题，也反映了不同运行时之间更广泛的架构不一致。

9. **[#57759](https://github.com/openai/codex/issues/57759)** — `[Linux/Wayland] Codex 26.1021.22027 fails to start UI and freezes VS Code 1.143.1`（4 条评论，**1 👍**）。可复现的回归，且已确认降级版本（26.908.40401）可用。宿主 IDE 硬冻结是扩展最糟糕的失败模式，而降级二分排查为维护者提供了干净复现。

10. **[#58148](https://github.com/openai/codex/issues/58148)** — `Credential security and authorization should be a core Codex capability`（1 条评论，10-29 提交）。由一位将 Codex 用于真实 DevOps 工作的用户提交（基础设施管理、部署、生产调试、高价值 API 密钥）。其主张是：密钥处理应成为一等原语，而不是委托给 shell 约定——随着使用场景从代码生成转向运维，这是一个方向上很重要的请求。

---

## 4. 重点 PR 进展

> 注：本时间窗口内更新的全部 50 个 PR 基本上均由 `copyberry[bot]` 创建，表明存在一条自动化/代理编写的合并列车。以下评审的是实质性行为变更。

1. **[#58147](https://github.com/openai/codex/pull/58147)** — *将独立网页搜索失败返回给模型。* 当前独立搜索错误会作为致命错误中止回合；此项改动将客户端设置错误和失败请求转换为不成功的工具输出，使模型能够推理并恢复。这显著提升了代理韧性。

2. **[#58140](https://github.com/openai/codex/pull/58140)** — *让独立网页搜索经由线程的工作区上下文路由。* 修复了请求被发送到 bootstrap 后端而非已发现的工作区后端、从而绕过工作区路由的问题。

3. **[#58125](https://github.com/openai/codex/pull/58125)** — *在 Code Mode 客户端中支持协商式服务端截断。* 为 stdio 和 gRPC 增加截断协商，使超大输出——包括脚本错误——在跨传输前受到限制，而不是在宿主侧截断。

4. **[#58045](https://github.com/openai/codex/pull/58045)** — *新增需要全新人工批准的托管命令检查点。* 在托管 `requirements.toml` 前缀规则中引入 `decision = "prompt-user"`，强制人工决策，不受自动评审、hook 允许和已保存批准影响。这是本批中清晰的策略控制新增项。

5. **[#58119](https://github.com/openai/codex/pull/58119)** — *为注入的线程命令新增实验性 Guardian review。* 暴露 `thread/guardianReview`，在不执行空闲线程最终注入的 `exec_command` 的情况下对其进行评估，返回调用 ID 及评估结果（当 exec 策略跳过审批时返回 `null`）。

6. **[#58075](https://github.com/openai/codex/pull/58075)** — *为自适应 Guardian review 使用服务端评估。* 将最终服务端评估匹配到响应/输出项并复用，而不是异步评分，从而使低风险操作可以走快速路径。

7. **[#58040](https://github.com/openai/codex/pull/58040)** — *在 Guardian review 过程中保留原生工具调用证据。* 即使调用已从实时历史中老化移除，也保留原始函数调用元数据——这是正确审查加密多代理消息所必需的。

8. **[#58122](https://github.com/openai/codex/pull/58122)** — *新增增量 exec 工具功能标志。* 将 `incremental_exec_tools` 注册为开发中、默认关闭的功能，并在配置 schema 中暴露——这是增量工具暴露的脚手架。

9. **[#58091](https://github.com/openai/codex/pull/58091)** — *更新记忆提取与整合的默认模型。* 当提供方未强制要求后端专用 ID 时，提取切换为 `gpt-6-luna`，整合切换为 `gpt-6.1-terra`——即使用更便宜/更小的模型进行记忆维护。

10. **[#58129](https://github.com/openai/codex/pull/58129)** — *在创建子存储之前持久化子代理关系。* 防止出现父子树删除无法发现的孤立子历史；关系写入失败现在会拒绝生成。

*其他值得注意：* [#58144](https://github.com/openai/codex/pull/58144)（新增 `codex.additional_context` 计数/字节/截断指标）、[#58121](https://github.com/openai/codex/pull/58121)（集中式提供方请求鉴权检查，并在凭证变更时重试）、[#58134](https://github.com/openai/codex/pull/58134)（模型迁移指引优先使用有文档记录的替代项）、[#58110](https://github.com/openai/codex/pull/58110)（针对仅 Windows 的 `libz-sys` 做限定范围的 RUSTSEC-2026-0418 忽略）。

---

## 5. 热门讨论

### 想法
- **[#30332](https://github.com/openai/codex/discussions/30332)** — *Codex CLI 后台更新，不阻塞启动。* 提议采用 Claude Code 风格的流程：在后台检查/下载，准备好后提示重启，而不是在启动时强制做出更新决定。启动摩擦是 CLI 工具中反复出现的抱怨。
- **[#57967](https://github.com/openai/codex/discussions/57967)** — *为 ChatGPT Plus 每月提供 1–2 次免费 Codex 用量重置。* 请求将当前促销性的重置变为可预测的月度额度；其表述是留存/套餐价值，而非权利诉求。

### 问答
- **[#8582](https://github.com/openai/codex/discussions/8582)** — *在当前聊天历史中搜索/查找*（4 👍）。`Ctrl-F` 无论焦点在哪都总是作用于代码编辑器；Codex 画布中不存在搜索上下文菜单。这是基础可导航性缺口，且随对话长度增长而加剧。
- **[#5210](https://github.com/openai/codex/discussions/5210)** — *有办法清空文本区域吗？* 在误粘贴大段内容后，没有发现可用于清空提示输入的快捷键——小小的 UX 痛点，帖子却已存在很久。

### 展示与分享
- **[#57746](https://github.com/openai/codex/discussions/57746)** — *Zozo：一个可检查的 issue-to-PR 示例，以及面向编码代理工作的评审清单。* 提供一个公开的 issue/diff/CI 轨迹，以及用于审查代理输出的清单。对于需要可审计代理运行的团队来说，这是一个有用的模式。
- **[#57591](https://github.com/openai/codex/discussions/57591)** — *toli — 让 Codex 和 Claude Code 协作，即使在不同机器上。* 一个 Apache-2.0 工具，用于跨开发者机器进行直接的代理间通信，动机是结对调试时本地上下文存在差异。
- **[#58093](https://github.com/openai/codex/discussions/58093)** — *OpenFusion：用于子任务处理的编排器与路由器。* 将每个子任务路由到最具成本效益的可用模型，并带有在结果不佳时升级的评判步骤——围绕 Codex/代理工作负载做成本优化。
- **[#58104](https://github.com/openai/codex/discussions/58104)** — *Kilobat：面向 AI 代理（以及人类）的网络工具。* macOS 菜单栏网络监视器，可跟踪 Codex、Claude Code 和 Gemini 流量，并提供开源 CLI + MCP，使代理可以自行检查网络状态。
- **[#56337](https://github.com/openai/codex/discussions/56337)** — *Off the Wall：在 Codex 回答前回忆你过去的纠正。* MIT 许可，保留用户原话中的纠正，并将其回引给 Codex 或 Claude Code——一个轻量级持久偏好层。
- **[#58031](https://github.com/openai/codex/discussions/58031)** — *结合当前阿里云文档与官方引用使用 Codex。* 报告称生成的云配置看似合理，但需要对照实时端点/地域/模型进行验证——这支持在领域特定工作中使用有依据的文档检索。

---

## 6. 功能请求趋势

- **代理行为的可配置性。** 获赞最多的问题（#34455，22 👍）希望 `request_user_input` 超时可配置；#34070 希望尊重 `CODEX_HOME`/`CODEX_DIR`；#58127（PR）让工具提示遵循某项偏好。主题：停止硬编码策略和 UI 默认值。
- **桌面端/CLI 对等与状态一致。** 环境变量处理、云环境发现（#58145：CLI 选择器返回 `HTTP 200 []`，而桌面端显示一个已发布环境）以及归档聊天删除（#43197）都指向不同界面之间分叉的代码路径。
- **平台对等，尤其是 Windows。** Computer Use（#54532、#57371）、沙箱执行（#55230）、策略拒绝消息（#56722）、`/approve` 可发现性（#57350）、文件/PDF 访问（#58139）——本时间窗口内最大的单一集群。
- **透明、可操作的安全与策略错误。** #58138 和 #58141（均为 10-29）报告网络安全护栏阻止普通 C/C++ 和本地 Git 集成工作；#56722 要求给出阻断规则和恢复路径，而不是仅仅显示“blocked by policy”。
- **凭证与密钥管理成为一等能力**（#58148）——由使用场景转向基础设施/部署/生产工作所驱动。
- **浏览器与扩展集成的健壮性**——Chrome Web Store 可用性（#36319）、IAB 会话绑定（#57107）、不支持的扩展侧边栏（#58133）。
- **IDE 易用性**——聊天内搜索（#8582）、清空输入快捷键（#5210）、文件链接尊重默认编辑器（#47702）。
- **成本/用量灵活性**——可预测的用量重置（#57967）以及社区构建的到更便宜模型的路由（#58093）。
- CLI 的**非阻塞更新流程**（#30332）。

---

## 7. 开发者痛点

- **Windows 是最薄弱的面。** 应用沙箱内的命令执行直接失败（HRESULT `0x80070020`，#55230）；已授权的命令被以“blocked by policy”为由拒绝，却未指明规则，也没有恢复操作（#56722）；`/approve` 在 UI 中没有文档说明，并返回“no command found”（#57350）。多个独立报告汇聚到同一体验：权限系统说不行，却不肯说为什么。
- **安全护栏对普通工作产生误报。** 一天内有两份报告（#58138 C/C++；#58141 本地 Git 集成）描述了网络安全过滤器反复中断明确授权的开发任务——这是直接的生产力税，也削弱了对审批流程的信任。
- **静默状态与缓存 bug。** IAB 在操作前丢失标签页的会话绑定（#57107）；PDF 刷新保留陈旧内容，因为缓存键遗漏了 `conversationId`（#56862）；归档聊天删除无操作（#43197）。静默失败在代理工作流中代价高昂，因为观察到它们的是代理，而不是人类。
- **回归进入稳定桌面通道。** Worktree 图标在 26.1023.50603 中消失（#57620）；VS Code 扩展在 Linux/Wayland 上的 26.1021.22027 中冻结整个 IDE（#57759，只能通过降级修复）。用户实际上在替发布门禁做调试。
- **配置未被一致遵循。** 桌面应用忽略 `CODEX_DIR`/`CODEX_HOME`（#34070），并且根据 #58145，它与 CLI 在哪些云环境存在这一点上不一致——迫使用户重复配置或手动同步设置。
- **扩展分发不可靠。** 持续数月的 Chrome Web Store 故障（#36319）阻断了文档中的安装路径，而不支持的扩展侧边栏（#58133，OKX Wallet）缩小了内置浏览器可承载的范围。
- **区域设置特定故障。** 不完整的 zh-CN 本地化（#27255）以及仅 zh-CN 出现的 Computer Use 失败（#54532）表明，en-US 之外的区域设置处理测试不足。
- **长对话可导航性与输入控制仍未解决。** 没有聊天内搜索（#8582），也没有清空输入快捷键（#5210）——这些是小请求，但日常代价被放大，而且两个帖子都已存在数月。

---

*以分析师摘要形式准备。源数据中的 alpha 发布说明为空；PR 意图根据标题和描述推断。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区简报 — 2026-10-30

## 今日亮点
过去 24 小时内没有发布新版本，但社区活动依然频繁：共更新了 46 个 issue 和 37 个 PR，关注焦点仍集中在 agent/subagent 的可靠性上。两个 P1 级 agent bug——`MAX_TURNS` 误报成功（#22323）以及通用 agent 无限挂起（#21409）——仍持续引发最多的讨论和反应。在 PR 方面，贡献者提交了一系列加固修复，涉及 checkpoint/restore 正确性、shell 替换安全性、重试去重以及 CI 测试覆盖率。

---

## 发布
过去 24 小时内没有新版本发布。

---

## 热门 Issue

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent 的 `MAX_TURNS` 被报告为 `GOAL` 成功（P1）**
   一个 `codebase_investigator` subagent 报告 `status: "success"` 和 `Termination Reason: "GOAL"`，但其自身输出却表示在执行分析前就已达到回合上限。对于任何依据 agent 状态进行分支的自动化流程来说，这都是一个正确性/信任问题。13 条评论和 2 个 👍 使其成为本时间段内讨论最多的 issue。

2. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — 通用 agent 永久挂起（P1）**
   一旦 CLI 交由通用 agent 处理，像创建文件夹这样的简单操作就会无限挂起；用户报告等待时间长达一小时。规避方案——指示模型不要使用 subagent——本身就说明了问题，该 issue 获得 8 个 👍，是本批中反响最多的。

3. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — 零依赖操作系统沙箱 + 执行后意图路由（P2，effort/large）**
   提议充分利用 Gemini 3 原生的 bash 亲和力，让模型在操作系统级沙箱内串联使用 POSIX 工具（`grep`、`sed`、`awk`），然后根据执行后意图进行路由。这是对其他地方提出的安全担忧的架构层面回应。9 条评论，1 个 👍。

4. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini 对 skill 和 subagent 使用不足**
   虽属轶事但引发广泛共鸣：除非明确指示，否则模型不会调用自定义 skill（`gradle`、`git`）或 subagent，即使它们高度相关。这直接削弱了可扩展性接口的价值。7 条评论。

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — EPIC：评估 AST 感知的读取、搜索与代码库映射（P2）**
   父级 epic，研究 AST 感知工具是否能减少错位读取、减少回合数并削减 token 噪声。相关调研（#22746、#22747）正在追踪 `tilth`/`glyph`/`ast-grep` 作为候选方案。7 条评论。

6. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 可用工具超过 128 个时报 400 错误（P2）**
   一旦启用的工具数量越过阈值，CLI 就会返回 400，且没有优雅的范围控制。对于拥有大量 MCP server 或扩展的用户而言，这是一道硬性的可扩展性上限。3 条评论。

7. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — Agent 应阻止/劝阻破坏性行为（P2）**
   在存在更安全替代方案时，模型仍会诉诸 `git reset` 或 `--force`，并且在破坏性数据库/资源操作方面缺乏护栏。与安全相关，可能影响策略层面的工作。3 条评论，1 个 👍。

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — 浏览器 subagent 在 Wayland 上失败（P1）**
   浏览器 subagent 在 Wayland 会话中以 `Termination Reason: GOAL` 终止，即失败被掩盖为成功——与 #22323 相同的报告模式。Linux/Wayland 用户实际上被阻断了浏览器自动化。4 条评论。

9. **[#22267](https://github.com/google-gemini/gemini-cli/issues/22267) — 浏览器 Agent 忽略 `settings.json` 覆盖项（P2）**
   `AgentRegistry` 在初始化时正确合并了设置，但浏览器 Agent 完全绕过了这些设置——包括 `maxTurns`。这种配置漂移若与上文的挂起/回合上限问题叠加，尤其令人困惑。4 条评论。

10. **[#23571](https://github.com/google-gemini/gemini-cli/issues/23571) — 模型在工作区乱丢临时脚本（P2）**
    当仅限 shell 执行时，模型会在任意目录中生成编辑脚本，在干净提交前制造清理负担。这是对纯 shell 配置的具体工作流负担。3 条评论。

*同样值得关注：* [#20079](https://github.com/google-gemini/gemini-cli/issues/20079)（符号链接的 agent 文件无法识别）、[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)（通过 `/chat share` 暴露 subagent 轨迹）、[#22741](https://github.com/google-gemini/gemini-cli/issues/22741)（通过 Ctrl+B 后台运行本地 agent，2 个 👍）。

---

## 重要 PR 进展

1. **[#30034](https://github.com/google-gemini/gemini-cli/pull/30034) — 在影子仓库中遵循 `.git/info/exclude` 和 `core.excludesFile`**
   修复了一类数据丢失 bug：在 Git 配置规则下本应被忽略的文件，却被 `/restore` 还原或删除。对于任何在 checkpoint 中使用本地专属排除规则的人都很重要。

2. **[#30035](https://github.com/google-gemini/gemini-cli/pull/30035) — 防止 LLM 提示词模板中的 `$` 模式损坏（P2）**
   将 `summarizer.ts`、`llm-edit-fixer.ts` 和 `sessionSummaryService.ts` 从 `String.replace(placeholder, value)` 迁移到单次遍历的 `safeTemplateReplace()`，消除提示词构造中动态值被解释的 bug。

3. **[#30031](https://github.com/google-gemini/gemini-cli/pull/30031) — 根据执行生命周期控制后台日志流的初始化（P2）**
   处理一个模型配置边界情况：当显式选择 `gemini-2.5-flash`，同时又设置 `useLatestFlash` 和动态模型配置时。防止日志流过早初始化。

4. **[#30023](https://github.com/google-gemini/gemini-cli/pull/30023) — 在 PR CI 中运行 SDK 测试，修复 `AgentLoopContext` mock（P2）**
   重新启用 6 个被跳过的 `GeminiCliSession.sendStream()` 测试，并将 SDK 包加入 `others` CI 分片。有效减少了未测试的代码面。

5. **[#29918](https://github.com/google-gemini/gemini-cli/pull/29918) — 通过 OSC 7501 报告 working/blocked/idle 状态**
   TUI 现在会发出终端程序状态报告，让 multiplexer 的标签页能够显示哪个会话需要关注。多会话工作流的一项体验改进（size/xl）。

6. **[#30020](https://github.com/google-gemini/gemini-cli/pull/30020) — 重试时丢弃失败尝试流出的工具调用**
   在流中途重试时，失败尝试和成功尝试的 `ToolCallRequest` 事件都会被执行——这意味着有副作用的命令可能运行两次。这是 agent 循环中高价值的正确性修复。

7. **[#30029](https://github.com/google-gemini/gemini-cli/pull/30029) — 使命令替换拦截可由用户配置（P3，招募帮助）**
   新增 `security.allowCommandSubstitution`（默认 `false`），用于替换 shell 工具中对 `$()`、反引号和进程替换的硬编码拦截。修复 #27393；在便利性与有意的安全默认值之间做权衡。

8. **[#30026](https://github.com/google-gemini/gemini-cli/pull/30026) — 在不可信标志检查中将项目临时路径视为本地**
   不再让 CLI 对 `~/.gemini/tmp/<project>/...` 下自己的辅助脚本弹出确认提示，这是 shell 输出将脚本路径泄漏到上下文后反复出现的摩擦点。

9. **[#30019](https://github.com/google-gemini/gemini-cli/pull/30019) — 在工具输出遮蔽期间保留会话历史**
   在恢复工具输出被遮蔽的会话时，通过不将 API 形态的 `getHistory()` 视图写回存储，防止首条用户提示被丢弃。

10. **[#29977](https://github.com/google-gemini/gemini-cli/pull/29977) — 在 `read_background_output` 中遵循取消（P2，招募帮助）**
    该工具此前会忽略其中止信号，无论如何都会睡满整个 `delay_ms` 再读取。它补充了 [#29978](https://github.com/google-gemini/gemini-cli/pull/29978)，后者修复了同一工具中边界/超长行被丢弃的问题。

*本时间段内同样合并/关闭：* [#30012](https://github.com/google-gemini/gemini-cli/pull/30012)（加载指示器中的 429 冷却倒计时）、[#30006](https://github.com/google-gemini/gemini-cli/pull/30006)（Windows IDE 进程查找的 PowerShell CIM 回退）、[#29989](https://github.com/google-gemini/gemini-cli/pull/29989)（core/cli 中的 `\n` 转义损坏）、[#30024](https://github.com/google-gemini/gemini-cli/pull/30024)（undici 7.10.0 → 7.30.1）。

---

## 功能请求趋势

- **Agent 编排的成熟度。** 这是迄今为止最大的集群：可后台运行的本地 agent（#22741）、共享内存/并行 subagent 协作（#18287）、将构建修复循环委托给通用 agent（#22602），以及专门的 subagent 评估策略（#22601）。Subagent 显然已是战略重心。
- **可观测性与可调试性。** 在 `/chat share` 中提供 subagent 轨迹（#22598）、在 `/bug` 报告中包含 subagent 上下文（#21763），以及让 agent 更好地“自知”自身标志与快捷键（#21432）——这些请求都指向同一个缺口：用户看不到 agent 在做什么。
- **Token 高效、结构感知的代码智能。** AST epic（#22745）加上 #22746/#22747、“Tactful Extraction”（#19561）以及持久化的基于文件的任务追踪（#18836），共同构成一股旨在减少上下文膨胀与上下文腐化的连贯推力。
- **带逃生通道的安全性。** 沙箱化的原生 bash（#19873）、劝阻破坏性 git/数据库命令（#22672）以及可配置的命令替换（#30029）表明，社区想要安全默认值*加上*明确的退出选项。
- **浏览器 agent 的韧性。** 会话接管/锁恢复（#22232）以及遵循 `settings.json`（#22267）是所有运行持久浏览器会话的人反复提出的诉求。
- **策略粒度。** 按工作区自动添加策略（#18397）反映了对仓库范围而非全局信任决策的需求。

---

## 开发者痛点

- **静默挂起与被掩盖的失败。** 两个最主要的 P1——通用 agent 挂起（#21409）以及 `MAX_TURNS` 被报告为 `GOAL` 成功（#22323，以及 #21983 中相同的模式）——是最具破坏性的一类 bug，因为它们同时击穿了脚本化、CI 和用户信任。
- **未被遵循的配置。** 浏览器 Agent 忽略 `settings.json`（#22267）以及符号链接的 agent 文件被静默跳过（#20079），都会造成“我配置对了却什么都没发生”的体验，且没有任何诊断信号。
- **工具的可扩展性上限。** 超过工具阈值后的 400 错误（#24246）恰恰惩罚了那些投入 MCP server 和扩展的高级用户。
- **工作区卫生。** 散落在各目录中的临时脚本（#23571）以及 `/restore` 触碰被忽略的文件（#30034），都会把一次干净提交变成手动清理。
- **平台特定故障。** Wayland 浏览器失败（#21983）和 Windows 路径/进程问题（#30033、#30006）反复出现；在 #30033 之前，Windows 上 `fs.stat` 在 Node 22.12–22.16/23.x 返回 `dev: 0`，导致*每一次*安全文件读取都失败。
- **agent 循环本身的正确性 bug。** 重试时工具调用重复执行（#30020）、`\n` 转义损坏（#29989）以及提示词模板中的 `$` 模式篡改（#30035）虽属底层，但影响半径很大——它们会静默改变行为，而不是大声失败。
- **评估基础设施尚不可信。** #23166（“evals bleed”）和 #23313（一个 steering eval 不得不被注释掉）表明团队自身仍在稳定测量层，这拖慢了人们对 agent 质量声明的信心。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI — 社区摘要
**日期：** 2026-10-30 · **来源：** [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

## 1. 今日亮点
过去 24 小时内没有新版本发布，但有 38 个 issue 有更新，活动集中在身份认证/平台缺陷以及 ACP（Agent Client Protocol）功能对齐缺口。长期存在的组织权益故障 [#552](https://github.com/github/copilot-cli/issues/552) 仍是讨论最多的主题帖，有 31 条评论；若干高严重度资源消耗报告（[#5254](https://github.com/github/copilot-cli/issues/5254), [#4613](https://github.com/github/copilot-cli/issues/4613)）也仍持续引发关注。新增分诊项包括 `copilot --cloud` 预配路径失效，以及 `/copy` 的 Markdown→HTML 回归。

## 2. 发布
_过去 24 小时内无新版本发布。_

## 3. 热门 Issue

1. **[#552](https://github.com/github/copilot-cli/issues/552) — `Failed to list models: 403 unauthorized`（OPEN，31 条评论，👍4）**
   仓库中流量最高的主题帖。已启用 Copilot CLI 的组织内用户仍无法枚举模型，阻塞基本使用。评论量（从 2025 年 11 月持续至今）表明，这是 GitHub 侧尚未解决的权益/映射问题，而非简单的客户端缺陷。

2. **[#2165](https://github.com/github/copilot-cli/issues/2165) — Ubuntu keychain 支持已损坏（OPEN，5 条评论，👍22）**
   本批次中反响最高的条目。包含两个不同缺陷：keychain 变通方案的文档有误，以及 `secret-tool` 相关的认证失败。Linux 用户认为这是头等平台支持缺口。

3. **[#4802](https://github.com/github/copilot-cli/issues/4802) — PRU 配额被清空，可能与 Assisted Permissions 有关（OPEN，8 条评论）**
   来自 Pro 年度/传统按请求计费用户的、影响计费的报告。社区反应谨慎但担忧——配额核算回归会迅速侵蚀信任，尤其是在没有明确补救路径的情况下。

4. **[#4851](https://github.com/github/copilot-cli/issues/4851) — Azure MCP 服务器发送 HTTP 请求失败（CLOSED，6 条评论，👍10）**
   验证 Azure API Center MCP 注册表时，Rust 运行时出现 `BrokenPipe`——这是一次“一夜之间坏掉”的企业级回归，该问题已关闭，暗示修复已落地。值得注意之处在于其 10 个赞以及企业对 MCP 的依赖。

5. **[#4275](https://github.com/github/copilot-cli/issues/4275) — ACP：将 `contextTier` 暴露为会话配置选项（OPEN，7 条评论，👍4）**
   交互式 `/model` 选择器支持在会话中途更改上下文层级；ACP 客户端只能在启动时设置。来自 GitKraken 集成方的一项明确对齐请求——这表明第三方 ACP 使用方如今已是一个真实用户群体。

6. **[#2109](https://github.com/github/copilot-cli/issues/2109) — ACP：支持 `ask_user` / `ask_question` 扩展方法（OPEN，4 条评论，👍8）**
   目前仅暴露 `session/request_permission`，因此自定义 ACP 客户端无法以结构化答案呈现澄清问题。反响良好（👍8），且对 ACP 生态具有架构上的重要意义。

7. **[#5254](https://github.com/github/copilot-cli/issues/5254) — 1.0.103：长时间并行 agent 会话中主进程增长到 37 GiB（OPEN，2 条评论）**
   在 32 GiB 的 Mac 上运行约 6 小时 19 分钟后，物理占用达到 37.3 GiB，伴随 1.33 亿次 malloc 分配和 10.7 GiB 碎片。这是本批次中最令人警惕的稳定性报告——带并行子代理的长时间恢复会话实际上已无法使用。

8. **[#4613](https://github.com/github/copilot-cli/issues/4613) — 1.0.80+ 回归：MCP schema 被提前注入，启动 token 数增加 354K（CLOSED，3 条评论）**
   CLI 似乎不再延迟加载 MCP 工具 schema，即使提示很简单，也会在首次请求中注入完整的 ambient 目录。对任何拥有大型 MCP 配置的人来说，这都是直接的成本/延迟回归；已关闭暗示已采取分诊处理。

9. **[#4576](https://github.com/github/copilot-cli/issues/4576) — `includeCoAuthoredBy: false` 未被任务子代理继承（OPEN，2 条评论，👍5）**
   子代理仍会添加 `Co-authored-by: Copilot` 尾注，这与 `settings.json` 中的显式退出设置相矛盾。影响面虽小，但对有严格提交归属政策的团队来说确实是合规烦恼。

10. **[#5275](https://github.com/github/copilot-cli/issues/5275) — 在非交互模式下支持默认拒绝的工具权限并配合显式白名单（OPEN，1 条评论）**
    `--deny-tool` 总是覆盖 `--allow-tool`，且某些工具默认被允许，因此 CI 流水线无法强制执行严格白名单。对于任何无人值守运行 CLI 的人来说，这是一项基础性需求。

## 4. 关键 PR 进展
_过去 24 小时内没有 PR 更新。_

## 5. 热门讨论
_本时段未提供讨论数据。_

## 6. 功能请求趋势

- **与交互式 TUI 的 ACP 对齐** 是最明显的新兴主题：将 `contextTier` 作为会话选项（[#4275](https://github.com/github/copilot-cli/issues/4275)）、`ask_user` 扩展方法（[#2109](https://github.com/github/copilot-cli/issues/2109)）、不会终止后台子代理的正确 `session/prompt` 语义（[#4555](https://github.com/github/copilot-cli/issues/4555)），以及使用 OAuth 刷新令牌而非浏览器提示（[#5229](https://github.com/github/copilot-cli/issues/5229)）。集成方希望 ACP 成为一等接口，而不是子集。
- **确定性、策略驱动的非交互模式**：严格的工具白名单（[#5275](https://github.com/github/copilot-cli/issues/5275)）以及将设置继承到子代理（[#4576](https://github.com/github/copilot-cli/issues/4576)）。无头 CI 使用场景正超出当前权限模型的承载能力。
- **配置可发现性**：为 `providers.json` 发布 JSON schema（[#5287](https://github.com/github/copilot-cli/issues/5287)），并添加文档中已有但实际缺失的 `--fusion-tier` 标志（[#5290](https://github.com/github/copilot-cli/issues/5290)）。用户正在逆向工程 BYOK 和模型层级设置。
- **跨平台身份集成**：Linux 密钥存储（[#2165](https://github.com/github/copilot-cli/issues/2165)）、macOS XARA keychain 分区（[#4273](https://github.com/github/copilot-cli/issues/4273)）、Windows Entra broker 令牌缓存（[#5236](https://github.com/github/copilot-cli/issues/5236)），以及沙箱模式下 `gh` 的 GHE 感知代理/令牌转发（[#5286](https://github.com/github/copilot-cli/issues/5286)）。
- **MCP 生命周期成熟度**：正确处理 Enterprise/Entra 范围（[#5061](https://github.com/github/copilot-cli/issues/5061)）、Datadog OAuth 令牌交换（[#5058](https://github.com/github/copilot-cli/issues/5058)），以及通过惰性 schema 加载控制启动 token 成本（[#4613](https://github.com/github/copilot-cli/issues/4613)）。
- **上下文窗口易用性**：可靠的滚动/检查点机制（[#5205](https://github.com/github/copilot-cli/issues/5205)），以及在高 effort 模型上不会于 50% 触发的压缩阈值（[#4571](https://github.com/github/copilot-cli/issues/4571)）。

## 7. 开发者痛点

- **身份认证和平台集成仍是最薄弱环节。** 仅在本时间窗口内，keychain/secret-store 问题就横跨 Ubuntu、macOS 和 Windows，此外还有 Enterprise/数据驻留登录混淆（`*.ghe.com` 被错误标记为 Enterprise Cloud，[#5280](https://github.com/github/copilot-cli/issues/5280)）。企业用户最先且最严重地遇到这些问题。
- **长时间会话中的资源和成本失控。** 37 GiB 的进程占用（[#5254](https://github.com/github/copilot-cli/issues/5254)）、空闲时仍占满 CPU 的失控 `copilot-file-search` 线程（[#4710](https://github.com/github/copilot-cli/issues/4710)），以及 354K token 的 MCP schema 提前注入（[#4613](https://github.com/github/copilot-cli/issues/4613)），都指向后台工作和启动载荷缺乏足够边界限制。
- **非交互/ACP 模式下的静默失败或过早失败。** `session/prompt` 无条件中止会话（[#4555](https://github.com/github/copilot-cli/issues/4555)）、插件自定义代理在 `--prompt` 下激活但在交互模式下不激活（[#4592](https://github.com/github/copilot-cli/issues/4592)），以及 `copilot --cloud` 立即失败并返回不透明的 `internal server error`（[#5289](https://github.com/github/copilot-cli/issues/5289)）。
- **计费/配额不透明。** PRU 被清空的报告（[#4802](https://github.com/github/copilot-cli/issues/4802)）虽然量少但严重性高；与功能开关绑定的配额变更需要更清晰的核算和回滚指引。
- **次要版本之间的回归频发。** `/copy` 现在返回 HTML 而非 Markdown（[#5288](https://github.com/github/copilot-cli/issues/5288)）、10 月的主题更改降低了热力图/高亮的可读性（[#5056](https://github.com/github/copilot-cli/issues/5056)），以及 1.0.80 中压缩行为发生变化（[#4571](https://github.com/github/copilot-cli/issues/4571)），都表明快速发布节奏已超过回归覆盖能力。本时间窗口引用的版本号范围从 `0.0.355` 到 `1.0.105`。
- **长期未关闭的长尾 Issue。** [#552](https://github.com/github/copilot-cli/issues/552) 自 2025 年 11 月起一直处于打开状态，已有 31 条评论且尚未解决——这是一个明显信号：组织级权益缺陷会掉进黑洞，从而打击后续高质量报告的积极性。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区摘要 — 2026-10-30

## 1. 今日亮点
24 小时内发布了两个版本：**v2.2.2** 为提供图像模型的供应商默认启用图像生成；**v2.2.1** 新增 `/goal`，用于目标驱动的会话，持续运行直到审查者确认完成。跟踪器中主要是免费套餐/配额混淆（大型讨论帖已有 104 条评论）以及 v2.2.1 会话卡在 “Working” 的报告。与此同时，维护者正在推进一批核心工作：无需 tree-sitter 的 shell 权限扫描器、Code Mode 计划检查，以及 TUI 中的按引用媒体 blob。

## 2. 发布

- **[v2.2.2](https://github.com/anomalyco/opencode/releases)** — *默认图像生成*：当已连接的供应商支持图像模型时，代理可调用 `experimental_image_generate`，无需额外配置。首选模型可通过 `experimental.image_generate.model` 配置（[#60258](https://github.com/anomalyco/opencode/pull/60258)）。
- **[v2.2.1](https://github.com/anomalyco/opencode/releases)** — *持续朝着目标工作*：TUI/Desktop 中的 `/goal <objective>` 会让会话持续运行，直到审查者确认目标已达成；`/goal pause|resume|clear` 控制循环（[#59437](https://github.com/anomalyco/opencode/pull/59437)）。
- **[process-daemon v0.3.3](https://github.com/anomalyco/opencode/releases)** — `opencode-pty 0.3.3`（协议 7）来自 `packages/process-daemon`，以 `@opencode/pty@0.3.3` 发布到 npm。

发布 PR：**[#60337 release: v2.2.2](https://github.com/anomalyco/opencode/pull/60337)** 将版本号和变更日志合并回 `dev`。

## 3. 热门 Issue

1. **[#59387 Free tier issues: read this first](https://github.com/anomalyco/opencode/issues/59387)** — *104 条评论，9 👍*。免费套餐失败的统一入口：“Free usage exceeded”、永不发生的重置，以及 Desktop 版本不匹配。仓库中互动量最高的讨论帖，也是最清晰的信号：配额提示信息需要改进。
2. **[#33356 Unbounded growth of the `event` table (13GB+ opencode.db)](https://github.com/anomalyco/opencode/issues/33356)** — *45 条评论，12 👍*。长期运行的实例膨胀到约 13 GB，因为 `message.updated.1` 快照从未被清理或压缩，使卷使用率达到 97–99%。票数最高的问题；对无头部署而言是真实的运维风险。
3. **[#58786 Desktop sessions hang in Working/Thinking after Oct 22 Bun runtime update](https://github.com/anomalyco/opencode/issues/58786)** — 在全新会话中可复现，未暴露错误。指向运行时迁移，而非会话损坏。
4. **[#60330 v2.2.1 stalls at "Working" all day in OpenCode GO](https://github.com/anomalyco/opencode/issues/60330)** — 针对当前版本的新报告；一条简单的 “Test” 消息出现 15 分钟延迟，而 Console 构建正常。表明可能存在回归，值得对照 v2.2.2 做 bisect。
5. **[#56288 `external_directory` ask is skipped for `shell`](https://github.com/anomalyco/opencode/issues/56288)** — *已复现，严重性：高*。文件工具会执行该规则，shell 不会；工作区外的路径可被静默写入。与 PR #60332 中移除 tree-sitter 的工作直接相关。
6. **[#46371 Hidden LLM calls billed but absent from session cost](https://github.com/anomalyco/opencode/issues/46371)** — 标题生成和摘要会调用 `LLM.stream()`，但从不持久化 token 使用量；账单层面的证据让一个已自动关闭的报告重新受到关注。成本透明度是反复出现的信任问题。
7. **[#57012 Allow insecure HTTP for authenticated remote MCP servers on internal networks](https://github.com/anomalyco/opencode/issues/57012)** — v2.0 对已认证的 MCP 严格执行 TLS；内网用户被阻塞。PR #60039（按服务器 TLS 信任）是上游的应对方案。
8. **[#60320 Active Go subscriber hard-blocked by rate limit on Beam Free](https://github.com/anomalyco/opencode/issues/60320)** — 付费账户，但宣传为不限量的 `beam` 返回无法摆脱的限流错误。与 [#60317](https://github.com/anomalyco/opencode/issues/60317) 中永不结束的重试倒计时相呼应。
9. **[#7487 `exec` variable substitution](https://github.com/anomalyco/opencode/issues/7487)** — *8 条评论，5 👍*，自 1 月起一直开放。长期请求：在 `exec` 中复用配置变量；这是一个反复出现的小型配置易用性缺口。
10. **[#46378 Unicode `×` (U+00D7) triggers HTTP 400 on GLM-5.3-Flash](https://github.com/anomalyco/opencode/issues/46378)** — 标准字符在网关确定性触发 `[1210] API parameter invalid`。一个范围窄但完全可复现的供应商兼容性 bug。

同样值得关注：[#46035 MCP children accumulate until OOM](https://github.com/anomalyco/opencode/issues/46035)（已关闭）、[#46164 `/compact` lacks a context-fit check](https://github.com/anomalyco/opencode/issues/46164)，以及 [#60328 free usage exceeded with zero usage](https://github.com/anomalyco/opencode/issues/60328)。

## 4. 关键 PR 进展

1. **[#60332 refactor(core): finish moving shell permission checks off tree-sitter](https://github.com/anomalyco/opencode/pull/60332)** — Shell 权限检查现在在所有渠道上都运行于内置扫描器，移除 2.3 MB 内嵌的 tree-sitter WASM，并修复八个 shell 解析边界情况。直接解决 #56288/#46398 中的一类绕过问题。
2. **[#60140 feat(core): Code Mode checks with static tool scanning for schedules](https://github.com/anomalyco/opencode/pull/60140)** — 计划可在唤醒会话前运行 JavaScript `if`/`until` 检查，无需调用模型，也无需维护允许列表。位于 `experimental.*` 之后。基于已合并的 #60137。
3. **[#60028 feat(core): let a Code Mode check decide when a schedule fires](https://github.com/anomalyco/opencode/pull/60028)** — #60140 的已关闭前身：`if: { type: "code", code, allow }` 会评估 `state`、`now` 和 `runs`，并返回 `{ wake, state, message? }`。
4. **[#60116 feat(tui): load stored images by reference, like desktop](https://github.com/anomalyco/opencode/pull/60116)** — TUI 按引用请求已存储的图像，仅在显示时下载，与 Desktop 一致。仅在 `experimental.media_blob` 下生效；对于大图像会话是重要一步。
5. **[#60102 fix(core): keep permission reasons and feedback in MCP tool failures](https://github.com/anomalyco/opencode/pull/60102)** — 拒绝此前会被压缩为 `Unable to execute <server>_<tool>`，从而对模型隐藏规则和用户反馈。拒绝后能更好地自我纠正。
6. **[#60120 fix(core): send execute progress at most every 100 ms](https://github.com/anomalyco/opencode/pull/60120)** — 嵌套的 `execute` 调用此前会发出 2N 个持续增长的快照；限流可降低带宽占用和大型程序上的 UI 抖动。
7. **[#60039 feat(mcp): per-server TLS trust for remote MCP servers](https://github.com/anomalyco/opencode/pull/60039)** — 为每个远程服务器新增 `tls` 配置块（`ca_file` 等）；先支持显式信任，后续支持首次使用即信任。这是对 #57012 的受支持答案。
8. **[#60315 feat(core): integration.connect and integration.use policies](https://github.com/anomalyco/opencode/pull/60315)** — 面向 Console 工作区的、可由 MDM 强制执行的组织策略；取代 `OPENCODE_CONSOLE_REQUIRE_ORG`（#58159）。企业部署正成为一等关注点。
9. **[#60084 fix(core): require one-way V1 upgrade acknowledgment](https://github.com/anomalyco/opencode/pull/60084)** — 启动导入 V1 历史前进行一次确认，明确采用 V2 适用于每个项目。减少迁移意外。
10. **[#60323 refactor(client): share the persistent pty protocol](https://github.com/anomalyco/opencode/pull/60323)** — 将持久 PTY socket 协议从 TUI 面板移入 `@opencode/client/solid`，以便 Desktop 终端复用（与 #60322/#60329 堆叠）。

UI 层修复推进迅速：[#60335 mobile question options/submit reachable](https://github.com/anomalyco/opencode/pull/60335)、[#60336 `#` in file search base](https://github.com/anomalyco/opencode/pull/60336)、[#60334 add-menu shortcuts inside bounds](https://github.com/anomalyco/opencode/pull/60334)、[#60333 Markdown frontmatter as YAML block](https://github.com/anomalyco/opencode/pull/60333)、[#60221 group added projects in settings](https://github.com/anomalyco/opencode/pull/60221)。

## 6. 功能请求趋势

- **供应商与传输可配置性** — 任意 LLM 的自定义 base URL/API key（[#59972](https://github.com/anomalyco/opencode/issues/59972)）、已认证内网 MCP 的不安全 HTTP（[#57012](https://github.com/anomalyco/opencode/issues/57012)）、按服务器 TLS 信任（[#60039](https://github.com/anomalyco/opencode/pull/60039)）。用户越来越多地在企业网络和私有网关后运行 OpenCode。
- **可编程自动化原语** — Code Mode 计划条件（[#60028](https://github.com/anomalyco/opencode/pull/60028)、[#60140](https://github.com/anomalyco/opencode/pull/60140)）和 `exec` 变量替换（[#7487](https://github.com/anomalyco/opencode/issues/7487) —— 投票最高的开放功能请求）表明用户需要无需模型往返的配置即代码。
- **长时运行/代理式会话控制** — v2.2.1 中的 `/goal` 将目标驱动循环正式化；计划加上 Code Mode 检查将同一理念扩展到无人值守运行。
- **成本与配额透明度** — 隐藏的标题/摘要 LLM 调用未计入会话成本（[#46371](https://github.com/anomalyco/opencode/issues/46371)），以及反复出现的免费套餐计量投诉。
- **企业策略控制** — 组织要求的 Console 登录（[#58159](https://github.com/anomalyco/opencode/pull/58159)）以及集成 connect/use 策略（[#60315](https://github.com/anomalyco/opencode/pull/60315)）。
- **媒体效率** — 按引用加载图像（[#60116](https://github.com/anomalyco/opencode/pull/60116)）以及 v2.2.2 中的默认图像生成。

## 7. 开发者痛点

- **配额与限流不透明** — 最响亮的主题：[#59387](https://github.com/anomalyco/opencode/issues/59387)（104 条评论）、[#60317](https://github.com/anomalyco/opencode/issues/60317)、[#60320](https://github.com/anomalyco/opencode/issues/60320)、[#60328](https://github.com/anomalyco/opencode/issues/60328)、[#59975](https://github.com/anomalyco/opencode/issues/59975)。症状包括免费套餐重置从不触发、付费账户在“不限量”模型上被阻塞，以及重试倒计时无限循环。
- **无诊断信息的卡死** — Bun 运行时切换后 Desktop 会话卡在 Working/Thinking（[#58786](https://github.com/anomalyco/opencode/issues/58786)），以及 v2.2.1 在琐碎提示上停滞数分钟（[#60330](https://github.com/anomalyco/opencode/issues/60330)）。未暴露任何错误，导致分诊困难。
- **本地状态增长与进程泄漏** — `event` 表无界增长至 13 GB（[#33356](https://github.com/anomalyco/opencode/issues/33356)）、MCP 子进程累积直至 OOM（[#46035](https://github.com/anomalyco/opencode/issues/46035)）、断连时 MCP 后代进程成为孤儿（[#46253](https://github.com/anomalyco/opencode/issues/46253)）。
- **权限执行缺口** — 在 POSIX 和 PowerShell 上可通过 shell 绕过 `external_directory`（[#56288](https://github.com/anomalyco/opencode/issues/56288)、[#46398](https://github.com/anomalyco/opencode/issues/46398)）；拒绝原因在 MCP 包装器中丢失（#60102）加剧了困惑。
- **计费与成本核算** — 标题/摘要生成产生真实供应商费用，却从未出现在会话成本中（[#46371](https://github.com/anomalyco/opencode/issues/46371)）。
- **供应商/模型边界情况** — Unicode `×` 导致的确定性 400（[#46378](https://github.com/anomalyco/opencode/issues/46378)），以及启用 MCP 时某些模型拒绝递归 JSON schema（[#45823](https://github.com/anomalyco/opencode/issues/45823)）。
- **压缩可靠性** — 手动 `/compact` 在未做上下文适配检查的情况下流式传输完整历史，导致上游请求失败（[#46164](https://github.com/anomalyco/opencode/issues/46164)）。
- **迁移摩擦** — V1→V2 导入需要显式确认（[#60084](https://github.com/anomalyco/opencode/pull/60084)）；多个“再也无法添加自定义 URL/API key”的报告（[#59972](https://github.com/anomalyco/opencode/issues/59972)）表明 v2 中供应商设置路径出现了回归。

*注：未提供 Discussion 数据，因此省略热门讨论部分。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 社区摘要 — 2026-10-30

**来源：** [github.com/earendil-works/pi](https://github.com/earendil-works/pi)  
**统计窗口：** 过去 24 小时（数据截至 2026-10-29）

## 今日亮点

过去 24 小时内没有发布新的 Pi 版本。活动主要集中在提供商兼容性和提示缓存正确性上：OpenRouter 上下文长度限制导致的 400 错误（[#10497](https://github.com/earendil-works/pi/issues/10497)）是评论最多的问题；动态工具排序/系统提示变更（[#10024](https://github.com/earendil-works/pi/issues/10024)、[#11529](https://github.com/earendil-works/pi/issues/11529)）以及发送给兼容提供商的 OpenAI 专有字段（[#9508](https://github.com/earendil-works/pi/issues/9508)）继续造成成本和错误处理问题。长时间会话稳定性也显著凸显：一份 V8 OOM 崩溃报告（[#11570](https://github.com/earendil-works/pi/issues/11570)）和一处渲染路径性能回归（[#11567](https://github.com/earendil-works/pi/issues/11567)）；同时社区重点介绍了一个 Pi 无头核心的 Rust 移植（[#11503](https://github.com/earendil-works/pi/discussions/11503)）。

## 热门 Issue

1. **[#10497](https://github.com/earendil-works/pi/issues/10497) — OpenRouter 错误：400** `[OPEN, bug, inprogress]`  
   OpenRouter 请求中的上下文长度溢出会以原始 `400` 错误暴露出来，尤其是对于将文件内容注入上下文的扩展。该问题有 13 条评论，是统计窗口内讨论最多的问题，表明需要更好的预检 token 计量和提供商错误归一化。

2. **[#9656](https://github.com/earendil-works/pi/issues/9656) — 在 Windows + Zellij 上全屏时，鼠标滚轮滚动的是提示历史而不是对话记录** `[OPEN, bug]`  
   这是 Windows → Alacritty → Zellij 特有的终端输入处理不一致。该问题有 12 条评论和 5 个 👍，是开放 bug 中反应数最高的，表明多路复用器兼容性是切实的 UX 痛点。

3. **[#9508](https://github.com/earendil-works/pi/issues/9508) — pi-ai 向兼容提供商发送不受支持的 OpenAI 专有请求字段/角色/认证信息** `[OPEN, bug]`  
   第三方 OpenAI 兼容提供商以 `400/422` 拒绝 Pi 请求，因为 OpenAI 专有字段、角色或认证头发生了泄漏。自 9 月以来有 9 条评论，表明这是持续存在的互操作缺口，而不是一次性的提供商问题。

4. **[#10024](https://github.com/earendil-works/pi/issues/10024) — 运行中工具集变更会移动系统提示开头并重新计费对话** `[OPEN]`  
   动态工具选择会根据实时工具集重新推导渲染出的工具项目符号列表，从而在一次运行期间改变系统提示并使提示缓存失效。5 条评论和 2 个 👍 反映了用户对成本的敏感关注。

5. **[#11157](https://github.com/earendil-works/pi/issues/11157) — 在 `session_start` 时执行 `sendMessage` 的扩展会把每个会话变成旧式对话记录** `[OPEN, inprogress, prio:p0]`  
   在 Pi 系统消息之前注入消息的扩展会破坏对话记录假设，包括 Anthropic 的 `system` 字段行为。p0 标签和 3 条评论表明，核心/扩展之间的排序契约需要被明确化。

6. **[#11570](https://github.com/earendil-works/pi/issues/11570) — 长时间会话中的 V8 OOM（SIGABRT）** `[CLOSED, no-action]`  
   长时间运行的会话（约 8 MB 会话文件、2 天以上）会崩溃，报 `FatalProcessOutOfMemory`，原因是 `flatMap` 内巨大的 `ConsString` 展平/正则替换。已有 5 份生产环境崩溃报告；尽管以 no-action 关闭，这仍是高严重性的稳定性信号。

7. **[#11527](https://github.com/earendil-works/pi/issues/11527) — Bedrock：每个请求都会创建一个新的 `BedrockRuntimeClient`** `[OPEN]`  
   每次模型调用都会创建新的客户端、凭证提供程序和 HTTP/2 会话。使用 SSO 配置文件时，这可能对每个请求触发一次 `GetRoleCredentials` 往返，增加延迟和凭证频繁更替。

8. **[#11529](https://github.com/earendil-works/pi/issues/11529) — 工具顺序取决于注册顺序，因此相同工具也可能击穿提示缓存** `[OPEN]`  
   `getCurrentTools()` 返回插入顺序，因此重新连接或通过 `tool_search` 加载的工具会移动到映射末尾。这会破坏提示缓存稳定性，并直接关联到 #10024 中的成本问题。

9. **[#11567](https://github.com/earendil-works/pi/issues/11567) — 长时间会话中输入变慢：`getSessionName()` 在每次渲染时扫描每个条目** `[CLOSED, bug, no-action]`  
   在约 40 万个条目时，按键到渲染的 p50 从 1.5 ms 上升到 21 ms，忙碌 CPU 的 94% 花在 `SessionManager.getSessionName()` 中。该问题以 no-action 关闭，但性能剖析很具体，且很可能再次出现。

10. **[#11538](https://github.com/earendil-works/pi/issues/11538) — google-generative-ai：带有独立思考签名的流式片段被合并或丢弃** `[OPEN]`  
   Google 流解析器会合并文本/思考片段，并且只保留最后一个 `thoughtSignature`，从而丢失思考连续性的重放保真度。只有两条评论，但提供商侧的正确性问题往往影响多个模型。

## 关键 PR 进展

1. **[#11545](https://github.com/earendil-works/pi/pull/11545) — Anthropic 消息线程** `[OPEN]`  
   增加对 Anthropic 服务端消息线程的支持：当设置了会话 ID 且缓存开启时，Pi 每轮可以只发送新消息，而不是完整历史。这可能显著降低 token 用量和成本。

2. **[#11562](https://github.com/earendil-works/pi/pull/11562) — 在 cwd 的默认目录中启动新会话** `[OPEN]`  
   修复当使用来自另一个项目的 cwd 打开会话时的会话存储语义。`/new`、`/fork` 和 `/clone` 现在使用会话 cwd 的默认文件夹，而不是把旧文件夹当作自定义 `--session-dir`。

3. **[#11546](https://github.com/earendil-works/pi/pull/11546) — 将 `pi.exec` 输出限制在 256 MiB** `[CLOSED]`  
   通过 `ExecOptions.maxBuffer` 限制合并后的 stdout/stderr，终止超限命令，并返回 `truncated`/`killed` 状态。这是防止代理执行的命令失控占用内存的实用保护措施。

4. **[#11577](https://github.com/earendil-works/pi/pull/11577) — 调整图像大小时选择 PNG 和 JPEG 中更小者** `[CLOSED]`  
   修复调整大小路径在 PNG 满足字节限制时总是优先选择 PNG 的问题，即使 JPEG 小得多。直接处理 [#11550](https://github.com/earendil-works/pi/issues/11550)，并避免不必要的载荷膨胀。

5. **[#11572](https://github.com/earendil-works/pi/pull/11572) — 不要重试 Zhipu 使用量限制错误（代码 1308）** `[CLOSED]`  
   Zhipu/Z.ai 套餐上限会返回 HTTP 429 和代码 `1308`；此前通用的 429 模式会让 Pi 徒劳重试。该修复将配额上限与瞬时速率限制区分开来。

6. **[#11565](https://github.com/earendil-works/pi/pull/11565) — 在常规模式下停止写入 OSC 133 提示符标记** `[CLOSED]`  
   防止 TUI 消息被会显示 OSC 7501 程序状态的终端解释为 shell 提示符，例如 Rex 和较新的 iTerm2。修复“working”指示器消失的问题。

7. **[#11556](https://github.com/earendil-works/pi/pull/11556) — 让 SDK 流为摘要解析认证** `[CLOSED]`  
   修复 `createAgentSession` 会话中的压缩、分支摘要和 bug 报告摘要：让 `modelRuntime.streamSimple` 解析已存储的 OAuth 凭证，而不是将访问令牌作为 `apiKey` 传入。

8. **[#11544](https://github.com/earendil-works/pi/pull/11544) — 守护进程终止时杀掉其命令** `[CLOSED]`  
   防止本地 Unix 守护进程关闭时留下孤立命令：守护进程现在处理 `SIGTERM`，以便运行 `kill_all`，而不是在清理前直接退出。

9. **[#11543](https://github.com/earendil-works/pi/pull/11543) — 在 `stripAnsi` 中剥离私有参数 CSI 序列** `[CLOSED]`  
   修复对带有私有前缀字节（`<`、`=`、`>`）的序列的 ANSI 剥离，使 SGR 鼠标报告和次级设备属性不再将 `35;59;1M` 之类的片段泄漏到渲染文本中。

10. **[#11571](https://github.com/earendil-works/pi/pull/11571) — 当 npm 包更新后安装版本未变化时发出警告** `[CLOSED]`  
    处理 `pi update --extensions` 期间 `npm view` 与 `npm install <name>@latest` 之间的注册表缓存不一致，使用户能看到原本静默无操作的更新。

## 热门讨论

**展示与分享**

- **[#11503](https://github.com/earendil-works/pi/discussions/11503) — pi-rs：无头核心的 Rust 移植**  
  一个社区对 Pi 0.74.2 无头核心（Agent 循环、七个内置工具、会话 JSONL、CLI 接口、系统提示）的 Rust 移植，行为一致性经过“逐个原子”验证。作者还分享了一个 DeepSeek API 兼容性发现。1 条评论和 1 个 👍。

**问答**

- **[#11574](https://github.com/earendil-works/pi/discussions/11574) — 如何将 npmjs 包上传到 Pi 包源？**  
  一位包作者询问如何向社区发布并分享 Pi 包。缺少显而易见的答案，凸显了第三方包分发在文档/可发现性方面的缺口。

## 功能请求趋势

- **提供商抽象加固：** 为兼容提供商清理 OpenAI 专有字段（[#9508](https://github.com/earendil-works/pi/issues/9508)），保留 Google 思考签名（[#11538](https://github.com/earendil-works/pi/issues/11538)），复用 Bedrock 客户端（[#11527](https://github.com/earendil-works/pi/issues/11527)），并正确处理提供商特定的认证元数据。
- **提示缓存稳定性与成本核算：** 稳定的系统提示开头和工具排序（[#10024](https://github.com/earendil-works/pi/issues/10024)、[#11529](https://github.com/earendil-works/pi/issues/11529)），Bedrock 缓存预热（[#11528](https://github.com/earendil-works/pi/issues/11528)），OpenRouter 会话 ID（[#10022](https://github.com/earendil-works/pi/issues/10022)），以及权威的 OpenRouter 成本/BYOK 数据（[#8940](https://github.com/earendil-works/pi/issues/8940)）。
- **长时间会话可靠性：** OOM 崩溃（[#11570](https://github.com/earendil-works/pi/issues/11570)）、渲染时扫描（[#11567](https://github.com/earendil-works/pi/issues/11567)）、上下文用量核算（[#11534](https://github.com/earendil-works/pi/issues/11534)），以及 token 估算钳制（[#10988](https://github.com/earendil-works/pi/issues/10988)）。
- **MCP 与工具发现：** 按命名空间限定的 `tool_search` 查询（[#11558](https://github.com/earendil-works/pi/issues/11558)）、健壮的 `WWW-Authenticate` 解析（[#11539](https://github.com/earendil-works/pi/issues/11539)），以及为缓存稳定性提供确定性的工具排序。
- **扩展契约与打包：** 明确的 `session_start` 消息排序规则（[#11157](https://github.com/earendil-works/pi/issues/11157)）、可恢复的不支持图像格式（[#11552](https://github.com/earendil-works/pi/issues/11552)）、可配置的 OAuth/Copilot 超时（[#11549](https://github.com/earendil-works/pi/issues/11549)），以及更清晰的包发布指引（[#11574](https://github.com/earendil-works/pi/discussions/11574)）。
- **终端 UX 可移植性：** Windows/Zellij 滚轮处理（[#9656](https://github.com/earendil-works/pi/issues/9656)）、Apple Terminal 的 `Shift+Enter` 行为（[#11559](https://github.com/earendil-works/pi/issues/11559)）、RTL 渲染（[#11580](https://github.com/earendil-works/pi/pull/11580)），以及更干净的 OSC/CSI 处理（[#11565](https://github.com/earendil-works/pi/pull/11565)、[#11543](https://github.com/earendil-works/pi/pull/11543)）。

## 开发者痛点

- **提供商特定的 400/422 失败仍是反复出现的负担。** OpenAI 兼容端点、OpenRouter 上下文限制、Google 思考签名、Bedrock 凭证和 Zhipu 配额错误都需要按提供商分别处理，而不是走通用请求路径。
- **提示缓存失效代价高昂且难以察觉。** 动态工具选择、注册顺序变化和系统提示开头移动可能会静默地重新计费对话；用户要求确定性排序和更好的成本可见性。
- **长时间会话会退化或崩溃。** 大型会话文件会触发 V8 OOM、每次渲染扫描和上下文核算问题，使多天的代理会话存在风险。
- **扩展可能违反核心假设。** 在 `session_start` 注入消息、使用带 `tools.` 前缀的名称配合小型本地模型，或发出不支持的图像格式，都可能破坏对话记录或提供商请求。
- **终端和多路复用器差异会造成不一致的 UX。** Windows/Zellij、Apple Terminal、RTL 文本和 OSC/CSI 序列都会产生平台特定行为，用户难以诊断。
- **会话存储与恢复语义令人困惑。** 从另一个项目打开会话可能会改变 `/new`、`/fork` 和 `/clone` 的保存位置，而且 `--session-dir` 检测曾被误认为自定义存储。
- **社区包分发缺乏清晰路径。** npm 包发布问题以及 Gondolin 打包修复（[#11582](https://github.com/earendil-works/pi/pull/11582)）都指向扩展作者的上手/文档摩擦。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区简报 — 2026-10-30

**来源：** [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) · 数据窗口：截至 2026-10-29 的更新

---

## 1. 今日亮点

CLI 发布了 **v0.26.4**，这是一个轻量版本，唯一面向用户的功能是生成式 UI 视图继承宿主主题；配套的 TypeScript SDK **v0.1.26** 和 **Desktop v0.26.4** 同步发布。工程投入几乎完全集中在 **CI 与发布可靠性** 上：在评论数最多的 20 个 PR 中，超过一半是基础设施加固（macOS 测试套件分片、Web Shell 冒烟测试隔离、runner 路由、Maven 缓存正确性、发布通知器对账）。最具实质内容的开放讨论仍是 **自托管模型的上下文不可变性**（#14215），其中低提示处理速度使可变上下文成本高昂。

---

## 2. 发布

| 版本 | 说明 |
|---|---|
| **v0.26.4**（[release](https://github.com/QwenLM/qwen-code/releases)） | 主要 CLI 版本。无已知破坏性变更。功能：`feat(generated-ui): follow the host theme in generated views`（[#15798](https://github.com/QwenLM/qwen-code/pull/15798)）。发布说明正文为占位符（`_See the complete change list below._`），因此变更日志实际上就是 PR 列表。 |
| **sdk-typescript-v0.1.26** | 捆绑 CLI **0.26.4**，使用与 SDK 相同的分支/ref 构建。发布说明正文仍包含引用 CLI **0.26.3** 的过时文本，表明存在值得清理的模板/自动化产物。 |
| **desktop-v0.26.4** | 包含 @yiliang114 的 `fix(config): report controls that were silently dropped`（[#15794](https://github.com/QwenLM/qwen-code/pull/15794)），以及托管会话文档更新。 |
| **v0.26.3-nightly.20261028.ca204559a7** | 从 `release/v0.26.3-nightly.20261028.ca204559a7` 切出的 nightly；包含相同的 `fix(config)` 变更和托管文档编辑。 |

**要点：** 一次协调一致的 CLI + SDK + Desktop 0.26.4 发布。唯一净新增产品能力是生成式视图的主题继承；其他内容均继承自 0.26.3。

---

## 3. 热门 Issue

> 24 小时窗口内仅更新了 **3 个 issue**，因此覆盖全部三个，而非筛选 top-10。

1. **[#14724](https://github.com/QwenLM/qwen-code/issues/14724) — 主 CI 失败：Managed Agent 门禁，未识别到测试** · `OPEN` · `type/bug`, `autofix/skip` · **84 条评论**
   一个由机器人提交的主分支 CI 失败，现已开放 10 天，有 84 条评论且无 👍。一个带有 `autofix/skip` 标签的条目却有极高评论数，这表明是自动化循环或反复人工分诊，而非真正的社区讨论——它是跟踪器中噪声最高的单项。

2. **[#14215](https://github.com/QwenLM/qwen-code/issues/14215) — 自托管模型的上下文不可变性** · `OPEN` · `P2`, `feature-request`, `performance`, `memory`, `caching`, `context-performance`, `need-discussion` · **7 条评论，1 个 👍**
   该窗口内最具实质内容的社区请求。报告者认为，memories、dreams、suggestions 和 sessions 等功能都假设提示处理速度很快；在预填充缓慢的自托管硬件上，可变上下文会变得过于昂贵。请求的行为是一种不可变上下文模式，可保留前缀缓存命中。标记为 `need-discussion`，因此维护者意见是阻塞点。

3. **[#15251](https://github.com/QwenLM/qwen-code/issues/15251) — Fleet Shepherd 看板** · `OPEN` · **0 条评论**
   仓库 agent 集群的自动维护运营看板。其当前状态值得注意：本次 tick 报告 **2 个 autofix 运行卡在 `queued`**（最旧为 2026-10-...），并且 `syncs: 0 · dispatches: 0 · releases: 0`。这实际上是一个公开健康信号，表明 autofix 流水线已停滞。

---

## 4. 关键 PR 进展

1. **[#15871](https://github.com/QwenLM/qwen-code/pull/15871) — refactor(managed-agent): 将服务器拆分为 Maven 模块** (@doudouOUC)
   将 Managed Agent Server 分解为六个生产 Maven 模块和一个未发布的验证模块，并使用框架无关的契约定义控制平面编排、Runtime Broker 编排、持久化和适配器之间的边界。这是进行中最大的架构变更。

2. **[#15870](https://github.com/QwenLM/qwen-code/pull/15870) — refactor(managed): 移除持久化的公开消息快照** (@doudouOUC)
   从托管服务器中移除持久化的公开消息快照——这是一种数据模型简化，可能减少存储增长和快照/流式结果分歧。

3. **[#11854](https://github.com/QwenLM/qwen-code/pull/11854) — feat: 添加混合代码模式** (@DragonnZhang)
   长期运行（自 2026-09-14 起）的功能，新增与 Codex 对齐的 `tools.mode` 枚举：`direct`、`code_mode`、`code_mode_only`。在 `code_mode` 下，普通工具仍可直接调用，同时还暴露一个隔离的 `exec` JavaScript 工具，支持嵌套 JS 声明。这是审查中最重大的能力新增。

4. **[#15887](https://github.com/QwenLM/qwen-code/pull/15887) — feat(serve): 无需重启即可从设置中启用远程访问** (@yiliang114)
   为运行中的 `qwen serve` 添加 **Settings → Connections → Allow remote connections**。远程访问默认关闭；本地操作员可以实时启用，然后将地址和单独的 bearer token 复制到另一个 Web Shell 的连接表单中。对守护进程工作流是重要的 UX 改进。

5. **[#15634](https://github.com/QwenLM/qwen-code/pull/15634) — feat(channels): 将注入消息投递到正在运行的 turn** (@Eric-GoodBoy-Tech)
   新增第四种 channel `dispatchMode`——`inject`：在 turn 中途到达的消息会进入运行中 turn 的 turn 中途队列，并在下一个工具批次边界被读取，而不是缓冲到 turn 结束。直接解决了 channel 会话中的 agent 响应性问题。

6. **[#15888](https://github.com/QwenLM/qwen-code/pull/15888) — fix(ci): 将完整 macOS 测试套件划分为有界作业** (@yiliang114)
   将 macOS CI 拆分为七个作业（三个 CLI 分片、两个核心分片、其余 workspace 套件、独立/运行时脚本），并保留原始检查作为聚合门禁。基于 #15884/#15883 堆叠。这是对 macOS 套件超时的直接响应。

7. **[#15886](https://github.com/QwenLM/qwen-code/pull/15886) + [#15884](https://github.com/QwenLM/qwen-code/pull/15884) — Web Shell 冒烟测试隔离** (@yiliang114)
   #15886 将每次准入运行的浏览器冒烟测试固定到 `ubuntu-latest`，与共享 Linux runner 集群解耦；#15884 将 Chromium 配置文件和共享内存临时文件移动到 runner 临时目录。两者共同针对 #15060 中跟踪的反复出现的冒烟测试失败。

8. **[#15885](https://github.com/QwenLM/qwen-code/pull/15885) — fix(ci): 通过 pool-first runner 表达式路由 E2E 构建作业** (@yiliang114)
   使 E2E 共享构建作业与全仓库路由约定保持一致：启用时优先使用自托管 `ecs-qwen`，回退到托管 Ubuntu，并加上标准的自托管磁盘设置。修复了一处路由不一致。

9. **[#15854](https://github.com/QwenLM/qwen-code/pull/15854) — perf(release): 跨发布复用已验证的原生音频预构建** (@yiliang114)
   当构建输入匹配时，复用成功官方主发布中的原生音频预构建；经校验的缓存命中会跳过整个原生构建矩阵，任何查找/下载/校验失败都会回退为重新构建全部五个目标。这是明显的发布延迟收益。

10. **[#15829](https://github.com/QwenLM/qwen-code/pull/15829) — fix(vscode): 写入 provider 配置时保留同级模型设置** (@2SinceJuly)
    修复了一个真实的数据丢失 bug：从 VS Code 配套扩展配置 Coding Plan 或 provider 时，会用仅含 `name` 的内容重写 `settings.model`，静默删除同级键。现在会逐键写入 `name` 及其配对的 `baseUrl`。**diff 虽小，用户影响却很大。**

**同样值得关注：** [#15852](https://github.com/QwenLM/qwen-code/pull/15852)（发布通知器仅在真实失败时创建 issue，并对陈旧 issue 进行对账）、[#15730](https://github.com/QwenLM/qwen-code/pull/15730)（用于 publish checkout 的 job token）、[#15274](https://github.com/QwenLM/qwen-code/pull/15274) / [#15286](https://github.com/QwenLM/qwen-code/pull/15286)（Maven 缓存/结果保存加固，均为 `autofix/needs-human`）、[#15771](https://github.com/QwenLM/qwen-code/pull/15771)（Fleet Shepherd 看板上的 Actions 队列普查）、[#11486](https://github.com/QwenLM/qwen-code/pull/11486)（`qwen update --target-version`）。

---

## 5. 热门讨论

*省略——此数据集中未提供 Discussion 数据。*

---

## 6. 功能请求趋势

- **自托管部署的上下文与缓存经济性。** #14215 是最清晰的信号：前缀缓存保留、上下文不可变性和更低的预填充成本。`roadmap/context-performance` + `scope/memory` + `scope/caching` 标签簇表明这是公认的路线图轴线，而非一次性需求。
- **工具调用架构。** #11854（`tools.mode`：`direct` / `code_mode` / `code_mode_only`）指向与 Codex 对齐的模型：工具既可直接调用，也可从隔离的 JS `exec` 沙箱中调用。
- **实时/远程服务易用性。** #15887 希望为 `qwen serve` 提供基于 token 认证的零重启远程访问——守护进程正被视为一等部署目标。
- **turn 中途消息注入。** #15634 请求在 channel 会话中提供可中断、感知工具边界的消息投递，而非在 turn 结束时缓冲。
- **确定性、可离线安装。** #11486（无需 npm 发现机制的 `--target-version`）反映出对固定、可复现独立安装的需求，包括自定义 `QWEN_UPDATE_BASE_URL` 镜像。
- **编辑器集成保真度。** #15829 表明 VS Code 配套扩展的配置写入必须不破坏同级设置——这是一类“不要弄丢我的配置”的请求。

---

## 7. 开发者痛点

1. **CI 不稳定是主要负担。** 前 20 个 PR 中至少有 8 个是 CI 修复。反复出现的主题包括：共享 runner 网络争用（#15886）、Web Shell 冒烟测试中的 Chromium 临时文件/共享内存行为（#15884）、macOS 套件时长（#15888）、runner 路由不一致（#15885），以及 Maven 缓存写回失败模式（#15274、#15286）。贡献者正在把评审带宽花在测试基础设施上，而不是产品代码上。
2. **Autofix 自动化正在停滞，而非提供帮助。** Issue #15251 报告 **2 个 autofix 运行卡在 `queued`**；#14724 在一个主 CI 失败上已累积 **84 条评论**；两个 `autofix/needs-human` PR（#15274、#15286）自 2026-10-22 起一直开放。机器人产生了大量产出，但越来越大的比例需要人工救援。
3. **发布自动化误报。** #15852 记录到，两个扇出发布通知器都把 **cancelled** 运行视为失败并创建 issue，而且当后续尝试发布成功时，二者都无法关闭这些 issue。再加上 v0.26.4 的占位发布说明以及 0.1.26 SDK 发布正文中过时的“0.26.3”文本，发布元数据正在与现实脱节。
4. **静默配置变更破坏用户状态。** 同一窗口内有两个独立工单——Desktop 的 `fix(config): report controls that were silently dropped`（#15794）和 VS Code 的 `settings.model` 覆盖（#15829）——表明存在系统性模式：写入方替换配置对象，而不是合并键。
5. **自托管用户感觉像二等公民。** #14215 直接表达了这种挫败感：前沿功能（memories、dreams、suggestions、sessions）围绕快速托管提示处理设计，在较慢的自托管硬件上严重退化。
6. **发布说明不透明或缺失。** v0.26.4 的变更日志以 `_See the complete change list below._` 形式发布，迫使用户从 PR 列表重建变更内容。

---

*本简报仅根据 GitHub 元数据生成。Issue/PR 正文在源数据中被截断；PR 的评论数不可用，Issue 的评论数按原样报告。*

</details>