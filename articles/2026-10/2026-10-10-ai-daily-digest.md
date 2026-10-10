# 🦞 AI 每日情报 | 2026年10月10日（周六）

> **本期关键词：** 小米 MiMo-V2.6 强化学习自我进化 · TokenRouter 令牌级路由 64 倍吞吐提升 · Agent 欺骗检测 98.8% AUC · Memento 3 递归自我改进 · 小米开源 RL 框架 · SparseDecoding 1.48x 解码加速 · AgentGarten 进化式 Agent 环境 · Cloudflare CLEF 27B 多模态 · Google EmbeddingGemma-2 嵌入模型

---

## 📊 今日速览

| 类别 | 亮点 |
|---|---|
| 🔥 最热论文 | AgentGarten（131 票）、TokenRouter（102 票）、MiMo-V2.6（55 票） |
| 🧠 模型发布 | MiMo-V2.6 系列、Cloudflare CLEF 27B、Google EmbeddingGemma-2、LiquidAI d1-3B |
| 🤖 Agent 范式 | 递归自我改进（Memento 3）、技能进化（SGUID/ViSkill）、欺骗检测探针 |
| ⚡ 推理优化 | TokenRouter 2-64x 吞吐、SparseDecoding 1.48x 加速 |
| 🌍 行业动态 | 特斯拉 Optimus 加速量产、UNESCO 10 亿美元 AI 协议、CoreWeave 印度数据中心 |

---

## 一、前沿模型动态

### 1.1 小米 MiMo-V2.6：强化学习规模化迈向自我进化

