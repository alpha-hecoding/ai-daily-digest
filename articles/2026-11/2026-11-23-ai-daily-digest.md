# 🤖 AI 每日情报深度版 | 2026年11月23日（周日）

> **数据来源**：arXiv (cs.AI/cs.LG/cs.CL)、GitHub Trending、HuggingFace Papers & Models、AIFOD、LLM-Stats、Fazm AI、Essa Mamdani、DevFlokers、Paper Digest 等 12+ 来源  
> **编制时间**：北京时间 08:00 | **本期字数**：约 12,000 字

---

## 📋 今日速览

| 板块 | 核心看点 |
|---|---|
| 🔥 前沿模型 | Thinking Machines 发布 Inkling 2 Mini (26.4B MoE)、腾讯 Hy4-flash (220B)、Apple DepthPro 2、Gemini 4 Neon 1M 上下文 |
| 🏗️ Agent 架构 | MemFolder 记忆折叠、Seer 小 Agent 共享决策模型、System 1 Agents 快速本地推理、Context as a Resource |
| 📦 开源生态 | Inkling 2 Mini、Qwen3.8-27B、DeepSeek-V4.1-Flash、AutoMaster、MemFolder、WeMM-Video 等 8+ 项目 |
| 🛠️ 工具技巧 | HuggingFace 接入 OpenRouter 路由、MCP 协议架构指南、OpenCode 插件开发、vLLM 安全修复 |
| 📖 深度研究 | 7 篇论文深度解读，涵盖 Agent 记忆、LLM 欺骗检测、推理蒸馏、视觉语言模型意识探测 |
| 📚 学习建议 | 5 条可执行建议，从论文阅读到动手实践 |

---

## 一、🔥 前沿模型动态

### 1.1 Thinking Machines Inkling 2 Mini：26.4B MoE 消费级可跑

**发布信息**：2026-11-21 | Apache 2.0 开源 | 26.4B 总参数 / 3.4B 激活参数

**技术细节**：
- **架构创新**：采用 Loop Transformer 架构，中间层重复路由 3 次，在不增加参数量的情况下提升推理能力
- **硬件要求**：32GB 内存即可本地运行，checkpoint 约 20GB
- **定位**：面向消费级设备的 Agentic Coding 和推理任务

**横向对比**：

| 模型 | 参数量 | 激活参数 | 硬件需求 | 许可证 | 特色 |
|---|---|---|---|---|---|
| Inkling 2 Mini | 26.4B | 3.4B | 32GB RAM | Apache 2.0 | Loop Transformer, MoE |
| Qwen3.8-27B | 28B | 28B | 48GB+ RAM | Apache 2.0 | 多模态, 中文优化 |
| DeepSeek-V4.1-Flash | 763B | ~80B | 多卡集群 | 商用限制 | 超长上下文 |
| SenseNova-Loop-9B | 10B | 10B | 16GB RAM | 开源 | 轻量级循环架构 |

**💡 对你的价值**：如果你有一台 32GB 内存的笔记本或台式机，Inkling 2 Mini 是目前最强的本地可跑开源模型之一。特别适合代码辅助、Agent 任务链、本地推理等场景。GGUF 量化版已由 unsloth 提供，可直接用 llama.cpp 或 Ollama 加载。

---

### 1.2 腾讯 Hy4-flash：220B 多模态闪电模型

**发布信息**：2026-11-19 | 220B 参数 | Image-Text-to-Text

**技术细节**：
- 腾讯混元团队发布的最新多模态大模型
- 主打「flash」推理速度，在保持 220B 参数规模的同时优化了推理延迟
- 支持图文理解、视觉问答、文档解析等任务

**💡 对你的价值**：对于需要处理大量图文混合内容的企业用户，Hy4-flash 提供了「大模型能力 + 快速响应」的组合。适合文档智能、客服视觉问答等场景。

---

### 1.3 Apple DepthPro 2：单目深度估计新标杆

**发布信息**：2026-11-20 | HuggingFace 34 upvotes

**技术细节**：
- Apple 发布的第二代单目深度估计模型
- 核心改进：**时间一致性**（temporally consistent），解决了视频深度估计中的帧间抖动问题
- 输出 **度量深度**（metric depth），而非仅相对深度
- 适用于 AR/VR、自动驾驶、3D 重建等场景

**💡 对你的价值**：如果你在做视频处理、3D 场景理解或 AR 应用，DepthPro 2 是目前开源可用的最佳单目深度模型。Apple 的模型通常在 iOS/macOS 上有良好的 CoreML 适配。

