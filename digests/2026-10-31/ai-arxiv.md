# ArXiv AI 研究日报 2026-10-31

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-10-31 00:15 UTC

---

## 今日亮点

今日的论文显示出一种强烈的趋势：通过统一的训练目标、token级自蒸馏、多路由MoE和多轮防御，使LLM训练、安全性和归因更加系统化。智能体研究正超越任务演示，迈向自主科学实验、计算机使用验证、持久检索记忆和可扩展监督。方法工作亮点包括更好的隐私-效用权衡、对神经丛解释的重新评估，以及离散扩散的确定性采样器。应用继续将基础模型扩展到EHR风险预测、机制性世界模型和低成本机器人仿真。

## 重点论文

### 🧠 大型语言模型（架构、训练、对齐、评估）

| 论文 | 作者 | 摘要 |
| :--- | :--- | :--- |
| [Elucidating the Design Space of LM Data Attribution](http://arxiv.org/abs/2610.40655v1) | Steven Yu, Sheng-Yu Wang, Kimia Hamidieh et al. | 系统性地分离出影响LM数据归因评估的数据集属性，揭示方法失败的原因并实现受控基准测试。其重要性在于可靠的归因是来源追踪、版权和训练数据审计的基础。 |
| [ShallowDefend: Harnessing Shallow Safety Alignment for Multi-Turn Defender](http://arxiv.org/abs/2610.40627v1) | Qiyao Ma, Xiaodong Liu, Weiwei Yang et al. | 表明多轮安全失败源于集中在模型早期行为中的浅层对齐，并提出ShallowDefend利用该浅层对齐作为多轮防御器。其重要性在于封堵了单轮对齐无法覆盖的实际越狱路径。 |
| [Multi-View MoE: Letting Every Router Shape Expert Computation](http://arxiv.org/abs/2610.40577v1) | Zelin Zhao, Tianchi Ma, Junyuan Shang et al. | 提出Multi-View MoE，其中每个路由器贡献一个视图来选择和塑造专家计算，而非依赖单一路由器排序。它在固定活跃专家预算下提升了专家利用率和能力，对稀疏MoE扩展具有重要意义。 |
| [Every Token Needs Its Own Teacher: Multi-teacher Adaptive On-policy Self-distillation](http://arxiv.org/abs/2610.40574v1) | Yifu Luo, Chuang Ma, Zeyu Chen et al. | 提出自适应多教师在线策略自蒸馏，为每个token分配一个以其特权参考为条件的专属教师，而非固定教师。它通过将监督与token级学习需求匹配来改善LLM的后训练信号。 |
| [Training Foundation Models with a Single Algorithm](http://arxiv.org/abs/2610.40564v1) | Yuda Song, Alvin Zhang, Fahim Tajwar et al. | 在单一算法框架下将预训练、中期训练、SFT和RL推导为最大似然/RL目标，挑战分阶段的基础模型训练。如果可行，它可能简化流水线并统一数据和目标设计。 |

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

| 论文 | 作者 | 摘要 |
| :--- | :--- | :--- |
| [Collaborative AI agents for autonomous experimental research with solid-state quantum spins](http://arxiv.org/abs/2610.40589v1) | El Mustapha Mansouri, Eikichi Kimura, Masato Koga et al. | 展示协作AI智能体自主开展固态量子自旋实验研究，从问题构建到稿件准备。这是对多智能体科学自主性的一次具体测试，具有领域特定的验证需求。 |
| [VeriCUA: Verification as Agentic Exploration for Computer-Using Agents](http://arxiv.org/abs/2610.40578v1) | Qiushi Sun, Da Yu, Alexander Knop et al. | 提出VeriCUA，将计算机使用智能体轨迹的验证视为智能体探索而非单一VLM判断。它面向桌面、移动和网页智能体的可靠数据构建、评估和RL。 |
| [Retrieval as Traversal: Value-Indexed Memory for Stateful Long-Context Agents](http://arxiv.org/abs/2610.40545v1) | Daniel Strauß, Zhenshan Bing, Alois Knoll | 提出值索引记忆和遍历式检索，使长上下文智能体能够复用先前的检索决策，而非每次前向传播都重新扫描全部存储。这对于反复解决密切相关检索任务的有状态智能体具有重要意义。 |
| [Efficient Scalable Oversight via Rewinding](http://arxiv.org/abs/2610.40535v1) | Ziyi Guan, Yael Tauman Kalai, Ron Rothblum et al. | 利用相对化交互证明中的回卷重新构建可扩展监督，使弱验证者能够更高效地检查强大的AI计算。它提供了一条理论和算法路径，使监督在模型能力增长时仍然可靠。 |

### 🔧 方法与框架（新技术、基准、效率改进）

| 论文 | 作者 | 摘要 |
| :--- | :--- | :--- |
| [Propose-Filter-Release: Scaling Noise to Typical Sensitivity via Private Filtering](http://arxiv.org/abs/2610.40654v1) | Moshe Shenfeld, Eliad Tsfadia, Katrina Ligett | 提出Propose-Filter-Release，一种通过过滤罕见高影响记录将噪声缩放到典型而非最坏情况敏感度的隐私过滤机制。它可以改善具有少量敏感离群值的估计器的精度-隐私权衡。 |
| [Rethinking Neural Thickets Without Weight Perturbations](http://arxiv.org/abs/2610.40649v1) | Nicolas Dufour, Elouan Gardès, Amil Dravid et al. | 复现了随机权重扰动所报告的神经丛增益，并表明它们不需要所提出的几何解释。该结果提醒人们不要将权重空间扰动增益解释为稠密专家邻域的证据。 |
| [An ODE-based Sampler for Discrete Diffusion Models](http://arxiv.org/abs/2610.40618v1) | Samson Gourevitch, Yazid Janati, Eric Moulines et al. | 为离散扩散模型开发了一种基于ODE的采样器，类似于连续概率流ODE。它可能为离散生成模型实现更快的确定性采样和一致性蒸馏。 |

### 📊 应用（领域特定、多模态、代码生成）

| 论文 | 作者 | 摘要 |
| :--- | :--- | :--- |
| [world2vec: Mechanistic world models through latent dynamics learning](http://arxiv.org/abs/2610.40637v1) | Tobias Schmidt, Rodrigo Gonzalez Laiz, Krisztián Szuppinger et al. | 提出world2vec，直接从潜在动力学学习机制性世界模型，无需奖励信息。它旨在提升基于模型的控制中的可解释性和科学发现。 |
| [TRACER, a time-to-event EHR foundation model for disease detection across health systems](http://arxiv.org/abs/2610.40536v1) | Mara Pleasure, Ekaterina Redekop, Vedrana Ivezic et al. | 提出TRACER，一种基于解码器的time-to-event EHR基础模型，在纵向记录上预训练，用于跨健康系统的疾病检测。它对临床基础模型的筛查和可迁移性具有重要意义。 |
| [BURGER: Benchmarking and Understanding Robotic Generalization via Embodied Drawing](http://arxiv.org/abs/2610.40532v1) | Xiangyu Xu, Bangshuai Peng, Ziyi Liu et al. | 提出BURGER，一个语言条件机器人绘画基准和数据生成设置，用于研究VLA泛化随训练数据规模的变化。它通过实现可扩展的具身评估来解决物理机器人数据成本问题。 |

## 研究趋势信号

一个明确的信号是：从孤立的模型改进转向可验证的、覆盖全生命周期的系统。LLM论文聚焦于归因、多轮安全和统一训练目标，反映出使训练数据、对齐和后训练可审计的压力。智能体工作正汇聚于评估和监督基础设施——轨迹验证、即将违规行为的探测、基于回卷的可扩展监督和持久检索记忆——而非仅仅任务演示。效率仍然通过稀疏MoE路由、token级蒸馏和确定性采样器保持核心地位。领域应用越来越多地使用基础模型作为骨干，包括EHR time-to-event模型、机制性世界模型和机器人仿真。总体而言，该领域似乎正趋向成熟，走向不仅有能力而且可检查、可复用、可在现实数据和安全约束下部署的系统。

## 值得深读

- **[Training Foundation Models with a Single Algorithm](http://arxiv.org/abs/2610.40564v1)** — 可能将标准的预训练到RL流水线重新构建为一个算法家族；对研究和工程实践都具有高杠杆作用。
- **[Efficient Scalable Oversight via Rewinding](http://arxiv.org/abs/2610.40535v1)** — 将复杂性理论与AI监督相结合，可能影响弱验证者监督更强系统的方式。
- **[Elucidating the Design Space of LM Data Attribution](http://arxiv.org/abs/2610.40655v1)** — 为一个众所周知存在混杂因素的评估领域提供了诊断框架，对审计和数据来源追踪具有直接影响。