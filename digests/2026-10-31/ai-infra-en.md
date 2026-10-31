# AI Infrastructure Digest 2026-10-31

> Generated: 2026-10-31 00:15 UTC | Projects covered: 6

- [vLLM](https://github.com/vllm-project/vllm)
- [SGLang](https://github.com/sgl-project/sglang)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [Ollama](https://github.com/ollama/ollama)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Unsloth](https://github.com/unslothai/unsloth)

---

## Cross-Project Comparison

# Cross-Project AI Infrastructure Comparison — 2026-10-31

## 1. Ecosystem Overview

Today’s AI infrastructure activity is predominantly hardening rather than expansion: no major new frontier architecture was merged, and the highest-severity items are silent correctness failures, memory/KV accounting, and API-contract breaks. Datacenter serving engines **vLLM** and **SGLang** are concentrating on frontier MoE paths — Kimi-K3, DeepSeek-V4.1, MiniMax — plus Blackwell/ROCm backends. Local runtimes **llama.cpp** and **Ollama** are pushing low-bit quantization, MLX, and heterogeneous device coverage. Gateways and fine-tuning stacks **LiteLLM** and **Unsloth** are absorbing production concerns: billing accuracy, Anthropic/OpenAI compatibility, install isolation, and quantization workflows. Release cadence is uneven — llama.cpp shipped multiple builds and Unsloth/LiteLLM cut beta/dev artifacts, while vLLM, SGLang, and Ollama shipped no releases.

## 2. Activity Comparison

| Project | Layer | Issues (24h updated) | PRs (24h updated) | Release status |
|---|---|---:|---:|---|
| **vLLM** | Serving engine | n/r | n/r | No releases/tags; no API removals landed |
| **SGLang** | Serving engine | n/r | n/r | No tags/images; FlashInfer dependency bump in flight |
| **llama.cpp** | Local runtime | **51** updated; digest lists top 30 | **125** updated; digest lists top 20 | **b12002–b12017** shipped |
| **Ollama** | Local runtime + cloud | n/r | n/r | No releases |
| **LiteLLM** | Gateway | **112** | **472** | **v1.109.0-dev.2** dev pre-release |
| **Unsloth** | Fine-tuning / Studio | n/r | n/r | **v0.1.913-beta** |

*Note: n/r = not reported in the supplied digest. Counts are 24h “updated” figures where explicitly disclosed; they are not total open issues/PRs and are not directly comparable across projects. llama.cpp’s feed is explicitly partial: top 30 of 51 updated issues and top 20 of 125 updated PRs.*

**Read-through:** LiteLLM shows the highest explicitly reported churn by a wide margin, consistent with gateway-layer cost-accounting and compatibility work. llama.cpp has the highest release cadence today. vLLM and SGLang show heavy engineering activity but intentionally shipped no releases. Ollama is quiet on releases but carries a critical cloud-endpoint issue. Unsloth shipped a beta but has an incident-level install-isolation regression.

## 3. Model Support Race

| Project | New / expanded model or hardware support today | Assessment |
|---|---|---|
| **vLLM** | No new architectures merged; Mistral Large 4 Responses fixes; Kimi-K3 stability/JIT; MiniMax-M3 ROCm DSpark; DeepSeek-V4.1 DSpark fused sampling; Blackwell MXFP8; MI355X/MI300X tuning; CPU DP×TP fix | **Frontier-model hardening and accelerator breadth**, not new-model breadth |
| **SGLang** | MiniMax-M3.1-Flash tracking + DFlash2 draft; DSV4 native H16 CuTe sparse prefill; B200/SM100 fused projection; MXFP8 KV in HiCache; AMD RDNA3/4 CI; rust-server multimodal image preprocessing | **Frontier MoE depth plus Blackwell/AMD specialization** |
| **llama.cpp** | OpenCL q2_0; IQ3 in review; Hexagon improvements; WASM relaxed SIMD; TML Inkling, PocketTTS, LFM3-Audio; Gemma 4 and Qwen3.8-Flash perf work | **Broadest local architecture/backend coverage and low-bit reach** |
| **Ollama** | AutoTrust MLX decision models; Intel Mac macOS 12 support; per-model thinking metadata; multimodal input validation | **Local UX, MLX, and API-shim compatibility** |
| **LiteLLM** | Databricks Gemini 3.5–3.8 audio/video capability flags; Gemini image batch pricing; provider onboarding fixes | **Gateway metadata/pricing, not runtime model support** |
| **Unsloth** | DeepSeek-V4.1-Flash-1017 GGUF; LFM3-Omni audio; LFM3-Audio-2B; integrated-GPU int8 path; MLX fixes | **Fine-tuning, GGUF export, and audio-model enablement** |

**Who is ahead:** There is no single leader — leadership is layer-specific. **vLLM** and **SGLang** lead datacenter frontier-model serving, with vLLM doing more Kimi-K3 correctness triage and SGLang showing more explicit new-model tracking plus DSV4 sparse-prefill work. **llama.cpp** leads breadth across local architectures, low-bit quantization, and non-NVIDIA backends. **Unsloth** leads open-model fine-tuning/GGUF enablement. **LiteLLM** leads provider abstraction and pricing metadata. **Ollama** leads packaged local/MLX UX but trails frontier serving.

## 4. Performance Frontier

| Optimization area | Evidence today | Implication |
|---|---|---|
| **KV cache & memory accounting** | vLLM #64460: KV-pool-saturated admission retries inflate decode TPOT **~2.3×**; SGLang MXFP8 KV in HiCache and Mamba HiCache work; llama.cpp keeps KV rotation constants resident and adds native quantized KV; Ollama per-layer KV sizing and MLX pre-flight gap; Unsloth memory-estimator inaccuracies | KV accounting — not raw FLOPS — is the dominant scaling and p99 constraint |
| **Scheduling / batching / routing** | vLLM admission-backoff request; SGLang scheduler decoupling RFC; LiteLLM Rust router and logging hot-path optimization; llama.cpp MoE expert cache `ClassLRU`; Ollama MLX scheduler fixes | Tail latency and cost-aware routing are active across serving, runtime, and gateway layers |
| **Kernels / JIT / cold start** | vLLM: ~**1.5 s** TTFT from residual Triton sampling kernels, **130 µs** MI355X idle before RCCL; SGLang: DeepGEMM fast warmup cuts DSV4.1 cold start from **~30 min to <3 min**; llama.cpp OpenCL/Hexagon/WASM kernels; Unsloth flex→SDPA split | Serverless/autoscaling economics depend heavily on warmup and kernel-cache behavior |
| **Quantization / low-bit** | vLLM Blackwell MXFP8; SGLang MXFP8 KV and MXFP4 MoE; llama.cpp OpenCL q2_0/IQ3 and q4/q8 KV; Unsloth int8 host offload and GGUF; Ollama nvfp4 MLX | Low-bit is expanding hardware reach; numeric validation per backend remains mandatory |
| **Distributed serving** | vLLM TP/PP/PD, Mooncake TP-rank stall; SGLang DP attention, EP, elastic-EP collectives, EAGLE+DP+FlashInfer crash; llama.cpp RPC/multi-device; LiteLLM multi-deployment routing | Rank-level correctness and feature interactions are now the weak spots, not single-feature throughput |

**Takeaway:** Optimization effort is shifting from headline throughput to **tail latency, memory correctness, cold-start cost, and rank-level reliability**. The most production-relevant numbers today are vLLM’s 2.3× TPOT inflation under KV pressure and SGLang’s ~27-minute DeepGEMM warmup reduction.

## 5. Layer Positioning

| Layer | Projects | Primary role | Current pain |
|---|---|---|---|
| **Datacenter serving engine** | **vLLM**, **SGLang** | High-throughput GPU/accelerator inference, frontier MoE, TP/PP/PD, KV cache, CUDA graphs | Silent output corruption, TP-rank stalls, KV-pressure latency, multi-feature crashes |
| **Local / edge runtime** | **llama.cpp**, **Ollama** | GGUF/MLX execution, desktop/edge/on-prem deployment, low-bit quantization, heterogeneous backends | Backend stability, memory accounting, prefix-cache invalidation, cloud endpoint reliability |
| **LLM gateway / proxy** | **LiteLLM** | Multi-provider routing, budgets, API translation, observability, cost attribution | Billing correctness, Anthropic/OpenAI compatibility, health-check cost leakage, Python-version support |
| **Fine-tuning / Studio** | **Unsloth** | LoRA/QLoRA, GGUF export, training workflows, local Studio | Install isolation, memory estimation, kernel correctness, update reliability |

**Overlap note:** vLLM and SGLang compete at the serving-engine layer; llama.cpp and Ollama overlap in local runtime but differ in abstraction level — llama.cpp is the low-level ggml runtime, Ollama is the packaged local/cloud experience. LiteLLM and Unsloth are not serving engines; they respectively control access/cost and model adaptation.

## 6. Trend Signals

- **Correctness is the new feature gate.** The highest-severity items are silent or hard-to-detect: vLLM Kimi-K3 `!!!!` token streams (#64758), SGLang DSV4.1 OOM loops (#43486) and rust-server routing defects, llama.cpp Gemma 4 + MTP illegal memory access (#31077), Ollama Cloud returning no HTTP response (#19111), and Unsloth’s isolated-install overwrite (#16186). Throughput gains matter only after these are gated.

- **KV cache and memory accounting are the main scaling bottleneck.** vLLM’s KV-saturation TPOT inflation, SGLang’s OOM at 29% KV utilization, Ollama’s 262k-context MLX booking discrepancy, and llama.cpp’s quantized-KV work all point to the same issue: allocator behavior and scheduler estimates diverge from real memory pressure.

- **Cold start and JIT warmup are product decisions.** SGLang’s `SGLANG_JIT_DEEPGEMM_FAST_WARMUP` report — ~30 min to under 3 min — is the clearest serverless/autoscaling lever in today’s digest. vLLM’s residual ~1.5 s TTFT from sampling kernels shows the same problem at smaller scale.

- **API compatibility remains a production blocker, especially around agents.** Tool-call parsing, Anthropic `x-api-key`, thinking-block replay, `raw_logprobs` under structured output, `stop_regex` trimming, and LiteLLM budget-window accounting are all active defects. Agent frameworks should validate outputs and pin versions rather than assume drop-in compatibility.

- **Feature interactions require explicit pinning.** EAGLE + DP attention + FlashInfer A2A + prefill CUDA graph; DSPARK + DSV4.1-Flash sustained decode; Gemma 4 + MTP; and torch 2.8/2.9 flex-attention causal-mask loss are interaction bugs, not single-feature failures. Test the exact combination you deploy.

- **Heterogeneous hardware and low-bit continue to expand.** Blackwell MXFP8, ROCm MI3xx/MI350X, AMD RDNA3/4, Intel SYCL/Vulkan, Apple MLX, and ARM all appear in today’s work. Validate numerics per backend; do not assume parity with CUDA.

**What agent/application developers should watch:** add degenerate-output guards for Kimi-K3; enforce tool-name allowlists; treat `raw_logprobs` as post-grammar-mask until fixed; keep warmup probes in deploy health checks; size concurrency for worst-case KV-pressure TPOT; do not treat LiteLLM windowed budgets as a hard cap yet; audit billed media health checks; and pin Unsloth installs until the `UNSLOTH_STUDIO_HOME` isolation regression is resolved.

---

## Per-Project Reports

<details>
<summary><strong>vLLM</strong> — <a href="https://github.com/vllm-project/vllm">vllm-project/vllm</a></summary>

# vLLM Digest — 2026-10-31

## 1. Today's Highlights

No releases landed in the last 24 hours, but the day's activity was dominated by correctness work on frontier-model paths: two separate Kimi-K3 failure modes (silent NaN-driven `!` token streams and a stalled TP rank in MooncakeStoreConnector) were filed and are being triaged against FlashKDA/FlashMLA and the KV connector respectively. Alongside that, the direct-weight-reload effort for RL training (#54477 RFC) advanced across four loader PRs, and a scheduler-level report quantified a ~2.3× decode TPOT inflation when KV-pool-saturated requests retry admission. CI/infra churn (automatic sharding rollout) and Scribe-style maintenance PRs round out the diff.

## 2. Releases & Breaking Changes

No new releases or tags in the last 24h. No API/config removals landed.

One config surface is expanding rather than breaking — PR [#64815](https://github.com/vllm-project/vllm/pull/64815) adds `KernelConfig.mxfp8_cublaslt_min_m` (default `128`, `null` disables) to control MXFP8 cuBLASLt dispatch on Blackwell.

Two PRs are staged but explicitly parked and should not be treated as imminent default behavior changes: [#64796](https://github.com/vllm-project/vllm/pull/64796) (automatic CI sharding on by default) and [#64795](https://github.com/vllm-project/vllm/pull/64795).

## 3. New Model & Hardware Support

No new model architectures merged today. Model-specific work was bug-fix and perf-tuning in nature:

- **Mistral Large 4** (`--tokenizer-mode mistral`) Responses API compatibility is broken on two request shapes; a fix for the `developer` role is already in review — [#64793](https://github.com/vllm-project/vllm/issues/64793), [#64789](https://github.com/vllm-project/vllm/issues/64789).
- **Kimi-K3** received the bulk of attention, both as a stability target and via JIT/gap-closing work — [#64824](https://github.com/vllm-project/vllm/issues/64824).
- **MiniMax-M3** on ROCm: adaptive DSpark verification enablement continues in review — [#56451](https://github.com/vllm-project/vllm/pull/56451).
- **Hardware:** Blackwell MXFP8 GEMM routing to cuBLASLt ([#64815](https://github.com/vllm-project/vllm/pull/64815)); ROCm MI355X scratch-allocation tuning ([#64791](https://github.com/vllm-project/vllm/issues/64791)); CPU DP×TP startup fix when assigned NUMA nodes are absent ([#64499](https://github.com/vllm-project/vllm/pull/64499)).

## 4. Performance & Optimization

**Scheduler / batching**
- **KV-pool-saturated admission retries inflate decode TPOT ~2.3×** on a P/D-disaggregated Ascend deployment (TP8, ~32k-token KV pool). The mechanism is described as platform-independent in the V1 scheduler; the request is for automatic admission backoff — [#64460](https://github.com/vllm-project/vllm/issues/64460). This is the most actionable throughput finding of the day for anyone running tight KV budgets.

**Kernel / runtime JIT**
- **Silent runtime JIT compilation** remains the headline ops problem: users cannot tell whether a kernel cache was missed, and DeepGEMM warmup gaps persist — tracking issue [#49349](https://github.com/vllm-project/vllm/issues/49349) and follow-up [#64824](https://github.com/vllm-project/vllm/issues/64824).
- **CPU + Model Runner V2:** 1–3 Triton sampling kernels still compile inside first requests, adding **~1.5 s to TTFT** for a fixed count of requests per server start — warmup PR [#64522](https://github.com/vllm-project/vllm/pull/64522).

**GPU kernels & memory**
- **MI355X:** ~**130 µs** of GPU idle before certain RCCL all-reduces in prefill/mixed steps due to per-dispatch scratch allocation; fix is setting `HSA_SCRATCH_SINGLE_LIMIT` in the ROCm image — [#64791](https://github.com/vllm-project/vllm/issues/64791).
- **MI300X:** DSA candidate-block scores and sampler fp32 logits are reallocated each step and outgrow allocator blocks; PR moves both to persistent buffers — [#63719](https://github.com/vllm-project/vllm/pull/63719).
- **DeepSeek-V4.1 DSpark:** sequential Markov sampling fused on NVIDIA via two Triton kernels + inverse CDF — [#64442](https://github.com/vllm-project/vllm/pull/64442).
- **Blackwell MXFP8:** large-M linear GEMMs routed to cuBLASLt through `torch._scaled_mm` while reusing existing 128x4-swizzled scales — [#64815](https://github.com/vllm-project/vllm/pull/64815).
- **V2 runner PP:** non-last pipeline stages now send from a preallocated buffer instead of live CUDA-graph outputs, removing a read/overwrite hazard — [#64755](https://github.com/vllm-project/vllm/pull/64755).
- **MoRIIO READ mode:** RFC to recover full CUDA graphs (currently forced to piecewise) via async KV-load gating — [#49643](https://github.com/vllm-project/vllm/issues/49643).

**Weight loading / RL**
- Direct weight reload for RL (RFC [#54477](https://github.com/vllm-project/vllm/issues/54477)) is progressing: live-model checkpoint writes ([#64336](https://github.com/vllm-project/vllm/pull/64336)), in-place refill of weight-derived tensors so captured CUDA graphs stay valid ([#64692](https://github.com/vllm-project/vllm/pull/64692)), MoE expert padding fill moved out of the loader ([#64352](https://github.com/vllm-project/vllm/pull/64352)), and one `weight_loader` call per fused shard ([#64620](https://github.com/vllm-project/vllm/pull/64620)). Rev 2 of the RFC notes Rev 1's "skip post-load processing" approach caused **silent errors** (stale MLA absorbed weights), which is why the design changed.

## 5. Stability & Regressions

Ranked by severity.

**Critical — silent output corruption / hangs**
1. **Kimi-K3 emits `!!!!` (token 0) streams under load.** A single request's activations go NaN for one step; FlashKDA spreads it across requests. Leading suspect is an unproven race in FlashMLA's SM90 decode kernel (PDL). Silent, load-dependent, and trivially missed by smoke tests — [#64758](https://github.com/vllm-project/vllm/issues/64758).
2. **MooncakeStoreConnector: one TP rank stalls** (GPU idle, peers spinning) on Kimi-K3 under agentic load. Reproduced across multiple nightlies on B300/EFA — [#64814](https://github.com/vllm-project/vllm/issues/64814).
3. **GLM-5.3 TP8 hangs** during OffloadingConnector CPU↔GPU copies on MI325X SR-IOV VFs when other vLLM processes share the GPUs; generation drops to zero with requests still running — [#64549](https://github.com/vllm-project/vllm/issues/64549).

**High — broken API contracts**
4. **Tool calling:** guidance backend rejects tool-calling structural tags (`KeyError: 'triggers'`), breaking strict/required/named `tool_choice` at request-validation time — [#55152](https://github.com/vllm-project/vllm/issues/55152).
5. **Qwen3 tool-call parser promotes quoted model markup into real tool calls**, including names outside `request.tools` and duplicates — [#58147](https://github.com/vllm-project/vllm/issues/58147). Treat as a prompt-injection surface for agent deployments.
6. **Mistral Large 4 Responses API:** `input_text` content and `developer` role both rejected with `--tokenizer-mode mistral` — [#64789](https://github.com/vllm-project/vllm/issues/64789), [#64793](https://github.com/vllm-project/vllm/issues/64793). Fix PR [#64800](https://github.com/vllm-project/vllm/pull/64800) is up (closed/reopened; verify merge state before relying on it).
7. **`raw_logprobs` computed after the structured-output grammar mask**, so reported raw logprobs are not actually raw — [#64809](https://github.com/vllm-project/vllm/issues/64809); fix PR [#64811](https://github.com/vllm-project/vllm/pull/64811).
8. **Anthropic Messages API rejects `x-api-key`**, only `Authorization: Bearer` works — [#51572](https://github.com/vllm-project/vllm/issues/51572).

**Medium — perf regressions & memory**
9. **EAGLE3 draft acceptance collapses after the first position** with `--block-size > 128` (MiniMax-M3, GB200) — [#64652](https://github.com/vllm-project/vllm/issues/64652).
10. **Gemma-4 MTP halves prefix-cache hits** when `--prefix-cache-retention-interval` is set — [#64808](https://github.com/vllm-project/vllm/issues/64808).
11. **Cold-cache KV OOM** with `--kv-cache-memory-bytes` + `--enable-sleep-mode` — [#62277](https://github.com/vllm-project/vllm/issues/62277).
12. **`fuse_rope_kvcache` breaks EAGLE spec decode on ROCm** when drafter and target attention shapes differ — [#64679](https://github.com/vllm-project/vllm/issues/64679).
13. **ROCm gfx950 (MI350X): `kernel_paged_attention_2d` illegal memory access** under long-context decode — [#48043](https://github.com/vllm-project/vllm/issues/48043).

**Low — packaging / metadata**
14. `vllm/vllm-openai:unlimited-ocr` image cannot serve Unlimited-OCR — [#64489](https://github.com/vllm-project/vllm/issues/64489).
15. Non-streaming `/derender` endpoints report `usage.prompt_tokens: 0` — [#64778](https://github.com/vllm-project/vllm/issues/64778).
16. *Closed today:* Qwen3.5 int32 token-offset overflow in three Triton kernels at large `--max-num-batched-tokens` ([#63759](https://github.com/vllm-project/vllm/issues/63759)); tokenizer/processor snapshot downloading ~1.57 GB of unneeded weights for gpt2 ([#63925](https://github.com/vllm-project/vllm/issues/63925)).

## 6. What This Means for Application Developers

- **Validate tool-call output, don't trust it.** Three independent parser/backend defects (#55152, #58147, #64810) sit on the tool-calling path. If you run strict `tool_choice`, pin a known-good image and assert on tool names against your own allowlist before execution — #58147 means the model can invent calls by quoting markup.
- **Kimi-K3 needs output-level guarding right now.** #64758 produces syntactically valid, token-0-only completions under load. Add a degenerate-output check (repeated `!` runs, low distinct-token ratio) to your gateway rather than waiting for a fix.
- **Anthropic-compat is not drop-in.** `x-api-key` auth (#51572), `developer` roles (#64793), `input_text` content (#64789), and Anthropic-defined tools like `web_search`/`bash` (#64810) are all still gaps. Claude Code–style clients will hit these.
- **Raw logprobs are ambiguous under structured output.** Until #64811 lands, `raw_logprobs` are post-grammar-mask. Any calibration, scoring, or reranking pipeline using them on constrained decoding is measuring the wrong distribution.
- **Budget for KV-pressure latency spikes.** #64460's ~2.3× TPOT inflation is a scheduler behavior, not a hardware limit — size admission concurrency assuming worst-case TPOT, or you'll breach p99 before you hit OOM.
- **Cold-start latency is still not fully solved.** JIT warmup gaps (#64824) and residual CPU sampling-kernel compiles (~1.5 s TTFT, #64522) mean first-requests-after-start remain unreliable; keep a warmup probe in your deploy health check rather than sending user traffic into a cold server.

</details>

<details>
<summary><strong>SGLang</strong> — <a href="https://github.com/sgl-project/sglang">sgl-project/sglang</a></summary>

# SGLang Digest — 2026-10-31

## 1. Today's Highlights
No releases shipped in the last 24h; activity is concentrated on stabilization and backend tuning. The most actionable finding is a report that `SGLANG_JIT_DEEPGEMM_FAST_WARMUP` cuts DeepSeek-V4.1 cold start from ~30 min to under 3 min with no measurable runtime regression at chunked-prefill 16384. Meanwhile a cluster of `rust-server` correctness bugs (DP-rank routing, endpoint advertisement, elastic-EP collectives) surfaced alongside a ~5% GB200 decode regression in Qwen3.8-Flash-Next-FP8 tied to the FP8 TRT-LLM MoE path.

## 2. Releases & Breaking Changes
None. No new tags or images in the last 24h. Note one dependency bump in flight: FlashInfer `0.7.2` → `0.7.2.post1`, which touches the Python pin, both Dockerfiles (`flashinfer-cubin` / `flashinfer-jit-cache`), and the runtime version check in `engine.py` — relevant if you pin images. ([PR #46926](https://github.com/sgl-project/sglang/pull/46926))

## 3. New Model & Hardware Support
- **MiniMax-M3.1-Flash** — new tracking issue for model support, including a DFlash2 draft checkpoint for speculative decoding and a published cookbook. ([Issue #46869](https://github.com/sgl-project/sglang/issues/46869))
- **AMD RDNA3/RDNA4 (gfx1100/gfx1201)** — CI and upstreaming plan proposed for consumer/edge RDNA parts on main; currently no CI coverage. ([Issue #46900](https://github.com/sgl-project/sglang/issues/46900))
- **DeepSeek-V4 native H16 CuTe sparse prefill** — experimental backend adding an H16 (rather than H64-padded) sparse-prefill path via CuTe DSL, targeting TP8 where DSV4 leaves 16 query heads per rank. Gated behind `--dsv4-prefill-...`. ([PR #36059](https://github.com/sgl-project/sglang/pull/36059))
- **B200 / SM100 runtime optimizations** — fused projection/all-gather admitted on SM100 at TP8 for BF16 projections with 4096/8192 output columns and ≤128 token rows. ([PR #47129](https://github.com/sgl-project/sglang/pull/47129))
- **MXFP8 KV cache in HiCache L3** — L3 previously raised `NotImplementedError` for every MXFP8 page; now pages are stored as payload + UE8M0 scales multi-buffer objects. ([PR #46936](https://github.com/sgl-project/sglang/pull/46936))
- **Rust server multimodal (image) preprocessing** via `sglang-processor` / Dynamo `dynamo-multimodal`, targeting bit-identical parity with the Python CPU path. ([PR #46291](https://github.com/sgl-project/sglang/pull/46291))

## 4. Performance & Optimization
- **DeepGEMM fast warmup on DSV4.1** — reported 3–5× faster cold start (30 min → <3 min) with no detectable runtime degradation at chunked-prefill 16384, contradicting the flag's documented "might cause performance degradation" caveat. Worth re-benchmarking in your own deployment before flipping the default. ([Issue #47397](https://github.com/sgl-project/sglang/issues/47397))
- **Qwen3.8-Flash-Next on gfx950/MI355X** — ongoing ROCm optimization tracker covering GatedDeltaNet (36 layers), QuerySparse Attention (12 layers), MXFP4 MoE and NEXTN MTP. ([Issue #44304](https://github.com/sgl-project/sglang/issues/44304))
- **AMD Qwen3-Next MoE router** — Triton softmax top-k router extended to the hidden-2048 envelope (previously gated to hidden 4096), replacing `aiter_fused_topk` on gfx950 for decode-sized rows. ([PR #47236](https://github.com/sgl-project/sglang/pull/47236))
- **Kimi-K3 MoE front on ROCm** — merged `[shared gate-up | router | latent down]` BF16 GEMM (N=6016, K=7168 at TP8) routed to AITER gfx950-tuned kernels instead of hipBLASLt heuristics. ([PR #44360](https://github.com/sgl-project/sglang/pull/44360))
- **RL routed-expert overhead** — three stacked changes cut CPU RAM pressure for `--enable-return-routed-experts`: host cache only on the output rank, skip capture on ranks that send no rows, and one all-gather per forward instead of per MoE layer under DeepEP + DP attention. All three are marked CLOSED. ([#47523](https://github.com/sgl-project/sglang/pull/47523), [#47547](https://github.com/sgl-project/sglang/pull/47547), [#47548](https://github.com/sgl-project/sglang/pull/47548))
- **Mamba HiCache without GPU slot donation** — removes the `max_running_requests * 5` GPU slot floor on Kimi-K3 c=48 recipes by keeping checkpoints host-side. ([PR #44718](https://github.com/sgl-project/sglang/pull/44718))
- **Scheduler architecture (RFC)** — proposal to decouple scheduler control from forward submission so the device launch queue stays populated across decode steps. ([Issue #47019](https://github.com/sgl-project/sglang/issues/47019)); also Attention–FFN disaggregation with pipelining + CUDA Graph support. ([Issue #41648](https://github.com/sgl-project/sglang/issues/41648))

## 5. Stability & Regressions

**Critical — memory exhaustion under sustained load**
- **DSV4.1-Flash + DSPARK OOM loop**: CUDA caching allocator exhausts GPU memory every 15–25 min under sustained max-batch decode, while the KV pool reports only 29% utilization — a strong signal of non-KV allocator fragmentation/leak rather than capacity exhaustion. No fix PR linked. ([Issue #43486](https://github.com/sgl-project/sglang/issues/43486))
- **HiCache Mooncake + DP attention**: each DP rank mounts the full `MOONCAKE_GLOBAL_SEGMENT_SIZE`, contradicting the README's "total = global segment size" claim; multiply this by your DP degree when sizing. ([Issue #46899](https://github.com/sgl-project/sglang/issues/46899))
- **ROCm DCP-PD allocator growth** preceding HIP resource aborts under burst load; reproduction on current main still pending. ([Issue #46831](https://github.com/sgl-project/sglang/issues/46831))

**High — crashes / correctness**
- **EAGLE draft extend crashes with negative dimension** under DP attention + FlashInfer A2A + prefill CUDA graph — a three-way feature interaction, so avoid that combination in production. ([Issue #47490](https://github.com/sgl-project/sglang/issues/47490))
- **`/start_profile` with `profile_by_stage=true` and no `num_steps`** raises `TypeError: NoneType += int` and crashes every scheduler. ([Issue #47294](https://github.com/sgl-project/sglang/issues/47294))
- **rust-server DP-rank routing**: `/internal/peer` serves relayed control requests without verifying target rank. ([Issue #47511](https://github.com/sgl-project/sglang/issues/47511)); `gather_server_endpoints` can advertise loopback/unroutable addresses and only warns. ([Issue #47509](https://github.com/sgl-project/sglang/issues/47509)); it also runs on elastic-EP joiners over a WORLD group serving ranks never enter. ([Issue #47505](https://github.com/sgl-project/sglang/issues/47505)). A companion PR publishes the listener map for attention-DP. ([PR #47532](https://github.com/sgl-project/sglang/pull/47532))
- **`stop_regex` leaks matched text** into the response and `no_stop_trim` is a no-op for regex stops — affects output post-processing contracts. ([Issue #47461](https://github.com/sgl-project/sglang/issues/47461))
- **GLM-5.3-Flash on SM120 (RTX PRO 6000)**: fa4 backend crashes at CUDA-graph capture on hybrid extend reshape; Triton is the only working attention backend on that hardware. ([Issue #42012](https://github.com/sgl-project/sglang/issues/42012))
- **AMD Quark MXFP4 W4A16 MoE with `--ep-size > 1`**: GPU abort with `HSA_STATUS_ERROR_EXCEPTION`. Fix PR open (restricts path to gfx1151). ([Issue/PR #47408](https://github.com/sgl-project/sglang/pull/47408))
- **NemotronHConfig rejects transformers 5 layer types** (`linear_attention` / `full_attention`) in `config.json` — blocks loading configs written by newer transformers. ([Issue #47444](https://github.com/sgl-project/sglang/issues/47444))

**Medium — observability & config**
- **Attention-DP ranks indistinguishable to routers**: `KvMetrics.data_parallel_rank` is hardcoded 0 and Prometheus series omit `dp_rank`, breaking per-rank load balancing and dashboards. ([Issue #47409](https://github.com/sgl-project/sglang/issues/47409))
- **S3 model URI silently overrides** an explicit `remote_instance` + modelexpress loader when `runai_streamer` is configured. ([Issue #47428](https://github.com/sgl-project/sglang/issues/47428))
- **HiCache + Mooncake L3 hit rate** reproducibly dips from 87.4% under L2/L3 capacity pressure in multi-turn benchmarks. ([Issue #47481](https://github.com/sgl-project/sglang/issues/47481))
- **Nomas diffusion pipeline**: KV budget ignores PyTorch-cached-but-freed memory, and SP divisibility is validated too late. ([Issue #47515](https://github.com/sgl-project/sglang/issues/47515))

**Regressions & fixes**
- **~5% decode regression on GB200** for Qwen3.8-Flash-Next-FP8 TP4/EP4 since [#45917](https://github.com/sgl-project/sglang/pull/45917) / commit `ac3db731`, where FP8 TRT-LLM MoE leaves in-kernel routing under EP. High-impact for anyone who merged past that commit. ([Issue #47501](https://github.com/sgl-project/sglang/issues/47501))
- **Deterministic top-p/top-k renormalization** for `tp_size > 1` landed (CLOSED): FlashInfer's default renorm uses float `atomicAdd` and is non-deterministic, causing TP rank divergence in DFlash/DSpark verify. ([PR #38565](https://github.com/sgl-project/sglang/pull/38565))
- **CI flakiness tracker** still very active — 159 comments, tracking recurring NVIDIA `PR Test Base` / `PR Test Extra` failures. Budget for red CI if you're landing PRs. ([Issue #42752](https://github.com/sgl-project/sglang/issues/42752))

## 6. What This Means for Application Developers
- **Cold start is your biggest cost lever right now.** If you run DeepSeek-V4.1 on serverless or autoscaling infrastructure, `SGLANG_JIT_DEEPGEMM_FAST_WARMUP` appears to remove ~27 minutes of warmup without runtime cost — pending broader confirmation. Validate on your own shapes before defaulting it on.
- **Avoid stacking advanced features blindly.** The two highest-severity crashes on the board (EAGLE + DP attention + FlashInfer A2A + prefill CUDA graph; DSPARK + DSV4.1-Flash sustained decode) come from feature *interactions*, not single features. Pin and test the exact combination you deploy.
- **Rust server is not yet a drop-in.** The DP-rank routing and endpoint-advertisement bugs are correctness issues that would silently misroute control traffic in multi-node setups. If you use `SGLANG_RUST_SERVER=1` for its multimodal preprocessing gains, keep it single-node or wait for [#47532](https://github.com/sgl-project/sglang/pull/47532).
- **Per-rank routing is currently blind under attention DP.** Until `dp_rank` lands in Prometheus series ([Issue #47409](https://github.com/sgl-project/sglang/issues/47409)), your gateway can't do load-aware routing across attention-DP ranks — plan for coarser-grained balancing.
- **Output-trimming contracts are unsafe for regex stops.** If your agent framework relies on `stop_regex` + `no_stop_trim` to bound tool-call or JSON generation, sanitize client-side until [#47461](https://github.com/sgl-project/sglang/issues/47461) is fixed.
- **KV cache utilization metrics are not trustworthy for OOM triage.** The DSV4.1 OOM report at 29% KV usage is a reminder that pool occupancy and actual GPU memory pressure diverge; instrument `torch.cuda.mem_get_info` and allocator stats directly.

</details>

<details>
<summary><strong>llama.cpp</strong> — <a href="https://github.com/ggml-org/llama.cpp">ggml-org/llama.cpp</a></summary>

# llama.cpp Digest — 2026-10-31

## Today's Highlights
A heavy release window (b12002–b12017) landed Windows/RPC UTF‑8 path and argv cleanups, a batched tensor copy API in ggml, and KV-cache rotation constants made resident on the GPU. In parallel, in-review work targets large Gemma 4 prefill gains, a new MoE expert cache policy, and broader low-bit OpenCL/Hexagon coverage. Backend stability remains the main drag: multiple open SYCL, HIP, Vulkan, and CUDA correctness/regression reports, including an illegal memory access with Gemma 4 + MTP.

## Releases & Breaking Changes
- **b12017 / b12015 / b12014 — Windows & RPC path handling cleanup.** `fs_path_to_utf8()` removed from `rpc` and `common`, and the Windows argv reconstruction dropped; argv is now UTF‑8 via the manifest from #31329. This fixes non-ASCII path handling (#26416) but is an interface removal for downstream code linking `common`. [b12017](https://github.com/ggml-org/llama.cpp/releases/tag/b12017) · [b12015](https://github.com/ggml-org/llama.cpp/releases/tag/b12015) · [b12014](https://github.com/ggml-org/llama.cpp/releases/tag/b12014)
- **b12012 — cpp-httplib updated to 0.64.0.** Server/HTTP dependency bump; worth rebuilding and re-running integration tests if you pin behavior. [b12012](https://github.com/ggml-org/llama.cpp/releases/tag/b12012)
- **b12004 — reasoning budget forcing now terminates on an end tag found in the prompt.** Behavior change for agent loops that rely on `--reasoning-budget`: budget enforcement can end earlier when the prompt already contains a stop tag. [b12004](https://github.com/ggml-org/llama.cpp/releases/tag/b12004)
- **b12002 — new ggml batched tensor copy API**, adopted by `llama` context I/O. Internal API addition, but out-of-tree ggml backends may want to implement/validate it. [b12002](https://github.com/ggml-org/llama.cpp/releases/tag/b12002)
- **PR #31444 — `common_get_path_from_env()` deletion** (follow-up cleanup to the path work). [PR #31444](https://github.com/ggml-org/llama.cpp/pull/31444)

## New Model & Hardware Support
- **OpenCL q2_0 support (b12005)** with AOS/SOA mat-vec, tiled mat-mul, and no-shuffle paths — meaningful for Adreno/mobile-class devices running very low-bit quantizations. [b12005](https://github.com/ggml-org/llama.cpp/releases/tag/b12005)
- **OpenCL IQ3 (IQ3_S, IQ3_XXS) initial support** in review, using the Adreno optimizations from #30180 as reference. [PR #31338](https://github.com/ggml-org/llama.cpp/pull/31338)
- **OpenCL `topk_mask`** (merge-ready) and **initial FWHT** support in review — closes more gaps against CUDA/Metal op coverage. [PR #31441](https://github.com/ggml-org/llama.cpp/pull/31441) · [PR #31434](https://github.com/ggml-org/llama.cpp/pull/31434)
- **SYCL `FLASH_ATTN_EXT` failures fixed (b12003)**. [b12003](https://github.com/ggml-org/llama.cpp/releases/tag/b12003)
- **Hexagon:** DMA transfers with strides >16M on v75+ devices, and batched HVX vgather-transpose for permuted CONT/CPY. [PR #31442](https://github.com/ggml-org/llama.cpp/pull/31442) · [PR #31446](https://github.com/ggml-org/llama.cpp/pull/31446)
- **WASM relaxed SIMD** dot-product implementations proposed; builds on #11453. [PR #19590](https://github.com/ggml-org/llama.cpp/pull/19590)
- **New architectures/models in review:** TML Inkling (safetensors→GGUF converter, graph, banded Flash Attention kernel, int64 indexing for large MoEs) [PR #25731](https://github.com/ggml-org/llama.cpp/pull/25731); PocketTTS voices without cloning [PR #31429](https://github.com/ggml-org/llama.cpp/pull/31429); LFM3-Audio codec decoder quantization guards relaxed (closed/merged) [PR #31386](https://github.com/ggml-org/llama.cpp/pull/31386).

## Performance & Optimization
- **KV-cache rotation constants kept resident on the GPU (b12007)**, with new tests verifying resident KV rotation buffers; documentation notes remaining multi-device work. Reduces per-step host→device traffic for quantized/rotated KV caches. [b12007](https://github.com/ggml-org/llama.cpp/releases/tag/b12007)
- **MoE expert cache: LRFU/MQ-like `ClassLRU` policy (PR #31233).** Reported +6% decode on QFN and +7% on GLM versus SLRU with a warm cache, and 8% fewer expert uploads; enables auto mode. [PR #31233](https://github.com/ggml-org/llama.cpp/pull/31233)
- **Gemma 4 E2B/E4B graph optimizations (PR #31356)** — skip compute for layers that do not contribute to the KV-shared cache and drop unused prompt tokens before KV-shared layers; described as "massive gains" on prompt processing, though no absolute numbers were provided. [PR #31356](https://github.com/ggml-org/llama.cpp/pull/31356)
- **Qwen3.8-Flash-Next (`qwen4exp`) conv-state tail written without an intermediate `cont`** — ~2% generation gain, verified on CUDA/CPU/meta (draft). [PR #31443](https://github.com/ggml-org/llama.cpp/pull/31443)
- **CUDA/HIP native quantized KV in `flash_attn_tile` (PR #31234)** — avoids per-step f16 dequantization or per-head cache rereads for q4/q8 KV. [PR #31234](https://github.com/ggml-org/llama.cpp/pull/31234)
- **MTP graph reallocation fix for Qwen3.5 dense** when switching between token and embedding inputs (PR #31415, fixes #31302). [PR #31415](https://github.com/ggml-org/llama.cpp/pull/31415)
- **Meta backend compute-view limit raised** for buffers with few tensors, fixing `ggml_new_object` OOM aborts with `-sm tensor` on DeepSeek-V4.1 (PR #31447). [PR #31447](https://github.com/ggml-org/llama.cpp/pull/31447)
- **Windows unbuffered model load** (DirectIO analogue) still seeking device testing. [PR #26014](https://github.com/ggml-org/llama.cpp/pull/26014)

## Stability & Regressions
Ranked by severity; all open unless noted.

1. **`GGML_ASSERT(src_ss[0].axis != GGML_BACKEND_SPLIT_AXIS_0)` abort** in `ggml-backend-meta.cpp` on a 4×3090 MiniMax M2.7 setup with split KV types. Open since June, still active. [Issue #24015](https://github.com/ggml-org/llama.cpp/issues/24015)
2. **CUDA illegal memory access: Gemma 4 31B + draft-MTP** after KV rollback/clear; no crash with MTP off. Reproduced on b11734/b11796/b11840. [Issue #31077](https://github.com/ggml-org/llama.cpp/issues/31077)
3. **SYCL segfaults:** oneAPI 2026.2.0 crash [Issue #31064](https://github.com/ggml-org/llama.cpp/issues/31064), and `server-intel-b11960` SIGSEGV in the persistent device code cache [Issue #31369](https://github.com/ggml-org/llama.cpp/issues/31369).
4. **HIP build failure on CDNA2 (gfx90a / MI210)** — compilation dies on Debian 12. [Issue #30869](https://github.com/ggml-org/llama.cpp/issues/30869)
5. **`qwen4exp` livelock during model load on HIP**, same config loads on Vulkan. [Issue #29149](https://github.com/ggml-org/llama.cpp/issues/29149)
6. **SYCL XMX-ESIMD MoE prompt-processing regression, 28–35% slower** on Arc Pro B70 between builds 11783 and 11851. [Issue #31068](https://github.com/ggml-org/llama.cpp/issues/31068)
7. **Vulkan Intel Arc Pro B70 deep-context decode collapse (~8× from 1k→64k tokens)**; SYCL degrades only ~2.4×. Backend-intrinsic, not model-specific. [Issue #28721](https://github.com/ggml-org/llama.cpp/issues/28721)
8. **CUDA arm64 Blackwell regression** between official builds b10655 and b11140 (RTX Spark N1X). [Issue #29341](https://github.com/ggml-org/llama.cpp/issues/29341)
9. **Prefix-cache invalidation from non-round-trippable reasoning/content whitespace** in Qwen3.5+ chat templates, causing full re-prefill on hybrid models. High impact for agent workloads. [Issue #30357](https://github.com/ggml-org/llama.cpp/issues/30357)
10. **DeepSeek-V4.1-Flash-1017 GGUF issues on CUDA** (dual EPYC + RTX 6000 Pro). [Issue #31385](https://github.com/ggml-org/llama.cpp/issues/31385)
11. **Intermittent `SOLVE_TRI` memory fault on gfx1200 HIP/ROCm.** [Issue #31108](https://github.com/ggml-org/llama.cpp/issues/31108)
12. **SYCL bf16 conversion instruction unsupported on Arrow Lake iGPU.** [Issue #31029](https://github.com/ggml-org/llama.cpp/issues/31029)
13. **CUDA misaligned address in `ggml_cuda_op_unary<op_sigmoid>`** on RTX 5090 Laptop with long prompts (regression range identified). [Issue #28877](https://github.com/ggml-org/llama.cpp/issues/28877)

Fix PRs in flight: #31447 (meta view limit), #31415 (MTP reallocations), #30743 (argsort/top-k on non-contiguous tensors), #31444 (path cleanup). Recently closed: LFM3 `response_format` grammar-stack 500 [Issue #31328](https://github.com/ggml-org/llama.cpp/issues/31328); LFM2.5 think-tag leakage [Issue #28675](https://github.com/ggml-org/llama.cpp/issues/28675); stale qwen35 RTX 5090 perf report [Issue #28196](https://github.com/ggml-org/llama.cpp/issues/28196).

## What This Means for Application Developers
- **Windows deployments get simpler:** update to b12014+ for UTF‑8 argv handling; non-ASCII model paths and CLI args should stop breaking. If you embed `common`, audit for removed `fs_path_to_utf8()`/`common_get_path_from_env()` symbols.
- **Reasoning-budget semantics changed in b12004.** Agents that inject stop/end tags into prompts may see shorter or earlier-terminated thinking; re-validate budget behavior before rolling forward.
- **Prefix-cache stability is the biggest agent-facing risk.** Issue #30357 means Qwen3.5+ hybrid models can silently lose prompt cache on whitespace mismatch, turning cheap follow-ups into full re-prefills. Pin chat templates carefully and monitor prefill time.
- **Low-bit inference reach is expanding:** OpenCL q2_0 landed and IQ3/topk_mask/FWHT are in review, making 2–3 bit quants viable on more non-NVIDIA hardware. Validate numerics per backend rather than assuming parity.
- **SYCL/HIP users should treat current builds as unstable** — segfaults, a build break on gfx90a, and a 28–35% MoE regression are open with no linked fix PRs. CUDA remains the safer default for production; Vulkan on Intel Xe2 has a context-scaling cliff.
- **Server operators:** the always-zero `prompt_tokens_seconds`/`predicted_tokens_seconds` gauges [Issue #27436](https://github.com/ggml-org/llama.cpp/issues/27436) and the lack of idle router-worker termination [Issue #25570](https://github.com/ggml-org/llama.cpp/issues/25570) still limit autoscaling/dashboards.

---
*Note: the supplied feed covers the top 30 of 51 updated issues and top 20 of 125 updated PRs, so this digest is a partial view.*

</details>

<details>
<summary><strong>Ollama</strong> — <a href="https://github.com/ollama/ollama">ollama/ollama</a></summary>

# Ollama Digest — 2026-10-31

## 1. Today's Highlights

Ollama Cloud remains the top operational concern: issue [#19111](https://github.com/ollama/ollama/issues/19111) reports `/v1/chat/completions` returning no HTTP response at all, with queued requests stalling ~5 minutes before a 429 — now at 6 comments and unresolved since 2026-10-16. On the local-runtime side, the bulk of engineering traffic is MLX: memory pre-flight accounting is demonstrably wrong for MLX models ([#19417](https://github.com/ollama/ollama/issues/19417)) while a per-layer KV-cache sizing fix ([#19327](https://github.com/ollama/ollama/pull/19327)) targets the same class of scheduler mis-estimation. API compatibility work continues on the Anthropic and OpenAI shims, with a fix in flight for dropped multi-block thinking content ([#19416](https://github.com/ollama/ollama/pull/19416)) and a Claude Code output cap raised from 32k to 128k tokens ([#19410](https://github.com/ollama/ollama/pull/19410)).

## 2. Releases & Breaking Changes

No releases in the last 24h. No API or config breaking changes landed.

Notable behavior changes in review:
- [PR #19410](https://github.com/ollama/ollama/pull/19410) (CLOSED) — `ollama launch` now advertises a 128k output-token cap for Claude Code instead of 32k, preventing mid-generation connection kills by the client.
- [PR #19408](https://github.com/ollama/ollama/pull/19408) — oversized prompts for MLX decision models now return a generic `413` rather than failing during runner load; longer state/schema inputs are accepted, total prompt expansion is bounded.

## 3. New Model & Hardware Support

- **AutoTrust decision models on MLX** — [PR #19399](https://github.com/ollama/ollama/pull/19399) wires text and vision AutoTrust models through model creation, prompt encoding, and API routing; test artifacts at `dhiltgen/autotrust-jev`.
- **Intel Macs on macOS 12 (Monterey)** — [PR #19413](https://github.com/ollama/ollama/pull/19413) adds best-effort build/run support for the desktop app and CLI, lifting the current macOS 14 floor for Intel hardware (e.g. 2015 iMacs capped at 12.7.6).
- **Per-model thinking metadata for OpenCode** — [PR #19409](https://github.com/ollama/ollama/pull/19409) derives thinking levels and defaults from model metadata rather than hardcoding GPT-OSS, so other reasoning models advertise correct controls.
- **Multimodal input validation** — [PR #19397](https://github.com/ollama/ollama/pull/19397) makes `/api/chat` reject clips the model has no encoder for; previously a base64 WAV passed through `images` on any model and the turn was silently answered from text only.

## 4. Performance & Optimization

- **Per-layer KV-cache sizing** — [PR #19327](https://github.com/ollama/ollama/pull/19327) fixes `PredictServerVRAM`, which currently sizes every layer using the smallest `head_count_kv`, `embedding_length / head_count` as head size, full context, and f16. On heterogeneous-layer models this overestimates badly and causes the scheduler to evict runners for memory that is never actually allocated.
- **MLX memory pre-flight gap** — [Issue #19417](https://github.com/ollama/ollama/issues/19417) reports MLX models bypass the scheduler's pre-flight check and are booked at weight size. On an M5 Max (128 GB, macOS 26), `qwen3.8:27b` (nvfp4) at the 262,144-token default context was booked at 16.9 GiB (`available` 91.5 → 74.6 GiB) while the runner's own memory accounting disagreed.
- **Speculative decoding benchmarking on MLX** — [PR #19391](https://github.com/ollama/ollama/pull/19391) adds `draft_num_predict=0` to disable drafting per request while keeping draft caches in lockstep; system default remains 4.
- **Runaway-generation guard for MLX** — [PR #19398](https://github.com/ollama/ollama/pull/19398) (CLOSED) ports the llama-server repeat limit into `mlxrunner`: generation aborts after 101 identical tokens with `prediction aborted, token repeat limit reached`.
- **Configurable mmproj headroom** — [Issue #19407](https://github.com/ollama/ollama/issues/19407) requests making the hardcoded 1 GiB multimodal projector safety margin configurable while preserving automatic `--fit` padding.

## 5. Stability & Regressions

Ranked by severity:

1. **CRITICAL — Cloud inference endpoint returns no response** ([#19111](https://github.com/ollama/ollama/issues/19111), OPEN, 6 comments). `POST https://ollama.com/v1/chat/completions` produces no status line and no body; concurrent request slots queue ~5 min then 429. Reported as a regression starting 2026-10-16 on a Pro plan; no fix PR yet.
2. **HIGH — Anthropic `/v1/messages` drops all but the last thinking block** ([#19415](https://github.com/ollama/ollama/issues/19415)). Earlier `thinking` blocks are silently discarded during conversion to an Ollama chat request, breaking clients that replay multi-block assistant turns. **Fix PR exists:** [#19416](https://github.com/ollama/ollama/pull/19416).
3. **HIGH — Claude Code auto-compaction fails on `deepseek-v4.1-flash:1017-cloud`** ([#19249](https://github.com/ollama/ollama/issues/19249)). Long-running `/goal` sessions exhaust context without compacting, looping on "Goal not yet met" >10 times and burning tokens.
4. **HIGH — MLX scheduler under-bookings** ([#19417](https://github.com/ollama/ollama/issues/19417)). Combined with concurrent model loads, this risks OOM/eviction thrash on large unified-memory Macs; related sizing fix in [#19327](https://github.com/ollama/ollama/pull/19327).
5. **MEDIUM — Rejected blob uploads persist on disk** ([#19414](https://github.com/ollama/ollama/issues/19414)). `POST /api/blobs/:digest` returns `400 digest mismatch` but still stores the bytes under their actual digest, orphaned and unreferenced until GC — an unbounded disk leak for clients that retry bad uploads.
6. **MEDIUM — cogito parser/renderer disagreement with tools** ([#19403](https://github.com/ollama/ollama/issues/19403)). With `think: true` and ≥1 tool, reasoning and `</think>` leak into message content because the renderer always emits `<think>` while the parser assumes the opposite.
7. **LOW — CRLF Modelfiles retain `\r` in triple-quoted values** ([#19404](https://github.com/ollama/ollama/issues/19404)). Windows-edited Modelfiles inject stray carriage returns into system prompts and templates.
8. **LOW — Windows 11 26H2 loopback TCP state ambiguity** ([#19418](https://github.com/ollama/ollama/issues/19418)). Native TCP tables report non-LISTEN states for the Ollama loopback endpoint on 0.40.13; reporter explicitly does not establish defect.
9. **LOW — Modelfile case-sensitivity docs incorrect** ([#19405](https://github.com/ollama/ollama/issues/19405)). Instruction names are case-insensitive; parameter names and message roles are not.

## 6. What This Means for Application Developers

- **Don't rely on Ollama Cloud for latency-sensitive agent loops right now.** If you are on `/v1/chat/completions` against `ollama.com`, add client-side timeouts well below 5 minutes and treat empty responses (no status line) as retryable rather than as a transport error to be surfaced to users. [#19111](https://github.com/ollama/ollama/issues/19111)
- **Anthropic-shim clients that replay thinking blocks will lose reasoning history.** If your agent persists and re-sends extended-thinking turns to `/v1/messages`, expect only the final thinking block to survive until [#19416](https://github.com/ollama/ollama/pull/19416) merges. Avoid depending on prior reasoning blocks for cache-aligned replay.
- **Long agent runs on hosted reasoning models need explicit compaction.** The DeepSeek failure in [#19249](https://github.com/ollama/ollama/issues/19249) means your harness should implement its own context-budget check rather than delegating compaction to the client. The 128k Claude Code cap in [#19410](https://github.com/ollama/ollama/pull/19410) reduces one class of premature disconnects but does not address compaction.
- **OpenAI-compat response IDs are deduplicating badly** — [PR #19401](https://github.com/ollama/ollama/pull/19401) notes `chatcmpl-%d` / `cmpl-%d` are generated from only 999 distinct values. Do not use response IDs as idempotency keys or trace identifiers today.
- **Tool-calling payloads with `content: []` are being fixed** — [PR #19152](https://github.com/ollama/ollama/pull/19152) tracks the case where assistant messages with empty-array content had their `tool_calls` migrated onto the previous message; if you interleave tools across turns, verify history integrity.
- **Multipart user messages with image-after-text can lose the instruction** — [PR #19198](https://github.com/ollama/ollama/pull/19198) addresses context truncation dropping the text that describes the image. Prefer text-last ordering only once this lands.
- **On Apple Silicon, pin context size explicitly for MLX models.** With the default VRAM-derived context (262k on a 128 GB M5 Max) and the accounting bug in [#19417](https://github.com/ollama/ollama/issues/19417), multi-model deployments can be scheduled into memory the runner cannot actually honor.

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM Digest — 2026-10-31

**Scope:** 1 new dev release, 112 issues and 472 PRs updated in the last 24h. Volume is dominated by cost-accounting correctness work and continued Claude Code / Anthropic-format compatibility fixes.

---

## 1. Today's Highlights

The day's center of gravity is **billing accuracy**: an open bug shows `/key/update` silently dropping in-flight request cost from budget-window spend, while a cluster of PRs reworks how provider-reported totals, Vertex server-side search calls, Perplexity filters, and billed media health checks are priced. In parallel, the router migration advanced to a flag-gated Rust core (`LITELLM_RUST`), and several long-stale Claude Code / Bedrock / Vertex translation issues were closed out.

---

## 2. Releases & Breaking Changes

- **v1.109.0-dev.2** — dev pre-release only; no stable cut in the last 24h. Supply-chain note: all Docker images are signed with **cosign** using the key introduced in commit [`e82a3c6`](https://github.com/BerriAI/litellm/commit/e82a3c646908ba0a6ee0beddc4310d7a6cac4065) — verify before rollout.
- **Breaking-flagged PRs in flight** (not yet merged):
  - [`#49227`](https://github.com/BerriAI/litellm/pull/49227) `fix(agentic)!` — surfaces failed agentic follow-up calls instead of returning the pre-loop tool call. Clients that implicitly relied on the swallowed-error 200 will see new error responses.
  - [`#49244`](https://github.com/BerriAI/litellm/pull/49244) `fix(health)!` — background health checks will **skip billed media generation modes** (image_generation, image_edit, video_generation) by default. Deployments using health checks as a liveness proxy for those modes must opt in explicitly.
- No config-schema migration required for the dev release itself.

---

## 3. New Model & Hardware Support

- [`#49361`](https://github.com/BerriAI/litellm/pull/49361) — Databricks: adds `supports_audio_input` / `supports_video_input` flags to the Gemini 3.5–3.8 Flash rows so capability metadata matches the documented `supported_modalities` (affects `databricks/databricks-gemini-*` routing eligibility).
- [`#49358`](https://github.com/BerriAI/litellm/pull/49358) (closed) — `gemini/gemini-2.5-flash-image` gains Batch/Flex/Priority **text output** prices (`1.25e-06` batch), which were previously falling through to the Standard $2.50/1M rate.
- Provider onboarding gaps closed on the UI side: Meta Model API (`meta/muse-spark-1.1`) missing from the Add Model dropdown [`#36164`](https://github.com/BerriAI/litellm/issues/36164); Nano-Gpt absent from provider list [`#34499`](https://github.com/BerriAI/litellm/issues/34499); Z.AI credential/model form fields not rendering [`#39310`](https://github.com/BerriAI/litellm/issues/39310).
- No new hardware backends (CUDA/ROCm/Metal/CPU) or quantization formats in this window.

---

## 4. Performance & Optimization

- **Router migration → Rust.** Three stacked PRs landed in review: [`#49118`](https://github.com/BerriAI/litellm/pull/49118) introduces `RoutingContext` so strategies/sub-routers stop holding the whole `Router`; [`#49119`](https://github.com/BerriAI/litellm/pull/49119) extracts `PythonCore` behind a `RouterCore` interface with `litellm.Router` as a thin facade; [`#49120`](https://github.com/BerriAI/litellm/pull/49120) adds the Rust core serving completions/messages/embeddings/responses routing behind `LITELLM_RUST`, with per-config fallback to Python and zero behavior change when the flag is off. No benchmarks published yet.
- [`#49228`](https://github.com/BerriAI/litellm/pull/49228) — logging hot path: the base64-image regex scan now runs only on strings containing `;`, `data:`, and `;base64,`, instead of on every message string of every successful request. Builds on the linear-scan fix from #45132.
- [`#34031`](https://github.com/BerriAI/litellm/issues/34031) (closed) — unbounded upstream error-body ingestion previously caused event-loop stalls and RSS blowup (observed with a ~114 MB HTTP 400 validation dump); proxied error bodies are now bounded before regex masking.
- [`#24720`](https://github.com/BerriAI/litellm/issues/24720) (closed) — lost-update race in `async_log_success_event` was degrading latency-based routing to count-weighted random selection under concurrency (16 Anthropic + 4 OpenAI keys per group).
- [`#34399`](https://github.com/BerriAI/litellm/issues/34399) (closed) — `Router._time_to_sleep_before_retry` now honors upstream `Retry-After` for multi-deployment model groups, not just single-deployment ones; previously caused instant-retry storms against rate-limited shared upstreams.

---

## 5. Stability & Regressions

**High**

- [`#49179`](https://github.com/BerriAI/litellm/issues/49179) **[OPEN, no fix PR]** — calling `/key/update` with `budget_limits` while a request is in flight drops that request's cost from `LiteLLM_BudgetWindowSpend`. `LiteLLM_SpendLogs` and the key's `spend` column stay correct, so window-based budget enforcement silently under-counts. **Data-plane correctness issue for anyone using windowed budgets as a hard cap.**
- [`#49356`](https://github.com/BerriAI/litellm/pull/49356) **[OPEN fix]** — `/v1/messages` on a plain Anthropic deployment returns 500 when the upstream 200s with `content` null/missing. Regression introduced by `#48254`, which began converting every native Messages body on the request path for pricing.
- [`#49227`](https://github.com/BerriAI/litellm/pull/49227) **[OPEN fix]** — a failed agentic follow-up (e.g. rate limit after a web search) was being swallowed; Claude Code received a 200 instructing it to call an undeclared tool and reported "Did 0 searches". Affects all agentic hooks.

**Medium**

- [`#48570`](https://github.com/BerriAI/litellm/issues/48570) (closed) — `import litellm` fails on **Python 3.15** (`sre_constants` removed); unconditional import in `router_strategy/complexity_router/config.py`. Related dep cleanup in [`#49347`](https://github.com/BerriAI/litellm/pull/49347) restricts `importlib-metadata` to Python <3.10.
- [`#34479`](https://github.com/BerriAI/litellm/issues/34479) (closed) — exhausting PostgreSQL `max_connections` under multi-worker deployment caused **all** user API keys to fail. Pool sizing remains an operator responsibility.
- [`#26237`](https://github.com/BerriAI/litellm/issues/26237) (closed) — transient Postgres/HAProxy outage surfaced as "Invalid model name" for valid, configured models.
- [`#49348`](https://github.com/BerriAI/litellm/pull/49348) **[OPEN fix]** — Vertex server-side Google Search invocations arriving as server-side `toolCall` parts (rather than grounding metadata `webSearchQueries`) were logged at zero cost.
- [`#49244`](https://github.com/BerriAI/litellm/pull/49244) **[OPEN fix]** — background health checks perform real generations for image/video deployments; a Gemini image model was billed ~**$0.135 per check** with zero traffic.
- [`#49213`](https://github.com/BerriAI/litellm/issues/49213) (closed) — API keys UI table truncates at 49 rows with 99 keys present and no pagination.

**Lower / translation-layer (mostly closed)**

- [`#26252`](https://github.com/BerriAI/litellm/issues/26252) — `websearch_interception` never fires for Claude Code → Bedrock pass-through; the referenced fix (`#25242`) reportedly re-breaks it via a new Bedrock skip, so the root cause remains contested.
- [`#45546`](https://github.com/BerriAI/litellm/issues/45546) — Mistral `_strip_output_only_fields` deleted `reasoning_content`/`thinking_blocks` before replay; docs require replaying as `thinking` chunks.
- [`#43012`](https://github.com/BerriAI/litellm/issues/43012) — Anthropic `stop_reason: model_context_window_exceeded` mapped to `"stop"` instead of a truncation signal.
- [`#26334`](https://github.com/BerriAI/litellm/issues/26334) — `response_format` + `thinking` returned 400 on `vertex_ai/claude-opus-4-7`.
- [`#27513`](https://github.com/BerriAI/litellm/issues/27513) — Bedrock retry path could replay stale SigV4 headers after signing.
- [`#46872`](https://github.com/BerriAI/litellm/issues/46872) — editing a model with `access_windows` returned 500 (`Object of type time is not JSON serializable`).
- [`#47777`](https://github.com/BerriAI/litellm/issues/47777) — key-level `router_settings.fallbacks` ignored on `/v1/images/generations`.
- [`#47261`](https://github.com/BerriAI/litellm/issues/47261) — Ollama embeddings ignored `api_key`, extra headers, and caller timeout.
- [`#45536`](https://github.com/BerriAI/litellm/issues/45536) / [`#49344`](https://github.com/BerriAI/litellm/pull/49344) — Perplexity Search dropped `search_recency_filter`, date filters, language, and mode; now forwarded, with provider validation errors propagated to the caller.

---

## 6. What This Means for Application Developers

- **Do not treat windowed budgets as a hard cap yet.** If you rely on `budget_limits` windows for tenant isolation, #49179 can leak cost during concurrent `/key/update` operations. Reconcile against `LiteLLM_SpendLogs` or the key `spend` column until a fix lands.
- **Media health checks may be costing you money.** If you run image/video generation deployments, audit health-check traffic now; ~$0.135/check on a 30s interval is meaningful. #49244 will change the default once merged.
- **Claude Code through LiteLLM remains the highest-friction path.** This window touched web-search interception, `thinking.type=adaptive`, `output_config.effort`, `reasoning.effort` on Azure/Foundry, `metadata.user_id` → `user` mapping, and agentic follow-up error propagation. Pin a version, and test `/v1/messages` responses with empty/null `content` — that path currently 500s.
- **Python 3.15 is not yet usable.** Stay on ≤3.14, and expect the `sre_constants` removal to surface in other transitive paths.
- **Router internals are moving.** The `RoutingContext` / `PythonCore` / Rust-core stack changes nothing behaviorally today (flag off = no-op), but custom router subclasses or anything reaching into `Router` private attributes should migrate to the documented endpoint surface.
- **Cost attribution is improving for chargeback.** [`#49360`](https://github.com/BerriAI/litellm/pull/49360) adds per-row key and user `metadata` to the daily usage export (no more per-row `/key/info` + `/user/info`), and [`#49133`](https://github.com/BerriAI/litellm/pull/49133) / [`#49190`](https://github.com/BerriAI/litellm/pull/49190) introduce opt-in durable, acknowledged usage persistence for accounting pipelines.
- **Pin and verify images.** Dev builds only in this window; use cosign verification against the `e82a3c6` key before deploying to production.

</details>

<details>
<summary><strong>Unsloth</strong> — <a href="https://github.com/unslothai/unsloth">unslothai/unsloth</a></summary>

# Unsloth Digest — 2026-10-31

## Today's Highlights
Unsloth shipped **v0.1.913-beta**, a UI/UX and performance release that adds custom backgrounds, cuts app update times, speeds up the Linux desktop app, and makes Qwen-Image generation viable on low-VRAM GPUs; it also adds `DeepSeek-V4.1-Flash-1017` to the Dynamic v3.1 GGUF lineup. On the kernel side, the team is actively reworking attention dispatch — Gemma 3 is moving off `flex_attention`'s fallback path onto SDPA for decode, while keeping flex for long-prompt prefill, plus a fix for a silent causal-mask loss on torch 2.8/2.9. Studio momentum continues with audio-capable LFM3 models and Flows-based data/training recipes, but an incident-level install regression around `UNSLOTH_STUDIO_HOME` needs attention.

## Releases & Breaking Changes
- **[v0.1.913-beta](https://github.com/unslothai/unsloth/releases)** — customization (custom backgrounds), improved UI/UX, faster app update times, Linux app speedups, and faster Qwen-Image generation under limited VRAM.
- **No documented API/config breaking changes** in this release, but be aware of a reported behavior regression in isolated installs: [#16186](https://github.com/unslothai/unsloth/issues/16186) / [#16185](https://github.com/unslothai/unsloth/issues/16185) (OPEN, duplicate filing) claim `UNSLOTH_STUDIO_HOME=<path> ./install.sh --local` now silently overwrites an existing baseline venv instead of creating a fully isolated runtime. If you rely on multi-tenant or per-project Studio homes, pin your installer or validate isolation before upgrading.
- Update-path reliability remains an open complaint: [#15866](https://github.com/unslothai/unsloth/issues/15866) (OPEN) — "Unsloth failed to update."

## New Model & Hardware Support
- **DeepSeek-V4.1-Flash-1017** added to Unsloth Dynamic v3.1 GGUFs (preview) — [docs](https://unsloth.ai/docs/models/deepseek-v4.1-flash), announced in v0.1.913-beta.
- **LFM3-Omni audio input** (plus export, LoRA defaults, and Stop for custom-code generate) — [PR #16242](https://github.com/unslothai/unsloth/pull/16242). Previously `LiquidAI/LFM3-Omni-2B` loaded as vision-only (`audio_type=None`).
- **LFM3-Audio-2B chat** (audio in, text out) replacing the prior load refusal — [PR #16243](https://github.com/unslothai/unsloth/pull/16243).
- **Integrated GPU quantisation path** (Strix Halo, Jetson, DGX Spark): native int8 host offload now respects `host_pinning_allowed` instead of always pinning — [PR #16235](https://github.com/unslothai/unsloth/pull/16235).
- **Apple MLX** fixes landed/closed: Dolphin Venice Edition rendering in Studio UI ([#15858](https://github.com/unslothai/unsloth/issues/15858)) and LFM3 MLX models missing from `curl /v1/models` ([#15832](https://github.com/unslothai/unsloth/issues/15832)).
- **AMD/Vulkan**: LFM3-Omni video input failure on RX 6800 ([#16065](https://github.com/unslothai/unsloth/issues/16065)) and LFM3-Omni safetensors load failure on Windows 11 ([#16054](https://github.com/unslothai/unsloth/issues/16054)) both closed.
- **ModelScope**: >50 GB model downloads were being blocked; issue closed — [#15989](https://github.com/unslothai/unsloth/issues/15989).

## Performance & Optimization
- **Gemma 3 attention path split** — [PR #16041](https://github.com/unslothai/unsloth/pull/16041): `flex_attention` remains compiled on L4 / A10 / RTX 3090 / 4090 / L40S across torch 2.10–2.14.1 (via #16049, #16073), but flex is *slower than SDPA for one-token decode* while *much faster for long-prompt prefill*. The PR routes generation to the non-flex path. This is the single most throughput-relevant change in flight for decode-heavy serving.
- **Compiled flex causal-mask correctness/perf** — [PR #16234](https://github.com/unslothai/unsloth/pull/16234): on torch 2.8/2.9, Dynamo evaluates `hasattr(query, "dim")` as `False`, causing `_dropped_causal_mask` to fall through and stock flex attention to receive `attention_mask=None` (bidirectional attention). Fixed upstream in torch 2.10. Affects anyone on 2.8/2.9 with per-layer compiled blocks (#10744, release `2026.10.6`).
- **Fused-loss recompilation** — [PR #15575](https://github.com/unslothai/unsloth/pull/15575): trainer-side fused call counters (`_unsloth_dpo_chunked_calls`, `_unsloth_pref_chunked_calls`, `_unsloth_gkd_*`, PPO/RLO) were recompiled every step under `torch.compile`; counters moved out of traced code and TRL head contracts narrowed.
- **v0.1.913-beta**: reduced app update times and faster Linux desktop app startup; Qwen-Image gen sped up when VRAM-constrained.
- **Memory estimation accuracy** — [#15935](https://github.com/unslothai/unsloth/issues/15935) (CLOSED): MLX estimator reported 69.7 GiB for a model that actually loads on a 24 GB Mac. Treat MLX estimators with caution until confirmed fixed.

## Stability & Regressions
Ranked by severity:

1. **Incident-level (OPEN)** — [#16186](https://github.com/unslothai/unsloth/issues/16186) / [#16185](https://github.com/unslothai/unsloth/issues/16185): `UNSLOTH_STUDIO_HOME` isolated installs silently overwrite an existing baseline venv, breaking cross-contamination guarantees. No linked fix PR in this data set.
2. **High (OPEN)** — [#16178](https://github.com/unslothai/unsloth/issues/16178): Studio image generation returns 404 after a managed account loads a cached gated model.
3. **High (OPEN)** — [#16187](https://github.com/unslothai/unsloth/issues/16187): `search_conversation` tool has disappeared entirely; related long-conversation breakage was closed in [#14708](https://github.com/unslothai/unsloth/issues/14708) (attachments unreadable after auto-compaction) and [#15800](https://github.com/unslothai/unsloth/issues/15800) (context not compacting on return to long conversations).
4. **Medium (OPEN)** — [#15999](https://github.com/unslothai/unsloth/issues/15999): AppImage Studio has a very laggy UI; [#15866](https://github.com/unslothai/unsloth/issues/15866): updater fails.
5. **Medium (OPEN)** — [#16221](https://github.com/unslothai/unsloth/issues/16221): ShareGPT image lists pass dataset format checks but fail downstream.
6. **Low (OPEN)** — [#16195](https://github.com/unslothai/unsloth/issues/16195): `unsloth list-checkpoints --outputs-dir` prints a traceback for paths outside Unsloth's outputs folder.
7. **Closed today** — Linux theme change aborting `WebKitWebProcess` and freezing the window ([#16028](https://github.com/unslothai/unsloth/issues/16028)); Windows/AMD `llama-server` holding ~16 GB commit charge after GGUF load ([#16015](https://github.com/unslothai/unsloth/issues/16015)); eval dataset task-name collisions with YAML tasks ([#15982](https://github.com/unslothai/unsloth/issues/15982)); chat textarea duplication across tabs ([#15782](https://github.com/unslothai/unsloth/issues/15782)); HF gated-repo token access ([#8604](https://github.com/unslothai/unsloth/issues/8604)).
8. **CI/test-signal issues** — [PR #16244](https://github.com/unslothai/unsloth/pull/16244) notes `test_build_group_layout_single_read_same_inputs` failing on main (`assert 0 == 1`); [PR #16245](https://github.com/unslothai/unsloth/pull/16245) fixes xdist worker port-block wraparound at 40 workers; [PR #16236](https://github.com/unslothai/unsloth/pull/16236) fixes a hub-source test that assumed Hugging Face rather than the inherited `UNSLOTH_STUDIO_HUB_SOURCE`.

## What This Means for Application Developers
- **Pin your installs.** The `UNSLOTH_STUDIO_HOME` regression is the one item that can silently destroy an existing environment. Use a container or explicit version pin until it is resolved, especially if you run multiple Studio instances on one host.
- **Decode latency should improve on Gemma 3.** The flex→SDPA generation split ([#16041](https://github.com/unslothai/unsloth/pull/16041)) targets the token-by-token path most user-facing apps care about, while preserving flex's prefill advantage for long system prompts and RAG contexts.
- **Audit torch versions if you rely on compiled flex attention.** On torch 2.8/2.9, causal masking can silently degrade to bidirectional attention ([#16234](https://github.com/unslothai/unsloth/pull/16234)) — a correctness bug that looks like a quality problem, not a crash. Prefer torch 2.10+, or take the PR.
- **Multimodal audio is arriving.** LFM3-Omni and LFM3-Audio-2B support ([#16242](https://github.com/unslothai/unsloth/pull/16242), [#16243](https://github.com/unslothai/unsloth/pull/16243)) is landing in Studio via the OpenAI-ish local server, but note the AMD/Vulkan and Windows paths have only just had blocking bugs closed.
- **Don't trust memory estimators blindly.** The MLX 69.7 GiB vs 24 GB discrepancy ([#15935](https://github.com/unslothai/unsloth/issues/15935)) and the missing per-model resource visibility ([#16055](https://github.com/unslothai/unsloth/issues/16055), OPEN) mean you should validate VRAM headroom empirically before sizing fleets.
- **Managed/team deployments:** private loopback HTTP MCP servers are still blocked for managed accounts ([#16029](https://github.com/unslothai/unsloth/issues/16029), closed as a feature request), so plan MCP topology around public-network endpoints or the owner account.
- **Flows is becoming the automation surface.** Data Recipes, a full Train node with hold-out splits ([#15604](https://github.com/unslothai/unsloth/pull/15604), [#15611](https://github.com/unslothai/unsloth/pull/15611)), and model-lifecycle fixes for download detection and unload-after-run ([#16239](https://github.com/unslothai/unsloth/pull/16239), [#16238](https://github.com/unslothai/unsloth/pull/16238)) suggest graph-orchestrated fine-tuning is the direction — worth prototyping against now.

</details>