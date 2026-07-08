# AI 每日情报 | 2026-07-08

> 数据来源：arXiv、GitHub Trending、HuggingFace Papers  
> 整理时间：2026年7月8日 北京时间

---

## 今日概览

**🔥 核心趋势：Claude Code 生态爆发 + AI Agent 工具链成熟**

今天的 GitHub Trending 被 Claude Code 相关项目屠榜，6 个 Top 10 项目直接或间接围绕 Claude Code 构建。同时，AI Agent 的"基础设施层"正在快速成型——从沙箱隔离、Office 文档操作到视频理解，完整的工具链正在浮出水面。

---

## 一、前沿模型动态

### 1.1 系统提示词透明度运动

**关键发现：** `system_prompts_leaks` 项目今日获得 1,691 星（总计 53,054 星），成为 GitHub 第三热门项目。

**项目概况：**
- 收录了 Claude Fable 5、Opus 4.8、Sonnet 5、Claude Code 等 Anthropic 全系列模型的系统提示词
- 同时覆盖 OpenAI GPT-5.5（Thinking/Instant）、Google Gemini 3.5 Flash、xAI Grok Expert
- 包含 Claude Code (Opus 4.8) 的完整工具定义（48 个工具 + 16 个技能）
- 提供模型间对比工具（如 [Opus 4.8 → Fable 5 差异](https://www.diffchecker.com/QJn9jFNk/)）

**💡 对你的价值：**
1. **理解 AI 行为：** 知道模型被如何指令，能更好预测和优化提示词
2. **学习最佳实践：** 从顶级 AI 公司的提示词工程中学习结构化思维
3. **安全研究：** 理解模型边界和限制，避免触发不必要的安全拦截

**相关资源：**
- GitHub: https://github.com/asgeirtj/system_prompts_leaks
- 华盛顿邮报报道: https://wapo.st/49t4gSb

---

## 二、Agent 架构与范式

### 2.1 Claude Code 生态爆发

**今日 GitHub Top 10 中有 6 个项目与 Claude Code 直接相关：**

#### 1. ai-job-search（+2,514 星，总计 11,103 星）
**今日第一热门项目**

**做什么：** 基于 Claude Code 的全栈求职助手框架
- 自动评估岗位匹配度
- 定制简历和求职信（LaTeX 输出）
- 面试准备辅助
- 支持丹麦本地招聘网站（可替换为其他市场）

**核心工作流：**
```
/setup → /scrape → /apply → /rank → /outcome
  ↓        ↓          ↓        ↓        ↓
建档    搜索岗位   申请岗位  批量评分  追踪结果
```

**💡 对你的价值：**
- 即使不在丹麦，这个框架的模式可以直接复用
- 展示了 Claude Code 作为"工作流引擎"的最佳实践
- 包含 drafter-reviewer 双 Agent 模式（写手 + 审核员）

**技术亮点：**
- 8 个 slash 命令覆盖完整求职流程
- 内置 ATS 可解析性检查
- 支持自定义 LaTeX 模板和招聘门户

**GitHub:** https://github.com/MadsLorentzen/ai-job-search

---

#### 2. agent-skills（+1,317 星，总计 72,204 星）
**Addy Osmani 出品，AI Agent 工程化技能包**

**做什么：** 将高级工程师的工作流、质量门禁、最佳实践编码为 Agent 可执行的技能

**核心技能矩阵：**
| 阶段 | 命令 | 关键原则 |
|------|------|----------|
| 定义 | `/spec` | 先写规格再写代码 |
| 规划 | `/plan` | 小而原子化的任务 |
| 构建 | `/build` | 薄垂直切片 |
| 验证 | `/test` | 测试即证明 |
| 审查 | `/review` | 合并前改进代码健康 |
| 发布 | `/ship` | 更快即更安全 |

**💡 对你的价值：**
- 24 个生产级技能，覆盖完整开发生命周期
- 支持 70+ Agent（Claude Code、Cursor、Codex、Copilot 等）
- 一键安装：`npx skills add addyosmani/agent-skills`

**实战建议：**
- 新项目：先 `/spec` 再 `/build`，避免"边写边想"
- 代码审查：用 `/review` 自动触发五轴审查
- 性能优化：`/webperf` 先测量再优化

**GitHub:** https://github.com/addyosmani/agent-skills

---

#### 3. claude-video（+965 星，总计 5,203 星）
**让 Claude 能"看"视频**

**做什么：** 给 Claude Code 添加视频理解能力
- 下载视频（支持 YouTube、Loom、TikTok 等 100+ 平台）
- 智能抽帧（场景感知 + 去重）
- 提取字幕/转录（优先免费字幕，Whisper API 兜底）
- 将帧 + 转录交给 Claude 分析

**核心命令：**
```bash
/watch https://youtu.be/xxx what happens at 30s?
/watch bug-repro.mov what's going wrong?
/watch https://youtu.be/long-video summarize this
```

**💡 对你的价值：**
1. **竞品分析：** 分析竞争对手的产品演示视频
2. **Bug 诊断：** 直接让用户发的屏幕录制"说话"
3. **学习加速：** 把长视频课程变成可搜索的笔记

**技术细节：**
- 智能帧预算：30 秒视频 ~30 帧，>10 分钟视频 100 帧封顶
- 去重算法：基于 16×16 灰度缩略图的平均绝对差异
- 支持聚焦模式：`--start 0:45 --end 1:00` 只分析特定时间段

**GitHub:** https://github.com/bradautomates/claude-video

---

#### 4. awesome-claude-code
**Claude Code 资源精选集**

**收录内容：**
- 顶级技能（skills）
- 双 Agent 模式（ambidextrous agents）
- 状态栏插件
- 开发者工具
- 插件生态

**💡 对你的价值：** 一站式发现 Claude Code 生态的最佳实践和工具

**GitHub:** https://github.com/hesreallyhim/awesome-claude-code

---

### 2.2 AI Agent 基础设施成熟

#### 1. CubeSandbox（+664 星，总计 8,485 星）
**腾讯云开源的 AI Agent 沙箱**

**核心指标：**
| 指标 | Docker | 传统 VM | CubeSandbox |
|------|--------|---------|-------------|
| 隔离级别 | 低（共享内核） | 高（独立内核） | 极高（独立内核 + eBPF） |
| 启动速度 | 秒级 | 分钟级 | **<60ms** |
| 内存开销 | 低 | 高（完整 OS） | **<5MB** |
| 部署密度 | 高 | 低 | **极高（单节点数千实例）** |

**关键特性：**
- **硬件级隔离：** 每个沙箱独立 Guest OS 内核，杜绝 Docker 共享内核逃逸
- **E2B SDK 兼容：** 一行环境变量替换，零业务代码改动
- **快照/克隆/回滚：** 百毫秒级检查点，支持任意状态恢复
- **凭证保险箱：** Agent 调用外部 API，密钥永不进入沙箱
- **AutoPause/AutoResume：** 空闲沙箱自动挂起，下次请求时唤醒

**💡 对你的价值：**
1. **安全执行不可信代码：** LLM 生成的代码在隔离环境运行
2. **高密度部署：** 单节点运行数千 Agent，成本大幅降低
3. **快速原型：** 毫秒级启动，适合 RL 训练和 SWE-Bench 场景

**GitHub:** https://github.com/TencentCloud/CubeSandbox

---

#### 2. OfficeCLI（+893 星，总计 10,070 星）
**为 AI Agent 设计的 Office 套件**

**做什么：** 让 AI Agent 完整控制 Word、Excel、PowerPoint
- 从零创建文档
- 读取文本、结构、样式、公式
- 修改任意元素（文本、字体、颜色、布局、图表）
- 实时预览（`officecli watch`）

**核心优势：**
- **单二进制文件：** 无需安装 Office，无依赖
- **跨平台：** macOS/Linux/Windows
- **高保真渲染：** 内置 HTML 渲染引擎，支持 .docx/.xlsx/.pptx → HTML/PNG
- **AI 视觉闭环：** 渲染 → 查看 → 修复，Agent 能"看到"文档

**实战示例：**
```bash
# 创建 PPT
officecli create deck.pptx
officecli add deck.pptx / --type slide --prop title="Q4 Report"

# 实时预览
officecli watch deck.pptx
# 浏览器打开 http://localhost:26315
# 每次 add/set/remove 命令都会实时刷新
```

**💡 对你的价值：**
1. **自动化报告：** Agent 直接生成 PPT/Word/Excel
2. **文档处理流水线：** 批量转换、分析、修改 Office 文件
3. **降低门槛：** 以前需要 50 行 Python + 3 个库，现在 1 行命令

**GitHub:** https://github.com/iOfficeAI/OfficeCLI

---

### 2.3 .NET 生态入场

#### dotnet/skills（+64 星，总计 4,318 星）
**微软官方 .NET AI Agent 技能包**

**做什么：** 为 .NET 和 C# 开发提供 AI Agent 技能

**💡 对你的价值：**
- .NET 开发者终于有官方支持的 Agent 技能
- 与 Addy Osmani 的 agent-skills 互补
- 企业级 .NET 项目的 Agent 辅助开发

**GitHub:** https://github.com/dotnet/skills

---

## 三、开源生态

### 3.1 今日热门开源项目

#### 1. pocket-tts（+531 星，总计 6,205 星）
**Kyutai Labs 出品的 CPU 端 TTS**

**核心指标：**
- **模型大小：** 100M 参数
- **运行环境：** 纯 CPU（无需 GPU）
- **延迟：** ~200ms 首包
- **速度：** MacBook Air M4 上 ~6x 实时
- **CPU 占用：** 仅 2 核
- **语言支持：** 英语、法语、德语、葡萄牙语、意大利语、西班牙语

**关键特性：**
- `pip install` 即用
- 支持声音克隆（传入 wav 文件）
- 流式音频输出
- 可处理无限长文本
- 可在浏览器端运行

**💡 对你的价值：**
1. **本地 TTS：** 无需 Web API，隐私友好
2. **低成本部署：** CPU 即可运行，边缘设备友好
3. **快速原型：** 几行代码即可集成语音功能

**实战示例：**
```bash
# 安装
uvx pocket-tts generate

# 指定声音和文本
pocket-tts generate --voice alba --text "Hello world"

# 启动本地服务
pocket-tts serve
# 访问 http://localhost:8000
```

**GitHub:** https://github.com/kyutai-labs/pocket-tts  
**Demo:** https://kyutai.org/pocket-tts

---

#### 2. meetily
**隐私优先的 AI 会议助手**

**核心特性：**
- 4x 更快的 Parakeet/Whisper 实时转录
- 说话人分离（speaker diarization）
- Ollama 本地总结
- 100% 本地处理，无需云端
- 支持 macOS 和 Windows
- 自托管、开源

**💡 对你的价值：**
- 企业内部会议记录，数据不出境
- 无需订阅 SaaS，一次部署永久使用
- 基于 Rust，性能优异

**GitHub:** https://github.com/Zackriya-Solutions/meetily

---

#### 3. RuView
**WiFi 信号 → 空间智能**

**做什么：** 将普通 WiFi 信号转化为实时空间感知、生命体征监测和存在检测
- **无需摄像头：** 完全基于 WiFi 信号
- **实时监测：** 人体存在、位置、生命体征
- **隐私友好：** 不采集图像/视频

**💡 对你的价值：**
- 智能家居/办公：无摄像头的人员检测
- 养老监护：非接触式生命体征监测
- 安防场景：低成本存在检测

**GitHub:** https://github.com/ruvnet/RuView

---

#### 4. CodexBar
**OpenAI Codex 和 Claude Code 用量统计**

**做什么：** 显示使用情况统计，无需登录

**💡 对你的价值：**
- 监控 AI 编码助手的使用频率和成本
- 无需依赖官方仪表板
- 适合团队成本管控

**GitHub:** https://github.com/steipete/CodexBar

---

### 3.2 技术趋势分析

**今日趋势总结：**

1. **Claude Code 成为"操作系统"：**
   - 不再是单一工具，而是生态平台
   - 第三方围绕它构建完整工作流（求职、开发、视频分析）
   - Skills 机制成为标准化接口

2. **Agent 工具链"三层架构"浮现：**
   - **执行层：** CubeSandbox（安全沙箱）
   - **操作层：** OfficeCLI（文档操作）、claude-video（视频理解）
   - **工程层：** agent-skills（工程化最佳实践）

3. **CPU 端 AI 推理崛起：**
   - pocket-tts：100M 参数 TTS 纯 CPU 运行
   - meetily：本地转录 + 总结
   - 趋势：边缘设备、隐私优先、低成本部署

4. **透明度运动：**
   - system_prompts_leaks 持续火爆
   - 用户渴望理解 AI 如何被指令
   - 推动 AI 公司更开放

---

## 四、AI 工具与技巧

### 4.1 实用工具推荐

#### 1. Agent Skills CLI
**一键为 70+ Agent 安装技能**

**安装：**
```bash
npx skills add addyosmani/agent-skills  # 安装全部 24 个技能
npx skills add addyosmani/agent-skills --list  # 浏览后选择
```

**支持的 Agent：**
- Claude Code（推荐）
- Cursor
- Codex
- GitHub Copilot
- Gemini CLI
- Windsurf
- OpenCode
- Kiro IDE
- 以及更多...

**💡 使用建议：**
- 新项目：先 `npx skills add` 再开始编码
- 团队协作：统一技能包，保证代码质量一致性
- 学习最佳实践：阅读每个 SKILL.md 理解工程化思维

**官网：** https://agentskills.io

---

#### 2. OfficeCLI 快速上手

**安装（macOS/Linux）：**
```bash
curl -fsSL https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.sh | bash
```

**或 Windows PowerShell：**
```powershell
irm https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.ps1 | iex
```

**基础用法：**
```bash
# 创建 PPT
officecli create presentation.pptx

# 添加幻灯片
officecli add presentation.pptx / --type slide --prop title="项目汇报"

# 实时预览
officecli watch presentation.pptx
# 浏览器打开，实时看到修改效果
```

**💡 进阶技巧：**
- 用 `officecli view doc.docx html` 在浏览器查看文档
- 用 `officecli get sheet.xlsx '/sheet[1]/cell[A1]' --json` 获取结构化数据
- 结合 Claude Code，让 Agent 自动生成报告

---

#### 3. Claude Video 实战

**安装（Claude Code）：**
```bash
/plugin marketplace add bradautomates/claude-video
/plugin install watch@claude-video
```

**或通用安装：**
```bash
npx skills add bradautomates/claude-video -g
```

**使用场景：**

**场景 1：竞品分析**
```
/watch https://youtu.be/competitor-demo what hook did they open with?
```
Claude 分析开场帧 + 转录，拆解结构

**场景 2：Bug 诊断**
```
/watch bug-repro.mov what's going wrong?
```
Claude 逐帧查看，定位问题时刻

**场景 3：长视频总结**
```
/watch https://youtu.be/long-tutorial summarize this to a note
```
生成结构化笔记，可搜索

**💡 进阶技巧：**
- 聚焦特定时间段：`--start 2:30 --end 3:00`
- 调整详细度：`--detail efficient|balanced|token-burner`
- 去重：默认开启，避免重复帧浪费 token

---

### 4.2 工作流最佳实践

#### AI Agent 开发工作流（基于 agent-skills）

**推荐流程：**
```
1. /spec - 写清楚要做什么
   ↓
2. /plan - 拆解成小任务
   ↓
3. /build - 薄垂直切片实现
   ↓
4. /test - 测试驱动，每步验证
   ↓
5. /review - 合并前审查
   ↓
6. /ship - 安全发布
```

**关键原则：**
- **先规格后代码：** 不要"边写边想"
- **小而原子：** 每个任务只改一件事
- **测试即证明：** 没有测试 = 没有完成
- **快速反馈：** 每步都验证，不要积累问题

---

### 4.3 初学者友好建议

**本周可以做的事：**
1. 安装 agent-skills：`npx skills add addyosmani/agent-skills`
2. 试用 OfficeCLI：创建一个简单的 PPT
3. 了解 Claude Code 生态：浏览 awesome-claude-code

**本月可以学的内容：**
1. 掌握 `/spec` → `/build` → `/test` 工作流
2. 用 pocket-tts 实现本地 TTS
3. 用 CubeSandbox 搭建安全的 Agent 执行环境

**长期方向：**
- 理解 Agent 工具链三层架构
- 构建自己的 Skills 包
- 探索 CPU 端 AI 推理的更多可能

---

## 五、值得深读的研究

### 5.1 Light-Omni: 基于反思的轻量级视频理解 Agent

**论文信息：**
- **标题：** Light-Omni: Reflex over Reasoning in Agentic Video Understanding with Long-Term Memory
- **机构：** 南京大学
- **arXiv ID：** 2607.05511
- **项目主页：** https://clare-nie.github.io/Light-Omni

**一句话总结：** 通过双重上下文状态，在单次前向传播中实现即时视频理解，避免昂贵的迭代推理。

**核心问题：**
现有视频 Agent 依赖"侦探式"迭代推理（搜索 → 聚合证据），导致成本高、延迟大。这些重推理主要是为了补偿全局上下文缺失和检索语义不对齐。

**解决方案：**
Light-Omni 引入双重上下文状态：
1. **全局状态：** 有限大小的多模态脚本，从情景记忆持续整合
   - 层级合并：保留近期细节，总结过去事件
2. **参数化潜在状态：** 基于全局状态生成，直接驱动自主动作和检索嵌入
   - 最小延迟，实现反射式响应

**核心结果：**
- 比 M3-Agent 平均准确率提升 2.4%
- 速度提升 12.1 倍
- GPU 内存效率提升 2.6 倍
- 可作为记忆系统增强现有 MLLM 的性能和效率

**💡 对你的价值：**
1. **视频 Agent 效率革命：** 从迭代推理 → 单次前向传播
2. **长期视频理解：** 适合监控、会议记录、长视频分析
3. **边缘部署：** 更低的计算成本意味着可在资源受限环境运行

**技术启发：**
- 全局状态 + 参数化状态的耦合设计
- 层级合并策略平衡细节与摘要
- 检索语义对齐是关键

**论文链接：** https://arxiv.org/abs/2607.05511

---

## 六、今日学习建议

### 本周行动
1. **安装 agent-skills：** 体验 `/spec` → `/build` 工作流
2. **试用 OfficeCLI：** 创建一个简单的 PPT 或 Word 文档
3. **了解 Claude Code 生态：** 浏览 awesome-claude-code，找到适合你的工具

### 本月目标
1. **掌握 Agent 开发工作流：** 从 `/spec` 到 `/ship` 的完整流程
2. **探索 CPU 端 AI 推理：** 用 pocket-tts 实现本地 TTS
3. **理解 Agent 工具链：** 沙箱（CubeSandbox）+ 文档操作（OfficeCLI）+ 视频理解（claude-video）

### 长期方向（6 个月后）
- 构建自己的 Skills 包，编码团队最佳实践
- 设计高效的 Agent 工作流，平衡质量与速度
- 探索边缘设备上的 AI Agent 部署

### 推荐资源
1. **agent-skills 文档：** https://github.com/addyosmani/agent-skills
   - 为什么推荐：生产级工程实践，覆盖完整开发生命周期
   
2. **OfficeCLI Wiki：** https://github.com/iOfficeAI/OfficeCLI/wiki
   - 为什么推荐：详细的 Office 文档操作指南

3. **CubeSandbox 架构文档：** https://github.com/TencentCloud/CubeSandbox/blob/master/docs/architecture/overview.md
   - 为什么推荐：理解 AI Agent 安全执行的最佳实践

4. **Claude Video Demo：** https://github.com/bradautomates/claude-video
   - 为什么推荐：视频理解 Agent 的实战案例

---

_本文由 Zoe AI 助手自动生成，每日更新。归档于 /data/share/work/ai-daily-digest/_
