# Custom Model Fine-Tuning (LoRA)

**Function**: Train location- or character-specific image models from small datasets, making a base diffusion model capable of generating images with specific visual properties it would otherwise miss.

**Used in**: [*Virus*](../projects/virus-2024.md), [Ciclic Residency](../projects/vendome-residency-2024.md)

---

## What problem this solves

Base diffusion models know the world in statistical generalities. They can generate "a prison corridor" but not this specific corridor, with its particular light, its specific architectural texture, its weight in the narrative. LoRA fine-tuning closes that gap: train on a few hundred images of the actual location (or person), and the model gains specific knowledge of it.

This is also the method for character consistency — generating a specific face or body across many varied images without it drifting into generic types.

---

## Method: Low-Rank Adaptation (LoRA)

LoRA (Low-Rank Adaptation) produces compact fine-tuned models (~50–300MB) by training small weight adjustments grafted onto a base model. The base model's general knowledge remains intact; the LoRA adds a specific vocabulary on top of it.

A location LoRA lets you say "the Bogotá jail corridor" and mean it precisely. A character LoRA ensures that "Joshua, 19, in his bedroom" generates the same face, the same body type, across 100 different frames.

### Dataset preparation

**For locations**:
- 100–300 photographs of the location
- Systematic coverage: all angles, distances, light conditions
- Avoid identifiable faces if the location is to be publicly released
- Consistent trigger word across all captions: e.g., `BCR_corridor, interior, prison, rough concrete`

**For characters**:
- 50–200 images of the subject's face and body
- Full facial coverage: frontal, 3/4, profile, various expressions
- Body in varied poses and clothes
- Automatic pre-annotation then manual review
- One trigger token per subject: e.g., `JRSG_person`

### Training parameters (reference)

- Base model: SDXL or Flux (depending on target output style)
- Network rank: 32–64 for locations, 16–32 for faces
- Learning rate: 1e-4 with cosine schedule
- Steps: 1000–3000 (location), 500–1500 (face)
- Hardware: RTX 5090 32GB — training time ~30min to 4h

### Quality evaluation

After training, test with a fixed evaluation set of prompts:
- Neutral framing, various lighting conditions
- Verify the LoRA activates correctly on trigger words
- Check for mode collapse (generation converging to a single output)

---

## Stacking multiple LoRAs

Multiple LoRAs can be combined at inference: `[location_LoRA] + [character_LoRA] + [style_LoRA]`, each with its own weight (0.0–1.5). This allows generating a specific character, in a specific location, in a specific visual register — from three small models rather than one massive fine-tune.

---

## Ethical framing

Character LoRAs trained on real persons require explicit consent and careful scoping of use. In *Virus*, the LoRA of Mihai Paunescu was trained with his knowledge, used exclusively for the film's artistic sequences, and is not released.

---

## Tools referenced

- ComfyUI (open source) — training and inference UI
- kohya_ss / sd-scripts — LoRA training scripts
- SDXL / Flux — base models
- Automatic captioning: JoyCaption, BLIP2
