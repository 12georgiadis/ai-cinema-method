# Image Upscaling

**Function**: Bring AI-generated images from generation resolution (512–1024px) to exhibition or cinema resolution (4K+) while preserving — or enhancing — photographic quality.

**Used in**: [*Nemo*](../projects/nemo-biennale-2023.md), [*Virus*](../projects/virus-2024.md)

---

## What problem this solves

Diffusion models generate at limited resolutions. Native generation at 2K+ is slow and quality degrades at sizes outside the model's training distribution. The standard workflow is: generate at 768–1024px, upscale. The upscaler must add information without inventing artifacts — or its artifacts must be useful (grain, texture, detail sharpening).

For physical installation (Nemo, sticker panels) and cinema projection, the jump from generation to output resolution is significant. Choosing the wrong upscaler introduces blurring, halos, or the plastic "AI sheen."

---

## Methods

### AI upscaling: Real-ESRGAN

Open-source, runs locally. Trained on perceptual quality — produces sharp edges and crisp detail. Default choice for single images going to 4× (e.g., 1024px → 4096px).

- Best for: photorealistic outputs, architectural and environmental stills
- Weakness: can over-sharpen faces, add artificial texture on smooth surfaces
- Models: `RealESRGAN_x4plus` for general use, `RealESRGAN_x4plus_anime_6B` for illustrated/flat styles

### Magnific AI

Commercial, cloud-based. Processes images with a diffusion-guided upscale that adds detail rather than just interpolating pixels. Produces results closer to "re-generation at higher resolution" than classical upscale.

- Used in *Nemo* for final sticker production. Generated images at 1024px → Magnific at 4× → 80×80cm physical print at 150dpi.
- Higher compute cost; best reserved for final outputs
- Tendency to add texture and grain — usually desirable for photographic register

### Topaz Gigapixel / Photo AI

Commercial desktop app. Strong on faces; handles compression artifacts well. Preferred for portrait images before print.

### Tile upscale via ComfyUI

For very large outputs (8K+), tile-based upscaling in ComfyUI processes the image in overlapping sections, running diffusion on each tile independently, then blending. Allows adding local detail at high resolution while respecting the global composition.

- Requires careful blending: edges between tiles can be visible if overlap is insufficient
- Best for: architecture, environmental scenes, any image where local detail matters everywhere

---

## Video upscaling

For AI-generated video sequences, Topaz Video AI provides the most reliable upscaling. Its temporal coherence mode reduces inter-frame flicker — important for footage that will be projected or viewed on large screens.

RIFE (optical flow frame interpolation) is applied before upscale to smooth from generation framerates (8–16fps) to exhibition framerates (24–25fps or slow-motion).

---

## Print production notes (Nemo)

Physical installation output (sticker panels, large format prints):
- Target: 150 dpi at final print size
- Minimum generation: 1024px square
- Workflow: generate → Real-ESRGAN 4× → Magnific 2× → export as TIFF 16-bit

---

## Tools referenced

- Real-ESRGAN (open source) — 4× AI upscale
- Magnific AI — diffusion-guided upscale (commercial)
- Topaz Gigapixel / Photo AI — portrait-specialized upscale
- Topaz Video AI — video upscale with temporal coherence
- ComfyUI tile upscale — tiled diffusion for very large outputs
- RIFE — frame interpolation
