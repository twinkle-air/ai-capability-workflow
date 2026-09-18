# AI Skill / Agent 开发工作流

**只用于 AI Skill / Agent 的创建、修改、测试与维护。**普通编程、资料检索、写作或介绍 AI Agent 原理等任务不调用本工作流。每个适用项目必须先研究并把详细任务清单交给用户确认，确认后才能构建。用户可修改清单；修改范围或验收标准时重新确认。

[English README](README.en.md)

## 五步流程

| 步骤 | 必须完成的工作 | 阶段产物/关口 |
| --- | --- | --- |
| 1. 研究与确认 | 查找相关论文、标准、官方文档和一手资料；核验来源，补足需求，列出可验收任务 | 来源记录与任务清单；**用户确认后才能进入第 2 步** |
| 2. 构建 | 按已确认清单制作 Skill / Agent；只采用权威、可追溯且适用于任务的数据 | 源文件、配置、资源；代码编译或静态检查结果 |
| 3. 样本测试 | 创建或合法获取样本，投入成品实际运行；有问题立即修复并重测 | 样本来源、测试输入、实际输出、修复记录 |
| 4. 清单复核 | 测试通过后逐项核对清单和证据 | 必需项全部完成、关键测试通过，才能提交 |
| 5. 交付 | 整理可复用成品、源文件和说明 | 可用 Skill / Agent、源文件、使用说明、来源与测试记录 |

详细操作规则见 [ai-capability-workflow/SKILL.md](ai-capability-workflow/SKILL.md)。尽量全面地检索指覆盖会影响设计的关键证据，保留检索范围和空缺记录；不能宣称查遍所有文献。资料取舍规则见 [research.md](ai-capability-workflow/references/research.md)。整个 `ai-capability-workflow/` 是可独立复制的 Skill 包，符合 [Agent Skills 结构规范](https://agentskills.io/specification)的基本格式；行为是否兼容仍需在目标环境实测。

## 每个新项目怎么开始

1. 复制 [项目简报](ai-capability-workflow/templates/项目简报.md)，填入用户原始要求和环境。
2. 研究并填写 [资料来源记录](ai-capability-workflow/templates/资料来源记录.md)。
3. 复制 [任务清单](ai-capability-workflow/templates/任务清单.md)，把具体任务、验收标准和来源列给用户确认。**未确认时暂停。**
4. 确认后构建，使用 [验证记录](ai-capability-workflow/templates/验证记录.md) 执行样本测试与复测。
5. 逐项复核清单，填写 [交付说明](ai-capability-workflow/templates/交付说明.md) 后交付。

若项目目标不适合 Skill 或 Agent，应在清单中说明更合适的实现方式，并由用户确认，不能自行改变用户要求。

## 分享与安装

共享整个仓库供阅读，或仅共享完整的 `ai-capability-workflow/` 文件夹（[压缩包](ai-capability-workflow.zip)）供安装。支持 Agent Skills 的 Codex、Claude Code、Gemini CLI、Cursor、ZCode Agent 和 DeepSeek Harness，各有发现目录；WorkBuddy 提供本地技能包上传入口。逐平台安装、检查步骤和官方文档见 [harnesses.md](ai-capability-workflow/references/harnesses.md)。没有原生 Skill 功能的 harness 可手动加载 `SKILL.md` 与随包模板，但应标明这种接入方式。WorkBuddy 开放平台发布另有必填元数据要求。

### Codex 用户级安装

将完整的 `ai-capability-workflow/` 文件夹复制到 `~/.agents/skills/`。为了让后续相关任务稳定触发，可在 `~/.codex/AGENTS.md` 保留原有内容并追加：

> 仅当用户要求创建、修改、测试或维护 AI Skill / Agent 时，读取并遵循用户级 `ai-capability-workflow` Skill；其他任务不要调用该工作流。

这作用于**当前主机的 Codex 环境**，不会自动安装到其他设备、云端会话或别人的账号。项目级指令和用户最新要求仍可能改变具体执行方式。安装后用 [正反例样本](ai-capability-workflow/assets/sample-request.md) 核对触发范围。

实际行为要在使用者的目标 harness 中测试。这里提供 [跨环境合成样本](ai-capability-workflow/assets/sample-request.md)，用于检查“未确认不构建”“改清单后重新确认”“确认后实际测试再交付”。本次检查结果见 [验证记录](VALIDATION.md)。各平台能力与版本会变化，不能因为目录格式相同就宣称所有环境已实测通过。

本项目采用 [MIT 许可证](LICENSE)。分享前移除密钥、个人路径、私人数据和临时文件。对受许可或隐私限制的样本，交付可复现获取方式或脱敏替代样本。

## 设计依据

- [Anthropic：Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) 讨论工作流与 Agent 的区别、从简单方案开始，以及在执行中根据环境反馈调整。
- [Anthropic：Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) 讨论多步骤 Agent 的场景评估与轨迹记录。
- [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) 强调记录数据选择、实验设计与测试验证方法。

这些资料支持本工作流的设计取舍；具体项目仍须重新检索自身领域和目标平台的权威资料。

## 目录

```text
README.md
README.en.md
LICENSE
VALIDATION.md
ai-capability-workflow/SKILL.md
ai-capability-workflow/references/{research,skill,agent,harnesses}.md
ai-capability-workflow/templates/{项目简报,资料来源记录,任务清单,验证记录,交付说明}.md
ai-capability-workflow/assets/sample-request.md
```


