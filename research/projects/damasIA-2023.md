# *DamasIA* — Live Performance, 2023

**Type**: Live performance / interactive installation
**Event**: Festival "Et maintenant ?" — ARTE carte blanche à Alain Damasio
**Venue**: Gaîté Lyrique, Paris
**Date**: October 19, 2023
**Collaborator**: Thibaud Frere
**Producer**: ARTE

---

## Context

Alain Damasio is one of France's most significant living science fiction writers (*La Horde du Contrevent*, *Les Furtifs*). ARTE gave him carte blanche at the Gaîté Lyrique during their "Et maintenant ?" festival. The result was DamasIA — a live encounter between Damasio, his AI double, and an audience that wrote with and against it in real time.

Four months of development, two people (Ismaël Joffroy Chandoutis + Thibaud Frere), the entire technical system built from scratch.

---

## What was built

### Literary corpus model

A large language model trained on:
- Dozens of recorded interviews with Damasio
- The complete corpus of his published literary work
- His documented cultural references and literary tastes

The model could not only generate text in Damasio's voice and register — it could produce *original* writing that plausibly extended his style. It had learned not just his surface stylistics but his underlying conceptual and imagistic logic.

### Audio and video deepfake

Combined with LLM text generation: a synchronized audio deepfake of Damasio's voice and a real-time video avatar. The complete digital double could speak, generated text aloud, in Damasio's face and voice.

### Interactive writing workshop interface

The performance structure: audience members submitted writing prompts and short texts via smartphone in real time. DamasIA responded — generating new text, critiquing audience submissions from multiple angles simultaneously (funniest, most original, most unsettling, most romantic, most spiritual).

Simultaneously, the system generated live data visualizations representing the analysis of the full audience text corpus as it accumulated.

---

## Performance structure

```
Audience (smartphones) → submit text prompts
    ↓
DamasIA (LLM fine-tuned on Damasio corpus)
    ├── Generates new text (Damasio's style)
    ├── Critiques audience submissions (multi-angle analysis)
    └── Drives audio+video avatar (speaks aloud)
    ↓
Live datavisualization of corpus analysis
    ↓
Projected on stage — Damasio present, watching his double
```

The real Damasio was present in the room, watching his AI double generate, speak, write. A live confrontation between an author and his statistical ghost.

---

## What makes this methodologically distinct

Most LLM applications use foundation models with prompt engineering. DamasIA went further: actual fine-tuning on a specific person's voice, style, and conceptual universe — building a model that had internalized one writer deeply enough to extend his work.

The combination of literary corpus fine-tuning + voice cloning + real-time video avatar in a live performance context, with the subject physically present, had no direct precedent at the time.

---

## Relation to other work

The method developed here — fine-tuning a model on a living person's voice and corpus — directly informed the approach to Mihai Paunescu in [*Virus*](virus-2024.md) and Joshua Ryne Goldberg in [*Goldberg Variations*](vendome-residency-2024.md): deep model training on a specific individual as a way of constructing a presence that can inhabit the film.

---

## Tools referenced

- LLM fine-tuning — on literary corpus and interview recordings
- Voice cloning — Damasio's voice from recorded interviews
- Real-time video avatar — synchronized with LLM output
- Live datavisualization — real-time corpus analysis
- Smartphone audience interface — live prompt submission
