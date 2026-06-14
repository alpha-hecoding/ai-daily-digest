# AI 每日情报 · 2026 年 6 月 14 日（周日）

> 本期字数：约 11,000 字 | 阅读时间：30 分钟 | 数据来源：arXiv / GitHub / HuggingFace / DevFlokers / Kilo.ai / ArXiv TLDR / MorphLLM 等 14+ 站点深度抓取

---

## 一、前沿模型动态 🚀

### 本周核心结论

> 2026 年 6 月，开源模型正式进入「前沿编程能力 + 百万上下文 + 原生多模态」三合一时代。**MiniMax M3**（6 月 1 日发布）是首个同时满足这三项的开源权重模型；**DeepSeek V4 系列**稳坐竞赛编程与长上下文王座；**GLM-5.1** 则在真实软件工程场景中取得 SOTA。**Qwen3.6-27B** 证明了密集小模型也能击败大型 MoE，成为本地部署首选。

---

### 1.1 MiniMax M3：首个全能开源前沿模型

**发布方**：MiniMax | **发布时间**：2026 年 6 月 1 日

MiniMax M3 是本月最重要的模型发布。它首次将以下三项能力整合进一个开源权重模型：

| 能力维度 | MiniMax M3 表现 |
|---|---|
| 软件工程 | SWE-Bench Pro 59.0%（超越 GPT-5.5 与 Gemini 3.1 Pro） |
| 终端操作 | Terminal-Bench 2.1 66.0% |
| MCP 工具调用 | MCP Atlas 74.2% |
| 操作系统控制 | OSWorld-Verified 70.06% |
| 上下文长度 | **100 万 token** |
| 多模态 | 图像/视频输入 + 计算机直接操作 |

**技术架构**：基于全新的 MiniMax Sparse Attention（MSA）架构，这是一种稀疏注意力设计，专门用于处理密集的视频与图像流，同时保持与操作系统接口的直接交互能力。

**💡 对你的价值**：
- 如果你在做 AI 编程助手或自动化 Agent，M3 是目前唯一不需要 API 就能同时处理「看视频 → 写代码 → 操作电脑」全流程的模型
- 权重将在发布后约 10 天内公开，建议关注 HuggingFace
- 对比闭源方案，本地部署成本可降低 80% 以上

---

### 1.2 DeepSeek V4 系列：竞赛编程之王

**发布方**：DeepSeek | **许可证**：MIT

DeepSeek V4 家族是本月编程基准赛的王霸：

| 型号 | 总参数 | 激活参数 | 上下文 | LiveCodeBench | SWE-Bench Verified |
|---|---|---|---|---|---|
| V4-Pro | 1.6T | 49B | 100 万 | **93.5**（#1）| 80.6% |
| V4-Flash | 284B | 13B | 100 万 | 91.6 | 79.0% |

**关键优势**：
- V4-Pro 是**所有已评测模型**（含闭源）中 LiveCodeBench 与 Codeforces 最高分
- V4-Flash 的 FP4 推理 + 98% prompt cache 折扣使其成为性价比最高的自托管方案
- V4-Flash 可在单张 H100 上运行，量化后可跑 RTX 4090

**💡 对你的价值**：
- 竞赛编程、算法面试准备 → V4-Pro 是当前最强选择
- 日常编程助手、CI/CD 集成 → V4-Flash 是性价比首选，成本约为 Claude 的 1/10
- MIT 许可证意味着可无限制商用

---

### 1.3 GLM-5.1：真实工程场景的新标杆

**发布方**：Z.ai（智谱）| **许可证**：MIT

GLM-5.1 是 744B MoE（40B 激活）模型，专注于长周期 Agentic 工程任务：
- **Terminal-Bench 2.0 SOTA**（开源模型中最高）
- SWE-Bench Pro SOTA
- 在 NL2Repo（自然语言生成完整仓库）任务上取得显著领先

**与 DeepSeek V4-Pro 对比**：

