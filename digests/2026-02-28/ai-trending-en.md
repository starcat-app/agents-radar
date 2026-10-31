# AI Open Source Trending Report 2026-02-28

> Data source: GitHub Trending + GitHub Search API | Generated at: 2026-02-28 03:32 UTC

---

# AI Open Source Trending Report | 2026-02-28

---

## Step 1: AI Relevance Filtering

**Trending list filtering result**: Of 16 repositories, **13 are AI/ML related**; 3 non-AI projects were excluded:
- ❌ `tukaani-project/xz` (compression tool)
- ❌ `D4Vinci/Scrapling` (general-purpose scraping framework, not AI-native)
- ❌ `steipete/CodexBar` (tool-usage statistics, an auxiliary utility)

**Topic search**: All 79 repositories are AI related and were retained.

---

## Step 2: Taxonomy

| Category | Definition |
|:---|:---|
| 🔧 **AI Foundational Tools** | Inference engines, development frameworks, CLI tools, SDKs, deployment infrastructure |
| 🤖 **AI Agents/Workflows** | Agent frameworks, multi-agent orchestration, automated workflows, MCP/tool calling |
| 📦 **AI Applications** | Concrete product forms: chat clients, coding assistants, OCR, speech, educational content |
| 🧠 **Large Models/Training** | Model implementations, training frameworks, fine-tuning tools, quantized inference, ASR/CV models |
| 🔍 **RAG/Knowledge Bases** | Vector databases, retrieval-augmented generation, knowledge graphs, memory layers |

---

## Step 3: Report Body

### 1. Today at a Glance

The AI open source landscape today shows an **"agent infrastructure" explosion**: ByteDance open sourced the `deer-flow` super-agent framework, Anthropic's official `claude-code` CLI tool stays red hot, and multiple agent skill libraries and orchestration platforms (`ruflo`, `superpowers`) hit the chart the same day — marking the industry's center of gravity shifting **from "model capability" to "engineered agent systems"**. New sensing+AI fusion technologies such as edge AI speech (`moonshine`) and WiFi sensing (`wifi-densepose`) entered the mainstream spotlight for the first time, and the vector DB space gained a high-performance Rust newcomer (`ruvector`). Educational content from the Chinese-speaking community's `hello-agents` drew attention, reflecting rapid growth in demand for learning agent development.

---

### 2. Hot Projects by Dimension

#### 🔧 AI Foundational Tools

