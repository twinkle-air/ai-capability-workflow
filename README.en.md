# AI Skill / Agent Development Workflow

**Use this workflow only to create, modify, test, or maintain an AI skill or agent.** Do not invoke it for ordinary programming, research, writing, or questions about AI agents. For an applicable project, research authoritative sources first and present a detailed task checklist to the user. Build only after the user confirms the current checklist version.

[中文 README](README.md)

## Five stages

| Stage | Required work | Gate or evidence |
| --- | --- | --- |
| 1. Research and plan | Search relevant papers, standards, official documentation, and primary sources; assess provenance; expand requirements into a detailed checklist | Give the checklist and key sources to the user; **wait for explicit confirmation** |
| 2. Build | Implement the approved skill or agent using trustworthy, traceable information | Source files, configuration, resources, and code checks where applicable |
| 3. Sample test | Create or lawfully obtain a representative sample; run it through the result; fix and rerun failures | Inputs, actual outputs, provenance, and repair records |
| 4. Reconcile | Review every approved checklist item against evidence after sample tests pass | Required items complete before submission |
| 5. Deliver | Hand over the usable skill or agent and its source | Installation guide, usage instructions, source register, test record, limitations |

The executable instructions are in [SKILL.md](ai-capability-workflow/SKILL.md). The folder is a self-contained Agent Skills package; copy the **entire** folder so that `references/`, `templates/`, and `assets/` remain available. The source evaluation rules are in [research.md](ai-capability-workflow/references/research.md).

## Start a project

1. Copy the [project brief](ai-capability-workflow/templates/项目简报.md) and record the original request and environment.
2. Record searches and decisions in the [source register](ai-capability-workflow/templates/资料来源记录.md).
3. Present the [task checklist](ai-capability-workflow/templates/任务清单.md). **Stop until the user confirms it.**
4. Build, then run samples and record actual outcomes in the [validation record](ai-capability-workflow/templates/验证记录.md).
5. Reconcile the checklist and complete the [handoff sheet](ai-capability-workflow/templates/交付说明.md).

The templates themselves are currently in Chinese. Their field names may be translated for a project without changing the five stages or the confirmation gate.

## Install and share

Share this repository for documentation or the complete `ai-capability-workflow/` folder for installation. A [ZIP package](ai-capability-workflow.zip) is also included. See [harnesses.md](ai-capability-workflow/references/harnesses.md) for documented paths for Codex, Claude Code, Gemini CLI, Cursor, ZCode Agent, DeepSeek Harness, and WorkBuddy. A compatible directory format does **not** establish that behavior has passed testing in every harness; check the [validation record](VALIDATION.md).

### Codex user-level installation

Copy the full folder to `~/.agents/skills/ai-capability-workflow/`. To make relevant future tasks trigger it consistently, preserve any existing `~/.codex/AGENTS.md` instructions and append this conditional rule:

> Only when the user asks to create, modify, test, or maintain an AI skill or agent, load and follow the user-level `ai-capability-workflow` skill. Do not invoke this workflow for other tasks.

This applies to Codex on the **current host**. It does not automatically sync to other devices, cloud sessions, or other people's accounts. Test both matching and unrelated prompts from the [synthetic sample](ai-capability-workflow/assets/sample-request.md).

## Licensing and sources

The project is released under the [MIT License](LICENSE). Remove secrets, private data, personal paths, and temporary files before redistributing it. Follow the provenance and licensing terms of any samples used in downstream projects.

The workflow's design draws on [Anthropic's agent engineering guidance](https://www.anthropic.com/engineering/building-effective-agents), [Anthropic's agent evaluation guidance](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents), and the [NIST AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/). Each new development project still requires research into its own domain and target platform.
