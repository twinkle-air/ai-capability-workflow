# 验证记录（2026-09-18）

## 1.0.0 发布前测试

- 触发边界：当前 Codex CLI 隔离会话已加载本 Skill。合成的“创建发布说明核对 Skill”请求得到资料依据与 14 项待确认任务清单，并在生成成品前要求确认；通过。
- 非触发边界：同一隔离工作区收到“用两句话解释 AI Agent 是什么”后直接回答，没有输出任务清单；通过。
- 文件检查：`quick_validate.py` 通过；中英文 README 及技能包的本地引用可解析；压缩包包含完整技能、模板、样本和许可证。
- 全局安装：当前主机 `~/.agents/skills/ai-capability-workflow/` 已安装；`~/.codex/AGENTS.md` 的原有四条规则保留，并新增仅针对 Skill / Agent 开发的触发条件。安装文件与最终发布文件再做一次哈希比对。
- 范围：以上行为结果只针对当前 Codex CLI；WorkBuddy、ZCode、DeepSeek Harness 等环境仍须分别实测。此前一次 CLI 测试因网络中断失败，不能代表本次结果。

## 样本与范围

- 合成请求：[sample-request.md](ai-capability-workflow/assets/sample-request.md)。它检查清单确认、修改后再次确认，以及确认后构建、测试和复核。
- 当前会话真实流程：用户补充 WorkBuddy、ZCode、DeepSeek Harness 后，先收到更新后的任务清单；用户回复“确认”后才开始修改文件。这验证了本次流程的**人工确认关口**，并非其他 harness 的独立执行结果。

## 本地检查

| 项目 | 方法与结果 |
| --- | --- |
| Skill 结构 | Codex `skill-creator/scripts/quick_validate.py`：通过；`name`、`description` 与目录匹配 |
| 文件完整性 | 模板已移入 `ai-capability-workflow/templates/`，分享整个技能文件夹即可保留相对资源 |
| 本地链接 | 检查 README、VALIDATION.md 及技能包内 Markdown 的本地链接；全部可解析 |
| 分享压缩包 | `ai-capability-workflow.zip` 已生成，检查压缩包中含 `SKILL.md` 和任务清单模板，共 11 个条目 |
| Codex CLI 独立样本运行 | 已尝试从临时工作区加载技能并运行样本 A；CLI 无法连接 `api.openai.com`，模型未执行。结果：**受环境阻碍，未通过行为测试** |
| WorkBuddy / ZCode / DeepSeek Harness / Claude Code / Gemini CLI / Cursor | 本机未发现对应可执行程序或会话；只依据官方资料核对接入方式，**未实测加载与行为** |

## 已确认任务清单复核

| 项目 | 状态 | 证据或限制 |
| --- | --- | --- |
| T01 通用五步核心 | 完成 | `ai-capability-workflow/SKILL.md` |
| T02 完整分享包 | 完成 | `ai-capability-workflow/` 内含入口、参考、模板和样本 |
| T03 多 Harness 适配说明 | 完成 | `ai-capability-workflow/references/harnesses.md`，逐平台附官方来源 |
| T04 清单确认关口 | 完成 | SKILL.md 第 1 阶段；本次会话实际等待用户确认后才构建 |
| T05 同一样本的跨环境行为验证 | 未完成 | 已制作样本；Codex CLI 因网络不可用未执行模型；其他 harness 本机不可用 |
| T06 复核与交付文件 | 完成，但交付声明须保留 T05 限制 | README、技能包、本记录 |

## 使用者复验

在目标 harness 按 [harnesses.md](ai-capability-workflow/references/harnesses.md) 安装完整技能包，然后依次发送样本 A、B、C。分别记录技能发现、模板读取、用户确认前是否暂停、确认后样本执行与复核结果。仅当目标 harness 实际通过，才能把该平台从“未实测”改为“行为通过”。WorkBuddy 开放平台发布还须由发布者填入真实作者信息并完成该平台解析检查。
