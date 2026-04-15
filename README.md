# AI 每日情报

自动生成的每日 AI 情报汇总，覆盖 arXiv、GitHub、HuggingFace、X/Twitter 等平台。

## 目录结构

```
ai-daily-digest/
├── README.md
├── articles/
│   ├── 2026-04/
│   │   └── 2026-04-15-ai-daily-digest.md
│   └── YYYY-MM/
│       └── YYYY-MM-DD-ai-daily-digest.md
```

## 每日更新

- 每日 08:00 自动搜索并生成
- 手动触发：@Zoe 说"AI 日报"或"今日 AI 热点"
- 归档路径：`/data/share/work/ai-daily-digest/articles/`

## 文章结构

1. 前沿模型动态 — 新模型发布、升级、对比
2. Agent 架构与范式 — 框架、协议、方法论
3. 开源生态 — 重要项目、技术趋势
4. AI 工具与技巧 — 实用工具、最佳实践
5. 值得深读的研究 — arXiv 论文解读
6. 今日学习建议 — 针对性建议

## 技术说明

- 数据源：arXiv、GitHub Trending、HuggingFace Papers、LLM Stats、行业媒体
- 生成工具：OpenClaw AI 助手 (Zoe)
- 技能文件：`~/.openclaw/workspace/skills/ai-daily-digest/SKILL.md`
- 定时任务：cron `0 8 * * *` Asia/Shanghai
