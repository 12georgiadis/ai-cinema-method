# Ciclic Residency — Vendôme, 2024

**Type**: R&D residency
**Host**: Ciclic Animation, Vendôme
**Period**: June–September 2024
**Collaborator**: Guillaume Menguy (technical and creative)
**Project**: *Goldberg Variations* (formerly *Deepfake*, *Madotsuki the Dreamer*)

---

## Context

The Ciclic Animation residency was a dedicated R&D phase for *Goldberg Variations* — a hybrid animation feature about Joshua Ryne Goldberg. The residency's mandate: develop a complete AI-cinema pipeline from capture to generation to real-time performance, using exclusively open-source tools.

The research ran in parallel with preproduction. The Florida filming mission (interviews with Joshua, location documentation) was prepared and shaped by the technical methodologies developed at Vendôme.

---

## Research axes

### 1. Volumetric capture and Gaussian Splatting

Complete methodology developed for 3DGS capture of narrative locations. See [Spatial Reconstruction](../methods/spatial-reconstruction.md).

The protocol covers: capture planning (trajectories, angle coverage, exposure consistency), data acquisition, processing (Colmap → 3DGS training), and integration into Unreal Engine 5 via the Akiya Research plugin.

### 2. Low-cost motion capture

Markerless body capture using standard webcams and open-source pose estimation (Mediapipe / similar). No specialized suit, no marker infrastructure. Captures skeletal data from a filmed performer and applies it to Metahuman or Blender rig in real time.

Tested: body tracking, facial expression capture via iPhone LiveLink, lip-sync from audio input.

### 3. Blender → ComfyUI real-time pipeline

The major technical development of the residency. See [Blender → ComfyUI Real-Time](../methods/blender-comfyui-realtime.md).

A WebSocket bridge between Blender and ComfyUI streams live animation data (object transforms, skeleton state, camera parameters) into ComfyUI as structured conditioning. AI-generated frames update in near real-time as the animator works in 3D space.

### 4. LoRA training methodology

Complete protocol for training character and location LoRAs from datasets of 100–300 images. See [Custom Model Fine-Tuning](../methods/lora-custom-training.md).

Includes: dataset curation, automatic captioning with manual review, training parameter benchmarks across SDXL and Flux bases, quality evaluation protocol.

### 5. Krita → ComfyUI drawing pipeline

Krita (open-source painting software) integrated as a drawing surface that feeds directly into ComfyUI. The artist sketches or paints a rough visual; ComfyUI generates from it as an img2img source. Closes the gap between hand drawing and AI generation without switching applications.

### 6. Interface comparison and convergence

Systematic testing of generation interfaces: Automatic1111, Fooocus, Forge, SwarmUI, ComfyUI. Final configuration: Fooocus for rapid concept iteration, ComfyUI for controlled production pipeline.

Flux models tested extensively as successors to SDXL — higher baseline coherence, different control behavior.

### 7. Audio synthesis and voice research

Exploration of voice synthesis and vocal cloning in the context of the Goldberg project. ElevenLabs voice cloning tested for character voice construction. Ethical framing developed for this use within a declared artistic work.

### 8. LLM-augmented writing

Claude, local Ollama (Mistral, Llama) trained on the screenplay and artistic intentions to produce context-aware writing assistants. Models fine-tuned on the project's voice for consistency in dialogue and visual description.

### 9. Real-time performance and generative editing

Research toward a real-time cinematographic performance system: a virtual editing suite where all film elements — space, characters, camera, style — can be generated and modified live, making post-production a performative act.

Live Portrait lipsync tested extensively: static photograph → driven performance from audio. A photograph of Joshua → speaks.

Video restyle research: transform the aesthetic of an existing sequence in real time using ControlNet + diffusion. Visual style as a dramaturgical parameter.

---

## Florida mission

The residency culminated with a three-week filming mission to Florida — Joshua's home state — with a team of two (Ismaël Joffroy Chandoutis + Bérengère Gimenez, camera assistant).

- 20+ hours of audio interviews recorded with Joshua Ryne Goldberg
- Systematic location documentation for 3DGS capture
- Reenactment sessions with Joshua filmed for LoRA dataset and motion reference
- Every session structured as dual-purpose: documentary capture + technical data collection

The Vendôme methodologies were applied directly in the field: capture protocols, data organization, preliminary processing.

---

## Theoretical framework

The residency included theoretical reflection published in the synthesis report:

- **AI as expressive medium** (not instrument): Deleuze/Guattari agencement as model for human-AI creative entanglement
- **Hyperreality** (Baudrillard): generated images that are neither true nor false, occupying a liminal space
- **Hauntology** (Mark Fisher): AI systems trained on the image-archive of the past, carrying a memory that is not theirs
- **Cyborg creativity** (Haraway): the augmented artist as hybrid entity, not replaced

---

## Outputs

- Complete 3DGS pipeline documentation
- Blender → ComfyUI WebSocket bridge (custom Blender plugin + ComfyUI custom nodes)
- LoRA training protocol and benchmark results
- 20+ hours Joshua interview material
- Location documentation for 3DGS reconstruction
- Synthesis report: *Rapport de synthèse — Résidence d'expérimentation cinématographique et intelligence artificielle* (Ciclic Animation, 2024)
