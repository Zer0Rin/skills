---
name: character-four-view-builder
description: Use when a user asks to build a character four-view, quad-view character sheet, turn-around sheet, or identity-consistent face/front/side/back reference from an image or written character design.
---

# 人物四视图建设

## 目标

把单个人物参考或文字设定整理成一张身份统一的生产用角色板。固定板式为：**面部近景、正面全身、侧面全身、背面全身**。不要用四分之三视角替换面部近景。

## 输入处理

- 有图片时先读取图片，以可见身份、发型、服装、体型、鞋履、装备和材质为事实；文字只补充图片不可见的信息。
- 多张图片时先标明各自职责：身份、服装或道具。冲突会改变角色时才询问用户。
- 只有文字时，先形成简短的身份锁定清单，再写生成提示词。

## 四格契约

| 顺序 | 画面 | 必须展示 |
|---|---|---|
| 1 | 面部近景 | 五官、发型前侧、关键识别特征；不变成半身像 |
| 2 | 正面全身 | 从头到脚、自然中性站姿、服装正面结构 |
| 3 | 侧面全身 | 严格侧面、从头到脚、轮廓与装备挂载关系 |
| 4 | 背面全身 | 真正背面、不回头、发型与服装背部结构 |

四格必须是同一角色、同一年龄、同一发型、同一套服装、同一鞋履与装备；统一比例、地面线、棚拍光和纯净浅色背景。除用户明确要求外，不加入文字标签、场景、动作、边框装饰或额外角色。

## 提示词编译

先写身份锁，再写板式：

1. 一句话锁定人物身份与不可变特征。
2. 说明将参考人物转换为 character sheet。
3. 按固定顺序列出四格。
4. 要求全身格完整、不裁头脚、无遮挡、无强透视。
5. 要求四格服装缝线、材质、配饰位置和身体比例一致。
6. 最后写背景、光线和排除项。

编辑已有图时优先使用短而明确的动作句：

```text
Convert the character in the reference image into one clean character sheet with four ordered views: a face close-up, a front full-body view, a strict side full-body view, and a true back full-body view. Preserve the same identity, age, hairstyle, body proportions, clothing, footwear, materials, accessories, and equipment in every view. Keep all full-body views visible from head to toe in neutral poses, aligned on one ground line, with even studio lighting and a plain light background. No extra character, no three-quarter substitute, no turned-back face, no cropped feet, no scene, no text, no watermark.
```

把用户的稳定特征插入第一句；不要为了“丰富”而改造角色设计。

## 交付

返回：角色身份锁、最终生成提示词、简短排除项。若用户要求直接生成图片，再调用可用图像生成/编辑工具；只有提示词请求时不要擅自生成。

需要复现原始 ComfyUI 工作流参数时，读取 [references/workflow-extraction.md](references/workflow-extraction.md)。

## 常见错误

- 四个全身角度，遗漏面部近景。
- 侧面变成四分之三，背面角色回头。
- 正背面换装、武器换边、鞋履或发型漂移。
- 为角色板加入剧情背景、电影光或动态姿势。
- 参考图已给出外观，却用冗长重述覆盖原身份。
