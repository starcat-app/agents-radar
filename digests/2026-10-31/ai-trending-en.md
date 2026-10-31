# AI Open Source Trends 2026-10-31

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-10-31 00:15 UTC

---

**Filtering note:** Only AI-relevant repositories were included. Ambiguous or non-AI trending items were excluded. Star counts are reproduced from the supplied data; trending-only repos show `0` total where only today’s gain is available.

## 1. Today’s Highlights

Agent context and skills were the clearest center of gravity: [claude-mem](https://github.com/thedotmack/claude-mem) added +1,140 today, while [anthropics/skills](https://github.com/anthropics/skills), [mattpocock/skills](https://github.com/mattpocock/skills), and [obra/superpowers](https://github.com/obra/superpowers) all trended, pointing to persistent memory and reusable agent behaviors as the new packaging layer. Code-generation quality tooling had the strongest single spike: [impeccable](https://github.com/pbakaus/impeccable) led AI trending at +2,300, with [JetBrains/thinkrail](https://github.com/JetBrains/thinkrail) (+722), [OpenBot](https://github.com/CopilotKit/OpenBot) (+706), and [OpenMausBot](https://github.com/milind-soni/OpenMausBot) (+895) reinforcing demand for controllable coding-agent workbenches. Vertical AI coworkers continued to convert demos into workflows: [DeepTutor](https://github.com/HKUDS/DeepTutor) (+2,282), [career-ops](https://github.com/career-ops-hq/career-ops) (78,898 stars), [ppt-master](https://github.com/hugohe3/ppt-master) (71,314), and stock/trading agents showed end-to-end task ownership. Retrieval and context infrastructure remained high-scale: [Graphify](https://github.com/Graphify-Labs/graphify) (139,472), [RAGFlow](https://github.com/infiniflow/ragflow) (93,222), [mem0](https://github.com/mem0ai/mem0) (68,117), and vector databases kept RAG/memory in the center of the stack. LLM security/prompting also surfaced: [jailbreaks](https://github.com/togg53192-cmd/jailbreaks) added +2,055 today, a signal that red-teaming and guardrail testing are moving into mainstream agent development.

## 2. Top Projects by Category

### 🔧 AI Infrastructure

| Project | Lang | Stars (total / today) | Summary |
| :--- | :--- | ---: | :--- |
| [ollama/ollama](https://github.com/ollama/ollama) | Go | 185,380 | Local model runner for Kimi, GLM, MiniMax, DeepSeek, gpt-oss, Qwen, Gemma and others. Its high star base and broad model support keep it a default local inference layer for agent and RAG stacks. |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | JavaScript | 293,402 | Agent-harness performance optimization system covering skills, instincts, memory, security, and research-first development across Claude Code, Codex, OpenCode, Cursor and more. Its huge star count signals strong interest in making coding agents more reliable and efficient. |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | Python | 78,383 | Compresses tool outputs, logs, files, and RAG chunks before they hit the LLM, with claims of 20% fewer tokens for coding agents and 60–95% fewer for JSON. Token/context compression is becoming a first-class infrastructure concern. |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | TypeScript | 38,401 | Frontend stack for agents and generative UI across React, Angular, mobile, Slack and more; also steward of the AG-UI Protocol. It is positioning agent UX and protocol interoperability as core infrastructure. |
| [lightpanda-io/browser](https://github.com/lightpanda-io/browser) | Zig | 0 (+626) | Headless browser designed for AI and automation. Its Zig implementation and AI-first focus make it notable as browser automation becomes a bottleneck for agents. |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Rust | 0 (+2,300) | Design vocabulary for coding agents, with commands like “polish,” “critique,” and “audit” to catch AI slop before shipping. It led today’s AI trending list by new stars, showing demand for quality-control layers around coding agents. |
| [anthropics/skills](https://github.com/anthropics/skills) | Python | 0 (+295) | Public repository for Agent Skills. It is a signal that skills are becoming a packaging unit for agent behavior, not just ad hoc prompts. |
| [mattpocock/skills](https://github.com/mattpocock/skills) | Shell | 0 (+876) | Skills for “real engineers,” published from an .agents directory. Its momentum reflects the rise of portable, versioned agent skills alongside official and community collections. |

### 🤖 AI Agents / Workflows

| Project | Lang | Stars (total / today) | Summary |
| :--- | :--- | ---: | :--- |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | Python | 258,876 | “The agent that grows with you,” an agent project with a very large star base. Its position at the top of ai-agent topic results shows continued appetite for general-purpose, adaptive agents. |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | Python | 187,839 | Long-running open-source agent platform aimed at accessible AI automation. It remains a high-visibility anchor for the agent ecosystem despite newer frameworks. |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | Python | 148,740 | Agent engineering platform with broad model/tool integrations. It continues to serve as a default integration layer for agent and workflow builders. |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | Python | 119,600 | Python library for AI browser agents, plus a hosted cloud option with stealth browsers. Browser control remains one of the most practical agent capabilities. |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | Python | 106,816 | Gives agents read/search access to Twitter, Reddit, YouTube, GitHub, Bilibili and XiaoHongShu through one CLI with zero API fees. It addresses the data-access bottleneck for agent research and monitoring. |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | Python | 44,185 | Build resilient agents with graph-based orchestration. It remains a mainstream framework for production agent workflows. |
| [CopilotKit/OpenBot](https://github.com/CopilotKit/OpenBot) | TypeScript | 0 (+706) | Open-source AI coworkers that each get a computer—browser, files, tools—with actions decided before execution and recorded after; bring any AG-UI agent. It trended today as a concrete “AI coworker” runtime. |
| [obra/superpowers](https://github.com/obra/superpowers) | Shell | 0 (+1,259) | Agentic skills framework and software-development methodology. Its strong new-star gain shows methodology and reusable skills are becoming as important as raw agent frameworks. |

### 📦 AI Applications

| Project | Lang | Stars (total / today) | Summary |
| :--- | :--- | ---: | :--- |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | Python | 157,293 | User-friendly AI interface supporting Ollama, OpenAI API and more. It remains one of the highest-starred self-hosted AI front ends. |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | Python | 136,606 | Generates HD short videos from a topic or keyword using AI models and automated workflows. It shows continued demand for turnkey generative-video pipelines. |
| [career-ops-hq/career-ops](https://github.com/career-ops-hq/career-ops) | JavaScript | 78,898 | Open-source AI job search agent that scans boards, scores jobs against a CV, tailors resumes/cover letters and tracks applications. It is a clear example of vertical agents owning an end-to-end workflow. |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | Python | 71,314 | Turns documents or topics into native PowerPoint decks with shapes, transitions, charts, narration and custom templates. It targets a high-value office workflow with native output rather than slide images. |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | Python | 67,298 | LLM-powered multi-market stock analysis system with market data, news, dashboards and scheduled notifications. Finance remains a strong vertical for agentic analysis and automation. |
| [HKUDS/DeepTutor](https://github.com/HKUDS/DeepTutor) | Python | 51,762 (+2,282) | Lifelong personalized tutoring project from HKUDS. It was one of today’s biggest AI gainers, highlighting education as a fast-moving agent application. |
| [microsoft/qlib](https://github.com/microsoft/qlib) | Python | 49,839 | AI-oriented quant investment platform covering ML modeling, market dynamics and RL, with RD-Agent automation. It brings industrial-grade AI tooling to quantitative research. |
| [jeecgboot/JeecgBoot](https://github.com/jeecgboot/JeecgBoot) | Java | 48,347 | Enterprise AI low-code platform that can generate full systems from prompts, with AI chat, knowledge base, workflow and MCP plugins. It shows enterprise Java teams adopting AI-assisted development and agentic low-code. |

### 🧠 LLMs / Training

| Project | Lang | Stars (total / today) | Summary |
| :--- | :--- | ---: | :--- |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | C++ | 201,234 | Open-source machine learning framework for everyone. Its scale and ecosystem make it a baseline for ML training and deployment. |
| [huggingface/transformers](https://github.com/huggingface/transformers) | Python | 168,374 | Model-definition framework for state-of-the-art text, vision, audio and multimodal models for inference and training. It remains the central hub for open model implementations. |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | Jupyter Notebook | 107,569 | Step-by-step implementation of a ChatGPT-like LLM in PyTorch. It continues to be a high-signal educational resource as more developers build and fine-tune models. |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | Python | 105,030 | Tensors and dynamic neural networks with strong GPU acceleration. It is still the dominant training/research stack for many open models. |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | Python | 64,665 | Train a 64M-parameter LLM from scratch in about two hours. It makes end-to-end LLM training unusually accessible for experimentation. |
| [keras-team/keras](https://github.com/keras-team/keras) | Python | 64,399 | Deep learning for humans, with a high-level API across backends. It remains relevant for fast prototyping and production ML. |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | Python | 7,559 | LLM evaluation platform supporting OpenAI, Anthropic, Gemini, Qwen, GLM, DeepSeek and 100+ datasets. Evaluation is increasingly critical as model choice and agent reliability matter. |
| [togg53192-cmd/jailbreaks](https://github.com/togg53192-cmd/jailbreaks) |  | 0 (+2,055) | Public list of jailbreak prompts that gained strong attention today. It is not a production framework, but it is a clear signal of community focus on LLM red-teaming, guardrails and prompt security. |

### 🔍 RAG / Knowledge

| Project | Lang | Stars (total / today) | Summary |
| :--- | :--- | ---: | :--- |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | Python | 139,472 | Turns codebases, docs, SQL schemas, configs and PDFs into a queryable knowledge graph via a /graphify skill for Claude Code, Cursor, Codex and Gemini CLI. Its no-vector-store, explainable-edge approach is a notable RAG alternative. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | TypeScript | 106,218 (+1,140) | Captures agent session activity, compresses it with AI and injects relevant context into future sessions across Claude Code, Codex, Gemini, Copilot and others. Today’s strong gain makes persistent agent memory one of the clearest trends. |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | Go | 93,222 | RAG engine that fuses retrieval-augmented generation with agent capabilities to create a context layer for LLMs. It remains a leading open-source RAG platform. |
| [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) | Python | 86,615 | Web crawler/scraper that turns sites into clean, LLM-ready Markdown. Data ingestion quality remains a practical differentiator for RAG and agents. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | Python | 68,117 | Drop-in memory layer for AI agents and apps with persistent context built for production. It is a key reference point as memory becomes a standard agent requirement. |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | JavaScript | 67,762 | Local-first agent and RAG experience for owning your intelligence. It appeals to teams wanting private, self-hosted knowledge and agent workflows. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | Go | 46,538 | High-performance cloud-native vector database for scalable ANN search. It remains core infrastructure for retrieval-heavy AI systems. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | Rust | 35,343 | High-performance vector database and vector search engine for next-generation AI. Rust-based vector infrastructure continues to attract production RAG teams. |

## 3. Trend Signal Analysis

The strongest signal today is the packaging of agent behavior. Memory/context projects such as [claude-mem](https://github.com/thedotmack/claude-mem), [mem0](https://github.com/mem0ai/mem0), and [Graphify](https://github.com/Graphify-Labs/graphify) and skills repositories such as [anthropics/skills](https://github.com/anthropics/skills) and [obra/superpowers](https://github.com/obra/superpowers) are proliferating because raw model access is no longer the bottleneck; reliability, reuse, and session continuity are. Coding-agent UX is also booming: [impeccable](https://github.com/pbakaus/impeccable) (+2,300), [JetBrains/thinkrail](https://github.com/JetBrains/thinkrail) (+722), and [OpenBot](https://github.com/CopilotKit/OpenBot) (+706) show users want controllable workbenches, design/review vocabularies, and isolated computer environments for agents. Vertical agents are moving from demos to full workflows—[career-ops](https://github.com/career-ops-hq/career-ops), [ppt-master](https://github.com/hugohe3/ppt-master), and [DeepTutor](https://github.com/HKUDS/DeepTutor)—often with dashboards, scheduled runs, and human approval steps. On the stack side, Rust/Zig/Go appear repeatedly in AI infrastructure and vector search, while “skills” are typically Shell/Python/TypeScript artifacts. The data also shows multi-client interoperability: projects explicitly support Claude Code, Codex, Gemini, Copilot, OpenCode, Hermes, and AG-UI. This aligns with the shift toward agent harnesses, tool protocols, local-first inference ([ollama](https://github.com/ollama/ollama)), and context compression/token efficiency ([headroom](https://github.com/headroomlabs-ai/headroom)). Security is a smaller but sharp signal: the [jailbreaks](https://github.com/togg53192-cmd/jailbreaks) list’s +2,055 indicates red-teaming is becoming mainstream alongside agent adoption.

## 4. Community Hot Spots

- **Agent skills as versioned behavior:** [anthropics/skills](https://github.com/anthropics/skills), [mattpocock/skills](https://github.com/mattpocock/skills), and [obra/superpowers](https://github.com/obra/superpowers). Skills are becoming the reusable unit for coding-agent methodology; watch for registries, evaluation, and cross-client compatibility.
- **Persistent context and memory layers:** [claude-mem](https://github.com/thedotmack/claude-mem), [mem0](https://github.com/mem0ai/mem0), and [Graphify](https://github.com/Graphify-Labs/graphify). Memory and graph/context retrieval are moving from feature to infrastructure; token compression and explainable retrieval are key differentiators.
- **AI coworker runtimes with isolated computers:** [OpenBot](https://github.com/CopilotKit/OpenBot), [OpenMausBot](https://github.com/milind-soni/OpenMausBot), and [lightpanda-io/browser](https://github.com/lightpanda-io/browser). Agents with their own VM/browser/files are a concrete next step beyond chat; isolation and auditability will matter.
- **Vertical agents with human approval:** [career-ops](https://github.com/career-ops-hq/career-ops), [ppt-master](https://github.com/hugohe3/ppt-master), and [DeepTutor](https://github.com/HKUDS/DeepTutor). These show end-to-end workflows with scoring, generation, dashboards, and submit/approval steps.
- **Agent quality and review tooling:** [impeccable](https://github.com/pbakaus/impeccable), [affaan-m/ECC](https://github.com/affaan-m/ECC), and [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom). As agents write more code and output, design vocabularies, harness optimization, and context compression become leverage points.