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

Each **pair** is the *same content spoken by two different speakers*, cut from
LibriTTS clean (`train-clean-100` + `train-clean-360`) using Montreal Forced
Aligner word and phone alignments. Word schemes (`word_nN`) match on whole
words; phone schemes (`phone_nN`) match on ARPABET phone sequences and can
begin or end mid-word — a leading or trailing hyphen marks the cut (`-t the`).
`N` is the length of the matched unit.

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

<h3>phone_n1 <small class="phones">(1-phone n-grams)</small></h3>

<div class="pair">
  <h4>/IY/ <span class="phones">— from "the"</span></h4>
  <div class="clip"><span class="who">Speaker 103 · 0.08 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair1/A_spk103.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1034 · 0.08 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair1/B_spk1034.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>/AY/ <span class="phones">— from "by"</span></h4>
  <div class="clip"><span class="who">Speaker 1246 · 0.13 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair2/A_spk1246.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1263 · 0.13 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n1/pair2/B_spk1263.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n3 <small class="phones">(3-phone n-grams)</small></h3>

<div class="pair">
  <h4>"-t the" <span class="phones">T DH AH</span></h4>
  <div class="clip"><span class="who">Speaker 1088 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair1/A_spk1088.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1116 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair1/B_spk1116.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"-n the" <span class="phones">N DH AH</span></h4>
  <div class="clip"><span class="who">Speaker 1098 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair2/A_spk1098.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 1246 · 0.15 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n3/pair2/B_spk1246.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n7 <small class="phones">(7-phone n-grams)</small></h3>

<div class="pair">
  <h4>"one of the" <span class="phones">W AH N AH V DH AH</span></h4>
  <div class="clip"><span class="who">Speaker 198 · 0.36 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair1/A_spk198.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 2289 · 0.36 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair1/B_spk2289.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"there was n-" <span class="phones">DH EH R W AH Z N</span></h4>
  <div class="clip"><span class="who">Speaker 2416 · 0.40 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair2/A_spk2416.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 4297 · 0.40 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n7/pair2/B_spk4297.mp3' | relative_url }}"></audio></div>
</div>

<h3>phone_n14 <small class="phones">(14-phone n-grams)</small></h3>

<div class="pair">
  <h4>"the united states" <span class="phones">DH IY Y UW N AY T IH D S T EY T S</span></h4>
  <div class="clip"><span class="who">Speaker 1271 · 0.98 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair1/A_spk1271.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 454 · 0.98 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair1/B_spk454.mp3' | relative_url }}"></audio></div>
</div>
<div class="pair">
  <h4>"it was impossible" <span class="phones">IH T W AH Z IH M P AA S AH B AH L</span></h4>
  <div class="clip"><span class="who">Speaker 6269 · 0.94 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair2/A_spk6269.mp3' | relative_url }}"></audio></div>
  <div class="clip"><span class="who">Speaker 7460 · 0.94 s</span><audio controls preload="none" src="{{ '/assets/pair-samples/phone_n14/pair2/B_spk7460.mp3' | relative_url }}"></audio></div>
</div>

</div>

<p class="pub-venue" markdown="1">
The 10 LibriTTS speakers reserved for DiffVC's test set are excluded throughout.
Samples cut from LibriTTS (CC BY 4.0). Part of ongoing doctoral work on
domain-robust voice conversion — see the
[project overview]({{ '/projects/' | relative_url }}).
</p>
