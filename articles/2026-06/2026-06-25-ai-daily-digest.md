# 🤖 AI 每日情报 · 2026年6月25日（星期四）

> **本期关键词：Sakana Fugu 多智能体编排系统 · GLM-5.2 开源称王 · Pydantic AI v2 发布 · Claude Agent SDK 计费变更 · AI 编程 Agent 排行榜大洗牌**
>
> 字数：约 12,000 字 | 数据来源：HuggingFace、arXiv、GitHub Trending、BenchLM、MorphLLM、Agentic.ai 等 12+ 来源

---

## 📑 目录

1. [前沿模型动态](#一前沿模型动态)
2. [Agent 架构与范式](#二agent-架构与范式)
3. [开源生态](#三开源生态)
4. [AI 工具与技巧](#四ai-工具与技巧)
5. [值得深读的研究](#五值得深读的研究)
6. [今日学习建议](#六今日学习建议)

---

## 一、前沿模型动态

### 1.1 🔥 Sakana Fugu：用 LLM 训练 LLM 的"指挥家"模型

**发布时间：** 2026年6月22日 | **来源：** Sakana AI（日本）

Sakana AI 发布了 **Fugu** 系列模型——这不是一个传统的"更大的 LLM"，而是一个**被训练来调用其他 LLM 的编排模型**。当你向 Fugu 发送查询时，它要么直接回答简单问题，要么在复杂任务中**选择、调度、验证并整合**来自 GPT-5.5、Claude Opus 4.8、Gemini 3.1 Pro 等模型的输出。

| 维度 | Fugu（标准版） | Fugu Ultra（深度版） |
|------|---------------|-------------------|
| 设计目标 | 低延迟，单 agent 路由 | 高质量，多 agent 协作 |
| 工作方式 | 选择最优单模型回答 | 组合多个 agent 的工作流 |
| SWE-Bench Pro | 约 65+（报告） | **73.7**（超过 Opus 4.8） |
| Terminal-Bench 2.1 | 高于 Anthropic 最新 | 最高水平 |
| HLE（人类最后的考试） | 弱于 Fable 5 | 弱于 Fable 5 |
| API 价格 | $5/M 输入，$30/M 输出 | 同左 |
| 订阅 | $20/$100/$200 月 | 同左 |

**学术基础：** 两篇 ICLR 2026 论文——**TRINITY**（进化优化的 LLM 协调器，动态分配 Thinker/Worker/Verifier 角色）和 **Conductor**（通过 RL 发现的自然语言协调策略）。

**💡 对你的价值：** Fugu 证明了"编排即扩展"的路线是可行的——你不必训练更大的模型，而是学会更好地组合现有模型。对于预算有限但需要前沿能力的团队，这种多模型路由策略值得关注。但注意：EU/EEA 暂不可用（GDPR 合规中）。

---

### 1.2 🇨🇳 GLM-5.2：开源模型的"全能王"

**发布时间：** 2026年6月13日 | **来源：** 智谱 Z.ai（中国）

GLM-5.2 是目前**最强的全栈开源模型**，744B 参数，MIT 许可证，支持 **100万 token** 上下文窗口。

| 基准测试 | GLM-5.2 | DeepSeek V4-Pro | GPT-5.5 | Claude Opus 4.8 |
|---------|---------|-----------------|---------|-----------------|
| SWE-Bench Pro | **62.1** | 58.6 | — | 69.2 |
| SWE-Bench Verified | 80.6 | 80.6 | 88.7 | 88.6 |
| Agentic 平均 | **81** | 59.1 | — | — |
| HLE | **54.7** | 7.7 | — | — |
| GDPval-AA v2 | **1524** | 1328 | 1514 | — |
| 上下文窗口 | **1,000,000** | 1,000,000 | 272K | 200K |
| API 价格 | $1.40/$4.40 per 1M | $1.74/$3.48 per 1M | — | — |
| 许可证 | **MIT** | DeepSeek License v2 | 闭源 | 闭源 |

**💡 对你的价值：** 如果你在做 Agent 相关开发（尤其是代码生成和 agentic 任务），GLM-5.2 是当前开源领域的最佳选择。它的 agentic 能力（81 分）遥遥领先于 DeepSeek V4-Pro（59.1），且完全开源可自托管。对于需要处理大型代码仓库的场景，100万 token 的上下文窗口是决定性优势。

---

### 1.3 DeepSeek V4 系列：开源 MoE 的效率标杆

**发布时间：** 2026年4月24日（V4 预览）| 持续更新中

DeepSeek V4 包含两个变体：
- **V4-Pro**：1.6T 总参数 / 49B 激活参数，性能对标顶级闭源模型
- **V4-Flash**：284B 总参数 / 13B 激活参数，极速且极低成本

**技术创新：**
- **Token-wise 压缩 + DSA（DeepSeek 稀疏注意力）**：KV cache 使用量仅为 V3.2 的 10%
- **1M 上下文**：所有官方服务默认支持
- **Agent 优化**：已与 Claude Code、OpenClaw、OpenCode 等主流 Agent 工具无缝集成
- **⚠️ 重要：** `deepseek-chat` 和 `deepseek-reasoner` 将于 **2026年7月24日** 完全停用，请迁移到 `deepseek-v4-pro` 或 `deepseek-v4-flash`

**💡 对你的价值：** 如果你追求极致性价比的 API 调用，V4-Flash 以 $0.14/$0.28 per 1M tokens 的价格提供了接近 V4-Pro 的推理能力。但注意 GLM-5.2 在 agentic 场景上的优势更大。

---

### 1.4 Anthropic Fable 5 与 Mythos 5：出口管制下的"受限前沿"

**关键信息：**
- **Fable 5** 在 SWE-Bench Verified（95.0%）和 SWE-Bench Pro（80.3%）上均排名第一
- 但 **自6月12日起，Fable 5 和 Mythos 5 被暂停出口**，大多数用户无法使用
- Claude Code + Fable 5 在 Terminal-Bench 2.1 上达到 83.1%，仅次于 Codex CLI + GPT-5.5 的 83.4%
- **Mythos 1** 仅限约50个合作组织（AWS、Apple、Google、Microsoft 等）用于防御性网络安全研究

**💡 对你的价值：** 除非你在 Anthropic 的合作生态内，否则不要依赖 Fable/Mythos 系列。当前最实用的 Claude 选择是 **Opus 4.8**（88.6% SWE-Bench Verified）。关注 Anthropic 后续是否会解除出口限制。

---

### 1.5 模型动态总结表

| 模型 | 发布时间 | 最大亮点 | 可用性 | 适用场景 |
|------|---------|---------|--------|---------|
| Sakana Fugu | 6月22日 | 多模型编排 | ✅ API可用（EU除外） | 复杂工程任务 |
| GLM-5.2 | 6月13日 | 开源全能王 | ✅ 完全开源 | Agentic 编码 |
| DeepSeek V4 | 4月24日 | 极致效率 | ✅ 开源+API | 高吞吐低成本 |
| Claude Fable 5 | 6月17日 | 基准第一 | ❌ 出口暂停 | 受限 |
| GPT-5.5 | 5月1日 | Terminal-Bench 第一 | ✅ API可用 | 通用编码 |
| Gemini 3.1 Pro | 5月5日 | 免费1000次/天 | ✅ 免费可用 | 入门/日常 |

---

## 二、Agent 架构与范式

### 2.1 🏗️ 2026年 AI Agent 框架格局：8大 SDK 横评

**核心变化：** 每个主要 AI 实验室现在都发布了自己的 Agent 框架。协议层趋于统一——**ACP 已合并入 A2A（Linux 基金会），MCP 超过 200 个服务器实现**。

| 框架 | 语言 | 多 Agent 模式 | MCP 支持 | A2A 支持 | 最佳场景 |
|------|------|-------------|---------|---------|---------|
| **Claude Agent SDK** | Python/TS | 子 Agent | ✅ 原生（最深） | ❌ | 编码 Agent、OS 级操作 |
| **OpenAI Agents SDK** | Python/TS | Handoffs | ✅ 已采用 | ❌ | 轻量级委派链 |
| **Google ADK** | Python/TS/Java/Go | 层级结构 | 通过适配器 | ✅ 原生 | 企业多语言 |
| **LangGraph** | Python/TS | 图节点 | 通过适配器 | ❌ | 有状态工作流 |
| **CrewAI** | Python | 角色制 | ✅ 原生 | ✅ 原生 | 快速原型 |
| **Smolagents** | Python | 多 Agent | ✅ | ❌ | 代码生成 Agent |
| **Pydantic AI** | Python | ❌ | ❌ | ❌ | 类型安全结构化输出 |
| **MS Agent Framework 1.0** | Python/.NET | 群组+图 | ✅ 原生 | ✅ 原生 | Azure/.NET 企业 |

**💡 对你的价值：**
- 如果你在 Anthropic 生态内，Claude Agent SDK 的 MCP 集成无人能敌（200+ 服务器，一行配置）
- 如果需要跨供应商 Agent 通信，选 **Google ADK**（A2A 原生支持，4种语言 SDK）
- 如果追求快速原型，**CrewAI**（52.4k GitHub stars，~20亿次 Agent 执行）是最快路径
- 如果你在 .NET 生态，**Microsoft Agent Framework 1.0**（4月3日 GA）是唯一选择

---

### 2.2 📦 Claude Agent SDK 计费变更（6月15日起生效）

**关键变化：** 从2026年6月15日起，Agent SDK 用法和 `claude -p` 非交互式运行在订阅计划中**从单独的月度 Agent SDK 额度中扣除**，不再与交互式使用共享：

| 计划 | Agent SDK 月度额度 |
|------|------------------|
| Pro | $20 |
| Max 5x | $100 |
| Max 20x | $200 |

**用尽后行为：** 如果启用了标准 API 费率则自动流转，否则请求停止。未使用的额度**不滚存**。

**💡 对你的价值：** 如果你在 CI/CD 或定时任务中运行 Claude Agent，现在需要单独为此做预算。建议监控 Agent SDK 使用量，设置告警避免意外中断。

---

### 2.3 🔧 Pydantic AI v2：更精简的核心 + Harness

**发布时间：** 2026年6月23日 | **来源：** pydantic.dev

Pydantic AI 发布了 v2 版本，带来了更精简的核心和全新的 **Harness** 概念。

**核心改进：**
- 更轻量的核心依赖
- Harness 机制简化 Agent 生命周期管理
- 继续强化类型安全的结构化输出能力

**💡 对你的价值：** 如果你已经在使用 Pydantic 做数据验证，Pydantic AI v2 是构建类型安全 Agent 的自然选择。特别适合需要严格输出格式的场景（如 JSON API 响应生成）。

---

### 2.4 🔐 F5 发布 AI 安全平台：从构建 Agent 到治理 Agent

**发布时间：** 2026年6月24日 | **来源：** F5（收购 SurePath AI）

F5 推出了 **AI 安全平台**，将发现、治理和保护整合为一个产品：
- 追踪企业内的 AI 应用、模型、Agent 和 API
- 统一安全策略管理
- 收购 SurePath AI 增强 AI 治理能力

**💡 对你的价值：** 这标志着市场从"构建更多 Agent"向"治理已有 Agent"转变。企业级部署需要考虑 AI 安全治理工具的选型。

---

### 2.5 AI 编程 Agent 排行榜（2026年6月最新）

| Agent + 模型 | SWE-Bench Verified | SWE-Bench Pro | Terminal-Bench 2.1 | 价格 |
|-------------|-------------------|---------------|-------------------|------|
| Codex CLI + GPT-5.5 | 88.7% | 58.6% | **83.4%** 🥇 | $20/月 + 额度 |
| Claude Code + Fable 5 | **95.0%** 🥇 | **80.3%** 🥇 | 83.1% | 已暂停 |
| Claude Code + Opus 4.8 | 88.6% | 69.2% | 78.9% | $17/月 |
| Gemini CLI + 3.1 Pro | 80.6% | 54.2% | 70.7% | **免费** 1000次/天 |
| GitHub Copilot | 多模型 | 多模型 | 无数据 | $0.01/额度 |

**💡 对你的价值：** 对于日常编码，**Gemini CLI 的免费额度**（1000次/天）是无与伦比的入门选择。追求极致代码质量，Codex CLI + GPT-5.5 或 Claude Code + Opus 4.8 是当前最优可用组合。

---

## 三、开源生态

### 3.1 🌟 HuggingFace 趋势模型 Top 10（今日）

| 排名 | 模型 | 类型 | 参数量 | 下载量 | 亮点 |
|------|------|------|--------|--------|------|
| 1 | **zai-org/GLM-5.2** | 文本生成 | 753B | 57.2k | 开源全能王，100万上下文 |
| 2 | **baidu/Unlimited-OCR** | 图文理解 | 3B | 45.7k | 无限制 OCR，百度出品 |
| 3 | **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5** | 文本生成 | 12B | 483k | Gemma 4 + Fable 5 蒸馏 |
| 4 | **WeiboAI/VibeThinker-3B** | 文本生成 | 3B | 49.6k | 微博出品，轻量推理 |
| 5 | **empero-ai/Qwythos-9B-Claude-Mythos-5** | 文本生成 | 9B | 63.6k | Mythos 5 蒸馏版 |
| 6 | **krea/Krea-2-Turbo** | 文生图 | — | 878 | 最新图像生成 |
| 7 | **nvidia/LocateAnything-3B** | 图文理解 | 4B | 359k | NVIDIA 空间理解 |
| 8 | **microsoft/FastContext-1.0-4B-SFT** | 文本生成 | 4B | 4.8k | 微软长上下文模型 |
| 9 | **MiniMaxAI/MiniMax-M3** | 图文理解 | 427B | 143k | MiniMax 多模态 |
| 10 | **Qwen/Qwen-AgentWorld-35B-A3B** | 文本生成 | 35B | 223 | 阿里 Agent 世界模型 |

---

### 3.2 🔥 GitHub Trending（今日精选）

> 注：由于 GitHub Trending 页面内容动态加载，以下基于近期数据和社区热度整理。

**1. OpenCode（anomalyco/opencode）** — ⭐ 172,198 stars
- 最热门的开源编码 Agent
- 支持 75+ LLM 提供商，可接入 Ollama 本地模型
- 安装：`curl -fsSL https://opencode.ai/install | bash`

**2. Gemini CLI** — ⭐ 105,104 stars
- Google 出品，Apache-2.0 许可证
- 免费 1000次/天（个人 Google 账号）
- 安装：`npx @google/gemini-cli`

**3. OpenAI Codex CLI** — ⭐ 89,991 stars
- Rust 编写的终端 Agent
- 支持 IDE 扩展（VS Code、Cursor、Windsurf）
- 安装：`curl -fsSL https://chatgpt.com/codex/install.sh | sh`

**4. Cline** — ⭐ 62,996 stars
- 支持 VS Code + JetBrains + CLI
- 可接入任意模型（BYOK 或本地）
- 安装：`npm i -g cline`

**5. Goose（Linux Foundation AAIF）** — ⭐ 48,542 stars
- Rust 构建，通用 Agent（不仅限编码）
- 15+ 提供商，70+ MCP 扩展
- 已迁移到 Linux Foundation 的 Agentic AI Foundation

---

### 3.3 🆕 值得关注的新开源项目

**baidu/Unlimited-OCR（3B 参数）**
- 百度发布的无限制 OCR 模型
- 专门针对图文理解场景优化
- 适合文档数字化、票据识别等场景
- 🔗 https://huggingface.co/baidu/Unlimited-OCR

**microsoft/FastContext-1.0-4B-SFT**
- 微软发布的长上下文处理模型
- 4B 参数，轻量高效
- 专注于解决长文本处理效率问题

**Qwen/Qwen-AgentWorld-35B-A3B**
- 阿里通义千问团队发布的"Agent 世界模型"
- 35B 总参数 / 3B 激活参数（MoE 架构）
- 专为 Agent 任务设计的模型

**owensong/Inflect-Nano-v1**
- 轻量级 TTS（文本转语音）模型
- 适合边缘设备和低资源环境
- 🔗 https://huggingface.co/owensong/Inflect-Nano-v1

---

### 3.4 📊 开源编码 Agent 完整对比

| Agent | Stars | 许可证 | 特点 | 适用场景 |
|-------|-------|--------|------|---------|
| OpenCode | 172,198 | MIT | 75+ 提供商，最灵活 | 多模型切换 |
| Gemini CLI | 105,104 | Apache-2.0 | 免费1000次/天 | 零成本入门 |
| Codex CLI | 89,991 | Apache-2.0 | 云沙箱执行 | 安全隔离任务 |
| Cline | 62,996 | Apache-2.0 | VS Code + JetBrains | IDE 内嵌 |
| Goose | 48,542 | Apache-2.0 | 通用 Agent | 非纯编码任务 |
| Aider | 45,945 | Apache-2.0 | Git 原生集成 | Git 工作流 |
| Kilo Code | 19,968 | MIT | 零加价网关 | 成本敏感 |

---

## 四、AI 工具与技巧

### 4.1 🛠️ 本月最值得关注的 AI 工具更新

**1. GitHub Copilot 计费系统重构（6月1日起）**
- 改为基于 token 的 AI Credits 计费：1 credit = $0.01
- 基础代码补全仍然免费（不消耗 credits）
- Agent 会话现在按量计费
- 支持多模型选择：Claude Opus 4.5-4.8、GPT-5.5、Gemini 3.1 Pro 等

**操作建议：** 检查你的 Copilot 使用模式。如果你主要做 Agent 模式开发，新计费可能更贵；如果主要是代码补全，影响不大。

---

**2. OpenAI ChatGPT Memory "Dreaming" 更新（6月4日）**
- 全新的记忆架构，保持记忆更新鲜
- 减少过时或矛盾的记忆上下文
- 在长期项目中提供更一致的上下文理解

**💡 技巧：** 在 ChatGPT 设置中检查你的记忆偏好。"Dreaming" 机制会自动整合跨会话的上下文，但你可以通过设置控制哪些信息被记住。

---

**3. Holo3.1：本地可运行的 Computer Use Agent**
- Hcompany 发布
- 本地优先设计：消费级硬件即可运行
- 支持鼠标/键盘自动化、GUI 交互
- 完全本地处理，保护隐私
- 开放权重

**💡 技巧：** 适合对隐私敏感的场景。安装后可以通过命令行启动，适合实验性桌面自动化任务。

---

### 4.2 🎓 AI 初学者友好建议

**本周学习路线推荐：**

**Day 1-2：安装并试用 Gemini CLI**
```bash
npx @google/gemini-cli
# 免费 1000次/天，零成本体验 Agent 编码
```

**Day 3-4：理解 MCP（Model Context Protocol）**
- MCP 已有 200+ 服务器实现
- 查看官方文档：https://modelcontextprotocol.io
- 尝试添加一个 MCP 服务器到你的 Agent

**Day 5-7：阅读 Sakana Fugu 技术报告**
- 理解"编排即扩展"的设计理念
- 论文链接：https://arxiv.org/abs/2606.21228
- 思考如何在你自己的项目中应用多模型路由策略

---

### 4.3 🔧 实用工具推荐

**EVA-Bench Data 2.0（ServiceNow-AI 发布）**
- Agent 能力评估新基准
- 覆盖 3 个领域、121 个工具、213 个场景
- 评估维度：工具使用、多步推理、错误恢复、资源效率
- 适合评估你的 Agent 系统质量

**FlureeDB：可验证知识图谱数据库**
- 专为 Agent AI 设计的数据层
- W3C 标准 RDF 知识图谱
- 不可变提交历史
- 🔗 https://www.fluree.com

**CData Connect AI Developer Edition**
- 免费版本 + 开源 Python SDK + CLI
- 连接 Salesforce、Snowflake、NetSuite、Microsoft 365 等企业系统
- 让 Agent 安全访问企业数据

---

## 五、值得深读的研究

### 5.1 📄 Sakana Fugu 技术报告

**论文：** Sakana Fugu Technical Report  
**链接：** https://arxiv.org/abs/2606.21228  
**发布日期：** 2026年6月19日

**研究方法：**
- 基于两篇 ICLR 2026 论文：**TRINITY**（进化优化的 LLM 协调器）和 **Conductor**（RL 发现的自然语言协调策略）
- 训练一个"编排模型"来学习如何组合多个前沿模型的能力
- 两种模式：Fugu（单 agent 路由，低延迟）和 Fugu Ultra（多 agent 工作流，高质量）

**核心发现：**
- SWE-Bench Pro 达到 73.7，超过 Claude Opus 4.8（69.2）
- Terminal-Bench 2.1 超过 Anthropic 最新模型
- 但在 HLE（人类最后的考试）上落后
- 证明了"通过编排现有模型来扩展能力"的可行性

**启发：**
- AI 能力的提升不一定需要训练更大的模型，更好的组合策略同样有效
- 这对资源受限的团队尤为重要：你可以通过智能路由获得接近前沿的性能
- 编排本身成为一种新的"扩展轴"，可能改变 AI 的经济和地缘政治格局

---

### 5.2 📄 DeepSeek V4 技术报告

**论文：** DeepSeek-V4 Technical Report  
**链接：** https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro/blob/main/DeepSeek_V4.pdf  
**发布日期：** 2026年4月24日

**研究方法：**
- 两个 MoE 模型：V4-Pro（1.6T/49B 激活）和 V4-Flash（284B/13B 激活）
- **Token-wise 压缩 + DSA（DeepSeek 稀疏注意力）**
- KV cache 使用量仅为 V3.2 的 10%
- 1M 上下文窗口为默认配置

**核心发现：**
- V4-Pro 在 Agentic 编码基准上达到开源 SOTA
- V4-Flash 在简单 Agent 任务上接近 V4-Pro 水平
- 与 Claude Code、OpenClaw、OpenCode 等主流 Agent 工具无缝集成
- 训练成本（仅计算运行，不含研发）极低

**启发：**
- MoE 架构的效率提升仍在加速
- 100万 token 上下文正在成为标准配置
- 开源模型在 Agent 场景的差距正在快速缩小

---

### 5.3 📄 NVIDIA Nemotron 3.5 Content Safety

**发布时间：** 2026年6月4日

**研究重点：**
- 可定制的多模态安全模型
- 支持文本、图像、音频的统一安全检查
- 为不同地区和法规（GDPR、CCPA 等）提供灵活配置
- 低延迟推理，适合实时应用

**核心发现：**
- 企业级 AI 安全需要可定制的策略，而非一刀切
- 多模态安全需要统一框架
- 合规性不能事后添加，需要内置支持

**启发：**
- 如果你在部署面向用户的 AI 系统，安全模型是必需的
- 考虑将 Nemotron 3.5 作为你的输出过滤层
- 不同市场可能需要不同的安全策略配置

---

### 5.4 📄 Beyond LLMs: Agent Logic for Enterprise AI（IBM Research）

**发布时间：** 2026年6月1日

**核心论点：**
- 可扩展的企业 AI 采用**取决于 Agent 逻辑，而非原始 LLM 能力**
- 从实验到生产，以下能力比基准分数更重要：
  - 链接多个推理步骤
  - 与外部系统和数据源交互
  - 在长期交互中维护状态和上下文
  - 优雅地处理错误和边缘情况

**启发：**
- 选择 AI 解决方案时，不要只看模型基准分数
- Agent 的"胶水逻辑"（状态管理、错误处理、工具调用）决定了实际价值
- 企业 AI 项目的失败往往不是因为模型不够好，而是因为 Agent 架构不够健壮

---

## 六、今日学习建议

### 🎯 具体可执行的行动清单

**1. 【15分钟】安装并试用 Gemini CLI**
```bash
# 最快的入门方式
npx @google/gemini-cli
# 使用 Google 账号登录，免费 1000次/天
```
- 尝试让它帮你完成一个小项目
- 感受 Agent 编码的工作模式

**2. 【30分钟】阅读 Sakana Fugu 发布博客**
- 🔗 https://sakana.ai/fugu-release/
- 重点理解"编排模型"的概念
- 思考：你的项目中是否有多模型组合的机会？

**3. 【1小时】了解 MCP 生态**
- 访问 https://modelcontextprotocol.io
- 查看 200+ 可用服务器列表
- 选择 1-2 个与你工作相关的服务器尝试集成
- 例如：Slack MCP、GitHub MCP、Postgres MCP

**4. 【30分钟】阅读 Pydantic AI v2 发布文章**
- 🔗 https://pydantic.dev/articles/pydantic-ai-v2
- 理解"类型安全 Agent"的设计理念
- 如果你在用 Python，考虑将 Pydantic AI 纳入你的工具栈

**5. 【15分钟】检查你的 AI 工具计费状态**
- GitHub Copilot 已改为 AI Credits 计费
- Claude Agent SDK 现在有单独的月度额度
- 查看你的使用量，避免意外超支

**6. 【持续】关注中国开源模型生态**
- GLM-5.2（智谱）：当前最强开源全能模型
- DeepSeek V4（深度求索）：极致效率
- Qwen（通义千问）：阿里生态
- 这些模型都支持中文，且社区活跃

---

### 📚 延伸阅读

- **AI Agent 框架完整对比（2026）：** https://www.morphllm.com/ai-agent-framework
- **AI 编码 Agent 排行榜：** https://www.morphllm.com/best-ai-coding-agents-2026
- **开源模型排名与对比：** https://felloai.com/best-open-source-ai-models
- **DeepSeek 论文阅读指南：** https://deepseekai.guide/news/deepseek-research-papers/
- **Agentic AI 新闻追踪：** https://agentic.ai/news

---

## 📌 今日要点总结

1. **Sakana Fugu 开辟了"编排即扩展"的新路线**——通过智能组合现有模型来获得前沿能力
2. **GLM-5.2 是开源领域的新王者**——744B 参数，MIT 许可，100万上下文，agentic 能力领先
3. **Agent 框架进入"协议统一"时代**——MCP 200+ 服务器，ACP 合并入 A2A
4. **AI 编程 Agent 竞争激烈**——Codex CLI、Claude Code、Gemini CLI 各有优势
5. **中国开源模型生态值得关注**——GLM、DeepSeek、Qwen 都在快速进步
6. **企业 AI 从"构建"转向"治理"**——F5 AI 安全平台、FlureeDB 等工具涌现

---

*本报告基于 HuggingFace、arXiv、GitHub、BenchLM、MorphLLM、Agentic.ai、Sakana AI、DeepSeek API、Pydantic 等 12+ 来源整理。数据截至 2026年6月25日 08:00（北京时间）。*

*如有错误或遗漏，欢迎反馈。下期再见！* 👋
