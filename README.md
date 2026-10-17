# AI Workflow · Agent Registry

一个多平台 AI 工作流架构的**专家 Agent 共享注册表**：35 个按领域划分的专家
（提示词、领域策略、测试集与精确版本锁），以语义化版本目录 + 冻结字节 + SHA256 校验的方式发布，
可被 Codex、Qoder、ZCode、WorkBuddy、豆包（Doubao）等任意命令行 AI 客户端按统一契约加载。

> 这些 Agent **由 Codex（OpenAI Codex CLI）与作者本人（MC-freshman）协作完成**：
> 从 GitHub 上的开源 skill / agent 项目中**搜集、筛选、改写与重构**，再按本架构的版本与锁定契约重新组织。
> 完整的上游来源与许可证清单见 [NOTICE.md](NOTICE.md)，每个版本的逐文件来源记录见其 `SOURCE.json`。

## 目录结构

```
agent/
├── registry.json                 # 全局注册表（schema 版本、全部专家指针）
├── _registry/                    # 注册表补充说明
├── <agent-id>/
│   ├── current.json              # 该专家的当前默认版本指针
│   └── versions/<semver>/
│       ├── manifest.json         # 专家清单（id/版本/依赖/profile/所需能力）
│       ├── agent.md              # 专家系统提示词（部分版本拆分为 prompt/ 与 policies/）
│       ├── policies/             # 领域策略、红线与边界
│       ├── tests/                # 该专家的验收测试
│       ├── tool-lock.json        # 精确锁定的技能/工作流/能力包版本（不可被平台默认覆盖）
│       ├── SOURCE.json           # 上游来源与逐文件溯源（sha256、许可）
│       └── SHA256SUMS            # 该版本全部文件的冻结校验和
└── docs/REGISTRY-README.md       # 注册表内部原始说明（保留结构溯源，路径为内部工作区路径）
```

**已发布版本只读、不可覆盖**：任何修改都必须新建语义化版本目录，并通过 `current.json` 切换默认指针。

## 专家清单（35）

| 领域 | 专家 |
|---|---|
| 软件工程 | software-architect、software-engineer、frontend-engineer、qa-engineer、devops-engineer、automation-engineer、framework-author |
| 数据与 AI | data-analyst、data-engineer、database-engineer、ml-engineer、llm-engineer、modeling-analyst |
| 数学建模 | math-modeling-programmer |
| 安全 | security-researcher，以及 mastermind 系列：mastermind-recon、mastermind-api-validation、mastermind-crypto-analysis、mastermind-js-analysis、mastermind-bug-bounty、mastermind-triage、mastermind-reporting |
| 游戏 | game-designer、game-builder |
| 内容与写作 | novel-writer、story-architect、content-strategist、paper-author |
| 文档与表达 | document-engineer、presentation-designer、spreadsheet-engineer、visualization-engineer |
| 产品与研究 | product-manager、research-analyst、ui-ux-designer |

每个专家的当前版本、显示名与能力声明以 `registry.json` 与各 `manifest.json` 为准。

## 版本与锁定机制

- 解析顺序：请求显式指定版本 → 平台本地默认 → 专家 `current.json`；执行前必须记录确切版本与来源。
- 专家内部的技能/工作流选择**必须**服从其 `tool-lock.json` 的精确版本，平台默认与显式参数都不能绕过。
- 一个专家可声明多个 profile（如某游戏引擎），但 profile 在执行前必须展开为精确的技能与工作流版本。
- 运行期状态（run、锁、产物、日志、凭据）属于加载它的平台，**本仓不存放任何运行时内容**。

## 与姊妹仓的关系

本仓与另外两个共享仓共同构成同构的三仓骨架：

| 仓库 | 职责 |
|---|---|
| **agent**（本仓） | 专家 Agent：提示词、领域策略、测试与版本锁 |
| [ai-workflow-tool](https://github.com/MC-freshman/ai-workflow-tool) | 技能（skill）、能力包（pack）与工作流（workflow）实体 |
| software 仓 | 外部软件配方与能力快照（暂未公开发布） |

## 快速开始

1. 阅读 `registry.json`，找到所需专家与当前版本。
2. 打开 `<agent-id>/versions/<semver>/manifest.json` 与 `agent.md`，了解其职责与能力需求。
3. 对照 `tool-lock.json`，到 tool 仓取对应版本的技能/工作流，确保版本一致。
4. 用 `SHA256SUMS` 校验文件字节，用 `SOURCE.json` 查看来源与许可。

## 许可证

[Apache License 2.0](LICENSE)。第三方与上游内容归各自作者所有，来源与许可见 [NOTICE.md](NOTICE.md) 与各 `SOURCE.json`。

## 说明

本仓为共享资源的**定义与发布面**，不含平台配置、密钥、运行时环境或任何项目输出；
仓库中出现的内部工作区路径（如 `E:\ai\...`）是开发期绝对路径，仅用于溯源，不影响在其他环境加载。
