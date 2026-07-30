# 🤖 AI 每日情报 · 2026年7月30日（周四）

> **深度版 | 8000+ 字 | 覆盖 15+ 信源 | 6 大板块**
> 
> 今日关键词：**Kimi-K3 2.8T 登顶 HF 趋势** · **Sora 2 发布** · **Desktop-Delta Bench 评测桌面 Agent** · **Relay-OPD 知识蒸馏新范式** · **UniMem Agent 记忆框架** · **speech-to-speech 语音 Agent 管线** · **book-to-skill 一天 1400 星**

---

## 📊 今日数据速览

| 指标 | 数据 |
|------|------|
| arXiv cs.AI 新论文 | 260 篇（7月29日） |
| arXiv cs.CL 新论文 | 83 篇 |
| HuggingFace 趋势榜第一 | Kimi-K3（2.8T，99.2k 下载） |
| GitHub 今日最热 | book-to-skill（1421 星/天） |
| 顶会动态 | ICML 2026 首尔 / ACL 2026 收录 2400+ 篇 |

---

## 一、前沿模型动态

### 1.1 Moonshot Kimi-K3：2.8T 多模态巨无霸登顶 HuggingFace

**概述：** 月之暗面（Moonshot AI）发布的 Kimi-K3 以 2.8 万亿参数规模登顶 HuggingFace 趋势榜，2 天内获得 99.2k 下载和 8.63k 赞。这是一个 Image-Text-to-Text 模型，意味着它原生支持图文多模态理解。

**技术细节：**
- 参数量：2.8T（目前开源最大级别之一）
- 模态：图文输入 → 文本输出
- Unsloth 团队已同步提供 GGUF 量化版本，降低本地部署门槛
- 配套 Kimi-K2.7-Code（1.1T）专注代码场景

**横向对比：**

| 模型 | 参数量 | 模态 | 下载量 | 特点 |
|------|--------|------|--------|------|
| Kimi-K3 | 2.8T | 图文 | 99.2k | 最大开源多模态 |
| GLM-5.2 | 753B | 文本 | 1.27M | 智谱最新旗舰 |
| Laguna-S-2.1 | 118B | 文本 | 67.3k | Poolside 新锐 |
| Solar-Open2-250B | 250B | 文本 | 4.8k | Upstage 开源 |
| Inkling | 952B | 图文 | 39.1k | Thinking Machines |

**💡 对你的价值：** 如果你需要部署一个强大的多模态模型做图文理解，Kimi-K3 是当前开源最强选择。但注意 2.8T 的部署成本——即使是量化版本，也需要多卡 A100/H100 集群。对于大多数应用场景，建议关注 unsloth/Kimi-K3-GGUF 的 4-bit 量化版。

---

### 1.2 百度 Unlimited-OCR：3B 参数实现 269 万下载

**概述：** 百度发布的 Unlimited-OCR 是一个仅 30 亿参数的 OCR 模型，却在 HuggingFace 上获得了 269 万次下载，成为下载量最高的新模型之一。

**技术细节：**
- 参数量：3B（轻量级）
- 任务：Image-Text-to-Text（OCR 理解）
- 更新频率：约 19 小时前还有更新
- 配套模型：ATH-MaaS/OvisOCR2（0.9B，47.1k 下载）同样热门

**为什么这么火：** OCR 是刚需场景。3B 参数意味着可以在消费级 GPU（甚至部分 CPU 环境）上运行，而下载量说明社区对轻量级高质量 OCR 的渴求。

**💡 对你的价值：** 如果你的项目涉及文档处理、票据识别、截图文字提取等场景，Unlimited-OCR 值得立即试用。3B 参数量意味着树莓派级别的设备也能跑（通过量化），非常适合边缘部署。

---

### 1.3 Microsoft 三连发：VibeVoice · Fara1.5 · Mage-VL

**概述：** 微软今日在 HuggingFace 上共有 4 个模型上榜趋势，覆盖语音识别、图文理解和 TTS。

| 模型 | 参数量 | 类型 | 亮点 |
|------|--------|------|------|
| VibeVoice | - | 开源前沿语音 AI | 完整语音 AI 系统 |
| VibeVoice-ASR-BitNet | 0.3B | 语音识别 | BitNet 量化，极低功耗 |
| Fara1.5-27B | 27B | 图文多模态 | 视觉理解 |
| Mage-VL | 5B | 图文多模态 | 轻量级视觉语言 |

