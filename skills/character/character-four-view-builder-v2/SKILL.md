---
name: character-four-view-builder-v2
description: Build production-ready character four-view sheets from reference images or written designs. Use for face-close-up, front, strict-side, and back character turnarounds when the user wants either soft idealized 3D game-CG rendering or GPT Image 2-assisted generation/editing with identity consistency and restrained detail.
---

# Character Four-View Builder v2

## Purpose

Create one clean production character sheet with four ordered panels: face close-up, front full body, strict side full body, and true back full body. Preserve the character's identity, age, hairstyle, body proportions, clothing, footwear, accessories, equipment, and material placement across all panels.

Do not replace or modify the original `character-four-view-builder` skill. This is the enhanced dual-mode version.

## Read the Reference First

- With image references, treat visible identity and design facts as authoritative. Use text only to add facts that are not visible.
- With multiple references, assign each one a single role: identity, clothing, equipment, or material. Ask one focused question only when sources conflict in a way that changes the character.
- With text only, make a short identity lock before writing the prompt. Do not invent decorative detail that is not required by the description.

## Fixed Four-Panel Contract

1. **Face close-up:** face, front/side hair shape, and key identifying features; never replace this with a half-body view.
2. **Front full body:** head-to-toe, neutral stance, clothing front construction, footwear, and equipment placement.
3. **Strict side full body:** head-to-toe, exact profile, silhouette, hair volume, and equipment attachment relationships; never use a three-quarter view.
4. **True back full body:** head-to-toe, back-facing without turning the head, hair and clothing back construction, and rear equipment placement.

Keep all panels on one ground line with matching scale, a clean light studio background, neutral poses, no cropping, no labels, no frames, no narrative scene, and no extra characters unless the user explicitly asks.

## Choose a Mode

- **Soft 3D rendering mode:** use when the user asks for soft idealized game-CG, Japanese game-like 3D, or PBR-style character references.
- **GPT Image 2-assisted mode:** use when the user asks to generate or edit with GPT Image 2, or when reference-image preservation is the main need.
- If the user names neither mode, select GPT Image 2-assisted mode for a GPT Image 2 task and Soft 3D rendering mode for an explicitly stylized 3D request. Ask one focused question only if neither intention is inferable.

## Shared Quality Contract

Apply these rules in both modes:

- Use global soft, diffused light. Avoid unnatural, dense clusters of highlight points.
- Avoid fragmented micro-detail and repeated fake high-frequency detail.
- Keep simple surfaces simple. Do not detail areas that have no design or material reason to carry detail.
- Favor clear silhouettes, readable construction, and restrained material separation over cinematic drama or decorative noise.

## Soft 3D Rendering Mode

Use soft idealized Japanese game-CG rendering: believable anatomy, clean tapered silhouettes, refined facial planes, softly rounded volumes, tactile but restrained PBR material separation, broad diffused area lighting, bounced fill, gentle contact shadows, controlled specular rolloff, and medium-low contrast. Read visible materials from the reference; describe only the materials that matter to identity or construction.

Append this mode block to the identity and four-panel contract:

```text
Soft idealized Japanese game-CG character sheet, broad diffused area lighting, soft global illumination, bounced fill, gentle contact shadows, controlled specular rolloff, medium-low contrast, restrained PBR material separation. Global soft lighting with no point-light hotspot clusters; no oily shine, harsh flash, blown highlights, sparkle pollution, cluttered micro-detail, repeated fake texture, text, logo, or watermark.
```

## GPT Image 2-Assisted Mode

For supplied images, preserve visible facts rather than rewriting every static feature. State what must remain unchanged, then describe the four-panel transformation. Keep the instruction concise and concrete: layout first, invariant identity second, panel details third, lighting and cleanliness last. For an edit, say `Convert the character in the reference image...`; for new generation, say `Create one clean character sheet...`.

Use this template, replacing bracketed content only with user-provided or safely inferred facts:

```text
[Create one clean character sheet / Convert the character in the reference image into one clean character sheet] with four ordered panels: a face close-up, a front full-body view, a strict side full-body view, and a true back full-body view. Preserve [identity lock] in every panel: the same age, hairstyle, face, body proportions, clothing, footwear, accessories, equipment, material placement, and left-right orientation. Keep every full-body panel visible from head to toe in neutral poses, aligned on one ground line, with a plain light studio background. Use global soft diffused lighting with natural broad highlights only; no dense pinpoint highlights, no fragmented over-detail, no repeated fake texture, and no unnecessary detail on simple surfaces. No extra character, no three-quarter substitute, no turned-back face, no cropped feet, no scene, no text, no logo, and no watermark.
```

## Deliverable

Return, in this order:

1. **Identity Lock** — only the invariant character facts.
2. **Mode** — Soft 3D rendering or GPT Image 2-assisted, with a one-sentence reason.
3. **Final Prompt** — a model-appropriate prompt compiled from the selected mode.
4. **Preservation / Exclusions** — a concise list of non-negotiable identity and layout constraints.

Do not generate an image unless the user explicitly asks to generate one. When generation is requested, use the available image-generation capability and pass the selected mode's compiled prompt.
