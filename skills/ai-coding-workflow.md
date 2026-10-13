# AI Coding 工作流 Skill 导览

依据[《入职大厂两个月，我的 AI 开发心得》](https://x.com/huangtongxueh/status/2108577165306687938)整理。记录日期：2026-10-12。

**当前状态：公开源码已下载并归档在本仓库 `sources/ai-coding-workflow/`；没有安装、启用或运行这些 Skill。** 归档版本固定在各上游的提交号，详见[源码索引](../sources/ai-coding-workflow/README.md)。这些文件是第三方项目的原文，不代表本手册的指令。

## 先分清概念

- **Skill**：给 Agent 的可复用做事方法，通常以 `SKILL.md` 为入口，可以附带参考文档或脚本。文章里的 `think`、`grill-me` 等属于这一类。
- **Prompt**：某次对话里直接给模型的要求。文章举的“第一性原理”“奥卡姆剃刀”等短句是方法提示，本身不是可安装的 Skill。
- **模型与 Agent**：GPT、Claude、DeepSeek 是模型；Codex、Claude Code、pi 是运行 Agent 的环境。它们不等于 Skill。
- **MCP、CLI、脚本与浏览器**：给 Agent 提供执行能力或数据入口。文章的只读数据库 MCP、测试 CLI、ego lite 浏览器属于这一层；把稳定操作写成说明后，才可能成为 Skill。
- **Harness**：围绕模型搭建的上下文、规则、工具、测试和验证环境，不是某一个包。

## 文章中的公开 Skill

| 名称 | 作用与适用时机 | 本仓库源码 | 来源确认程度 |
| --- | --- | --- | --- |
| `think` | 需求还模糊时讨论目标、取舍与方案，产出可执行计划 | [tw93/waza：think](../sources/ai-coding-workflow/tw93-waza/skills/think/SKILL.md) | 文章点名 tw93，来源明确 |
| `grill-me` | 连续追问需求和设计，把影响实现的分歧问清楚 | [Matt Pocock：grill-me](../sources/ai-coding-workflow/mattpocock-skills/skills/productivity/grill-me/SKILL.md) | 与文中 `implement` 同属 Matt Pocock 技能组，匹配度高 |
| `grill-with-docs` | 追问的同时沉淀术语表与架构决策记录（ADR） | [Matt Pocock：grill-with-docs](../sources/ai-coding-workflow/mattpocock-skills/skills/engineering/grill-with-docs/SKILL.md) | 同上 |
| `implement` | 根据已有 Spec、Issue 或任务实现，并按其流程做测试与审查 | [Matt Pocock：implement](../sources/ai-coding-workflow/mattpocock-skills/skills/engineering/implement/SKILL.md) | 文章明确点名 Matt Pocock |
| `ponytail` | 压制过度设计，选择满足需求的最小完整改动 | [DietrichGebert：ponytail](../sources/ai-coding-workflow/dietrichgebert-ponytail/skills/ponytail/SKILL.md) | 名称和用途吻合；文章没有给作者或链接，**不能确认就是作者使用的版本** |
| `handoff` | 把已验证事实、未完成项与入口整理为下一会话的交接材料 | [Matt Pocock：handoff](../sources/ai-coding-workflow/mattpocock-skills/skills/productivity/handoff/SKILL.md) | 与前述技能组匹配；文章没有给精确链接 |
| `check` | 审查代码差异、PR 或发布准备情况 | [tw93/waza：check](../sources/ai-coding-workflow/tw93-waza/skills/check/SKILL.md) | **同名候选**；文章未注明其作者，不能确认版本 |
| Superpowers | 一套覆盖设计、计划、TDD、调试、评审、验证与工作树的流程 Skill | [obra/superpowers 技能目录](../sources/ai-coding-workflow/obra-superpowers/skills) | 文章点名项目，来源明确 |

`grill-me`、`grill-with-docs` 和 `implement` 并非完全独立：前两者分别调用 [`grilling`](../sources/ai-coding-workflow/mattpocock-skills/skills/productivity/grilling/SKILL.md) 与 [`domain-modeling`](../sources/ai-coding-workflow/mattpocock-skills/skills/engineering/domain-modeling/SKILL.md)；`implement` 还引用 [`tdd`](../sources/ai-coding-workflow/mattpocock-skills/skills/engineering/tdd/SKILL.md) 和 [`code-review`](../sources/ai-coding-workflow/mattpocock-skills/skills/engineering/code-review/SKILL.md)。这些直接依赖已一并归档。

Matt Pocock 的几个入口 Skill 使用 `Call the Skill tool` 这样的调用方式，并且 `code-review` 预期有 Issue Tracker 设置。因此，**有源码不表示可直接在当前 Codex 环境里运行**；将来如需启用，应先核对当前 Agent 的 Skill 调用方式及上游安装说明，逐项验证。`implement` 的原文还要求在当前分支提交，使用前要看清它将执行的动作。

## 哪个先用

| 遇到的情况 | 可先试的 Skill 或做法 | 一句话提问示例 |
| --- | --- | --- |
| 需求方向不明、存在多种方案 | `think` | “先梳理目标、约束和验收标准，给出一个推荐方案；现在不要写代码。” |
| 需求材料互相矛盾、隐含假设多 | `grill-me`；术语与决策需要留档时用 `grill-with-docs` | “基于 PRD 和代码追问会影响实现的未决问题，每轮给出你的推荐答案。” |
| Spec 和验收标准已经明确 | `implement` 的方法 | “按这个 Spec 分小步实现，每步给出验证结果。” |
| AI 给出大批抽象层或无关扩展 | `ponytail` | “检查这份方案中的过度设计，保留满足验收标准的最小完整改动。” |
| MR 准备交付 | `check` 的审查思路 | “基于当前 diff 找出有证据支持的问题，并指出尚未验证的风险。” |
| 换 Agent、换会话或任务中断 | `handoff` | “把当前 commit、相关文件、验证命令、未完成项和待确认假设写成交接清单。” |
| 碰到复杂、跨模块、需要严密流程的任务 | 按需参考 Superpowers 的某个子 Skill | “参考它的计划和验证方法，为这个任务选必要步骤。” |

可以只借用上表的**方法**，无需先安装。以 iOS 开发为例：先明确交互和验收标准；改动时查看现有架构与调用方；在模拟器或真机走完整用户路径；对照日志、接口返回和产品预期检查结果；提交前审查 diff。是否使用某个 Skill，要看它能否减少当下任务的遗漏或返工。

## 不建议一口气全启用的原因

文章最有价值的判断是：**准确上下文、清楚的验收标准和真实环境验证，比叠加更多流程更重要。** Superpowers 的完整套件适合复杂任务，但流程较重，会增加上下文和时间成本；轻任务应只选必要的步骤。`think`、`grill-me` 和 `grill-with-docs` 都可能帮助前期澄清，同一问题不必重复跑三套。`check` 和 Matt Pocock 的 `code-review` 也有重叠。

Skill 能规定工作方法，却不能替代业务事实。文章里最值得复用的是：**把可操作的能力做成 MCP/CLI，把重复的操作流程写成 Skill，再让 Agent 用真实入口验证用户结果。** 特别是验收预期必须来自需求或业务契约，不能因为系统返回了某个结果，就认定这个结果正确。

## 本次没有可下载源码的部分

作者提到的内部端到端测试、查日志、查数据库、Trace 和测试环境 Skill 是基于其业务系统沉淀的能力，文章没有公开仓库，因此本次无法下载。它们也不能直接搬到个人 iOS 项目里；可以借鉴其结构，为自己的项目逐步整理“环境启动 → 测试数据 → 操作路径 → 结果检查 → 清理”的 SOP。

## 来源与更新

四个上游项目分别是 [tw93/waza](https://github.com/tw93/waza)、[mattpocock/skills](https://github.com/mattpocock/skills)、[DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) 和 [obra/superpowers](https://github.com/obra/superpowers)。本仓库保存的是固定提交的**部分目录或技能目录快照**，不是对上游项目的完整镜像。每份快照旁都保留了 MIT 许可证及提交号。更新时应先对比新旧内容、依赖和许可证，再替换快照并修改本页；不要把 `sources/` 当作 Agent 的安装目录。
