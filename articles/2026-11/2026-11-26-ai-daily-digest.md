# AI 每日情报 - 2026年11月26日

> 📊 数据来源：arXiv (cs.AI/cs.LG/cs.CL)、GitHub Trending、HuggingFace Papers/Models、AIFOD、LLM Stats、PaperDigest 等 12+ 来源
> 
> 🎯 目标读者：AI 工程师、Agent 开发者、技术决策者

---

## 目录

1. [前沿模型动态](#1-前沿模型动态)
2. [Agent 架构与范式](#2-agent-架构与范式)
3. [开源生态](#3-开源生态)
4. [AI 工具与技巧](#4-ai-工具与技巧)
5. [值得深读的研究](#5-值得深读的研究)
6. [今日学习建议](#6-今日学习建议)

---

## 1. 前沿模型动态

### 1.1 ShellBench 揭示：模型选择比 Harness 更重要，但差距正在缩小

**核心发现**

ShellBench 是今日发布的一项大规模基准测试，基于 1000 万+ 用户请求构建了 100 个日常任务，评估了 12 个模型 × 5 个 Agent Harness × 3 个推理级别，共 53,100 次试验。

**关键数据**

| 模型 | Pass@1 | Token 成本（相对） | 备注 |
|------|--------|-------------------|------|
| GPT-6 Astra | 62.5% | 1.0x | 当前最强 |
| GPT-6.1 Sol | 61.4% | ~0.17x | 性价比之王 |
| Claude Opus 5.5 | ~61% | 0.8x | 紧随其后 |

**Harness 对比**

| Harness | Pass@1 | 安全性评分 |
|---------|--------|-----------|
| OpenClaw | 45.2% | 良好 |
| Claude Code | 42.9% | 良好 |
| 其他 | 43-45% | 差异不显著 |

**💡 对你的价值**

- **成本优化**：GPT-6.1 Sol 以 1/6 的成本达到接近的性能，适合高频日常任务
- **Harness 选择**：差异仅 2-3 个百分点，说明你的 prompt 工程和工作流设计比工具选择更重要
- **行动建议**：如果你在用 GPT-6 Astra，考虑将非关键任务切换到 GPT-6.1 Sol，月成本可降 80%+

**论文链接**：[arXiv:2611.32946](https://arxiv.org/abs/2611.32946)

---

### 1.2 Qwen 占据开源下载量 54%，DeepSeek 主导 API Token

**Helmcode 报告核心数据**

| 维度 | 领先者 | 份额 |
|------|--------|------|
| HuggingFace 下载量 | Qwen | 54.2% |
| OpenRouter API Token | DeepSeek | 31.3% |
| Agentic 任务性价比 | Kimi K3.1 Pro | $7.18 vs Claude Opus 5.5 $18.48 |

**趋势解读**

1. **Qwen 的统治地位**：超过一半的开源模型下载来自 Qwen 系列，说明阿里在大模型开源生态的影响力持续扩大
2. **DeepSeek 的 API 优势**：虽然下载量不如 Qwen，但实际生产环境的 API 调用量领先
3. **Kimi 的性价比突破**：在 agentic 任务上与闭源模型差距缩小到 1.5 个百分点

**💡 对你的价值**

- **选型参考**：如果你在做开源部署，Qwen 是社区验证最多的选择
- **成本对比**：Kimi K3.1 Pro 在 agentic 任务上比 Claude Opus 5.5 便宜 61%，值得测试
- **行动建议**：评估你的 Agent 工作流，考虑用 Kimi K3.1 Pro 做 A/B 测试

**来源**：[AIFOD](https://af.net/realtime/helmcode-report-finds-qwen-captures-54-of-open-ai-downloads-while-deepseek-leads-api-tokens/)

---

### 1.3 HuggingFace 热门模型速览

**今日 Trending 模型**

| 模型 | 类型 | 参数量 | 下载量 | 亮点 |
|------|------|--------|--------|------|
| Inkling-2-Mini | Image-Text-to-Text | 26B | 96.5k | 多模态新秀 |
| Qwen3.8-27B | Image-Text-to-Text | 28B | 6.05M | 持续霸榜 |
| Ling-3.2-air | Text | 128B | 1.47k | 轻量级大模型 |
| Hy4-flash | Image-Text-to-Text | 220B | 10.5k | 腾讯新作 |
| ERNIE-5.5-Flash-Preview | Text | 300B | 1.19k | 百度旗舰 |
| Nemotron-Labs-Image-30B-A3B | Text-to-Image | 33B | 218 | NVIDIA 图像生成 |

**💡 对你的价值**

- **多模态趋势**：Inkling-2-Mini 和 Qwen3.8-27B 的火爆说明 20-30B 参数的多模态模型是实用甜点
- **本地部署**：26-28B 模型可在单张 A100/H100 上运行，适合边缘场景
- **行动建议**：如果你还没试过 Qwen3.8-27B，现在是时候了——社区验证充分，工具链成熟

**来源**：[HuggingFace Models](https://huggingface.co/models?sort=trending)

---

### 1.4 DeepMind 发布 Humanity's First Exam：前沿模型可靠性仅 85.6%

**基准设计**

- 544 个 prompt，测试模型在轻微变化下的一致性
- 严格评分规则：pass^4（4 个变体全部通过才算通过）
- 图像解释失败占错误响应的 74%

**模型表现**

| 模型 | 单次得分 | pass^4 得分 | 下降幅度 |
|------|---------|------------|---------|
| 平均前沿模型 | 96-98% | 85.6% | -10-12% |
| GPT-6.2 Astra | - | 90.7% | 领先 |

**💡 对你的价值**

- **可靠性警示**：即使是最好的模型，在细微变化下也会失败 1/10 次
- **图像理解是短板**：74% 的错误来自图像，多模态应用需要额外验证
- **行动建议**：在生产环境部署前，用类似方法测试你的 prompt 对输入变化的鲁棒性

**来源**：[AIFOD](https://af.net/realtime/deepmind-humanitys-first-exam-cuts-frontier-ai-reliability-to-85-6/)

---

## 2. Agent 架构与范式

### 2.1 RLVB：用可验证信念训练 Agent 克服"懒惰"

**问题定义**

AI Agent 在处理长任务时经常"懒惰"——在证据不足时就提交答案。传统结果奖励无法教会 Agent 何时该继续探索、何时该提交。

**RLVB 解决方案**

```
核心思想：在训练时利用模拟器计算精确后验，奖励 Agent：
- 当后验仍允许多个答案时，继续探索 → 正奖励
- 当证据充分时提交 → 正奖励
- 不需要 judge、critic 或 reward model
```

**实验结果**

| 设置 | 基础模型 | GRPO/PPO | RLVB | 提升 |
|------|---------|----------|------|------|
| 平均提升 | baseline | 低于 baseline | +17.1% | 显著 |
| 充分证据提交率 | 8%/0.4%/36% | - | 51%/12%/74% | 大幅提升 |
| 证据不足时错误提交 | 3-68% | - | 0.1-2.2% | 显著降低 |

**技术亮点**

- 无需 LLM Judge，节省 1.6x GPU 时间
- 比带过程奖励的 PPO 高 9.3%
- 在 3 个 benchmark 上全面领先

**💡 对你的价值**

- **Agent 训练新范式**：如果你在做 Agent 微调，RLVB 提供了无需额外奖励模型的方案
- **可靠性提升**：减少 Agent "拍脑袋"决策，提高答案可信度
- **行动建议**：阅读论文，考虑在你的 Agent 训练流程中引入类似的可验证信念机制

**论文链接**：[arXiv:2611.32884](https://arxiv.org/abs/2611.32884)

---

### 2.2 NightWatch：给 Computer-Use Agent 装上"实时感知"

**核心问题**

当前 CUA（Computer-Use Agent）通过离散快照感知环境，VLM 推理延迟导致"感知-行动差距"——观察到的状态在执行时已经过时。

**NightWatch 架构**

```
┌─────────────────────────────────────────────────────────┐
│                    CUA (VLM Agent)                       │
│   模型/prompt/动作空间完全不变                             │
└─────────────────────────────────────────────────────────┘
                            ↕ 同步状态
┌─────────────────────────────────────────────────────────┐
│              NightWatch-0.8B (System-1)                  │
│   • 流式监控界面状态                                      │
│   • 低延迟、低计算成本                                    │
│   • 保持 Agent 与环境同步                                 │
└─────────────────────────────────────────────────────────┘
```

**实验效果**

| 环境 | 指标 | 基线 | NightWatch | 改进 |
|------|------|------|------------|------|
| OSWorld | 非推理时间 | 100% | 67% | -33% |
| OSWorld | 浪费时间 | 100% | 47% | -53% |
| DynaCU-Bench | 成功率 | 39.5% | 44.2% | +4.7% |

**关键洞察**

> "感知的时机与内容同样重要" —— 从"轮次感知"到"持续感知"是 Agent 架构的重要演进

**💡 对你的价值**

- **即插即用**：不改变现有 Agent 架构，只需添加一个轻量级 watcher
- **动态环境必备**：如果你的 Agent 在变化的 UI 上工作（网页、桌面），这个方法值得尝试
- **行动建议**：评估你的 CUA 在动态环境中的失败案例，看有多少是因为"状态过时"导致

**论文链接**：[arXiv:2611.28947](https://arxiv.org/abs/2611.28947)

---

### 2.3 Bathys：深度搜索 Agent 的训练框架

**深度搜索能力拆解**

```
深度搜索 ≠ 单次检索
= 迭代信息收集 + 查询重构 + 证据验证
```

**Bathys 训练流水线**

```
1. 可验证问题合成
   └─ 每条线索重构为间接引用，需独立检索
   
2. SFT (监督微调)
   └─ 长程工具使用 + 查询重构基础
   
3. KTO (Kahneman-Tversky Optimization)
   └─ 基于轨迹的二元反馈，提升证据 grounding
   
4. CM-GSPO (Compaction-Managed Group Sequence Policy Optimization)
   └─ 在上下文压缩下进行在线 RL
   └─ 长度归一化似然比
   └─ 子轨迹优势重加权
```

**性能表现**

| 模型 | BrowseComp 得分 |
|------|----------------|
| Bathys 9B | 66.51% |
| Bathys 27B | 80.49% |

**💡 对你的价值**

- **搜索 Agent 新标准**：如果你在做 research agent 或 deep search 功能，Bathys 的训练框架是参考实现
- **开源可用**：模型和数据都在 HuggingFace 上
- **行动建议**：试用 Bathys 27B 处理复杂研究任务，对比你现有的搜索方案

**论文链接**：[arXiv:2611.32660](https://arxiv.org/abs/2611.32660) | **模型**：[HuggingFace/Bathys](https://huggingface.co/Bathys)

---

### 2.4 LoomFormer：让 Transformer 在每个 token 上动态重连电路

**核心创新：Loom Attention**

```
传统 Transformer:
  Head → Q/K/V → 水平注意力(over tokens) → 输出

LoomFormer:
  Head → 垂直注意力(over earlier heads' outputs) 
       + 水平注意力(over tokens)
       = 动态电路重连
```

**技术实现**

- 垂直注意力：归一化+门控线性注意力，作用于 per-token 矩阵记忆
- 双流架构：向量流（控制）+ 矩阵流（内容）
- 仅增加 2% FLOPs

**性能对比**

| 模型 | 训练 Token | 下游任务提升 | 等效计算量 |
|------|-----------|-------------|-----------|
| Pythia-2.8B | 300B | baseline | 1x |
| mHC-Pythia-2.8B | 300B | +X% | ~1.7-2.8x |
| LoomPythia-2.8B | 300B | +1.6X% | 1.02x |
| Pythia-12B | 300B | - | 1x |

**LoomPythia-2.8B 在 0-shot 匹配 Pythia-12B，5-shot 超越**

**💡 对你的价值**

- **架构创新**：如果你在做模型架构研究，Loom Attention 提供了新的设计空间
- **效率提升**：2% FLOPs 增加获得 3x 计算等效性能
- **行动建议**：关注这个方向，代码已开源 [github.com/Caiyun-AI/LoomFormer](https://github.com/Caiyun-AI/LoomFormer)

**论文链接**：[arXiv:2611.30634](https://arxiv.org/abs/2611.30634)

---

## 3. 开源生态

### 3.1 Qwen3.8-27B：持续霸榜的多模态工作马

**模型概况**

| 属性 | 值 |
|------|-----|
| 参数量 | 28B |
| 类型 | Image-Text-to-Text |
| 下载量 | 6.05M |
| 点赞 | 21.8k |
| 更新 | 19 天前 |

**为什么持续火热**

1. **尺寸适中**：27-28B 可在单张 A100/H100 上运行
2. **多模态能力**：图文理解一体化
3. **社区生态**：大量 GGUF 量化版本（unsloth、nari-labs 等）
4. **衍生作品**：各种 uncensored、adapted 版本活跃

**可用变体**

- `unsloth/Inkling-2-Mini-GGUF` - 2.45M 下载
- `AtomicChat/Inkling-2-Mini-Uncensored-GGUF` - 762k 下载
- `harness-hub/Qwen3.8-27B-pi-adapted` - 3.84k 下载

**💡 对你的价值**

- **本地部署首选**：如果你有 GPU 资源，这是最成熟的 20-30B 级选择
- **行动建议**：用 Ollama 或 llama.cpp 快速体验

**来源**：[HuggingFace](https://huggingface.co/Qwen/Qwen3.8-27B)

---

### 3.2 Inkling-2-Mini：多模态新秀崛起

**模型概况**

| 属性 | 值 |
|------|-----|
| 参数量 | 26B |
| 类型 | Image-Text-to-Text |
| 下载量 | 96.5k (1天) |
| 点赞 | 6.03k |
| 更新 | 1 天前 |

**快速走红原因**

1. **性能强劲**：在多个 benchmark 上超越同级别模型
2. **社区支持**：多个 GGUF 版本同日上线
3. **时机好**：填补了 Qwen3.8 之外的选择空白

**💡 对你的价值**

- **新选择**：如果你在用 Qwen，可以对比测试 Inkling-2-Mini
- **行动建议**：在你的任务上跑个对比测试

**来源**：[HuggingFace](https://huggingface.co/thinkingmachines/Inkling-2-Mini)

---

### 3.3 腾讯 Hy4-flash：220B 参数的开源重磅

**模型概况**

| 属性 | 值 |
|------|-----|
| 参数量 | 220B |
| 类型 | Image-Text-to-Text |
| 下载量 | 10.5k |
| 点赞 | 712 |
| 更新 | 3 天前 |

**技术亮点**

- 220B 参数开源，是目前最大的开源多模态模型之一
- Flash 变体暗示优化了推理速度

**💡 对你的价值**

- **大模型本地化**：如果你有多卡资源，可以体验 200B+ 级别的开源模型
- **行动建议**：需要至少 4x A100/H100，评估你的硬件配置

**来源**：[HuggingFace](https://huggingface.co/tencent/Hy4-flash)

---

### 3.4 百度 ERNIE-5.5-Flash-Preview：300B 旗舰预览

**模型概况**

| 属性 | 值 |
|------|-----|
| 参数量 | 300B |
| 类型 | Text Generation |
| 下载量 | 1.19k |
| 点赞 | 304 |
| 更新 | 1 天前 |

**💡 对你的价值**

- **关注动态**：百度大模型开源进程加速
- **行动建议**：目前是 Preview，等稳定版再评估

**来源**：[HuggingFace](https://huggingface.co/baidu/ERNIE-5.5-Flash-Preview)

---

### 3.5 NVIDIA Nemotron-Labs-Image-30B-A3B：图像生成新选择

**模型概况**

| 属性 | 值 |
|------|-----|
| 参数量 | 33B |
| 类型 | Text-to-Image |
| 下载量 | 218 |
| 点赞 | 156 |
| 更新 | 5 小时前 |

**💡 对你的价值**

- **新工具**：NVIDIA 官方图像生成模型
- **行动建议**：刚发布，关注社区评测

**来源**：[HuggingFace](https://huggingface.co/nvidia/Nemotron-Labs-Image-30B-A3B)

---

### 3.6 LoomFormer：架构创新开源

**项目概况**

| 属性 | 值 |
|------|-----|
| 类型 | Transformer 架构变体 |
| 核心 | Loom Attention |
| 代码 | github.com/Caiyun-AI/LoomFormer |
| FLOPs 增加 | 仅 2% |

**💡 对你的价值**

- **架构研究**：如果你在做模型架构创新，这是重要的参考
- **行动建议**：clone 代码，在你的任务上测试

**来源**：[arXiv:2611.30634](https://arxiv.org/abs/2611.30634)

---

### 3.7 Bathys：深度搜索 Agent 开源

**项目概况**

| 属性 | 值 |
|------|-----|
| 模型 | Bathys 9B / 27B |
| 任务 | 深度搜索 |
| BrowseComp | 66.51% / 80.49% |
| 开源 | 模型 + 数据 |

**💡 对你的价值**

- **搜索 Agent**：如果你在做 research agent，这是现成的解决方案
- **行动建议**：从 HuggingFace 下载，集成到你的工作流

**来源**：[HuggingFace/Bathys](https://huggingface.co/Bathys)

---

### 3.8 LoomKV：LLM Serving 的 KV Cache 压缩方案

**技术概况**

| 属性 | 值 |
|------|-----|
| 功能 | 无损 KV Cache 压缩 |
| 压缩率 | BF16: 0.71x, FP8: 0.85-0.87x |
| 集成 | LMCache + vLLM |
| 效果 | 1.4x 有效容量 |

**核心创新**

- Tier 模式：外部存储层压缩，不改变引擎
- Pool 模式：GPU 内存压缩，fused decode-attention kernel
- Bit-exact：tier 模式与原方案位精确一致

**💡 对你的价值**

- **Serving 优化**：如果你在部署 LLM 服务，这可以显著提升并发能力
- **行动建议**：评估你的 serving 栈是否兼容 vLLM + LMCache

**论文链接**：[arXiv:2611.32954](https://arxiv.org/abs/2611.32954)

---

## 4. AI 工具与技巧

### 4.1 MCP (Model Context Protocol) 架构指南

**核心概念**

MCP 是 Anthropic 推出的标准化协议，用于连接 LLM 与外部工具/资源。

**架构组件**

```
┌─────────────────────────────────────────────────────────┐
│                    MCP Host (Claude)                     │
└─────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────┐
│                   MCP Server                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐       │
│  │   Tools     │ │  Resources  │ │   Prompts   │       │
│  └─────────────┘ └─────────────┘ └─────────────┘       │
└─────────────────────────────────────────────────────────┘
```

**关键能力**

| 组件 | 功能 | 示例 |
|------|------|------|
| Tools | 可执行操作 | 数据库查询、API 调用 |
| Resources | 只读数据源 | 文件内容、数据库记录 |
| Prompts | 预定义模板 | 代码审查、文档生成 |

**💡 对你的价值**

- **工具集成标准化**：如果你在构建 AI 应用，MCP 提供了标准接口
- **行动建议**：阅读 [Essa Mamdani 的 MCP 指南](https://www.essamamdani.com/blog/model-context-protocol-claude-architecture-guide)

---

### 4.2 OpenCode 插件开发指南

**核心概念**

OpenCode 支持通过插件扩展功能，包括自定义工具和 hooks。

**插件类型**

| 类型 | 用途 | 触发时机 |
|------|------|---------|
| Tools | 扩展能力 | Agent 主动调用 |
| Hooks | 拦截/增强 | 特定事件发生时 |

**快速开始**

```javascript
// 示例：自定义工具插件
export default {
  name: 'my-tool',
  tools: [{
    name: 'search_docs',
    description: '搜索文档',
    parameters: { query: 'string' },
    execute: async ({ query }) => {
      // 实现搜索逻辑
    }
  }]
};
```

**💡 对你的价值**

- **扩展 AI 编码工具**：如果你在用 OpenCode，可以定制化工具链
- **行动建议**：阅读 [完整指南](https://www.essamamdani.com/blog/writing-opencode-plugins-custom-extensions-tools-guide)

---

### 4.3 OpenCode Agents 配置指南

**核心概念**

OpenCode 支持主 Agent 和委托 Subagent 的配置。

**配置层级**

```
Primary Agent
├── 权限范围 (Permission Scoping)
├── 工具边界 (Tool Boundaries)
└── Delegated Subagents
    ├── 专用工具集
    └── 受限权限
```

**💡 对你的价值**

- **多 Agent 编排**：如果你在做复杂项目，可以用 subagent 分解任务
- **行动建议**：阅读 [官方文档](https://www.essamamdani.com/blog/opencode-agents-architecture-subagent-delegation-rules)

---

### 4.4 Gemini 4 Neon 架构解析

**核心特性**

| 特性 | 值 |
|------|-----|
| 上下文窗口 | 1M tokens (统一) |
| 发布时间 | 2026年11月18日 |
| 定位 | 生产级 pipelines |

**💡 对你的价值**

- **长上下文应用**：1M token 窗口适合大型代码库分析
- **行动建议**：阅读 [架构指南](https://www.essamamdani.com/blog/introducing-gemini-4-neon-guide)

---

### 4.5 vLLM 安全漏洞修复指南

**漏洞详情**

- **编号**：GHSA-xgh8-qwjh-q853
- **问题**：`/v1/systemone` 端点绕过 chat template 验证
- **影响**：LLM serving 端点安全

**修复建议**

1. 立即更新 vLLM 到最新版本
2. 审计你的 serving 端点配置
3. 添加额外的输入验证层

**💡 对你的价值**

- **安全警示**：如果你在运行 vLLM，这是一个需要立即修复的漏洞
- **行动建议**：阅读 [完整分析和修复指南](https://www.essamamdani.com/blog/fixing-vllm-ghsa-xgh8-qwjh-q853-securing-chat-templates)

---

## 5. 值得深读的研究

### 5.1 RLVB：用可验证信念训练 Agent

**论文**：[arXiv:2611.32884](https://arxiv.org/abs/2611.32884)

**研究方法**

1. **问题识别**：Agent 在长任务中过早提交答案（"懒惰"行为）
2. **核心洞察**：训练时模拟器可计算精确后验，判断证据是否充分
3. **奖励设计**：
   - 证据不足时继续探索 → 正奖励
   - 证据充分时提交 → 正奖励
   - 无需额外 judge/critic/reward model

**核心发现**

| 指标 | 基础模型 | RLVB | 提升 |
|------|---------|------|------|
| 平均准确率提升 | baseline | +17.1% | 显著 |
| 充分证据提交率 | 8-36% | 51-74% | 大幅提升 |
| 错误提交率 | 3-68% | 0.1-2.2% | 显著降低 |
| GPU 时间 | 1x | 0.625x | 节省 37.5% |

**启发**

- **训练信号设计**：不需要复杂的奖励模型，利用环境本身的可验证性
- **Agent 可靠性**：从"猜测"到"基于证据决策"的范式转变
- **应用前景**：任何需要多步推理的 Agent 任务

**💡 对你的价值**

如果你在训练 Agent，考虑引入类似的可验证信念机制，可以显著提升可靠性并降低训练成本。

---

### 5.2 NightWatch：Computer-Use Agent 的实时感知

**论文**：[arXiv:2611.28947](https://arxiv.org/abs/2611.28947)

**研究方法**

1. **问题定义**：VLM 推理延迟导致感知-行动差距
2. **解决方案**：添加轻量级 System-1 watcher (0.8B)
3. **设计原则**：不改变主 Agent 的模型/prompt/动作空间

**核心发现**

| 环境 | 指标 | 改进 |
|------|------|------|
| OSWorld | 非推理时间 | -33% |
| OSWorld | 浪费时间 | -53% |
| DynaCU-Bench | 成功率 | +4.7% |

**启发**

- **感知时机**：与内容同样重要
- **架构演进**：从"轮次感知"到"持续感知"
- **即插即用**：不改变现有架构即可增强

**💡 对你的价值**

如果你的 CUA 在动态 UI 上工作，考虑添加类似的实时感知层。

---

### 5.3 LoomFormer：动态电路重连的 Transformer

**论文**：[arXiv:2611.30634](https://arxiv.org/abs/2611.30634)

**研究方法**

1. **核心创新**：Loom Attention - 垂直注意力 + 水平注意力
2. **技术实现**：
   - 垂直注意力：归一化+门控线性注意力
   - 矩阵记忆：per-token 的第二残差流
   - 双流架构：控制流 + 内容流

**核心发现**

| 模型 | FLOPs 增加 | 性能等效 |
|------|-----------|---------|
| LoomPythia-2.8B | 2% | Pythia-12B |
| 对比 mHC-Pythia-2.8B | - | 1.6x 提升 |

**启发**

- **架构创新空间**：注意力机制还有很大的改进余地
- **效率提升**：微小 FLOPs 增加换取大幅性能提升

**💡 对你的价值**

关注 Transformer 架构创新，Loom Attention 可能影响未来的模型设计。

---

### 5.4 ShellBench：模型 vs Harness 的大规模对比

**论文**：[arXiv:2611.32946](https://arxiv.org/abs/2611.32946)

**研究方法**

- 100 个日常任务，基于 1000 万+ 用户请求
- 12 模型 × 5 Harness × 3 推理级别
- 53,100 次试验

**核心发现**

1. 模型选择 > Harness 选择（但差距在缩小）
2. 前 3 名模型差距仅 1.1 个百分点
3. GPT-6.1 Sol 是性价比之王（1/6 成本，接近性能）

**启发**

- **成本优化**：非关键任务可以用更便宜的模型
- **Harness 选择**：差异不大，prompt 工程更重要

**💡 对你的价值**

重新评估你的模型选择策略，考虑分层使用不同成本的模型。

---

### 5.5 Bathys：深度搜索 Agent 训练框架

**论文**：[arXiv:2611.32660](https://arxiv.org/abs/2611.32660)

**研究方法**

1. **数据构建**：可验证问题合成，线索重构为间接引用
2. **训练流水线**：SFT → KTO → CM-GSPO
3. **在线 RL**：在上下文压缩下进行

**核心发现**

| 模型 | BrowseComp |
|------|-----------|
| Bathys 9B | 66.51% |
| Bathys 27B | 80.49% |

**启发**

- **深度搜索**：不是单次检索，而是迭代收集+验证
- **训练方法**：多阶段训练 + 在线 RL

**💡 对你的价值**

如果你在做 research agent，Bathys 提供了完整的训练框架和开源模型。

---

## 6. 今日学习建议

### 6.1 入门级：体验开源多模态模型

**目标**：了解 20-30B 级多模态模型的能力边界

**具体步骤**

1. 安装 Ollama（如未安装）
   ```bash
   curl -fsSL https://ollama.com/install.sh | sh
   ```

2. 下载 Qwen3.8-27B
   ```bash
   ollama run qwen3.8:27b
   ```

3. 测试多模态能力
   - 图片理解：上传工作截图，让模型描述内容
   - 图表分析：上传数据图表，让模型提取关键信息
   - 代码审查：上传代码截图，让模型 review

**预期时间**：30-60 分钟

**💡 对你的价值**

建立对开源多模态模型的直觉，为后续应用打基础。

---

### 6.2 进阶级：研究 Agent 训练方法

**目标**：理解 RLVB 的核心思想

**具体步骤**

1. 阅读论文 [arXiv:2611.32884](https://arxiv.org/abs/2611.32884)
2. 重点关注：
   - "懒惰"行为的定义和测量
   - 可验证信念的奖励设计
   - 与 GRPO/PPO 的对比
3. 思考：你的 Agent 任务中，是否有类似的"可验证性"可以利用？

**预期时间**：2-3 小时

**💡 对你的价值**

掌握 Agent 训练的新范式，提升 Agent 可靠性。

---

### 6.3 高级：部署深度搜索 Agent

**目标**：试用 Bathys 进行复杂研究任务

**具体步骤**

1. 从 [HuggingFace](https://huggingface.co/Bathys) 下载模型
2. 准备测试任务（需要多步搜索的问题）
3. 对比 Bathys 与你现有的搜索方案

**示例任务**

- "比较 2026 年主流 LLM 在代码生成任务上的表现，包括 benchmark 分数和实际用户评价"
- "分析最近 3 个月 AI Agent 框架的发展趋势"

**预期时间**：1-2 小时

**💡 对你的价值**

评估深度搜索 Agent 在实际工作中的价值。

---

### 6.4 安全级：检查 vLLM 漏洞

**目标**：确保你的 LLM serving 安全

**具体步骤**

1. 检查 vLLM 版本
   ```bash
   pip show vllm | grep Version
   ```

2. 如版本受影响，立即更新
   ```bash
   pip install --upgrade vllm
   ```

3. 审计 `/v1/systemone` 端点配置

**预期时间**：15 分钟

**💡 对你的价值**

避免安全漏洞被利用。

---

## 附录：今日关键数据

| 指标 | 数值 | 趋势 |
|------|------|------|
| arXiv cs.AI 新论文 | 300+ | 稳定 |
| arXiv cs.LG 新论文 | 233+ | 稳定 |
| arXiv cs.CL 新论文 | 126+ | 稳定 |
| HuggingFace 热门模型 | Qwen3.8-27B | 持续霸榜 |
| 开源下载量份额 | Qwen 54.2% | 领先 |
| API Token 份额 | DeepSeek 31.3% | 领先 |

---

## 明日预告

- NeurIPS 2026 会议论文陆续公开
- 更多 Agent 训练方法论文预计发布
- 关注 Qwen 和 DeepSeek 的下一步动态

---

*本情报由 AI 自动生成，数据来源已在文中标注。如有遗漏或错误，欢迎反馈。*

*生成时间：2026-11-26 08:00 (Asia/Shanghai)*
