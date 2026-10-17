# 上游来源与致谢（NOTICE）

本仓的专家 Agent（提示词、领域策略、测试与版本锁）由 **MC-freshman 与 Codex（OpenAI Codex 命令行助手）协作完成**：
在多平台 AI 工作流架构的设计目标下，从 GitHub 上的开源 skill / agent 项目中**搜集、梳理、改写与重构**，
并以语义化版本目录、冻结字节、SHA256SUMS 校验与精确 tool-lock 的方式重新组织。

本仓不包含任何上游项目的逐字快照（vendored 副本统一存放在私有正本的 `references/upstream/` 中，未随公开导出发布）。
每个版本目录下的 `SOURCE.json` 记录了该版本参考过的来源、许可与逐文件 sha256 指针；下表为来源汇总。

## 上游来源汇总

| 来源 | 上游仓库 | 许可证 | 在本仓中的使用方式 |
|---|---|---|---|
| ECC（领域源目录） | https://github.com/affaan-m/ECC | MIT | 各领域专家的方法学与 `ecc/skills/` 内容，经领域边界重写为专家提示词、策略与测试 |
| 共享技能库（姊妹仓） | https://github.com/MC-freshman/ai-workflow-tool | Apache-2.0 | 专家 `tool-lock.json` 锁定的技能/工作流实体均位于 tool 仓；技能的上游来源见该仓 NOTICE |

快照基线：多数来源记录为 `snapshot-2026.08.31`；具体到每个版本的参考文件与 sha256 见各版本 `SOURCE.json`。

## 开源协作工具说明

- 本仓的结构设计、版本治理、发布流程与大量文档由作者与 **Codex CLI** 协作完成。
- 各专家的 `tool-lock.json` 精确锁定其调用的技能、能力包与工作流版本；Agent 本体不携带任何运行时状态、凭据或产物。
- 各运行平台（codex / dsh / workbuddy / zcode / doubao / qoder 等命令行 AI 客户端）的配置、运行环境与输出不在本仓内。

## 许可证

本仓原创与重构内容以 **Apache License 2.0** 发布（见 `LICENSE`）。
上游内容归各自作者所有，其许可证在 `SOURCE.json` 中逐文件标注；若本仓文件与上游许可声明存在冲突，以上游原许可为准。

若本仓某一来源的 URL 或许可信息已过时或存在错漏，欢迎提 issue 指正，我们会在后续版本中修正。
