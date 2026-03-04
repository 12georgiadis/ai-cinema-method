# Archive Animation

**Function**: Give motion to archival photographs, internet screenshots, and static documentary material — making a frozen image into a living presence.

**Used in**: [*Virus*](../projects/virus-2024.md)

---

## What problem this solves

Documentary cinema has always worked with the archive. The static photograph, the low-resolution screenshot, the surveillance still — these images testify to events but they're fixed, removed from time. Animating them doesn't reconstruct what happened; it adds a layer of presence, of unease, of uncanny life. The archive image that moves is neither the original document nor a reconstruction — it's something else.

---

## Method: Image-to-Video

Commercial image-to-video models take a single still and generate several seconds of motion from it. Unlike AI video generation from text, image-to-video is anchored to the specific image: the face, the lighting, the composition are preserved while motion is extrapolated.

### Use cases in documentary

- **Face animation**: archival portrait photographs, low-resolution screenshots of social media profiles. The face takes on micro-expressions, slight head movements — enough to feel present, disturbing.
- **Scene animation**: static news photographs of events. The crowd, the smoke, the police line — small movements that make the image feel contemporaneous.
- **Lipsync from audio**: combine with Live Portrait or similar to animate mouth movement from audio recording. A photograph of a person who spoke — now speaks again.

### Models tested

**RunwayML Gen-3 / Gen-4**: best quality for faces and controlled motion. 4–8s clips. Commercial, cloud-based.

**Luma Dream Machine**: strong on scene animation, slightly softer on faces. Cloud-based.

**CogVideoX** (open source): 6 seconds at 720×480. Lower quality but fully local. Useful for rough cuts and tests.

---

## Video extension

Image-to-video models can be applied to their own output to extend sequences. This creates a specific artifact: as the model moves further from the initial frame, the context window empties and the image begins to hallucinate. Objects drift, faces change, backgrounds dissolve. This "generational decay" is cinematically productive — it externalizes the failure of memory.

In *Virus*, this technique was applied to internet archive images of the Curtis Culwell Centre attack. The photographs, already low-resolution and compressed, animated for a few seconds, then began to transform — as if the image itself was forgetting what it depicted.

---

## Lipsync and facial animation

**Live Portrait**: animate a static portrait using audio. A 2D approach — works with photographs and drawings. Produces convincing facial animation including lip-sync from audio input. Low compute.

**ACT-ONE / Viggle**: full-body animation from video reference. Drive a static portrait using a reference performance — transplant movement from a real person onto an archival image.

---

## Ethical frame

Animating archival images of real events and persons raises documentary ethics questions. These are not simulations presented as real; they're declared transformations. The material difference from the original document — the motion, the artificiality at the edges — is part of the meaning, not a deception.

---

## Tools referenced

- RunwayML Gen-3 — image-to-video
- Luma Dream Machine — image-to-video
- CogVideoX (open source) — image-to-video
- Live Portrait (open source) — portrait lipsync animation
- ComfyUI — local pipeline for open source models