**重点：VibeVoice-ASR-BitNet** 是首个使用 BitNet（1-bit 量化）技术的 ASR 模型，仅 0.3B 参数。这意味着：
- 在手机上可以实时运行
- 功耗极低，适合 Always-on 语音监听场景
- 为端侧 AI 语音助手铺路

**💡 对你的价值：** 如果你在构建语音 Agent 或需要端侧语音识别能力，VibeVoice 系列提供了从 0.3B（端侧）到完整系统的全栈方案。BitNet ASR 是低功耗场景的游戏规则改变者。

---

### 1.4 OpenAI Sora 2 发布：AI 视频生成进入新纪元

**概述：** 据 AIFOD 报道，OpenAI 发布了 Sora 2，支持生成长时间、高分辨率视频并嵌入音频，提供实时编辑和多模态兼容。

**关键升级（vs Sora 1）：**
- ✅ 集成音频生成（不再是默片）
- ✅ 实时编辑能力
- ✅ 更长的视频时长
- ✅ 多模态输入兼容

**💡 对你的价值：** Sora 2 的音频集成是一个重大突破——之前的 AI 视频工具最大的痛点就是需要后期配音。如果你的工作涉及短视频制作、广告创意、教学内容，Sora 2 值得第一时间尝试。但注意，国内访问可能受限，建议关注是否有 API 接口开放。

---

### 1.5 其他值得关注的模型动态

| 模型 | 来源 | 亮点 |
|------|------|------|
| Nanbeige4.2-3B | Nanbeige | 4B 文本生成，18.9k 下载，小模型新选择 |
| KAT-Coder-V2.5-Dev | Kwaipilot | 35B 代码专用模型，快手出品 |
| Inflect-Micro-v2 / Nano-v2 | owensong | 新一代 TTS 模型，语音自然度提升 |
| Prism-Bonsai-27B-gguf | prism-ml | 2.34M 下载，4-bit GGUF 量化 27B |

---

## 二、Agent 架构与范式

### 2.1 Desktop-Delta Bench (DDB)：首次系统评测桌面 Agent 的 GUI 状态理解

**论文：** arXiv:2607.26041 — *Do Computer-Use Models Understand Desktop GUI Transitions?*

**问题背景：** 当前桌面 Agent 评测只看"最终任务是否成功"或"能否定位 UI 元素"，但忽略了中间环节——Agent 是否真正理解一次操作引起的 GUI 状态变化？这导致 Agent 经常：
- 把过时的截图当作最新状态
- 无法判断操作是否真的生效
- 在失败后不知道如何恢复

**研究方法：**
- 构建了 2,013 个人工验证的实例，覆盖 Linux 上 ~15 个应用、50 个任务域
- 设计了两个互补任务：
  - 三帧时序排序（463 个实例）：判断截图 A→B→C 的时间顺序
  - 操作前后配对（1,550 个实例）：从 5 种操作类型中推断发生了什么
- 评测了 8 个闭源和开源模型家族

**核心发现：**
- 最优模型的时序排序准确率仅 65.1%（远未饱和）
- 加入干扰帧后准确率几乎不变（65.7%），说明模型并不真正理解因果关系
- 推断操作类型比定位操作位置更难：点击 F1 准确率 0.96，但拖拽操作仅 0.76
- 模型存在系统性"抄近路"行为——直接复制给出的 A-B-C 顺序

**💡 对你的价值：** 如果你在构建桌面自动化 Agent，这篇论文揭示了一个被严重低估的瓶颈。建议：
1. 不要只依赖截图对比来验证操作结果
2. 为 Agent 添加显式的状态确认步骤（如检查元素属性）
3. 关注 DDB benchmark 后续发展，用它来评测你的 Agent

---

### 2.2 UniMem：Agent 的自路由记忆管理框架

**论文：** arXiv:2607.26017 — *Complementary Episodic-to-Parametric Memory for Boundary-Agnostic Task Streams*

