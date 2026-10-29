# AI 基础设施日报 2026-10-30

> 生成时间: 2026-10-29 18:48 UTC | 覆盖项目: 6 个

- [vLLM](https://github.com/vllm-project/vllm)
- [SGLang](https://github.com/sgl-project/sglang)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [Ollama](https://github.com/ollama/ollama)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Unsloth](https://github.com/unslothai/unsloth)

---

## 横向对比

# 跨项目对比报告 — AI 基础设施，2026-10-30

## 1. 生态概览

生态系统正处于加固阶段而非发布阶段：vLLM 和 SGLang 未发布新版本，而是集中处理 KV 缓存正确性、连接器可靠性以及特定后端的回归问题；llama.cpp、Ollama、LiteLLM 和 Unsloth 则通过构建、补丁和 Studio 修复持续推进。当前主要技术断层线是 KV 缓存迁移与复用——卸载层级、NIXL/Mooncake 连接器、前缀缓存和会话感知路由——如今这已成为正确性和多租户隔离问题，而不再只是吞吐量杠杆。硬件碎片化同样明显：SM120 Blackwell 在 vLLM/SGLang 路径中缺少所需的稀疏 MLA 内核，而 ROCm、SYCL、Hexagon、MLX 和 XPU 工作则处于不同成熟度。Agent 工作负载正暴露出服务引擎和网关中的工具调用、推理往返、语法/模式以及确定性缺口。网关计量/护栏和微调数据掩码仍然不够成熟，生产团队仍需下游控制和验证。

## 2. 活动对比

以下计数是各 24 小时摘要中引用的不同 GitHub issue/PR 编号，并非仓库总量。它们反映维护者和报告者的关注集中在哪里。

| 项目 | 引用的 issue 数（24 小时） | 引用的 PR 数（24 小时） | 发布状态 |
|---|---:|---:|---|
| **vLLM** | 21 | 12 | 24 小时内无发布；未宣布 API/配置破坏性变更。 |
| **SGLang** | 18 | 18 | 24 小时内无发布；无破坏性变更。 |
| **llama.cpp** | 20 | 25 | 无 API/配置破坏性变更；围绕 `b11972`–`b11985` 持续构建/打标签。 |
| **Ollama** | 15 | 9 | **v0.40.13 已发布**：LFM3 系列支持 Linux/Windows；无 API/配置破坏性变更。 |
| **LiteLLM** | 16 | 14 | **v1.108.0-rc.1** 以及稳定补丁 **v1.106.6**、**v1.105.7**；多个破坏性行为 PR 仍开启。 |
| **Unsloth** | 17 | 17 | 无带标签发布；`v0.1.912-beta` 已在现场使用；合并/修复密集日。 |

## 3. 模型支持竞赛

| 项目 | 窗口期内模型/硬件支持进展 | 定位 |
|---|---|---|
| **vLLM** | 没有新的模型/后端支持被合并。进行中：Intel XPU Mooncake 修复、面向 KVPP 的 MLA 缓存分片、打包 MLA 块几何。**SM120 上的 DeepSeek-V4.1-Flash 被阻塞**，因为 FlashInfer 0.7.0 缺少用于 `page_block_size=32` 的稀疏 MLA 解码内核；GLM-5.3 优化跟踪仍在继续。 | 在 KV/连接器管线方面较强，但在最新 SM120 模型启用方面落后。 |
| **SGLang** | 推进了对 **KimiK3** 的支持（通过 FlashInfer AllReduce Fusion）、**nemotron-h** CuTe DSL W4A16 MoE、NPU 上的 **HiDream-O1-Image**，以及 XPU `sage_attn`；RDNA3/RDNA4 上游化提案仍开启。SM120 上的 DeepSeek-V4.1-Flash 和 GLM-5.3-Flash 存在活跃的正确性问题。 | 本窗口期在新架构/后端 PR 的广度上略领先，但后端正确性拖了后腿。 |
| **llama.cpp** | 已交付/推进了面向视觉/多模态的 **Hexagon UPSCALE**、**量化 KV 上的 SYCL DPAS flash attention**、OpenCL IQ 量化覆盖、**ROCm/HIP RDNA4_M**、FP8/NVFP4 栈、LFM3 audio/omni 量化保护，以及 RPC 异步/事件 API。 | 在本地/边缘后端广度和量化覆盖方面明显领先。 |
| **Ollama** | **v0.40.13** 将 LFM3、`lfm3-audio` 和 `lfm3-omni` 扩展到 Linux 和 Windows。MLX runner 的 Windows/CPU 后端 PR 仍开启。`gpt-oss:120b` 的 MXFP4 大型 MoE 加载已损坏；不支持三值量化。 | 在开箱即用的本地模型打包方面领先；在大型 MoE 和面向 Agent 的正确性方面落后。 |
| **LiteLLM** | 推进了 DashScope 图像编辑/TTS、OpenAI 实时翻译和流式 `gpt-transcribe`、Azure AI Foundry Agents v2、`nokeep` 零保留提供商，以及 CLF AI Gateway 模型。 | 在提供商/API 网关广度方面领先；不是推理引擎。 |
| **Unsloth** | MLX 上的 LFM3 Audio/Omni 已落地（外加修复）、Apple MLX ANE 预填充开关、多 GPU 音频加载、AMD iGPU 处理、NVFP4 Apple Silicon 修复。通用 LFM3 1.7B 支持仍是一个未关闭的请求。 | 在易用的微调和 Apple/消费级硬件方面领先；通用 LFM3 支持不完整。 |

**谁领先：** 没有单一项目在整个栈上领先。对于数据中心服务，**SGLang** 在本窗口期的新模型/后端启用方面似乎略领先，而 **vLLM** 仍保有更强的 KV/卸载和连接器广度。对于本地/边缘，**llama.cpp** 在深度上领先，**Ollama** 在打包上领先。**LiteLLM** 领先网关层，**Unsloth** 领先易用的微调/Studio 工作流。

## 4. 性能前沿

| 前沿 | 今日摘要中的证据 | 方向 |
|---|---|---|
| **KV 缓存与内存迁移** | vLLM：NIXL/Mooncake/P2P 卸载、MLA 缓存分片、KVPP、卸载最近性正确性。SGLang：Mooncake SWA 打包、decode 主机接收、前缀缓存行为。llama.cpp：FP8 KV 缓存、量化 KV 上的 SYCL DPAS。Ollama：KV 状态泄漏和 VRAM 驱逐修复。Unsloth：MLX 内存估算和上下文压缩。 | 主战场。工作重心正从原始容量转向分层、正确性和多租户隔离。 |
| **调度与批处理** | vLLM：准入退避，防止 KV 池饱和将 decode TPOT 抬高约 2.3×。SGLang：最短预填充优先的预算核算、上下文并行、调度器统计。Ollama：投机解码 A/B 和调度器驱逐。Unsloth：分组 GEMM MoE LoRA 和 T4 NF4 批大小交叉点。 | 尾延迟、公平性和多任务效率。 |
| **量化** | llama.cpp：FP8/OCP FP8/NVFP4、OpenCL IQ、SYCL DPAS 量化 KV。Unsloth：NF4/NVFP4/MLX，T4 NF4 decode 在批大小为 4 时提升 13–30%。Ollama：MXFP4 大型 MoE 损坏。vLLM/SGLang：fp8 混合批次和 MXFP4 MoE 跟踪。 | 更激进的格式，但各后端的数值风险仍然很高。 |
| **分布式服务** | vLLM：NIXL 拉取、P2P KV 层、MLA 分片、ROCm 多进程挂起。SGLang：AllReduce 融合、EPLB、上下文并行、Mooncake。llama.cpp：RPC 流水线并行。LiteLLM：最不繁忙路由预留修复。 | KV 传输、集合通信融合和缓存感知路由是关键分布式杠杆。 |
| **内核/后端** | vLLM：DiffKV SM80 分块在 200K 上下文分块上 **3.0×**。SGLang：Qwen3 融合 QK-norm/RoPE 复用。llama.cpp：Metal MXFP4 mat-vec、SYCL DPAS、Hexagon IM2COL。Ollama：面向 248K 词表行的 MLX top-k。Unsloth：视频导出 **115–184 秒 → 约 1–2 秒**。 | 后端特定内核优化占据主导；不同硬件的性能差异很大。 |

**净结论：** 大部分优化精力集中在 **KV 缓存迁移和后端内核**，其次是调度/批处理。量化正日益与 KV 缓存设计耦合，尤其是 FP8/NVFP4 和量化 KV 注意力。

## 5. 层级定位

| 层级 | 项目 | 主要角色 | 当前信号 |
|---|---|---|---|
| **数据中心服务引擎** | **vLLM**、**SGLang** | 高吞吐 GPU 推理、KV/卸载、分布式服务、OpenAI 兼容前端 | vLLM 在连接器/卸载广度上更强；SGLang 在调度器/上下文并行/Rust 前端以及扩散/NPU 实验上更强。 |
| **本地运行时** | **llama.cpp**、**Ollama** | 边缘/消费级/CPU/GPU 推理 | llama.cpp 是底层可移植性和量化层；Ollama 是开箱即用的模型分发和本地 API 层。 |
| **LLM 网关** | **LiteLLM** | 提供商抽象、路由、护栏、支出跟踪、OpenAI 兼容性 | 提供商覆盖广，但支出核算和护栏语义仍存在生产环境缺口。 |
| **微调/训练** | **Unsloth** | LoRA/微调、Studio、量化、消费级/Apple/AMD 支持 | 易用性和 MLX/消费级聚焦很强；数据掩码和内存估算问题需要验证。 |

重叠正在增加：vLLM 和 SGLang 暴露 OpenAI 兼容前端；Ollama 和 Unsloth Studio 可以提供本地 OpenAI 兼容端点；LiteLLM 可路由到其中任何一个。但它们的核心层级仍然不同。

## 6. 趋势信号

1. **KV 缓存正在成为控制平面。** 会话感知 KV 提示正出现在 vLLM（#52113）和 SGLang（#43098, #45189）中，而重启语义（#55155）和静默损坏（#64117）仍未关闭。Agent 开发者应围绕稳定会话 ID、缓存局部性感知路由和输出验证来设计，而不是假设缓存复用是透明的。

2. **硬件后端固定仍是强制要求。** SM120 Blackwell 在 vLLM 中缺少内核（#59203），在 SGLang 中出现注意力崩溃（#42012）；ROCm 多进程挂起在 vLLM 中持续存在（#64549, #62588）；SYCL 在 llama.cpp 中独立出现约 30% 的 MoE 预填充回退（#31262, #31068）。固定后端、版本和镜像摘要；对你实际部署的 `llama-server` 或引擎配置进行基准测试。

3. **面向 Agent 的正确性正成为新的采用门槛。** 工具调用仍然脆弱：Ollama MLX `qwen3.8` 静默无法输出 `tool_calls`（#19353），vLLM Muse 解析器改变字符串语义（#64546），LiteLLM 的 Anthropic 服务端工具修复改变 Agent 调度（#48385）。添加 schema 校验、规范化内容数组，并保留非工具回退路径。

4. **网关支出和护栏不能作为唯一控制手段被信任。** LiteLLM 流式 OpenAI 兼容流量可能记录为 `$0`（#48937）；Lakera v2 `on_flagged: block` 此前在仅 PII 检测时失效放行（#48944）；`print_verbose` 可能泄漏 API 密钥（#34705）。在下游强制执行预算，并明确审计护栏行为。

5. **量化 KV 和 FP8/NVFP4 正在进入生产——但有注意事项。** llama.cpp 的 FP8 KV 缓存已进入评审，并在 `q4_0`/`q8_0` KV 上使用 SYCL DPAS；Unsloth 正在改进 NF4/NVFP4 和 MLX；vLLM 跟踪 fp8 混合批次问题。现在可对长上下文成本节省进行原型验证，但要按后端验证数值。

6. **投机解码仍是高风险点。** SGLang EAGLE 挂起（#35822）、llama.cpp 在图像输入上的 draft-KV 空洞（#27408）和 MTP 上下文大小设置（#28433），以及 vLLM 结构化输出/投机解码 RFC（#62818），都显示出相同模式：失败要么是硬错误，要么是静默质量变化。保留非投机回退路径。

7. **本地/边缘多模态支持正在扩展，但回滚和验证较弱。** Ollama 在 Linux/Windows 上增加了 LFM3 audio/omni，但仍没有受支持的模型摘要回滚（#19385）；Unsloth 增加了 ANE 预填充和 AMD iGPU 处理；llama.cpp 增加了 Hexagon/RDNA4 覆盖。将模型摘要作为部署项固定，并按主机测试音频/工具路径。

8. **可观测性和缓存感知路由正在成为产品功能。** SGLang 的 Rust 前端正在增加按请求的调度器统计和缓存层级细分（#46963, #46961）；LiteLLM 正在修复最不繁忙路由的突发塌缩问题（#47484）；vLLM 正在增加 HTTP keep-alive 可配置性（#60459）。Agent 平台应准备好支持缓存局部性感知路由和按请求的成本/延迟归因。

---

## 各项目详细报告

<details>
<summary><strong>vLLM</strong> — <a href="https://github.com/vllm-project/vllm">vllm-project/vllm</a></summary>

# vLLM 摘要 — 2026-10-30

## 今日亮点

过去 24 小时内没有新的 vLLM 版本发布。活动主要围绕 **KV 卸载与连接器可靠性**——NIXL、Mooncake 和 P2P 分层——展开，包括一个静默 KV 损坏 bug，以及对端故障时 fail-fast 缺失的问题。最受关注的阻塞项仍是 **SM120 上的 DeepSeek-V4.1-Flash**：其压缩层 `page_block_size=32` 没有匹配的 FlashInfer sparse-MLA decode kernel；与此同时，性能工作推进了 DiffKV SM80 tiling 和 DeepSeek V4.1 Engram 预取。

---

## 发布与破坏性变更

过去 24 小时无发布；本时间窗口内未宣布 API 或配置破坏性变更。

---

## 新模型与硬件支持

本时间窗口内没有合并新的模型或后端支持。进行中的启用工作与阻塞项：

- **SM120（RTX PRO 6000 Blackwell）上的 DeepSeek-V4.1-Flash 被阻塞。** 压缩层路径使用 `page_block_size=32`，但 FlashInfer 0.7.0 仅为 `pbs=64` 实例化 sparse-MLA decode kernel，因此该模型完全无法在 SM120 上运行。24 条评论——当日最活跃的 issue。[#59203](https://github.com/vllm-project/vllm/issues/59203)
- **GLM-5.3 优化跟踪**继续围绕共享的 `glm_moe_dsa` 架构进行，并在 GLM-5.2 优化之外提出了额外的 CUDA 工作。[#57406](https://github.com/vllm-project/vllm/issues/57406)
- **Intel XPU Mooncake 支持**：PR 修复了 `MooncakeStoreConnector` 中的两处 CUDA 假设（特别是 XPU 上 `torch.cuda.Event` 注解求值问题）。[#62546](https://github.com/vllm-project/vllm/pull/62546)
- **面向 KVPP 的 MLA cache 分片**：可选的 `--enable-kvpp` 增加按层分片的 MLA KV cache，并在 PCP × TP 副本组之间通过 NCCL 广播预取。[#59059](https://github.com/vllm-project/vllm/pull/59059)
- **Packed MLA block 几何结构**：修复为 TP1 DeepSeek-V4-Flash NIXL P/D 引擎保留混合粒度缓存几何结构。[#50717](https://github.com/vllm-project/vllm/pull/50717)

---

## 性能与优化

- **SM80 上的 DiffKV prefill tiling**：`BLOCK_M=128` + KV tile 64 在 `TRITON_ATTN_DIFFKV` 的 200K 上下文分块上带来 **3.0×** 提升；此前的 `BLOCK_M=16` 会针对每个 query 位置重新加载整个 KV tile。[#61095](https://github.com/vllm-project/vllm/issues/61095)
- **KV 池饱和时的准入重试使 decode TPOT 增大约 2.3×**（Ascend 910B / V1 调度器）；提议采用自动准入退避。该机制与平台无关。[#64460](https://github.com/vllm-project/vllm/issues/64460)
- **ROCm 滑动窗口 prefill**：在 `ROCM_ATTN` prefix prefill 中跳过完全被 mask 的上下文 tile；输出逐 bit 一致，仅省略窗口之前的 tile。[#63867](https://github.com/vllm-project/vllm/pull/63867)
- **DeepSeek V4.1 Engram 预取**：可选的 Numba worker 对 prompt token 做哈希，并在 eager prefill 之前为 PCIe 连接的 GPU 收集 CPU 卸载的 Engram 行。[#64500](https://github.com/vllm-project/vllm/pull/64500)
- **Unified-attention TD 循环**：将 tensor descriptor 构造提升到每 tile 循环之外，避免每次迭代执行 `tensormap_create`，并恢复流水线。[#51506](https://github.com/vllm-project/vllm/pull/51506)
- **NIXL pull receiver**：面向大型 NIXL pull 的可选后台 receiver，将 descriptor 准备、READ 提交、轮询和 handle 释放移出 decode 模型线程。[#57987](https://github.com/vllm-project/vllm/pull/57987)
- **卸载近期性正确性/性能**：将延迟卸载的 GPU block 返回到驱逐端而不是 MRU 端（否则 CPU 持有的陈旧 block 会比更新的 block 存活更久）。[#59383](https://github.com/vllm-project/vllm/pull/59383)；同时在 CPU 卸载近期性中记录 GPU 本地前缀复用。[#57746](https://github.com/vllm-project/vllm/pull/57746)

---

## 稳定性与回归

**严重**

- **BHLNC 下 `MooncakeStoreConnector` 中的静默 KV 损坏**：每个 head 的 segment 在传输时使用 whole-block stride 作为其长度。在 Qwen2.5-0.5B / T4 / vLLM 0.29.0 上出现静默数据损坏。本时间窗口内未发现直接修复的 PR。[#64117](https://github.com/vllm-project/vllm/issues/64117)
- **DeepSeek-V4.1-Flash 无法在 SM120 上运行**：缺少针对 `pbs=32` 的 FlashInfer sparse-MLA decode kernel 实例化。在 RTX PRO 6000 Blackwell 上构成硬性启动/运行时阻塞项。[#59203](https://github.com/vllm-project/vllm/issues/59203)

**高**

- **FlashMLA sparse decode 在 SM90 上重新分配 split-KV workspace**——#53413 的回归，可能导致 H200 在 fp8 mixed-batch 下运行时 OOM。[#59305](https://github.com/vllm-project/vllm/issues/59305)
- **P2P KV 卸载层在对端故障时不会快速失败**：请求可能挂起，而不是暴露对端故障；已在 H200 + mlx5 InfiniBand + NIXL 1.5.0 上复现。[#63602](https://github.com/vllm-project/vllm/issues/63602)
- **ROCm GLM-5.3 TP8 挂起**：当其他 vLLM 进程共享 MI325X SR-IOV VF 时，在 `OffloadingConnector` 的 CPU↔GPU 拷贝期间发生；生成量降为零，但请求仍在运行。[#64549](https://github.com/vllm-project/vllm/issues/64549)
- **ROCm 在 MI300X SR-IOV VF 上的多进程挂起**：两个或更多 vLLM 进程在几分钟内挂起——queue head dispatch 已接受，但没有 wave，GFX 100%。[#62588](https://github.com/vllm-project/vllm/issues/62588)
- **`custom_all_reduce.cuh:164 'invalid argument'`** 在多 GPU 配置下出现 CUDA 失败。[#56180](https://github.com/vllm-project/vllm/issues/56180)

**中等**

- **`dots.ocr` 在 TP=2 时对每个区域产生相同的“模糊图像”输出**（Ascend 910B）。[#64541](https://github.com/vllm-project/vllm/issues/64541)
- **`vllm/vllm-openai:unlimited-ocr` 镜像无法服务 Unlimited-OCR 模型。** [#64489](https://github.com/vllm-project/vllm/issues/64489)
- **Muse tool parser 对 `Optional[str]` 参数进行 JSON 解码**——`"10001"` 变成 `10001`，改变工具调用语义。[#64546](https://github.com/vllm-project/vllm/issues/64546)
- **Rust `vllm-bench` 在使用合成数据集时静默忽略 `--dataset-path`**，转而基准测试随机 prompt——导致基准结果失效。[#64538](https://github.com/vllm-project/vllm/issues/64538)

**本时间窗口内已关闭/解决**

- `/v1/messages` 在未指定 `--chat-template` 时提升对话中途的 system message，破坏 DeepSeek-V4.1-Flash 的前缀缓存。[#60537](https://github.com/vllm-project/vllm/issues/60537)
- `/v1/completions/derender` 丢弃了请求的 `prompt_logprobs`。[#57929](https://github.com/vllm-project/vllm/issues/57929)
- `kimi_k25_vit` 中裸用 `@torch.compile` 会在生命周期之外编译，并在进程范围内固定 `TRITON_CACHE_DIR`。[#52965](https://github.com/vllm-project/vllm/issues/52965)

**持续进行的正确性工作**

- **HiSparse 跟踪**：已修复 swap 容量 off-by-one 以及 long-prefill/decoder mixed-batch OOM；新修复在准入时为 in-flight import 的 host page 预留空间，避免两个等待中的 load 因彼此的 page 而死锁。[#60072](https://github.com/vllm-project/vllm/issues/60072), [#62979](https://github.com/vllm-project/vllm/pull/62979)
- **NIXL 加固**：在 receive 注册之前校验 `kv_transfer_params`，防止畸形客户端输入使 Decode EngineCore 崩溃。[#54807](https://github.com/vllm-project/vllm/pull/54807)
- **结构化输出 + 投机解码 RFC 已关闭**：解决将 draft token 裁剪为语法有效前缀时的输出分布保持问题。[#62818](https://github.com/vllm-project/vllm/issues/62818)

---

## 这对应用开发者意味着什么

- **在 #64117 修复之前，不要部署使用 BHLNC 布局、基于 Mooncake 的 KV 卸载**——其故障模式是静默 KV 损坏，而不是崩溃。要验证输出，而不只是可用性。
- **目前 Blackwell（SM120）上的 DeepSeek-V4.1-Flash 不可用。** 继续使用 Hopper/其他受支持的 SKU，或等待 FlashInfer 的 `pbs=32` sparse-MLA kernel。
- **工具调用正确性问题**：如果使用 `--tool-call-parser muse`，字符串类型参数可能以整数形式到达。请在客户端为 ID、ZIP code 以及其他看起来像数字的字符串增加 schema 级校验。
- **Rust `vllm-bench` 的基准结果不可信**：当传入 `--dataset-path` 且使用合成数据集设置时——在将数字用于容量规划之前，请验证 prompt 来源。
- **Agentic 工作负载有一项开放的 RFC：会话感知的 KV cache 提示**（释放已完成分支、固定即将恢复的 agent、共享长 system/tool 前缀）。如果你构建多 agent 系统，值得跟踪。[#52113](https://github.com/vllm-project/vllm/issues/52113)
- **KV 传输重启语义尚未支持**：NIXL connector 缺少重启生命周期 hook，这对快照/恢复和设备恢复流程很重要。[#55155](https://github.com/vllm-project/vllm/issues/55155)
- **前端可配置性正在改善**：`--http-timeout-keep-alive` 正在被加入 Python API server、CPU render server 和 Rust 前端。[#60459](https://github.com/vllm-project/vllm/pull/60459)

</details>

<details>
<summary><strong>SGLang</strong> — <a href="https://github.com/sgl-project/sglang">sgl-project/sglang</a></summary>

# SGLang 摘要 — 2026-10-30

## 1. 今日亮点
过去 24 小时内没有新发布，但活动主要集中在硬件后端正确性工作：在 SM120 上针对 GLM-5.3-Flash 的 `fa4` 注意力后端崩溃、DeepSeek-V4 在多模态流中止时导致调度器崩溃的 bug，以及影响 DFLASH 草稿模型的静默权重更新风险。性能方面，已有 PR 落地或推进：Qwen3 融合 QK-norm/RoPE 解码复用、MiniMax 稀疏解码索引器在 Hopper 上的上下文并行，以及扩大 K3 对 FlashInfer AllReduce Fusion 的覆盖。

## 2. 发布与破坏性变更
过去 24 小时内无。

## 3. 新模型与硬件支持
- **[PR #47306](https://github.com/sgl-project/sglang/pull/47306)** — 为 `KimiK3ForConditionalGeneration` 启用 FlashInfer AllReduce Fusion 自动启用（此前 `_FLASHINFER_ALLREDUCE_FUSION_ARCHS` 中只有 Kimi-K2.5）。
- **[PR #44750](https://github.com/sgl-project/sglang/pull/44750)** — nemotron-h：允许显式指定 CuTe DSL W4A16 MoE 路径。
- **[PR #45137](https://github.com/sgl-project/sglang/pull/45137)** — Diffusion/NPU：新增 HiDream-O1-Image 支持（Dev-2604、Dev、Full 变体）。
- **[PR #45485](https://github.com/sgl-project/sglang/pull/45485)** — SGLang-Diffusion XPU：为 `sage_attn` 增加 Triton 路径，移植自 SageAttention 内核。
- **[Issue #46900](https://github.com/sgl-project/sglang/issues/46900)** — 提议将 RDNA3/RDNA4（`gfx1100`/`gfx1201`）合入 main，并配套 CI 覆盖与上游化计划。
- **[Issue #38515](https://github.com/sgl-project/sglang/issues/38515)** — `sgl_kernel` AOT wheel 在 sm_75 上存在逐算子 cubin 覆盖缺口：`rmsnorm` 因 `cudaErrorNoKernelImageForDevice` 失败，而 `silu_and_mul`/`gelu_and_mul` 正常；且没有回退到 torch/Triton 的软回退。

## 4. 性能与优化
- **[PR #46908](https://github.com/sgl-project/sglang/pull/46908)** — Qwen3 解码：复用已有的基于表的 QK-norm/RoPE 融合内核，原地完成两者，移除每层一次 launch 以及中间的 Q/K 写/读，无需新内核。在 Qwen3-8B 上实测。
- **[PR #46597](https://github.com/sgl-project/sglang/pull/46597)** — minimax-sparse：在 Hopper 上以 TP4/TP8 运行解码索引器上下文并行。动机说明：在 128K 上下文下，否则每个 rank 在每个解码步骤的每个稀疏层都要为每个请求扫描约 33.5 MB。
- **[PR #44115](https://github.com/sgl-project/sglang/pull/44115)** — 为 EAGLE 向 FlashInfer target-verify plan 传入 `uniform_q_len`，让 FA2 CUDA-graph planner 获得其无法从 ragged CSR 推断的恒定步长 query 形状。
- **[PR #47308](https://github.com/sgl-project/sglang/pull/47308)** — 调度器：在 shortest-prefill-first 预留时同时考虑 chunk 预算和独立的 input 预算（例如：4096 token 的 chunk 预算与 2048 token 的 input 预算可能把 256 token 的等待者上限设为 3840 token）。
- **[PR #47307](https://github.com/sgl-project/sglang/pull/47307)** — AMD/Mooncake：默认关闭的 `SGLANG_MOONCAKE_SWA_PACKING` 在 prefill TP < decode TP 时收集目标本地 heads，并写入完整 SWA KV 页。
- **[PR #47106](https://github.com/sgl-project/sglang/pull/47106)** — Rust 前端：`RustServer.push_generation` 仅对携带 egress logprob 的行展平这些列，减少调度器线程上持有 GIL 的每步工作。
- **[PR #46592](https://github.com/sgl-project/sglang/pull/46592)**（已关闭）— EPLB：在多节点 full-EP 布局中、KV 缓存定容之前预热默认组 NCCL P2P 传输，避免首次再平衡时延迟建立跨节点连接。
- **[Issue #44304](https://github.com/sgl-project/sglang/issues/44304)** — 开放 Qwen3.8-Flash-Next 的 ROCm gfx950/MI355X 性能追踪（GatedDeltaNet、QuerySparse Attention、MXFP4 MoE、NEXTN MTP）。

## 5. 稳定性与回归
按严重程度排序：

1. **[Issue #47218](https://github.com/sgl-project/sglang/issues/47218)** — *严重。* 当并发中止的流下，多模态嵌入路径中的 `items_offset_list` 为 `None` 时，DeepSeek-V4.1-Flash 调度器崩溃；导致所有 TP/EP worker 挂掉并重启服务容器（`lmsysorg/sglang:dev-dsv41`）。
2. **[Issue #46806](https://github.com/sgl-project/sglang/issues/46806)** — *高 / 静默正确性。* `update_weights_from_disk` 没有 `selector`，因此权重更新可能把目标模型的权重加载到 DFLASH 草稿模型中。相同症状此前已在 THUDM/slime#1177 的 EAGLE3 外部草稿中记录。
3. **[Issue #45525](https://github.com/sgl-project/sglang/issues/45525)** — *高。* DeepSeek-V4-Flash：投机解码与普通解码产生不同的 greedy 输出。
4. **[Issue #47213](https://github.com/sgl-project/sglang/issues/47213)** — *高。* Qwen3.5：即使启用确定性推理，前缀缓存复用也会改变 logprobs。
5. **[Issue #42012](https://github.com/sgl-project/sglang/issues/42012)** — *在 SM120 上高。* 8× RTX PRO 6000 上的 GLM-5.3-Flash：`fa4` 在 hybrid extend reshape 的 CUDA-graph 捕获时崩溃；Triton 是唯一可用的注意力后端（`v0.5.20` 镜像）。
6. **[Issue #35822](https://github.com/sgl-project/sglang/issues/35822)** — *高。* 在 Ampere 上（2× A2，TP=2，低功耗下 GPU 利用率 100%），使用原生 Qwen3.5/3.8 MTP 的 EAGLE 投机解码在 `tree_speculative_sampling_target_only` 中挂起。
7. **[Issue #47245](https://github.com/sgl-project/sglang/issues/47245)** — *中。* 一个被撤回并重新 prefill 的请求会把 `frequency_penalty`/`presence_penalty`/`repetition_penalty` 累加器和 `min_new_tokens` 重置为零，静默改变输出。
8. **[Issue #47205](https://github.com/sgl-project/sglang/issues/47205)** — *中。* 在 `split_special_tokens` 下，当 think-end 标记被拆分时，推理语法门控始终不打开。
9. **[Issue #47294](https://github.com/sgl-project/sglang/issues/47294)** — *中。* 在 v0.5.22 配合 DSpark 投机解码时，使用 `profile_by_stage=true` 且不带 `num_steps` 的 `/start_profile` 会让每个调度器崩溃（`TypeError: NoneType += int`）。
10. **[Issue #46803](https://github.com/sgl-project/sglang/issues/46803)** — *低 / 延迟尖峰。* 在 pip 安装环境中，FlashInfer `cascade` 会在第一个带前缀的请求内进行 JIT 编译（约 4.5 秒）。
11. **[Issue #47297](https://github.com/sgl-project/sglang/issues/47297)** — Diffusion：LingBot-Video-MoE 在默认 layerwise offload 下于文本编码阶段崩溃（tied vocab table 留在 CPU）。
12. **打包说明 — [Issue #47242](https://github.com/sgl-project/sglang/issues/47242):** 在 Python 3.13 上，安装 SGLang 0.5.22 需要 Rust 工具链，原因是 `outlines==0.1.11` → `outlines_core==0.1.26` 的精确 pin；未记录在文档中。

正在推进的配套修复：**[PR #46373](https://github.com/sgl-project/sglang/pull/46373)**（分离式：仅在正在进行的 forward 之后把 decode 传输目的地发送给 prefill，避免在 active forward 期间释放 KV 页）、**[PR #46262](https://github.com/sgl-project/sglang/pull/46262)**（MLX/Metal `rope_pool_fused` 数组泄漏）、**[PR #47124](https://github.com/sgl-project/sglang/pull/47124)**（在统一 page-envelope 主机池上接收 decode host）、**[PR #47158](https://github.com/sgl-project/sglang/pull/47158)**（follower-rank SIGTERM handler 改为可覆盖）。CI flake 追踪继续在 **[Issue #42752](https://github.com/sgl-project/sglang/issues/42752)**（138 条评论）。

## 6. 这对应用开发者意味着什么
- **在消费级/工作站 Blackwell（SM120）上显式固定后端。** 如果你在 RTX PRO 6000 上服务 GLM-5.3-Flash 或类似模型，请把注意力后端设为 Triton；`fa4` 当前会在 CUDA-graph 捕获期间崩溃。
- **在 DFLASH selector 缺口修复前，将运行时权重更新视为不安全。** RLHF/GRPO 权重同步等工作流（slime、外部草稿模型）可能会用目标模型的权重静默覆盖草稿模型的权重——这种故障表现为接受率下降，而不是报错。
- **确定性保证在边缘场景中仍在退化**：前缀缓存复用改变 logprobs（#47213）、DeepSeek-V4-Flash 上投机解码与 greedy 解码分歧（#45525），以及撤回/重新 prefill 时采样惩罚状态被重置（#47245）。如果你的应用要跨运行或跨副本比较输出，请增加容差，或在这些路径上禁用前缀缓存/投机解码。
- **会话级与 agent 级 KV 编排是发展方向。** [Issue #43098](https://github.com/sgl-project/sglang/issues/43098)（Agentic Cache Scheduling 路线图，7 👍）和 [Issue #45189](https://github.com/sgl-project/sglang/issues/45189)（路由器中的会话感知 KV 缓存编排）表明跨引擎 KV 共享与会话感知路由即将到来——值得围绕稳定的会话 ID 和缓存局部性感知来设计 agent 架构。
- **丰富的可观测性正通过 Rust 前端到来**：每请求调度器统计（[PR #46963](https://github.com/sgl-project/sglang/pull/46963)）、按缓存层级拆分的 cached-token（[PR #46961](https://github.com/sgl-project/sglang/pull/46961)），以及带 request/headers/outcome 的原生 `/generate` 扩展钩子（[PR #47112](https://github.com/sgl-project/sglang/pull/47112)），将使缓存命中和延迟归因精确得多。
- **Python 3.13 用户**：在镜像构建中为 Rust 工具链预留资源，或在 `outlines_core` pin 解决前继续使用 3.12。

</details>

<details>
<summary><strong>llama.cpp</strong> — <a href="https://github.com/ggml-org/llama.cpp">ggml-org/llama.cpp</a></summary>

# llama.cpp 摘要 — 2026-10-30

## 1. 今日亮点

过去 24 小时由后端内核工作主导：Metal 合入了重写的 MXFP4 mat-vec 路径，SYCL 新增了可直接作用于量化 KV 块的 DPAS flash-attention 内核，Hexagon 则增加了 IM2COL 并行化以及新的 UPSCALE 算子。与此同时，FP8/NVFP4 技术栈正在 CUDA、Vulkan 和 ggml 核心中趋于成熟，FP8 KV-cache 支持正在审查中。稳定性方面，HIP 融合 Gated Delta Net 的 bug 会在复用的 server slot 上跨请求泄漏 recurrent state，这是多租户服务当前最严重的未决问题。

## 2. 版本发布与破坏性变更

无公开 API 或配置层面的破坏性变更。值得注意的行为修复：

- **b11972** — `common, mtmd`：control-vector 层索引现在受模型层数约束，M-RoPE 位置循环也受到边界限制。此前会导致越界写入的畸形 tensor 名称 / 位置现会被拒绝。([#31336](https://github.com/ggml-org/llama.cpp/pull/31336)，[tag](https://github.com/ggml-org/llama.cpp/releases/tag/b11972))
- **b11977** — `ggml-openvino`：SCALE 现在能正确处理带步长的视图输入，而不是缩放整个源 tensor。对于此前走错误路径的场景，这会改变模型输出——请重新验证 OpenVINO 数值结果。([#31334](https://github.com/ggml-org/llama.cpp/pull/31334)，[tag](https://github.com/ggml-org/llama.cpp/releases/tag/b11977))
- **b11978** — 仅测试修复：针对 `comp_padding` CUDA graph 预留。([#31344](https://github.com/ggml-org/llama.cpp/pull/31344)，[tag](https://github.com/ggml-org/llama.cpp/releases/tag/b11978))

## 3. 新模型与硬件支持

- **Hexagon：UPSCALE 算子** — 最近邻 2x/4x 和双线性 4x、非连续行、维度折叠，使用 `vgather` 而非标量暂存。使视觉/多模态计算图可在 Hexagon 上运行。([#31331](https://github.com/ggml-org/llama.cpp/pull/31331)，[b11982](https://github.com/ggml-org/llama.cpp/releases/tag/b11982))
- **SYCL：面向量化 KV cache 的 DPAS flash attention** — decode 和小批量（1–31 个 query token）直接在 `q4_0`/`q8_0` KV 块上运行 FA，避免标量反量化或转换。([#31125](https://github.com/ggml-org/llama.cpp/pull/31125)，[b11980](https://github.com/ggml-org/llama.cpp/releases/tag/b11980))
- **OpenCL 量化覆盖** — 初步支持 IQ1_S/IQ1_M（[#31341](https://github.com/ggml-org/llama.cpp/pull/31341)）、IQ3_S/IQ3_XXS（[#31338](https://github.com/ggml-org/llama.cpp/pull/31338)）和 IQ4_XS（[#31339](https://github.com/ggml-org/llama.cpp/pull/31339)），并针对 Adreno 优化。
- **ROCm/HIP：RDNA4_M 系列** — 面向 `gfx1170`/`gfx1171`（128b WMMA，与 RDNA4 不同）。([#31373](https://github.com/ggml-org/llama.cpp/pull/31373))
- **FP8 / NVFP4 技术栈** — CUDA OCP FP8（[#28413](https://github.com/ggml-org/llama.cpp/pull/28413)）、Vulkan FP8 + scaled matmul（[#29791](https://github.com/ggml-org/llama.cpp/pull/29791)）、跨后端的 ggml 级 FP8/NVFP4 量化 scale（[#28898](https://github.com/ggml-org/llama.cpp/pull/28898)），以及支持可选静态 per-tensor scale 的 FP8 KV-cache（[#28392](https://github.com/ggml-org/llama.cpp/pull/28392)）。OCP FP8 E4M3 量化支持已合入（[#27512](https://github.com/ggml-org/llama.cpp/pull/27512)）。
- **LFM3 音频/omni** — 放宽了 LFM3-Audio-2B 和 LFM3-Omni-2B codec 解码器的量化限制（经 QAT 训练，可干净地量化）；mmproj 大小保持不变，仍为 BF16 570.8 MB。([#31386](https://github.com/ggml-org/llama.cpp/pull/31386))。LFM2 shortconv/FFN 块已重构为共享的 LFM 基类以便复用。([#30874](https://github.com/ggml-org/llama.cpp/pull/30874))
- **RPC：event + async 后端 API** 已实现，支持通过 RPC 进行流水线并行。([#18626](https://github.com/ggml-org/llama.cpp/pull/18626))

## 4. 性能与优化

- **Metal MXFP4 mat-vec** — 使用 fp16 bit-trick 解码替代 threadgroup 查找表；打包的 nibble 按对齐的 32-bit word 加载；unary/binary/GLU 使用完整 threadgroup。([#31075](https://github.com/ggml-org/llama.cpp/pull/31075)，[b11985](https://github.com/ggml-org/llama.cpp/releases/tag/b11985))
- **Hexagon 转置 CONCAT** — 行块大小翻倍并采用 scratchpad 双缓冲，对 `src1` 行分块，使用 VTCM stride padding 分散 gather lane；目标是提升 DDR 带宽利用率。([#31277](https://github.com/ggml-org/llama.cpp/pull/31277)，[b11981](https://github.com/ggml-org/llama.cpp/releases/tag/b11981))
- **Hexagon IM2COL** — 基于块的 HVX 跨线程并行化，修复 padding 处理，展开常见情况。([#31050](https://github.com/ggml-org/llama.cpp/pull/31050)，[b11976](https://github.com/ggml-org/llama.cpp/releases/tag/b11976))
- **SYCL 重排布局的反量化存储** — 对 Q4_0、K-quants、IQ3、MXFP4 使用加宽 store，替代此前相隔 16 个元素步长的逐字节标量写入。([#30976](https://github.com/ggml-org/llama.cpp/pull/30976)，[b11979](https://github.com/ggml-org/llama.cpp/releases/tag/b11979))
- **Gemma 4 prompt-processing 计算图优化** — 对不贡献 KV cache 的层跳过计算；据报告，E2B/E4B 的 PP 获得“巨大收益”。([#31356](https://github.com/ggml-org/llama.cpp/pull/31356)，相关 [#29189](https://github.com/ggml-org/llama.cpp/pull/29189))
- **KV-cache：旋转常量常驻 GPU** — Hadamard 静态矩阵保留在设备端，避免每步往返主机；在 PCIe 受限的多 GPU 配置上有明显意义。([#31073](https://github.com/ggml-org/llama.cpp/pull/31073))
- **SYCL CONV_TRANSPOSE_1D** — 在 Arc Pro B70 上限制输入迭代范围。([#31109](https://github.com/ggml-org/llama.cpp/pull/31109))

## 5. 稳定性与回归

按严重程度排序：

1. **跨请求状态污染（对多租户尤其严重）** — HIP/ROCm 融合 Gated Delta Net 在复用的 server slot 上会跨请求携带 recurrent state（qwen35/qwen35moe）；较早 prompt 的文本会在后续补全中原样输出。未引用修复 PR。([#29092](https://github.com/ggml-org/llama.cpp/issues/29092))
2. **安全：通过 `?q=` 查询参数对 WebUI 进行指令注入。** ([#25790](https://github.com/ggml-org/llama.cpp/issues/25790))。相关：`json_schema` 中无界 `enum` 会导致语法构造呈超线性，每个小请求即可占满一个核心数十秒（DoS）。([#29457](https://github.com/ggml-org/llama.cpp/issues/29457))。GBNF 嵌套重复导致的栈溢出问题已关闭。([#18988](https://github.com/ggml-org/llama.cpp/issues/18988))
3. **语法失败返回 HTTP 500** — LFM3 会以 “Unexpected empty grammar stack after accepting piece: 6 (30)” 拒绝任何 `response_format`。([#31328](https://github.com/ggml-org/llama.cpp/issues/31328))。`json-schema-to-grammar` 会将原始控制字符（例如来自 `\u0000` 的 NUL）原样复制到 GBNF 模式中 → “failed to parse grammar”。([#31199](https://github.com/ggml-org/llama.cpp/issues/31199))
4. **崩溃 / 初始化失败** — `--split-mode tensor` 在第二个请求时触发 `GGML_ASSERT(bcj.nodes[i])` 断言（2x/3x Tesla P100，CUDA）。([#29466](https://github.com/ggml-org/llama.cpp/issues/29466))。SYCL bf 转换指令在 Arrow Lake iGPU 上不受支持。([#31029](https://github.com/ggml-org/llama.cpp/issues/31029))。Jetson Orin NX 在 b8638→b9016 的 server 重写后，于开始服务前挂起。([#29499](https://github.com/ggml-org/llama.cpp/issues/29499))。macOS 14 / M2 Ultra 上因 `unary.metal` 中 `constexpr` bfloat 转换导致的 Metal 初始化失败已关闭。([#31272](https://github.com/ggml-org/llama.cpp/issues/31272))
5. **性能回归** — 在使用 CPU offload 的 MoE experts（`-ncmoe`）时，SYCL `llama-server` 的 prompt processing 在 b11804 相比 b11046 慢约 35%，`llama-bench` 未复现（即属于 server 路径特有问题）。([#31262](https://github.com/ggml-org/llama.cpp/issues/31262))。SYCL XMX-ESIMD 路径在 Arc Pro B70 的 MoE PP 上慢约 28–35%（回归来自 `d81d0d8fb`）。([#31068](https://github.com/ggml-org/llama.cpp/issues/31068))。Vulkan 深上下文 decode 在 Arc Pro B70 上从 1k→64k token 时性能骤降约 8 倍（SYCL 仅下降约 2.4 倍）。([#28721](https://github.com/ggml-org/llama.cpp/issues/28721))。有报告称投机解码性能下降。([#31220](https://github.com/ggml-org/llama.cpp/issues/31220))
6. **正确性** — 混合 LFM2 co-batching 会破坏 recurrent/short-conv 状态；greedy 输出发生偏离，并可能在句子中途停止。([#29002](https://github.com/ggml-org/llama.cpp/issues/29002))。SYCL CPY 到 `q4_1`/`q5_1`/`q8_0` 的结果与 CPU 参考不一致。([#31140](https://github.com/ggml-org/llama.cpp/issues/31140))
7. **投机解码 / 多模态** — mtmd 图像块会在 draft KV cache 中留下位置空洞，导致约 500 秒停顿，随后在使用 `--spec-type draft-dflash` 时返回 HTTP 500。([#27408](https://github.com/ggml-org/llama.cpp/issues/27408))。`draft-mtp` 上下文按 `llama_n_ctx()` 而非 `llama_n_ctx_seq()` 设定大小，在较大的 `--ctx-size` 下会使 server 崩溃。([#28433](https://github.com/ggml-org/llama.cpp/issues/28433))。MiMo-V2.6 sidecar MTP draft 因 `blk.0.attn_q not found` 失败。([#29345](https://github.com/ggml-org/llama.cpp/issues/29345))
8. **缓存效率** — 对于 Qwen3.5+ 聊天模板，reasoning/content 中的空白无法往返保真 → 导致前缀缓存失效，并在混合模型上完整重新 prefill。([#30357](https://github.com/ggml-org/llama.cpp/issues/30357))

## 6. 这对应用开发者意味着什么

- **在 ROCm 上进行多租户服务：固定或隔离。** Gated Delta Net 的状态泄漏（#29092）意味着复用的 slot 可能输出另一位用户的 prompt 文本。在修复前，对于混合/循环模型，应避免在 HIP 上激进复用 slot，或每个会话运行一个 slot。
- **将 grammar/schema 处理视为不可信输入面。** 三个独立问题（向 GBNF 注入控制字符、大 `enum` 的超线性构造、LFM3 空 grammar 栈）可让单个请求产生 500 或占满一个核心。应在网关处校验/规范化 `response_format` payload，并限制 `enum` 大小。
- **后端版本固定仍比头条基准成绩更重要。** SYCL 有两个独立的约 30% MoE prefill 回归（#31262、#31068），以及一个 Vulkan 长上下文 decode 性能骤降（#28721）；`llama-bench` 无法复现 server 路径的回归，因此请对你实际部署的 `llama-server` 配置做基准测试。
- **量化 KV 推理正在走向实用。** SYCL 在 `q4_0`/`q8_0` KV 上的 DPAS FA，加上正在审查的 FP8 KV-cache（#28392），将显著降低长上下文 agent 的 KV 内存——现在值得做原型验证，但要做好不同后端数值差异的准备（见 #31140）。
- **投机解码仍是 agent 工作负载中最棘手的环节**：图像输入上的 draft-KV 位置空洞（#27408）和 MTP 上下文大小设定（#28433）都会表现为硬性 500，而非优雅降级。请保留非投机解码的回退路径。
- **Gemma 4 的 prompt-processing 优化收益正在落地**（#31356），并且 **FP8/NVFP4 支持正在 CUDA/Vulkan/ggml 上扩大**——请围绕 FP8 E4M3 和 NVFP4 规划量化流水线，而不是只假设 Q4/Q8。

</details>

<details>
<summary><strong>Ollama</strong> — <a href="https://github.com/ollama/ollama">ollama/ollama</a></summary>

# Ollama 摘要 — 2026-10-30

## 1. 今日亮点
Ollama 发布了 **v0.40.13**，将 Liquid AI 的 **LFM3** 系列（包括 `lfm3-audio` TTS 和 `lfm3-omni`）从 Apple silicon 扩展到 **Linux 和 Windows**。问题跟踪器上占主导的是面向 agent 的正确性问题，而不是吞吐优化工作：`qwen3.8` 上的 MLX 工具调用回归、ROCm iGPU 上的 KV 状态串扰，以及围绕 reasoning/content 数组的多个 OpenAI 兼容性缺口——其中两个已有修复 PR 打开。与此同时，MLX runner 正在获得 Windows/CPU 后端支持，以及面向大词表的开销显著更低的 top-k 路径。

## 2. 发布与破坏性变更
- **v0.40.13** — LFM3（`lfm3`、`lfm3-audio`、`lfm3-omni`）现在除 Apple silicon 外，也可在 Linux 和 Windows 上运行。此前该模型需要 MLX 运行时，这一要求未文档化，并导致 Linux 上的 pull/run 失败（[#19369](https://github.com/ollama/ollama/issues/19369)，已关闭）。如果你曾将 LFM3 的发布范围限制在 macOS，现在可以解除该限制——但请在非 Apple 主机上重新验证音频路径。
- **今日未宣布 API/配置破坏性变更。** 运维提示：在就地“update”之后，仍没有受支持的方式将模型回滚到先前的 digest（[#19385](https://github.com/ollama/ollama/issues/19385)，已关闭但未提供机制）。请在生产 manifest 中显式固定 digest。

## 3. 新模型与硬件支持
- **Linux + Windows 上的 LFM3 / lfm3-audio / lfm3-omni** — [release v0.40.13](https://github.com/ollama/ollama/releases)。
- **Windows + CPU 后端上的 MLX runner** — [PR #19366](https://github.com/ollama/ollama/pull/19366) 新增原生 Windows 执行以及 Metal/CUDA 之外的 CPU 后端，并在这些路径上启用完整 TTS 推理（例如 `phonon:en`）。处于打开状态，尚未合并。
- **MXFP4 大型 MoE 加载损坏**：`gpt-oss:120b` 在 0.40.12 上因 `unsupported tensor "blk.0.ffn_down_exps.weight" size overflows` 而 GGUF 元数据解析失败（[#19375](https://github.com/ollama/ollama/issues/19375)）；0.40.1 上也报告了同类失败（[#18869](https://github.com/ollama/ollama/issues/18869)，已关闭）。在溢出修复落地前，应将 120B MXFP4 视为不可用。
- **三值量化（Bonsai 2）** — 相关请求已关闭，未提供支持（[#19388](https://github.com/ollama/ollama/issues/19388)）。

## 4. 性能与优化
- **长行上的 MLX top-k** — [PR #19392](https://github.com/ollama/ollama/pull/19392)：MLX 的 `argpartition` 会对整行排序，而在 Metal 上，超过 2048 个值的一行会触发多趟归并排序，这在 **248K token 词表**上主导了 top-k 开销。该补丁单趟排序每个 2048 值分块，然后再合并。这直接关系到大词表 MLX 模型的采样延迟。
- **MLX 上的投机解码基准测试** — [PR #19391](https://github.com/ollama/ollama/pull/19391) 新增 `draft_num_predict=0`，用于按请求禁用 drafting（系统默认仍为 4）。这样无需更改服务器配置即可对 spec-decode 加速做 A/B；draft 缓存会保持同步，因此后续 drafting 请求不受影响。
- **调度器 VRAM 驱逐正确性** — [PR #19284](https://github.com/ollama/ollama/pull/19284)：在多 GPU 主机上，预加载 VRAM 预测可能超过报告的空闲内存，并驱逐一个仅按空闲时间选出的 runner——包括内存并无帮助的**仅 CPU runner**。可防止误驱逐和重载抖动。
- **gpt-oss 不再强制启用 flash attention** — [PR #17477](https://github.com/ollama/ollama/pull/17477) 对默认使用 flash attention 的架构显式请求 flash attention；该回归导致部分卸载下 **GPT-OSS Q8 在长上下文时崩溃**（[#17430](https://github.com/ollama/ollama/issues/17430)）。仍处于打开状态。

## 5. 稳定性与回归（按严重程度排序）
1. **跨请求 KV 缓存污染（严重，正确性）** — Strix Halo `gfx1151` iGPU 上的 ROCm（`0.32.14-rocm`）：响应会被*上一个*请求的内容污染（[#17847](https://github.com/ollama/ollama/issues/17847)，自 8 月起打开，11 条评论）。尚无修复 PR。请勿在此后端上承载不受信任/多租户流量。
2. **MLX 工具调用静默失效（高）** — 当 assistant 先产生自由文本 content 时，`qwen3.8:27b-mlx` 从不发出 `tool_calls`；仅在 `content` 为空时有效（[#19353](https://github.com/ollama/ollama/issues/19353)）。这破坏了标准的“先宣告再行动”agent 模式。
3. **go_template 丢弃整个 assistant 轮次（高）** — 带 `tools` 的 `/api/chat` 返回空 content、`tool_calls: null`、`eval_count > 0`；llama.cpp 能正确解析同一生成结果（[#19377](https://github.com/ollama/ollama/issues/19377)，已关闭）。
4. **OpenAI 兼容性：reasoning 被丢弃 / 仅含 reasoning 的轮次被删除**——当 `content` 是 content-parts 数组时（[#19380](https://github.com/ollama/ollama/issues/19380)）——修复已打开：[PR #19384](https://github.com/ollama/ollama/pull/19384)。
5. **`/v1/models` 在零模型时返回 `"data": null`**，破坏强类型 SDK（[#19381](https://github.com/ollama/ollama/issues/19381)）；针对空 embedding 数组的相关修复：[PR #19387](https://github.com/ollama/ollama/pull/19387)。
6. **间歇性 CUDA 预热失败并静默回退到 CPU（中）** — 在 Windows + RTX 5070 Ti 上使用 `gpt-oss:20b` 时出现 `shared object initialization failed`，会回退到 `CUDA_Host`→CPU pinned buffers，而不暴露该降级（[#17380](https://github.com/ollama/ollama/issues/17380)）。
7. **`OLLAMA_NUM_PARALLEL=1` 似乎未被执行（中）** — 尽管设置了该值，仍观察到两个并发会话（[#19262](https://github.com/ollama/ollama/issues/19262)）；如果你依赖串行化来控制内存边界，这一点值得关注。
8. **原生 API 中的静默字段丢弃（低–中）** — `/api/chat` 会忽略 `audio`，即使模型声明了 `audio` 能力；音频只能通过 `images` 工作（[#19378](https://github.com/ollama/ollama/issues/19378)）。与 `tool_calls` 一起出现的无效 content 类型会被静默强制转换，而不是返回 400（[PR #19389](https://github.com/ollama/ollama/pull/19389)，打开）。
9. **macOS 27 应用外壳损坏（低，仅客户端）** — 窗口和菜单栏图标从不出现（`com.electron.ollama` bundle 查找）；服务器和 CLI 正常（[#19370](https://github.com/ollama/ollama/issues/19370)，已关闭）。
10. **聊天截断可能丢弃最新的用户消息**——在多步工具循环中，导致 `500: no user query found`（[PR #18697](https://github.com/ollama/ollama/pull/18697)，打开）。

## 6. 这对应用开发者意味着什么
- **固定模型 digest。** 由于 `ollama pull` 更新 tag 后没有回滚路径，一次模型更新对你的评估基线而言就是一扇单向门。请把 digest 变更当作部署来处理。
- **暂时不要依赖 `reasoning` 经 `/v1` 往返。** 如果你以 content-parts 数组重放 assistant 轮次（LangChain、LiteLLM、OpenAI SDK 封装器），reasoning 会被丢弃，仅含 reasoning 的轮次会被删除。请等到 [PR #19384](https://github.com/ollama/ollama/pull/19384) 合并，或规整为字符串 content。
- **加固 OpenAI 兼容响应解析。** 对列表字段（`/v1/models` 的 `data`、embeddings 的 `data`）接受 `null`，而不是假定为 `[]`。
- **避免将 MLX `qwen3.8` 用于使用工具的 agent**，直到 #19353 解决；该失败是静默的（没有工具调用，也没有错误），会让你的 agent 陷入循环。
- **音频尚未成为原生 API 的一等接口。** 目前请通过 `images` 字段传递音频；`/api/chat` 没有文档化的 `audio` 参数。
- **按请求对投机解码做基准测试**，一旦 `draft_num_predict=0` 落地——有助于在 MLX 上无需重启服务器进行 A/B。
- **容量规划：** 同时关注 #19284 和 #19262；二者都会影响你声明的并发度和内存预算是否真正被执行。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 摘要 — 2026-10-30

来源：[github.com/BerriAI/litellm](https://github.com/BerriAI/litellm)

## 1. 今日亮点

LiteLLM 发布了新的候选版本（`v1.108.0-rc.1`），同时发布了稳定补丁 `v1.106.6` 和 `v1.105.7`，三者均延续 cosign 签名的 Docker 镜像策略。正在进行中的两项影响最大的变更是 Anthropic 转换中的破坏性行为修复——Claude **服务端**工具此前被作为客户端 `tool_calls` 返回，导致 OpenAI Agents SDK 和 LangGraph 无法正常工作（[#48385](https://github.com/BerriAI/litellm/pull/48385））——以及一项护栏修正：Lakera v2 的 `on_flagged: block` 此前会静默放行仅含 PII 的检测（[#48944](https://github.com/BerriAI/litellm/pull/48944））。花费核算问题占据了 issue 跟踪器的主要位置：通过 OpenAI 兼容上游的流式和非流式流量在多个已报告路径中仍以 `$0` 记录到 `LiteLLM_SpendLogs`，这直接削弱了预算执行。

## 2. 发布与破坏性变更

- **`v1.108.0-rc.1`** — 候选发布版本。Docker 镜像使用 cosign 签名；验证密钥在提交 [`e82a3c6`](https://github.com/BerriAI/litellm/commit/e82a3c646908ba0a6ee0beddc4310d7a6cac4065) 中引入。→ [发布](https://github.com/BerriAI/litellm/releases/tag/v1.108.0-rc.1)
- **`v1.106.6`** — 1.106 系列上的稳定补丁，使用相同签名密钥。→ [发布](https://github.com/BerriAI/litellm/releases/tag/v1.106.6)
- **`v1.105.7`** — 1.105 系列上的稳定补丁，使用相同签名密钥。→ [发布](https://github.com/BerriAI/litellm/releases/tag/v1.105.7)

注意：这三个版本已发布的 release 正文均只包含镜像签名验证的样板内容——没有包含变更日志或迁移说明，因此这些标签的 diff 范围在源头上没有文档记录。

**未合并 PR 中的破坏性行为变更**（作者标记为 `!`）：
- `fix(anthropic)!` — chat completions 将**仅**在 `tool_calls` 中列出**客户端工具**；Claude 服务端工具（web search、web fetch、tool search、code execution）不再作为客户端可执行的工具调用暴露。任何根据 `tool_calls` 进行分支以路由服务端工具的 Agent 都将出现行为变化。→ [#48385](https://github.com/BerriAI/litellm/pull/48385)
- `fix(guardrails)!` — 使用 `on_flagged: block` 的 Lakera v2 现在会阻断**每一次**检测，包括仅含 PII 的检测。先前的“屏蔽并放行”行为现在通过新的 `on_flagged: mask` 模式保留。使用默认配置的用户将开始看到此前未出现的 400。→ [#48944](https://github.com/BerriAI/litellm/pull/48944)
- `feat(realtime)!` — OpenAI/Azure 上新增翻译路由和流式转录，按音频秒数计费。→ [#35600](https://github.com/BerriAI/litellm/pull/35600)
- `feat(dashscope)` — 图像编辑计费语义对**所有**提供商发生变化：`/v1/images/edits` 现在按部署自身的图像价格计费。→ [#48998](https://github.com/BerriAI/litellm/pull/48998)

## 3. 新模型与硬件支持

- **DashScope 图像编辑 + TTS** — DashScope 模型现在支持 `/v1/images/edits`（此前返回 500）和 `/v1/audio/speech`（此前返回 404）。→ [#48998](https://github.com/BerriAI/litellm/pull/48998)
- **OpenAI 实时翻译与流式 `gpt-transcribe`** — 在 OpenAI 和 Azure 上，通过 WebSocket 翻译会话按发送的音频秒数计费。→ [#35600](https://github.com/BerriAI/litellm/pull/35600)
- **Azure AI Foundry Agents v2** — 使用 `agent_reference`（按名称 + 版本寻址 Agent）的 Responses API，替代已弃用的 Assistants 原语。Issue 已关闭。→ [#25372](https://github.com/BerriAI/litellm/issues/25372)
- **`nokeep`** — 零数据保留的 OpenAI 兼容提供商；仅包含三个模型的花费/限制/能力条目（没有提供商特定的 Python 代码路径）。→ [#49111](https://github.com/BerriAI/litellm/pull/49111)
- **CLF AI Gateway** — 面向开放权重模型的 OpenAI 兼容网关，已将十个模型添加到成本映射。→ [#39324](https://github.com/BerriAI/litellm/pull/39324)
- **Soniox 实时流式 STT（`stt-rt-v5`）** — 通过代理进行 WebSocket 转录的功能请求仍处于开放状态；尚未支持。→ [#43677](https://github.com/BerriAI/litellm/issues/43677)

## 4. 性能与优化

- **least-busy 路由突发流量塌缩** — 并发请求都读取相同的在途计数器，因此突发流量会全部涌向第一个部署，而其他部署处于空闲。修复在选取时预留被选中的部署，以便下一个请求将其视为繁忙（对于始终未到达的请求，预留会过期）。→ [#47484](https://github.com/BerriAI/litellm/pull/47484)
- **OpenAI/Azure 的 PDF token 计价已修正** — 一页 *文本* PDF 此前在 Azure GPT 部署上按 1664 token 的 Claude 页面图像计价，而实际只计 141 token；预算检查拒绝了本应可用的请求。还覆盖位于另一网关前缀之后的 GPT 部署。→ [#47554](https://github.com/BerriAI/litellm/pull/47554)
- **Responses API 图像的 TPM 预留重复计数** — 嵌套在 `custom_tool_call_output.output[]` 下的 base64 图像负载使用 `str(item)` 序列化并被当作文本计数，导致在 Proxy 1.101.0 上预留估算翻倍。已关闭。→ [#47814](https://github.com/BerriAI/litellm/issues/47814)
- **事件循环客户端缓存以 `id(loop)` 为键** — CPython 在回收后会复用事件循环地址，导致缓存的异步客户端被交给错误的事件循环并提前关闭。现在改为按每个事件循环的 token 作为键；同步客户端跨事件循环只缓存一次。→ [#48877](https://github.com/BerriAI/litellm/pull/48877)
- **启动延迟 / 气隙环境** — 自 `v1.92.0` 起，代理会在启动时下载 Prisma 二进制文件，并在无外网出口时失败。仍未关闭。→ [#33167](https://github.com/BerriAI/litellm/issues/33167)

## 5. 稳定性与回归

按对代理运维人员的严重程度排序：

1. **流式花费日志为 `$0`** — 当上游报告 `usage.cost: 0` 时，通过 OpenAI 兼容上游的流式 `/v1/chat/completions` 会记录为 `spend = 0` 和 `cost_breakdown.input_cost = 0.0`；所有此类流式流量的花费和预算都读为零。未关闭。→ [#48937](https://github.com/BerriAI/litellm/issues/48937)
2. **非流式 `usage.cost` 被忽略** — `custom_llm_provider: openai` 上游存在同类 bug，非流式调用中 `response_cost = 0`。已关闭。→ [#47533](https://github.com/BerriAI/litellm/issues/47533)
3. **未校验 `usage.cost` 导致的幻影花费** — 提供商报告的成本被逐字信任为 USD，未做单位检查；一个非美元值产生了天文数字的花费。已关闭。→ [#35829](https://github.com/BerriAI/litellm/issues/35829)
4. **Claude 服务端工具被暴露为客户端 `tool_calls`** — OpenAI Agents SDK 会因不拥有的工具而失败；LangGraph Agent 会运行一个存根并报告搜索失败。修复 PR 仍开放。→ [#48385](https://github.com/BerriAI/litellm/pull/48385)
5. **Claude 工具调用在 OpenRouter/Vertex 后端上损坏** — 长期存在的未关闭报告，6 条评论，未关联修复 PR。→ [#19858](https://github.com/BerriAI/litellm/issues/19858)
6. **`print_verbose` 将 API 密钥泄漏到 stdout** — 当 `set_verbose=True` 时，verbose 辅助函数会原样打印字典形式的诊断信息，其中包括 `api_key`，没有脱敏或控制字符清理。未关闭，标记为安全。→ [#34705](https://github.com/BerriAI/litellm/issues/34705)
7. **Presidio `logging_only` 在失败调用中未屏蔽提示词** — 屏蔽只在成功时运行，因此失败的请求会将原始姓名和邮箱发送到 Langfuse 以及所有其他日志记录器。修复 PR 仍开放。→ [#49057](https://github.com/BerriAI/litellm/pull/49057)
8. **Lakera v2 `on_flagged: block` 让 PII 通过** — 在默认配置下，被标记的卡号从未产生 400。修复已关闭/合并。→ [#48944](https://github.com/BerriAI/litellm/pull/48944)
9. **团队密钥花费污染用户预算** — 未设置 `apply_user_budget_to_team_keys` 时，团队密钥用量免于用户预算*检查*，但仍通过 Redis/内存计数器、缓存和数据库行计入用户预算*计量*。修复 PR 仍开放。→ [#49110](https://github.com/BerriAI/litellm/pull/49110)
10. **内存中的花费缓冲区在关闭时丢失** — `update_spend` 和 `update_daily_tag_spend` 是由 APScheduler 驱动的内存缓冲区，在代理停止时被静默丢失。未关闭。→ [#34805](https://github.com/BerriAI/litellm/issues/34805)
11. **没有 Redis 时 `provider_budget_config` 从不重置** — `budget_reset_at` 报告为约 57 年之后，因此每月提供商预算实际上从不重置。未关闭。→ [#37261](https://github.com/BerriAI/litellm/issues/37261)
12. **终端用户的 `model_max_budget` 未被执行** — 通过 `/budget/new` 为客户端设置的单模型预算未被遵守。已关闭。→ [#31842](https://github.com/BerriAI/litellm/issues/31842)
13. **`/cursor/chat/completions` 未记录日志** — 返回 200 且提供商被收费，但没有创建 SpendLogs/Logs UI 条目（1.88.1）。未关闭。→ [#30126](https://github.com/BerriAI/litellm/issues/30126)
14. **凭证编辑覆盖真实密钥** — `/credentials` 返回脱敏后的 `credential_values`，仪表盘弹窗会预填这些值，因此保存时用占位符替换了实时密钥。已关闭。→ [#28906](https://github.com/BerriAI/litellm/issues/28906)
15. **`litellm.responses()` 丢失代理错误响应体** — 被拒绝的请求（例如护栏阻断）抛出 `BadRequestError` 时，`e.body`、`e.code`、`e.type` 全为 `None`，与 `litellm.completion()` 不同。修复 PR 仍开放。→ [#49073](https://github.com/BerriAI/litellm/pull/49073)
16. **代理 `--num_workers > 1` 子进程死亡** — 从 1.78.0 升级到 1.80.8 时启动失败，通过降到一个 worker 规避。已关闭。→ [#18457](https://github.com/BerriAI/litellm/issues/18457)
17. **Claude 空内容清理泄漏** — `[System: Empty message content sanitised to satisfy protocol]` 被作为模型输出返回。已关闭，12 条评论（该时间窗口内流量最高的 issue）。→ [#24498](https://github.com/BerriAI/litellm/issues/24498)
18. **Bedrock 音频转录 HTTP 400** — 系统消息与 `/v1/audio/transcriptions` 上的音频块不兼容。已关闭。→ [#41544](https://github.com/BerriAI/litellm/issues/41544)

另外已合入：同步响应成本现在会在发送响应头之前只最终确定一次，因此响应头、花费记录和预算计数器保持一致；已完成的提供商用量在经过失败的后置调用钩子和取消后仍会保留（[#48993](https://github.com/BerriAI/litellm/pull/48993)）；`drop_params` 现在会发出 WARNING，指明参数、值、模型和原因，而不是静默丢弃所请求的推理级别（[#48933](https://github.com/BerriAI/litellm/pull/48933)）。

## 6. 这对应用开发者意味着什么

- **暂时不要信任 OpenAI 兼容上游的代理侧预算。** 如果你的上游返回 `usage.cost`，流式流量会被记录为 `$0`（[#48937](https://github.com/BerriAI/litellm/issues/48937)），而非流式流量直到最近也是如此（[#47533](https://github.com/BerriAI/litellm/issues/47533)）。在这些问题修复之前，请在下游或提供商侧配额上强制执行花费限制。
- **在升级到包含 Anthropic 修复的版本之前，审计 Agent 集成。** 服务端工具不再作为客户端 `tool_calls` 出现（[#48385](https://github.com/BerriAI/litellm/pull/48385)）。如果你将 OpenAI Agents SDK 或 LangGraph 与 Claude web search/fetch/code-execution 一起使用，请验证你的工具分发分支——故障模式是 SDK 中硬错误，以及 LangGraph 中静默错误的存根。
- **重新检查护栏配置。** Lakera v2 默认配置（`on_flagged: block`）此前在仅含 PII 的检测上会失效放行；修复后改为失效阻断。如果这破坏了某个工作流，请显式选择新的 `mask` 模式，而不是依赖旧的隐式行为（[#48944](https://github.com/BerriAI/litellm/pull/48944)）。
- **Token 计数漂移可能拒绝有效请求。** OpenAI/Azure 部署上的 PDF 输入此前被高估约 12 倍（1664 对 141 token）（[#47554](https://github.com/BerriAI/litellm/pull/47554)），而 Responses API 工具输出中的 base64 图像可能使 TPM 预留翻倍（[#47814](https://github.com/BerriAI/litellm/issues/47814)）。如果你在文档或图像工作负载上看到无法解释的 429，这很可能是原因。
- **除非显式设置 `apply_user_budget_to_team_keys`，否则团队密钥核算会向用户预算多计。**（[#49110](https://github.com/BerriAI/litellm/pull/49110)）。值得在 `general_settings` 中显式设置，而不是依赖默认值。
- **气隙和多 worker 部署仍是棘手问题。** 启动时下载 Prisma 二进制文件（[#33167](https://github.com/BerriAI/litellm/issues/33167)）以及 `--num_workers > 1` 启动失败（[#18457](https://github.com/BerriAI/litellm/issues/18457)）都在 issue 跟踪器中反复出现；请在预发布环境中测试这些问题，而不是在生产环境。
- **版本建议：** `v1.108.0-rc.1` 是候选版本，没有已发布的变更日志——应视为预发布版本。`v1.106.6` 和 `v1.105.7` 是当前稳定补丁版本选择；两者发布相同的 cosign 签名镜像，因此固定到提交 `e82a3c6` 的签名验证在三个版本上仍然有效。

---

</details>

<details>
<summary><strong>Unsloth</strong> — <a href="https://github.com/unslothai/unsloth">unslothai/unsloth</a></summary>

# Unsloth 摘要 — 2026-10-30

## 今日亮点
过去 24 小时内没有带标签的版本发布，但 Studio/Desktop 经历了密集的合并与修复日：T4 NF4 解码路径针对 batch‑4 重新调优（`gemm_4bit` 上提升 13–30%），批量 MoE LoRA 训练被重构为单次分组 GEMM pass（[#16012](https://github.com/unslothai/unsloth/pull/16012)），多个高影响 Studio 正确性 bug 获得了修复 PR（上下文压缩、MLX 内存估算、`/v1/models` 发现）。两起围绕 Alpaca/仅 completion 掩码的静默训练数据丢失报告（[#15894](https://github.com/unslothai/unsloth/issues/15894)/[#15895](https://github.com/unslothai/unsloth/issues/15895)）是当前最严重的未决事项，且尚无关联修复。

## 发布与破坏性变更
无。过去 24 小时内没有新版本，也没有宣布 API/配置迁移。当前实际使用的 beta 版本线为 `v0.1.912-beta`（多个 issue 报告中有引用）。

## 新模型与硬件支持
- **LFM3 系列（1.7B）** —— 功能请求已开启，已有 10 个 👍；LiquidAI 的新骨干网络尚未获得支持（[#15588](https://github.com/unslothai/unsloth/issues/15588)）。LFM3 的 **MLX** 检查点目前无法出现在 `GET /v1/models` 中，也无法自动切换（[#15832](https://github.com/unslothai/unsloth/issues/15832)）——修复 PR [#15945](https://github.com/unslothai/unsloth/pull/15945) 通过本地模型解析器的 `auto_map` 门控解决了该问题。
- **MLX 上的 LFM3‑Audio / LFM3‑Omni** —— 已合入 #15889；随后在 [#16023](https://github.com/unslothai/unsloth/pull/16023) 中对音频输入 heal gate 进行修复（修复 main 上的红色 CI）。
- **Apple MLX Neural Engine prefill** —— 新增可选开关，将 dense SwiGLU MLP prefill 在 ANE 与 GPU 之间拆分，与现有 Int8 Prefill 开关类似（[#15954](https://github.com/unslothai/unsloth/pull/15954)）。
- **多 GPU 音频模型加载** —— 自动原生音频加载现在固定到单个 GPU，而不是拒绝池化设备选择（[#16022](https://github.com/unslothai/unsloth/pull/16022)）。
- **AMD iGPU 处理** —— 集成 Radeon（共享系统内存）已从 Train 页面 VRAM 总量和默认 GPU 选择中排除；这解除了此前双 R9700 配置中真实 VRAM 为 64 GiB 却显示 `VRAM 100 GiB` 的阻塞（[#14039](https://github.com/unslothai/unsloth/pull/14039)）。
- **Vulkan 后端** —— MiniCPM‑V‑4.7‑1B 文本生成失败问题已关闭（[#14987](https://github.com/unslothai/unsloth/issues/14987)）。
- **Apple Silicon 上的 NVFP4** —— 当全部 61/61 层均卸载时，MiniMax‑M3.1 GGUF 不再回退到 CPU（已关闭）（[#15409](https://github.com/unslothai/unsloth/issues/15409)）。

## 性能与优化
- **T4 NF4 解码切换点从 batch 5 → batch 4** —— batch 2–4 现在交给 bitsandbytes 的融合 `gemm_4bit`，而不是 Triton GEMV‑rows 内核；在 Colab T4 上实测 **batch 4 时快 13–30%**（[#15988](https://github.com/unslothai/unsloth/pull/15988)，已关闭/已合并）。
- **批量 MoE LoRA 训练** —— 每个 adapter 的 expert LoRA 现在在一次分组 GEMM pass 中运行，而不是为每个 adapter 重新运行融合 experts（Qwen3 MoE、Qwen3.5/3.6‑MoE，包括 Qwen3.6‑35B‑A3B）——直接面向 Studio 中排队的多任务训练（[#16012](https://github.com/unslothai/unsloth/pull/16012)）。
- **视频导出卡顿** —— `StreamEncode._matches` 过去会分配块大小的临时对象；在 A100‑40 上导出 MiniMax‑H3 1344×768×124 片段从 **115–184 秒降至约 1–2 秒**（[#16024](https://github.com/unslothai/unsloth/pull/16024)）。
- **MLX 内存估算** —— 当 mlx 回退到未融合的全宽（f16）注意力时，估算现在会计入完整的 `[heads, ctx]` 分数矩阵，而不是仅在 KV cache 量化时才计入（[#16021](https://github.com/unslothai/unsloth/pull/16021)）。预计估算值会*上升*；见下方回归说明。
- **上下文压缩超时缩放** —— token 计数超时现在会随 payload 缩放，因此数百万 token 的 GGUF 记录仍可压缩（[#15900](https://github.com/unslothai/unsloth/pull/15900)），另外在 `/apply-template` 上增加了字节数保护，避免超大 payload 引发 503/500 风暴（[#15857](https://github.com/unslothai/unsloth/pull/15857)）。

## 稳定性与回归
按严重程度排序：

1. **Alpaca / 仅 completion 掩码上的静默训练数据丢失（尚无修复 PR）。** 在*任意* instruct 模型上，“Train on completions”会丢弃 Alpaca 数据集的 **80%+**：Alpaca 模板从未安装，但掩码仍会搜索其标记。已在两个不相关的模型系列上复现；Windows 11、RTX 5060 8 GiB、`v0.1.911-beta`。注意该报告存在两份——[#15894](https://github.com/unslothai/unsloth/issues/15894)（已关闭）和 [#15895](https://github.com/unslothai/unsloth/issues/15895)（仍开启）。值得核实关闭是去重还是真正修复。
2. **单列数据集不可用。** 只有一列 `text` 的 JSONL 会报告 `Format: unknown`，AI Assist 拒绝处理，Start 静默返回预览——即 Unsloth 自家 notebook 中的标准 SFT 形状（[#15892](https://github.com/unslothai/unsloth/issues/15892)，已关闭）以及单列 `content`（[#15901](https://github.com/unslothai/unsloth/issues/15901)，已关闭）。AI Assist 现在会解释*为何*无法映射无 prompt/response 的数据集（[#15991](https://github.com/unslothai/unsloth/pull/15991)）。
3. **Windows + AMD GGUF 内存暴涨。** 加载 GGUF 后，即使选择“Don't reserve system RAM”，`llama-server` 仍持有**约 16 GB 提交内存**；提交限制被耗尽后进程死亡（[#16015](https://github.com/unslothai/unsloth/issues/16015)）。无修复 PR。
4. **0.1.912-beta 中的加载回归。** 一个已正常工作数周的模型在桌面端更新后（macOS 15.0.1）无法加载（[#15932](https://github.com/unslothai/unsloth/issues/15932)）。无修复 PR。
5. **长对话记录上的压缩死锁。** 存储 token 达数百万的聊天既无法自动压缩，也无法“Compact conversation”，导致线程在约 2 分钟卡顿后无法继续（[#15800](https://github.com/unslothai/unsloth/issues/15800)）；Anthropic 透传 `/v1/messages` 路径将同一失败暴露为不可恢复的 400 `exceed_context_size_error`，而不是进行压缩（[#15417](https://github.com/unslothai/unsloth/issues/15417)，已关闭）。修复 PR：[#15900](https://github.com/unslothai/unsloth/pull/15900)、[#15857](https://github.com/unslothai/unsloth/pull/15857)。
6. **MLX 内存估算器严重高报。** 对一个实际可在 24 GB Mac 上加载的模型估算为 69.7 GiB（[#15935](https://github.com/unslothai/unsloth/issues/15935)）。[#16021](https://github.com/unslothai/unsloth/pull/16021) 修正了分数矩阵的*少计*；#15935 中的高报方向相反，需要单独关注。
7. **MLX UI 渲染/列表缺口。** 通过 MLX 加载的 Dolphin Venice Edition 在 Studio UI 中渲染不正确，但在其他应用中正常（[#15858](https://github.com/unslothai/unsloth/issues/15858)）；LFM3 MLX 模型未出现在 `/v1/models` 中（[#15832](https://github.com/unslothai/unsloth/issues/15832)，修复 [#15945](https://github.com/unslothai/unsloth/pull/15945)）。
8. **ModelScope 50 GB 上限。** 当 ModelScope 作为模型源时，大于 50 GB 的文件会被阻止（[#15989](https://github.com/unslothai/unsloth/issues/15989)）。
9. **Unsloth Studio 上的 AppImage UI 卡顿**（[#15999](https://github.com/unslothai/unsloth/issues/15999)）。
10. **CLI 任务名冲突**——取决于 `--tasks` 顺序，eval 数据集任务名会与后续 YAML 任务冲突（上游 `4a87de122`，Python 3.12）（[#15982](https://github.com/unslothai/unsloth/issues/15982)）。
11. **Studio 沙箱正确性**——rewind 恢复了所有文件，*除了*点目录（`.github/`、`.vscode/`、`.devcontainer/`）内的编辑（[#16017](https://github.com/unslothai/unsloth/pull/16017)）；第二次沙箱内 `pip install` 会静默丢失模块，因为 `--target` 会跳过已存在的顶层目录（[#16018](https://github.com/unslothai/unsloth/pull/16018)）。

## 对应用开发者的意义
- **永远不要假设 masked-SFT 真的执行了掩码。** 如果你正在用“train on completions”对 Alpaca 形状的数据进行微调，请在预处理前后审计数据集行数——80% 的样本可能被静默丢弃。在 #15895 解决之前，优先使用显式的 prompt/completion 列或聊天模板。
- **OpenAI 兼容的发现机制正在加固。** `GET /v1/models` 现在会列出本地下载的 `auto_map` safetensors/MLX 检查点（[#15945](https://github.com/unslothai/unsloth/pull/15945)），并且 `/v1/audio/speech` 终于会遵循内置语音的 `speed` 参数，而不是静默返回 1.0×（[#16020](https://github.com/unslothai/unsloth/pull/16020)）。如果你依赖模型列表进行门控，升级后请重新测试。
- **长时间运行的 agent 得到缓解。** 压缩超时缩放和 `/apply-template` payload 保护（[#15900](https://github.com/unslothai/unsloth/pull/15900)、[#15857](https://github.com/unslothai/unsloth/pull/15857)）针对的是一类故障：数百万 token 的线程会永久卡住——但这些变更仍是开放的 PR，尚未合并。
- **面向 agentic retrieval 的韧性工作：** Deep Research 现在会从提供方 `structured_output_failed` JSON 拒绝中恢复，并继续同一决策点（[#15788](https://github.com/unslothai/unsloth/pull/15788)）；附加文档不再因报告预算而被截断（[#16019](https://github.com/unslothai/unsloth/pull/16019)）。
- **多租户 LoRA 服务/训练的单任务成本正在降低**——如果你针对一个 MoE 基础模型排队许多 adapter，分组 GEMM 的 MoE 路径（[#16012](https://github.com/unslothai/unsloth/pull/16012)）很重要。
- **在 Apple 上的容量规划：** 目前应把 Studio 中的 MLX VRAM 估算视为双向不可靠（#15935 高报，#16021 提高了未融合 prefill 的估算），并用实际加载情况验证。

</details>