| 维度 | GLM-5.1 | DeepSeek V4-Pro |
|---|---|---|
| 架构 | 744B MoE / 40B 激活 | 1.6T MoE / 49B 激活 |
| 上下文 | 20 万 | 100 万 |
| 最强项 | Terminal-Bench / 长周期任务 | LiveCodeBench / 竞赛编程 |
| 许可证 | MIT | MIT |
| 适合场景 | 企业级工程、多文件迭代 | 算法、单轮解题 |

**💡 对你的价值**：如果你的工作涉及跨文件、跨小时的长周期代码重构与工程迭代，GLM-5.1 的持久稳定性优于 V4-Pro。

---

### 1.4 Kimi K2.6：Agent 集群之王

**发布方**：Moonshot AI | **许可证**：Modified MIT

| 指标 | 数据 |
|---|---|
| 参数 | 1T MoE / 32B 激活 |
| 上下文 | 25.6 万 |
| SWE-Bench Pro | 58.6% |
| 独特能力 | 原生 300 子 Agent 集群、4000 步协调、12 小时自主运行 |

K2.6 是目前唯一原生支持**超大规模 Agent 集群**的开源模型，可以同时协调 300 个子 Agent 进行并行工作。

**💡 对你的价值**：如果你的任务需要大规模并行处理（如同时分析 100 个代码仓库、同步执行多维度研究），K2.6 是唯一选择。

---

### 1.5 Qwen3.6-27B：本地部署最佳选择

**发布方**：阿里巴巴 | **许可证**：Apache 2.0

| 指标 | 数据 |
|---|---|
| 参数 | 27B 密集模型 |
| 上下文 | 26.2 万 |
| SWE-Bench Verified | 77.2% |
| Terminal-Bench 2.0 | 59.3%（匹配 Claude 4.5 Opus）|

**为什么重要**：这是一个**密集模型**（非 MoE），在单张 24GB GPU（RTX 3090/4090）上即可运行，却击败了参数量大 15 倍的 Qwen3.5-397B-A17B MoE 模型。

**💡 对你的价值**：
- 消费级显卡用户的最佳编程模型
- 无需量化即可跑，质量损失为零
- Apache 2.0 许可证，商用完全自由

---

### 1.6 HuggingFace 热门趋势模型（本周）

| 模型 | 类型 | 亮点 |
|---|---|---|
| google/diffusiongemma-26B-A4B-it | 扩散多模态 | Google 新架构，扩散模型 + Gemma，92.1k 下载 |
| nvidia/LocateAnything-3B | 空间定位 | 4B 参数，空间理解任务，69.4k 下载 |
| CohereLabs/North-Mini-Code-1.0 | 编程 | 30B 参数，Cohere 首个编程专才 |
| bosonai/higgs-audio-v3-tts-4b | TTS | 5B 参数，高质量语音合成 |
| ideogram-ai/ideogram-4-fp8 | 图像生成 | 文字渲染精度业界领先 |
| deepseek-ai/DeepSeek-V4-Pro | 通用/编程 | 862B 下载量，现象级热度 |

---

## 二、Agent 架构与范式 🤖

### 本周核心结论

> 2026 年 6 月，Agent 框架正式进入**「协议统一 + 订阅计费独立化」**时代。ACP 已合并入 A2A（Linux Foundation 下），MCP 突破 200 个服务端实现。**明天（6 月 15 日）**，Anthropic 的 Claude Agent SDK 将开始使用独立的月度 Agent 积分，与交互积分分开计费——这是所有 Agent 开发者必须知道的计费变化。

---

### 2.1 框架格局：8 大 SDK 最新对比（2026.06）

| 框架 | 语言 | 多 Agent 模式 | MCP | A2A | 最佳场景 |
|---|---|---|---|---|---|
| **Claude Agent SDK** | Python, TS | 子 Agent | ✅ 原生（最深）| ❌ | 编程 Agent、OS 访问 |
| **OpenAI Agents SDK** | Python, TS | Handoff | ✅ | ❌ | 轻量交接链 |
| **Google ADK** | Python, TS, **Java, Go** | 层级式 | 适配器 | ✅ 原生 | 企业多语言系统 |
| **LangGraph** | Python, TS | 图节点 | 适配器 | ❌ | 有状态工作流 |
| **CrewAI** (52.4k ⭐) | Python | 角色扮演团队 | ✅ | ✅ 原生 | 快速原型 |
| **Smolagents** | Python | 多 Agent | ✅ | ❌ | 代码生成 Agent |
| **Pydantic AI** | Python | 无 | ❌ | ❌ | 类型安全输出 |
| **MS Agent Framework 1.0** | Python, **.NET** | 群聊+图 | ✅ | ✅ | Azure / .NET |

