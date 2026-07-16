---
layout: page
title: Cross-speaker pair corpora
description: >-
  Audio samples of cross-speaker, content-matched word and phone pairs mined
  from force-aligned LibriTTS — training supervision for diffusion voice
  conversion (DiffVC / Grad-VC).
permalink: /research/pair-corpora/
---

<style>
  .pair-grid .pair {
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 0.6rem 1rem;
    margin: 0.8rem 0;
  }
  .pair-grid .pair h4 {
    margin: 0.2rem 0 0.5rem;
  }
  .pair-grid .pair .phones {
    color: #888;
    font-weight: 400;
    font-size: 0.9em;
  }
  .pair-grid .clip {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    margin: 0.35rem 0;
    flex-wrap: wrap;
  }
  .pair-grid .clip .who {
    width: 11rem;
    color: #444;
    font-size: 0.9em;
  }
  .pair-grid audio {
    height: 34px;
    max-width: 100%;
  }
</style>

Each **pair** below is the *same linguistic content spoken by two different
speakers* — the cross-speaker, content-matched supervision that a standard
diffusion voice-conversion model never sees during training.

## Why these samples exist

Diffusion voice-conversion (VC) models such as **DiffVC** (Popov et al., 2021)
train their decoder as a *reconstruction* objective: given a speaker-averaged
("average-voice") content representation of an utterance, rebuild *that same
utterance in its own speaker's voice*. The model therefore only ever learns to
map content → the voice it was already spoken in. It is **never shown two
speakers saying the same thing**, even though matching content across voices is
exactly the signal voice conversion must produce at inference.

These corpora supply that missing signal. By mining LibriTTS for sequences that
recur across speakers, we build genuine **(speaker A, speaker B)
content-matched pairs** and can train the decoder on cross-speaker mappings
directly, rather than only on same-voice reconstruction. The scientific
question: **does adding this cross-speaker pairing supervision improve
conversion?** This is Phase 2 of my
[voice-conversion-for-ASR project]({{ '/projects/' | relative_url }}).

## The n-gram ladder

Content matches are collected at two granularities — whole **words** and
**phones** — and at several context lengths. Longer context means the two clips
share more of the utterance, but such matches are rarer; shorter context is
abundant but noisier and increasingly sub-lexical. The samples below walk that
trade-off. Listening top-to-bottom in each unit, the two voices track each
other ever more tightly in content as the context grows.

| Scheme | Unit × length | Example | What it isolates |
|--------|---------------|---------|------------------|
| `word_n1`  | 1 word    | "Beautiful"           | single content word, maximal data |
| `word_n3`  | 3 words   | "As soon as"          | short phrase |
| `word_n5`  | 5 words   | "As a matter of fact" | full phrase, strongest content match |
| `phone_n1` | 1 phone   | /IY/ in "the"         | single phone, degenerate limit |
| `phone_n3` | 3 phones  | "at the" `T DH AH`    | sub-word span, crosses word edges |
| `phone_n7` | 7 phones  | "one of the" `W AH N AH V DH AH` | multi-word phone span |
| `phone_n14`| 14 phones | "the united states"   | long phone span, closest to `word_n5` |

## How the pairs are built

- **Source:** LibriTTS *clean* (`train-clean-100` + `train-clean-360`), 24 kHz,
  1,141 speakers.
- **Alignment:** Montreal Forced Aligner (`english_us_arpa`) — the same aligner
  DiffVC used — giving word- and phone-level timings.
- **Held-out speakers excluded:** the 10 LibriTTS speakers DiffVC reserves for
  testing are removed everywhere, so no pair can leak the evaluation set.
- **Pairs:** for every sequence spoken by ≥ 2 speakers, each speaker's
  occurrence is a segment; cross-speaker pairings of those segments are the
  training pairs.
- The clips here are the *typical* case (near-median duration, contiguous),
  chosen only for listenability — cut by the exact same tokenisation as the full
  training corpora.

## Caveats

- **Phone n-grams cross word boundaries by design.** The same phone sequence can
  span different text — `T DH AH` is both "a**t the**" and "eigh**t the**". That
  is intended (the phone schemes match on sound, not spelling), but every pair
  shown here was verified to recover to the *same* word string on both sides so
  the demo is not misleading.
- **Single-phone (`phone_n1`) clips are ~0.1 s** and deliberately degenerate —
  they mark the shortest, least linguistically meaningful end of the ladder.

---

## Samples

<div class="pair-grid" markdown="0">

<h3>word_n1 <small class="phones">(1-word n-grams)</small></h3>

<div class="pair">
  <h4>"Beautiful"</h4>
  <div class="clip"><span class="who">Speaker 103 · 0.51 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n1/pair1/A_spk103.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1841 · 0.51 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n1/pair1/B_spk1841.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"Together"</h4>
  <div class="clip"><span class="who">Speaker 1743 · 0.49 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n1/pair2/A_spk1743.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 201 · 0.49 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n1/pair2/B_spk201.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"Remember"</h4>
  <div class="clip"><span class="who">Speaker 1970 · 0.46 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n1/pair3/A_spk1970.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 254 · 0.46 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n1/pair3/B_spk254.mp3' | relative_url }}"></audio></div>