**问题背景：** LLM Agent 需要记忆来积累经验，但真实场景中的任务流是连续的、没有明确边界的。现有方案要么依赖外部检索（快但不内化），要么依赖参数记忆（稳定但需要任务标签和固定预算）。

**核心方案：UniMem**
- 受大脑海马体-新皮层互补记忆启发
- 使用**可学习路由 token** 作为记忆控制器
- 两条互补通路：
  - **情景记忆缓冲区**：存储新颖或稀疏任务，通过检索增强执行
  - **参数记忆**：将反复出现的可靠模式巩固到可扩展的参数块中
- 关键创新：路由 token 解耦了"任务识别"和"任务执行"，按需扩展记忆而不需要任务标签

**实验结果：**
- 在长时序流式任务上，三种骨干模型平均提升 4.0 EM 点
- 记忆按需扩展，不产生不可控的参数增长

**💡 对你的价值：** 这是 Agent 记忆系统设计的一个重要参考。如果你在做长期运行的 Agent（如个人助手、自动化工作流），UniMem 的路由机制值得借鉴：
1. 新任务先存外部记忆（快、灵活）
2. 反复执行的任务模式固化到模型参数中（快、稳定）
3. 路由决策本身应该是可学习的，而不是硬编码规则

---

### 2.3 Relay-OPD：轨迹中继式在策略蒸馏

**论文：** arXiv:2607.26057 — *Pass the Baton: Trajectory-Relayed On-Policy Distillation*

**问题背景：** 在策略蒸馏（OPD）中，学生在自己的轨迹上接受 token 级监督。但一旦学生在推理早期走错方向，后续所有生成都建立在偏差之上，导致不可靠的监督信号。

**核心发现：** 教师-学生在失败前缀上存在**延续不对称性**——教师倾向于纠偏，而学生继续沿着错误方向前进。

**方案：Relay-OPD**
- 在检测到触发点时，让教师短暂"接力"，产生一段教师轨迹
- 然后学生恢复，在完整的中继轨迹上优化
- 有限的中继预算将干预集中在关键的早期位置

**实验结果：**
- 使用 Qwen3-4B 做教师，Qwen3-0.6B/1.7B 做学生
- 在 8 个数学推理 benchmark 上全部取得最佳或次佳
- 标准 OPD 提升 +5.73%，比最强基线 FastOPD 提升 +1.49%
- 训练轨迹长度减少超过 50%

**💡 对你的价值：** 如果你在做模型蒸馏或小模型训练，Relay-OPD 提供了一种优雅的方式解决"_prefix failure"问题。实际应用中：
1. 不需要额外标注数据
2. 训练成本减半（轨迹更短）
3. 特别适合推理/数学场景的小模型优化

---

## 三、开源生态

### 3.1 🏆 book-to-skill：一天 1421 星，把技术书变成 Claude Code 技能

