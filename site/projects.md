---
layout: page
title: Projects
description: >-
  Software projects in endangered language technology, Manx Gaelic AI tools,
  speech synthesis, recognition, and voice conversion.
permalink: /projects/
---

## Gaelg AI

<a href="https://gaelgai.im">gaelgai.im</a> is a public web platform providing AI-powered tools for the Manx Gaelic language. Built as part of my doctoral research and maintained as an open resource for the Manx-speaking community.

The platform currently offers four tools, each trained on Manx language resources:

- **Text-to-speech** — Type or paste Manx text and hear it spoken aloud, with a choice of male and female voices and adjustable speed.
- **Automatic speech recognition** — Upload or record Manx audio to get an automatic transcription.
- **Translation** — Translate between Manx and English in either direction.
- **Audio timestamping** — Upload a Manx recording with its transcript to generate word- and phrase-level timestamps, useful for subtitling and corpus annotation.

The platform is hosted at the University of Sheffield and is free to use. Feedback and data contributions are welcome.

---

## Domain-Robust Voice Conversion for Low-Resource ASR

*PhD project, 2025– · in preparation*

Speech recognisers trained on clean, read speech degrade sharply on **spontaneous** speech (filled pauses, reduced articulation, variable speaking rate), which is exactly what dominates low-resource and endangered-language recordings. This project asks whether **voice conversion (VC) can serve as an offline data-augmentation method** to close that read↔spontaneous gap, and builds toward a diffusion model purpose-designed for it.

The work runs in phases, each answering one question:

- **Phase 0 — VC as augmentation.** Benchmark four modern VC methods (kNN-VC, VEVO, Seed-VC, DiffVC) as augmentation for ASR: convert read LibriSpeech toward a spectrum of spontaneous domains, fine-tune five acoustic models, and measure WER across a read→spontaneous test continuum.
- **Phase 1 — Motivating diffusion.** Move from utterance-level to **word-level** evaluation to expose where conversion actually helps or hurts.
- **Phase 2 — A diffusion model trained on word pairs.** A minimal-change adaptation of DiffVC that, unlike the original same-voice reconstruction objective, is trained on **cross-speaker, content-matched word and phone pairs** mined from force-aligned LibriTTS. → [**Listen to sample training pairs**](/research/pair-corpora/)
- **Phase 3 — Endangered languages.** Apply the method to real endangered-language ASR (Manx, Cornish), where read↔spontaneous, speaker and accent mismatch compound.

It complements the corpus-building line of work (Interspeech 2026): that paper addresses the *data-format* problem, this one the *domain-mismatch* problem, and the two are additive.

---

## Other work

**COM4511/6511 Speech Processing** — Teaching materials and marking support for the University of Sheffield's speech technology module, covering MFCC extraction, keyword spotting, VAD, GMMs, and K-means clustering.

**Endangered language ASR pipeline** — End-to-end pipeline for training ASR models from short-form, heterogeneous corpora, used in the Interspeech 2026 paper.