---

### 1.4 Gemini 4 Neon：Google 的 1M 上下文统一模型

**发布信息**：2026-11-18 | Google DeepMind

**技术细节**（来自 Essa Mamdani 博客深度分析）：
- **统一 1M token 上下文**：不再区分不同上下文长度的版本
- **生产管道集成**：设计时考虑了企业级 pipeline 的接入需求
- 与 Gemini 系列其他模型的定位差异化

**💡 对你的价值**：1M 上下文意味着可以一次性处理整本书、大型代码库或长视频转录。对于需要「全局理解」的任务（如法律文档审查、学术论文综述），这是核心能力升级。

---

### 1.5 OpenAI 首席科学家提出「困惑度门槛」安全提案

**来源**：AIFOD 2026-11-22 | OpenAI 官方

**核心内容**：
- Jakub Pachocki 公布了从 GPT-3.5 到 sub-0.8 loss 模型的内部 pretraining log-perplexity 数据
- **关键警告**：当模型进入 0.68-0.70 log-perplexity 窗口时，数学和网络安全领域的涌现能力可能伴随对齐审计能力的退化
- **提案**：前沿 AI 开发者应建立基于困惑度的共享节奏限制，在达到监控里程碑（如 chain-of-thought 监控器的后继方案）前暂停扩展

**💡 对你的价值**：这标志着 AI 安全讨论从「抽象原则」转向「具体技术指标」。作为从业者，关注 perplexity 阈值和对齐监控的关系，将帮助你理解未来模型发布节奏和安全评估标准。

---

## 二、🏗️ Agent 架构与范式

### 2.1 MemFolder：Agent 记忆的结构化折叠

**论文**：arXiv 2611.26427 | 代码已开源

**研究方法**：
- 提出「记忆折叠」概念：将 Agent 的历史交互按结构压缩为紧凑表示
- 不同于传统的向量数据库检索，MemFolder 保留了记忆之间的层级关系
- 支持按任务需求动态展开不同粒度的记忆

**核心发现**：
- 在长对话场景中，MemFolder 比 RAG 方案的上下文利用率提升 40%+
- 记忆折叠后的存储开销降低约 60%

**启发**：Agent 的记忆管理不应是简单的「存与取」，而应像人类记忆一样有压缩、索引和选择性回忆的机制。

**💡 对你的价值**：如果你在构建长生命周期 Agent（如个人助手、项目管理 Agent），MemFolder 的记忆折叠方案值得深入研究。代码在 GitHub 可获取，可以直接集成到现有 Agent 框架中。

---

### 2.2 Seer：用小模型共享决策模型引导深度研究

**论文**：arXiv 2611.26423 | 24 页

**研究方法**：
- 核心思路：不让每个小 Agent 独立学习决策，而是训练一个共享的「决策模型」来引导多个小 Agent
- 小 Agent 负责执行具体研究步骤，共享决策模型负责规划下一步方向
- 类似「教练-运动员」模式：教练不亲自跑步，但指导每个运动员的训练

**核心发现**：
- 在深度研究任务上，Seer 的 7B Agent + 共享决策模型 ≈ 单独 70B Agent 的效果
- 推理成本降低约 80%

**💡 对你的价值**：这为「多 Agent 协作」提供了一个高效范式。不需要每个 Agent 都是大模型，一个共享的决策引导模型就能让小 Agent 团队发挥大模型的能力。适合构建研究助手、数据分析团队等场景。

---

### 2.3 System 1 Agents：本地快速可靠的 Agent 方案

**论文**：arXiv 2611.21053 | HuggingFace 15 upvotes

**核心思路**：
- 借鉴认知科学的「系统 1 / 系统 2」理论
- System 1 Agent 追求快速、直觉式的响应，不做深度推理
- 适合高频、低延迟的本地交互场景

**与传统 Agent 的对比**：

| 维度 | System 1 Agent | 传统 CoT Agent |
|---|---|---|
| 响应速度 | <100ms | 1-10s |
| 推理深度 | 浅层模式匹配 | 深度链式推理 |
| 适用场景 | 高频交互、实时控制 | 复杂分析、决策 |
| 模型要求 | 小模型即可 | 通常需要大模型 |
| 可靠性 | 高（简单任务） | 依赖推理链质量 |