**仓库：** [virgiliojr94/book-to-skill](https://github.com/virgiliojr94/book-to-skill)
**语言：** Python | **星数：** 12,701（今日 +1,421）

**做什么：** 将任何技术书籍 PDF 转换为 Claude Code 可用的 skill 文件——可以直接在学习和工作中引用。

**工作原理：**
1. 读取 PDF 技术书籍
2. 使用 LLM 提取核心知识点、模式和实践
3. 生成结构化的 skill 文件（包含规则、示例、参考）
4. 输出可直接在 Claude Code 中使用的格式

**💡 对你的价值：** 这是一个极其实用的工具。如果你有大量技术书籍但没时间反复翻阅，可以：
- 把《SICP》转成编程 skill，让 AI 在写代码时自动参考
- 把系统设计书籍转成架构决策 skill
- 操作步骤：`pip install book-to-skill` → 提供 PDF → 生成 skill → 放入 Claude Code 的 skills 目录

---

### 3.2 speech-to-speech：HuggingFace 全栈语音 Agent 管线

**仓库：** [huggingface/speech-to-speech](https://github.com/huggingface/speech-to-speech)
**语言：** Python | **星数：** 7,844（今日 +827）

**做什么：** 低延迟、全模块化的语音 Agent 管线：VAD → STT → LLM → TTS，暴露为 OpenAI Realtime 兼容的 WebSocket API。

**架构特点：**
- **完全模块化**：每个组件可替换
- **VAD**：Silero VAD v5
- **STT 选择**：Parakeet TDT（默认）/ Whisper / Faster Whisper / Paraformer 等 7 种
- **LLM**：任何 OpenAI 兼容 API 或本地 vLLM/llama.cpp
- **TTS 选择**：Qwen3-TTS（默认）/ Kokoro-82M / Pocket TTS / ChatTTS 等 6 种
- **运行模式**：realtime（WebSocket）/ local（麦克风）/ websocket / socket

**生产验证：** 已作为数千台 Reachy Mini 机器人的对话后端运行。

**快速启动：**
```bash
pip install speech-to-speech
export OPENAI_API_KEY=...
speech-to-speech
# 启动 OpenAI Realtime 兼容服务器 ws://localhost:8765/v1/realtime
```

**💡 对你的价值：** 这是目前最完整的开源语音 Agent 框架。如果你想构建类似 ChatGPT Voice 的本地替代品：
1. 完全本地运行（用 llama.cpp + Qwen3-TTS）
2. 兼容 OpenAI Realtime 协议（现有客户端可直接对接）
3. macOS 有优化设置：`--local_mac_optimal_settings`

---

### 3.3 openwork：开源版 Claude Cowork

**仓库：** [different-ai/openwork](https://github.com/different-ai/openwork)
**语言：** TypeScript | **星数：** 17,879

**做什么：** Claude Cowork 的开源替代品，基于 opencode 驱动。

**💡 对你的价值：** 如果你想要类似 Claude Cowork 的 AI 协作工作空间但不想依赖闭源服务，openwork 提供了自托管方案。

---

### 3.4 GeoLibre：云原生 GIS 平台，全平台运行

**仓库：** [opengeos/GeoLibre](https://github.com/opengeos/GeoLibre)
**语言：** TypeScript | **星数：** 4,013（今日 +671）

**做什么：** 轻量级云原生 GIS 平台，支持浏览器、桌面、移动端、Jupyter 笔记本。

**技术栈：** Tauri v2 + React + TypeScript + MapLibre GL JS + DuckDB-WASM Spatial + deck.gl

**亮点功能：**
- 同一工作空间跨四种平台运行
- 数据本地化，隐私保护
- 支持月球、火星等行星底图
- 700+ 免费 GIS 工具，零安装
- 3D Tiles 支持，可可视化城市建筑

**💡 对你的价值：** 即使你不是 GIS 专业人员，GeoLibre 的架构也值得学习——如何用 Tauri + Web 技术构建真正的跨平台应用。

---

### 3.5 alibaba/open-code-review：阿里级代码审查工具

**仓库：** [alibaba/open-code-review](https://github.com/alibaba/open-code-review)

**做什么：** 混合架构代码审查工具：确定性管线 + LLM Agent，提供精准的行级评论。

**内置能力：**
- 内置微调规则集（NPE、线程安全、XSS、SQL 注入）
- 兼容 OpenAI 和 Anthropic API
- 经过阿里巴巴规模验证

**💡 对你的价值：** 开源免费，且经过大厂实战检验。如果你的团队需要自动化代码审查，这比直接用 LLM 裸做要可靠得多——确定性管线处理已知模式，LLM 处理上下文理解。

---

### 3.6 MoonshotAI/FlashKDA：高性能 Kimi Delta Attention 内核

**仓库：** [MoonshotAI/FlashKDA](https://github.com/MoonshotAI/FlashKDA)
**语言：** CUDA | **星数：** 980（今日 +91）

**做什么：** FlashKDA 提供高性能的 Kimi Delta Attention 计算内核，是 Kimi 模型效率的关键组件。

**💡 对你的价值：** 如果你部署 Kimi 系列模型或使用 Delta Attention 架构，这些 CUDA 内核可以显著提升推理速度。

---

### 3.7 maderix/ANE：在 Apple Neural Engine 上训练神经网络

**仓库：** [maderix/ANE](https://github.com/maderix/ANE)
**语言：** Objective-C | **星数：** 7,139

**做什么：** 通过逆向工程的私有 API 在 Apple Neural Engine 上训练神经网络。

**💡 对你的价值：** 这是 Apple Silicon 用户的福音——利用专用 AI 硬件而不仅限于推理。虽然使用了私有 API（存在稳定性风险），但为 Mac 上的模型训练开辟了新路径。

---

### 3.8 airi：开源 AI 虚拟伙伴，支持实时语音、Minecraft 和 Factorio

**仓库：** [moeru-ai/airi](https://github.com/moeru-ai/airi)
**语言：** TypeScript | **星数：** 45,366（今日 +682）

**做什么：** 自托管的 AI 虚拟角色系统，支持实时语音对话、玩 Minecraft/Factorio、Live2D 显示。目标是复刻 Neuro-sama 的能力。

**技术特点：**
- WebGPU / WebAudio / Web Workers / WebAssembly 全 Web 技术栈
- 桌面版支持原生 CUDA 和 Apple Metal
- 支持 PWA，可在手机运行
- 内存系统：DuckDB WASM / pglite
- 语音：STT + TTS 多供应商支持

**💡 对你的价值：** 虽然定位是娱乐/虚拟角色，但 airi 的技术架构（WebGPU 推理、模块化 Agent、实时语音）对构建其他类型的 AI Agent 也有参考价值。

---

## 四、AI 工具与技巧

### 4.1 工具推荐：ClipProxy —— 把 CLI 订阅变成 OpenAI 兼容 API

**来源：** FAZM Blog

**做什么：** 将 ChatGPT CLI、Claude Code、Gemini CLI 等命令行工具的订阅暴露为 OpenAI 兼容 API 端点，支持 OAuth、负载均衡和故障转移。

**使用场景：**
- 让不支持某个 AI 服务的工具通过 API 调用它
- 在多个 CLI 订阅间做负载均衡
- 构建统一的 AI 调用网关

**💡 对你的价值：** 如果你有多个 AI 订阅（ChatGPT Plus、Claude Pro 等），ClipProxy 可以把它们统一成一个 API 端点，避免浪费。

---

### 4.2 工具推荐：ECC —— Agent 性能优化系统

**仓库：** [affaan-m/ECC](https://github.com/affaan-m/ECC)（GitHub Trending）

**做什么：** 为 Claude Code、Codex、Opencode、Cursor 等编程 Agent 提供技能、本能、记忆、安全等优化。

**💡 对你的价值：** 如果你使用编程 Agent 但觉得效果不够好，ECC 提供了一套系统化的优化框架。

---

### 4.3 工作流建议：用 Shieldstral 构建内容安全管线

**论文：** arXiv:2607.25857

**核心思路：** Shieldstral 用仅 3B 参数就匹配或超越了 7 倍大小的安全分类模型。关键创新是将内容审核建模为二分类问答任务（yes/no），统一了不同审核策略。

**实操建议：**
1. 用 Shieldstral 做第一层快速过滤（3B 推理快）
2. 对可疑内容再用大模型做精细判断
3. 54.1M 训练样本的数据构造方法可复用到你的领域

---

### 4.4 初学者友好：HuggingFace 语音 Agent 5 分钟部署

基于 speech-to-speech 项目，最快的上手路径：

```bash
# 1. 安装
pip install speech-to-speech

# 2. 设置 API（用 OpenAI 或任何兼容服务）
export OPENAI_API_KEY=sk-xxx

# 3. 启动（默认配置）
speech-to-speech

# 4. 另开终端对话
python scripts/listen_and_play_realtime.py --host 127.0.0.1 --port 8765
```

**完全本地运行（无需 API）：**
```bash
# 用 llama.cpp 跑 Gemma 4
llama-server -hf ggml-org/gemma-4-E4B-it-GGUF -np 2 -c 65536

# 指向本地 LLM
speech-to-speech \
  --model_name "ggml-org/gemma-4-E4B-it-GGUF" \
  --responses_api_base_url "http://127.0.0.1:8080/v1" \
  --responses_api_api_key ""
```

---

### 4.5 实用技巧：macOS 上最优语音 Agent 配置

```bash
speech-to-speech --local_mac_optimal_settings
```

这个命令会自动：
- 启用 MPS 加速
- 选择 Parakeet TDT 做 STT
- 使用 MLX LM 做 LLM 后端
- 使用 Qwen3-TTS 做语音输出（mlx-audio 6bit 量化）
- 启动本地麦克风模式

**💡 提示：** 可以替换 LLM 模型：
```bash
speech-to-speech \
  --local_mac_optimal_settings \
  --model_name mlx-community/Qwen3-4B-Instruct-2507-bf16
```

---

## 五、值得深读的研究

### 5.1 📖 AI 辅助科研：能力与偏见

**论文：** arXiv:2607.25881 — *AI's Capability in Assisting Scientific Research in Physics, Astrophysics, and Cosmology II*

**研究方法：**
- 8 个物理/天体物理/宇宙学研究项目
- 分别由人类和 3 个 LLM（ChatGPT、Claude、DeepSeek）独立撰写一页纸项目计划
- 共 32 份提案，由 4 位人类评审和 2 个前沿 LLM（Claude Opus 4.8、ChatGPT Pro 5.5）盲审

**核心发现：**
1. **人类评审**：对人类和 AI 撰写的提案评分相似——AI 可以写出质量匹美的研究计划
2. **AI 评审**：系统性地给 AI 写的提案高约 1 分（5 分制）
3. **识别能力**：人类正确识别 AI 文案的概率为 72-79%，而两个 AI 评审 100% 识别了所有提案
4. **警示信号**：AI 评审对 AI 生成内容有系统性偏好

**启发：**
- AI 已能写出"以假乱真"的科研计划
- 但 AI 评审存在对 AI 文案的偏好偏见——如果未来基金评审大量使用 AI，可能形成正反馈循环
- 建议：AI 辅助写作可以使用，但评审环节应限制 AI 参与度

---

### 5.2 📖 LLM 做运筹优化：京东多仓库存分配实战

**论文：** arXiv:2607.25956 — *Large Language Model for Operations Research Formulation Selection in Multi-Warehouse Inventory Allocation*

**研究方法：**
- 将多仓库存分配建模为 MIP（混合整数规划）
- 构建"OR 专家库"，每个专家对应一种 MIP 公式
- 用 LLM 做实例级的公式选择器
- 训练两阶段：SFT（schema 学习）→ GRPO（强化学习优化）

**核心结果（来自京东真实数据）：**
- GRPO 将选择准确率从 21.45% 提升到 50.42%（Hit@1）
- 比最佳固定公式准确率提升 12.57 个百分点
- 与事后最优 Oracle 的差距缩小到仅 4.85 个百分点

**启发：**
- LLM 不是直接求解优化问题，而是做"方法选择"——根据实例特征选择最合适的求解策略
- GRPO 比 SFT+IPO 效果更好——强化学习在策略选择场景的优势
- 这个"LLM 做路由/选择"的模式可以推广到很多领域

---

### 5.3 📖 ClinPRISM：低成本多模态 LLM 处理不规则临床时间序列

**论文：** arXiv:2607.25947 — *A Cost-Effective Multimodal LLM Reasoning Framework for Question Answering over Irregular Clinical Time Series*

**问题：** 临床时间序列数据具有稀疏性、异步性和不规则采样模式，通用时间序列 LLM 难以处理。

**方法创新：**
1. 不规则感知多尺度编码器：在多个时间尺度上捕获稀疏临床证据
2. 时间证据蒸馏器：跨尺度整合并压缩为少量 LLM 兼容 token
3. 渐进式对齐策略：将不规则轨迹逐步对齐到 LLM 文本嵌入空间

**数据规模：**
- 30,000 临床时间序列 + 多尺度描述
- 41,000 指令微调实例，覆盖 11 个任务

**令人印象深刻的效率：**
- 仅 40 亿参数骨干
- 只用 16 个时间序列 token
- 平均推理延迟仅 0.15 秒/问题

**💡 启发：** 这种"压缩 → 少量 token → LLM"的范式适用于任何不规则序列数据（IoT 传感器、金融交易、用户行为日志等）。关键创新在于渐进式对齐——不是一次性对齐，而是逐步让序列数据"融入"LLM 的理解空间。

---

### 5.4 📖 Shieldstral：3B 参数匹配 21B 的安全分类器

**论文：** arXiv:2607.25857

**核心创新：**
- 将内容审核建模为二分类问答（yes/no）
- 54.1M 训练样本
- 3B 参数匹配或超越 7 倍大小模型
- 统一了不同审核策略和分类体系

**💡 启发：** 任务建模方式比模型大小更重要。如果你的安全分类任务效果不佳，先检查建模方式——也许不需要更大的模型，而是需要更好的任务形式化。

---

## 六、今日学习建议

### 🎯 具体可执行建议

#### 1. 动手：部署一个本地语音 Agent（30 分钟）

**目标：** 用 speech-to-speech 搭建完全本地的语音对话系统

**步骤：**
1. `pip install speech-to-speech`
2. 安装 llama.cpp，下载 Gemma 4 模型
3. 启动本地 LLM 服务器
4. 启动 speech-to-speech 指向本地 LLM
5. 体验全栈开源语音 Agent 的效果

**学到什么：** VAD → STT → LLM → TTS 管线的完整工作流，理解每个环节的延迟瓶颈

---

#### 2. 阅读：Desktop-Delta Bench 论文（1 小时）

**论文：** [arXiv:2607.26041](https://arxiv.org/abs/2607.26041)

**重点关注：**
- 为什么 GUI 状态理解是桌面 Agent 的瓶颈
- 时序排序 vs 操作推断两种评测方法的差异
- 模型"抄近路"行为的分析

**为什么现在读：** 桌面 Agent 正在成为热点（Computer Use），但这篇论文揭示了被忽视的基础能力缺陷。

---

#### 3. 实践：用 book-to-skill 转换一本你一直在读的技术书（1 小时）

**目标：** 把一本技术 PDF 转换为 Claude Code 可用的 skill

**步骤：**
1. `git clone https://github.com/virgiliojr94/book-to-skill`
2. 准备一本你经常参考的技术书 PDF
3. 运行转换
4. 将生成的 skill 放入你的工作目录
5. 在实际编码中测试效果

**学到什么：** 如何把静态知识转化为 AI 可消费的结构化技能

---

#### 4. 研究：UniMem 的记忆路由机制（45 分钟）

**论文：** [arXiv:2607.26017](https://arxiv.org/abs/2607.26017)

**思考问题：**
- 你的 Agent 目前如何处理记忆？是纯检索还是参数化？
- 路由 token 的设计能否简化为规则？什么时候可学习的路由明显更好？
- 如何在不标注任务边界的情况下检测"这个任务模式已经足够稳定，可以固化"？

**延伸阅读：** 对比 MemGPT、LangChain Memory、AutoGPT 的记忆方案

---

#### 5. 关注：ICML 2026 和 ACL 2026 论文

**资源：**
- ICML 2026（首尔）：[Paper Digest 索引](https://resources.paperdigest.org/) — 6,500+ 论文
- ACL 2026：2,400+ 论文已索引

**建议策略：**
1. 先用 Paper Digest 的搜索功能按你感兴趣的主题筛选
2. 关注"有代码"的论文（ICML 页面专门列出了公开代码的论文）
3. 每天精读 1-2 篇，比泛读 20 篇更有效

---

## 📌 今日总结

| 类别 | 今日最重要的事 |
|------|--------------|
| 模型 | Kimi-K3 2.8T 登顶，开源多模态新标杆 |
| Agent | DDB 揭示桌面 Agent 的 GUI 理解瓶颈 |
| 记忆 | UniMem 提出自路由情景/参数双通路记忆 |
| 蒸馏 | Relay-OPD 解决学生模型前缀失败问题 |
| 工具 | speech-to-speech 全栈语音 Agent 管线 |
| 效率 | book-to-skill 一天 1400+ 星，知识转化利器 |
| 安全 | Shieldstral 3B 匹配 21B 安全分类器 |
| 应用 | LLM 做 OR 公式选择在京东实战验证 |

---

> **编辑说明：** 本期情报基于 arXiv cs.AI/cs.CL/cs.LG（2026-07-29）、GitHub Trending、HuggingFace Models/Papers、AIFOD、FAZM Blog、DevFlokers、Paper Digest 等 15+ 信源生成。所有论文链接均为 arXiv 原始链接，可直接访问。
>
> **下期预告：** 关注 ICML 2026 最佳论文公布、Kimi-K3 社区评测结果、Sora 2 实际效果反馈。

---

*Generated at 2026-07-30 08:00 (Asia/Shanghai) by AI Daily Digest*
