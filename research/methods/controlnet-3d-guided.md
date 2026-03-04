# 3D-Guided Image Generation (ControlNet)

**Function**: Control the spatial composition, character poses, and depth structure of AI-generated images by feeding data extracted from 3D scenes or reference photographs.

**Used in**: [*Nemo*](../projects/nemo-biennale-2023.md), [*Virus*](../projects/virus-2024.md), [Ciclic Residency](../projects/vendome-residency-2024.md)

---

## What problem this solves

Diffusion models are stochastic. Left to text prompts alone, they tend toward their statistical mean: generic compositions, generic bodies, generic space. ControlNet adds a hard spatial constraint: the model must generate an image that matches a provided depth map, edge map, or pose skeleton. This turns prompt-based generation into something closer to directed photography.

The key insight is that the control signal doesn't have to come from a real photograph. It can come from a 3D render, a quick Blender sketch, a depth estimation of an existing frame. You're giving the model the skeleton of an image, then asking it to flesh it out in any visual register you choose.

---

## Method

### Control signal types

**Depth map**: Extract per-pixel depth from a reference image or 3D render. The model reproduces the spatial structure (foreground/background, volumes in space) while generating a new image in the target style. Used for environmental and architectural shots.

**Canny edges**: Extract contour lines from a reference. Less strict than depth — gives the model more creative latitude while preserving overall composition. Useful when you want the structure but not the spatial rigidity.

**OpenPose skeleton**: Detect keypoint skeletons from a reference image or 3D character animation. The model generates a new character in the same pose, with any desired face, body, clothing, and visual treatment. Used for character sequences.

**Normal maps**: Surface orientation data from 3D renders. More precise than depth for object surfaces. Used in architectural and object-heavy scenes.

### Workflow

1. Prepare control signal:
   - From photograph: run depth estimator (Depth Anything V2), edge detector, or pose estimator
   - From 3D: render depth pass or normal pass directly from Blender/UE5
2. Load into ComfyUI with ControlNet node
3. Set conditioning weight (0.3–1.0): lower = more creative freedom, higher = strict adherence
4. Generate against base model + LoRA stack

### Multi-ControlNet

Multiple control signals can run simultaneously with individual weights:
- Depth (0.7) + Pose (0.9) = preserved spatial structure and character posture, free color/texture/style
- Edge (0.4) + Style reference (0.6) = loose spatial guide with strong aesthetic direction

---

## In practice: Nemo installation (2023)

For the Joshua Goldberg installation at Biennale Nemo, ControlNet was used to generate images anchored to 3D scenes built in Blender. The scenes established the spatial structure of each panel — the virtual room, the surveillance angles, the VR worlds — and ControlNet ensured the generated images respected this structure while adopting the desired photographic and painterly qualities.

This was 2023: ControlNet had been public for only a few months. The technique was not yet widely used in production contexts.

---

## Tools referenced

- ControlNet (open source) — spatial conditioning add-on for Stable Diffusion
- Depth Anything V2 — monocular depth estimation
- OpenPose / DWPose — human pose estimation
- ComfyUI — workflow management
- Blender — 3D scene source for control signals