| Project | Stars | New Today | One-Line Summary |
|:---|:---|:---|:---|
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | - | +494 | Anthropic's official terminal Agent tool: natural-language-driven code understanding, execution, and Git workflows, defining a new standard for "conversational development" |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | - | +696 | ByteDance's open source SuperAgent framework with sandboxing, memory, tools, and sub-agents for long-horizon tasks from minutes to hours |
| [ruvnet/ruvector](https://github.com/ruvnet/ruvector) | - | +410 | A high-performance, real-time, self-learning vector graph-neural-network database built in Rust, aimed at next-generation RAG infrastructure |
| [ollama/ollama](https://github.com/ollama/ollama) | 163,624 | - | The de facto standard for running local LLMs; already supports the latest models including Kimi-K2.5, GLM-5, MiniMax, and DeepSeek |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 71,444 | - | High-throughput, memory-efficient LLM inference and serving engine; a first choice for production deployment |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 125,182 | - | User-friendly AI interface with dual Ollama and OpenAI API stacks; a benchmark for self-hosted deployment |
| [abhigyanpatwari/GitNexus](https://github.com/abhigyanpatwari/GitNexus) | - | +1,385 | **Fastest growth today**: A pure in-browser code knowledge graph + Graph RAG Agent whose zero-server architecture reimagines code exploration |
| [moonshine-ai/moonshine](https://github.com/moonshine-ai/moonshine) | - | +593 | Fast, accurate ASR for edge devices written in C, filling a gap in on-device speech understanding infrastructure |

#### 🤖 AI Agents/Workflows

| Project | Stars | New Today | One-Line Summary |
|:---|:---|:---|:---|
| [obra/superpowers](https://github.com/obra/superpowers) | - | **+1,546** | **Today's growth champion**: An agent skills framework plus software development methodology that emphasizes "working" engineering practice over concept demos |
| [muratcankoylan/Agent-Skills-for-Context-Engineering](https://github.com/muratcankoylan/Agent-Skills-for-Context-Engineering) | - | +803 | A skill library for context engineering and multi-agent architecture; essential for debugging and tuning production-grade agent systems |
| [ruvnet/ruflo](https://github.com/ruvnet/ruflo) | - | +531 | A leading agent orchestration platform in the Claude ecosystem with distributed swarm intelligence, RAG integration, and native Claude Code/Codex compatibility |
| [langgenius/dify](https://github.com/langgenius/dify) | 130,627 | - | Production-grade agentic workflow platform; a benchmark balance of visual orchestration and code-level flexibility |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 127,706 | - | The de facto standard for dependable agent platforms and industry infrastructure for tool calling and chain abstractions |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 79,167 | - | Makes websites accessible to AI agents; a general layer for browser-automated task execution |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 68,285 | - | Full-stack AI-driven development platform automating the whole flow: code generation, testing, PRs |
| [trycua/cua](https://github.com/trycua/cua) | 12,755 | - | Open source infrastructure for computer-use agents with full desktop control across macOS/Linux/Windows |
| [e2b-dev/E2B](https://github.com/e2b-dev/E2B) | 11,062 | - | Enterprise-grade secure sandbox environments for agents, with real toolchain integration |
| [activepieces/activepieces](https://github.com/activepieces/activepieces) | 20,986 | - | AI automation platform with ~400 MCP servers, fusing agents and workflows |
| [alibaba/OpenSandbox](https://github.com/alibaba/OpenSandbox) | - | +105 | A general-purpose sandbox platform for AI applications with multi-language SDKs, covering coding agents, GUI agents, RL training, and more |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 19,234 | - | Build a Claude Code-style agent from scratch; minimalist engineering teaching with a "Bash is all you need" ethos |

#### 📦 AI Applications

| Project | Stars | New Today | One-Line Summary |
|:---|:---|:---|:---|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 40,355 | - | AI productivity studio with smart chat + autonomous agents + 300+ assistants and unified access to frontier LLMs |
| [zhayujie/chatgpt-on-wechat](https://github.com/zhayujie/chatgpt-on-wechat) | 41,590 | - | CowAgent, an LLM-based super AI assistant with proactive thinking, task planning, and long-term memory, deployable across platforms |
| [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | 71,320 | - | Lightweight yet powerful OCR toolkit for 100+ languages; a bridge for extracting structured data from images/PDFs |
| [moeru-ai/airi](https://github.com/moeru-ai/airi) | - | +199 | Self-hosted Grok companion with real-time voice chat and Minecraft/Factorio gameplay; a "neuro-sama" style virtual being |
| [ruvnet/wifi-densepose](https://github.com/ruvnet/wifi-densepose) | - | +478 | **Technical breakthrough**: Real-time through-wall human pose estimation using commodity mesh routers; a new paradigm fusing WiFi sensing and AI |
| [datawhalechina/hello-agents](https://github.com/datawhalechina/hello-agents) | - | +324 | A Chinese-language tutorial, 《从零开始构建智能体》 (Building Agents from Scratch), filling the gap in systematic agent education content |

#### 🧠 Large Models/Training

| Project | Stars | New Today | One-Line Summary |
|:---|:---|:---|:---|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 157,110 | - | The framework for state-of-the-art ML model definitions, unifying text/vision/audio/multimodal |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 86,208 | - | Implement a ChatGPT-style LLM from scratch with step-by-step PyTorch teaching; the top pick for understanding the fundamentals |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 67,654 | - | Unified, efficient fine-tuning of 100+ LLMs/VLMs; ACL 2024; infrastructure for model customization at scale |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 3,829 | - | A course on LLM inference serving on Apple Silicon; hands-on tiny vLLM + Qwen |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 300 | - | X-Bit quantization-driven on-device LLM inference; a new option for edge deployment |
| [testtimescaling/testtimescaling.github.io](https://github.com/testtimescaling/testtimescaling.github.io) | 88 | - | A Test-Time Scaling survey repository collecting frontier research on inference-time compute scaling |

#### 🔍 RAG/Knowledge Bases

| Project | Stars | New Today | One-Line Summary |
|:---|:---|:---|:---|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 73,875 | - | Leading open source RAG engine fusing cutting-edge RAG and agent capabilities; a quality context layer for LLMs |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 47,247 | - | Leading document-agent and OCR platform; the de facto standard for data connectivity and retrieval |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 48,229 | - | A universal memory layer for AI agents: cross-session long-term memory and personalization |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 12,605 | - | Build an AI agent memory knowledge engine in 6 lines of code, with developer experience first |
| [yichuan-w/LEANN](https://github.com/yichuan-w/LEANN) | 10,158 | - | RAG on personal devices: 97% storage savings, 100% privacy, MLsys2026 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 29,173 | - | High-performance vector database at scale; a next-generation AI vector search engine |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 43,020 | - | Cloud-native, high-performance vector ANN search in a scalable vector database |
| [chroma-core/chroma](https://github.com/chroma-core/chroma) | 26,361 | - | Open source search-and-retrieval database for AI applications; a developer-friendly embedded option |

---

### 3. Trend Signal Analysis

**The year of agent engineering begins**: Today's trending list shows a **clustered burst of "Agent infrastructure"** — from ByteDance's `deer-flow` long-horizon task framework and Anthropic's official `claude-code` terminal tool to `superpowers`' methodology and `ruflo`'s Claude-ecosystem orchestration, the community is moving from "demo-grade agents" to "production-grade systems". `obra/superpowers` topped the chart with +1,546 stars; its software-engineering orientation that stresses "works" reflects an industry-wide consensus that **reliability beats showing off**.

**Emerging tech-stack signals**: ① **Rust penetrating AI infrastructure**: `ruvector` (vectors + GNN) and `moonshine` (ASR) both deliver high performance in Rust/C; ② **Physical-world sensing fusion**: `wifi-densepose` pioneers a new modality of WiFi signals + pose estimation, breaking the dependence on vision; ③ **Zero-server architecture**: `GitNexus` runs Graph RAG purely in the browser, challenging the traditional backend-heavy paradigm.

**Links to industry events**: Anthropic's recent Claude updates keep rippling — official `claude-code` open sourcing plus community mirror services (`claude-relay-service`), skill libraries (`everything-claude-code`), and teaching projects (`learn-claude-code`) now form a complete ecosystem layer. ByteDance entering with `deer-flow` marks Chinese tech giants formally joining the international agent-framework competition.

---

### 4. Community Focus Points

- **🔥 `obra/superpowers`** — Growth champion; the "agent skills framework + methodology" combination fills an industry gap and suits teams building agent engineering standards
- **🔥 `abhigyanpatwari/GitNexus`** — Architectural innovation of a pure-frontend knowledge graph + RAG with zero ops cost; a good fit for fast codebase exploration
- **🔥 `ruvnet/wifi-densepose`** — A cross-modal sensing breakthrough: through-wall human tracking over WiFi; a new hardware-software junction for smart home/security/health monitoring
- **🔥 `bytedance/deer-flow`** — ByteDance's first open source agent framework; its long-horizon task design (minutes → hours) benchmarks against Devin-class systems and is worth tracking
- **🔥 `moonshine-ai/moonshine`** — A high-performance C implementation of edge ASR; a key puzzle piece for on-device voice agents, suited to IoT/wearable scenarios

---

*Report generated at: 2026-02-28 | Data source: GitHub Trending & Search API*

---
*This report was auto-generated by [agents-radar](https://github.com/duanyytop/agents-radar).*