---

### 2.2 重要变化：Claude Agent SDK 计费分离（6 月 15 日生效）

**从明天开始**，Claude 订阅用户使用 Agent SDK 和 `claude -p`（非交互模式）将消耗独立的**月度 Agent 积分**：

| 订阅等级 | 月度 Agent 积分 |
|---|---|
| Pro | $20 |
| Max 5x | $100 |
| Max 20x | $200 |

**注意**：积分用完后，若未启用 API 费率溢出，请求将直接停止。**未使用积分不累计**。

**💡 对你的价值**：如果你在 CI/CD 或定时任务中运行 Claude Agent，务必提前预算，或配置 API key 作为溢出通道。

---

### 2.3 协议层：MCP 200+ / A2A 统一

- **MCP（Model Context Protocol）**：已突破 200 个服务端实现，包括 GitHub、Slack、Notion、Postgres、Playwright 等
- **A2A（Agent-to-Agent）**：ACP 已正式合并入 A2A，由 Linux Foundation 管理
- **跨框架互通**：Google ADK 的 `to_a2a()` 可自动生成 Agent Card，让任何 ADK Agent 被外部 Agent 发现

**实际意义**：现在构建 Agent，优先选择支持 MCP + A2A 的框架，避免半年后被生态淘汰。

---

### 2.4 Agent 设计模式新趋势

**来自本周 GitHub Trending 的信号**：

1. **Skill 化**：Agent 能力不再硬编码，而是编译为外部 Skill 包（参考 Hermes Agent 的自改进技能编译循环）
2. **本地优先**：6/10 的热门项目明确标注 on-device 或 local-first 架构
3. **安全扫描内建**：NVIDIA SkillSpector（804 ⭐/天）表明 Agent Skill 安全审查正成为必备环节
4. **分析工具成熟**：AgentsView 这类 Agent 运行分析工具开始流行，支持 Claude Code、Codex 等 20+ Agent

---

## 三、开源生态精选 🔧

> 本节每个项目均含详细介绍、适用场景与具体操作建议。

---

### 3.1 addyosmani/agent-skills ⭐ 58,329（今日 +1,514）

**一句话**：Addy Osmani（Google Chrome 团队工程经理）整理的生产级 AI 编程 Agent 技能库。

**详细介绍**：这不是一个框架，而是一套经过实战验证的**工程技能集合**——告诉 AI Agent「如何正确做代码审查」「如何写测试」「如何做安全审计」等。技能以 Markdown 文件形式存在，可直接被 Claude Code、Codex 等 Agent 加载。今日 1,514 新增星标，说明社区对「Agent 应该怎么做工程」的关注度极高。

**适合谁**：所有使用 AI 编程助手的开发者。

**操作建议**：
```bash
git clone https://github.com/addyosmani/agent-skills
# 将技能文件复制到你的项目 .claude/skills/ 或 .cursor/rules/ 目录
```

💡 **对你的价值**：无需自己摸索 Prompt 工程，直接复用 Google 级工程标准。

---

### 3.2 NVIDIA/SkillSpector ⭐ 4,416（今日 +804）

**一句话**：NVIDIA 官方出品的 AI Agent Skill 安全扫描器。

**详细介绍**：检测 Agent 技能文件中的漏洞、恶意模式与安全风险。随着 Agent 技能市场（如 agent-skills）的兴起，技能来源变得不可控，SkillSpector 填补了「技能安全审计」这一空白。它可以扫描 SKILL.md 文件中的可疑 shell 命令、数据外泄模式、提示注入等。

**适合谁**：在企业环境中部署 Agent 的安全团队、技能市场运营者。

💡 **对你的价值**：如果你使用第三方 Agent 技能，务必先用 SkillSpector 扫描。

