---
layout: page
title: Projects
description: >-
  Software projects in endangered language technology, Manx Gaelic AI tools,
  speech synthesis, recognition, and voice conversion.
permalink: /projects/
---

## Gaelg AI

<a href="https://gaelgai.im">gaelgai.im</a> — A public web platform providing AI-powered tools for the Manx Gaelic language. Built as part of my doctoral research and maintained as an open resource for the Manx-speaking community.

The platform currently offers four tools, each trained on Manx language resources:

- **Text-to-speech** — Type or paste Manx text and hear it spoken aloud, with a choice of male and female voices and adjustable speed.
- **Automatic speech recognition** — Upload or record Manx audio to get an automatic transcription.
- **Translation** — Translate between Manx and English in either direction.
- **Audio timestamping** — Upload a Manx recording with its transcript to generate word- and phrase-level timestamps, useful for subtitling and corpus annotation.

The platform is hosted at the University of Sheffield and is free to use. Feedback and data contributions are welcome.

---

## Grad-VC

A diffusion-based voice conversion framework designed for low-resource and endangered language settings. Built on Grad-TTS and DiffVC, Grad-VC uses word-pair supervision for non-parallel training, eliminating the need for forced alignment — a critical advantage when working with languages that lack the phonetic inventories and pronunciation lexicons that alignment tools require.

Key design decisions include a static speaker embedding approach chosen for low-resource constraints, and a joint diffusion-prior loss for training stability.

*Research code — not yet publicly released.*

---

## Manx Search Data

<a href="https://github.com/c-bartley/manx-search-data">github.com/c-bartley/manx-search-data</a> — Structured bilingual texts for the Manx language (forked from [david-allison/manx-search-data](https://github.com/david-allison/manx-search-data)), supporting searchable access to Manx-English parallel texts.

---

## Other work

**COM4511/6511 Speech Processing** — Teaching materials and marking support for the University of Sheffield's speech technology module, covering MFCC extraction, keyword spotting, VAD, GMMs, and K-means clustering.

**Endangered language ASR pipeline** — End-to-end pipeline for training ASR models from short-form, heterogeneous corpora, used in the Interspeech 2026 paper.
