# *Virus* — Feature Documentary, 2024—

**Type**: Feature documentary (in production)
**Subject**: Mihai Ionut Paunescu — Romanian hacker, arrested in Bogotá 2012, extradited to the United States
**Filming**: September 2024

---

## Context

Mihai Ionut Paunescu ("Virus") ran one of the world's largest botnets from Romania. Arrested in Bogotá in 2012, he spent years in legal limbo before extradition and trial in the US. *Virus* is a feature documentary that follows Mihai and reconstructs his world — the physical and the digital — using four distinct image regimes that contaminate each other throughout the film.

The film was shot on iPhone 15 Pro Max (4K ProRes Log) — a deliberate choice: the caméra-stylo as a pocket instrument, capable of sustained intimate presence.

---

## Four image regimes

### I. Present footage
Real-time documentary capture. iPhone 15 Pro Max, 4K ProRes Log. Drone footage (sub-250g) for surveillance-perspective aerial shots.

### II. Archives
Internet archives (social media, news, forum screenshots), personal archives, court documents. Source material that is already mediated, already degraded, already at one remove from the event.

### III. 3D Gaussian Splatting
Spatial reconstruction of key locations — Mihai's home environments, operational spaces, the Bogotá context. See [Spatial Reconstruction](../methods/spatial-reconstruction.md). Collaboration with GraphDeco / Inria Sophia Antipolis and Shatamata Productions for processing.

### IV. AI generative sequences
The "liquid and floating" register — psychological states, digital space, imagined reconstructions. Not photorealism: a visual space between hyperrealism and abstract expressionism, where the world dematerializes and reconstitutes. See [Cinematic Still Image](../methods/sd-cinematic-image.md), [Latent Drift Animation](../methods/latent-drift-animation.md).

---

## Technical pipeline

### 3D production

```
Location → systematic photo capture
→ Colmap camera estimation
→ 3DGS training (GraphDeco / Inria)
→ Unreal Engine 5 (Akiya Research plugin)
→ Metahuman avatar (Metahuman Creator)
→ Markerless mocap (Dollars MoCap)
→ Facial capture (LiveLink iPhone)
→ Virtual camera operator (gamepad or iPhone)
→ Real-time rendered scene
```

### AI image production

**Still image**:
- ComfyUI + SDXL-based cinematic models (Photon, Chinhook, JuggernautXL)
- Custom LoRAs for locations and characters
- ControlNet conditioning from depth, edges, or pose references
- See [Custom Model Fine-Tuning](../methods/lora-custom-training.md) and [3D-Guided Generation](../methods/controlnet-3d-guided.md)

**Animation**:
- AnimateDiff for latent drift sequences (see [Latent Drift Animation](../methods/latent-drift-animation.md))
- RunwayML Gen-3 / Luma for archive animation and sequence extension
- CogVideoX (open source) + Topaz upscale for local generation

**Archive animation**:
- Image-to-video models animate archival photographs and internet documents
- Video extension creates "generational decay" — the image forgets itself
- See [Archive Animation](../methods/animation-archives.md)

### Production workflow

- Rushes: iPhone 4K ProRes Log → FCP
- FCP markers → Notion via CSV2Notion Neo + MarkersExtractor (sync production data)
- Strada (Michael Cioni) collaboration for rushes analysis
- Voice: 3 hours of Mihai's voice recorded → ElevenLabs for voice reconstruction
- Transcription: OpenAI Whisper

---

## Collaborators

- **Guillaume Menguy** — technical collaborator (3D, pipeline)
- **Shatamata Productions** — Gaussian Splatting processing
- **GraphDeco / Inria Sophia Antipolis** — 3DGS research collaboration
- **Simon Weber** — technical
- **Bérengère Gimenez** — camera assistant, Florida mission

---

## Note on sensitive methods

Identity transformation (FaceFusion, Live Portrait, Viggle, ACT-ONE) and voice cloning (ElevenLabs, Whisper) are used in this project with Mihai's knowledge and consent, within the ethical frame of a declared artistic documentary work. These methods are documented in the private repository.