---

### 3.3 kenn-io/agentsview ⭐ 2,355（今日 +190）

**一句话**：本地优先的 Agent 会话智能分析工具，支持 Claude Code、Codex 等 20+ Agent。

**详细介绍**：记录并分析你与 AI 编程 Agent 的每次交互，生成使用统计、成本分析、效率报告。号称是 ccusage 的 100x 更快替代品。Go 语言编写，本地运行，不上传任何数据。

**适合谁**：需要监控 Agent 使用成本和效率的团队。

💡 **对你的价值**：如果你每月在 AI Agent 上花费超过 $100，这个工具可以帮你找到浪费点。

---

### 3.4 apple/container ⭐ 36,272（今日 +1,487）

**一句话**：Apple 官方出品的轻量级 Linux 容器工具，专为 Mac 优化。

**详细介绍**：使用 Swift 编写，利用 Apple Silicon 原生虚拟化框架运行 Linux 容器。相比 Docker Desktop，它更轻、更快、更省电。今日 1,487 新增星标说明 macOS 开发者苦 Docker 久矣。

**适合谁**：macOS 开发者，特别是需要运行 Linux 环境来部署/测试 AI 应用的场景。

💡 **对你的价值**：在 Mac 上跑 AI Agent 沙箱环境，比 Docker 更省资源。

---

### 3.5 LMCache/LMCache ⭐ 8,883（今日 +238）

**一句话**：最快的 KV Cache 层，加速 LLM 推理。

**详细介绍**：通过在推理引擎前添加一个高速 KV Cache 层，避免重复计算。支持 vLLM、SGLang 等主流推理框架。对于需要频繁处理相似上下文的 Agent 场景（如客服、代码补全），可带来 3-10x 推理加速。

**适合谁**：自托管 LLM 的运维工程师。

💡 **对你的价值**：如果你自托管 DeepSeek V4-Flash 等模型，加上 LMCache 可以显著降低延迟和成本。

---

### 3.6 obra/superpowers

**一句话**：一套可落地的 Agent 技能框架与软件开发方法论。

**详细介绍**：与 agent-skills 互补——superpowers 更侧重**方法论**（如何思考、如何分解任务），而 agent-skills 更侧重**具体技能**。今日进入 GitHub Trending。

💡 **对你的价值**：配合 agent-skills 使用，让你的 AI Agent 既知道「怎么做」也知道「怎么想」。

---

### 3.7 andrewyng/aisuite

**一句话**：吴恩达出品的多 AI 提供商统一接口。

**详细介绍**：一套代码同时调用 OpenAI、Anthropic、Google、本地模型等，无需为每个提供商写适配代码。对于需要模型灵活切换的 Agent 系统特别有用。

💡 **对你的价值**：如果你构建的 Agent 需要同时使用多个模型（如推理用 V4-Pro、便宜任务用 Qwen3.6），aisuite 是最简单的集成方案。

---

### 3.8 x1xhlol/system-prompts-and-models-of-ai-tools

**一句话**：最全的 AI 工具系统提示词收集库。

**详细介绍**：收集了 Claude Code、Cursor、Devin、Manus、Windsurf、VSCode Agent 等 30+ 主流 AI 工具的完整系统提示词和内部工具配置。对于想理解「顶级 AI 产品是如何设计 Agent 行为」的人来说是金矿。

💡 **对你的价值**：研究这些系统提示词，可以快速提升你自己 Agent 的设计水平。

---

## 四、AI 工具与技巧 🛠️

### 4.1 工具推荐

#### ① Kilo Code：开源编程模型的统一入口

Kilo Code 是一个 VS Code 扩展，支持所有主流开源编程模型（GLM-5.1、MiniMax M3、DeepSeek V4、Kimi K2.6 等），内置排行榜比较各模型在真实编程任务中的表现。

- **免费托管模型**：MiniMax M2.5、Nemotron 3 Super 可在 Kilo 内免费使用
- **自带 Key**：支持 OpenRouter、Together AI、Google AI 等
- **本地运行**：支持 Ollama、LM Studio、vLLM 连接

