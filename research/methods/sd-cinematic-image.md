# Cinematic Still Image Generation

**Function**: Generate photographic-register stills — concept art, narrative visualizations, set previsualization — using Stable Diffusion-based models fine-tuned on cinematic imagery.

**Used in**: [*Virus*](../projects/virus-2024.md), [*Nemo*](../projects/nemo-biennale-2023.md), [Ciclic Residency](../projects/vendome-residency-2024.md)

---

## What problem this solves

The "AI aesthetic" — oversaturated, hyper-detailed, uncanny — is a function of default models and default settings. Generating images that sit in the documentary, film-still, or photoreal register requires deliberate model selection, prompt construction, and parameter choices. The method below documents how to avoid the default and work toward images that could plausibly belong in a film.

---

## Model selection

Base models trained explicitly on cinematic and photographic datasets produce fundamentally different output from general-purpose models. The models below were selected and tested across the *Virus* and Ciclic productions:

**Photon** — trained on film photography datasets. Produces grain, exposure latitude, and color rendering consistent with analog-adjacent aesthetics. Strong for close portraiture and atmospheric stills.

**CinematicXL / JuggernautXL** — SDXL-based, large dataset emphasizing film production stills. Good balance of photorealism and dramatic lighting. Reliable for wide-register outputs.

**Flux** (2024 onward) — generation step forward in coherence and textural fidelity. Less controllable than SDXL but higher baseline quality. Being integrated progressively into the pipeline.

**Fooocus** — not a model but an interface that pre-bakes many quality-of-life defaults. Useful for rapid iteration during concept phases before moving to ComfyUI for final control.

---

## Prompt construction

The register of the image is set more by negative space in the prompt than by positive description. Avoid terms that activate the AI aesthetic:
- No: `highly detailed, masterpiece, trending on artstation, 8K`
- Yes: `35mm still, shallow depth of field, available light, documentary`

Frame the shot as a photographer would frame a photograph:
- Camera position and angle
- Light source and quality (window light, overcast, practical lamp)
- Subject relationship to frame
- Photographic texture reference (grain, softness)

---

## Parameter guidance

| Parameter | Typical range | Notes |
|---|---|---|
| Guidance scale (CFG) | 4–7 | Higher = prompt adherence but loses naturalness |
| Steps | 20–35 | More steps rarely improves; often hurts naturalness |
| Denoise (img2img) | 0.3–0.6 | Lower = stay closer to input; higher = diverge |
| Resolution | 1024×1024 or 832×1216 | Train-native for SDXL. Avoid extreme ratios |

---

## img2img for frame-level control

img2img is the more cinematically useful mode: provide a rough reference (a sketch, a location photo, a 3D render) and diffuse from it at a denoise strength that preserves the structure while transforming the visual register. This is how to go from a Blender preview to a film-quality still without losing the composition.

Denoise at 0.3–0.4: the output is close to the input, style-shifted.
Denoise at 0.6–0.7: significant transformation, structure roughly preserved.
Denoise at 0.8+: generation takes over, minimal relationship to input.

---

## Tools referenced

- ComfyUI — workflow interface
- Photon, JuggernautXL, Flux — base models
- Fooocus — rapid iteration interface
- Automatic1111 / Forge — alternative interfaces used in 2023
