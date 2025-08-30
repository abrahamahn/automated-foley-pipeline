# V2T-Foley-Script-Generator

This repository is dedicated to the foundational, first phase of a larger AI sound design pipeline. The goal is to build an advanced Video-to-Text (V2T) system that generates a detailed, multi-track audio "script" from any given video. This script will serve as the primary input for a future Text-to-Audio (T2A) or Text-Video-to-Audio (TV2A) model, automating the creative process of sound design.

The project is built by forking and enhancing an open-source video-LLM, specifically [Video-LLaVA](https://github.com/PKU-YuanGroup/Video-LLaVA), as its foundational model.

---

### 💡 Core Concept: A Chain-of-Thought V2T Pipeline

Instead of a single, simple video caption, this project focuses on a sophisticated, multi-stage V2T pipeline that mimics a human sound designer's thought process. It uses a "chain-of-thought" approach where the model breaks down the task into smaller, more manageable steps to ensure a highly granular and accurate output. This approach is designed to generate multiple, distinct text descriptions for different audio layers.

#### **Phase 1: Chain-of-Thought Reasoning**

This phase uses the multimodal capabilities of a Video-LLaVA-based model to analyze a video and perform the following tasks sequentially:

1.  **Event Identification:** The model first identifies all significant audio-visual events in the video.

2.  **Chain-of-Thought Reasoning:** For each event (e.g., an airplane crashing), the model performs a series of internal reasoning steps to answer a structured set of questions:
    * What is the main object involved?
    * What is the primary action of that object?
    * What is the context or environment?
    * What are all the potential sounds that would occur as a result of this action?

#### **Phase 2: Output Categorization**

The goal of this phase is to use the reasoning from Phase 1 to synthesize a structured output. The output will be a detailed, machine-readable text format (e.g., JSON) that isolates each individual object, subject, or ambient event. This ensures that every component of an event happening in the video is isolated for future individual audio generation. This is a crucial step that prepares the data for a future audio generation model.

#### **Output of the Pipeline**

The final output is a clean, machine-readable text format (e.g., JSON) that contains a set of text descriptions dedicated to each audio category.

```json
{
  "foley": [
    {"timestamp": "00:05", "description": "The sound of a key turning in a lock."},
    {"timestamp": "00:07", "description": "The sound of footsteps on a wooden floor."},
  ],
  "fx": [
    {"timestamp": "00:10", "description": "A loud, explosive crash as glass shatters."},
  ],
  "ambience": [
    {"timestamp": "00:00", "description": "The sound of a quiet forest with birds chirping and leaves rustling."},
  ],
  "dialogue": [
    {"timestamp": "00:15", "description": "A man whispers, 'Is anyone there?'"}
  ]
}