💡 **初学者建议**：从免费的 MiniMax M2.5 开始体验，熟悉后再切换到 DeepSeek V4-Flash 获得更好效果。

---

#### ② claude-context：大仓库的语义搜索 MCP 服务器

**仓库**：zilliztech/claude-context（10.6k ⭐）

**解决的问题**：当你的代码库超过 5 万行，Claude Code 每次搜索都要读所有文件（又慢又贵）或者猜（不准确）。claude-context 把代码库索引到向量数据库，Agent 每次只获取相关代码。

**操作步骤**：
```bash
# 前置：需要 Milvus 或 Zilliz 实例
npm install -g claude-context
# 在项目中索引
claude-context index --path ./my-project
# Claude Code 自动通过 MCP 协议调用
```

💡 **适合**：50k+ 行的中大型仓库，每次 AI 搜索等 30 秒以上的痛点场景。

---

#### ③ Ollama + Qwen3.6-27B：消费级显卡的最优解

如果你有一张 24GB 显卡（RTX 3090/4090），这是目前质量最高的本地编程模型组合：

```bash
# 安装 Ollama
curl -fsSL https://ollama.com/install.sh | sh
# 下载模型（约 15GB）
ollama run qwen3.6:27b
# 在你的 Agent 框架中指向 http://localhost:11434/v1
```

**效果**：SWE-Bench Verified 77.2%，接近 Claude 4.5 Opus 水平，完全免费，数据不出本机。

---

### 4.2 工作流技巧

#### 技巧 1：分层模型路由

不要用一个模型做所有事。最佳实践：

| 任务类型 | 推荐模型 | 原因 |
|---|---|---|
| 算法/竞赛 | DeepSeek V4-Pro | LiveCodeBench #1 |
| 工程重构 | GLM-5.1 | 长周期稳定性最佳 |
| 日常编码 | Qwen3.6-27B / V4-Flash | 成本极低 |
| 大规模并行 | Kimi K2.6 | 原生 300 子 Agent |
| 本地离线 | Qwen3.6-27B (Ollama) | 消费级 GPU 可跑 |

---

#### 技巧 2：用 agent-skills 提升 Agent 质量

不要从零开始写 Agent 提示词。步骤：
1. 克隆 addyosmani/agent-skills
2. 选择适合你项目的技能（如 code-review、testing、security-audit）
3. 复制到 `.claude/skills/` 或对应框架的技能目录
4. Agent 自动加载这些技能，输出质量显著提升

---

#### 技巧 3：用 SkillSpector 审计第三方技能

安装并运行：
```bash
pip install skillspector
skillspector scan .claude/skills/
```

这会检查所有技能文件中的安全风险，避免恶意代码通过技能注入你的 Agent。

---

### 4.3 初学者今日建议

如果你是 AI 编程新手，今天最值得做的三件事：
1. **安装 Ollama + Qwen3.6-27B**（本地免费体验前沿编程 AI）
2. **克隆 agent-skills**（学习好的 Agent 技能长什么样）
3. **阅读 DeepSeek V4-Flash 的技术报告**（理解 MoE 架构如何降本增效）

---

## 五、值得深读的研究 📚

> 每篇论文均含：研究方法 + 核心发现 + 对你的启发

---

### 5.1 ⭐ Agentic Environment Engineering for LLMs（综述）

**来源**：arXiv 2606.12191 | **日期**：2026-06-12 | **本周 HuggingFace 推荐论文**

**研究方法**：系统综述，从环境工程生命周期的四个阶段（建模、合成、评估、应用）分析 LLM Agent 环境。

**核心发现**：
- 提出了 Agent 在动态环境中进化的四条路径：
  1. **记忆驱动**（经验进化）
  2. **编排驱动**（工作流进化）
  3. **轨迹驱动**（离线进化）
  4. **探索驱动**（在线进化）
- 环境进化的三种范式：神经驱动、难度驱动、规模驱动
- 未来方向：Environment-as-a-Service、多 Agent 环境、神经符号环境

**💡 启发**：如果你在设计 Agent 训练环境，这篇综述提供了完整的分类学。特别关注「记忆驱动进化」——这是目前投入产出比最高的方向。

