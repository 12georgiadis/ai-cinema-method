# LLM Corpus Fine-Tuning for Living Subjects

**Function**: Fine-tune a large language model on a specific person's recorded speech, published writing, and documented thought — building a model that can generate text, voice, and presence in that person's register.

**Used in**: [*DamasIA*](../projects/damasIA-2023.md), [Ciclic Residency / *Goldberg Variations*](../projects/vendome-residency-2024.md)

---

## What problem this solves

Foundation LLMs know everyone and no one specifically. Fine-tuning on a person's actual corpus produces something qualitatively different: a model that has internalized a specific voice, a specific way of structuring thought, specific references and obsessions. The resulting model doesn't imitate — it extends.

In the context of documentary and post-documentary work, this has a precise use: constructing the presence of someone who cannot be present, or whose presence needs to be extended beyond what was recorded.

---

## Method

### Corpus preparation

**Audio/video interviews**:
- Collect all available recordings of the subject speaking (interviews, talks, recordings)
- Transcribe with Whisper (local, high-accuracy model)
- Clean transcripts: remove filler words, interviewer turns, transcription errors
- Result: clean text corpus of the subject's spoken language

**Written work** (if applicable):
- Published texts, books, articles, social media posts
- Annotated with context (formal register vs. informal, period, subject matter)

**Cultural references**:
- Document stated influences, references, aesthetic preferences
- Provides the model with the subject's intellectual territory, not just surface stylistics

### Fine-tuning

- Base model: a capable open-source LLM (Mistral, Llama, or similar) or API model with fine-tuning access
- Training on the cleaned corpus with appropriate instruction format
- Few-shot examples that demonstrate the subject's characteristic moves (opening a thought, building an argument, arriving at an image)
- Evaluation: generate text on topics the subject has addressed, compare to actual statements

### Integration with voice and avatar

The LLM generates text → fed to voice cloning model (ElevenLabs or equivalent) trained on the subject's voice → drives video avatar (Live Portrait, Metahuman, or similar).

The full pipeline:
```
Prompt / audience input
    ↓
LLM (fine-tuned on subject's corpus)
    → generates text in subject's voice and register
    ↓
Voice synthesis (cloned voice model)
    → audio output in subject's voice
    ↓
Video avatar (face driven by audio)
    → synchronized lip and expression animation
    ↓
Live projection / interactive display
```

---

## Distinguishing this from prompt engineering

Prompt engineering (system prompt + few-shot examples) produces surface-level stylistic approximation. Fine-tuning produces something deeper: the model has processed the corpus at a statistical level, integrating patterns of thought that don't surface in short-context prompting.

The difference is apparent in long-form generation: fine-tuned models sustain the subject's logic across paragraphs; prompted models drift toward generic LLM patterns after a few sentences.

---

## Ethical protocol

This method constructs a functional representation of a living (or recently living) person's mind and voice. It raises distinct ethical questions from image deepfake:

1. **Consent**: the subject must know a model is being trained on their corpus and consent to its specific use
2. **Scope**: the model is trained for a defined project and not distributed as a general-purpose tool
3. **Transparency**: performances or outputs using the model are declared as AI-generated, with the method described
4. **Subject's presence**: where possible, the subject is present alongside their model (as in DamasIA) — creating dialogue rather than replacement

The goal is not to substitute the person but to extend a documented presence into new contexts, in ways that remain clearly marked as construction.

---

## Tools referenced

- Whisper (open source) — transcription of audio corpus
- LLM fine-tuning — Mistral, Llama, or equivalent base
- ElevenLabs — voice cloning from audio corpus
- Live Portrait (open source) — voice-driven video avatar
- Metahuman (Unreal Engine) — photorealistic avatar alternative
