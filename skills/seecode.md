# SeeCode：把描述变成可交互图表

## 速览

| 项目 | 记录 |
| --- | --- |
| 适合做什么 | 架构图、流程图、时序图、数据模型、图表、等距 3D 对象等 |
| 产物 | 可交互的独立 HTML；可导出 PNG、JPEG、SVG、GIF、MP4 |
| 原项目 | [Aryanutkarsh/SeeCode](https://github.com/Aryanutkarsh/SeeCode) |
| 中文笔记首次记录 | 2026-10-12 |
| 本机版本 | 0.6.1 |
| 本机状态 | 已安装到 Codex 全局 skill 目录；`doctor` 诊断通过 |
| 安装位置 | `~/.codex/skills/seecode` |
| 环境要求 | Node.js 20 或更新版本；本机验证时为 Node.js 24.19.0 |

## 什么时候用

- 想看系统有哪些组件、请求如何流转、谁依赖谁。
- 想把流程、状态变化、数据库关系或时间顺序画清楚。
- 想做可交互的 HTML 图，或导出图片和视频用于文档、幻灯片。
- 想把已有 Mermaid、Graphviz/DOT、PlantUML、draw.io 等图重新整理成 SeeCode 图。

一句话或表格就能讲清的内容，直接用文字或表格更省事。

## 最简单的用法

在 Codex 中直接用自然语言提出要求，例如：

> 用 SeeCode 画一个结账流程：浏览器请求 API，API 写入 Postgres，调用 Stripe 收款，然后向 Kafka 发布事件。突出支付路径，使用深色风格。

后续可以继续说：

- “把它改成时序图。”
- “只突出支付路径。”
- “导出一张适合放进幻灯片的 SVG。”
- “把动画关掉，做成静态图。”

SeeCode 支持 45 类图，包括架构图、流程图、时序图、状态机、ER 图、甘特图、桑基图和等距 3D。完整类型及示例见[原项目说明](https://github.com/Aryanutkarsh/SeeCode#45-diagram-types)。

## 首次在一个项目中使用

第一次使用时，SeeCode 会询问采用全局设置还是为当前项目创建独立设置：

- **全局设置**：普通临时项目，想沿用同一套风格时选它。
- **项目设置**：一个项目需要专门的主题、输出目录或品牌色时选它。

截至本笔记记录时，尚未替当前项目做这个选择。真正第一次绘图时再决定即可。

## 安装与验证

本机这次通过 Codex 内置的 `skill-installer` 从原仓库 `skills/seecode` 安装。原项目给 Codex 等 Agent Skills 主机提供的通用安装命令是：

```bash
npx skills add Aryanutkarsh/seecode -g
```

`-g` 表示全局安装。安装后可用下面的命令检查环境：

```bash
node ~/.codex/skills/seecode/scripts/seecode.mjs doctor
```

本机验证结果：Node、渲染、浏览器、静态图片、GIF、MP4 检查均通过。新安装的 skill 通常在**新任务或新会话**中自动出现在可用列表。

## 更新

本机这次是通过 Codex 的安装脚本下载，不会自动更新。需要更新时，可以让 Codex 重新从[原项目](https://github.com/Aryanutkarsh/SeeCode#updating)安装并再次运行 `doctor`，同时把本页版本号改成实际安装版本。

如果以后改用上面的 `npx skills add` 方式管理，可按原项目说明使用：

```bash
npx skills update seecode -g
```

这条更新命令适用于通过 `npx skills add` 安装的副本；不能据此假定当前安装会自动更新。

## 常用入口

- [原项目 README](https://github.com/Aryanutkarsh/SeeCode)
- [图表规格示例](https://github.com/Aryanutkarsh/SeeCode/tree/main/examples/specs)
- [等距 3D 说明](https://github.com/Aryanutkarsh/SeeCode/blob/main/skills/seecode/references/isometric.md)
- [安装和更新说明](https://github.com/Aryanutkarsh/SeeCode#install)
