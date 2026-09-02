# Zer0Rin Skills

一组按领域组织、可单独安装的 Codex skills，用于复用角色一致性和多模态视频提示词工作流。

This repository contains reusable Codex skills organized by domain. Each skill keeps its own instructions, references, and optional agent metadata in one directory.

## Available Skills

### Character

| Skill | Purpose |
|---|---|
| [`character-four-view-builder`](skills/character/character-four-view-builder/) | 生成包含面部近景、正面、严格侧面和真实背面的角色四视图参考表。 |
| [`character-four-view-builder-v2`](skills/character/character-four-view-builder-v2/) | 在四视图流程上增加 Soft 3D game-CG 与 GPT Image 2 辅助模式，并约束细节和柔和光照。 |

### Video

| Skill | Purpose |
|---|---|
| [`minimax-h3-prompt-expander`](skills/video/minimax-h3-prompt-expander/) | 将文本、图片、首尾帧和多参考输入扩展为可执行的 MiniMax H3 视频提示词。 |

## Repository Structure

```text
skills/
├─ character/
│  ├─ character-four-view-builder/
│  └─ character-four-view-builder-v2/
└─ video/
   └─ minimax-h3-prompt-expander/
```

每个 skill 的入口是目录中的 `SKILL.md`。部分 skill 还包含 `references/` 或 `agents/openai.yaml`，应与主文件一起复制。

## Install

复制需要的完整 skill 目录到 Codex skills 目录。例如：

```bash
cp -R skills/character/character-four-view-builder ~/.codex/skills/
```

重新启动 Codex，使其发现新安装的 skill。

## Use

在对话中直接提到 skill 名称，或提出与其描述匹配的任务。例如：

```text
使用 character-four-view-builder，为这个角色建立可复用的四视图参考表。
```

Codex 会先读取对应的 `SKILL.md`，再按其中的流程执行。

## Boundaries

- 本仓库提供工作流说明，不包含模型额度、第三方 API Key 或生成服务；
- 图像和视频结果仍取决于所使用的模型、参考素材与服务限制；
- 安装时复制完整目录，不要只复制 `SKILL.md`；
- 各 skill 可独立更新，不要求一次安装整个仓库。
