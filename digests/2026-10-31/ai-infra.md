# AI 基础设施日报 2026-10-31

> 生成时间: 2026-10-31 00:15 UTC | 覆盖项目: 6 个

- [vLLM](https://github.com/vllm-project/vllm)
- [SGLang](https://github.com/sgl-project/sglang)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [Ollama](https://github.com/ollama/ollama)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Unsloth](https://github.com/unslothai/unsloth)

---

## 横向对比

# 跨项目 AI 基础设施对比 — 2026-10-31

## 1. 生态概览

今日 AI 基础设施活动以加固为主，而非扩张：没有合并重要的新前沿架构，最高严重级别的问题集中在静默正确性故障、内存/KV 核算以及 API 契约破坏。数据中心服务引擎 **vLLM** 与 **SGLang** 正集中在前沿 MoE 路径——Kimi-K3、DeepSeek-V4.1、MiniMax——以及 Blackwell/ROCm 后端。本地运行时 **llama.cpp** 与 **Ollama** 正在推进低位量化、MLX 与异构设备覆盖。网关与微调栈 **LiteLLM** 与 **Unsloth** 正在承接生产关切：计费准确性、Anthropic/OpenAI 兼容性、安装隔离与量化工作流。发布节奏不均——llama.cpp 发布了多个构建，Unsloth/LiteLLM 推出了 beta/dev 产物，而 vLLM、SGLang 与 Ollama 未发布版本。

## 2. 活跃度对比

| 项目 | 层级 | 问题（24 小时内更新） | PR（24 小时内更新） | 发布状态 |
|---|---|---:|---:|---|
| **vLLM** | 服务引擎 | n/r | n/r | 无发布/标签；无已落地的 API 移除 |
| **SGLang** | 服务引擎 | n/r | n/r | 无标签/镜像；FlashInfer 依赖升级进行中 |
| **llama.cpp** | 本地运行时 | **51** 个更新；摘要列出前 30 | **125** 个更新；摘要列出前 20 | **b12002–b12017** 已发布 |
| **Ollama** | 本地运行时 + 云 | n/r | n/r | 无发布 |
| **LiteLLM** | 网关 | **112** | **472** | **v1.109.0-dev.2** 开发预发布 |
| **Unsloth** | 微调 / Studio | n/r | n/r | **v0.1.913-beta** |

*注：n/r = 所提供摘要中未报告。计数为明确披露的 24 小时“更新”数量；它们不是未关闭问题/PR 总数，也不能跨项目直接比较。llama.cpp 的信息流明确不完整：51 个更新问题中的前 30 个，以及 125 个更新 PR 中的前 20 个。*

**解读：** LiteLLM 明确报告的变动量以较大优势位居最高，这与网关层成本核算和兼容性工作一致。llama.cpp 今日发布节奏最高。vLLM 与 SGLang 展现出大量工程活动，但有意未发布版本。Ollama 在发布方面安静，但带有一个关键的云端点问题。Unsloth 发布了一个 beta，但存在事故级安装隔离回归。

## 3. 模型支持竞赛

| 项目 | 今日新增/扩展的模型或硬件支持 | 评估 |
|---|---|---|
| **vLLM** | 未合并新架构；Mistral Large 4 Responses 修复；Kimi-K3 稳定性/JIT；MiniMax-M3 ROCm DSpark；DeepSeek-V4.1 DSpark 融合采样；Blackwell MXFP8；MI355X/MI300X 调优；CPU DP×TP 修复 | **前沿模型加固与加速器覆盖广度**，而非新模型广度 |
| **SGLang** | MiniMax-M3.1-Flash 跟踪 + DFlash2 草稿；DSV4 原生 H16 CuTe 稀疏预填充；B200/SM100 融合投影；HiCache 中的 MXFP8 KV；AMD RDNA3/4 CI；rust-server 多模态图像预处理 | **前沿 MoE 深度以及 Blackwell/AMD 专项优化** |
| **llama.cpp** | OpenCL q2_0；IQ3 审核中；Hexagon 改进；WASM relaxed SIMD；TML Inkling、PocketTTS、LFM3-Audio；Gemma 4 与 Qwen3.8-Flash 性能工作 | **最广的本地架构/后端覆盖与低位覆盖范围** |
| **Ollama** | AutoTrust MLX 决策模型；Intel Mac macOS 12 支持；逐模型 thinking 元数据；多模态输入校验 | **本地用户体验、MLX 与 API shim 兼容性** |
| **LiteLLM** | Databricks Gemini 3.5–3.8 音视频能力标志；Gemini 图像批量定价；提供商接入修复 | **网关元数据/定价，而非运行时模型支持** |
| **Unsloth** | DeepSeek-V4.1-Flash-1017 GGUF；LFM3-Omni 音频；LFM3-Audio-2B；集成 GPU int8 路径；MLX 修复 | **微调、GGUF 导出与音频模型启用** |

**谁领先：** 不存在单一领先者——领先地位因层而异。**vLLM** 与 **SGLang** 在数据中心前沿模型服务方面领先，其中 vLLM 进行了更多 Kimi-K3 正确性排查，SGLang 展现出更明确的新模型跟踪以及 DSV4 稀疏预填充工作。**llama.cpp** 在本地架构、低位量化与非 NVIDIA 后端的广度上领先。**Unsloth** 在开放模型微调/GGUF 启用方面领先。**LiteLLM** 在提供商抽象与定价元数据方面领先。**Ollama** 在打包式本地/MLX 用户体验方面领先，但在前沿模型服务方面落后。

## 4. 性能前沿

| 优化领域 | 今日证据 | 影响 |
|---|---|---|
| **KV 缓存与内存核算** | vLLM #64460：KV 池饱和时准入重试使解码 TPOT 膨胀 **~2.3×**；SGLang 在 HiCache 中的 MXFP8 KV 与 Mamba HiCache 工作；llama.cpp 将 KV 轮转常量常驻并增加原生量化 KV；Ollama 逐层 KV 大小设置与 MLX 预检缺口；Unsloth 内存估算器不准确 | **KV 核算——而非原始 FLOPS——是主要的扩展与 p99 约束** |
| **调度 / 批处理 / 路由** | vLLM 准入退避请求；SGLang 调度器解耦 RFC；LiteLLM Rust 路由器与日志热路径优化；llama.cpp MoE 专家缓存 `ClassLRU`；Ollama MLX 调度器修复 | 尾延迟与成本感知路由在服务、运行时和网关层都很活跃 |
| **内核 / JIT / 冷启动** | vLLM：残余 Triton 采样内核导致 ~**1.5 s** TTFT，**130 µs** MI355X 在 RCCL 前空闲；SGLang：DeepGEMM 快速预热将 DSV4.1 冷启动从 **约 30 分钟降至 <3 分钟**；llama.cpp OpenCL/Hexagon/WASM 内核；Unsloth flex→SDPA 拆分 | **无服务器/自动扩缩容经济性在很大程度上取决于预热与内核缓存行为** |
| **量化 / 低位** | vLLM Blackwell MXFP8；SGLang MXFP8 KV 与 MXFP4 MoE；llama.cpp OpenCL q2_0/IQ3 与 q4/q8 KV；Unsloth int8 主机卸载与 GGUF；Ollama nvfp4 MLX | **低位量化正在扩大硬件覆盖范围；每个后端的数值验证仍然必不可少** |
| **分布式服务** | vLLM TP/PP/PD、Mooncake TP-rank 停滞；SGLang DP attention、EP、elastic-EP 集合通信、EAGLE+DP+FlashInfer 崩溃；llama.cpp RPC/多设备；LiteLLM 多部署路由 | **现在薄弱点是 rank 级正确性与特性交互，而非单一特性吞吐** |

**要点：** 优化工作正从显眼吞吐量转向**尾延迟、内存正确性、冷启动成本与 rank 级可靠性**。今天最具生产相关性的数字是 vLLM 在 KV 压力下 2.3× 的 TPOT 膨胀，以及 SGLang 约 27 分钟的 DeepGEMM 预热缩短。

## 5. 层级定位

| 层级 | 项目 | 主要角色 | 当前痛点 |
|---|---|---|---|
| **数据中心服务引擎** | **vLLM**、**SGLang** | 高吞吐 GPU/加速器推理、前沿 MoE、TP/PP/PD、KV 缓存、CUDA graphs | 静默输出损坏、TP-rank 停滞、KV 压力导致的延迟、多特性崩溃 |
| **本地 / 边缘运行时** | **llama.cpp**、**Ollama** | GGUF/MLX 执行、桌面/边缘/本地部署、低位量化、异构后端 | 后端稳定性、内存核算、前缀缓存失效、云端点可靠性 |
| **LLM 网关 / 代理** | **LiteLLM** | 多提供商路由、预算、API 转换、可观测性、成本归因 | 计费正确性、Anthropic/OpenAI 兼容性、健康检查成本泄漏、Python 版本支持 |
| **微调 / Studio** | **Unsloth** | LoRA/QLoRA、GGUF 导出、训练工作流、本地 Studio | 安装隔离、内存估算、内核正确性、更新可靠性 |

**重叠说明：** vLLM 与 SGLang 在服务引擎层竞争；llama.cpp 与 Ollama 在本地运行时上重叠，但抽象层级不同——llama.cpp 是底层 ggml 运行时，Ollama 是打包式本地/云体验。LiteLLM 与 Unsloth 不是服务引擎；它们分别控制访问/成本与模型适配。

## 6. 趋势信号

- **正确性是新的功能门槛。** 最高严重级别的问题都是静默或难以检测的：vLLM Kimi-K3 的 `!!!!` token 流（#64758）、SGLang DSV4.1 OOM 循环（#43486）与 rust-server 路由缺陷、llama.cpp Gemma 4 + MTP 非法内存访问（#31077）、Ollama Cloud 未返回 HTTP 响应（#19111），以及 Unsloth 的隔离安装覆盖（#16186）。只有先针对这些问题设好门槛，吞吐收益才有意义。

- **KV 缓存与内存核算是主要扩展瓶颈。** vLLM 的 KV 饱和 TPOT 膨胀、SGLang 在 29% KV 利用率时 OOM、Ollama 的 262k 上下文 MLX 占用差异，以及 llama.cpp 的量化 KV 工作，都指向同一个问题：分配器行为与调度器估算偏离真实内存压力。

- **冷启动与 JIT 预热是产品决策。** SGLang 的 `SGLANG_JIT_DEEPGEMM_FAST_WARMUP` 报告——约 30 分钟降至 3 分钟以内——是今日摘要中最清晰的无服务器/自动扩缩容杠杆。vLLM 因采样内核残留导致约 1.5 秒 TTFT，展示了较小规模下的同一问题。

- **API 兼容性仍是生产阻塞项，尤其是在 agent 场景。** 工具调用解析、Anthropic `x-api-key`、thinking-block 重放、结构化输出下的 `raw_logprobs`、`stop_regex` 裁剪，以及 LiteLLM 预算窗口核算，都是活跃缺陷。Agent 框架应验证输出并固定版本，而不是假定可直接替换兼容。

- **特性交互需要显式固定版本。** EAGLE + DP attention + FlashInfer A2A + prefill CUDA graph；DSPARK + DSV4.1-Flash 持续解码；Gemma 4 + MTP；以及 torch 2.8/2.9 flex-attention 因果掩码丢失，都是交互缺陷，而非单一特性故障。请测试你实际部署的精确组合。

- **异构硬件与低位量化持续扩展。** Blackwell MXFP8、ROCm MI3xx/MI350X、AMD RDNA3/4、Intel SYCL/Vulkan、Apple MLX 与 ARM 都出现在今日工作中。请按后端验证数值；不要假定与 CUDA 对等。

**Agent/应用开发者应关注：** 为 Kimi-K3 增加退化输出防护；强制执行工具名允许列表；在修复前将 `raw_logprobs` 视为经过 grammar mask 后的结果；在部署健康检查中保留预热探针；按最坏情况 KV 压力下的 TPOT 来设置并发规模；暂不要将 LiteLLM 窗口预算视为硬上限；审计计费的媒体健康检查；并在 `UNSLOTH_STUDIO_HOME` 隔离回归解决前固定 Unsloth 安装版本。

---

## 各项目详细报告

<details>
<summary><strong>vLLM</strong> — <a href="https://github.com/vllm-project/vllm">vllm-project/vllm</a></summary>

# vLLM 摘要 — 2026-10-31

## 1. 今日亮点

过去 24 小时内没有版本发布，但当天的活动主要集中在前沿模型路径上的正确性工作：两个独立的 Kimi-K3 故障模式（由 NaN 驱动的静默 `!` token 流，以及 MooncakeStoreConnector 中某个 TP rank 卡住）已被提交，并分别针对 FlashKDA/FlashMLA 和 KV connector 进行分类排查。与此同时，面向 RL 训练的直接权重重载工作（#54477 RFC）在四个 loader PR 中取得进展；一份调度器层面的报告量化了当 KV pool 饱和的请求重试准入时，解码 TPOT 膨胀约 2.3×。CI/基础设施变动（自动分片 rollout）以及 Scribe 风格的维护 PR 构成了其余变更。

## 2. 版本发布与破坏性变更

过去 24 小时内没有新版本或标签。没有 API/配置移除落地。

有一个配置面是在扩展而非破坏 —— PR [#64815](https://github.com/vllm-project/vllm/pull/64815) 新增 `KernelConfig.mxfp8_cublaslt_min_m`（默认 `128`，`null` 表示禁用），用于控制 Blackwell 上的 MXFP8 cuBLASLt dispatch。

有两个 PR 已暂存但被明确搁置，不应被视为即将发生的默认行为变更：[#64796](https://github.com/vllm-project/vllm/pull/64796)（默认开启自动 CI 分片）和 [#64795](https://github.com/vllm-project/vllm/pull/64795)。

## 3. 新模型与硬件支持

今天没有合并新的模型架构。模型相关工作本质上是缺陷修复和性能调优：

- **Mistral Large 4**（`--tokenizer-mode mistral`）的 Responses API 兼容性在两种请求形态下被破坏；针对 `developer` 角色的修复已在评审中 —— [#64793](https://github.com/vllm-project/vllm/issues/64793)、[#64789](https://github.com/vllm-project/vllm/issues/64789)。
- **Kimi-K3** 获得的关注最多，既作为稳定性目标，也通过 JIT/补齐缺口的工作 —— [#64824](https://github.com/vllm-project/vllm/issues/64824)。
- ROCm 上的 **MiniMax-M3**：自适应 DSpark 验证启用仍在评审中 —— [#56451](https://github.com/vllm-project/vllm/pull/56451)。
- **硬件：** Blackwell MXFP8 GEMM 路由到 cuBLASLt（[#64815](https://github.com/vllm-project/vllm/pull/64815)）；ROCm MI355X scratch 分配调优（[#64791](https://github.com/vllm-project/vllm/issues/64791)）；当分配的 NUMA 节点不存在时的 CPU DP×TP 启动修复（[#64499](https://github.com/vllm-project/vllm/pull/64499)）。

## 4. 性能与优化

**调度器 / 批处理**
- **KV pool 饱和后的准入重试会使解码 TPOT 膨胀约 2.3×**，发生在 P/D 解耦的 Ascend 部署上（TP8，约 32k token 的 KV pool）。该机制在 V1 调度器中被描述为与平台无关；请求是支持自动准入退避 —— [#64460](https://github.com/vllm-project/vllm/issues/64460)。对于任何在紧张 KV 预算下运行的人，这是当天最具可操作性的吞吐发现。

**Kernel / 运行时 JIT**
- **静默运行时 JIT 编译**仍是首要运维问题：用户无法判断是否发生了 kernel cache miss，DeepGEMM 预热缺口也持续存在 —— 跟踪 issue [#49349](https://github.com/vllm-project/vllm/issues/49349) 和后续 [#64824](https://github.com/vllm-project/vllm/issues/64824)。
- **CPU + Model Runner V2：** 仍有 1–3 个 Triton 采样 kernel 在首批请求内编译，在每次服务器启动后固定请求数内给 **TTFT 增加约 1.5 s** —— 预热 PR [#64522](https://github.com/vllm-project/vllm/pull/64522)。

**GPU kernel 与内存**
- **MI355X：** 由于每次 dispatch 的 scratch 分配，在 prefill/mixed 步骤中某些 RCCL all-reduce 之前出现约 **130 µs** 的 GPU 空闲；修复方法是在 ROCm 镜像中设置 `HSA_SCRATCH_SINGLE_LIMIT` —— [#64791](https://github.com/vllm-project/vllm/issues/64791)。
- **MI300X：** DSA 候选块分数和采样器 fp32 logits 每步都会重新分配，并超出分配器块；PR 将两者移至持久缓冲区 —— [#63719](https://github.com/vllm-project/vllm/pull/63719)。
- **DeepSeek-V4.1 DSpark：** 在 NVIDIA 上通过两个 Triton kernel + 逆 CDF 融合顺序 Markov 采样 —— [#64442](https://github.com/vllm-project/vllm/pull/64442)。
- **Blackwell MXFP8：** 大 M 线性 GEMM 通过 `torch._scaled_mm` 路由到 cuBLASLt，同时复用现有的 128x4-swizzled scales —— [#64815](https://github.com/vllm-project/vllm/pull/64815)。
- **V2 runner PP：** 非最后流水线阶段现在从预分配缓冲区发送，而不是从实时 CUDA graph 输出发送，从而消除读/覆盖风险 —— [#64755](https://github.com/vllm-project/vllm/pull/64755)。
- **MoRIIO READ 模式：** RFC 提出通过异步 KV-load gating 恢复完整 CUDA graph（当前被迫使用分段模式）—— [#49643](https://github.com/vllm-project/vllm/issues/49643)。

**权重加载 / RL**
- 面向 RL 的直接权重重载（RFC [#54477](https://github.com/vllm-project/vllm/issues/54477)）正在推进：在线模型 checkpoint 写入（[#64336](https://github.com/vllm-project/vllm/pull/64336)）、原地重填由权重派生的张量以使已捕获的 CUDA graph 保持有效（[#64692](https://github.com/vllm-project/vllm/pull/64692)）、MoE expert padding 填充移出 loader（[#64352](https://github.com/vllm-project/vllm/pull/64352)），以及每个融合分片调用一次 `weight_loader`（[#64620](https://github.com/vllm-project/vllm/pull/64620)）。RFC 的 Rev 2 指出，Rev 1 的“跳过加载后处理”方案导致了**静默错误**（MLA 吸收权重陈旧），因此设计发生了变更。

## 5. 稳定性与回归

按严重程度排序。

**严重 —— 静默输出损坏 / 挂起**
1. **Kimi-K3 在负载下输出 `!!!!`（token 0）流。** 单个请求的激活在一个 step 内变为 NaN；FlashKDA 将其扩散到多个请求。首要怀疑是 FlashMLA 的 SM90 解码 kernel（PDL）中存在未经证实的竞争条件。静默、依赖负载，且很容易被冒烟测试漏掉 —— [#64758](https://github.com/vllm-project/vllm/issues/64758)。
2. **MooncakeStoreConnector：一个 TP rank 卡住**（GPU 空闲，对等方自旋）发生在 agentic 负载下的 Kimi-K3 上。在 B300/EFA 上跨多个 nightly 版本复现 —— [#64814](https://github.com/vllm-project/vllm/issues/64814)。
3. **GLM-5.3 TP8 挂起**，发生在 MI325X SR-IOV VF 上、当其他 vLLM 进程共享 GPU 时，于 OffloadingConnector 的 CPU↔GPU 拷贝期间；生成降至零而请求仍在运行 —— [#64549](https://github.com/vllm-project/vllm/issues/64549)。

**高 —— API 契约破坏**
4. **工具调用：** guidance 后端拒绝工具调用结构化标签（`KeyError: 'triggers'`），在请求校验阶段破坏 strict/required/named `tool_choice` —— [#55152](https://github.com/vllm-project/vllm/issues/55152)。
5. **Qwen3 工具调用解析器将带引号的模型 markup 提升为真实工具调用**，包括 `request.tools` 之外的名字和重复项 —— [#58147](https://github.com/vllm-project/vllm/issues/58147)。对 agent 部署而言，应将其视为 prompt injection 攻击面。
6. **Mistral Large 4 Responses API：** `input_text` 内容和 `developer` 角色在 `--tokenizer-mode mistral` 下都会被拒绝 —— [#64789](https://github.com/vllm-project/vllm/issues/64789)、[#64793](https://github.com/vllm-project/vllm/issues/64793)。修复 PR [#64800](https://github.com/vllm-project/vllm/pull/64800) 已提交（已关闭/已重新打开；依赖它之前请核实合并状态）。
7. **`raw_logprobs` 在结构化输出 grammar mask 之后计算**，因此上报的 raw logprobs 实际上并不 raw —— [#64809](https://github.com/vllm-project/vllm/issues/64809)；修复 PR [#64811](https://github.com/vllm-project/vllm/pull/64811)。
8. **Anthropic Messages API 拒绝 `x-api-key`**，只有 `Authorization: Bearer` 可用 —— [#51572](https://github.com/vllm-project/vllm/issues/51572)。

**中 —— 性能回归与内存**
9. **在 `--block-size > 128` 时，EAGLE3 draft 接受率在第一个位置之后骤降**（MiniMax-M3，GB200）—— [#64652](https://github.com/vllm-project/vllm/issues/64652)。
10. **设置 `--prefix-cache-retention-interval` 时，Gemma-4 MTP 使 prefix cache 命中减半** —— [#64808](https://github.com/vllm-project/vllm/issues/64808)。
11. **使用 `--kv-cache-memory-bytes` + `--enable-sleep-mode` 时冷缓存 KV OOM** —— [#62277](https://github.com/vllm-project/vllm/issues/62277)。
12. **`fuse_rope_kvcache` 在 drafter 与 target attention shape 不同时破坏 ROCm 上的 EAGLE 投机解码** —— [#64679](https://github.com/vllm-project/vllm/issues/64679)。
13. **ROCm gfx950（MI350X）：`kernel_paged_attention_2d` 在长上下文解码下非法内存访问** —— [#48043](https://github.com/vllm-project/vllm/issues/48043)。

**低 —— 打包 / 元数据**
14. `vllm/vllm-openai:unlimited-ocr` 镜像无法服务 Unlimited-OCR —— [#64489](https://github.com/vllm-project/vllm/issues/64489)。
15. 非流式 `/derender` 端点报告 `usage.prompt_tokens: 0` —— [#64778](https://github.com/vllm-project/vllm/issues/64778)。
16. *今日已关闭：* 在较大的 `--max-num-batched-tokens` 下，Qwen3.5 在三个 Triton kernel 中出现 int32 token offset 溢出（[#63759](https://github.com/vllm-project/vllm/issues/63759)）；tokenizer/processor snapshot 为 gpt2 下载约 1.57 GB 不需要的权重（[#63925](https://github.com/vllm-project/vllm/issues/63925)）。

## 6. 这对应用开发者意味着什么

- **校验工具调用输出，不要信任它。** 工具调用路径上存在三个独立的解析器/后端缺陷（#55152、#58147、#64810）。如果你运行严格 `tool_choice`，请固定一个已知良好镜像，并在执行前根据你自己的 allowlist 断言工具名 —— #58147 意味着模型可以通过引用 markup 来凭空发明调用。
- **Kimi-K3 现在就需要输出层防护。** #64758 会在负载下产生语法有效、仅含 token 0 的补全。请在你的网关中加入退化输出检查（重复 `!` 串、低 distinct-token 比例），而不是等待修复。
- **Anthropic 兼容并非开箱即用。** `x-api-key` 认证（#51572）、`developer` 角色（#64793）、`input_text` 内容（#64789），以及像 `web_search`/`bash` 这样由 Anthropic 定义的工具（#64810）都仍是缺口。Claude Code 风格的客户端会碰到这些问题。
- **在结构化输出下，原始 logprobs 含义不明确。** 在 #64811 落地前，`raw_logprobs` 是 grammar mask 之后的。任何在受限解码中使用它们的校准、评分或重排流水线，测的都是错误的分布。
- **为 KV 压力下的延迟尖峰做预算。** #64460 的约 2.3× TPOT 膨胀是调度器行为，不是硬件限制 —— 按最坏情况 TPOT 来设定准入并发，否则你会在 OOM 之前先突破 p99。
- **冷启动延迟仍未完全解决。** JIT 预热缺口（#64824）和残余的 CPU 采样 kernel 编译（约 1.5 s TTFT，#64522）意味着启动后的首批请求仍不可靠；请在部署健康检查中保留预热探针，而不是把用户流量发送到冷服务器。

</details>

<details>
<summary><strong>SGLang</strong> — <a href="https://github.com/sgl-project/sglang">sgl-project/sglang</a></summary>

# SGLang 摘要 — 2026-10-31

## 1. 今日亮点
过去 24 小时没有发布版本；活动集中在稳定性与后端调优上。最具可操作性的发现是：有报告称 `SGLANG_JIT_DEEPGEMM_FAST_WARMUP` 将 DeepSeek-V4.1 冷启动从约 30 分钟缩短到 3 分钟以内，且在 chunked-prefill 16384 下未观察到可测的运行时回退。与此同时，一组 `rust-server` 正确性 bug（DP-rank 路由、端点通告、弹性 EP 集合通信）浮出水面，另有一个与 FP8 TRT-LLM MoE 路径相关的 Qwen3.8-Flash-Next-FP8 在 GB200 上约 5% 的 decode 回退。

## 2. 版本发布与破坏性变更
无。过去 24 小时没有新 tag 或镜像。注意有一个依赖升级正在进行中：FlashInfer `0.7.2` → `0.7.2.post1`，涉及 Python 版本固定、两个 Dockerfile（`flashinfer-cubin` / `flashinfer-jit-cache`）以及 `engine.py` 中的运行时版本检查——如果你固定了镜像，这一项与你相关。([PR #46926](https://github.com/sgl-project/sglang/pull/46926))

## 3. 新模型与硬件支持
- **MiniMax-M3.1-Flash** — 用于模型支持的新追踪 issue，包括用于投机解码的 DFlash2 draft checkpoint 以及已发布的 cookbook。([Issue #46869](https://github.com/sgl-project/sglang/issues/46869))
- **AMD RDNA3/RDNA4 (gfx1100/gfx1201)** — 已提出针对 main 上消费级/边缘 RDNA 部件的 CI 和上游化计划；目前没有 CI 覆盖。([Issue #46900](https://github.com/sgl-project/sglang/issues/46900))
- **DeepSeek-V4 原生 H16 CuTe 稀疏 prefill** — 实验性后端，通过 CuTe DSL 增加 H16（而非 H64 padding）稀疏 prefill 路径，目标是在 DSV4 每 rank 仅剩 16 个 query head 的 TP8 场景。由 `--dsv4-prefill-...` 控制启用。([PR #36059](https://github.com/sgl-project/sglang/pull/36059))
- **B200 / SM100 运行时优化** — 在 SM100、TP8 下，针对输出列数为 4096/8192 且 token 行数 ≤128 的 BF16 projection，已合入 fused projection/all-gather。([PR #47129](https://github.com/sgl-project/sglang/pull/47129))
- **HiCache L3 中的 MXFP8 KV cache** — 此前 L3 对每个 MXFP8 page 都会抛出 `NotImplementedError`；现在 page 以 payload + UE8M0 scales 的多缓冲区对象形式存储。([PR #46936](https://github.com/sgl-project/sglang/pull/46936))
- **Rust server 多模态（图像）预处理** — 通过 `sglang-processor` / Dynamo `dynamo-multimodal` 实现，目标是与 Python CPU 路径逐位一致。([PR #46291](https://github.com/sgl-project/sglang/pull/46291))

## 4. 性能与优化
- **DSV4.1 上的 DeepGEMM 快速预热** — 报告称冷启动快 3–5 倍（30 分钟 → <3 分钟），在 chunked-prefill 16384 下未检测到运行时性能下降，这与该开关文档中“可能导致性能下降”的说明相矛盾。在将其设为默认前，值得在你自己的部署中重新基准测试。([Issue #47397](https://github.com/sgl-project/sglang/issues/47397))
- **gfx950/MI355X 上的 Qwen3.8-Flash-Next** — 正在进行的 ROCm 优化追踪，覆盖 GatedDeltaNet（36 层）、QuerySparse Attention（12 层）、MXFP4 MoE 与 NEXTN MTP。([Issue #44304](https://github.com/sgl-project/sglang/issues/44304))
- **AMD Qwen3-Next MoE router** — Triton softmax top-k router 扩展到 hidden-2048 范围（此前仅限 hidden 4096），在 gfx950 上针对 decode 规模的行替换 `aiter_fused_topk`。([PR #47236](https://github.com/sgl-project/sglang/pull/47236))
- **ROCm 上的 Kimi-K3 MoE 前端** — 已合入 `[shared gate-up | router | latent down]` BF16 GEMM（TP8 下 N=6016, K=7168），将其路由到 AITER gfx950 调优内核，而非 hipBLASLt 启发式。([PR #44360](https://github.com/sgl-project/sglang/pull/44360))
- **RL routed-expert 开销** — 三项叠加改动降低了 `--enable-return-routed-experts` 的 CPU RAM 压力：仅在输出 rank 上保留 host cache；对不发送任何行的 rank 跳过 capture；在 DeepEP + DP attention 下，每次 forward 仅执行一次 all-gather，而非每个 MoE 层一次。三项均已标记为 CLOSED。([#47523](https://github.com/sgl-project/sglang/pull/47523), [#47547](https://github.com/sgl-project/sglang/pull/47547), [#47548](https://github.com/sgl-project/sglang/pull/47548))
- **无需 GPU slot donation 的 Mamba HiCache** — 通过将 checkpoint 保留在 host 侧，移除了 Kimi-K3 c=48 配置方案中的 `max_running_requests * 5` GPU slot 下限。([PR #44718](https://github.com/sgl-project/sglang/pull/44718))
- **Scheduler 架构（RFC）** — 提议将 scheduler 控制与 forward 提交解耦，使设备启动队列在 decode 步骤之间持续有任务。([Issue #47019](https://github.com/sgl-project/sglang/issues/47019))；另有 Attention–FFN 分离，支持流水线 + CUDA Graph。([Issue #41648](https://github.com/sgl-project/sglang/issues/41648))

## 5. 稳定性与回归

**严重 — 持续负载下的内存耗尽**
- **DSV4.1-Flash + DSPARK OOM 循环**：在持续 max-batch decode 下，CUDA caching allocator 每 15–25 分钟耗尽 GPU 内存，而 KV pool 报告利用率仅为 29%——这强烈表明是非 KV allocator 的碎片化/泄漏，而非容量耗尽。没有关联修复 PR。([Issue #43486](https://github.com/sgl-project/sglang/issues/43486))
- **HiCache Mooncake + DP attention**：每个 DP rank 都会挂载完整的 `MOONCAKE_GLOBAL_SEGMENT_SIZE`，这与 README 中“total = global segment size”的说法相矛盾；规划容量时需将其乘以 DP 度。([Issue #46899](https://github.com/sgl-project/sglang/issues/46899))
- **ROCm DCP-PD allocator 增长** 在突发负载下先于 HIP 资源中止出现；在当前 main 上的复现仍待完成。([Issue #46831](https://github.com/sgl-project/sglang/issues/46831))

**高 — 崩溃 / 正确性**
- **EAGLE draft extend 因负维度崩溃** 在 DP attention + FlashInfer A2A + prefill CUDA graph 下发生——这是三方特性交互，因此生产环境应避免该组合。([Issue #47490](https://github.com/sgl-project/sglang/issues/47490))
- **`/start_profile` 在 `profile_by_stage=true` 且未提供 `num_steps` 时** 抛出 `TypeError: NoneType += int`，并使每个 scheduler 崩溃。([Issue #47294](https://github.com/sgl-project/sglang/issues/47294))
- **rust-server DP-rank 路由**：`/internal/peer` 在未验证目标 rank 的情况下处理转发的控制请求。([Issue #47511](https://github.com/sgl-project/sglang/issues/47511))；`gather_server_endpoints` 可能通告 loopback/不可路由地址，且仅发出警告。([Issue #47509](https://github.com/sgl-project/sglang/issues/47509))；它还会在 elastic-EP joiner 上通过 WORLD group 运行，而 serving rank 从不进入该 group。([Issue #47505](https://github.com/sgl-project/sglang/issues/47505))。一个配套 PR 发布 attention-DP 的 listener map。([PR #47532](https://github.com/sgl-project/sglang/pull/47532))
- **`stop_regex` 将匹配文本泄漏** 到响应中，且 `no_stop_trim` 对 regex stop 是 no-op——影响输出后处理约定。([Issue #47461](https://github.com/sgl-project/sglang/issues/47461))
- **SM120（RTX PRO 6000）上的 GLM-5.3-Flash**：fa4 后端在 hybrid extend reshape 的 CUDA-graph capture 时崩溃；Triton 是该硬件上唯一可用的 attention 后端。([Issue #42012](https://github.com/sgl-project/sglang/issues/42012))
- **AMD Quark MXFP4 W4A16 MoE 且 `--ep-size > 1`**：GPU 以 `HSA_STATUS_ERROR_EXCEPTION` 中止。修复 PR 已开放（将该路径限制到 gfx1151）。([Issue/PR #47408](https://github.com/sgl-project/sglang/pull/47408))
- **NemotronHConfig 拒绝 transformers 5 的层类型**（`linear_attention` / `full_attention`）位于 `config.json` 中——阻止加载由更新版 transformers 写出的配置。([Issue #47444](https://github.com/sgl-project/sglang/issues/47444))

**中 — 可观测性与配置**
- **Attention-DP rank 对路由器不可区分**：`KvMetrics.data_parallel_rank` 硬编码为 0，且 Prometheus 序列省略 `dp_rank`，破坏按 rank 的负载均衡与仪表盘。([Issue #47409](https://github.com/sgl-project/sglang/issues/47409))
- **S3 模型 URI 静默覆盖** 显式的 `remote_instance` + modelexpress loader（当配置了 `runai_streamer` 时）。([Issue #47428](https://github.com/sgl-project/sglang/issues/47428))
- **HiCache + Mooncake L3 命中率** 在多轮基准测试中，于 L2/L3 容量压力下可复现地从 87.4% 下降。([Issue #47481](https://github.com/sgl-project/sglang/issues/47481))
- **Nomas diffusion pipeline**：KV 预算忽略 PyTorch 已缓存但已释放的内存，且 SP 整除性验证过晚。([Issue #47515](https://github.com/sgl-project/sglang/issues/47515))

**回归与修复**
- **GB200 上约 5% 的 decode 回退**：Qwen3.8-Flash-Next-FP8 TP4/EP4 自 [#45917](https://github.com/sgl-project/sglang/pull/45917) / commit `ac3db731` 起出现，其中 FP8 TRT-LLM MoE 在 EP 下保留 kernel 内路由。对任何已合入该 commit 之后代码的人影响很大。([Issue #47501](https://github.com/sgl-project/sglang/issues/47501))
- **确定性 top-p/top-k 重归一化** 针对 `tp_size > 1` 已合入（CLOSED）：FlashInfer 默认 renorm 使用 float `atomicAdd`，是非确定性的，导致 DFlash/DSpark verify 中 TP rank 分歧。([PR #38565](https://github.com/sgl-project/sglang/pull/38565))
- **CI 不稳定追踪** 仍非常活跃——159 条评论，追踪反复出现的 NVIDIA `PR Test Base` / `PR Test Extra` 失败。如果你在合入 PR，请为红色 CI 预留预算。([Issue #42752](https://github.com/sgl-project/sglang/issues/42752))

## 6. 这对应用开发者意味着什么
- **冷启动是当前最大的成本杠杆。** 如果你在 serverless 或自动扩缩容基础设施上运行 DeepSeek-V4.1，`SGLANG_JIT_DEEPGEMM_FAST_WARMUP` 似乎可消除约 27 分钟的预热，且没有运行时成本——仍有待更广泛确认。在将其设为默认前，请在你自己的输入 shape 上验证。
- **不要盲目叠加高级特性。** 看板上两个最高严重级别的崩溃（EAGLE + DP attention + FlashInfer A2A + prefill CUDA graph；DSPARK + DSV4.1-Flash 持续 decode）来自特性*交互*，而非单一特性。固定并测试你实际部署的精确组合。
- **Rust server 尚不能直接替换。** DP-rank 路由与端点通告 bug 是正确性问题，在多节点部署中会静默错误路由控制流量。如果你因多模态预处理的收益而使用 `SGLANG_RUST_SERVER=1`，请保持单节点，或等待 [#47532](https://github.com/sgl-project/sglang/pull/47532)。
- **在 attention DP 下，按 rank 路由目前是盲的。** 在 `dp_rank` 进入 Prometheus 序列之前（[Issue #47409](https://github.com/sgl-project/sglang/issues/47409)），你的网关无法跨 attention-DP rank 进行负载感知路由——请按更粗粒度的均衡做规划。
- **输出裁剪约定对 regex stop 不安全。** 如果你的 agent 框架依赖 `stop_regex` + `no_stop_trim` 来约束 tool-call 或 JSON 生成，请在 [#47461](https://github.com/sgl-project/sglang/issues/47461) 修复前于客户端侧做清理。
- **KV cache 利用率指标对 OOM 排查并不可信。** DSV4.1 在 29% KV 使用率下 OOM 的报告提醒我们，pool 占用率与实际 GPU 内存压力会背离；请直接对 `torch.cuda.mem_get_info` 和 allocator 统计做埋点。

</details>

<details>
<summary><strong>llama.cpp</strong> — <a href="https://github.com/ggml-org/llama.cpp">ggml-org/llama.cpp</a></summary>

# llama.cpp 文摘 — 2026-10-31

## 今日亮点
密集的发布窗口（b12002–b12017）带来了 Windows/RPC UTF‑8 路径与 argv 清理、ggml 中的批量张量拷贝 API，以及将 KV-cache 旋转常量常驻 GPU。与此同时，评审中的工作瞄准 Gemma 4 大幅 prefill 提升、新的 MoE 专家缓存策略，以及更广泛的低比特 OpenCL/Hexagon 覆盖。后端稳定性仍是主要拖累：有多个开放的 SYCL、HIP、Vulkan 和 CUDA 正确性/回归报告，包括 Gemma 4 + MTP 的非法内存访问。

## 发布与破坏性变更
- **b12017 / b12015 / b12014 — Windows 与 RPC 路径处理清理。** 从 `rpc` 和 `common` 中移除了 `fs_path_to_utf8()`，并去掉了 Windows 的 argv 重建；现在 argv 通过来自 #31329 的 manifest 以 UTF‑8 传递。这修复了非 ASCII 路径处理（#26416），但对链接 `common` 的下游代码而言是一次接口移除。[b12017](https://github.com/ggml-org/llama.cpp/releases/tag/b12017) · [b12015](https://github.com/ggml-org/llama.cpp/releases/tag/b12015) · [b12014](https://github.com/ggml-org/llama.cpp/releases/tag/b12014)
- **b12012 — cpp-httplib 更新至 0.64.0。** Server/HTTP 依赖升级；如果你固定了行为，值得重新构建并重跑集成测试。[b12012](https://github.com/ggml-org/llama.cpp/releases/tag/b12012)
- **b12004 — reasoning budget forcing 现在会在 prompt 中发现结束标签时终止。** 对于依赖 `--reasoning-budget` 的 agent 循环来说这是行为变更：当 prompt 已包含停止标签时，预算强制执行可能更早结束。[b12004](https://github.com/ggml-org/llama.cpp/releases/tag/b12004)
- **b12002 — 新的 ggml 批量张量拷贝 API**，已被 `llama` 上下文 I/O 采用。这是内部 API 新增，但树外 ggml 后端可能希望实现/验证它。[b12002](https://github.com/ggml-org/llama.cpp/releases/tag/b12002)
- **PR #31444 — 删除 `common_get_path_from_env()`**（路径工作的后续清理）。[PR #31444](https://github.com/ggml-org/llama.cpp/pull/31444)

## 新模型与硬件支持
- **OpenCL q2_0 支持（b12005）**，包含 AOS/SOA mat-vec、tiled mat-mul 和无 shuffle 路径——对运行极低比特量化的 Adreno/移动级设备意义重大。[b12005](https://github.com/ggml-org/llama.cpp/releases/tag/b12005)
- **OpenCL IQ3（IQ3_S、IQ3_XXS）初步支持**正在评审中，以 #30180 中的 Adreno 优化为参考。[PR #31338](https://github.com/ggml-org/llama.cpp/pull/31338)
- **OpenCL `topk_mask`**（已可合并）和**初步 FWHT** 支持正在评审中——进一步缩小与 CUDA/Metal 算子覆盖的差距。[PR #31441](https://github.com/ggml-org/llama.cpp/pull/31441) · [PR #31434](https://github.com/ggml-org/llama.cpp/pull/31434)
- **SYCL `FLASH_ATTN_EXT` 失败已修复（b12003）**。[b12003](https://github.com/ggml-org/llama.cpp/releases/tag/b12003)
- **Hexagon：** v75+ 设备上 stride >16M 的 DMA 传输，以及针对 permuted CONT/CPY 的批量 HVX vgather-transpose。[PR #31442](https://github.com/ggml-org/llama.cpp/pull/31442) · [PR #31446](https://github.com/ggml-org/llama.cpp/pull/31446)
- **WASM relaxed SIMD** 点积实现已提出；基于 #11453 构建。[PR #19590](https://github.com/ggml-org/llama.cpp/pull/19590)
- **评审中的新架构/模型：** TML Inkling（safetensors→GGUF 转换器、graph、banded Flash Attention kernel、用于大型 MoE 的 int64 索引）[PR #25731](https://github.com/ggml-org/llama.cpp/pull/25731)；无需克隆的 PocketTTS 语音 [PR #31429](https://github.com/ggml-org/llama.cpp/pull/31429)；LFM3-Audio codec decoder 量化保护放宽（已关闭/已合并）[PR #31386](https://github.com/ggml-org/llama.cpp/pull/31386)。

## 性能与优化
- **KV-cache 旋转常量保留在 GPU 上常驻（b12007）**，新增测试验证常驻 KV 旋转缓冲区；文档指出仍有多设备工作待完成。减少量化/旋转 KV cache 的每步 host→device 传输。[b12007](https://github.com/ggml-org/llama.cpp/releases/tag/b12007)
- **MoE 专家缓存：类似 LRFU/MQ 的 `ClassLRU` 策略（PR #31233）。** 报告称在缓存预热时，相比 SLRU，QFN 上 decode +6%、GLM 上 +7%，专家上传减少 8%；并启用自动模式。[PR #31233](https://github.com/ggml-org/llama.cpp/pull/31233)
- **Gemma 4 E2B/E4B 图优化（PR #31356）**——对不贡献到 KV-shared cache 的层跳过计算，并在 KV-shared 层之前丢弃未使用的 prompt token；据称在 prompt 处理上有“巨大收益”，但未提供绝对数字。[PR #31356](https://github.com/ggml-org/llama.cpp/pull/31356)
- **Qwen3.8-Flash-Next（`qwen4exp`）** 的 conv-state tail 写入不再经过中间 `cont`——生成约 +2%，已在 CUDA/CPU/meta 上验证（draft）。[PR #31443](https://github.com/ggml-org/llama.cpp/pull/31443)
- **`flash_attn_tile` 中的 CUDA/HIP 原生量化 KV（PR #31234）**——对 q4/q8 KV 避免每步 f16 反量化或逐 head 缓存重读。[PR #31234](https://github.com/ggml-org/llama.cpp/pull/31234)
- **Qwen3.5 dense 的 MTP 图重分配修复**，用于在 token 与 embedding 输入之间切换时（PR #31415，修复 #31302）。[PR #31415](https://github.com/ggml-org/llama.cpp/pull/31415)
- **Meta 后端提高了 compute-view 限制**，针对张量较少的缓冲区，修复 DeepSeek-V4.1 上使用 `-sm tensor` 时 `ggml_new_object` OOM 中止（PR #31447）。[PR #31447](https://github.com/ggml-org/llama.cpp/pull/31447)
- **Windows 无缓冲模型加载**（类似 DirectIO）仍在寻求设备测试。[PR #26014](https://github.com/ggml-org/llama.cpp/pull/26014)

## 稳定性与回归
按严重程度排序；除非注明，均为开放状态。

1. **`GGML_ASSERT(src_ss[0].axis != GGML_BACKEND_SPLIT_AXIS_0)` 中止**，发生在 `ggml-backend-meta.cpp`，配置为 4×3090、MiniMax M2.7、拆分 KV 类型。自 6 月起开放，仍活跃。[Issue #24015](https://github.com/ggml-org/llama.cpp/issues/24015)
2. **CUDA 非法内存访问：Gemma 4 31B + draft-MTP**，在 KV rollback/clear 后发生；关闭 MTP 时不崩溃。已在 b11734/b11796/b11840 复现。[Issue #31077](https://github.com/ggml-org/llama.cpp/issues/31077)
3. **SYCL 段错误：** oneAPI 2026.2.0 崩溃 [Issue #31064](https://github.com/ggml-org/llama.cpp/issues/31064)，以及 `server-intel-b11960` 在持久设备代码缓存中 SIGSEGV [Issue #31369](https://github.com/ggml-org/llama.cpp/issues/31369)。
4. **CDNA2（gfx90a / MI210）上的 HIP 构建失败**——在 Debian 12 上编译失败。[Issue #30869](https://github.com/ggml-org/llama.cpp/issues/30869)
5. **`qwen4exp` 在 HIP 上模型加载期间发生活锁**，同一配置在 Vulkan 上可加载。[Issue #29149](https://github.com/ggml-org/llama.cpp/issues/29149)
6. **SYCL XMX-ESIMD MoE prompt 处理回归，慢 28–35%**，在 Arc Pro B70 上，构建 11783 与 11851 之间。[Issue #31068](https://github.com/ggml-org/llama.cpp/issues/31068)
7. **Vulkan Intel Arc Pro B70 深上下文 decode 崩塌（从 1k→64k token 约 8×）**；SYCL 仅退化约 2.4×。属于后端内在问题，而非模型特定问题。[Issue #28721](https://github.com/ggml-org/llama.cpp/issues/28721)
8. **CUDA arm64 Blackwell 回归**，发生在官方构建 b10655 与 b11140 之间（RTX Spark N1X）。[Issue #29341](https://github.com/ggml-org/llama.cpp/issues/29341)
9. **Qwen3.5+ 聊天模板中不可往返的 reasoning/content 空白导致前缀缓存失效**，在混合模型上引发完整重新 prefill。对 agent 工作负载影响很大。[Issue #30357](https://github.com/ggml-org/llama.cpp/issues/30357)
10. **DeepSeek-V4.1-Flash-1017 在 CUDA 上的 GGUF 问题**（双 EPYC + RTX 6000 Pro）。[Issue #31385](https://github.com/ggml-org/llama.cpp/issues/31385)
11. **gfx1200 HIP/ROCm 上间歇性 `SOLVE_TRI` 内存故障。**[Issue #31108](https://github.com/ggml-org/llama.cpp/issues/31108)
12. **Arrow Lake iGPU 不支持 SYCL bf16 转换指令。**[Issue #31029](https://github.com/ggml-org/llama.cpp/issues/31029)
13. **RTX 5090 Laptop 上长 prompt 导致 `ggml_cuda_op_unary<op_sigmoid>` 中的 CUDA 地址未对齐**（已确定回归范围）。[Issue #28877](https://github.com/ggml-org/llama.cpp/issues/28877)

修复 PR 进行中：#31447（meta view 限制）、#31415（MTP 重分配）、#30743（非连续张量上的 argsort/top-k）、#31444（路径清理）。最近关闭：LFM3 `response_format` grammar-stack 500 [Issue #31328](https://github.com/ggml-org/llama.cpp/issues/31328)；LFM2.5 think-tag 泄漏 [Issue #28675](https://github.com/ggml-org/llama.cpp/issues/28675)；过时的 qwen35 RTX 5090 性能报告 [Issue #28196](https://github.com/ggml-org/llama.cpp/issues/28196)。

## 这对应用开发者意味着什么
- **Windows 部署变得更简单：** 更新到 b12014+ 以获得 UTF‑8 argv 处理；非 ASCII 模型路径和 CLI 参数不应再出问题。如果你嵌入了 `common`，请审计已移除的 `fs_path_to_utf8()`/`common_get_path_from_env()` 符号。
- **b12004 中 reasoning-budget 语义已改变。** 会向 prompt 注入 stop/end 标签的 agent 可能会看到更短或更早终止的思考；在推进上线前重新验证预算行为。
- **前缀缓存稳定性是面向 agent 的最大风险。** Issue #30357 意味着 Qwen3.5+ 混合模型可能因空白不匹配而静默丢失 prompt 缓存，使低成本的后续请求变成完整重新 prefill。请仔细固定聊天模板并监控 prefill 时间。
- **低比特推理的覆盖范围正在扩大：** OpenCL q2_0 已落地，IQ3/topk_mask/FWHT 正在评审中，使 2–3 bit 量化在更多非 NVIDIA 硬件上可行。请按后端验证数值，而不是假定一致。
- **SYCL/HIP 用户应将当前构建视为不稳定**——段错误、gfx90a 构建失败以及 28–35% 的 MoE 回归均处于开放状态，且没有关联修复 PR。生产环境仍以 CUDA 为更安全的默认选择；Intel Xe2 上的 Vulkan 存在上下文扩展悬崖。
- **服务器运维者：** 始终为零的 `prompt_tokens_seconds`/`predicted_tokens_seconds` 指标 [Issue #27436](https://github.com/ggml-org/llama.cpp/issues/27436) 以及缺少空闲 router-worker 终止机制 [Issue #25570](https://github.com/ggml-org/llama.cpp/issues/25570) 仍限制自动扩缩容/仪表盘。

---
*注：所提供的 feed 覆盖了 51 个更新 issue 中的前 30 个，以及 125 个更新 PR 中的前 20 个，因此本文摘是部分视图。*

</details>

<details>
<summary><strong>Ollama</strong> — <a href="https://github.com/ollama/ollama">ollama/ollama</a></summary>

# Ollama 摘要 — 2026-10-31

## 1. 今日亮点

Ollama Cloud 仍是首要运维关注点：issue [#19111](https://github.com/ollama/ollama/issues/19111) 报告 `/v1/chat/completions` 完全无 HTTP 响应，请求排队约 5 分钟后返回 429——目前有 6 条评论，自 2026-10-16 起未解决。本地运行时方面，工程流量主要集中在 MLX：MLX 模型的内存预检核算明显有误（[#19417](https://github.com/ollama/ollama/issues/19417)），同时一项按层 KV-cache  sizing 修复（[#19327](https://github.com/ollama/ollama/pull/19327)）针对同一类调度器误估问题。API 兼容性工作继续在 Anthropic 和 OpenAI 兼容层上推进，一项针对多块 thinking 内容丢失的修复正在评审中（[#19416](https://github.com/ollama/ollama/pull/19416)），Claude Code 输出上限从 32k 提升至 128k token（[#19410](https://github.com/ollama/ollama/pull/19410)）。

## 2. 发布与破坏性变更

过去 24 小时内无发布。无 API 或配置破坏性变更落地。

评审中的显著行为变更：
- [PR #19410](https://github.com/ollama/ollama/pull/19410)（CLOSED）——`ollama launch` 现在为 Claude Code 宣传 128k 输出 token 上限，而非 32k，防止生成中途被客户端断开连接。
- [PR #19408](https://github.com/ollama/ollama/pull/19408)——MLX 决策模型的超大 prompt 现在返回通用 `413`，而非在 runner 加载阶段失败；接受更长的状态/schema 输入，总 prompt 扩展被限制。

## 3. 新模型与硬件支持

- **MLX 上的 AutoTrust 决策模型**——[PR #19399](https://github.com/ollama/ollama/pull/19399) 将文本和视觉 AutoTrust 模型接入模型创建、prompt 编码和 API 路由；测试产物位于 `dhiltgen/autotrust-jev`。
- **macOS 12（Monterey）上的 Intel Mac**——[PR #19413](https://github.com/ollama/ollama/pull/19413) 为桌面应用和 CLI 增加尽力而为之的构建/运行支持，将当前 Intel 硬件所需的 macOS 14 下限放宽（例如最高仅支持 12.7.6 的 2015 款 iMac）。
- **OpenCode 按模型 thinking 元数据**——[PR #19409](https://github.com/ollama/ollama/pull/19409) 从模型元数据推导 thinking 级别和默认值，而非硬编码 GPT-OSS，使其他推理模型能宣传正确的控制项。
- **多模态输入校验**——[PR #19397](https://github.com/ollama/ollama/pull/19397) 使 `/api/chat` 拒绝模型没有对应编码器的片段；此前 base64 WAV 可经 `images` 传给任何模型，且该轮仅凭文本被静默回答。

## 4. 性能与优化

- **按层 KV-cache sizing**——[PR #19327](https://github.com/ollama/ollama/pull/19327) 修复 `PredictServerVRAM`，该函数目前使用最小的 `head_count_kv`、以 `embedding_length / head_count` 作为 head size、完整上下文和 f16 来为每一层 sizing。在异构层模型上会严重高估，导致调度器为实际从未分配的内存驱逐 runner。
- **MLX 内存预检缺口**——[Issue #19417](https://github.com/ollama/ollama/issues/19417) 报告 MLX 模型绕过调度器的预检并以权重大小记账。在 M5 Max（128 GB，macOS 26）上，`qwen3.8:27b`（nvfp4）在 262,144 token 默认上下文下被记为 16.9 GiB（`available` 从 91.5 → 74.6 GiB），而 runner 自身的内存核算与之不一致。
- **MLX 投机解码基准测试**——[PR #19391](https://github.com/ollama/ollama/pull/19391) 增加 `draft_num_predict=0` 以按请求禁用 drafting，同时保持 draft 缓存同步；系统默认仍为 4。
- **MLX 失控生成防护**——[PR #19398](https://github.com/ollama/ollama/pull/19398)（CLOSED）将 llama-server 的重复限制移植进 `mlxrunner`：连续 101 个相同 token 后中止生成，并提示 `prediction aborted, token repeat limit reached`。
- **可配置的 mmproj 余量**——[Issue #19407](https://github.com/ollama/ollama/issues/19407) 请求将硬编码的 1 GiB 多模态投影器安全余量改为可配置，同时保留自动 `--fit` padding。

## 5. 稳定性与回归

按严重程度排序：

1. **CRITICAL——云端推理端点无响应**（[#19111](https://github.com/ollama/ollama/issues/19111)，OPEN，6 条评论）。`POST https://ollama.com/v1/chat/completions` 不产生状态行和响应体；并发请求槽位排队约 5 分钟后返回 429。报告为自 2026-10-16 起在 Pro 计划上的回归；尚无修复 PR。
2. **HIGH——Anthropic `/v1/messages` 丢弃除最后一个 thinking 块以外的所有内容**（[#19415](https://github.com/ollama/ollama/issues/19415)）。较早的 `thinking` 块在转换为 Ollama chat 请求时被静默丢弃，破坏重放多块 assistant 轮次的客户端。**已有修复 PR：**[#19416](https://github.com/ollama/ollama/pull/19416)。
3. **HIGH——Claude Code 自动压缩在 `deepseek-v4.1-flash:1017-cloud` 上失败**（[#19249](https://github.com/ollama/ollama/issues/19249)）。长时间运行的 `/goal` 会话耗尽上下文却不压缩，循环出现 "Goal not yet met" 超过 10 次并消耗 token。
4. **HIGH——MLX 调度器记账不足**（[#19417](https://github.com/ollama/ollama/issues/19417)）。结合并发模型加载，在大统一内存 Mac 上有 OOM/驱逐抖动风险；相关 sizing 修复见 [#19327](https://github.com/ollama/ollama/pull/19327)。
5. **MEDIUM——被拒绝的 blob 上传仍留在磁盘上**（[#19414](https://github.com/ollama/ollama/issues/19414)）。`POST /api/blobs/:digest` 返回 `400 digest mismatch` 但仍以实际 digest 存储字节，孤立且未被引用直到 GC——对于重试坏上传的客户端而言是无界的磁盘泄漏。
6. **MEDIUM——cogito 解析器/渲染器在工具场景下不一致**（[#19403](https://github.com/ollama/ollama/issues/19403)）。在 `think: true` 且 ≥1 个工具时，推理和 `</think>` 泄漏进消息内容，因为渲染器总是输出 `<think>` 而解析器假设相反。
7. **LOW——CRLF Modelfile 在三引号值中保留 `\r`**（[#19404](https://github.com/ollama/ollama/issues/19404)）。Windows 编辑的 Modelfile 将多余回车注入 system prompt 和模板。
8. **LOW——Windows 11 26H2 回环 TCP 状态不明确**（[#19418](https://github.com/ollama/ollama/issues/19418)）。在 0.40.13 上原生 TCP 表对 Ollama 回环端点报告非 LISTEN 状态；报告者明确未确立缺陷。
9. **LOW——Modelfile 大小写敏感文档错误**（[#19405](https://github.com/ollama/ollama/issues/19405)）。指令名不区分大小写；参数名和消息角色区分大小写。

## 6. 对应用开发者的意义

- **目前不要依赖 Ollama Cloud 用于延迟敏感的 agent 循环。** 如果你在 `/v1/chat/completions` 上访问 `ollama.com`，请添加远低于 5 分钟的客户端超时，并将空响应（无状态行）视为可重试，而非应向用户暴露的传输错误。[#19111](https://github.com/ollama/ollama/issues/19111)
- **重放 thinking 块的 Anthropic-shim 客户端将丢失推理历史。** 如果你的 agent 持久化并向 `/v1/messages` 重发扩展 thinking 轮次，在 [#19416](https://github.com/ollama/ollama/pull/19416) 合并前，预期只有最后一个 thinking 块能保留。避免依赖先前推理块进行缓存对齐重放。
- **托管推理模型上的长时间 agent 运行需要显式压缩。** [#19249](https://github.com/ollama/ollama/issues/19249) 中的 DeepSeek 失败意味着你的 harness 应实现自己的上下文预算检查，而非将压缩委托给客户端。[#19410](https://github.com/ollama/ollama/pull/19410) 中的 128k Claude Code 上限减少了一类过早断开，但未解决压缩问题。
- **OpenAI 兼容响应 ID 去重效果很差**——[PR #19401](https://github.com/ollama/ollama/pull/19401) 指出 `chatcmpl-%d` / `cmpl-%d` 仅由 999 个不同值生成。目前不要将响应 ID 用作幂等键或追踪标识符。
- **`content: []` 的工具调用载荷正在被修复**——[PR #19152](https://github.com/ollama/ollama/pull/19152) 追踪以下情况：assistant 消息的 content 为空数组时，其 `tool_calls` 被迁移到上一条消息；如果你跨轮次交错工具，请验证历史完整性。
- **图在文字之后的多部分用户消息可能丢失指令**——[PR #19198](https://github.com/ollama/ollama/pull/19198) 解决上下文截断丢弃描述图片的文字的问题。在此落地前，优先使用文字在后的顺序。
- **在 Apple Silicon 上，为 MLX 模型显式固定上下文大小。** 在默认由 VRAM 推导的上下文（128 GB M5 Max 上为 262k）加上 [#19417](https://github.com/ollama/ollama/issues/19417) 中的记账 bug 下，多模型部署可能被调度进 runner 实际无法兑现的内存。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 摘要 — 2026-10-31

**范围：** 过去 24 小时内有 1 个新的 dev 版本发布，112 个 issue 和 472 个 PR 有更新。工作量主要集中在成本核算正确性，以及持续的 Claude Code / Anthropic 格式兼容性修复。

---

## 1. 今日重点

今日的重心是**计费准确性**：一个仍未修复的 bug 显示 `/key/update` 会静默地将进行中请求的成本从预算窗口支出中丢弃，同时一批 PR 正在重构 provider 上报总额、Vertex 服务端搜索调用、Perplexity 过滤器以及计费媒体健康检查的计价方式。与此同时，router 迁移推进到一个由开关门控的 Rust 核心（`LITELLM_RUST`），若干长期搁置的 Claude Code / Bedrock / Vertex 转换问题被关闭。

---

## 2. 发布与破坏性变更

- **v1.109.0-dev.2** —— 仅为 dev 预发布；过去 24 小时内没有稳定版发布。供应链提示：所有 Docker 镜像均使用 commit [`e82a3c6`](https://github.com/BerriAI/litellm/commit/e82a3c646908ba0a6ee0beddc4310d7a6cac4065) 中引入的密钥通过 **cosign** 签名 —— 上线前请先验证。
- **标记为破坏性的进行中 PR**（尚未合并）：
  - [`#49227`](https://github.com/BerriAI/litellm/pull/49227) `fix(agentic)!` —— 将失败的 agentic 后续调用暴露出来，而非返回循环前的 tool call。那些隐式依赖被吞掉错误的 200 响应的客户端将看到新的错误响应。
  - [`#49244`](https://github.com/BerriAI/litellm/pull/49244) `fix(health)!` —— 后台健康检查默认将**跳过计费媒体生成模式**（image_generation、image_edit、video_generation）。将健康检查用作这些模式存活探针的部署必须显式选择加入。
- dev 版本本身无需配置 schema 迁移。

---

## 3. 新模型与硬件支持

- [`#49361`](https://github.com/BerriAI/litellm/pull/49361) —— Databricks：为 Gemini 3.5–3.8 Flash 行增加 `supports_audio_input` / `supports_video_input` 标志，使能力元数据与文档中描述的 `supported_modalities` 一致（影响 `databricks/databricks-gemini-*` 的路由资格）。
- [`#49358`](https://github.com/BerriAI/litellm/pull/49358)（已关闭）—— `gemini/gemini-2.5-flash-image` 新增 Batch/Flex/Priority 的**文本输出**价格（batch 为 `1.25e-06`），此前这些价格会落到 Standard 的 $2.50/1M 费率。
- UI 侧补齐了 provider 接入缺口：Add Model 下拉列表中缺少 Meta Model API（`meta/muse-spark-1.1`）[`#36164`](https://github.com/BerriAI/litellm/issues/36164)；provider 列表中缺少 Nano-Gpt [`#34499`](https://github.com/BerriAI/litellm/issues/34499)；Z.AI 的凭据/模型表单字段未渲染 [`#39310`](https://github.com/BerriAI/litellm/issues/39310)。
- 本窗口内无新增硬件后端（CUDA/ROCm/Metal/CPU）或量化格式。

---

## 4. 性能与优化

- **Router 迁移 → Rust。** 三个堆叠的 PR 已进入评审：[`#49118`](https://github.com/BerriAI/litellm/pull/49118) 引入 `RoutingContext`，使策略/子路由不再持有整个 `Router`；[`#49119`](https://github.com/BerriAI/litellm/pull/49119) 将 `PythonCore` 抽取到 `RouterCore` 接口之后，`litellm.Router` 成为薄门面；[`#49120`](https://github.com/BerriAI/litellm/pull/49120) 新增 Rust 核心，在 `LITELLM_RUST` 之后提供 completions/messages/embeddings/responses 路由，按配置回退到 Python，且开关关闭时行为零变化。尚未公布基准测试。
- [`#49228`](https://github.com/BerriAI/litellm/pull/49228) —— 日志热点路径：base64 图片正则扫描现在仅对包含 `;`、`data:` 和 `;base64,` 的字符串执行，而不再对每个成功请求的每条消息字符串执行。此改动基于 #45132 的线性扫描修复。
- [`#34031`](https://github.com/BerriAI/litellm/issues/34031)（已关闭）—— 无界摄入上游错误正文此前会导致事件循环停滞和 RSS 暴涨（在约 114 MB 的 HTTP 400 校验转储中观察到）；代理错误正文现在在正则脱敏前已做边界限制。
- [`#24720`](https://github.com/BerriAI/litellm/issues/24720)（已关闭）—— `async_log_success_event` 中的丢失更新竞争在并发下使基于延迟的路由退化为按计数加权的随机选择（每组 16 个 Anthropic + 4 个 OpenAI key）。
- [`#34399`](https://github.com/BerriAI/litellm/issues/34399)（已关闭）—— `Router._time_to_sleep_before_retry` 现在对多部署模型组也会遵循上游的 `Retry-After`，而不仅仅是单部署；此前会对限流的共享上游造成即时重试风暴。

---

## 5. 稳定性与回归

**高**

- [`#49179`](https://github.com/BerriAI/litellm/issues/49179) **[未关闭，无修复 PR]** —— 在有请求进行中时调用带 `budget_limits` 的 `/key/update`，会将该请求的成本从 `LiteLLM_BudgetWindowSpend` 中丢弃。`LiteLLM_SpendLogs` 和 key 的 `spend` 列仍保持正确，因此基于窗口的预算执行会静默少计。**对任何将窗口预算用作硬上限的用户而言，这是数据面正确性问题。**
- [`#49356`](https://github.com/BerriAI/litellm/pull/49356) **[未关闭的修复]** —— 在普通 Anthropic 部署上，当上游返回 200 但 `content` 为 null/缺失时，`/v1/messages` 返回 500。此回归由 `#48254` 引入，后者开始在请求路径上为计价转换所有原生 Messages 正文。
- [`#49227`](https://github.com/BerriAI/litellm/pull/49227) **[未关闭的修复]** —— 失败的 agentic 后续调用（例如 web 搜索后的限流）此前被吞掉；Claude Code 收到 200 并被告知调用未声明的工具，报告 “Did 0 searches”。影响所有 agentic hook。

**中**

- [`#48570`](https://github.com/BerriAI/litellm/issues/48570)（已关闭）—— `import litellm` 在 **Python 3.15** 上失败（`sre_constants` 被移除）；问题出在 `router_strategy/complexity_router/config.py` 中的无条件导入。相关依赖清理见 [`#49347`](https://github.com/BerriAI/litellm/pull/49347)，将 `importlib-metadata` 限制在 Python <3.10。
- [`#34479`](https://github.com/BerriAI/litellm/issues/34479)（已关闭）—— 多 worker 部署下耗尽 PostgreSQL `max_connections` 导致**所有**用户 API key 失败。连接池大小仍是运维责任。
- [`#26237`](https://github.com/BerriAI/litellm/issues/26237)（已关闭）—— 瞬时的 Postgres/HAProxy 故障表现为有效且已配置的模型报 “Invalid model name”。
- [`#49348`](https://github.com/BerriAI/litellm/pull/49348) **[未关闭的修复]** —— Vertex 服务端 Google Search 调用以服务端 `toolCall` 部件（而非 grounding 元数据 `webSearchQueries`）到达时，此前按零成本记录。
- [`#49244`](https://github.com/BerriAI/litellm/pull/49244) **[未关闭的修复]** —— 后台健康检查会对 image/video 部署执行真实生成；一个 Gemini 图片模型在零流量下每次检查被计费约 **$0.135**。
- [`#49213`](https://github.com/BerriAI/litellm/issues/49213)（已关闭）—— API keys UI 表格在存在 99 个 key 时截断为 49 行且无分页。

**较低 / 转换层（大多已关闭）**

- [`#26252`](https://github.com/BerriAI/litellm/issues/26252) —— `websearch_interception` 在 Claude Code → Bedrock 直通场景下从不触发；所引用的修复（`#25242`）据称通过新的 Bedrock 跳过逻辑再次破坏它，因此根因仍有争议。
- [`#45546`](https://github.com/BerriAI/litellm/issues/45546) —— Mistral 的 `_strip_output_only_fields` 在重放前删除了 `reasoning_content`/`thinking_blocks`；文档要求以 `thinking` chunk 形式重放。
- [`#43012`](https://github.com/BerriAI/litellm/issues/43012) —— Anthropic 的 `stop_reason: model_context_window_exceeded` 被映射为 `"stop"` 而非截断信号。
- [`#26334`](https://github.com/BerriAI/litellm/issues/26334) —— `response_format` + `thinking` 在 `vertex_ai/claude-opus-4-7` 上返回 400。
- [`#27513`](https://github.com/BerriAI/litellm/issues/27513) —— Bedrock 重试路径在签名后可能重放陈旧的 SigV4 头。
- [`#46872`](https://github.com/BerriAI/litellm/issues/46872) —— 编辑带 `access_windows` 的模型返回 500（`Object of type time is not JSON serializable`）。
- [`#47777`](https://github.com/BerriAI/litellm/issues/47777) —— key 级 `router_settings.fallbacks` 在 `/v1/images/generations` 上被忽略。
- [`#47261`](https://github.com/BerriAI/litellm/issues/47261) —— Ollama embeddings 忽略 `api_key`、额外请求头和调用方超时。
- [`#45536`](https://github.com/BerriAI/litellm/issues/45536) / [`#49344`](https://github.com/BerriAI/litellm/pull/49344) —— Perplexity Search 丢弃了 `search_recency_filter`、日期过滤器、语言和模式；现已转发，并将 provider 校验错误传播给调用方。

---

## 6. 对应用开发者的意义

- **暂时不要把窗口预算当作硬上限。** 如果你依赖 `budget_limits` 窗口做租户隔离，#49179 可能在并发 `/key/update` 操作期间漏计成本。在修复落地前，请对照 `LiteLLM_SpendLogs` 或 key 的 `spend` 列进行核对。
- **媒体健康检查可能在花钱。** 如果你运行 image/video 生成部署，请立即审计健康检查流量；30 秒间隔下每次检查约 $0.135 并非小数目。#49244 合并后将改变默认行为。
- **经 LiteLLM 使用 Claude Code 仍是摩擦最大的路径。** 本窗口触及了 web 搜索拦截、`thinking.type=adaptive`、`output_config.effort`、Azure/Foundry 上的 `reasoning.effort`、`metadata.user_id` → `user` 映射，以及 agentic 后续调用的错误传播。请固定版本，并测试 `content` 为空/null 的 `/v1/messages` 响应 —— 该路径目前会 500。
- **Python 3.15 尚不可用。** 请停留在 ≤3.14，并预计 `sre_constants` 移除会在其他传递路径中浮现。
- **Router 内部正在变动。** `RoutingContext` / `PythonCore` / Rust 核心这套栈目前行为上无变化（开关关闭即无操作），但自定义 router 子类或任何触及 `Router` 私有属性的代码应迁移到有文档的 endpoint 接口面。
- **成本归因正在改进，利于费用分摊。** [`#49360`](https://github.com/BerriAI/litellm/pull/49360) 在每日使用导出中增加逐行的 key 和 user `metadata`（不再需要逐行调用 `/key/info` + `/user/info`），[`#49133`](https://github.com/BerriAI/litellm/pull/49133) / [`#49190`](https://github.com/BerriAI/litellm/pull/49190) 为计费流水线引入可选启用的持久化、确认式使用记录。
- **固定并验证镜像。** 本窗口仅有 dev 构建；部署到生产前请使用 `e82a3c6` 密钥进行 cosign 验证。

</details>

<details>
<summary><strong>Unsloth</strong> — <a href="https://github.com/unslothai/unsloth">unslothai/unsloth</a></summary>

# Unsloth 摘要 — 2026-10-31

## 今日亮点
Unsloth 发布了 **v0.1.913-beta**，这是一个 UI/UX 与性能版本，新增自定义背景、缩短应用更新时间、加速 Linux 桌面应用，并让 Qwen-Image 生成在低显存 GPU 上可行；它还将 `DeepSeek-V4.1-Flash-1017` 加入 Dynamic v3.1 GGUF 阵容。在 kernel 侧，团队正在积极重构注意力调度——Gemma 3 正从 `flex_attention` 的回退路径迁移到用于 decode 的 SDPA，同时保留 flex 用于长提示词 prefill，并修复 torch 2.8/2.9 上因果掩码静默丢失的问题。Studio 势头延续：具备音频能力的 LFM3 模型，以及基于 Flows 的数据/训练配方，但围绕 `UNSLOTH_STUDIO_HOME` 的 incident 级安装回归问题需要关注。

## 版本发布与破坏性变更
- **[v0.1.913-beta](https://github.com/unslothai/unsloth/releases)** — 自定义（自定义背景）、改进的 UI/UX、更快的应用更新时间、Linux 应用加速，以及在有限显存下更快的 Qwen-Image 生成。
- **本版本未记录 API/配置层面的破坏性变更**，但需注意已报告的隔离安装行为回归：[#16186](https://github.com/unslothai/unsloth/issues/16186) / [#16185](https://github.com/unslothai/unsloth/issues/16185)（OPEN，重复提交）声称 `UNSLOTH_STUDIO_HOME=<path> ./install.sh --local` 现在会静默覆盖现有 baseline venv，而不是创建完全隔离的运行时。如果你依赖多租户或按项目隔离的 Studio home，请固定安装器版本，或在升级前验证隔离性。
- 更新路径可靠性仍是一个未解决的抱怨：[#15866](https://github.com/unslothai/unsloth/issues/15866)（OPEN）——“Unsloth 更新失败。”

## 新增模型与硬件支持
- **DeepSeek-V4.1-Flash-1017** 已加入 Unsloth Dynamic v3.1 GGUFs（预览）——[docs](https://unsloth.ai/docs/models/deepseek-v4.1-flash)，在 v0.1.913-beta 中公布。
- **LFM3-Omni 音频输入**（以及导出、LoRA 默认值和自定义代码生成的 Stop）——[PR #16242](https://github.com/unslothai/unsloth/pull/16242)。此前 `LiquidAI/LFM3-Omni-2B` 加载为纯视觉（`audio_type=None`）。
- **LFM3-Audio-2B 聊天**（音频输入、文本输出），取代此前的加载拒绝——[PR #16243](https://github.com/unslothai/unsloth/pull/16243)。
- **集成 GPU 量化路径**（Strix Halo、Jetson、DGX Spark）：原生 int8 host offload 现在会遵循 `host_pinning_allowed`，而不是始终固定——[PR #16235](https://github.com/unslothai/unsloth/pull/16235)。
- **Apple MLX** 修复已合入/关闭：Studio UI 中 Dolphin Venice Edition 渲染（[#15858](https://github.com/unslothai/unsloth/issues/15858)），以及 LFM3 MLX 模型未出现在 `curl /v1/models` 中（[#15832](https://github.com/unslothai/unsloth/issues/15832)）。
- **AMD/Vulkan**：RX 6800 上 LFM3-Omni 视频输入失败（[#16065](https://github.com/unslothai/unsloth/issues/16065)）以及 Windows 11 上 LFM3-Omni safetensors 加载失败（[#16054](https://github.com/unslothai/unsloth/issues/16054)）均已关闭。
- **ModelScope**：大于 50 GB 的模型下载曾被阻止；该问题已关闭——[#15989](https://github.com/unslothai/unsloth/issues/15989)。

## 性能与优化
- **Gemma 3 注意力路径拆分**——[PR #16041](https://github.com/unslothai/unsloth/pull/16041)：在 torch 2.10–2.14.1 上，`flex_attention` 在 L4 / A10 / RTX 3090 / 4090 / L40S 上仍保持编译（通过 #16049、#16073），但 flex 在单 token decode 时*比 SDPA 更慢*，而在长提示词 prefill 时*快得多*。该 PR 将生成路由到非 flex 路径。这是当前进行中的、对 decode 密集型服务吞吐量最相关的一项变更。
- **编译后 flex 因果掩码的正确性/性能**——[PR #16234](https://github.com/unslothai/unsloth/pull/16234)：在 torch 2.8/2.9 上，Dynamo 将 `hasattr(query, "dim")` 求值为 `False`，导致 `_dropped_causal_mask` 落入默认分支，并使原生 flex attention 收到 `attention_mask=None`（双向注意力）。已在 torch 2.10 上游修复。影响所有在 2.8/2.9 上使用逐层编译块的用户（#10744，release `2026.10.6`）。
- **融合损失重编译**——[PR #15575](https://github.com/unslothai/unsloth/pull/15575)：trainer 侧的融合调用计数器（`_unsloth_dpo_chunked_calls`、`_unsloth_pref_chunked_calls`、`_unsloth_gkd_*`、PPO/RLO）在 `torch.compile` 下每个 step 都会被重新编译；计数器已移出被追踪代码，且收窄了 TRL head 契约。
- **v0.1.913-beta**：缩短应用更新时间，加快 Linux 桌面应用启动；在显存受限时加速 Qwen-Image 生成。
- **显存估算准确性**——[#15935](https://github.com/unslothai/unsloth/issues/15935)（CLOSED）：MLX 估算器为一个实际可在 24 GB Mac 上加载的模型报告了 69.7 GiB。在确认修复前，请谨慎对待 MLX 估算器。

## 稳定性与回归
按严重程度排序：

1. **事件级（OPEN）**——[#16186](https://github.com/unslothai/unsloth/issues/16186) / [#16185](https://github.com/unslothai/unsloth/issues/16185)：`UNSLOTH_STUDIO_HOME` 隔离安装会静默覆盖现有 baseline venv，破坏交叉污染保障。本数据集中没有关联的修复 PR。
2. **高（OPEN）**——[#16178](https://github.com/unslothai/unsloth/issues/16178)：托管账户加载缓存的 gated 模型后，Studio 图像生成返回 404。
3. **高（OPEN）**——[#16187](https://github.com/unslothai/unsloth/issues/16187)：`search_conversation` 工具已完全消失；相关的长对话故障已在 [#14708](https://github.com/unslothai/unsloth/issues/14708)（自动压缩后附件不可读）和 [#15800](https://github.com/unslothai/unsloth/issues/15800)（返回长对话时上下文未压缩）中关闭。
4. **中（OPEN）**——[#15999](https://github.com/unslothai/unsloth/issues/15999)：AppImage Studio 的 UI 非常卡顿；[#15866](https://github.com/unslothai/unsloth/issues/15866)：更新器失败。
5. **中（OPEN）**——[#16221](https://github.com/unslothai/unsloth/issues/16221)：ShareGPT 图像列表通过数据集格式检查，但在下游失败。
6. **低（OPEN）**——[#16195](https://github.com/unslothai/unsloth/issues/16195)：对于 Unsloth outputs 文件夹之外的路径，`unsloth list-checkpoints --outputs-dir` 会打印 traceback。
7. **今日已关闭**——Linux 主题切换中止 `WebKitWebProcess` 并冻结窗口（[#16028](https://github.com/unslothai/unsloth/issues/16028)）；Windows/AMD `llama-server` 在 GGUF 加载后持有约 16 GB commit charge（[#16015](https://github.com/unslothai/unsloth/issues/16015)）；eval 数据集任务名与 YAML 任务冲突（[#15982](https://github.com/unslothai/unsloth/issues/15982)）；聊天文本区在多个标签页间重复（[#15782](https://github.com/unslothai/unsloth/issues/15782)）；HF gated 仓库 token 访问（[#8604](https://github.com/unslothai/unsloth/issues/8604)）。
8. **CI/测试信号问题**——[PR #16244](https://github.com/unslothai/unsloth/pull/16244) 指出 `test_build_group_layout_single_read_same_inputs` 在 main 上失败（`assert 0 == 1`）；[PR #16245](https://github.com/unslothai/unsloth/pull/16245) 修复 40 个 worker 时 xdist worker 端口块回绕问题；[PR #16236](https://github.com/unslothai/unsloth/pull/16236) 修复了一个 hub-source 测试，该测试假定使用 Hugging Face，而不是继承的 `UNSLOTH_STUDIO_HUB_SOURCE`。

## 这对应用开发者意味着什么
- **固定你的安装版本。** `UNSLOTH_STUDIO_HOME` 回归问题是唯一可能静默破坏现有环境的一项。在解决前，请使用容器或显式固定版本，尤其是在同一主机上运行多个 Studio 实例时。
- **Gemma 3 的 decode 延迟应会改善。** flex→SDPA 生成拆分（[#16041](https://github.com/unslothai/unsloth/pull/16041)）针对的是多数面向用户的应用所关心的逐 token 路径，同时保留 flex 在长系统提示词和 RAG 上下文中的 prefill 优势。
- **如果依赖编译后的 flex attention，请审查 torch 版本。** 在 torch 2.8/2.9 上，因果掩码可能静默退化为双向注意力（[#16234](https://github.com/unslothai/unsloth/pull/16234)）——这是正确性 bug，看起来像质量问题而非崩溃。优先使用 torch 2.10+，或合入该 PR。
- **多模态音频正在到来。** LFM3-Omni 和 LFM3-Audio-2B 支持（[#16242](https://github.com/unslothai/unsloth/pull/16242)、[#16243](https://github.com/unslothai/unsloth/pull/16243)）正通过类 OpenAI 本地服务器落地到 Studio，但请注意 AMD/Vulkan 和 Windows 路径才刚刚关闭阻塞性 bug。
- **不要盲目相信显存估算器。** MLX 的 69.7 GiB 与 24 GB 差异（[#15935](https://github.com/unslothai/unsloth/issues/15935)）以及缺少按模型资源可见性（[#16055](https://github.com/unslothai/unsloth/issues/16055)，OPEN）意味着在确定集群规模前应基于实测验证显存余量。
- **托管/团队部署：** 私有 loopback HTTP MCP 服务器仍对托管账户禁用（[#16029](https://github.com/unslothai/unsloth/issues/16029)，作为功能请求关闭），因此请围绕公网端点或所有者账户来规划 MCP 拓扑。
- **Flows 正在成为自动化界面。** Data Recipes、带留出拆分的完整 Train 节点（[#15604](https://github.com/unslothai/unsloth/pull/15604)、[#15611](https://github.com/unslothai/unsloth/pull/15611)），以及针对下载检测和运行后卸载的模型生命周期修复（[#16239](https://github.com/unslothai/unsloth/pull/16239)、[#16238](https://github.com/unslothai/unsloth/pull/16238)），表明图编排式微调是发展方向——现在值得据此做原型验证。

---

</details>