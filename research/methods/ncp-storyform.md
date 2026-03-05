# NCP — Narrative Context Protocol for Documentary

## What is NCP?

The Narrative Context Protocol (NCP) is an open-source JSON schema created by [Subtxt](https://subtxt.app) for transporting narrative intentionality between AI agents. It encodes a story's deep structure — throughlines, themes, character dynamics — in a machine-readable format.

NCP was designed for fiction screenwriting, but the underlying Dramatica theory applies to documentary storytelling as well.

## Why adapt it for documentary?

Post-documentary filmmaking isn't chronological journalism. It has throughlines, thematic cycles, character arcs, and genre mechanics — just like fiction. But these structures are discovered during editing, not prescribed beforehand.

NCP gives us a way to:
1. **Formalize** the narrative structure as it emerges from source material
2. **Share** that structure between AI agents (RAG, writing assistants, editing tools)
3. **Evolve** the storyform iteratively as the film develops

## Schema adaptation for post-documentary

### Original Dramatica throughlines (fiction)

| Throughline | Concern |
|---|---|
| Overall Story | The big picture plot |
| Main Character | Protagonist's inner journey |
| Influence Character | Who challenges the MC's worldview |
| Relationship Story | The evolving relationship between MC and IC |

### Documentary adaptation

| Throughline | Documentary equivalent |
|---|---|
| Overall Story | The investigation / revelation arc |
| Main Character | The subject's inner world (what the film discovers) |
| Influence Character | The filmmaker's presence / the system / the audience |
| Relationship Story | The evolving dynamic between filmmaker and subject |

### Additional documentary-specific fields

```json
{
  "documentary_specifics": {
    "source_types": ["interviews", "archive", "correspondence", "online_posts"],
    "ethical_framework": "...",
    "verification_level": "primary_sources | secondary | unverified",
    "genre_shift_mechanics": {
      "description": "How the film's genre perception changes",
      "shifts": [
        {"from": "investigative", "to": "portrait", "trigger": "..."}
      ]
    }
  }
}
```

## How it integrates with tools

```
Film Bible (markdown)
    ↓
NCP Storyform (JSON)
    ↓
├── FCPXML Generator → FCP timeline with act markers
├── RAG Agent → Context-aware research queries
├── Writing Assistant → Scene drafts with thematic awareness
└── Emotion Curve → D3.js visualization of narrative arcs
```

The storyform acts as a shared contract between tools. Each tool reads the same narrative intent and produces output consistent with it.

## Empty template

```json
{
  "storyform": {
    "title": "",
    "genre": "",
    "throughlines": {
      "overall_story": {
        "concern": "",
        "issue": "",
        "problem": "",
        "solution": ""
      },
      "main_character": {
        "concern": "",
        "issue": "",
        "problem": "",
        "solution": "",
        "resolve": "changed | steadfast"
      },
      "influence_character": {
        "concern": "",
        "issue": "",
        "problem": ""
      },
      "relationship_story": {
        "concern": "",
        "issue": "",
        "problem": ""
      }
    },
    "characters": [],
    "themes": {
      "core_theme": "",
      "thematic_cycles": []
    },
    "structure": {
      "acts": [],
      "sequences": []
    }
  }
}
```

## References

- [Subtxt NCP spec](https://subtxt.app/ncp) — original schema
- Dramatica theory — Melanie Anne Phillips & Chris Huntley
- [Jim Hull on narrative structure](https://narrativefirst.com)

## Status

Experimental. This adaptation is being tested on an active feature documentary production. The schema will evolve as we learn what works.