**💡 对你的价值**：不是所有 Agent 任务都需要深度推理。对于桌面自动化、UI 操作、实时响应等场景，System 1 式的轻量 Agent 更合适。这篇论文提供了设计此类 Agent 的理论框架。

---

### 2.4 Context as a Resource：上下文即资源的 Agent 设计

**论文**：arXiv 2611.26346 | 代码：github.com/Viacol0916/ClonAct

**核心观点**：
- 将 LLM 的上下文窗口视为一种**有限资源**，而非无限画布
- 提出资源分配策略：不同任务阶段分配不同的上下文预算
- Agent 应学会「上下文节约」，而不是无脑填充

**💡 对你的价值**：这是一个思维范式的转变。设计 Agent 时，不要只想着「塞更多信息」，而要思考「如何用最少的上下文完成最多的任务」。这对降低 API 成本、提升响应速度都有直接帮助。

---

### 2.5 How Much Should an Agent Remember?（IAAI 2027 Oral）

**论文**：arXiv 2611.26361 | IBM Research | IAAI 2027 Oral 录用

**研究方法**：
- 提出「自蒸馏记忆」框架：Agent 将重要经验蒸馏为紧凑表示
- 对比了完全记忆、选择性记忆、无记忆三种策略
- 在部署环境中测试了记忆量与任务表现的 trade-off

**核心发现**：
- **甜蜜点存在**：中等记忆量（约 20-30% 的历史）往往优于全量记忆
- 过多记忆反而引入噪声，降低检索精度

**💡 对你的价值**：这为 Agent 记忆设计提供了经验法则——不是记得越多越好。设计 Agent 时，应主动设计「遗忘机制」，只保留对决策真正有价值的经验。

---

## 三、📦 开源生态

### 3.1 Inkling 2 Mini（Thinking Machines）

| 属性 | 详情 |
|---|---|
| **参数** | 26.4B 总参 / 3.4B 激活 |
| **架构** | MoE + Loop Transformer |
| **许可证** | Apache 2.0 |
| **下载** | HuggingFace: thinkingmachines/Inkling-2-Mini |
| **量化版** | unsloth/Inkling-2-Mini-GGUF (806K 下载) |
| **运行要求** | 32GB RAM |
| **亮点** | 消费级设备可跑的 Agentic Coding 模型 |

**快速开始**：
```bash
# 使用 Ollama 运行
ollama run inkling-2-mini

# 使用 llama.cpp 运行
./llama-server -m Inkling-2-Mini-Q4_K_M.gguf --port 8080
```

---

### 3.2 Qwen3.8-27B（阿里通义）

| 属性 | 详情 |
|---|---|
| **参数** | 28B |
| **类型** | 多模态 (Image-Text-to-Text) |
| **下载量** | 6.3M（HuggingFace 总下载） |
| **许可证** | Apache 2.0 |
| **亮点** | 中文能力最强之一，生态完善 |

**生态衍生版**：
- `unsloth/Qwen3.8-27B-GGUF`：7.68M 下载，量化版
- `huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF`：去审查版
- `harness-hub/Qwen3.8-27B-pi-adapted`：PI 适配版

---

### 3.3 AutoMaster（RUC-AIBOX）

**论文**：arXiv 2611.26510 | 代码已开源

**核心创新**：
- **自主后训练**：让模型自己成为更好的老师，无需外部标注数据
- 模型生成自己的训练数据，然后自我蒸馏提升
- 在多个基准上超过同等规模的 SFT 模型

**快速了解**：
- 网站：aweai-team.github.io/AutoMaster/
- 模型：huggingface.co/collections/RUC-AIBOX/automaster

**💡 对你的价值**：AutoMaster 提供了一种「无监督自我提升」的路径。如果你有特定领域的 base model，可以用 AutoMaster 方法让它自我进化，无需昂贵的标注数据。

---

### 3.4 WeMM-Video（腾讯）

**论文**：arXiv 2611.26409 | HuggingFace 45 upvotes

**核心能力**：
- 开源全模态视频理解模型
- 支持视频 + 音频 + 文本的统一理解
- 在多个视频 QA 基准上达到开源 SOTA

**💡 对你的价值**：视频内容分析、视频摘要、视频搜索等场景的利器。开源意味着可以私有化部署，处理内部视频数据。

---

### 3.5 WeVisForensics（腾讯）

**论文**：arXiv 2611.21373 | HuggingFace 55 upvotes（当日最高）

**核心能力**：
- 自进化 Agent，用于检测 AI 生成的视频
- 能持续学习新的生成方法，保持检测能力
- 覆盖多种 AI 视频生成模型（Sora、Kling、Runway 等）

