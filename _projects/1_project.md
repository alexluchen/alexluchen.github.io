---
layout: page
title: AlexTTS
description: A text-to-speech system built from scratch using a decoder-only autoregressive transformer
img: assets/img/alextts_architecture.png
importance: 1
category: work
related_publications: false
---

AlexTTS is a text-to-speech system built from scratch, leveraging a decoder-only autoregressive transformer implemented via Meta's [Lingua](https://github.com/facebookresearch/lingua) framework. Given a text prompt, the model synthesizes speech.

**[View project page →](https://alexluchen.github.io/AlexTTS/)**

<div class="row mt-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/alextts_architecture.png" title="AlexTTS high-level architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    High-level architecture of AlexTTS. The model takes raw audio and text as input and autoregressively decodes speech tokens which are then converted back to audio. Note that the reference was not used in the code.
</div>

## How it works

The pipeline has three main stages:

- **Pre-processing:** Raw audio is tokenized via a speech tokenizer (e.g. DAC), while text is converted to phonemes using a G2P phonemizer (Misaki).
- **Training:** The autoregressive transformer is trained with cross-entropy loss between predicted and ground-truth speech tokens, conditioned on text and speech embeddings.
- **Inference:** The model autoregressively generates speech tokens conditioned on the text embeddings, which are then decoded back to audio by the speech tokenizer.