</div>

<h3>word_n3 <small class="phones">(3-word n-grams)</small></h3>

<div class="pair">
  <h4>"One of the"</h4>
  <div class="clip"><span class="who">Speaker 101 · 1.14 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n3/pair1/A_spk101.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 2256 · 0.81 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n3/pair1/B_spk2256.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"As soon as"</h4>
  <div class="clip"><span class="who">Speaker 231 · 1.16 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n3/pair2/A_spk231.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 225 · 0.99 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n3/pair2/B_spk225.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"I don't know"</h4>
  <div class="clip"><span class="who">Speaker 250 · 1.34 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n3/pair3/A_spk250.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 6104 · 1.26 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n3/pair3/B_spk6104.mp3' | relative_url }}"></audio></div>
</div>

<h3>word_n5 <small class="phones">(5-word n-grams)</small></h3>

<div class="pair">
  <h4>"As a matter of fact"</h4>
  <div class="clip"><span class="who">Speaker 8772 · 1.29 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n5/pair1/A_spk8772.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 7286 · 1.24 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n5/pair1/B_spk7286.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"It seems to me that"</h4>
  <div class="clip"><span class="who">Speaker 8050 · 1.53 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n5/pair2/A_spk8050.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 6836 · 1.48 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n5/pair2/B_spk6836.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"What do you mean by"</h4>
  <div class="clip"><span class="who">Speaker 7247 · 1.64 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n5/pair3/A_spk7247.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 5802 · 1.04 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/word_n5/pair3/B_spk5802.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n1 <small class="phones">(1-phone n-grams)</small></h3>

<div class="pair">
  <h4>/IY/ <span class="phones">in the word "the"</span></h4>
  <div class="clip"><span class="who">Speaker 103 · 0.08 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair1/A_spk103.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1034 · 0.08 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair1/B_spk1034.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>/AY/ <span class="phones">in the word "by"</span></h4>
  <div class="clip"><span class="who">Speaker 1246 · 0.13 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair2/A_spk1246.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1263 · 0.13 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair2/B_spk1263.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>/AH/ <span class="phones">in the word "the"</span></h4>
  <div class="clip"><span class="who">Speaker 1040 · 0.06 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair3/A_spk1040.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1069 · 0.06 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair3/B_spk1069.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n3 <small class="phones">(3-phone n-grams)</small></h3>

<div class="pair">
  <h4>"At the" <span class="phones">T DH AH</span></h4>
  <div class="clip"><span class="who">Speaker 1088 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair1/A_spk1088.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1116 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair1/B_spk1116.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"In the" <span class="phones">N DH AH</span></h4>
  <div class="clip"><span class="who">Speaker 1098 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair2/A_spk1098.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1246 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair2/B_spk1246.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"To do" <span class="phones">T IH D</span></h4>
  <div class="clip"><span class="who">Speaker 1069 · 0.18 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair3/A_spk1069.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1867 · 0.18 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair3/B_spk1867.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n7 <small class="phones">(7-phone n-grams)</small></h3>

<div class="pair">
  <h4>"One of the" <span class="phones">W AH N AH V DH AH</span></h4>
  <div class="clip"><span class="who">Speaker 198 · 0.36 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair1/A_spk198.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 2289 · 0.36 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair1/B_spk2289.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"There was no" <span class="phones">DH EH R W AH Z N</span></h4>
  <div class="clip"><span class="who">Speaker 2416 · 0.40 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair2/A_spk2416.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 4297 · 0.40 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair2/B_spk4297.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"A moment" <span class="phones">AH M OW M AH N T</span></h4>
  <div class="clip"><span class="who">Speaker 3526 · 0.45 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair3/A_spk3526.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 4137 · 0.45 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair3/B_spk4137.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n14 <small class="phones">(14-phone n-grams)</small></h3>

<div class="pair">
  <h4>"The united states" <span class="phones">DH IY Y UW N AY T IH D S T EY T S</span></h4>
  <div class="clip"><span class="who">Speaker 1271 · 0.98 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair1/A_spk1271.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 454 · 0.98 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair1/B_spk454.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"It was impossible" <span class="phones">IH T W AH Z IH M P AA S AH B AH L</span></h4>
  <div class="clip"><span class="who">Speaker 6269 · 0.94 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair2/A_spk6269.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 7460 · 0.94 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair2/B_spk7460.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"Responsibility" <span class="phones">R IY S P AA N S AH B IH L AH T IY</span></h4>
  <div class="clip"><span class="who">Speaker 340 · 0.92 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair3/A_spk340.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 7447 · 0.91 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair3/B_spk7447.mp3' | relative_url }}"></audio></div>
</div>

</div>

---

<p class="pub-venue" markdown="1">
Samples cut from LibriTTS (CC BY 4.0) with the Montreal Forced Aligner. Part of
ongoing doctoral work on domain-robust voice conversion at the University of
Sheffield.
</p>