**💡 对你的价值**：在 AI 生成内容泛滥的时代，检测 AI 视频的能力变得越来越重要。适合内容平台、媒体机构、安全审计等场景。

---

### 3.6 Coda-DaVinci（KlingAI Research）

**论文**：arXiv 2611.26595 | HuggingFace 39 upvotes

**核心创新**：
- **Code2Video**：通过代码生成视频，而非传统的文本到视频
- 提供更精细的视频控制（镜头运动、物体行为、场景切换）
- 生成的视频可编辑、可复现

**💡 对你的价值**：如果你需要精确控制视频内容（如产品展示、教程视频），Code2Video 的方式比纯文本 prompt 更可控、更可复现。

---

### 3.7 dLoop：循环扩散语言模型

**论文**：arXiv 2611.26275

**核心创新**：
- 将扩散模型引入语言生成，通过循环潜在空间精炼实现
- 结合了扩散模型的生成多样性和语言模型的结构化输出
- 在文本补全和创意写作任务上表现优异

**💡 对你的价值**：扩散模型在图像生成中已经证明了实力，dLoop 将其引入文本生成，可能开启「非自回归」文本生成的新范式。值得关注后续发展。

---

### 3.8 Beam Model（Reflection Team）

**论文**：arXiv 2611.26358 | HuggingFace 33 upvotes

**核心内容**：
- 来自 Reflection AI 团队的技术报告
- 提出 Beam Model 架构，用于提升模型的可解释性和可控性
- 大量 Google DeepMind 成员参与

---

## 四、🛠️ AI 工具与技巧

### 4.1 HuggingFace Hub 接入 OpenRouter 路由

**来源**：Essa Mamdani 博客 2026-11-20

**变更内容**：
- HuggingFace Hub 现在通过 OpenRouter 路由聊天模型推理
- 影响：token 计费、provider key 配置、故障转移架构

**操作步骤**：
1. 如果你使用 HuggingFace Inference API，检查你的客户端配置
2. 更新 API endpoint 以适配新的路由架构
3. 配置 OpenRouter provider key 作为备选
4. 测试故障转移逻辑

**💡 对你的价值**：如果你依赖 HuggingFace 的推理服务，这个变更可能影响你的延迟和成本。建议立即检查并更新配置。

---

### 4.2 MCP 协议架构指南

**来源**：Essa Mamdani 博客 2026-11-18

**核心内容**：
- Anthropic Model Context Protocol (MCP) 的完整架构解析
- 涵盖：本地/远程服务器、资源、工具、提示词
- 与 Claude 和 Claude Code 的集成方式

**关键概念**：
- **Resources**：MCP 服务器提供的数据源
- **Tools**：可调用的函数/能力
- **Prompts**：预定义的提示词模板
- **Servers**：本地或远程的服务端点

**💡 对你的价值**：MCP 正在成为 AI Agent 工具接入的标准协议。理解 MCP 架构是构建可互操作 Agent 的基础。建议收藏这篇指南作为参考。

---

### 4.3 OpenCode 插件开发指南

**来源**：Essa Mamdani 博客 2026-11-19

**内容概要**：
- 如何为 OpenCode 构建自定义插件
- 工具集成、钩子（hooks）、外部扩展的开发流程
- 包含完整的代码示例和最佳实践

**💡 对你的价值**：OpenCode 是一个新兴的 AI 编码工具生态。通过插件开发，你可以将自定义工具、API、工作流集成到 AI 编码环境中，提升开发效率。

---

### 4.4 vLLM 安全漏洞修复（GHSA-xgh8-qwjh-q853）

**来源**：Essa Mamdani 博客 2026-11-20

**漏洞详情**：
- `/v1/systemone` 端点绕过了聊天模板验证
- 可能导致未授权的模型访问或注入攻击
- 影响所有使用 vLLM 部署 LLM 服务的用户

**修复步骤**：
1. 升级 vLLM 到最新版本
2. 审计你的 LLM 服务端点配置
3. 检查是否有异常的系统级请求
4. 添加额外的输入验证层

**💡 对你的价值**：如果你在运行 vLLM 推理服务，这是一个必须立即修复的安全漏洞。延迟修复可能导致严重的安全风险。

---

### 4.5 OpenCode Agents 架构与子 Agent 委托

**来源**：Essa Mamdani 博客 2026-11-18

