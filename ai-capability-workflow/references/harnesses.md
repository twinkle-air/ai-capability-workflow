# Harness 适配与验证

本文件说明如何把同一个 `ai-capability-workflow/` 文件夹交给不同运行环境。核心流程始终是 [SKILL.md](../SKILL.md) 的五步；平台只负责发现、读取文件和提供工具。以下路径与界面依据 2026-09-18 可查到的官方资料，实际安装前须核对目标版本。

## 通用要求

安装时复制**整个** `ai-capability-workflow/` 文件夹，保留 `SKILL.md`、`references/` 和 `templates/` 的相对位置。使用者在目标 harness 中检查四件事：技能是否被发现；能否读到模板；收到开发请求时是否先列任务清单并等待明确确认；确认后能否实际运行样本并保留结果。仅能读取 Markdown、但无法调用工具的 harness，可执行研究和规划；构建与测试须由具备相应工具权限的环境完成。

不要把某个 harness 的默认权限、联网能力或确认 UI 当作其他 harness 也具备的能力。安装成功只证明文件可加载，行为通过要靠实际任务样本验证。

## 已查证的接入方式

| Harness | 放置或导入方式 | 发现后如何核验 | 官方资料 |
| --- | --- | --- | --- |
| Codex | 项目 `.agents/skills/ai-capability-workflow/`，或用户级 `~/.agents/skills/ai-capability-workflow/` | 在技能选择器中找到名称，发出示例开发请求 | [OpenAI 文档](https://learn.chatgpt.com/docs/build-skills) |
| Claude Code | 项目 `.claude/skills/ai-capability-workflow/`，或个人 `~/.claude/skills/ai-capability-workflow/` | 在技能列表中找到，尝试以名称调用 | [Claude Code 文档](https://code.claude.com/docs/en/skills) |
| Gemini CLI | 项目 `.gemini/skills/ai-capability-workflow/` 或 `.agents/skills/ai-capability-workflow/`；也可用户级安装或链接 | `/skills list`，修改后 `/skills reload`；注意工作区信任与技能激活确认 | [Gemini CLI 文档](https://geminicli.com/docs/cli/using-agent-skills/) |
| ZCode Agent | 用户级 `~/.zcode/skills/ai-capability-workflow/`；也可在“设置 → 技能”导入外部 Skill | 刷新技能列表，确认启用，再用 `$ai-capability-workflow` 调用 | [ZCode 文档](https://zcode.z.ai/cn/docs/skill) |
| DeepSeek Harness | 启用技能相关插件的配置中，项目 `.dsh/skills/ai-capability-workflow/` 或 `.agents/skills/ai-capability-workflow/`；也可配置自定义根目录 | 检查会话技能目录及 `skill` 加载工具；仅放文件但未启用 provider/consumer 时不算接入 | [技能子系统](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/skills.md)、[插件说明](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/skill/README.md) |
| WorkBuddy | 在“技能”页通过“上传技能”导入本地技能包；开放平台发布可提交包含技能文件夹的 zip 包 | 确认出现在“已安装”且已启用，再用示例请求测试 | [WorkBuddy 使用文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market)、[开放平台格式](https://open.workbuddy.cn/docs/skill) |
| Cursor | 项目 `.cursor/skills/ai-capability-workflow/` 或 `.agents/skills/ai-capability-workflow/`；用户级也有对应目录 | 检查 Agent 能发现此 Skill、读取模板并遵守确认关口 | [Cursor Agent Skills 文档](https://prod.cursor.com/docs/skills) |

不直接识别 Agent Skills 的环境，可用以下项目指令作为**适配示例**，但须把技能包放在项目可读的位置，按实际路径改写：

```md
仅当用户要求创建、修改、测试或维护 AI Skill / Agent 的运行能力或配置时，读取 ai-capability-workflow/SKILL.md，遵循其中工作流；按需读取同目录的 references/ 与 templates/。仅修改面向读者的文档、仓库元数据或仅推送、上传、上架、发表、发布已有成品时不触发。提交详细任务清单并获得用户明确确认前，不开始构建或样本执行测试。仅测试任务跳过构建，保持待测对象原状，交付测试报告；修复必须在已确认的修改范围内。
```

其他 harness 也可将相同指令放进其项目级上下文文件或启动提示中。若不支持按需读取文件，应把核心规则作为项目指令，并将模板显式作为附件提供；不要因此声称已完成原生 Skill 安装。

WorkBuddy **开放平台发布**另要求 `description_zh`、`description_en`、`version`、`author` 等字段。发布者须按开放平台当时的规范补齐自己的真实作者信息，重新打包并实测解析；本仓库不代填作者身份。本地上传与开放平台发布是不同路径，不能因本地上传成功就声称开放平台审核通过。

## 描述摘要长度

2026-10-04 核对 [ZCode 官方说明](https://zcode.z.ai/cn/docs/skill)：技能元数据注入上下文时，单条描述摘要最多 250 字符，完整 description 的格式上限则为 1024 字符。两者不同。为使触发与排除条件完整进入摘要，本包将 description 控制在 250 字符以内，流程细节留在正文。这是按官方限制做的长度检查，不代表已在 ZCode 完成自动触发行为测试。

## 兼容性判定

分别记录三层结果：

1. **结构：** `SKILL.md` 元数据与引用文件完整。
2. **加载：** 目标 harness 能发现并读取技能及模板。
3. **行为：** 对同一示例请求，先研究和列清单，等待用户确认；确认后完成样本测试和清单复核。

未安装或无法访问的 harness，只能记“官方文档支持该接入方式，未在本机实测”。不得把结构检查记作加载或行为测试通过。