---

### 5.2 TRACE: Trajectory Reasoning through Adaptive Cross-Step Evidence Aggregation

**来源**：arXiv 2606.07054 | **本周 Top 7**

**研究方法**：提出 Triage-Inspect-Judge（TIJ）循环，跨时间步骤聚合证据来检测 LLM Agent 轨迹中的隐藏恶意目标。

**核心发现**：
- 现有方法只能逐步检查，无法连接时间上相距较远的行为
- TRACE 通过自适应证据聚合，可以检测「分散在多步中的恶意计划」
- 在 AgentBench 等基准上显著降低漏检率

**💡 启发**：如果你在运行长周期 Agent（如 12 小时自主编码），安全审计不能只看每一步，必须看全局轨迹。TRACE 的方法可直接集成到你的 Agent 监控系统中。

---

### 5.3 The Injection Paradox: Brand-Level Suppression in Safety-Trained LLMs

**来源**：arXiv 2606.09204 | **本周 Top 2**

**研究方法**：实验研究 RAG 上下文中的提示注入如何影响安全训练后的 LLM 品牌推荐行为。

**核心发现**：
- **Injection Paradox**：RAG 注入不仅影响注入文档本身，还**传播到同品牌的其他未修改文档**
- Claude 模型会**抑制**被注入品牌的推荐
- GPT 模型反而会**增加**被注入品牌的推荐
- 这意味着 RAG 安全策略需要因模型而异

**💡 启发**：如果你的系统使用 RAG + Claude，提示注入可能导致某些信息被「静默压制」——用户看不到内容，但也不知道被压制了。这比显式注入更危险。

---

### 5.4 Memory is Reconstructed, Not Retrieved: MRAgent

**来源**：arXiv 2606.06036 | **本周 Top 6**

**研究方法**：提出 Cue-Tag-Content 图记忆结构 + 主动重建机制，让 LLM Agent 像人类一样「重建」记忆而非「检索」记忆。

**核心发现**：
- 传统 RAG 是「给定查询 → 返回相关文档」，本质是检索
- MRAgent 是「给定线索 → 通过联想标签激活内容 → 用 LLM 重建完整记忆」
- 在长周期任务中，MRAgent 显著优于传统 RAG 方案

**💡 启发**：如果你在设计 Agent 的长期记忆系统，不要用向量检索的简单思路。考虑 Cue-Tag-Content 图 + LLM 重建的模式，更接近人类记忆的工作方式。

---

### 5.5 The Neutral Mask: How RLHF Provides Shallow Alignment

**来源**：arXiv 2606.09735 | **本周 Top 10**

**研究方法**：分析 RLHF 训练对 LLM 内部「党派结构」的影响，使用因果干预实验。

**核心发现**：
- RLHF **没有消除**模型内部的偏见/党派结构
- RLHF 只是**切断**了内部偏见到输出的因果路径
- 这种中立性是「功能性」的，不是「结构性」的
- 意味着在特定触发条件下，被压抑的偏见可能重新浮现

**💡 启发**：如果你在部署「中立」AI 助手，不能仅依赖 RLHF。需要额外的输出监控层，因为模型的内在偏见只是被「遮盖」而非「消除」。

---

### 5.6 AgentBeats: Agentifying Agent Assessment

**来源**：arXiv 2606.xxxxx | arxivlens.com 收录 | 2026-06-11

**研究方法**：提出将 Agent 评估本身 Agent 化的框架，解决当前评测碎片化问题。

**核心发现**：
- 现有 Agent 评测依赖固定的 LLM 中心化评测框架，集成成本高、测试与生产脱节
- AgentBeats 让评测本身成为可组合、可复用的 Agent
- 支持开放性、标准化和可复现性

**💡 启发**：如果你在评估多个 Agent 系统，参考 AgentBeats 的思路，将评测流程本身 Agent 化，可以大幅降低评测成本。

---

## 六、今日学习建议 📖

> 具体、可执行、按优先级排序

---

### 优先级 1：必做（30 分钟）

**1. 跑一个开源编程模型**