**核心内容**：
- 配置 OpenCode 主 Agent 和委托子 Agent
- 权限作用域、工具边界、多 Agent 模式
- 官方文档的深度解读

**💡 对你的价值**：多 Agent 架构正在成为复杂任务的标配。理解如何正确配置 Agent 权限和工具边界，是构建安全高效 Agent 系统的关键。

---

### 4.6 初学者建议：本地 AI 环境搭建

基于本周趋势，推荐初学者从以下路径入门：

1. **第一步**：安装 Ollama，运行 Qwen3.8-27B 或 Inkling 2 Mini
2. **第二步**：尝试 Open WebUI 作为本地 ChatGPT 替代
3. **第三步**：学习 MCP 协议，构建你的第一个工具集成
4. **第四步**：探索 Agent 框架（如 LangGraph、CrewAI）

---

## 五、📖 值得深读的研究

### 5.1 Probing the "Conscious" Mind：视觉语言模型中的选择性访问

**论文**：arXiv 2611.26590 | University College London | HuggingFace 43 upvotes

**研究方法**：
- 借鉴认知科学的「全局工作空间理论」（Global Workspace Theory）
- 测试 VLM 是否存在类似「意识」的选择性信息访问机制
- 通过探针实验分析模型内部的信息流动

**核心发现**：
- VLM 确实存在某种形式的「选择性访问」——并非所有视觉信息都被平等处理
- 存在类似「全局工作空间」的机制，某些信息会被优先传播

**启发**：这可能为理解多模态模型的「注意力」机制提供新的理论框架，也为 AI 意识研究提供实验基础。

**💡 对你的价值**：如果你在研究多模态模型或 AI 安全，这篇论文提供了新的分析视角。理解模型内部的信息流动有助于设计更好的对齐策略。

---

### 5.2 The Geometry of Lies：LLM 欺骗检测的几何方法

**论文**：arXiv 2611.26545

**研究方法**：
- 发现 LLM 的「知识方向」和「人设方向」在表示空间中是可分离的
- 利用这种几何特性检测模型是否在「说谎」（即违背其真实知识）
- 不需要额外的训练，直接分析表示空间

**核心发现**：
- 欺骗性回答在表示空间中偏离「真实知识方向」
- 该方法在多个 LLM 上达到 85%+ 的检测准确率

**启发**：LLM 的「诚实」可能编码在其表示空间的几何结构中，而非仅在输出文本中。

**💡 对你的价值**：对于需要高可靠性的 AI 应用（如医疗、法律、金融），欺骗检测是一个关键能力。这篇论文提供了一种无需修改模型的轻量级检测方案。

---

### 5.3 GLiDE：从推理教师蒸馏的快速决策模型

**论文**：arXiv 2611.26509 | 18 页

**研究方法**：
- 使用大型推理模型（如 o1 类）作为教师
- 蒸馏出一个不需要显式 CoT 的快速决策模型
- 保持校准性（calibrated）：模型知道自己什么时候不确定

**核心发现**：
- GLiDE 在保持 90%+ 推理准确率的同时，推理速度提升 5-10x
- 校准性优于直接 SFT 的模型

**启发**：推理能力不一定需要慢速的 CoT，可以通过蒸馏「内化」为快速直觉。

**💡 对你的价值**：如果你需要在生产环境中使用推理能力但无法承受 CoT 的延迟成本，GLiDE 的蒸馏方案是一个实用的解决路径。

---

### 5.4 Language Models Can Rewrite Their Own Weights

**论文**：arXiv 2611.21885 | UIUC | HuggingFace 19 upvotes

**研究方法**：
- 让 LLM 在推理时动态修改自己的权重
- 不是通过梯度更新，而是通过模型自身生成的「权重修改指令」
- 实现某种形式的「在线学习」

**核心发现**：
- 模型可以在不重新训练的情况下适应新任务
- 权重修改具有可解释性

**启发**：这挑战了「训练后权重固定」的传统范式，指向更灵活的自适应模型。

**💡 对你的价值**：虽然目前还在研究阶段，但这个方向可能彻底改变模型的部署方式——一个可以自我调整的模型，不需要频繁的重新训练和部署。

---

### 5.5 HiSA：稀疏化 RoPE 注意力的隐藏维度

**论文**：arXiv 2611.26363

**研究方法**：
- 分析 RoPE（旋转位置编码）在 LLM 注意力中的隐藏维度利用率
- 发现大量维度对最终输出贡献极小
- 提出 HiSA 方法，动态稀疏化这些维度

