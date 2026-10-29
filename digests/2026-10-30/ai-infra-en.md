# AI Infrastructure Digest 2026-10-30

> Generated: 2026-10-29 18:48 UTC | Projects covered: 6

- [vLLM](https://github.com/vllm-project/vllm)
- [SGLang](https://github.com/sgl-project/sglang)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [Ollama](https://github.com/ollama/ollama)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Unsloth](https://github.com/unslothai/unsloth)

---

## Cross-Project Comparison

# Cross-Project Comparison Report — AI Infrastructure, 2026-10-30

## 1. Ecosystem Overview

The ecosystem is in a hardening phase rather than a release phase: vLLM and SGLang shipped no new releases and concentrated on KV-cache correctness, connector reliability, and backend-specific regressions, while llama.cpp, Ollama, LiteLLM, and Unsloth advanced through builds, patches, and Studio fixes. The dominant technical fault line is KV-cache movement and reuse—offload tiers, NIXL/Mooncake connectors, prefix caching, and session-aware routing—now a correctness and multi-tenant isolation problem, not just a throughput lever. Hardware fragmentation is equally visible: SM120 Blackwell lacks required sparse-MLA kernels in vLLM/SGLang paths, while ROCm, SYCL, Hexagon, MLX, and XPU work proceeds at different maturity levels. Agent workloads are exposing tool-calling, reasoning round-trip, grammar/schema, and determinism gaps across both serving engines and gateways. Gateway accounting/guardrails and fine-tuning data masking remain immature enough that production teams still need downstream controls and validation.

## 2. Activity Comparison

Counts below are distinct GitHub issue/PR numbers cited in each 24h digest, not repository-wide totals. They indicate where maintainer and reporter attention concentrated.

| Project | Issues cited (24h) | PRs cited (24h) | Release status |
|---|---:|---:|---|
| **vLLM** | 21 | 12 | No release in 24h; no API/config breaking changes announced. |
| **SGLang** | 18 | 18 | No release in 24h; no breaking changes. |
| **llama.cpp** | 20 | 25 | No API/config break; continuous builds/tags around `b11972`–`b11985`. |
| **Ollama** | 15 | 9 | **v0.40.13 shipped**: LFM3 family on Linux/Windows; no API/config break. |
| **LiteLLM** | 16 | 14 | **v1.108.0-rc.1** plus stable patches **v1.106.6**, **v1.105.7**; multiple breaking-behavior PRs open. |
| **Unsloth** | 17 | 17 | No tagged release; `v0.1.912-beta` in field; heavy merge/fix day. |

## 3. Model Support Race

| Project | Model / hardware support movement in window | Position |
|---|---|---|
| **vLLM** | No new model/backend support merged. In-flight: Intel XPU Mooncake fix, MLA cache sharding for KVPP, packed MLA block geometry. **DeepSeek-V4.1-Flash on SM120 is blocked** because FlashInfer 0.7.0 lacks sparse-MLA decode kernels for `page_block_size=32`; GLM-5.3 optimization tracking continues. | Strong on KV/connector plumbing, but behind on newest SM120 model enablement. |
| **SGLang** | Advanced support for **KimiK3** via FlashInfer AllReduce Fusion, **nemotron-h** CuTe DSL W4A16 MoE, **HiDream-O1-Image** on NPU, and XPU `sage_attn`; RDNA3/RDNA4 upstreaming proposal open. Active correctness issues on DeepSeek-V4.1-Flash and GLM-5.3-Flash on SM120. | Slightly ahead on breadth of new architecture/backend PRs in this window, but backend correctness is a drag. |
| **llama.cpp** | Shipped/advanced **Hexagon UPSCALE** for vision/multimodal, **SYCL DPAS flash attention on quantized KV**, OpenCL IQ quant coverage, **ROCm/HIP RDNA4_M**, FP8/NVFP4 stack, LFM3 audio/omni quantization guards, and RPC async/event APIs. | Clear leader in local/edge backend breadth and quantization coverage. |
| **Ollama** | **v0.40.13** extends LFM3, `lfm3-audio`, and `lfm3-omni` to Linux and Windows. MLX runner Windows/CPU backend PR open. MXFP4 large-MoE loading is broken for `gpt-oss:120b`; ternary quantization unsupported. | Ahead in turnkey local model packaging; behind on large MoE and agent-facing correctness. |
| **LiteLLM** | Advanced DashScope image edits/TTS, OpenAI realtime translation and streamed `gpt-transcribe`, Azure AI Foundry Agents v2, `nokeep` zero-retention provider, and CLF AI Gateway models. | Ahead in provider/API gateway breadth; not an inference engine. |
| **Unsloth** | LFM3 Audio/Omni on MLX landed (plus repair), Apple MLX ANE prefill toggle, multi-GPU audio loading, AMD iGPU handling, NVFP4 Apple Silicon fix. General LFM3 1.7B support is still an open request. | Ahead in accessible fine-tuning and Apple/consumer hardware; general LFM3 support incomplete. |

**Who is ahead:** no single project leads across the stack. For datacenter serving, **SGLang** appears slightly ahead on new model/backend enablement in this window, while **vLLM** retains stronger KV/offload and connector breadth. For local/edge, **llama.cpp** leads on depth and **Ollama** on packaging. **LiteLLM** leads the gateway layer, and **Unsloth** leads accessible fine-tuning/Studio workflows.

## 4. Performance Frontier

| Frontier | Evidence from today’s digests | Direction |
|---|---|---|
| **KV cache and memory movement** | vLLM: NIXL/Mooncake/P2P offload, MLA cache sharding, KVPP, offload recency correctness. SGLang: Mooncake SWA packing, decode host receive, prefix-cache behavior. llama.cpp: FP8 KV-cache, SYCL DPAS on quantized KV. Ollama: KV-state bleed and VRAM eviction fixes. Unsloth: MLX memory estimation and context compaction. | The main battleground. Effort is shifting from raw capacity to tiering, correctness, and multi-tenant isolation. |
| **Scheduling and batching** | vLLM: admission backoff to prevent KV-pool saturation from inflating decode TPOT ~2.3×. SGLang: shortest-prefill-first budget accounting, context parallelism, scheduler stats. Ollama: speculative-decoding A/B and scheduler eviction. Unsloth: grouped-GEMM MoE LoRA and T4 NF4 batch crossover. | Tail latency, fairness, and multi-job efficiency. |
| **Quantization** | llama.cpp: FP8/OCP FP8/NVFP4, OpenCL IQ, SYCL DPAS quantized KV. Unsloth: NF4/NVFP4/MLX, T4 NF4 decode +13–30% at batch 4. Ollama: MXFP4 large-MoE breakage. vLLM/SGLang: fp8 mixed-batch and MXFP4 MoE tracking. | More aggressive formats, but per-backend numerics risk remains high. |
| **Distributed serving** | vLLM: NIXL pulls, P2P KV tier, MLA sharding, ROCm multi-process hangs. SGLang: AllReduce fusion, EPLB, context parallelism, Mooncake. llama.cpp: RPC pipeline parallelism. LiteLLM: least-busy routing reservation fix. | KV transfer, collective fusion, and cache-aware routing are the key distributed levers. |
| **Kernels/backends** | vLLM: DiffKV SM80 tiling **3.0×** on 200K-context chunks. SGLang: Qwen3 fused QK-norm/RoPE reuse. llama.cpp: Metal MXFP4 mat-vec, SYCL DPAS, Hexagon IM2COL. Ollama: MLX top-k for 248K-vocab rows. Unsloth: video export **115–184 s → ~1–2 s**. | Backend-specific kernel wins dominate; performance variance by hardware is large. |

**Net:** most optimization energy is in **KV-cache movement and backend kernels**, with scheduling/batching next. Quantization is increasingly coupled to KV-cache design, especially FP8/NVFP4 and quantized-KV attention.

## 5. Layer Positioning

| Layer | Projects | Primary role | Current signal |
|---|---|---|---|
| **Datacenter serving engines** | **vLLM**, **SGLang** | High-throughput GPU inference, KV/offload, distributed serving, OpenAI-compatible frontends | vLLM stronger on connector/offload breadth; SGLang stronger on scheduler/context-parallel/Rust frontend and diffusion/NPU experiments. |
| **Local runtimes** | **llama.cpp**, **Ollama** | Edge/consumer/CPU/GPU inference | llama.cpp is the low-level portability and quantization layer; Ollama is the turnkey model distribution and local API layer. |
| **LLM gateway** | **LiteLLM** | Provider abstraction, routing, guardrails, spend tracking, OpenAI compatibility | Broad provider coverage, but spend accounting and guardrail semantics still have production gaps. |
| **Fine-tuning / training** | **Unsloth** | LoRA/fine-tuning, Studio, quantization, consumer/Apple/AMD support | Strong accessibility and MLX/consumer focus; data masking and memory-estimation issues need validation. |

There is growing overlap: vLLM and SGLang expose OpenAI-compatible frontends; Ollama and Unsloth Studio can serve local OpenAI-compatible endpoints; LiteLLM routes to any of them. But their primary layers remain distinct.

## 6. Trend Signals

1. **KV cache is becoming the control plane.** Session-aware KV hints are appearing in vLLM (#52113) and SGLang (#43098, #45189), while restart semantics (#55155) and silent corruption (#64117) remain open. Agent developers should design around stable session IDs, cache-locality-aware routing, and output validation rather than assuming cache reuse is transparent.

2. **Hardware backend pinning is still mandatory.** SM120 Blackwell has missing kernels in vLLM (#59203) and SGLang attention crashes (#42012); ROCm multi-process hangs persist in vLLM (#64549, #62588); SYCL has independent ~30% MoE prefill regressions in llama.cpp (#31262, #31068). Pin backend, version, and image digest; benchmark the actual `llama-server` or engine config you deploy.

3. **Agent-facing correctness is the new adoption gate.** Tool-calling is still fragile: Ollama MLX `qwen3.8` silently fails to emit `tool_calls` (#19353), vLLM Muse parser changes string semantics (#64546), and LiteLLM’s Anthropic server-tool fix changes agent dispatch (#48385). Add schema validation, normalize content arrays, and keep a non-tool fallback.

4. **Gateway spend and guardrails cannot be trusted as sole controls.** LiteLLM streaming OpenAI-compatible traffic can log at `$0` (#48937); Lakera v2 `on_flagged: block` previously failed open on PII-only detections (#48944); `print_verbose` can leak API keys (#34705). Enforce budgets downstream and audit guardrail behavior explicitly.

5. **Quantized KV and FP8/NVFP4 are moving into production—with caveats.** llama.cpp has FP8 KV-cache in review and SYCL DPAS on `q4_0`/`q8_0` KV; Unsloth is improving NF4/NVFP4 and MLX; vLLM tracks fp8 mixed-batch issues. Prototype long-context cost savings now, but validate numerics per backend.

6. **Speculative decoding remains a sharp edge.** SGLang EAGLE hangs (#35822), llama.cpp draft-KV holes on image inputs (#27408) and MTP context sizing (#28433), and vLLM structured-output/spec-decoding RFC (#62818) all show the same pattern: failures are hard errors or silent quality changes. Keep a non-speculative fallback path.

7. **Local/edge multimodal support is expanding, but rollback and validation are weak.** Ollama added LFM3 audio/omni on Linux/Windows, but still has no supported model-digest rollback (#19385); Unsloth added ANE prefill and AMD iGPU handling; llama.cpp added Hexagon/RDNA4 coverage. Pin model digests as deploys and test audio/tool paths per host.

8. **Observability and cache-aware routing are becoming product features.** SGLang’s Rust frontend is adding per-request scheduler stats and cache-tier breakdowns (#46963, #46961); LiteLLM is fixing least-busy burst collapse (#47484); vLLM is adding HTTP keep-alive configurability (#60459). Agent platforms should prepare for cache-locality-aware routing and per-request cost/latency attribution.

---

## Per-Project Reports

<details>
<summary><strong>vLLM</strong> — <a href="https://github.com/vllm-project/vllm">vllm-project/vllm</a></summary>

# vLLM Digest — 2026-10-30

## Today's Highlights

No new vLLM releases landed in the last 24 hours. Activity was dominated by **KV offload and connector reliability** — NIXL, Mooncake, and P2P tiering — including a silent KV corruption bug and a fail-fast gap on peer faults. The highest-visibility blocker remains **DeepSeek-V4.1-Flash on SM120**, where a compressed-layer `page_block_size=32` has no matching FlashInfer sparse-MLA decode kernel, while performance work advanced on DiffKV SM80 tiling and DeepSeek V4.1 Engram prefetching.

---

## Releases & Breaking Changes

No releases in the last 24h; no API or config breaking changes announced in this window.

---

## New Model & Hardware Support

No new model or backend support was merged in this window. In-flight enablement and blockers:

- **DeepSeek-V4.1-Flash on SM120 (RTX PRO 6000 Blackwell) is blocked.** The compressed-layer path uses `page_block_size=32`, but FlashInfer 0.7.0 only instantiates sparse-MLA decode kernels for `pbs=64`, so the model cannot run at all on SM120. 24 comments — the most active issue of the day. [#59203](https://github.com/vllm-project/vllm/issues/59203)
- **GLM-5.3 optimization tracking** continues on the shared `glm_moe_dsa` architecture, with additional CUDA work proposed beyond the GLM-5.2 optimizations. [#57406](https://github.com/vllm-project/vllm/issues/57406)
- **Intel XPU Mooncake support**: PR fixes two CUDA assumptions in `MooncakeStoreConnector` (notably `torch.cuda.Event` annotation evaluation on XPU). [#62546](https://github.com/vllm-project/vllm/pull/62546)
- **MLA cache sharding for KVPP**: opt-in `--enable-kvpp` adds layer-sharded MLA KV caches with NCCL broadcast prefetch across PCP × TP replica groups. [#59059](https://github.com/vllm-project/vllm/pull/59059)
- **Packed MLA block geometry**: fix preserves mixed-granularity cache geometry for TP1 DeepSeek-V4-Flash NIXL P/D engines. [#50717](https://github.com/vllm-project/vllm/pull/50717)

---

## Performance & Optimization

- **DiffKV prefill tiling on SM80**: `BLOCK_M=128` + KV tile 64 yields **3.0×** on 200K-context chunks for `TRITON_ATTN_DIFFKV`; prior `BLOCK_M=16` reloaded the whole KV tile per query position. [#61095](https://github.com/vllm-project/vllm/issues/61095)
- **KV-pool-saturated admission retries inflate decode TPOT ~2.3×** on Ascend 910B / V1 scheduler; proposal is automatic admission backoff. Platform-independent mechanism. [#64460](https://github.com/vllm-project/vllm/issues/64460)
- **ROCm sliding-window prefill**: skip fully-masked context tiles in `ROCM_ATTN` prefix prefill; output is bit-identical, only tiles before the window are omitted. [#63867](https://github.com/vllm-project/vllm/pull/63867)
- **DeepSeek V4.1 Engram prefetch**: opt-in Numba worker hashes prompt tokens and gathers CPU-offloaded Engram rows ahead of eager prefill for PCIe-attached GPUs. [#64500](https://github.com/vllm-project/vllm/pull/64500)
- **Unified-attention TD loop**: hoist tensor-descriptor construction out of the per-tile loop to avoid a `tensormap_create` per iteration and restore pipelining. [#51506](https://github.com/vllm-project/vllm/pull/51506)
- **NIXL pull receiver**: opt-in background receiver for large NIXL pulls, moving descriptor prep, READ submission, polling, and handle release off the decode model thread. [#57987](https://github.com/vllm-project/vllm/pull/57987)
- **Offload recency correctness/perf**: return lazily offloaded GPU blocks to the eviction end rather than the MRU end (otherwise stale CPU-held blocks outlive fresher ones). [#59383](https://github.com/vllm-project/vllm/pull/59383); also record GPU-local prefix reuse in CPU offload recency. [#57746](https://github.com/vllm-project/vllm/pull/57746)

---

## Stability & Regressions

**Critical**

- **Silent KV corruption in `MooncakeStoreConnector` under BHLNC**: per-head segments are transferred using the whole-block stride as their length. Silent data corruption on Qwen2.5-0.5B / T4 / vLLM 0.29.0. No direct fix PR identified in this window. [#64117](https://github.com/vllm-project/vllm/issues/64117)
- **DeepSeek-V4.1-Flash cannot run on SM120**: missing FlashInfer sparse-MLA decode kernel instantiation for `pbs=32`. Hard startup/runtime blocker on RTX PRO 6000 Blackwell. [#59203](https://github.com/vllm-project/vllm/issues/59203)

**High**

- **FlashMLA sparse decode re-allocates split-KV workspace on SM90** — regression of #53413, risking runtime OOM on H200 with fp8 mixed-batch. [#59305](https://github.com/vllm-project/vllm/issues/59305)
- **P2P KV offload tier does not fail fast on peer faults**: requests can hang rather than surface peer failures; reproduced on H200 + mlx5 InfiniBand + NIXL 1.5.0. [#63602](https://github.com/vllm-project/vllm/issues/63602)
- **ROCm GLM-5.3 TP8 hang** during `OffloadingConnector` CPU↔GPU copies when other vLLM processes share MI325X SR-IOV VFs; generation drops to zero with requests still running. [#64549](https://github.com/vllm-project/vllm/issues/64549)
- **ROCm multi-process hang on MI300X SR-IOV VF**: two or more vLLM processes hang within minutes — queue head dispatch accepted, no waves, GFX 100%. [#62588](https://github.com/vllm-project/vllm/issues/62588)
- **`custom_all_reduce.cuh:164 'invalid argument'`** CUDA failure in multi-GPU setups. [#56180](https://github.com/vllm-project/vllm/issues/56180)

**Medium**

- **`dots.ocr` produces identical "blurry image" output for every region at TP=2** on Ascend 910B. [#64541](https://github.com/vllm-project/vllm/issues/64541)
- **`vllm/vllm-openai:unlimited-ocr` image cannot serve the Unlimited-OCR model.** [#64489](https://github.com/vllm-project/vllm/issues/64489)
- **Muse tool parser JSON-decodes `Optional[str]` parameters** — `"10001"` becomes `10001`, changing tool-call semantics. [#64546](https://github.com/vllm-project/vllm/issues/64546)
- **Rust `vllm-bench` silently ignores `--dataset-path`** with synthetic datasets and benchmarks random prompts instead — invalidates benchmark results. [#64538](https://github.com/vllm-project/vllm/issues/64538)

**Closed / resolved in this window**

- `/v1/messages` hoisting mid-conversation system messages without `--chat-template`, breaking prefix caching for DeepSeek-V4.1-Flash. [#60537](https://github.com/vllm-project/vllm/issues/60537)
- `/v1/completions/derender` dropped requested `prompt_logprobs`. [#57929](https://github.com/vllm-project/vllm/issues/57929)
- Bare `@torch.compile` in `kimi_k25_vit` compiled outside the lifecycle and pinned `TRITON_CACHE_DIR` process-wide. [#52965](https://github.com/vllm-project/vllm/issues/52965)

**Ongoing correctness work**

- **HiSparse tracking**: swap-capacity off-by-one and long-prefill/decoder mixed-batch OOM fixed; new fix reserves in-flight imports' host pages at admission to avoid two waiting loads deadlocking on each other's pages. [#60072](https://github.com/vllm-project/vllm/issues/60072), [#62979](https://github.com/vllm-project/vllm/pull/62979)
- **NIXL hardening**: validate `kv_transfer_params` before receive registration to prevent malformed client input crashing the Decode EngineCore. [#54807](https://github.com/vllm-project/vllm/pull/54807)
- **Structured output + speculative decoding RFC closed**: addresses output-distribution preservation when trimming draft tokens to grammar-valid prefixes. [#62818](https://github.com/vllm-project/vllm/issues/62818)

---

## What This Means for Application Developers

- **Do not deploy Mooncake-backed KV offload with BHLNC layouts** until #64117 is fixed — the failure mode is silent KV corruption, not a crash. Validate outputs, not just availability.
- **DeepSeek-V4.1-Flash on Blackwell (SM120) is not viable today.** Stay on Hopper/other supported SKUs, or wait for a FlashInfer `pbs=32` sparse-MLA kernel.
- **Tool-calling correctness issue**: if you use `--tool-call-parser muse`, string-typed parameters may arrive as integers. Add schema-level validation on the client side for IDs, ZIP codes, and other numeric-looking strings.
- **Benchmark results from Rust `vllm-bench` are untrustworthy** when passing `--dataset-path` with synthetic dataset settings — verify the prompt source before using numbers for capacity planning.
- **Agentic workloads have an open RFC for session-aware KV cache hints** (release completed branches, pin soon-to-resume agents, share long system/tool prefixes). Worth tracking if you build multi-agent systems. [#52113](https://github.com/vllm-project/vllm/issues/52113)
- **KV transfer restart semantics are not yet supported**: NIXL connectors lack restart lifecycle hooks, which matters for snapshot/restore and device-recovery flows. [#55155](https://github.com/vllm-project/vllm/issues/55155)
- **Frontend configurability improving**: `--http-timeout-keep-alive` is being added across the Python API server, CPU render server, and Rust frontend. [#60459](https://github.com/vllm-project/vllm/pull/60459)

</details>

<details>
<summary><strong>SGLang</strong> — <a href="https://github.com/sgl-project/sglang">sgl-project/sglang</a></summary>

# SGLang Digest — 2026-10-30

## 1. Today's Highlights
No new releases in the last 24h, but activity is dominated by hardware-backend correctness work: a crash in the `fa4` attention backend on SM120 for GLM-5.3-Flash, a scheduler-killing bug in DeepSeek-V4 under aborted multimodal streams, and a silent weight-update hazard affecting DFLASH draft models. On the performance side, PRs landed or advanced for Qwen3 fused QK-norm/RoPE decode reuse, MiniMax sparse decode indexer context parallelism on Hopper, and widening K3 coverage for FlashInfer AllReduce Fusion.

## 2. Releases & Breaking Changes
None in the last 24h.

## 3. New Model & Hardware Support
- **[PR #47306](https://github.com/sgl-project/sglang/pull/47306)** — Enables FlashInfer AllReduce Fusion auto-enable for `KimiK3ForConditionalGeneration` (previously only Kimi-K2.5 was in `_FLASHINFER_ALLREDUCE_FUSION_ARCHS`).
- **[PR #44750](https://github.com/sgl-project/sglang/pull/44750)** — nemotron-h: allow explicit CuTe DSL W4A16 MoE path.
- **[PR #45137](https://github.com/sgl-project/sglang/pull/45137)** — Diffusion/NPU: adds HiDream-O1-Image support (Dev-2604, Dev, Full variants).
- **[PR #45485](https://github.com/sgl-project/sglang/pull/45485)** — SGLang-Diffusion XPU: Triton path for `sage_attn`, ported from the SageAttention kernels.
- **[Issue #46900](https://github.com/sgl-project/sglang/issues/46900)** — Proposal to bring RDNA3/RDNA4 (`gfx1100`/`gfx1201`) onto main with CI coverage and an upstreaming plan.
- **[Issue #38515](https://github.com/sgl-project/sglang/issues/38515)** — Per-op cubin coverage gap in the `sgl_kernel` AOT wheel on sm_75: `rmsnorm` fails with `cudaErrorNoKernelImageForDevice` while `silu_and_mul`/`gelu_and_mul` work; no soft fallback to torch/Triton.

## 4. Performance & Optimization
- **[PR #46908](https://github.com/sgl-project/sglang/pull/46908)** — Qwen3 decode: reuses the existing table-based QK-norm/RoPE fused kernel to do both in place, removing one launch per layer plus the intervening Q/K write/read, with no new kernel. Measured on Qwen3-8B.
- **[PR #46597](https://github.com/sgl-project/sglang/pull/46597)** — minimax-sparse: runs the decode indexer context-parallel at TP4/TP8 on Hopper. Motivation notes that at 128K context every rank otherwise scans ~33.5 MB per request per sparse layer on each decode step.
- **[PR #44115](https://github.com/sgl-project/sglang/pull/44115)** — Passes `uniform_q_len` to the FlashInfer target-verify plan for EAGLE, giving the FA2 CUDA-graph planner the constant-stride query shape it cannot infer from ragged CSR.
- **[PR #47308](https://github.com/sgl-project/sglang/pull/47308)** — Scheduler: accounts for both the chunk budget and the separate input budget during shortest-prefill-first reservation (example: 4096-token chunk budget vs. 2048-token input budget could cap a 256-token waiter at 3840 tokens).
- **[PR #47307](https://github.com/sgl-project/sglang/pull/47307)** — AMD/Mooncake: default-off `SGLANG_MOONCAKE_SWA_PACKING` gathers destination-local heads and writes whole SWA KV pages when prefill TP < decode TP.
- **[PR #47106](https://github.com/sgl-project/sglang/pull/47106)** — Rust frontend: `RustServer.push_generation` flattens egress logprob columns only for rows that carry them, reducing GIL-held per-step work on the scheduler thread.
- **[PR #46592](https://github.com/sgl-project/sglang/pull/46592)** (closed) — EPLB: warms default-group NCCL P2P transports on multi-node full-EP layouts before KV-cache sizing, avoiding lazy cross-node connection setup during the first rebalance.
- **[Issue #44304](https://github.com/sgl-project/sglang/issues/44304)** — Open ROCm gfx950/MI355X performance tracker for Qwen3.8-Flash-Next (GatedDeltaNet, QuerySparse Attention, MXFP4 MoE, NEXTN MTP).

## 5. Stability & Regressions
Ranked by severity:

1. **[Issue #47218](https://github.com/sgl-project/sglang/issues/47218)** — *Critical.* DeepSeek-V4.1-Flash scheduler crashes when `items_offset_list` is `None` in the multimodal embedding path under concurrent aborted streams; takes down all TP/EP workers and restarts the serving container (`lmsysorg/sglang:dev-dsv41`).
2. **[Issue #46806](https://github.com/sgl-project/sglang/issues/46806)** — *High / silent correctness.* `update_weights_from_disk` has no `selector`, so weight updates can load the target model's weights into a DFLASH draft model. Same symptom previously noted for EAGLE3 external drafts in THUDM/slime#1177.
3. **[Issue #45525](https://github.com/sgl-project/sglang/issues/45525)** — *High.* DeepSeek-V4-Flash: speculative and ordinary decoding produce different greedy outputs.
4. **[Issue #47213](https://github.com/sgl-project/sglang/issues/47213)** — *High.* Qwen3.5: prefix-cache reuse changes logprobs even with deterministic inference enabled.
5. **[Issue #42012](https://github.com/sgl-project/sglang/issues/42012)** — *High on SM120.* GLM-5.3-Flash on 8× RTX PRO 6000: `fa4` crashes at CUDA-graph capture on hybrid extend reshape; Triton is the only working attention backend (`v0.5.20` image).
6. **[Issue #35822](https://github.com/sgl-project/sglang/issues/35822)** — *High.* EAGLE speculative decoding with native Qwen3.5/3.8 MTP hangs in `tree_speculative_sampling_target_only` on Ampere (2× A2, TP=2, 100% GPU util at low power).
7. **[Issue #47245](https://github.com/sgl-project/sglang/issues/47245)** — *Medium.* A retracted and re-prefilled request resets `frequency_penalty`/`presence_penalty`/`repetition_penalty` accumulators and `min_new_tokens` to zero, silently changing output.
8. **[Issue #47205](https://github.com/sgl-project/sglang/issues/47205)** — *Medium.* Reasoning grammar gate never opens when the think-end marker is split under `split_special_tokens`.
9. **[Issue #47294](https://github.com/sgl-project/sglang/issues/47294)** — *Medium.* `/start_profile` with `profile_by_stage=true` and no `num_steps` crashes every scheduler (`TypeError: NoneType += int`) on v0.5.22 with DSpark speculative decoding.
10. **[Issue #46803](https://github.com/sgl-project/sglang/issues/46803)** — *Low / latency spike.* FlashInfer `cascade` JIT-compiles inside the first prefixed request (~4.5 s) on pip installs.
11. **[Issue #47297](https://github.com/sgl-project/sglang/issues/47297)** — Diffusion: LingBot-Video-MoE crashes in text encoding under default layerwise offload (tied vocab table left on CPU).
12. **Packaging note — [Issue #47242](https://github.com/sgl-project/sglang/issues/47242):** on Python 3.13, installing SGLang 0.5.22 requires a Rust toolchain, caused by the `outlines==0.1.11` → `outlines_core==0.1.26` exact pin; undocumented.

Supporting fixes in flight: **[PR #46373](https://github.com/sgl-project/sglang/pull/46373)** (disaggregation: send decode transfer destinations to prefill only after the in-flight forward, avoiding KV page free during an active forward), **[PR #46262](https://github.com/sgl-project/sglang/pull/46262)** (MLX/Metal `rope_pool_fused` array leak), **[PR #47124](https://github.com/sgl-project/sglang/pull/47124)** (decode host receive on the unified page-envelope host pool), **[PR #47158](https://github.com/sgl-project/sglang/pull/47158)** (follower-rank SIGTERM handler made overridable). CI flake tracking continues in **[Issue #42752](https://github.com/sgl-project/sglang/issues/42752)** (138 comments).

## 6. What This Means for Application Developers
- **Pin your backend explicitly on consumer/workstation Blackwell (SM120).** If you serve GLM-5.3-Flash or similar on RTX PRO 6000, set the attention backend to Triton; `fa4` currently dies during CUDA-graph capture.
- **Treat runtime weight updates as unsafe until the DFLASH selector gap is fixed.** Workflows like RLHF/GRPO weight sync (slime, external draft models) can silently overwrite a draft model's weights with the target's — a failure that surfaces as degraded acceptance rates, not an error.
- **Determinism guarantees are still eroding in edge cases**: prefix-cache reuse shifting logprobs (#47213), spec-vs-greedy divergence on DeepSeek-V4-Flash (#45525), and sampling-penalty state resets across retraction/re-prefill (#47245). If your app compares outputs across runs or replicas, add tolerance or disable prefix caching / speculative decoding for those paths.
- **Session- and agent-level KV orchestration is the direction of travel.** [Issue #43098](https://github.com/sgl-project/sglang/issues/43098) (Agentic Cache Scheduling roadmap, 7 👍) and [Issue #45189](https://github.com/sgl-project/sglang/issues/45189) (session-aware KV cache orchestration in the router) signal that cross-engine KV sharing and session-aware routing are coming — worth designing agent architectures around stable session IDs and cache-locality awareness.
- **Rich observability is arriving via the Rust frontend**: per-request scheduler stats ([PR #46963](https://github.com/sgl-project/sglang/pull/46963)), cached-token breakdowns by cache tier ([PR #46961](https://github.com/sgl-project/sglang/pull/46961)), and a native `/generate` extension hook with request/headers/outcome ([PR #47112](https://github.com/sgl-project/sglang/pull/47112)) will make cache-hit and latency attribution much more precise.
- **Python 3.13 users**: budget for a Rust toolchain in your image build, or stay on 3.12 until the `outlines_core` pin is resolved.

</details>

<details>
<summary><strong>llama.cpp</strong> — <a href="https://github.com/ggml-org/llama.cpp">ggml-org/llama.cpp</a></summary>

# llama.cpp Digest — 2026-10-30

## 1. Today's Highlights

Backend kernel work dominates the last 24 hours: Metal landed a rewritten MXFP4 mat-vec path, SYCL added a DPAS flash-attention kernel that operates directly on quantized KV blocks, and Hexagon picked up IM2COL parallelization plus a new UPSCALE op. In parallel, the FP8/NVFP4 stack is maturing across CUDA, Vulkan, and ggml core, with FP8 KV-cache support in review. On the stability side, a HIP fused Gated Delta Net bug that leaks recurrent state across requests on a reused server slot is the most serious open item for multi-tenant serving.

## 2. Releases & Breaking Changes

No public API or config breaking changes. Notable behavioral fixes:

- **b11972** — `common, mtmd`: control-vector layer indices are now bounded by model layer count, and M-RoPE position loops are bounded. Malformed tensor names / positions that previously caused out-of-bounds writes are now rejected. ([#31336](https://github.com/ggml-org/llama.cpp/pull/31336), [tag](https://github.com/ggml-org/llama.cpp/releases/tag/b11972))
- **b11977** — `ggml-openvino`: SCALE now correctly handles strided view inputs instead of scaling the entire source tensor. This changes model output where the previous (incorrect) path was taken — re-validate OpenVINO numerics. ([#31334](https://github.com/ggml-org/llama.cpp/pull/31334), [tag](https://github.com/ggml-org/llama.cpp/releases/tag/b11977))
- **b11978** — test-only fix for `comp_padding` CUDA graph reservation. ([#31344](https://github.com/ggml-org/llama.cpp/pull/31344), [tag](https://github.com/ggml-org/llama.cpp/releases/tag/b11978))

## 3. New Model & Hardware Support

- **Hexagon: UPSCALE op** — nearest 2x/4x and bilinear 4x, non-contiguous rows, dimension collapsing, `vgather` instead of scalar staging. Enables vision/multimodal graphs on Hexagon. ([#31331](https://github.com/ggml-org/llama.cpp/pull/31331), [b11982](https://github.com/ggml-org/llama.cpp/releases/tag/b11982))
- **SYCL: DPAS flash attention for quantized KV cache** — decode and small batches (1–31 query tokens) run FA directly on `q4_0`/`q8_0` KV blocks, avoiding scalar dequant or conversion. ([#31125](https://github.com/ggml-org/llama.cpp/pull/31125), [b11980](https://github.com/ggml-org/llama.cpp/releases/tag/b11980))
- **OpenCL quantization coverage** — initial IQ1_S/IQ1_M ([#31341](https://github.com/ggml-org/llama.cpp/pull/31341)), IQ3_S/IQ3_XXS ([#31338](https://github.com/ggml-org/llama.cpp/pull/31338)), and IQ4_XS ([#31339](https://github.com/ggml-org/llama.cpp/pull/31339)) support, Adreno-optimized.
- **ROCm/HIP: RDNA4_M family** for `gfx1170`/`gfx1171` (128b WMMA, distinct from RDNA4). ([#31373](https://github.com/ggml-org/llama.cpp/pull/31373))
- **FP8 / NVFP4 stack** — CUDA OCP FP8 ([#28413](https://github.com/ggml-org/llama.cpp/pull/28413)), Vulkan FP8 + scaled matmul ([#29791](https://github.com/ggml-org/llama.cpp/pull/29791)), ggml-level quant scales for FP8/NVFP4 across backends ([#28898](https://github.com/ggml-org/llama.cpp/pull/28898)), and FP8 KV-cache with optional static per-tensor scales ([#28392](https://github.com/ggml-org/llama.cpp/pull/28392)). OCP FP8 E4M3 quant support has merged ([#27512](https://github.com/ggml-org/llama.cpp/pull/27512)).
- **LFM3 audio/omni** — quantization guards relaxed for LFM3-Audio-2B and LFM3-Omni-2B codec decoders (QAT-trained, quantize cleanly); mmproj size unchanged at BF16 570.8 MB. ([#31386](https://github.com/ggml-org/llama.cpp/pull/31386)). LFM2 shortconv/FFN blocks refactored into a shared LFM base for reuse. ([#30874](https://github.com/ggml-org/llama.cpp/pull/30874))
- **RPC: event + async backend APIs** implemented, enabling pipeline parallelism over RPC. ([#18626](https://github.com/ggml-org/llama.cpp/pull/18626))

## 4. Performance & Optimization

- **Metal MXFP4 mat-vec** — fp16 bit-trick decode replaces the threadgroup lookup table; packed nibbles loaded as aligned 32-bit words; full threadgroups for unary/binary/GLU. ([#31075](https://github.com/ggml-org/llama.cpp/pull/31075), [b11985](https://github.com/ggml-org/llama.cpp/releases/tag/b11985))
- **Hexagon transposed CONCAT** — doubled row block size and scratchpad double-buffering, chunked `src1` rows, VTCM stride padding to spread gather lanes; targets DDR bandwidth utilization. ([#31277](https://github.com/ggml-org/llama.cpp/pull/31277), [b11981](https://github.com/ggml-org/llama.cpp/releases/tag/b11981))
- **Hexagon IM2COL** — block-based HVX parallelization across threads, fixed padding handling, unrolled common cases. ([#31050](https://github.com/ggml-org/llama.cpp/pull/31050), [b11976](https://github.com/ggml-org/llama.cpp/releases/tag/b11976))
- **SYCL reordered-layout dequant stores** — widened stores for Q4_0, K-quants, IQ3, MXFP4 instead of per-byte scalar writes strided 16 elements apart. ([#30976](https://github.com/ggml-org/llama.cpp/pull/30976), [b11979](https://github.com/ggml-org/llama.cpp/releases/tag/b11979))
- **Gemma 4 prompt-processing graph optimizations** — skip compute for layers that do not contribute to the KV cache; reported "massive gains" on PP for E2B/E4B. ([#31356](https://github.com/ggml-org/llama.cpp/pull/31356), related [#29189](https://github.com/ggml-org/llama.cpp/pull/29189))
- **KV-cache: rotation constants resident on GPU** — Hadamard static matrices kept on-device instead of per-step host trips; meaningful on PCIe-constrained multi-GPU setups. ([#31073](https://github.com/ggml-org/llama.cpp/pull/31073))
- **SYCL CONV_TRANSPOSE_1D** — bounded input iteration on Arc Pro B70. ([#31109](https://github.com/ggml-org/llama.cpp/pull/31109))

## 5. Stability & Regressions

Ranked by severity:

1. **Cross-request state contamination (critical for multi-tenant)** — HIP/ROCm fused Gated Delta Net carries recurrent state across requests on a reused server slot (qwen35/qwen35moe); earlier prompts' text is emitted verbatim in later completions. No fix PR referenced. ([#29092](https://github.com/ggml-org/llama.cpp/issues/29092))
2. **Security: WebUI instruction injection via `?q=` query parameter.** ([#25790](https://github.com/ggml-org/llama.cpp/issues/25790)). Related: unbounded `enum` in `json_schema` causes superlinear grammar construction, pinning a core for tens of seconds per small request (DoS). ([#29457](https://github.com/ggml-org/llama.cpp/issues/29457)). GBNF nested-repetition stack overflow was closed. ([#18988](https://github.com/ggml-org/llama.cpp/issues/18988))
3. **Grammar failures returning HTTP 500** — LFM3 rejects any `response_format` with "Unexpected empty grammar stack after accepting piece: 6 (30)". ([#31328](https://github.com/ggml-org/llama.cpp/issues/31328)). `json-schema-to-grammar` copies raw control characters (e.g. NUL from `\u0000`) into GBNF patterns verbatim → "failed to parse grammar". ([#31199](https://github.com/ggml-org/llama.cpp/issues/31199))
4. **Crashes / init failures** — `--split-mode tensor` asserts on `GGML_ASSERT(bcj.nodes[i])` on the second request (2x/3x Tesla P100, CUDA). ([#29466](https://github.com/ggml-org/llama.cpp/issues/29466)). SYCL bf conversion instruction unsupported on Arrow Lake iGPU. ([#31029](https://github.com/ggml-org/llama.cpp/issues/31029)). Jetson Orin NX hangs before serving after the b8638→b9016 server rewrite. ([#29499](https://github.com/ggml-org/llama.cpp/issues/29499)). Metal init failure on macOS 14 / M2 Ultra from a `constexpr` bfloat cast in `unary.metal` has been closed. ([#31272](https://github.com/ggml-org/llama.cpp/issues/31272))
5. **Performance regressions** — SYCL `llama-server` prompt processing ~35% slower in b11804 vs b11046 with CPU-offloaded MoE experts (`-ncmoe`), not reproduced by `llama-bench` (i.e., server-path specific). ([#31262](https://github.com/ggml-org/llama.cpp/issues/31262)). SYCL XMX-ESIMD path ~28–35% slower on MoE PP for Arc Pro B70 (regression in `d81d0d8fb`). ([#31068](https://github.com/ggml-org/llama.cpp/issues/31068)). Vulkan deep-context decode collapses ~8x from 1k→64k tokens on Arc Pro B70 (SYCL degrades only ~2.4x). ([#28721](https://github.com/ggml-org/llama.cpp/issues/28721)). Speculative decode performance drop reported. ([#31220](https://github.com/ggml-org/llama.cpp/issues/31220))
6. **Correctness** — hybrid LFM2 co-batching corrupts recurrent/short-conv state; greedy output diverges and can stop mid-sentence. ([#29002](https://github.com/ggml-org/llama.cpp/issues/29002)). SYCL CPY to `q4_1`/`q5_1`/`q8_0` does not match CPU reference. ([#31140](https://github.com/ggml-org/llama.cpp/issues/31140))
7. **Speculative decoding / multimodal** — mtmd image chunks leave positional holes in the draft KV cache, causing ~500 s stalls then HTTP 500 with `--spec-type draft-dflash`. ([#27408](https://github.com/ggml-org/llama.cpp/issues/27408)). `draft-mtp` context sized from `llama_n_ctx()` rather than `llama_n_ctx_seq()`, killing the server on large `--ctx-size`. ([#28433](https://github.com/ggml-org/llama.cpp/issues/28433)). MiMo-V2.6 sidecar MTP draft fails with `blk.0.attn_q not found`. ([#29345](https://github.com/ggml-org/llama.cpp/issues/29345))
8. **Cache efficiency** — reasoning/content whitespace not round-trippable for Qwen3.5+ chat templates → prefix-cache invalidation and full re-prefill on hybrid models. ([#30357](https://github.com/ggml-org/llama.cpp/issues/30357))

## 6. What This Means for Application Developers

- **Multi-tenant serving on ROCm: pin or isolate.** The Gated Delta Net state-bleed (#29092) means a reused slot can emit another user's prompt text. Until fixed, avoid aggressive slot reuse on HIP for hybrid/recurrent models, or run one slot per session.
- **Treat grammar/schema handling as an untrusted input surface.** Three separate issues (control-character injection into GBNF, large-`enum` superlinear construction, LFM3 empty grammar stack) let a single request produce 500s or pin a core. Validate/normalize `response_format` payloads at the gateway and cap `enum` size.
- **Backend version pinning still matters more than headline benchmarks.** SYCL has two independent ~30% MoE prefill regressions (#31262, #31068) and a Vulkan long-context decode collapse (#28721); `llama-bench` does not reproduce the server-path regression, so benchmark the actual `llama-server` configuration you deploy.
- **Quantized-KV inference is getting real.** SYCL DPAS FA on `q4_0`/`q8_0` KV plus FP8 KV-cache in review (#28392) will materially cut KV memory for long-context agents — worth prototyping now, but expect per-backend numerics differences (see #31140).
- **Speculative decoding remains the sharpest edge** for agent workloads: draft-KV positional holes on image inputs (#27408) and MTP context sizing (#28433) both manifest as hard 500s, not graceful degradation. Keep a non-speculative fallback path.
- **Prompt-processing wins are landing for Gemma 4** (#31356) and **FP8/NVFP4 support is broadening** across CUDA/Vulkan/ggml — plan quantization pipelines around FP8 E4M3 and NVFP4 rather than assuming Q4/Q8 only.

</details>

<details>
<summary><strong>Ollama</strong> — <a href="https://github.com/ollama/ollama">ollama/ollama</a></summary>

# Ollama Digest — 2026-10-30

## 1. Today's Highlights
Ollama shipped **v0.40.13**, extending Liquid AI's **LFM3** family (including `lfm3-audio` TTS and `lfm3-omni`) from Apple silicon to **Linux and Windows**. The issue tracker is dominated by agent-facing correctness problems rather than throughput work: an MLX tool-calling regression on `qwen3.8`, KV-state bleed on ROCm iGPUs, and multiple OpenAI-compatibility gaps around reasoning/content arrays — for two of which fix PRs are already open. In parallel, the MLX runner is getting Windows/CPU backend support and a substantially cheaper top-k path for large vocabularies.

## 2. Releases & Breaking Changes
- **v0.40.13** — LFM3 (`lfm3`, `lfm3-audio`, `lfm3-omni`) now runs on Linux and Windows in addition to Apple silicon. Previously the model required the MLX runtime, which was undocumented and caused Linux pull/run failures ([#19369](https://github.com/ollama/ollama/issues/19369), closed). If you gated LFM3 rollouts to macOS, that gate can be lifted — but re-validate audio paths on non-Apple hosts.
- **No API/config breaking changes announced today.** Operational note: there is still no supported way to **roll back a model to a previous digest** after an in-place "update" ([#19385](https://github.com/ollama/ollama/issues/19385), closed without a mechanism). Pin digests explicitly in production manifests.

## 3. New Model & Hardware Support
- **LFM3 / lfm3-audio / lfm3-omni on Linux + Windows** — [release v0.40.13](https://github.com/ollama/ollama/releases).
- **MLX runner on Windows + CPU backend** — [PR #19366](https://github.com/ollama/ollama/pull/19366) adds native Windows execution and a CPU backend alongside Metal/CUDA, and enables full TTS inference (e.g. `phonon:en`) on those paths. Open, not merged.
- **MXFP4 large-MoE loading is broken**: `gpt-oss:120b` fails GGUF metadata parse with `unsupported tensor "blk.0.ffn_down_exps.weight" size overflows` on 0.40.12 ([#19375](https://github.com/ollama/ollama/issues/19375)); same class of failure reported on 0.40.1 ([#18869](https://github.com/ollama/ollama/issues/18869), closed). Treat 120B MXFP4 as unusable until an overflow fix lands.
- **Ternary quantization (Bonsai 2)** — request closed without support ([#19388](https://github.com/ollama/ollama/issues/19388)).

## 4. Performance & Optimization
- **MLX top-k over long rows** — [PR #19392](https://github.com/ollama/ollama/pull/19392): MLX's `argpartition` sorts entire rows, and on Metal a row >2048 values triggers a multi-pass merge sort, which dominates top-k cost on a **248K-token vocabulary**. The patch sorts each 2048-value chunk in a single pass, then merges. Directly relevant to sampling latency on large-vocab MLX models.
- **Speculative decoding benchmarking on MLX** — [PR #19391](https://github.com/ollama/ollama/pull/19391) adds `draft_num_predict=0` to disable drafting per request (system default stays 4). Lets you A/B the spec-decode speedup without changing server config; draft caches are maintained in lockstep so later drafting requests are unaffected.
- **Scheduler VRAM eviction correctness** — [PR #19284](https://github.com/ollama/ollama/pull/19284): on multi-GPU hosts, the pre-load VRAM prediction can exceed reported free memory and evict a runner selected purely by idle time — including **CPU-only runners** whose memory doesn't help. Prevents spurious evictions and reload churn.
- **Flash attention no longer forced for gpt-oss** — [PR #17477](https://github.com/ollama/ollama/pull/17477) explicitly requests flash attention for architectures that default to it; the regression caused **GPT-OSS Q8 crashes at long context** under partial offload ([#17430](https://github.com/ollama/ollama/issues/17430)). Still open.

## 5. Stability & Regressions (ranked)
1. **KV cache contamination across requests (critical, correctness)** — ROCm on Strix Halo `gfx1151` iGPU (`0.32.14-rocm`): responses are contaminated by the *previous* request's content ([#17847](https://github.com/ollama/ollama/issues/17847), open since Aug, 11 comments). No fix PR. Do not serve untrusted/multi-tenant traffic on this backend.
2. **MLX tool calling silently broken (high)** — `qwen3.8:27b-mlx` never emits `tool_calls` when the assistant produces free-text content first; only works with empty `content` ([#19353](https://github.com/ollama/ollama/issues/19353)). Breaks the standard "announce then act" agent pattern.
3. **go_template drops the entire assistant turn (high)** — `/api/chat` with `tools` returns empty content, `tool_calls: null`, `eval_count > 0`; llama.cpp parses the same generation correctly ([#19377](https://github.com/ollama/ollama/issues/19377), closed).
4. **OpenAI compat: reasoning dropped / reasoning-only turns deleted** when `content` is a content-parts array ([#19380](https://github.com/ollama/ollama/issues/19380)) — fix open: [PR #19384](https://github.com/ollama/ollama/pull/19384).
5. **`/v1/models` returns `"data": null`** with zero models, breaking strongly-typed SDKs ([#19381](https://github.com/ollama/ollama/issues/19381)); related fix for empty embedding arrays: [PR #19387](https://github.com/ollama/ollama/pull/19387).
6. **Intermittent CUDA warmup failure with silent CPU fallback (medium)** — `shared object initialization failed` on Windows + RTX 5070 Ti with `gpt-oss:20b`, falling back to `CUDA_Host`→CPU pinned buffers without surfacing the downgrade ([#17380](https://github.com/ollama/ollama/issues/17380)).
7. **`OLLAMA_NUM_PARALLEL=1` apparently not enforced (medium)** — two concurrent sessions observed despite the setting ([#19262](https://github.com/ollama/ollama/issues/19262)); relevant if you rely on serialization for memory bounds.
8. **Silent field drops in native API (low–medium)** — `/api/chat` ignores `audio` even for models advertising the `audio` capability; audio only works via `images` ([#19378](https://github.com/ollama/ollama/issues/19378)). Invalid content types alongside `tool_calls` are silently coerced instead of 400ing ([PR #19389](https://github.com/ollama/ollama/pull/19389), open).
9. **macOS 27 app shell broken (low, client only)** — window and menu bar icon never appear (`com.electron.ollama` bundle lookup); server and CLI fine ([#19370](https://github.com/ollama/ollama/issues/19370), closed).
10. **Chat truncation can drop the newest user message** during multi-step tool loops, yielding `500: no user query found` ([PR #18697](https://github.com/ollama/ollama/pull/18697), open).

## 6. What This Means for Application Developers
- **Pin model digests.** With no rollback path after `ollama pull` updates a tag, a model update is a one-way door for your eval baselines. Treat digest changes as deploys.
- **Don't depend on `reasoning` round-tripping through `/v1` yet.** If you replay assistant turns as content-parts arrays (LangChain, LiteLLM, OpenAI SDK wrappers), reasoning is dropped and reasoning-only turns are deleted. Hold until [PR #19384](https://github.com/ollama/ollama/pull/19384) merges, or normalize to string content.
- **Harden OpenAI-compat response parsing.** Accept `null` for list fields (`/v1/models` `data`, embeddings `data`) rather than assuming `[]`.
- **Avoid MLX `qwen3.8` for tool-using agents** until #19353 is resolved; the failure is silent (no tool call, no error) and will loop your agent.
- **Audio is not yet a first-class native API surface.** Route audio through the `images` field today; there's no documented `audio` param for `/api/chat`.
- **Benchmark spec decoding per-request** once `draft_num_predict=0` lands — useful for A/B on MLX without a server restart.
- **Capacity planning:** keep an eye on #19284 and #19262 together; both affect whether your declared concurrency and memory budget are actually honored.

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM Digest — 2026-10-30

Source: [github.com/BerriAI/litellm](https://github.com/BerriAI/litellm)

## 1. Today's Highlights

LiteLLM published a new release candidate (`v1.108.0-rc.1`) alongside stable patches `v1.106.6` and `v1.105.7`, all continuing the cosign-signed Docker image policy. The two most consequential changes in flight are breaking-behavior fixes in Anthropic translation — Claude **server-side** tools were being returned as client `tool_calls`, breaking the OpenAI Agents SDK and LangGraph ([#48385](https://github.com/BerriAI/litellm/pull/48385)) — and a guardrail correction where Lakera v2 `on_flagged: block` silently passed PII-only detections ([#48944](https://github.com/BerriAI/litellm/pull/48944)). Spend accounting dominated the issue tracker: streaming and non-streaming traffic through OpenAI-compatible upstreams is still landing at `$0` in `LiteLLM_SpendLogs` in multiple reported paths, which directly undermines budget enforcement.

## 2. Releases & Breaking Changes

- **`v1.108.0-rc.1`** — release candidate. Docker images signed with cosign; verification key introduced in commit [`e82a3c6`](https://github.com/BerriAI/litellm/commit/e82a3c646908ba0a6ee0beddc4310d7a6cac4065). → [release](https://github.com/BerriAI/litellm/releases/tag/v1.108.0-rc.1)
- **`v1.106.6`** — stable patch on the 1.106 line, same signing key. → [release](https://github.com/BerriAI/litellm/releases/tag/v1.106.6)
- **`v1.105.7`** — stable patch on the 1.105 line, same signing key. → [release](https://github.com/BerriAI/litellm/releases/tag/v1.105.7)

Note: the published release bodies for all three contain only the image-signature verification boilerplate — no changelog or migration notes were included, so the diff surface for these tags is not documented at source.

**Breaking-behavior changes in open PRs** (marked `!` by authors):
- `fix(anthropic)!` — chat completions will list **only client tools** in `tool_calls`; Claude server tools (web search, web fetch, tool search, code execution) are no longer surfaced as client-executable tool calls. Any agent that branched on `tool_calls` to route server-side tools will change behavior. → [#48385](https://github.com/BerriAI/litellm/pull/48385)
- `fix(guardrails)!` — Lakera v2 with `on_flagged: block` now blocks **every** detection, including PII-only. The previous mask-and-allow behavior is preserved behind a new `on_flagged: mask` mode. Default-config users will start seeing 400s they did not see before. → [#48944](https://github.com/BerriAI/litellm/pull/48944)
- `feat(realtime)!` — new translation routes and streamed transcription on OpenAI/Azure with audio-second billing. → [#35600](https://github.com/BerriAI/litellm/pull/35600)
- `feat(dashscope)` — image-edits billing semantics change for **all** providers: `/v1/images/edits` now bills a deployment's own image price. → [#48998](https://github.com/BerriAI/litellm/pull/48998)

## 3. New Model & Hardware Support

- **DashScope image edits + TTS** — `/v1/images/edits` (previously 500) and `/v1/audio/speech` (previously 404) for DashScope models. → [#48998](https://github.com/BerriAI/litellm/pull/48998)
- **OpenAI realtime translation & streamed `gpt-transcribe`** on OpenAI and Azure, with WebSocket translation sessions billed by seconds of audio sent. → [#35600](https://github.com/BerriAI/litellm/pull/35600)
- **Azure AI Foundry Agents v2** — Responses API with `agent_reference` (agents addressed by name + version) instead of deprecated Assistants primitives. Issue closed. → [#25372](https://github.com/BerriAI/litellm/issues/25372)
- **`nokeep`** — OpenAI-compatible provider with zero data retention; three models with cost/limit/capability entries only (no provider-specific Python code path). → [#49111](https://github.com/BerriAI/litellm/pull/49111)
- **CLF AI Gateway** — OpenAI-compatible gateway for open-weight models, ten models added to the cost map. → [#39324](https://github.com/BerriAI/litellm/pull/39324)
- **Soniox real-time streaming STT (`stt-rt-v5`)** — feature request open for WebSocket transcription through the proxy; not yet supported. → [#43677](https://github.com/BerriAI/litellm/issues/43677)

## 4. Performance & Optimization

- **Least-busy routing burst collapse** — concurrent requests all read the same in-flight counters, so a burst funnels to the first deployment while peers idle. The fix reserves the picked deployment at selection time so the next request observes it as busy (with reservation expiry for requests that never arrive). → [#47484](https://github.com/BerriAI/litellm/pull/47484)
- **PDF token pricing corrected for OpenAI/Azure** — a one-page *text* PDF was priced as a 1664-token Claude page image on an Azure GPT deployment that actually bills 141 tokens; budget checks were refusing requests that fit. Also covers GPT deployments behind another gateway's prefix. → [#47554](https://github.com/BerriAI/litellm/pull/47554)
- **TPM reservation double-counting for Responses API images** — base64 image payloads nested under `custom_tool_call_output.output[]` were serialized with `str(item)` and counted as text, doubling the reservation estimate on Proxy 1.101.0. Closed. → [#47814](https://github.com/BerriAI/litellm/issues/47814)
- **Event-loop client cache keyed by `id(loop)`** — CPython reuses loop addresses after collection, causing cached async clients to be handed to the wrong loop and closed prematurely. Now keyed by a per-loop token; sync clients cached once across loops. → [#48877](https://github.com/BerriAI/litellm/pull/48877)
- **Startup latency / air-gap** — since `v1.92.0` the proxy downloads Prisma binaries at startup and fails with no egress. Still open. → [#33167](https://github.com/BerriAI/litellm/issues/33167)

## 5. Stability & Regressions

Ranked by severity for proxy operators:

1. **Streaming spend logs at `$0`** — streamed `/v1/chat/completions` through OpenAI-compatible upstreams is recorded with `spend = 0` and `cost_breakdown.input_cost = 0.0` when the upstream reports `usage.cost: 0`; spend and budgets read zero for all such streaming traffic. Open. → [#48937](https://github.com/BerriAI/litellm/issues/48937)
2. **Non-streaming `usage.cost` ignored** — same class of bug for `custom_llm_provider: openai` upstreams, `response_cost = 0` on non-streaming calls. Closed. → [#47533](https://github.com/BerriAI/litellm/issues/47533)
3. **Phantom spend from unvalidated `usage.cost`** — provider-reported cost trusted verbatim as USD with no unit check; a non-dollar value produced astronomical spend. Closed. → [#35829](https://github.com/BerriAI/litellm/issues/35829)
4. **Claude server tools surfaced as client `tool_calls`** — OpenAI Agents SDK fails on a tool it doesn't own; LangGraph agents run a stub and report search failure. Fix PR open. → [#48385](https://github.com/BerriAI/litellm/pull/48385)
5. **Claude tool calling broken with OpenRouter/Vertex backends** — longstanding open report, 6 comments, no fix PR linked. → [#19858](https://github.com/BerriAI/litellm/issues/19858)
6. **`print_verbose` leaks API keys to stdout** — when `set_verbose=True`, verbose helpers print dict-shaped diagnostics raw, including `api_key`, with no redaction or control-char sanitization. Open, security-tagged. → [#34705](https://github.com/BerriAI/litellm/issues/34705)
7. **Presidio `logging_only` unmasked prompts on failed calls** — masking only ran on success, so failed requests sent raw names and emails to Langfuse and every other logger. Fix PR open. → [#49057](https://github.com/BerriAI/litellm/pull/49057)
8. **Lakera v2 `on_flagged: block` let PII through** — a flagged card number never produced a 400 under the default config. Fix closed/merged. → [#48944](https://github.com/BerriAI/litellm/pull/48944)
9. **Team-key spend polluting user budgets** — with `apply_user_budget_to_team_keys` unset, team-key usage was exempt from the user budget *check* but still fed the user budget *measurement* via Redis/in-memory counters, cache, and DB rows. Fix PR open. → [#49110](https://github.com/BerriAI/litellm/pull/49110)
10. **In-memory spend buffers dropped on shutdown** — `update_spend` and `update_daily_tag_spend` are APScheduler-driven in-memory buffers silently lost on proxy stop. Open. → [#34805](https://github.com/BerriAI/litellm/issues/34805)
11. **`provider_budget_config` never resets without Redis** — `budget_reset_at` reported ~57 years in the future, so monthly provider budgets effectively never reset. Open. → [#37261](https://github.com/BerriAI/litellm/issues/37261)
12. **`model_max_budget` for end-users not enforced** — per-model budget on customers via `/budget/new` not honored. Closed. → [#31842](https://github.com/BerriAI/litellm/issues/31842)
13. **`/cursor/chat/completions` unlogged** — returns 200 and the provider is charged, but no SpendLogs/Logs UI entry is created (1.88.1). Open. → [#30126](https://github.com/BerriAI/litellm/issues/30126)
14. **Credential edit overwrites real secrets** — `/credentials` returns masked `credential_values` and the dashboard modal pre-populates them, so saving replaces the live secret with a placeholder. Closed. → [#28906](https://github.com/BerriAI/litellm/issues/28906)
15. **`litellm.responses()` loses proxy error bodies** — rejected requests (e.g. guardrail blocks) raise `BadRequestError` with `e.body`, `e.code`, `e.type` all `None`, unlike `litellm.completion()`. Fix PR open. → [#49073](https://github.com/BerriAI/litellm/pull/49073)
16. **Proxy `--num_workers > 1` child process death** — startup failure upgrading 1.78.0 → 1.80.8, worked around by dropping to one worker. Closed. → [#18457](https://github.com/BerriAI/litellm/issues/18457)
17. **Claude empty-content sanitization leak** — `[System: Empty message content sanitised to satisfy protocol]` returned as model output. Closed, 12 comments (highest-traffic issue of the window). → [#24498](https://github.com/BerriAI/litellm/issues/24498)
18. **Bedrock audio transcription HTTP 400** — system messages incompatible with audio blocks on `/v1/audio/transcriptions`. Closed. → [#41544](https://github.com/BerriAI/litellm/issues/41544)

Also landed: synchronous response cost is now finalized once before headers are sent, so response headers, spend records, and budget counters agree, and completed provider usage survives failed post-call hooks and cancellation ([#48993](https://github.com/BerriAI/litellm/pull/48993)); `drop_params` now emits a WARNING naming param, value, model and reason instead of silently discarding a requested reasoning level ([#48933](https://github.com/BerriAI/litellm/pull/48933)).

## 6. What This Means for Application Developers

- **Don't trust proxy-side budgets for OpenAI-compatible upstreams yet.** If your upstream returns `usage.cost`, streaming traffic is logged at `$0` ([#48937](https://github.com/BerriAI/litellm/issues/48937)) and non-streaming was until recently ([#47533](https://github.com/BerriAI/litellm/issues/47533)). Enforce spend limits downstream or on provider-side quotas until these are patched.
- **Audit agent integrations before upgrading past the Anthropic fix.** Server tools no longer appear as client `tool_calls` ([#48385](https://github.com/BerriAI/litellm/pull/48385)). If you use OpenAI Agents SDK or LangGraph with Claude web search/fetch/code-execution, verify your tool-dispatch branch — the failure mode was a hard error in the SDK and a silently-wrong stub in LangGraph.
- **Re-check guardrail configs.** Lakera v2 default (`on_flagged: block`) was failing open on PII-only detections; the fix makes it fail closed. If that breaks a workflow, opt into the new `mask` mode explicitly rather than relying on the old implicit behavior ([#48944](https://github.com/BerriAI/litellm/pull/48944)).
- **Token-counting drift can reject valid requests.** PDF inputs on OpenAI/Azure deployments were over-counted by ~12x (1664 vs 141 tokens) ([#47554](https://github.com/BerriAI/litellm/pull/47554)), and base64 images in Responses API tool outputs could double the TPM reservation ([#47814](https://github.com/BerriAI/litellm/issues/47814)). If you saw unexplained 429s on document or image workloads, this is the likely cause.
- **Team-key accounting over-counts toward user budgets** unless `apply_user_budget_to_team_keys` is explicitly set ([#49110](https://github.com/BerriAI/litellm/pull/49110)). Worth an explicit setting in `general_settings` rather than relying on the default.
- **Air-gapped and multi-worker deployments remain sharp edges.** Prisma binary downloads at startup ([#33167](https://github.com/BerriAI/litellm/issues/33167)) and `--num_workers > 1` startup failures ([#18457](https://github.com/BerriAI/litellm/issues/18457)) both recur in the tracker; test these in staging, not production.
- **Version guidance:** `v1.108.0-rc.1` is a candidate with no published changelog — treat as pre-release. `v1.106.6` and `v1.105.7` are the current stable patch picks; both ship the same cosign-signed images, so signature verification pinned to commit `e82a3c6` continues to work across all three.

</details>

<details>
<summary><strong>Unsloth</strong> — <a href="https://github.com/unslothai/unsloth">unslothai/unsloth</a></summary>

# Unsloth Digest — 2026-10-30

## Today's Highlights
No tagged release landed in the last 24h, but Studio/Desktop saw a heavy merge-and-fix day: the T4 NF4 decode path was retuned for batch‑4 (+13–30% on `gemm_4bit`), batched MoE LoRA training was reworked into a single grouped GEMM pass ([#16012](https://github.com/unslothai/unsloth/pull/16012)), and several high-impact Studio correctness bugs got fix PRs (context compaction, MLX memory estimation, `/v1/models` discovery). Two silent training-data-loss reports around Alpaca/completion-only masking ([#15894](https://github.com/unslothai/unsloth/issues/15894)/[#15895](https://github.com/unslothai/unsloth/issues/15895)) are the most serious open items and have no linked fix yet.

## Releases & Breaking Changes
None. No new versions, no announced API/config migrations in the last 24h. Current beta line in the field is `v0.1.912-beta` (referenced across several issue reports).

## New Model & Hardware Support
- **LFM3 family (1.7B)** — feature request open with 10 👍; LiquidAI's new backbone not yet supported ([#15588](https://github.com/unslothai/unsloth/issues/15588)). LFM3 **MLX** checkpoints currently fail to appear in `GET /v1/models` and can't be auto-switched ([#15832](https://github.com/unslothai/unsloth/issues/15832)) — fix PR [#15945](https://github.com/unslothai/unsloth/pull/15945) resolves it via the local model resolver's `auto_map` gating.
- **LFM3‑Audio / LFM3‑Omni on MLX** — landed in #15889; follow-up repair to the audio-input heal gate in [#16023](https://github.com/unslothai/unsloth/pull/16023) (fixes red CI on main).
- **Apple MLX Neural Engine prefill** — new opt-in toggle splitting dense SwiGLU MLP prefill between ANE and GPU, mirroring the existing Int8 Prefill switch ([#15954](https://github.com/unslothai/unsloth/pull/15954)).
- **Multi-GPU audio model loading** — automatic native audio loads now pin to a single GPU instead of refusing a pooled device pick ([#16022](https://github.com/unslothai/unsloth/pull/16022)).
- **AMD iGPU handling** — integrated Radeon (shared system RAM) excluded from the Train page VRAM total and default GPU pick; unblocks dual‑R9700 setups that previously showed `VRAM 100 GiB` for 64 GiB of real VRAM ([#14039](https://github.com/unslothai/unsloth/pull/14039)).
- **Vulkan backend** — MiniCPM‑V‑4.7‑1B text generation failure closed ([#14987](https://github.com/unslothai/unsloth/issues/14987)).
- **NVFP4 on Apple Silicon** — MiniMax‑M3.1 GGUF no longer falls back to CPU when all 61/61 layers are offloaded (closed) ([#15409](https://github.com/unslothai/unsloth/issues/15409)).

## Performance & Optimization
- **T4 NF4 decode crossover moved from batch 5 → batch 4** — batches 2–4 now hand off to bitsandbytes' fused `gemm_4bit` instead of the Triton GEMV‑rows kernel; measured **13–30% faster at batch 4** on Colab T4 ([#15988](https://github.com/unslothai/unsloth/pull/15988), closed/merged).
- **Batched MoE LoRA training** — every adapter's expert LoRA now runs in one grouped GEMM pass rather than re-running fused experts once per adapter (Qwen3 MoE, Qwen3.5/3.6‑MoE incl. Qwen3.6‑35B‑A3B) — directly targets queued multi-job Studio training ([#16012](https://github.com/unslothai/unsloth/pull/16012)).
- **Video export stall** — `StreamEncode._matches` was allocating chunk-sized temporaries; exporting a MiniMax‑H3 1344×768×124 clip on A100‑40 went from **115–184 s to ~1–2 s** ([#16024](https://github.com/unslothai/unsloth/pull/16024)).
- **MLX memory estimation** — estimate now charges the full `[heads, ctx]` score matrix when mlx falls back to unfused full-width (f16) attention, instead of only when the KV cache is quantized ([#16021](https://github.com/unslothai/unsloth/pull/16021)). Expect estimates to go *up*; see regression note below.
- **Context compaction timeout scaling** — token-count timeout now scales with payload so multi-million-token GGUF transcripts can still compact ([#15900](https://github.com/unslothai/unsloth/pull/15900)), plus a byte-count guard on `/apply-template` to avoid 503/500 storms on oversized payloads ([#15857](https://github.com/unslothai/unsloth/pull/15857)).

## Stability & Regressions
Ranked by severity:

1. **Silent training-data loss on Alpaca / completion-only masking (no fix PR yet).** "Train on completions" drops **80%+** of an Alpaca dataset on *any* instruct model: the Alpaca template is never installed, but masking still searches for its markers. Reproduced on two unrelated model families; Windows 11, RTX 5060 8 GiB, `v0.1.911-beta`. Note the report exists twice — [#15894](https://github.com/unslothai/unsloth/issues/15894) (closed) and [#15895](https://github.com/unslothai/unsloth/issues/15895) (still open). Worth verifying whether the close was a dedupe or a real fix.
2. **Single-column datasets unusable.** A JSONL with one `text` column reports `Format: unknown`, AI Assist declines, and Start silently returns to the preview — i.e. the standard SFT shape from Unsloth's own notebooks ([#15892](https://github.com/unslothai/unsloth/issues/15892), closed) and single-column `content` ([#15901](https://github.com/unslothai/unsloth/issues/15901), closed). AI Assist now explains *why* it can't map a no-prompt/response dataset ([#15991](https://github.com/unslothai/unsloth/pull/15991)).
3. **Windows + AMD GGUF memory blowup.** `llama-server` holds **~16 GB commit charge** after loading a GGUF even with "Don't reserve system RAM"; the commit limit gets exhausted and the process dies ([#16015](https://github.com/unslothai/unsloth/issues/16015)). No fix PR.
4. **Load regression in 0.1.912-beta.** A model that worked for weeks no longer loads after the desktop update (macOS 15.0.1) ([#15932](https://github.com/unslothai/unsloth/issues/15932)). No fix PR.
5. **Compaction deadlock on long transcripts.** Chats of several million stored tokens can neither auto-compact nor "Compact conversation", making threads non-continuable after a ~2 min stall ([#15800](https://github.com/unslothai/unsloth/issues/15800)); the Anthropic passthrough `/v1/messages` path surfaced the same failure as an unrecoverable 400 `exceed_context_size_error` instead of compacting ([#15417](https://github.com/unslothai/unsloth/issues/15417), closed). Fix PRs: [#15900](https://github.com/unslothai/unsloth/pull/15900), [#15857](https://github.com/unslothai/unsloth/pull/15857).
6. **MLX memory estimator wildly over-reports.** 69.7 GiB estimated for a model that actually loads on a 24 GB Mac ([#15935](https://github.com/unslothai/unsloth/issues/15935)). [#16021](https://github.com/unslothai/unsloth/pull/16021) corrects the *under*-counting of the score matrix; the over-report in #15935 is the opposite direction and needs separate attention.
7. **MLX UI rendering/listing gaps.** Dolphin Venice Edition via MLX renders incorrectly in the Studio UI while working in other apps ([#15858](https://github.com/unslothai/unsloth/issues/15858)); LFM3 MLX models missing from `/v1/models` ([#15832](https://github.com/unslothai/unsloth/issues/15832), fix #[15945](https://github.com/unslothai/unsloth/pull/15945)).
8. **ModelScope 50 GB cap.** Files >50 GB blocked when ModelScope is the model source ([#15989](https://github.com/unslothai/unsloth/issues/15989)).
9. **AppImage UI lag** on Unsloth Studio ([#15999](https://github.com/unslothai/unsloth/issues/15999)).
10. **CLI task-name collision** — eval dataset task names collide with later YAML tasks depending on `--tasks` ordering (upstream `4a87de122`, Python 3.12) ([#15982](https://github.com/unslothai/unsloth/issues/15982)).
11. **Studio sandbox correctness** — rewind restored all files *except* edits inside dot folders (`.github/`, `.vscode/`, `.devcontainer/`) ([#16017](https://github.com/unslothai/unsloth/pull/16017)); a second sandboxed `pip install` silently lost modules because `--target` skips existing top-level dirs ([#16018](https://github.com/unslothai/unsloth/pull/16018)).

## What This Means for Application Developers
- **Never assume masked-SFT actually masked.** If you're fine-tuning with "train on completions" over Alpaca-shaped data, audit your dataset row counts before/after preprocessing — 80% of samples may be silently discarded. Until #15895 is resolved, prefer explicit prompt/completion columns or a chat template.
- **OpenAI-compatible discovery is being hardened.** `GET /v1/models` now lists locally downloaded `auto_map` safetensors/MLX checkpoints ([#15945](https://github.com/unslothai/unsloth/pull/15945)), and `/v1/audio/speech` finally honors the `speed` parameter for built-in voices rather than silently returning 1.0× ([#16020](https://github.com/unslothai/unsloth/pull/16020)). If you gate on model listing, re-test after upgrading.
- **Long-running agents get relief.** The compaction timeout scaling and `/apply-template` payload guard ([#15900](https://github.com/unslothai/unsloth/pull/15900), [#15857](https://github.com/unslothai/unsloth/pull/15857)) target the class of failures where a multi-million-token thread becomes permanently stuck — but the changes are open, not merged.
- **Resilience work for agentic retrieval:** Deep Research now recovers from provider `structured_output_failed` JSON rejections by resuming the same decision point ([#15788](https://github.com/unslothai/unsloth/pull/15788)), and attached documents are no longer truncated out of the report budget ([#16019](https://github.com/unslothai/unsloth/pull/16019)).
- **Multi-tenant LoRA serving/training is getting cheaper per job** — the grouped-GEMM MoE path ([#16012](https://github.com/unslothai/unsloth/pull/16012)) matters if you queue many adapters against one MoE base.
- **Capacity planning on Apple:** treat MLX VRAM estimates in Studio as unreliable in both directions right now (#15935 over-reports, #16021 raises the estimate for unfused prefill) and validate against actual load.

</details>