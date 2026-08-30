---
name: minimax-h3-prompt-expander
description: Use when a user provides a short video idea, dialogue, image, first/last frames, or multiple reference assets and needs a MiniMax H3 prompt expanded, structured, translated, or adapted to Seedance 2.5-style video prompt logic.
---

# MiniMax H3 提示词扩写

## 目标

把简短意图编译成可执行的视频说明：主体与参考素材职责明确，动作能在时长内完成，镜头有起点和终点，对白与声音可实现。H3 与 Seedance 共用同一“镜头事实”，但最终格式分开编译，不混写两套标签。

## 先确定任务

| 素材 | 模式 | 编译重点 |
|---|---|---|
| 无图 | T2V | 补齐主体、场景、动作与镜头 |
| 一张起始图 | I2V | 少复述静态外观，重点写运动与保持项 |
| 首帧和尾帧 | FLF | 写连续过渡，尾帧是明确终点 |
| 多张图/视频/音频 | R2V | 先给每份素材分配唯一职责，再写保留与非转移项 |

优先使用用户给定时长；未给时默认 5 秒并明确标注。先判断对白和动作是否能在时长内完成，不能完成时压缩动作或提示用户缩短对白，不把多个故事节拍硬塞进一个短片。

## 扩写顺序

1. 锁定一个主要可见事件和结束状态。
2. 为每个参考素材建立角色：身份、服装、场景、动作、镜头、声音或风格，一份素材不要同时模糊承担所有职责。
3. 写主体的连续动作、衣发与环境的次级运动，以及不能漂移的身份/产品特征。
4. 只使用一个主要镜头运动，写清起始景别、运动方式和结束景别。
5. 用时间戳或短时间段安排动作与对白；角色名必须与参考编号绑定。
6. 对白保留原文和语言，H3 使用 `<d>[Chinese] 台词</d>` 等语言标签；不要擅自改写用户台词。
7. 分开写画内环境声、音效和画外音乐；用户没有要求音乐时写 `N/A`，不要自动添加史诗音乐。

## 两种输出表面

**MiniMax H3：** I2V/T2V/FLF 使用 `integrated_multimodal_description`；R2V 使用 `subject_definitions → summary → retention_analysis → detailed_description`；最后独立输出 `overall_soundscape` 与 `non_diegetic_music`。精确模板见 [references/h3-contracts.md](references/h3-contracts.md)。

**Seedance 2.5 风格：** 保留同一参考角色表、身份锁、时间结构、镜头终点、对白语言与声音设计，改用目标环境的 `@Image1` / `@Video1` 等引用，输出紧凑的自然语言拍摄说明，不携带 H3 的 section 名或 `<Subject 1>` 标签。

用户未指定目标时，默认交付 H3 完整结构，并附一段简短的 Seedance 可移植版；用户只要一个平台时只输出该平台格式。

## 交付契约

返回：模式与时长、参考素材角色表、最终提示词。只在存在真实矛盾时补一条风险说明。不要返回推理过程、模型参数、API 配置或泛化的“电影感/高质量”堆词。

## 常见错误

- 只把短句写长，没有建立素材职责与保留关系。
- 把参考图可见内容反复重述，导致身份漂移。
- 镜头动作过多，没有明确终点。
- 5 秒内塞入多段对白、多次转场和复杂动作。
- H3 section、Seedance `@` 引用和普通散文混在同一最终提示词。
- 添加用户未要求的旁白、字幕、音乐或新角色。
