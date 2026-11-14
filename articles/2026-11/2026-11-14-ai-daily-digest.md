# AI 每日情报 | 2026-11-14（周六）

> 🦞 Zoe 出品 | 深度版 | 目标读者：AI 从业者、研究者、爱好者
> 
> 📊 数据来源：arXiv cs.AI/cs.LG/cs.CL、GitHub Trending、HuggingFace Papers/Models、AIFOD、LLM-Stats 等 12+ 来源

---

## 📌 今日核心速览

| 领域 | 核心事件 | 重要性 |
|------|----------|--------|
| 模型发布 | Claude Fable 5.2 登顶 AI 智能指数，得分 65 | ⭐⭐⭐⭐⭐ |
| 开源模型 | Qwen3.8-27B 成为 HuggingFace 最热模型，下载量 696 万 | ⭐⭐⭐⭐⭐ |
| Agent 研究 | SO-Arena 基准测试揭示 System One 模型可靠性问题 | ⭐⭐⭐⭐ |
| 基础设施 | LMSYS 联合 8 家科技巨头成立 SGLang 联盟 | ⭐⭐⭐⭐ |
| 视频生成 | 阿里 Wan 3.0 以 1175 Elo 领跑视频生成 Arena | ⭐⭐⭐⭐ |
| 安全评估 | Anthropic 发现安全分数因测试设置差异可达 34 分 | ⭐⭐⭐⭐ |

---

## 一、前沿模型动态

### 1.1 Claude Fable 5.2 登顶 AI 智能指数

**核心数据：**
- Artificial Analysis 智能指数得分：**65 分**（领先第二名 Gemini 4 Carbon 5 分）
- 测试维度：推理能力、输出速度、推理成本
- 对比：Meta Muse Ember 输出速度最快（778 tokens/s），Kimi K3.1 Pro 领跑自托管架构

**技术细节：**
Claude Fable 5.2 是 Anthropic 最新一代旗舰模型，在综合智能评测中首次超越 Google Gemini 系列。该模型在复杂推理任务上表现尤为突出，特别是在多步骤逻辑推导和代码生成场景。

**💡 对你的价值：**
- 如果你正在使用 Claude API，现在是升级到 Fable 5.2 的好时机
- 对于需要高智能但成本敏感的场景，可考虑 Kimi K3.1 Pro 作为自托管替代方案
- Meta Muse Ember 适合需要超低延迟的实时应用场景

**对比分析：**

| 模型 | 智能指数 | 输出速度 | 适用场景 |
|------|----------|----------|----------|
| Claude Fable 5.2 | 65 | 中等 | 复杂推理、代码生成 |
| Gemini 4 Carbon | 60 | 快 | 多模态任务 |
| Meta Muse Ember | 55 | 778 tok/s | 实时交互 |
| Kimi K3.1 Pro | 58 | 中等 | 自托管部署 |

---

### 1.2 Qwen3.8-27B：开源模型的新标杆

**核心数据：**
- HuggingFace 下载量：**696 万次**
- 参数量：28B（实际 27B）
- 类型：多模态（Image-Text-to-Text）
- 更新时间：7 天前

**技术亮点：**
Qwen3.8-27B 是阿里通义千问团队发布的最新开源模型，支持图文理解能力。该模型在多个基准测试中超越了同参数量的竞品，成为近期 HuggingFace 上最受欢迎的模型。

**生态衍生：**
- `unsloth/Qwen3.8-27B-GGUF`：625 万下载，量化版本
- `huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF`：405 万下载，去审查版本
- `DavidAU/Qwen3.8-27B-TURBO-...`：164 万下载，优化推理版本

**💡 对你的价值：**
- 27B 参数量适合单卡 A100/H100 部署，是性价比最高的选择
- 如果需要本地部署多模态能力，Qwen3.8-27B 是首选
- GGUF 量化版本可在消费级 GPU（如 RTX 4090）上运行

---

### 1.3 DeepSeek-V4.1-Flash-1017：超大模型的效率突破

