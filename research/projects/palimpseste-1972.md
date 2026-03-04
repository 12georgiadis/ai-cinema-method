# *Palimpseste mémoriel / TNR 1972* — Ongoing

**Type**: Research project / visual series
**Subject**: The popular uprisings of May 1972 in Tananarive (Antananarivo), Madagascar
**Method**: LoRA fine-tuning on family photographs for historical reconstruction

---

## Context

In May 1972, Tananarive was shaken by a popular uprising — student demonstrations, general strikes, government crackdowns. The events left deep marks on the country's history, but the photographic archive is sparse and scattered. The colonial and postcolonial gaze dominates what little official image record exists.

This project starts from a different archive: family photographs. Images taken by ordinary people, for private memory, in and around the events. Not press photography. Not official documentation. The images families kept of their streets, their neighborhoods, their lives — in which history is present as atmosphere rather than document.

The question: can a LoRA trained on this private archive reconstruct the visual texture of these events? Can the model learn enough from family photographs to generate the images that were never taken — or were taken and lost?

---

## Method

### Dataset

- Family photographs from the maternal side (Madagascar, 1970s)
- Images spanning: street scenes, public spaces, domestic interiors, events — the specific geographic and social world of Tananarive in that period
- 100–300 selected images, cleaned and prepared for training

The photographs are not images *of* the events. They are images *from* the same world, the same bodies, the same visual texture. The model trains on the period's light, clothing, architecture, the quality of the photographic medium itself.

### Training

LoRA trained on SDXL base. Trigger tokens anchor the model to the specific visual register of 1970s Tananarive. The model learns:
- The grain and color rendering of period photography
- The architectural and street texture of the city
- The faces and bodies of that community
- The specific light and atmosphere

### Generation

With the fine-tuned model, scenes from the uprising are reconstructed: demonstrations, fires, confrontations, the physical experience of streets under pressure. Prompted from oral history — the mother's memory of specific events, described in words — the model translates verbal memory into visual form.

The results are neither documentary photographs nor illustrations. They're something between: images that feel like they could have been taken, distilled from a photographic world that actually existed, reconstructed from the texture of surviving memory.

---

## What this does and doesn't claim

These images are not historical evidence. They don't depict events that were photographed. They are *reconstructions from memory* — in the oldest sense: images that emerge from the gap between what was lived and what was kept.

The LoRA's "knowledge" is statistical generalization from a family archive. The resulting images carry the grain of that archive — its era, its geography, its private particularity — but they are generated, not found. The distinction matters and is not hidden.

This is post-documentary in the fullest sense: it documents not events but the act of remembering them.

---

## Outputs (partial)

Generated visual series includes:
- *TNR 1972 — Incendie*, from mother's memory of fires during the uprising
- *TNR 1972 — Manifestation*, street demonstration reconstructed from oral description
- *TNR 1972 — Palais Royal / Stade Mahamasina*, key sites of the events
- *TNR — 1970s, après mémoire maternelle* — scenes reconstructed from maternal memory, more atmospheric than event-specific

---

## Tools referenced

- LoRA fine-tuning (see [Custom Model Fine-Tuning](../methods/lora-custom-training.md))
- SDXL base model
- ComfyUI — generation pipeline
- Oral history as prompt source
