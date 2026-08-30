# 原始工作流提取记录

来源：`▶▷MiniMaxH3辅助四视图生成流-k2.json`。

## 可复用事实

- `LoadImage` 节点标题为 `Body Reference`，说明该流程以一张人物图作为主参考。
- 输入先以 `ImageResizeKJv2` 调整为 `1024 × 1536`。
- 输出 latent 为横向 `1536 × 1024`，适合并排角色板。
- `Krea2EditGroundedEncode` 的核心提示词为：

```text
Convert the character in the image to a Character Sheet showing a face close-up, front full body, side full body and back full body views
```

- 工作流使用 `Krea2-四视图QuadView_krea2_v1.safetensors` LoRA，强度 1。这是原工作流实现参数，不是 skill 对其他生图模型的通用强制参数。

## 提取后的边界

真正可迁移的能力是固定四格语义、人物一致性和干净角色板约束。Krea2 模型名、LoRA、采样器与分辨率仅在用户要求复现这份 ComfyUI 流程时使用。