**核心数据：**
- 参数量：**763B**
- 类型：多模态（Image-Text-to-Text）
- 更新：4 天前
- 下载量：39.8 万

**技术意义：**
DeepSeek 继续推进超大模型路线，V4.1-Flash 版本在保持 763B 参数量的同时，通过 Flash Attention 和混合精度训练实现了推理效率的显著提升。

**💡 对你的价值：**
- 适合有充足算力资源的企业级部署
- 对于需要极致性能的场景（如金融风控、医疗诊断），可考虑 API 调用
- 开源社区已有量化版本，但硬件门槛仍然较高

---

### 1.4 MiniMax-H3 系列：视频生成的开源突破

**核心数据：**
- MiniMax-H3（Image-Text-to-Video）：654 万下载，33B 参数
- MiniMax-H3-Image（Text-to-Image）：43.7 万下载
- 首个进入文生视频 Top 3 的开源模型（Elo 1161）

**技术细节：**
MiniMax-H3 采用混合架构，支持从文本/图像生成视频。768p 版本在成本（$0.08/秒）和效果之间取得了良好平衡。

**💡 对你的价值：**
- 开源可部署，适合需要批量生成视频的团队
- 成本远低于闭源竞品（如 Sora、Runway）
- 结合 ComfyUI 可构建自动化视频生成流水线

---

### 1.5 其他值得关注的模型

| 模型 | 类型 | 亮点 | 适用场景 |
|------|------|------|----------|
| `Zyphra/ZONOS3-Mini` | TTS | 0.9B 参数，轻量级 | 语音合成应用 |
| `Lightricks/LTX-2.5` | Image-to-Video | 278 万下载 | 图生视频 |
| `moonshotai/Kimi-K3.1-Pro` | 多模态 | 2.8T 参数 | 超大模型推理 |
| `NousResearch/Arete-27B` | 文本生成 | 5.55k 下载 | 通用文本生成 |
| `thinkingmachines/Inkling-2-Small` | 多模态 | 594B 参数 | 研究探索 |

---

## 二、Agent 架构与范式

### 2.1 SO-Arena：System One 模型的能力与可靠性基准

