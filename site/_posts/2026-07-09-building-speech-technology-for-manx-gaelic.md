---
layout: post
title: "Building speech technology for an endangered language"
date: 2026-07-09
description: >-
  Why Manx Gaelic needs its own speech technology, and how we're building
  ASR, TTS, translation, and voice conversion with limited data.
tags:
  - manx-gaelic
  - speech-technology
  - endangered-languages
  - research
crosspost: true
---

Manx Gaelic — *Gaelg* — is a Celtic language from the Isle of Man that was declared extinct by UNESCO in 2009 following the death of the last native speaker, Ned Maddrell, in 1974. But Manx never truly died. A community of passionate speakers kept it alive, and today there are around 2,000 speakers and a Manx-medium primary school (*Bunscoill Ghaelgagh*) producing a new generation of fluent speakers.

<!--more-->

What Manx doesn't have, though, is the digital infrastructure that most of us take for granted. There's no Manx Siri, no Manx Google Translate, no Manx autocorrect. When the tools we use every day don't speak your language, it sends a clear message: this language doesn't belong in the modern world.

My PhD research at the University of Sheffield is about changing that.

## The low-resource problem

Modern speech and language technology is hungry for data. Training a decent text-to-speech system typically requires tens of hours of studio-quality recorded speech. A competitive ASR model wants hundreds or thousands of hours. Machine translation systems are trained on millions of parallel sentences.

Manx has a fraction of this. The total available speech data amounts to a handful of hours across varying recording conditions, speakers, and time periods. Written parallel text is similarly scarce. Standard approaches simply won't work.

This is the **low-resource problem**, and it's not unique to Manx. The vast majority of the world's 7,000+ languages face the same data scarcity. The techniques that work for English, Mandarin, and Spanish are designed for a world of abundance. We need methods designed for scarcity.

## What we've built

The [Gaelg AI](https://gaelgai.im) platform is my attempt to bring these technologies to the Manx-speaking community right now, even while the research is ongoing. It currently provides four tools:

**Text-to-speech** lets you type Manx text and hear it spoken aloud. We offer male and female voices with adjustable speed. The underlying models are trained on the limited Manx speech data available, with cross-lingual transfer from related Celtic languages helping to fill the gaps.

**Automatic speech recognition** takes Manx audio — uploaded or recorded in the browser — and produces a text transcription. My Interspeech 2026 paper, *Bootstrapping Endangered Language ASR from Short-Form Corpora*, details the techniques that make this possible with very little training data.

**Translation** provides Manx-to-English and English-to-Manx translation. The models are experimental and make mistakes, but they're useful for getting the gist of a text or producing a first draft that a speaker can correct.

**Audio timestamping** aligns a Manx transcript to its audio at the word and phrase level, producing timestamps useful for subtitling, corpus annotation, and language learning materials.

## Diffusion-based voice conversion

Beyond the platform, a major strand of my research is **Grad-VC** — a voice conversion framework built on Grad-TTS and DiffVC. Voice conversion lets you change *who* a recording sounds like without changing *what* is said. This has exciting applications for endangered languages: you could, for example, generate speech in the voice of a historical speaker from a text prompt, or convert a learner's pronunciation into a more native-like form for feedback.

The challenge is that standard voice conversion systems require parallel data (the same sentences spoken by both the source and target speakers) or rely on forced alignment tools that don't exist for languages like Manx. Grad-VC uses word-pair supervision instead, removing both dependencies.

## Why this matters

Language technology isn't just a convenience — it's infrastructure. When a language has TTS, it can have screen readers for the visually impaired. When it has ASR, it can have live captioning for the deaf. When it has translation, it can have bilingual interfaces that make government services accessible. When it has voice conversion, it can generate diverse training data from a single speaker.

These aren't abstract benefits. They're the tools that will determine whether Manx — and hundreds of languages like it — can survive in a world that increasingly runs on AI.

If you're interested in this work, I'd love to hear from you. You can try the tools at [gaelgai.im](https://gaelgai.im), find me on [GitHub](https://github.com/c-bartley), or [get in touch](mailto:csjbartley1@sheffield.ac.uk) directly.