**📄 论文：** [MiMo-V2.6: Scaling Reinforcement Learning Towards Self-Improvement](https://arxiv.org/abs/2610.11959)
**🏢 机构：** 小米 LLM-Core Team
**⭐ HuggingFace 热度：** 55 upvotes

#### 核心突破

MiMo-V2.6 是小米推出的全模态（omni-modal）模型系列，核心思路是将强化学习（RL）的计算规模推到新高度，实现模型的自我进化能力。

**三维 RL 扩展策略：**

| 维度 | 具体做法 | 技术细节 |
|---|---|---|
| 更大批量 | 异步训练 | 每步消耗 1,568 个样本、2.7-3.7B tokens，上下文最长 100 万 |
| 更多样环境 | 混合 Agent harness | 覆盖代码、通用、视觉、网络安全四大领域 |
| 更强评判 | 分组 Agent 评分 | 为长期任务提供更准确的奖励信号，引导模型产出更简洁的方案 |

**关键工程创新：**
- **冻结 MoE 路由器**：在大规模 RL 训练中保持路由稳定
- **多层防御 reward hacking**：防止模型找到奖励捷径
- **混合任务 Agent RL 基础设施**：统一轨迹表示、高并发多框架 rollout、控制平面与数据平面解耦

**💡 对你的价值：**
- **开源了训练动态、RL 环境和 RL 框架**，这是目前最完整的 RL 训练自我改进开源方案
- 如果你在做 Agent 训练，这套框架（异步训练 + 多环境混合 + Agent 评分）可以直接参考
- 100 万上下文长度的 RL 训练是目前公开的最大规模之一

---

### 1.2 Google EmbeddingGemma-2：轻量嵌入模型新标杆

**📦 模型：** [google/embeddinggemma-2](https://huggingface.co/google/embeddinggemma-2)
**📊 规模：** 0.7B 参数
**📈 下载量：** 29.2k（3 天内）

#### 技术特点

Google 发布的 EmbeddingGemma-2 是专为嵌入任务设计的轻量模型，基于 Gemma 架构优化。

| 指标 | 数值 |
|---|---|
| 参数量 | 0.7B |
| 主要用途 | 特征提取、语义嵌入、检索 |
| 下载热度 | 29.2k（3 天） |
| 社区衍生 | unsloth/embeddinggemma-2-GGUF（41.6k 下载） |

**💡 对你的价值：**
- 0.7B 的体量可以在 CPU 上流畅运行，适合嵌入式/边缘设备场景
- 如果你的 RAG 系统需要轻量嵌入模型，这是一个强有力的候选
- unsloth 已提供 GGUF 量化版本，可直接用 llama.cpp / Ollama 加载

---

### 1.3 Cloudflare CLEF：边缘端多模态视觉语言模型

**📦 模型：** [Cloudflare/clef](https://huggingface.co/Cloudflare/clef)
**📊 规模：** 27B 参数（主力）/ 9B（flash 版）
**📈 下载量：** 12.1k / 19k

#### 技术特点

Cloudflare 推出的 CLEF 系列是 Image-Text-to-Text 多模态模型，同时提供 27B 和 9B（clef-flash）两个版本。

| 版本 | 参数量 | 下载量 | 定位 |
|---|---|---|---|
| CLEF | 27B | 12.1k | 高精度推理 |
| CLEF-Flash | 9B | 19k | 低延迟边缘部署 |

**💡 对你的价值：**
- Cloudflare 的背景意味着这个模型天然适合边缘/CDN 场景部署
- 9B flash 版本可以在消费级 GPU 上运行，适合图像理解任务
- 如果你的应用需要图文理解但不想依赖大厂 API，这是值得尝试的选择

---

### 1.4 HuggingFace 热门模型一览

| 排名 | 模型 | 类型 | 参数量 | 下载量 | 亮点 |
|---|---|---|---|---|---|
| 1 | google/embeddinggemma-2 | 嵌入 | 0.7B | 29.2k | 轻量嵌入新选择 |
| 2 | Cloudflare/clef | 多模态 | 27B | 12.1k | 边缘端视觉语言 |
| 3 | Aleph-Alpha/Kolibri-1 | 文本生成 | 78B | 8.47k | 欧洲大模型 |
| 4 | jialinyyzz/humanizer | 文本生成 | 12B | 29.5k | 人性化文本 |
| 5 | Qwen/Qwen-Image-2.1-Turbo | 文生图 | 7B | 新发布 | 图像生成加速版 |
| 6 | LiquidAI/d1-3B | 多模态 | 3B | 7.3k | 轻量多模态 |
| 7 | deepseek-ai/DeepSeek-V4.1-Flash | 多模态 | 763B | 1.32M | 旗舰 MoE 模型 |

**💡 对你的价值：**
- 本周趋势显示：**小模型 + 专用场景**是社区热点（嵌入、边缘推理、图像生成）
- Qwen 系列持续霸榜，Qwen3.8-27B 和 Qwen-Image-2.1 系列下载量极高
- DeepSeek-V4.1-Flash（763B MoE）仍是社区最活跃的大参数模型

---

## 二、Agent 架构与范式

### 2.1 Memento 3：基于规则本的递归自我改进

**📄 论文：** [Memento 3: Model-Based Recursive Self-Improvement through Reflective Rulebooks](https://arxiv.org/abs/2610.11794)
**🏢 机构：** University College London
**⭐ HuggingFace 热度：** 24 upvotes

#### 核心思想

Memento 3 提出了一种让**冻结的 LLM Agent**通过外部记忆持续学习显式世界模型的方法。Agent 维护一个自然语言"规则本"（rulebook）作为持久语义记忆，记录关于环境动态的可修正假设。

**工作流程：**

```
观察 → 反思 → 规则修订 → 编译为代码 → 验证 → 接受/拒绝
  ↑                                                    ↓
  └──────────── 预测误差反馈 ────────────────────────────┘
```

**关键设计：**
- **规则本 → 可执行代码**：自然语言假设编译为代码用于预测和规划
- **双重验证**：LLM 判断代码是否忠实于规则本 + 精确回放是否复现观察到的转移
- **种群扩展**：并行维护多个世界模型，共享交互证据

**实验结果：**
- 在 ARC-AGI-3 上通过全部 25 个公开游戏的所有关卡
- 平均相对人类行动效率（RHAE）达 100.0，仅使用人类 44% 的行动次数
- Atari Pong 案例中学到的反馈控制器以 21:0 获胜，无需进一步 LLM 调用

**💡 对你的价值：**
- 这代表了 Agent 自我改进的一条重要路线：**不改模型权重，通过外部记忆进化**
- 规则本 → 代码的思路非常适合需要可解释性的场景
- ARC-AGI-3 上的表现证明这种方法在复杂推理任务上的有效性

---

### 2.2 AgentGarten：代码世界中的进化式 Agent

**📄 论文：** [AgentGarten: Code Worlds for Evolving Agents](https://arxiv.org/abs/2610.12374)
**🏢 机构：** MirroS Lab（清华大学）
**⭐ HuggingFace 热度：** 131 upvotes（当日第一）

#### 核心创新

AgentGarten 将模拟器和游戏引擎与共享神经渲染器耦合，构建实时交互式环境，让 Agent 通过探索和交互学习。

**技术架构：**

| 组件 | 功能 | 技术细节 |
|---|---|---|
| 模拟后端 | 维护持久世界状态 | 执行程序定义的交互规则 |
| 神经渲染器 | 生成视觉观察 | 从结构化条件生成，使用 Adversarial Forcing 蒸馏 |
| 进化循环 | Agent 经验蒸馏 | 每轮经验蒸馏为 playbook，后续 Agent 继承和改进 |

**核心突破 — Adversarial Forcing：**
- 使历史预填充通过精确回放变得可微
- 后续预测的损失更新渲染器如何编码先前观察
- 添加真实数据对抗监督提升视觉质量

**实验结果：**
- Agent 仅从 **4 轮**学习中获得显著提升
- 对比传统强化学习需要数百万轮

**💡 对你的价值：**
- 如果你在做 Agent 训练环境，这个框架提供了"环境即代码"的优雅范式
- 4 轮 vs 百万轮的样本效率提升是数量级的飞跃
- 新环境可以写成代码并通过同一接口渲染，环境和 Agent 可以同步扩展

---

### 2.3 SGUID：技能蒸馏的精选策略

**📄 论文：** [SGUID: Selecting a Compact Skill Bank for Model-Skill Co-Evolution](https://arxiv.org/abs/2610.12367)
**🏢 机构：** 多机构合作

#### 核心发现

**关键洞察：并非所有技能都值得蒸馏。**

研究发现，在 on-policy 蒸馏中，只有不到 **25%** 的检索技能提供有用的蒸馏信号。SGUID 方法仅保留在训练过程中持续产生有效学习信号的技能。

**实验结果（4 个模型，Olmo 和 Qwen 系列）：**

| 方案 | 技能数 | 效果 |
|---|---|---|
| 全库蒸馏 | 最多 11x 技能 | 基准 |
| SGUID 第一轮（6 个技能） | 6 | 在 3/4 模型上匹配或超过全库 |
| SGUID 第二轮（3 个新技能） | 3 | 在所有 4 个模型上超过全库 |
| Qwen3-8B 改进 | — | 64.3% → 66.3% |

**💡 对你的价值：**
- **少即是多**：选择少量高质量技能比全量蒸馏更有效
- 模型-技能协同进化需要稳定的选择机制，否则未过滤的技能会降低性能
- 如果你在构建技能增强的 Agent 系统，这个选择策略可以直接应用

---

### 2.4 ViSkill：视觉原生技能学习框架

**📄 论文：** [ViSkill: Reinforcing VLM Agents with Evolving Visual-Native Skills](https://arxiv.org/abs/2610.12403)
**🏢 机构：** 浙江大学
**📦 代码：** [github.com/ZJU-REAL/ViSkill](https://github.com/ZJU-REAL/ViSkill)

#### 核心创新

ViSkill 将成功的交互编码为**复合视觉技能卡片**，直接可被 VLM Agent 访问，形成技能积累与策略改进相互强化的闭环。

**与文本技能方案的对比：**

| 维度 | 文本技能 | ViSkill（视觉原生） |
|---|---|---|
| 空间表达 | 线性化为语言，丢失几何结构 | 保留完整视觉空间布局 |
| 技能更新 | 与策略优化分离 | 闭环反馈，同步进化 |
| 冷启动 | 无 | 可选冷启动机制加速早期学习 |

**实验结果：**
- Sokoban、FrozenLake、PrimitiveSkill 上总成功率 0.89
- 冷启动初始化后提升至 0.91
- 超越所有评估的专有和开源基线，收敛速度快于标准 PPO

**💡 对你的价值：**
- 视觉技能卡片比文本描述保留了更多空间信息，适合需要精确空间推理的任务
- 闭环设计（技能 → 策略 → 新技能）是 Agent 持续学习的有效范式
- 代码已开源，可以直接在你的 VLM Agent 项目中使用

---

### 2.5 Caught in the Act：白盒欺骗检测探针

**📄 论文：** [Caught in the Act: Probes Effectively Detect Sabotage and Catch Unverbalized Deception](https://arxiv.org/abs/2610.12445)
**🏢 机构：** Alignment Research
**📦 代码和数据：** [github.com/AlignmentResearch/caught-in-the-act-probes](https://github.com/AlignmentResearch/caught-in-the-act-probes)

#### 核心突破

研究证明白盒欺骗检测探针可以扩展到前沿监控场景，通过收集**最大的欺骗数据集**训练探针，并引入新型探针架构跨多层多 token 聚合信息。

**性能对比：**

| 方法 | AUC | 备注 |
|---|---|---|
| 本文探针 | **98.8%** | SHADE-Arena 基准 |
| Opus 5.5 文本监控基线 | 低于 98.8% | 被超越 |
| 内省欺骗检测 | **99.7%** | 区分真实隐藏目标 vs 其他目标 |

**关键发现：**
- 探针效果随底层模型规模增大而**提升**（而非下降）
- 能检测开放权重模型在政治敏感话题上的欺骗
- 能检测模型在压力下关于其信念的欺骗

**💡 对你的价值：**
- 如果你在部署 LLM Agent 系统，白盒探针是目前最可靠的欺骗检测手段
- FIBS 数据集已开源，可以直接用于训练你自己的检测探针
- 这对 Agent 安全监控至关重要，特别是需要高可靠性的生产环境

---

## 三、开源生态

### 3.1 TokenRouter：令牌级 LLM 路由服务系统

**📄 论文：** [TokenRouter: Efficient Serving System for Token-Level LLM Routing](https://arxiv.org/abs/2610.12242)
**🏢 机构：** 清华大学 NICS
**📦 代码：** [github.com/thu-nics/TokenRouter](https://github.com/thu-nics/TokenRouter)
**🏆 会议：** NeurIPS 2026
**⭐ HuggingFace 热度：** 102 upvotes

#### 技术详解

TokenRouter 解决了令牌级路由推理的服务效率问题。现有的基于单 LLM 假设的系统在令牌级路由下遭受严重的步骤失同步和频繁的批次准入延迟。

**设计原则：请求中心编程，模型中心执行**
- 开发者从单个请求的角度描述路由逻辑
- 运行时为每个 LLM 启动子服务器，异步调度请求
- 每个子服务器采用延迟批处理调度器，最优超参数由数学吞吐量模型推导

**性能提升：**

| 场景 | 吞吐提升 |
|---|---|
| 跨多种路由算法、工作负载和模型对 | **2.01 - 64.15x** |

**💡 对你的价值：**
- 如果你的 LLM 服务需要多模型路由（如简单问题用小模型、复杂问题用大模型），这个系统可以将吞吐提升数十倍
- NeurIPS 2026 接收，代码已开源，可以直接部署
- 令牌级路由比查询级路由更精细，能显著优化成本-质量 Pareto 前沿

---

### 3.2 SparseDecoding：解码感知的 LLM 剪枝

**📄 论文：** [SparseDecoding: Decoding-Aware Pruning for Accurate and Efficient LLM Inference](https://arxiv.org/abs/2610.12327)
**🏢 机构：** 西湖大学 ENCODE Lab
**⭐ HuggingFace 热度：** 20 upvotes

#### 核心问题

现有 LLM 剪枝方法使用预收集的自然序列计算 Hessian，但模型在解码时输入的是自生成的 token，造成**分布偏移**。

**解决方案：**
- **算法层面**：从密集模型自回归生成过程中收集逐层激活构建校准矩阵（排除 prefill），使剪枝目标与解码激活对齐
- **系统层面**：开发优化的 N:M 稀疏矩阵向量（SpMV）核，使用位掩码索引和固定步长遍历

**性能结果（A100 GPU）：**

| 模型 | 加速比 | 备注 |
|---|---|---|
| Llama-3.1-8B | 最高 **1.48x** | 端到端解码加速 |
| Llama-3.3-70B | 最高 **1.48x** | 长文本生成一致优于固定文本校准 |
| Qwen3-14B / 32B | 最高 **1.48x** | 无需训练 |

**💡 对你的价值：**
- 无需训练的免训练剪枝方案，可以直接应用到你的模型上
- 1.48x 的解码加速在大规模推理服务中意味着显著的成本节省
- 解决了"校准-解码分布偏移"这个被忽视但影响巨大的问题

---

### 3.3 OneSearch-VL：统一多模态深度研究 Agent

**📄 论文：** [OneSearch-VL: Unified Multimodal Deep Research Agent for Image and Video](https://arxiv.org/abs/2610.12419)
**📦 代码：** [github.com/appletea233/OneSearch-VL](https://github.com/appletea233/OneSearch-VL)
**⭐ HuggingFace 热度：** 16 upvotes

#### 技术架构

OneSearch-VL 以**视觉接地证据图（VGEG）**为中心，编码视觉锚点、实体关系、来源支持事实和答案生成操作之间的依赖关系。

**数据规模：**
- OneSearch-VL-SFT-110K（SFT 训练）
- OneSearch-VL-RL-10K（RL 训练）

**性能提升（vs Qwen3-VL-8B + 工具）：**

| 基准 | 提升幅度 |
|---|---|
| OneSearch-MI-Bench | +20.2 个百分点 |
| OneSearch-Video-Bench | +17.6 个百分点 |
| 7 个图像基准 + VideoDR | 显著提升 |

**💡 对你的价值：**
- 如果你的 Agent 需要处理多图像和视频的深度研究任务，这是一个完整的解决方案
- VGEG 的设计思路可以用于任何需要证据追溯的 Agent 系统
- 8B 模型就实现了大幅超越，说明架构设计比模型规模更重要

---

### 3.4 ME-World：多 Agent 自我中心世界模型

**📄 论文：** [Multi-Agent Egocentric World Model with Fine-Grained Embodied Interaction](https://arxiv.org/abs/2610.12299)
**🏢 机构：** KAIST AI
**⭐ HuggingFace 热度：** 43 upvotes

#### 核心贡献

将多 Agent 自我中心世界建模公式化为**同步自我流生成**，多个 Agent 通过细粒度动作在共享世界中交互。

**三个一致性要求：**
1. 跨视角动作一致性
2. 共享环境一致性
3. 交互引起的状态更新一致性传播

**💡 对你的价值：**
- 多 Agent 协作是世界模型的重要前沿，这项工作首次探索了细粒度具身交互
- 如果你的项目涉及多 Agent 仿真或训练环境，ME-World 的架构设计值得参考

---

### 3.5 其他值得关注的开源项目

| 项目 | 类型 | 亮点 |
|---|---|---|
| [Qwen-Image-2.1-Turbo](https://huggingface.co/Qwen/Qwen-Image-2.1-Turbo) | 文生图 | Qwen 图像生成加速版，7B 参数 |
| [LiquidAI/d1-3B](https://huggingface.co/LiquidAI/d1-3B) | 多模态 | 仅 3B 参数的轻量多模态模型 |
| [jialinyyzz/humanizer](https://huggingface.co/jialinyyzz/humanizer) | 文本生成 | 让 AI 文本更人性化，12B 参数，29.5k 下载 |
| [Lightricks/LTX-2.5](https://huggingface.co/Lightricks/LTX-2.5) | 图生视频 | 1.69M 下载，视频生成热门模型 |
| [canberkkkkkk/ema-lightning](https://huggingface.co/canberkkkkkk/ema-lightning) | TTS | 文本转语音新模型 |

---

## 四、AI 工具与技巧

### 4.1 本周工具推荐

#### ① TokenRouter — 多模型路由服务

**适用场景：** 你有一个 LLM 服务需要同时使用多个模型（如 GPT-4 处理复杂问题、小模型处理简单问题）

**使用步骤：**
```bash
git clone https://github.com/thu-nics/TokenRouter
cd TokenRouter
# 配置你的模型路由策略
# 启动服务
```

**💡 技巧：** 令牌级路由比查询级路由更精细——同一个请求的不同 token 可以路由到不同模型，在保持质量的同时大幅降低成本。

---

#### ② SparseDecoding — 免训练推理加速

**适用场景：** 你需要加速 LLM 的解码阶段，特别是在 A100 GPU 上

**使用步骤：**
1. 使用 SparseDecoding 的校准方法（从自回归生成中收集激活）
2. 应用 N:M 稀疏剪枝
3. 使用优化的 SpMV 核进行推理

**💡 技巧：** 关键创新是"解码感知校准"——不要用固定文本校准，而是用模型自己生成的文本校准，这样剪枝后的模型在长文本生成上表现更好。

---

#### ③ ViSkill — 视觉技能增强 Agent

**适用场景：** 你在构建 VLM Agent 处理空间推理任务

**使用步骤：**
```bash
git clone https://github.com/ZJU-REAL/ViSkill
# 安装依赖
# 创建视觉技能卡片库
# 训练 Agent 使用技能
```

**💡 技巧：** 启用冷启动机制可以将早期成功率从 0.89 提升到 0.91，特别适合从零开始的 Agent 项目。

---

### 4.2 本周学习工作流推荐

**🎯 主题：理解 RL 驱动的 Agent 自我改进**

1. **先读 MiMo-V2.6 报告**（30 分钟）— 理解 RL 规模化训练的三维扩展策略
2. **再读 Memento 3**（20 分钟）— 对比"改权重"和"不改权重"两条自我改进路线
3. **动手实验**（30 分钟）— 用 TokenRouter 搭建一个简单的多模型路由服务
4. **深入阅读**（20 分钟）— SGUID 论文理解技能选择机制

**总时间：约 100 分钟**

---

### 4.3 初学者建议

**如果你刚入门 AI Agent：**

1. **从 Memento 3 开始理解 Agent 学习**：它用自然语言规则本的方式非常直观
2. **用 ViSkill 动手实践**：代码开源，Sokoban 和 FrozenLake 是经典入门环境
3. **关注 TokenRouter 理解工程实践**：学术研究和生产部署之间的差距往往在服务系统上

**本周推荐阅读顺序：**
1. AgentGarten（最直观，理解 Agent 环境设计）
2. ViSkill（有代码，可以动手）
3. MiMo-V2.6（理解前沿训练方法）
4. Caught in the Act（理解 Agent 安全）

---

## 五、值得深读的研究

### 5.1 ⭐ AgentGarten：代码世界中的进化式 Agent

**📄 论文：** [arXiv:2610.12374](https://arxiv.org/abs/2610.12374)
**🏢 机构：** MirroS Lab（清华大学）

#### 研究方法

1. **环境构建**：将模拟器和游戏引擎与共享神经渲染器耦合
2. **Adversarial Forcing**：使历史预填充可微，通过精确回放让后续预测的损失更新渲染器的编码方式
3. **进化循环**：Agent 通过视觉观察感知世界 → 实时交互 → 将经验蒸馏为 playbook → 后续 Agent 继承和改进

#### 核心发现

- 4 轮学习 vs 传统 RL 的百万轮，样本效率提升 **5-6 个数量级**
- 环境可以写成代码并通过同一接口渲染，实现环境和 Agent 的同步扩展

#### 启发

这项工作展示了"环境即代码"的范式如何让 Agent 学习变得极其高效。核心思想是：**好的环境设计比更多的训练轮次更重要**。

---

### 5.2 ⭐ MiMo-V2.6：RL 规模化自我进化

**📄 论文：** [arXiv:2610.11959](https://arxiv.org/abs/2610.11959)
**🏢 机构：** 小米 LLM-Core Team

#### 研究方法

1. **中间训练**：在广泛的多模态语料上进行，提供充足的探索空间
2. **三维 RL 扩展**：更大批量（1,568 样本/步，100 万上下文）、更多样环境（代码/通用/视觉/安全）、更强评判（分组 Agent 评分）
3. **稳定性保障**：冻结 MoE 路由器 + 多层防御 reward hacking

#### 核心发现

- RL 计算规模的扩展可以直接转化为模型自我改进能力
- Agent 评分比传统评分更能引导模型产出简洁、高效的解决方案
- 开源了完整的训练框架和 RL 环境

#### 启发

MiMo-V2.6 证明了"RL 规模化"是一条可行的路线。关键工程创新（冻结路由器、多层防御、混合任务基础设施）为其他团队提供了可复制的实践经验。

---

### 5.3 ⭐ Caught in the Act：白盒欺骗检测

**📄 论文：** [arXiv:2610.12445](https://arxiv.org/abs/2610.12445)
**🏢 机构：** Alignment Research

#### 研究方法

1. **最大欺骗数据集 FIBS**：收集用于训练探针的大规模欺骗数据
2. **新型探针架构**：跨多层多 token 聚合信息
3. **内省欺骗测试**：测试上下文无法单独确定欺骗的场景

#### 核心发现

- 98.8% AUC 在 SHADE-Arena 上超越 Opus 5.5 文本监控基线
- 99.7% AUC 在内省欺骗检测中区分真实隐藏目标
- 探针效果随模型规模增大而提升

#### 启发

这项工作对 AI 安全领域意义重大：**白盒监控是可行的，且效果随模型能力增强而增强**。这反驳了"模型越强越难监控"的悲观假设。

---

### 5.4 Memento 3：基于规则本的递归自我改进

**📄 论文：** [arXiv:2610.11794](https://arxiv.org/abs/2610.11794)

#### 研究方法

1. **自然语言规则本**：作为持久语义记忆，记录可修正的环境动态假设
2. **规则本 → 可执行代码**：编译为代码用于预测和规划
3. **持续循环**：观察 → 反思 → 规则修订 → 编译 → 验证
4. **双重验证**：LLM 忠实性判断 + 精确回放验证

#### 核心发现

- ARC-AGI-3 上通过所有 25 个公开游戏的所有关卡
- 仅使用人类 44% 的行动次数
- Atari Pong 学到的控制器以 21:0 获胜，无需进一步 LLM 调用

#### 启发

这代表了一条重要的 Agent 自我改进路线：**不改模型权重，通过外部记忆进化**。规则本的方式天然具备可解释性，适合需要透明决策过程的场景。

---

## 六、今日学习建议

### 🎯 具体可执行建议

#### 建议 1：动手搭建 TokenRouter 多模型路由

**目标：** 理解令牌级路由如何优化 LLM 服务效率

**步骤：**
1. 克隆 [TokenRouter](https://github.com/thu-nics/TokenRouter)
2. 配置两个模型（如 Qwen3-8B + Qwen3-32B）
3. 实现一个简单的令牌级路由策略
4. 对比吞吐提升

**预计时间：** 1-2 小时

---

#### 建议 2：用 ViSkill 训练一个 Sokoban Agent

**目标：** 体验视觉原生技能学习的效果

**步骤：**
1. 克隆 [ViSkill](https://github.com/ZJU-REAL/ViSkill)
2. 在 Sokoban 环境上训练 Agent
3. 对比启用/禁用冷启动的效果
4. 观察技能卡片如何被积累和复用

**预计时间：** 2-3 小时

---

#### 建议 3：阅读 MiMo-V2.6 的 RL 训练部分

**目标：** 理解 RL 规模化训练的工程细节

**步骤：**
1. 阅读 [MiMo-V2.6 论文](https://arxiv.org/abs/2610.11959)的第 3-4 节（RL 训练细节）
2. 重点关注：异步训练、Agent 评分、reward hacking 防御
3. 思考如何将这些技术应用到你自己的 Agent 训练中

**预计时间：** 1 小时

---

#### 建议 4：探索 Caught in the Act 的 FIBS 数据集

**目标：** 理解 LLM 欺骗检测的前沿方法

**步骤：**
1. 访问 [FIBS 数据集](https://github.com/AlignmentResearch/caught-in-the-act-probes)
2. 阅读数据格式和标注方式
3. 尝试训练一个简单的欺骗检测探针
4. 思考如何在你的 Agent 系统中集成类似的安全监控

**预计时间：** 1-2 小时

---

### 📚 本周阅读清单

| 优先级 | 论文 | 预计时间 | 理由 |
|---|---|---|---|
| ⭐⭐⭐ | AgentGarten | 45 分钟 | 当日最热，Agent 环境设计新范式 |
| ⭐⭐⭐ | MiMo-V2.6 | 60 分钟 | RL 规模化自我改进的完整方案 |
| ⭐⭐ | TokenRouter | 30 分钟 | NeurIPS 2026，实用价值高 |
| ⭐⭐ | Caught in the Act | 40 分钟 | Agent 安全的重要进展 |
| ⭐ | Memento 3 | 30 分钟 | 递归自我改进的新路线 |
| ⭐ | SGUID | 20 分钟 | 技能选择的实用方法 |

---

## 📌 附录：今日数据汇总

### arXiv 统计（2026-10-09）

| 分类 | 新增论文数 |
|---|---|
| cs.AI | 302 篇 |
| cs.LG | 324 篇 |
| cs.CL | 144 篇 |
| **合计** | **770 篇** |

### HuggingFace 热门论文 Top 5

| 排名 | 论文 | 热度 |
|---|---|---|
| 1 | AgentGarten | 131 |
| 2 | TokenRouter | 102 |
| 3 | From Traces to Agentic Worlds | 97 |
| 4 | Learn2Play Bench | 76 |
| 5 | SuperNav | 62 |

### 行业动态

| 事件 | 详情 |
|---|---|
| 特斯拉 Optimus | 弗里蒙特工厂加速生产至每周数百台 |
| CoreWeave + AdaniConneX | 在印度新孟买建设 240MW AI 数据中心 |
| UNESCO 全球 AI 协议 | 10 亿美元用于新兴经济体 AI 开发者培训 |
| 印度-非盟 AI 合作 | AI Labs of India 与非盟合作推动全球南方 AI 能力 |

---

> 📝 **编辑说明：** 本期情报基于 arXiv cs.AI/cs.LG/cs.CL（2026-10-09）、HuggingFace Papers/Models、GitHub Trending、AIFOD 等 12+ 来源的深度抓取和分析。所有论文均提供了原文链接和代码仓库（如有）。

> 🔗 **飞书文档版本：** 稍后将在群内分享，方便移动端阅读。

---

_下期预告：关注 MiMo-V2.6 开源框架的实际使用体验、TokenRouter 在生产环境的部署案例。_