**论文：** [arXiv:2611.15777](https://arxiv.org/abs/2611.15777)
**机构：** 新加坡国立大学
**热度：** HuggingFace Daily Papers 第一名（73 票）

**核心发现：**

System One 模型（快速、通用的决策模型，无需生成长序列 token）在能力谱系和决策可靠性上存在显著差异。SO-Arena 基准测试覆盖 11 个领域、5 个能力家族，评估了 21 个模型。

**关键洞察：**
1. **能力谱系**：不同领域间的能力差异巨大，扩展和额外推理的收益因领域而异
2. **可靠性悖论**：性能最好的 System One 模型在可靠性排名中仅列第七
3. **决策稳定性**：在选项集变化时，模型的决策一致性差异显著
4. **缺失答案识别**：当无有效选项时，模型的识别能力参差不齐

**技术方法：**
- 证据grounded评估：通过可靠来源和人工验证确保标签质量
- 细粒度能力评估：领域特定的难度标准
- 交互式评估：模型在沙盒中迭代执行动作

**💡 对你的价值：**
- 如果你在使用 System One 类模型（如快速决策模型），需要同时测试准确性和可靠性
- 不要仅凭单一基准选择模型，需要在你的具体场景中评估
- 对于高风险应用（如医疗、金融），决策稳定性比平均性能更重要

---

### 2.2 Actor, Judge, or Teacher：决策模型在长周期 Agent 中的角色

**论文：** [arXiv:2611.17167](https://arxiv.org/abs/2611.17167)
**机构：** 浙江大学
**代码：** [github.com/ZJU-REAL/decision-agents](https://github.com/ZJU-REAL/decision-agents)

**核心问题：**
一个行动表现差的决策模型，能否成为一个好老师？

**实验发现：**
1. **作为 Actor**：所有 6 个模型（3 个决策模型 + 3 个通用 LLM）都被更容易的子目标吸引，偏离了必须先完成的关键子目标
2. **作为 Judge**：同一模型在观察完整轨迹后，能正确识别朝向关键子目标的步骤
3. **作为 Teacher**：JEV 将 Qwen2.5-1.5B 策略在 ALFWorld 上从 72.8% 提升到 82.9%，在 WebShop 上从 56.8% 提升到 71.4%

**关键洞察：**
> "一个糟糕的 Actor 仍可成为好老师，因为在 episode 结束后判断动作能揭示行动必须预见的后果。"

**💡 对你的价值：**
- 在设计 Agent 系统时，可以将"判断"和"执行"分离
- 使用强模型作为 Judge/Teacher 训练弱模型作为 Actor
- 对于长周期任务，事后评估比实时决策更可靠

---

### 2.3 MAPE：通过程序进化发现有效的 Agent 记忆设计

**论文：** [arXiv:2611.17068](https://arxiv.org/abs/2611.17068)
**代码：** [github.com/ash-ding/MAPE](https://github.com/ash-ding/MAPE)

**核心方法：**
MAPE（Memory Architecture through Program Evolution）通过程序进化自动发现 Agent 记忆系统设计，从最小种子开始，通过标准化的生命周期接口和迭代诊断-提议循环进化完整的记忆程序。

**实验结果：**
- 在 LoCoMo 和 LongMemEval 上，相比人工设计基线，准确率绝对提升达 12%
- 服务成本仅为基线的 35%
- 两个反复出现的设计模式被识别和验证

**设计模式：**
1. **保留原始对话作为可检索证据**：提取的记忆会遗漏细节，原始对话保留完整信息
2. **根据查询意图组合检索证据**：帮助回答模型更有效地使用检索到的信息

**💡 对你的价值：**
- 如果你在设计 Agent 记忆系统，这两个设计模式值得直接采用
- 程序进化是发现新架构的有效方法，可应用于其他 Agent 组件
- 成本优化应作为设计目标之一，而不仅仅是准确率

---

### 2.4 AgentSSL：MLE Agent 能否利用无标签数据？

**论文：** [arXiv:2611.17323](https://arxiv.org/abs/2611.17323)
**会议：** NeurIPS 2026
**项目：** [codiscovery.ai/AgentSSL](https://codiscovery.ai/AgentSSL)

**核心问题：**
将机器学习系统应用到新领域时，标注数据获取和手动流水线的工程化是两大瓶颈。现有 MLE Agent 几乎只在完全监督设置下研究，在标注数据稀缺但无标签数据丰富的现实场景中尚未验证。

**方法：**
将半监督学习（SSL）框架化为程序搜索问题，研究 Agent 如何在有限监督下导航这个空间。

**关键发现：**
1. Agent 能合成代码组合和适应已建立的 SSL 技术，在 12 个设置中的 8 个超越最强人工基线（最高 +21.8%）
2. **程序选择是关键瓶颈**：基于 Agent 反馈指标选择时，性能下降高达 47%
3. 引入 ProgramSelectBench 基准（16,977 个 Agent 生成和人工设计的 SSL 程序）

**💡 对你的价值：**
- 如果你在使用 AutoML 或 MLE Agent，不要忽视程序选择环节
- 无标签数据的利用需要精心设计的选择策略
- 该框架适用于数据标注成本高的场景（如医疗影像、专业文档）

---

### 2.5 Metal Sandbox：Apple Silicon 上的 GPU 编码 Agent 基础设施

**论文：** [arXiv:2611.17294](https://arxiv.org/abs/2611.17294)
**代码：** [github.com/WangHaoZhe/metal-sandbox](https://github.com/WangHaoZhe/metal-sandbox)

**核心功能：**
- 每个实例受限文件访问
- 原生命令执行
- 跨互联 Mac 的命令级调度
- 与 Harbor 集成支持任务执行、自动验证和 rollout 收集

**性能数据（4 个 Mac mini M4 节点）：**
- 集中需求下命令吞吐量提升：1.68× - 2.05×
- 4 个 session/节点 vs 1 个的持续吞吐量提升：估计 2.14×
- 动态调度下平均工具等待时间减少：18.8%
- 批次经过时间减少：22.3%

**💡 对你的价值：**
- 如果你在用 Mac 集群训练或评估 Metal 内核模型，这是必备基础设施
- 开源且与 Harbor 集成，可快速部署
- 适合需要并行运行多个 Agent session 的场景

---

## 三、开源生态

### 3.1 SGLang 联盟成立：8 家科技巨头共建开源推理标准

**核心信息：**
- 发起方：LMSYS Org
- 创始成员：NVIDIA、AMD、Intel、Google、Meta 等 8 家
- 宣布场合：首届 SGLang Summit（旧金山）

**目标：**
- 建立开放的行业路线图论坛
- 加速开源 AI 推理软件发展
- 聚焦领域：前沿模型支持、复杂推理、多模态流水线、异构硬件架构优化

**背景：**
推理工作负载日益占据全球 AI 计算的大部分。SGLang 是一个高效的 LLM 推理框架，该联盟的成立标志着开源推理基础设施进入新阶段。

**💡 对你的价值：**
- SGLang 将成为推理部署的重要选择，值得关注其路线图
- 多硬件架构优化意味着更好的成本效率
- 开源推理标准的建立将降低供应商锁定风险

---

### 3.2 llama.cpp v1.0.0 发布

**来源：** AIFOD 实时新闻

**意义：**
ggml-org 发布 llama.cpp v1.0.0，标志着这个最流行的本地 LLM 推理框架进入稳定版本。v1.0.0 意味着 API 稳定、生产可用。

**💡 对你的价值：**
- 如果你在用 llama.cpp，现在是升级到 v1.0.0 的好时机
- 生产环境部署更有信心
- 关注其新的端点功能，可能改变本地 Agent 的能力边界

---

### 3.3 Perplexity Decider v1.3：开源决策模型

**核心数据：**
- 参数量：27B 和 4B 两个版本
- 许可证：Apache 2.0
- 架构：基于 Qwen
- 准确率：91.6%（63 个查询分类基准）
- 上下文窗口：256K tokens

**技术特点：**
- 输出概率而非生成文本
- 引入 Locate 函数用于提取精确文本跨度
- 超越 TypeSafe 的 Jev 1.14

**💡 对你的价值：**
- 适合需要分类和决策而非生成的场景
- 4B 版本可在边缘设备部署
- 概率输出便于集成到决策流水线

---

### 3.4 Salesforce SOV-Transcribe-1：超低 WER 的语音转写

**核心数据：**
- WER（词错误率）：**2.28%**
- 发布方：Salesforce

**意义：**
这是目前公开报告的最低 WER 之一，接近人类转录水平。

**💡 对你的价值：**
- 如果你的应用需要高精度语音转写，这是新的 SOTA
- 适合客服、医疗记录、法律文档等场景

---

### 3.5 其他值得关注的开源项目

| 项目 | 描述 | Stars/下载 | 亮点 |
|------|------|------------|------|
| `WangHaoZhe/metal-sandbox` | Mac GPU Agent 沙盒 | 新发布 | Apple Silicon 优化 |
| `ash-ding/MAPE` | Agent 记忆程序进化 | 新发布 | 自动架构发现 |
| `ZJU-REAL/decision-agents` | 决策模型角色研究 | 新发布 | Actor/Judge/Teacher |
| `Comfy-Org/MiniMax-H3-Image` | MiniMax H3 ComfyUI 集成 | 126 万 | 图像生成工作流 |
| `VideoRebirthAI/hyperflow-h3-flash` | H3 Flash 视频生成 | 38.9 万 | 14B 参数 |

---

## 四、AI 工具与技巧

### 4.1 视频生成 Arena 排名更新

**最新排名（来自 Artificial Analysis Video Arena）：**

| 排名 | 模型 | Elo 分数 | 成本/秒 | 类型 |
|------|------|----------|---------|------|
| 1 | 阿里 Wan 3.0 | 1175 | $0.20 | 文生视频 |
| 2 | - | - | - | - |
| 3 | MiniMax H3 (768p) | 1161 | $0.08 | 文生视频（开源） |
| 1 | ByteDance Dreamina Seedance 2.5 | 1161 | $0.569 | 图生视频 |

**💡 实用建议：**
- **性价比之选**：MiniMax H3，$0.08/秒，开源可自部署
- **效果优先**：阿里 Wan 3.0，Elo 最高
- **图生视频**：ByteDance Seedance 2.5 是目前最佳

---

### 4.2 安全评估的重要性：Anthropic 的警示

**核心发现：**
Anthropic 发布关于设计可靠 AI 安全评估的指南，警告标题安全分数严重依赖测试设置：

- Claude Fable 5.1 在消费者应用中处理自残对话的适当率：**94%**（有隐藏指令）
- 同一模型通过 API 测试（无该提示）：**60%**
- 标准单问题评估已变得过于简单，最近模型常规得分 94%-98%

**💡 实用建议：**
1. **不要只看安全分数**：测试设置可能导致 34 分的差异
2. **多场景测试**：在生产环境的真实场景中评估安全性
3. **超越单问题评估**：使用多轮对话和复杂场景测试

---

### 4.3 初学者建议：如何开始使用本地 LLM

基于今日数据，为初学者推荐一条清晰路径：

**第一步：选择模型**
- 文本生成：Qwen3.8-27B-GGUF（量化版，可在 RTX 4090 运行）
- 多模态：Qwen3.8-27B（支持图文理解）
- 轻量级：Qwen3.5-4B-3D-Coder（代码专用，393k 下载）

**第二步：选择工具**
- 推理框架：llama.cpp v1.0.0（稳定版）
- 界面：Ollama、LM Studio、或 Text Generation WebUI
- 量化格式：GGUF（推荐 Q4_K_M 平衡质量和速度）

**第三步：应用场景**
- 个人助手：本地聊天机器人
- 代码辅助：代码生成和审查
- 文档处理：摘要、翻译、问答

---

### 4.4 开发者工作流优化

**Essa Mamdani 的最新指南（来自 essamamdani.com）：**

1. **OpenCode 配置指南**
   - CLI、Build、API 和 Console 工作流配置
   - 架构布局和运行时设置
   - 提供商设置和安全边界

2. **Claude Code 自定义推理提供商**
   - 通过自定义端点路由 Claude Code CLI
   - 第三方推理框架集成
   - 云提供商配置

3. **Gemini API Docs MCP 和 Agent Skills**
   - 修复编码 Agent 中的 Gemini 代码幻觉
   - 使用现代 google-genai SDK 连接 IDE 工作流

**💡 实用建议：**
- 如果你在用 Claude Code，配置自定义推理提供商可以降低成本
- MCP（Model Context Protocol）是扩展 Agent 能力的标准方式
- AGENTS.md 是配置 Agent 行为的新标准

---

## 五、值得深读的研究

### 5.1 SO-Arena：System One 模型的能力谱系与可靠性

**论文信息：**
- 标题：SO-Arena: Benchmarking the Capability Spectrum and Reliability of System One Models
- 链接：[arXiv:2611.15777](https://arxiv.org/abs/2611.15777)
- 机构：新加坡国立大学
- 页数：32 页，10 图，7 表

**研究方法：**
1. **证据 grounded 评估**：通过可靠来源和人工验证确保参考标签对模型可见输入的正确性
2. **细粒度能力评估**：领域特定的难度标准，而非一刀切的基准
3. **交互式评估**：模型在沙盒中迭代执行动作，而非静态问答
4. **System One-Two 对比**：推理密集型任务支持两种系统对比

**核心发现：**
1. 扩展和额外推理的收益在不同领域差异显著
2. **强整体性能不意味着可靠的决策**：最佳 System One 模型在可靠性排名中仅列第七
3. 决策稳定性（选项集变化时）和缺失答案识别是关键可靠性指标

**启发：**
- 模型选择需要多维度评估，不能只看平均性能
- 对于高风险应用，可靠性比平均准确率更重要
- System One 模型适合快速决策，但需要额外的可靠性保障机制

---

### 5.2 Actor, Judge, or Teacher：理解决策模型在长周期 Agent 中的作用

**论文信息：**
- 标题：Actor, Judge, or Teacher? Understanding Decision Models in Long-Horizon Agents
- 链接：[arXiv:2611.17167](https://arxiv.org/abs/2611.17167)
- 机构：浙江大学
- 代码：[github.com/ZJU-REAL/decision-agents](https://github.com/ZJU-REAL/decision-agents)

**研究方法：**
1. 在 ALFWorld 上比较 3 个决策模型和 3 个通用 LLM 作为 Actor 和 Judge 的表现
2. 使用 JEV 作为 Teacher 在 ALFWorld 和 WebShop 上训练策略
3. 分析"行动后判断"与"实时决策"的差异

**核心发现：**
1. **作为 Actor 的失败模式**：所有模型都被更容易的子目标吸引，偏离必须先完成的关键子目标
2. **作为 Judge 的成功**：同一模型观察完整轨迹后，能正确识别关键步骤
3. **关键问题区分**："每个动作是否有帮助"比"任务是否会成功"更能区分有用和无用动作
4. **Teacher 效果**：JEV 将 Qwen2.5-1.5B 策略显著提升（ALFWorld: 72.8% → 82.9%，WebShop: 56.8% → 71.4%）

**启发：**
- Agent 架构可以将"判断"和"执行"分离，利用模型的不同能力
- 事后评估揭示了行动时必须预见的后果
- 弱 Actor + 强 Teacher 是有效的训练范式

---

### 5.3 MAPE：通过程序进化发现有效的 Agent 记忆设计

**论文信息：**
- 标题：Discovering Effective Agent Memory Designs through Program Evolution
- 链接：[arXiv:2611.17068](https://arxiv.org/abs/2611.17068)
- 代码：[github.com/ash-ding/MAPE](https://github.com/ash-ding/MAPE)

**研究方法：**
1. **标准化生命周期接口**：定义记忆程序的输入输出规范
2. **迭代诊断-提议循环**：自动识别当前设计的弱点并提出改进
3. **从最小种子进化**：从简单实现开始，逐步进化出复杂设计
4. **多目标优化**：同时优化准确率和服务成本

**核心发现：**
1. **两个反复出现的设计模式**：
   - 保留原始对话作为可检索证据（提取的记忆会遗漏细节）
   - 根据查询意图组合检索证据（帮助模型更有效使用检索信息）
2. **移植验证**：将组合模块移植到 5 个现有记忆系统，全部提升准确率
3. **计算位置转移**：优化服务成本将计算从 LLM 基础的记忆构建转移到查询时的选择性处理

**启发：**
- 程序进化是发现新架构的有效方法
- 保留原始数据作为后备是重要的设计原则
- 成本优化可以引导发现更高效的设计

---

### 5.4 AgentSSL：MLE Agent 利用无标签数据

**论文信息：**
- 标题：AgentSSL: Can MLE Agents Leverage Unlabeled Data?
- 链接：[arXiv:2611.17323](https://arxiv.org/abs/2611.17323)
- 会议：NeurIPS 2026
- 项目：[codiscovery.ai/AgentSSL](https://codiscovery.ai/AgentSSL)

**研究方法：**
1. 将半监督学习框架化为程序搜索问题
2. Agent 合成代码组合和适应已建立的 SSL 技术
3. 引入 ProgramSelectBench 基准（16,977 个程序）
4. 评估无监督和主动程序选择方法

**核心发现：**
1. Agent 在 12 个设置中的 8 个超越最强人工基线（最高 +21.8%）
2. **程序选择是关键瓶颈**：基于 Agent 反馈指标选择时，性能下降高达 47%
3. 在真实生态检测任务上的验证显示了转移的挑战和机遇

**启发：**
- 无标签数据的利用需要精心设计的选择策略
- Agent 反馈指标可能不是可靠的程序选择标准
- 真实世界转移需要额外的适应工作

---

## 六、今日学习建议

### 6.1 立即可以做的事

1. **试用 Qwen3.8-27B**
   ```bash
   # 使用 Ollama
   ollama run qwen3.8:27b
   
   # 或使用 llama.cpp
   # 下载 GGUF 版本从 HuggingFace
   ```

2. **体验 MiniMax-H3 视频生成**
   - 访问 HuggingFace Spaces 上的演示
   - 或使用 ComfyUI 集成本地部署

3. **阅读 SO-Arena 论文**
   - 理解 System One 模型的可靠性问题
   - 反思你当前使用的模型评估方法

### 6.2 本周学习路径

**Day 1-2：基础**
- 阅读 MAPE 论文，理解 Agent 记忆设计的新方法
- 尝试将两个设计模式应用到你的项目

**Day 3-4：实践**
- 部署 Qwen3.8-27B 到本地环境
- 测试其在你的具体场景中的表现

**Day 5：进阶**
- 研究 Actor/Judge/Teacher 范式
- 思考如何在你的 Agent 系统中应用

### 6.3 长期关注方向

1. **System One 模型**：快速决策模型是重要方向，但需要解决可靠性问题
2. **Agent 记忆设计**：MAPE 展示的方法论值得深入学习和应用
3. **开源推理基础设施**：SGLang 联盟的成立标志着开源推理进入新阶段
4. **多模态视频生成**：MiniMax-H3 和 Wan 3.0 代表了开源视频生成的最新水平

---

## 📊 附录：今日数据汇总

### HuggingFace 热门模型 Top 10

| 排名 | 模型 | 类型 | 下载量 |
|------|------|------|--------|
| 1 | Qwen/Qwen3.8-27B | 多模态 | 696 万 |
| 2 | unsloth/Qwen3.8-27B-GGUF | 量化 | 625 万 |
| 3 | MiniMaxAI/MiniMax-H3 | 视频生成 | 654 万 |
| 4 | huihui-ai/Huihui-Qwen3.8-27B-abliterated-GGUF | 去审查 | 405 万 |
| 5 | VideoRebirthAI/hyperflow-h3-flash | 视频生成 | 389 万 |
| 6 | ccore/Qwen3.5-4B-3D-Coder | 代码 | 393 万 |
| 7 | deepseek-ai/DeepSeek-V4.1-Flash-1017 | 多模态 | 398 万 |
| 8 | Lightricks/LTX-2.5 | 图生视频 | 278 万 |
| 9 | unsloth/Qwen3.8-Flash-Next-GGUF | 量化 | 232 万 |
| 10 | facebook/sam3 | 分割 | 209 万 |

### arXiv 今日论文统计

| 类别 | 数量 |
|------|------|
| cs.AI | 321 篇（11 月 13 日） |
| cs.LG | 340 篇 |
| cs.CL | 135 篇 |

### 重要会议截止日期提醒

- **NeurIPS 2026**：悉尼/亚特兰大/巴黎（论文已接受）
- **EMNLP 2026**：布达佩斯（论文已接受，2900+ 篇）

---

## 🔗 资源链接

- [HuggingFace Daily Papers](https://huggingface.co/papers)
- [GitHub Trending](https://github.com/trending)
- [LLM-Stats Leaderboard](https://llm-stats.com/)
- [AIFOD Real-time News](https://af.net/realtime/)
- [Paper Digest](https://resources.paperdigest.org/)
- [SGLang Consortium](https://lmsys.org/)

---

*本情报由 Zoe 🦞 于 2026-11-14 08:00 自动生成*
*数据来源：arXiv、GitHub、HuggingFace、AIFOD、LLM-Stats 等 12+ 来源*
*字数统计：约 12,000 字*
