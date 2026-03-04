# *Nemo* — Biennale Nemo, 2023

**Type**: Physical installation
**Event**: Biennale Nemo, Paris, September 2023
**Subject**: Joshua Ryne Goldberg

---

## Context

Joshua Ryne Goldberg is an American internet figure who, between ages 10 and 20, inhabited dozens of contradictory online identities — white supremacist, feminist, ISIS recruiter, progressive activist — before being arrested in 2015 in a federal sting operation for plotting a fictitious terrorist attack in Kansas City. He was later diagnosed with autism spectrum disorder and committed.

The Nemo installation was a stage in the development of *Madotsuki the Dreamer*, a feature film project structured around Joshua's story. The installation materialized the fragmentary, contradictory nature of his digital existence as a physical space — panels of AI-generated images arranged as an environment to be traversed.

---

## Narrative structure

The installation was organized in six acts:
1. FBI agent's point of view entering an investigation
2. Joshua's online worlds: forums, Second Life, 4chan
3. The Curtis Culwell Centre attack in Garland, Texas (which Joshua orchestrated from Florida via online radicalization)
4. SWAT arrest at Joshua's home
5. GTA V reconstruction of the attack scene
6. Prison journal fragments

---

## Image production workflow

### Method 1: ControlNet from Blender scenes

This was an early production use of ControlNet — mid-2023, shortly after the technique became publicly available.

3D scenes were built in Blender representing the key environments of Joshua's story: his suburban Florida bedroom, the IRC chatrooms rendered as physical spaces, the attack location reconstructed from news photographs. Depth passes and edge passes from these Blender renders were extracted and used as ControlNet conditioning to guide Stable Diffusion generation.

This allowed precise control over composition and spatial structure while producing images in varied visual registers — photorealistic, painterly, graphic — without manually composing each image.

### Method 2: Midjourney + Magnific

For panels requiring higher image quality or more abstract visual treatment, Midjourney was used for generation and Magnific for upscaling. Magnific's diffusion-guided upscale added detail and surface texture appropriate for large-format physical output.

---

## Physical production

Images were produced at final print resolution (150dpi, 80×80cm panels) and applied as stickers to the installation panels. The material choice — sticker on panel rather than traditional print — was deliberate: reproducible, cheap, adhesive to surfaces, associated with internet culture and urban posting.

---

## Tools used

| Function | Tool |
|---|---|
| 3D scene composition | Blender |
| Spatial image conditioning | ControlNet (SD 1.5, 2023) |
| Image generation | Stable Diffusion (A1111 / Automatic1111) |
| Alternative generation | Midjourney |
| High-resolution output | Magnific AI |
| Physical installation | Large-format sticker print |

---

## Notes on timing

This work was produced when ControlNet was a few months old. There were few reference uses in production contexts. The pipeline described here had no documentation to follow — it was developed through direct experimentation with the tools in their first public versions.
