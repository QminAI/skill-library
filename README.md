# 我的 Skill 手册

这里记录我觉得值得长期保留的 Agent Skills：它们解决什么问题、如何调用、安装在哪里，以及以后怎样更新。文档用中文编写，方便忘记名称时通过用途找回。

这里以中文使用笔记为主。`sources/` 另存经过筛选的第三方 Skill 源码快照、原项目地址、提交号和许可证，供阅读与比较；**归档不等于安装或启用**。实际安装位置由各个 Agent 决定。

## 已收录

| Skill | 一句话用途 | 关键词 | 状态 | 文档 |
| --- | --- | --- | --- | --- |
| SeeCode | 把简短描述或 JSON 规格变成可交互、可导出的图表 | 架构图、流程图、时序图、数据图、等距 3D | 已在 Codex 全局安装 | [使用笔记](skills/seecode.md) |
| AI Coding 工作流技能组 | 梳理需求、实现、审查与交接；收录文章提到的公开 Skill | think、grill、implement、ponytail、handoff、check、Superpowers | 已下载归档，未安装 | [中文导览](skills/ai-coding-workflow.md) |

## 怎么用这份手册

1. 先从上面的关键词找到对应 skill，再打开使用笔记看适用场景和示例提问。
2. 下载或安装新 skill 后，按 [笔记模板](skills/_template.md)新增一页，并在上表加一行，写明实际状态。
3. 每篇笔记至少写清楚：**适用场景、来源、当前是否安装、最简单的提问、更新方式**。
4. 如果 skill 有项目级配置或会访问外部服务，在笔记中说明首次使用步骤和相关限制。

## 本机与 GitHub

- 本机文档库：`~/Documents/Codex/skill-library`
- Codex 全局 skill 目录：`~/.codex/skills`
- GitHub：<https://github.com/QminAI/skill-library>

文档库是长期维护的位置。安装目录由 Codex 读取，可能随 skill 更新；不要在安装目录里写个人笔记。

## 新增一项的简短流程

```text
找到原项目 → 确认来源、许可证和版本 → 按需下载或安装 → 写中文笔记并标明状态 → 更新索引 → 提交并推送
```

只有实际安装、运行过，才标为“已安装”“已验证”。上游功能和安装方法可能变化，以原项目说明为准。