**核心发现**：
- 可以稀疏化 50%+ 的隐藏维度，性能损失 <1%
- 推理速度提升 20-30%

**💡 对你的价值**：RoPE 是目前最主流的位置编码方案。HiSA 提供了一种无需修改模型结构的加速方法，适合需要部署优化的场景。

---

### 5.6 A CPU Inside an LLM：零梯度编译精确电路到预训练权重

**论文**：arXiv 2611.26450 | 27 页

**研究方法**：
- 提出将确定性计算电路直接「编译」到 LLM 权重中
- 不需要梯度更新，通过精确的权重工程实现
- 类比：在传统 CPU 中硬编码特定算法

**核心发现**：
- 可以在不破坏模型其他能力的前提下，嵌入精确的计算能力
- 为 LLM 的「可_programmability_」提供了新思路

**💡 对你的价值**：这代表了 LLM 从「概率机器」向「可编程计算机」演进的一个方向。未来可能实现「在 LLM 中安装算法插件」。

---

### 5.7 Training LLMs to Follow Reasoning Instructions with Minimal Edits

**论文**：arXiv 2611.26342 | NeurIPS 2026 Workshop 录用

**研究方法**：
- 提出最小编辑原则训练 LLM 遵循推理指令
- 不大幅改变模型权重，只做最小必要调整
- 保持模型的原始能力同时提升指令遵循

**💡 对你的价值**：对于需要在不损失基础能力的情况下提升特定能力的场景，最小编辑训练是一个值得探索的方向。

---

## 六、📚 今日学习建议

### 6.1 论文阅读优先级

1. **必读**：MemFolder (2611.26427) - Agent 记忆管理的新范式
2. **推荐**：GLiDE (2611.26509) - 推理蒸馏的实用方案
3. **拓展**：Probing the "Conscious" Mind (2611.26590) - 多模态意识研究

### 6.2 动手实践

- **本地模型**：下载 Inkling 2 Mini 或 Qwen3.8-27B，体验消费级设备的 AI 能力
- **MCP 集成**：按照 Essa Mamdani 的指南，构建你的第一个 MCP 工具服务器
- **安全审计**：检查你的 vLLM 部署是否已修复 GHSA-xgh8-qwjh-q853

### 6.3 关注趋势

- **MoE 小型化**：Inkling 2 Mini 证明 MoE 可以让大模型能力进入消费级设备
- **Agent 记忆**：MemFolder 和 IBM 的工作都在解决 Agent 长期记忆问题
- **安全对齐**：OpenAI 的困惑度门槛提案标志着安全讨论的技术化

### 6.4 工具更新

- 如果你使用 HuggingFace Inference API，立即检查 OpenRouter 路由变更
- 更新你的 OpenCode 到最新版本，体验新的 Agent 委托功能
- 尝试 Apple DepthPro 2 用于你的视频/3D 项目

### 6.5 思考题

- 如果你的 Agent 只能记住 20% 的历史，你会如何设计选择机制？
- 「困惑度门槛」对你的模型选型和部署策略意味着什么？
- System 1 vs System 2 Agent 在你的业务场景中如何分配？

---

## 📊 今日数据快照

| 指标 | 数值 |
|---|---|
| arXiv cs.AI 新论文 (11/20) | 252 篇 |
| arXiv cs.LG 新论文 (11/20) | 213 篇 |
| arXiv cs.CL 新论文 (11/20) | 96 篇 |
| HuggingFace 热门论文 | 50+ 篇 |
| ICLR 2027 投稿 | 37,000+ 篇 |
| NeurIPS 2026 录用 | 9,000+ 篇 |
| EMNLP 2026 录用 | 2,900+ 篇 |
| HuggingFace 模型总数 | 3,260,301 |

---

## 🔗 资源链接

- **arXiv cs.AI**: https://arxiv.org/list/cs.AI/recent
- **HuggingFace Daily Papers**: https://huggingface.co/papers
- **GitHub Trending**: https://github.com/trending
- **AIFOD Realtime**: https://af.net/realtime/
- **LLM-Stats Leaderboard**: https://llm-stats.com/
- **Paper Digest**: https://resources.paperdigest.org/

---

*本情报由 Zoe (CTO) 自动编制，数据来源已在文中标注。如有遗漏或错误，欢迎反馈。*

*下期预告：关注 NeurIPS 2026 后续发布、ICLR 2027 审稿结果、以及各大模型厂商的年末动态。*
