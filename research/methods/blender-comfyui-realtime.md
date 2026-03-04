# Blender → ComfyUI Real-Time Pipeline

**Function**: Drive diffusion image generation directly from live 3D animation data in Blender, enabling real-time preview of AI-generated frames as the animation plays.

**Developed at**: [Ciclic Residency, Vendôme 2024](../projects/vendome-residency-2024.md)

---

## What problem this solves

Generating images with AI usually means describing what you want through text prompts and reference images, then waiting. The feedback loop is slow and disconnected from spatial thinking. This pipeline collapses that gap: the filmmaker works in 3D space in Blender (positioning characters, camera, lighting) and sees AI-generated frames updating in near real-time.

Animation data — object positions, skeletal poses, camera parameters — flows continuously from Blender into ComfyUI as structured control signals. The AI generates not from a static description, but from a live spatial state.

---

## Architecture

```
Blender (animation / scene)
    ↓ WebSocket stream
    JSON: {transforms, skeleton_pose, camera_params, frame_number, metadata}
    ↓
ComfyUI custom nodes
    ├── Positional data → ControlNet conditioning (depth, pose, composition)
    ├── Camera params → framing / focal length hints
    └── Temporal metadata → frame consistency management
    ↓
Diffusion generation (SDXL or Flux base)
    ↓
Near real-time preview
```

### Blender plugin

A custom Blender plugin exposes the scene's animation state as structured JSON streams:
- Object transforms (position, rotation, scale) per frame
- Skeleton data (bone positions and rotations for rigged characters)
- Active camera parameters (focal length, position, orientation)
- Frame number and timing metadata

The stream is transmitted via WebSocket to a local ComfyUI instance.

### ComfyUI custom nodes

A set of custom nodes interprets the incoming JSON:
- Transform data is converted into ControlNet spatial conditioning (depth maps, composition guides)
- Pose data feeds into OpenPose-style ControlNet for character positioning
- Camera data informs prompt conditioning for framing and perspective

### Scheduling system

A dynamic scheduler in ComfyUI switches between models and conditioning weights based on animation state — allowing, for example, a more photorealistic model for close-ups and a looser model for wide environmental shots.

---

## Workflow in practice

1. Build rough animation in Blender (blocking, not final)
2. Stream → ComfyUI generates preview frames
3. Adjust timing, staging, camera in Blender
4. See results immediately without re-prompting
5. When animation is locked, render final batch at full resolution

This transforms the creative process: the artist thinks in space and movement, not in text descriptions.

---

## Limitations

- Latency: generation at ~2–4 seconds per frame on RTX 5090 at 768px. Not true real-time but workable for blocking
- Temporal coherence: generated frames are independent. Some flickering at transitions. Mitigated by AnimateDiff post-process or careful ControlNet strength tuning
- Complex scenes with many characters degrade pose tracking accuracy

---

## Tools referenced

- Blender (open source) — 3D animation, scene composition
- ComfyUI (open source) — diffusion UI with custom node system
- ControlNet — spatial conditioning for diffusion models
- WebSocket — real-time communication protocol
- SDXL / Flux — base diffusion models