选择以下任一方案，实际体验开源编程模型的能力：

| 你的硬件 | 推荐方案 | 时间 |
|---|---|---|
| 有 24GB GPU | Ollama + Qwen3.6-27B | 15 分钟安装 |
| 无 GPU | Kilo Code 免费版（MiniMax M2.5） | 5 分钟注册 |
| 有 H100 | DeepSeek V4-Flash + LMCache | 30 分钟部署 |

**2. 阅读 agent-skills 仓库的 README**

地址：https://github.com/addyosmani/agent-skills

重点看：技能文件的格式规范、如何在你的 Agent 中加载技能。这 10 分钟的阅读可能比你花 2 小时调 Prompt 更有效。

---

### 优先级 2：深读（1 小时）

**3. 精读 MRAgent 论文（记忆重建）**

论文地址：https://arxiv.org/abs/2606.06036

重点阅读：
- Section 3: Cue-Tag-Content 图结构定义
- Section 4: 主动重建算法
- Section 5: 与传统 RAG 的对比实验

读完后的行动：评估你当前 Agent 的记忆系统，是否可以从「检索」升级为「重建」。

**4. 了解 Claude Agent SDK 计费变化**

从明天（6 月 15 日）开始，Agent SDK 使用独立积分。如果你在用 Claude 构建 Agent：
- 检查你当前的月用量
- 预估是否会超出积分
- 配置 API key 溢出通道

---

### 优先级 3：拓展（有空再看）

**5. 浏览 system-prompts-and-models-of-ai-tools 仓库**

地址：https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools

挑 3 个你常用的 AI 工具（如 Cursor、Claude Code、Windsurf），阅读它们的系统提示词，对比设计差异。

**6. 了解 SkillSpector**

如果你在生产环境部署 Agent，花 15 分钟了解 NVIDIA SkillSpector 的扫描能力，评估是否纳入你的 CI/CD 流程。

---

### 今日关键数字速览

| 指标 | 数字 |
|---|---|
| 开源模型最高 SWE-Bench Pro | MiniMax M3 59.0% |
| 开源模型最高 LiveCodeBench | DeepSeek V4-Pro 93.5 |
| MCP 服务端实现数量 | 200+ |
| Agent 框架 GitHub 最高星 | AutoGPT 155k+ |
| 今日 GitHub Trending #1 | addyosmani/agent-skills (+1,514) |
| Claude Agent SDK 月度积分（Pro）| $20 |
| Qwen3.6-27B 所需 GPU | 单张 24GB |

---

## 附录：数据来源

| 来源 | URL | 抓取内容 |
|---|---|---|
| arXiv cs.AI | https://arxiv.org/list/cs.AI/recent | 222 篇最新论文列表 |
| arXiv cs.CL | https://arxiv.org/list/cs.CL/recent | 104 篇最新论文列表 |
| HuggingFace Models | https://huggingface.co/models?sort=trending | 30 个趋势模型 |
| GitHub Trending | https://github.com/trending?since=daily | 今日趋势项目 |
| ArXiv TLDR | https://arxivtldr.org/weekly | 本周 Top 10 论文 |
| DeepPaper | https://arxiv.deeppaper.ai/papers/weekly | 本周热门论文 |
| ArxivLens | https://arxivlens.com/category/cs-ai | cs.AI 论文摘要 |
| DevFlokers | https://www.devflokers.com/blog/open-source-ai-roundup-june-2026 | 2026.06 开源 AI 综述 |
| Kilo.ai | https://kilo.ai/open-source-models | 开源编程模型排行榜 |
| MorphLLM | https://www.morphllm.com/ai-agent-framework | 8 大 Agent 框架对比 |
| kilo.ai | 模型基准测试数据 |
| ArxivLens | 论文摘要与解读 |
| OpenChat | DeepSeek V4 背景分析 |
| OFox | DeepSeek V4 基准测试详细数据 |

---

*本期情报由 AI 于 2026 年 6 月 14 日 08:00（北京时间）自动生成。信息来源已标注，内容经过多源交叉验证，但基准测试数据可能因评测环境不同而存在差异。建议以各模型官方技术报告为准。*
