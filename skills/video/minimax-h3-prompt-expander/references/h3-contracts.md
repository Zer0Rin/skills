# MiniMax H3 输出契约与工作流提取

来源：`▶▷MiniMaxH3-加速视频流整合.json`。

## 工作流事实

- `TE_H3_Prompt_Enhancer` 先接收简单提示词，再要求选择任务类型和视频时长。
- 原工作流注释顺序是：选择任务类型 → 填写与生成一致的时长 → 接出提示词 → 单独运行简短提示词以便调整。
- 工作流展示两类增强结果：单图/图生结构与多参考结构。
- 默认示例时长为 5 秒；这只是缺省值，不覆盖用户指定时长。

## T2V / I2V / FLF 模板

```text
integrated_multimodal_description:
[Shot 1] <主体和场景的必要信息>。<在给定时长内发生的连续动作>。<次级运动>。镜头从<起始景别>开始，<一个主要镜头运动>，最终停在<结束景别/视觉终点>。保持<身份、产品或首尾帧连续性>。

overall_soundscape:
<画内环境声、动作音效、对白；没有则写 N/A>

non_diegetic_music:
<画外音乐；用户未要求则写 N/A>
```

首尾帧模式只描述从第一帧到最后一帧的连续变化，不重新设计两个端点。

## R2V 多参考模板

```text
subject_definitions:
<Picture 1> 作为 <Subject 1> 的人物外观来源，保持<身份锁>。
<Picture 2> 作为 <Subject 2> 的人物外观来源，保持<身份锁>。
<Subject 1> 表示 Picture 1 中人物，在视频中的职责是<动作/对白>。
<Subject 2> 表示 Picture 2 中人物，在视频中的职责是<动作/对白>。

summary:
[reference generation] <一句话说明成片与参考素材关系>。

retention_analysis:
<Subject 1>（出现于 [Shot 1]）：fully_preserved - <必须保留的身份、服装或产品特征>。
<Subject 2>（出现于 [Shot 1]）：fully_preserved - <必须保留的身份、服装或产品特征>。
<Picture 1>（人物外观来源）：fully_preserved - <允许迁移与禁止漂移的内容>。
<Picture 2>（人物外观来源）：fully_preserved - <允许迁移与禁止漂移的内容>。

detailed_description:
<场景、光线与摄影机的连续设置>。
[Shot 1] At 00:00.000, <Subject 1> 与 <Subject 2> <可见动作>，<Subject 2> 说，<d>[Chinese] 用户原台词</d>，随后 <Subject 1> 回应，<d>[Chinese] 用户原台词</d>。<动作终点和背景运动>。

overall_soundscape:
<环境声、脚步、物件声、对白相对音量>

non_diegetic_music:
N/A
```

只声明实际提供的 Picture/Video/Audio；不要为不存在的素材机械添加“不适用”。若参考视频只负责动作或镜头，必须明确“不迁移人物身份、服装或场景”。

## Seedance 编译映射

| H3 内部事实 | Seedance 最终表面 |
|---|---|
| `<Picture 1>` / `<Subject 1>` | `@Image1` 及其角色职责 |
| `retention_analysis` | 自然语言 preservation / do-not-transfer 约束 |
| `[Shot 1] At 00:00.000` | 时长内的动作顺序或时间段 |
| `<d>[Chinese] ...</d>` | 明确说话者、语言和原文对白 |
| `overall_soundscape` | `Sound:` 或自然语言声音段 |
| `non_diegetic_music: N/A` | 明确无画外音乐，或省略音乐描述 |

映射的是事实，不是逐字段翻译。Seedance 最终提示词应读成紧凑的拍摄说明。
