# AI 开源趋势日报 2026-10-31

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-10-31 00:15 UTC

---

**筛选说明：** 仅纳入与 AI 相关的仓库。模糊或非 AI 的热门条目已排除。Star 数按所提供数据复现；仅因趋势上榜的仓库在只有今日新增数据时显示总数 `0`。

## 1. 今日亮点

智能体上下文与技能是最明显的重心：[claude-mem](https://github.com/thedotmack/claude-mem) 今日新增 +1,140，而 [anthropics/skills](https://github.com/anthropics/skills)、[mattpocock/skills](https://github.com/mattpocock/skills) 和 [obra/superpowers](https://github.com/obra/superpowers) 均登上趋势榜，指向持久记忆与可复用智能体行为正成为新的封装层。代码生成质量工具出现了最强的单点飙升：[impeccable](https://github.com/pbakaus/impeccable) 以 +2,300 领跑 AI 趋势榜，[JetBrains/thinkrail](https://github.com/JetBrains/thinkrail)（+722）、[OpenBot](https://github.com/CopilotKit/OpenBot)（+706）和 [OpenMausBot](https://github.com/milind-soni/OpenMausBot)（+895）则强化了对可控编码智能体工作台的需求。垂直 AI 同事持续把演示转化为工作流：[DeepTutor](https://github.com/HKUDS/DeepTutor)（+2,282）、[career-ops](https://github.com/career-ops-hq/career-ops)（78,898 个 Star）、[ppt-master](https://github.com/hugohe3/ppt-master)（71,314），以及股票/交易智能体展示了端到端任务承接能力。检索与上下文基础设施仍保持大规模：[Graphify](https://github.com/Graphify-Labs/graphify)（139,472）、[RAGFlow](https://github.com/infiniflow/ragflow)（93,222）、[mem0](https://github.com/mem0ai/mem0)（68,117），向量数据库则让 RAG/记忆继续处于技术栈中心。LLM 安全/提示词工程也开始浮现：[jailbreaks](https://github.com/togg53192-cmd/jailbreaks) 今日新增 +2,055，这一信号表明红队测试与护栏测试正进入主流智能体开发。

## 2. 按类别划分的热门项目

### 🔧 AI 基础设施

| 项目 | 语言 | Star 数（总数 / 今日） | 简介 |
| :--- | :--- | ---: | :--- |
| [ollama/ollama](https://github.com/ollama/ollama) | Go | 185,380 | 面向 Kimi、GLM、MiniMax、DeepSeek、gpt-oss、Qwen、Gemma 等模型的本地模型运行器。其高 Star 基数和广泛模型支持，使其持续成为智能体与 RAG 技术栈的默认本地推理层。 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | JavaScript | 293,402 | 智能体运行框架性能优化系统，覆盖技能、本能、记忆、安全以及研究优先的开发方式，支持 Claude Code、Codex、OpenCode、Cursor 等。其庞大的 Star 数表明，人们对让编码智能体更可靠、更高效有强烈兴趣。 |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | Python | 78,383 | 在进入 LLM 之前压缩工具输出、日志、文件和 RAG 分块，据称可为编码智能体减少 20% token，对 JSON 减少 60–95%。Token/上下文压缩正成为核心基础设施关注点。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | TypeScript | 38,401 | 面向智能体与生成式 UI 的前端技术栈，覆盖 React、Angular、移动端、Slack 等；同时是 AG-UI Protocol 的维护者。它正将智能体用户体验与协议互操作性定位为核心基础设施。 |
| [lightpanda-io/browser](https://github.com/lightpanda-io/browser) | Zig | 0 (+626) | 为 AI 与自动化设计的无头浏览器。随着浏览器自动化成为智能体的瓶颈，其 Zig 实现和 AI 优先的定位使其值得关注。 |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Rust | 0 (+2,300) | 面向编码智能体的设计词汇，提供 “polish”、“critique” 和 “audit” 等命令，在交付前捕捉 AI 粗制滥造内容。它按新增 Star 数领跑今日 AI 趋势榜，显示围绕编码智能体的质量控制层存在需求。 |
| [anthropics/skills](https://github.com/anthropics/skills) | Python | 0 (+295) | Agent Skills 的公共仓库。它释放出一个信号：技能正成为智能体行为的封装单元，而不再只是临时提示词。 |
| [mattpocock/skills](https://github.com/mattpocock/skills) | Shell | 0 (+876) | 面向“真正的工程师”的技能，从 .agents 目录发布。其势头反映出，可移植、带版本管理的智能体技能正与官方及社区集合一同兴起。 |

### 🤖 AI 智能体 / 工作流

| 项目 | 语言 | Star 数（总数 / 今日） | 简介 |
| :--- | :--- | ---: | :--- |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | Python | 258,876 | “与你共同成长的智能体”，一个拥有庞大 Star 基数的智能体项目。其位居 ai-agent 主题结果榜首，表明人们对通用、自适应智能体的兴趣持续存在。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | Python | 187,839 | 长期运行的开源智能体平台，目标是让 AI 自动化更易获得。尽管出现了更新的框架，它仍是智能体生态中高可见度的锚点。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | Python | 148,740 | 智能体工程平台，提供广泛的模型/工具集成。它持续作为智能体与工作流构建者的默认集成层。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | Python | 119,600 | 用于 AI 浏览器智能体的 Python 库，另提供带隐身浏览器的托管云选项。浏览器控制仍是最实用的智能体能力之一。 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | Python | 106,816 | 通过一个 CLI 让智能体以零 API 费用读取/搜索 Twitter、Reddit、YouTube、GitHub、Bilibili 和 XiaoHongShu。它解决了智能体研究与监控中的数据访问瓶颈。 |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | Python | 44,185 | 通过基于图的编排构建高韧性智能体。它仍是生产级智能体工作流的主流框架。 |
| [CopilotKit/OpenBot](https://github.com/CopilotKit/OpenBot) | TypeScript | 0 (+706) | 开源 AI 同事，每个都获得一台计算机——浏览器、文件、工具——行动在执行前决定、执行后记录；可接入任意 AG-UI 智能体。它今日登上趋势榜，成为一个具体的“AI 同事”运行时。 |
| [obra/superpowers](https://github.com/obra/superpowers) | Shell | 0 (+1,259) | 智能体技能框架与软件开发方法论。其强劲的新增 Star 增长表明，方法论与可复用技能正变得和原始智能体框架同样重要。 |

### 📦 AI 应用

| 项目 | 语言 | Star 数（总数 / 今日） | 简介 |
| :--- | :--- | ---: | :--- |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | Python | 157,293 | 用户友好的 AI 界面，支持 Ollama、OpenAI API 等。它仍是 Star 数最高的自托管 AI 前端之一。 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | Python | 136,606 | 使用 AI 模型和自动化工作流，根据主题或关键词生成高清短视频。它显示出对开箱即用的生成式视频流水线的持续需求。 |
| [career-ops-hq/career-ops](https://github.com/career-ops-hq/career-ops) | JavaScript | 78,898 | 开源 AI 求职智能体，可扫描招聘板、按 CV 为职位评分、定制简历/求职信并跟踪申请。它是垂直智能体承接端到端工作流的清晰示例。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | Python | 71,314 | 将文档或主题转换为原生 PowerPoint 演示文稿，包含形状、切换效果、图表、旁白和自定义模板。它面向高价值办公工作流，输出原生格式而非幻灯片图片。 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | Python | 67,298 | LLM 驱动的多市场股票分析系统，包含市场数据、新闻、仪表盘和定时通知。金融仍是智能体分析与自动化的重要垂直领域。 |
| [HKUDS/DeepTutor](https://github.com/HKUDS/DeepTutor) | Python | 51,762 (+2,282) | 来自 HKUDS 的终身个性化辅导项目。它是今日 AI 新增 Star 最多的项目之一，凸显教育是快速演进的智能体应用。 |
| [microsoft/qlib](https://github.com/microsoft/qlib) | Python | 49,839 | 面向 AI 的量化投资平台，覆盖 ML 建模、市场动态和 RL，并具备 RD-Agent 自动化能力。它将工业级 AI 工具引入量化研究。 |
| [jeecgboot/JeecgBoot](https://github.com/jeecgboot/JeecgBoot) | Java | 48,347 | 企业级 AI 低代码平台，可根据提示词生成完整系统，并具备 AI 聊天、知识库、工作流和 MCP 插件。它显示企业 Java 团队正在采用 AI 辅助开发和智能体低代码。 |

### 🧠 LLM / 训练

| 项目 | 语言 | Star 数（总数 / 今日） | 简介 |
| :--- | :--- | ---: | :--- |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | C++ | 201,234 | 面向所有人的开源机器学习框架。其规模和生态使其成为 ML 训练与部署的基线。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | Python | 168,374 | 面向最先进文本、视觉、音频和多模态模型的模型定义框架，用于推理与训练。它仍是开放模型实现的核心枢纽。 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | Jupyter Notebook | 107,569 | 在 PyTorch 中逐步实现类 ChatGPT LLM。随着更多开发者构建和微调模型，它持续是高质量的教育资源。 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | Python | 105,030 | 具备强 GPU 加速的张量与动态神经网络。它仍是许多开放模型的主导训练/研究技术栈。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | Python | 64,665 | 约两小时内从零训练一个 64M 参数的 LLM。它让端到端 LLM 训练在实验场景中变得异常容易上手。 |
| [keras-team/keras](https://github.com/keras-team/keras) | Python | 64,399 | 面向人类的深度学习，提供跨后端的高级 API。它对于快速原型开发和生产级 ML 仍然重要。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | Python | 7,559 | LLM 评估平台，支持 OpenAI、Anthropic、Gemini、Qwen、GLM、DeepSeek 和 100+ 数据集。随着模型选择和智能体可靠性变得重要，评估正日益关键。 |
| [togg53192-cmd/jailbreaks](https://github.com/togg53192-cmd/jailbreaks) |  | 0 (+2,055) | 公开的越狱提示词列表，今日获得强烈关注。它不是一个生产框架，但清晰表明社区对 LLM 红队测试、护栏和提示词安全的关注。 |

### 🔍 RAG / 知识

| 项目 | 语言 | Star 数（总数 / 今日） | 简介 |
| :--- | :--- | ---: | :--- |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | Python | 139,472 | 通过面向 Claude Code、Cursor、Codex 和 Gemini CLI 的 /graphify 技能，将代码库、文档、SQL schema、配置和 PDF 转换为可查询的知识图谱。其无向量存储、边可解释的方法是一种值得注意的 RAG 替代方案。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | TypeScript | 106,218 (+1,140) | 捕获智能体会话活动，用 AI 压缩，并将相关上下文注入未来的会话，覆盖 Claude Code、Codex、Gemini、Copilot 等。今日的强劲增长使持久智能体记忆成为最清晰的趋势之一。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | Go | 93,222 | RAG 引擎，将检索增强生成与智能体能力融合，为 LLM 创建上下文层。它仍是领先的开源 RAG 平台。 |
| [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) | Python | 86,615 | 网页爬虫/抓取器，可将网站转换为干净、可供 LLM 使用的 Markdown。数据摄取质量仍是 RAG 和智能体的实际差异化因素。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | Python | 68,117 | 面向 AI 智能体和应用的即插即用记忆层，具备为生产环境构建的持久上下文。随着记忆成为智能体的标准需求，它是关键参考点。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | JavaScript | 67,762 | 本地优先的智能体与 RAG 体验，让你掌控自己的智能。它吸引希望拥有私有、自托管知识和智能体工作流的团队。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | Go | 46,538 | 高性能云原生向量数据库，用于可扩展的 ANN 搜索。它仍是检索密集型 AI 系统的核心基础设施。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | Rust | 35,343 | 面向下一代 AI 的高性能向量数据库和向量搜索引擎。基于 Rust 的向量基础设施持续吸引生产级 RAG 团队。 |

## 3. 趋势信号分析

今日最强的信号是智能体行为的封装。记忆/上下文项目，如 [claude-mem](https://github.com/thedotmack/claude-mem)、[mem0](https://github.com/mem0ai/mem0) 和 [Graphify](https://github.com/Graphify-Labs/graphify)，以及技能仓库，如 [anthropics/skills](https://github.com/anthropics/skills) 和 [obra/superpowers](https://github.com/obra/superpowers)，正在激增，因为原始模型访问不再是瓶颈；可靠性、复用和会话连续性才是。编码智能体用户体验也在蓬勃发展：[impeccable](https://github.com/pbakaus/impeccable)（+2,300）、[JetBrains/thinkrail](https://github.com/JetBrains/thinkrail)（+722）和 [OpenBot](https://github.com/CopilotKit/OpenBot)（+706）表明用户想要可控工作台、设计/评审词汇，以及为智能体提供隔离的计算机环境。垂直智能体正从演示走向完整工作流——[career-ops](https://github.com/career-ops-hq/career-ops)、[ppt-master](https://github.com/hugohe3/ppt-master) 和 [DeepTutor](https://github.com/HKUDS/DeepTutor)——通常带有仪表盘、定时运行和人工审批步骤。在技术栈一侧，Rust/Zig/Go 在 AI 基础设施和向量搜索中反复出现，而“技能”通常是 Shell/Python/TypeScript 制品。数据还显示出多客户端互操作性：项目明确支持 Claude Code、Codex、Gemini、Copilot、OpenCode、Hermes 和 AG-UI。这与向智能体运行框架、工具协议、本地优先推理（[ollama](https://github.com/ollama/ollama)）以及上下文压缩/token 效率（[headroom](https://github.com/headroomlabs-ai/headroom)）的转变相一致。安全是一个较小但鲜明的信号：[jailbreaks](https://github.com/togg53192-cmd/jailbreaks) 列表的 +2,055 表明红队测试正随着智能体采用而成为主流。

## 4. 社区热点

- **作为版本化行为的智能体技能：** [anthropics/skills](https://github.com/anthropics/skills)、[mattpocock/skills](https://github.com/mattpocock/skills) 和 [obra/superpowers](https://github.com/obra/superpowers)。技能正成为编码智能体方法论的可复用单元；关注注册表、评估和跨客户端兼容性。
- **持久上下文与记忆层：** [claude-mem](https://github.com/thedotmack/claude-mem)、[mem0](https://github.com/mem0ai/mem0) 和 [Graphify](https://github.com/Graphify-Labs/graphify)。记忆和图/上下文检索正从功能转向基础设施；token 压缩和可解释检索是关键差异化因素。
- **带隔离计算机的 AI 同事运行时：** [OpenBot](https://github.com/CopilotKit/OpenBot)、[OpenMausBot](https://github.com/milind-soni/OpenMausBot) 和 [lightpanda-io/browser](https://github.com/lightpanda-io/browser)。拥有自己的 VM/浏览器/文件的智能体是超越聊天的一个具体下一步；隔离与可审计性将很重要。
- **带人工审批的垂直智能体：** [career-ops](https://github.com/career-ops-hq/career-ops)、[ppt-master](https://github.com/hugohe3/ppt-master) 和 [DeepTutor](https://github.com/HKUDS/DeepTutor)。它们展示了包含评分、生成、仪表盘以及提交/审批步骤的端到端工作流。
- **智能体质量与评审工具：** [impeccable](https://github.com/pbakaus/impeccable)、[affaan-m/ECC](https://github.com/affaan-m/ECC) 和 [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)。随着智能体编写更多代码和输出，设计词汇、运行框架优化和上下文压缩成为杠杆点。

---