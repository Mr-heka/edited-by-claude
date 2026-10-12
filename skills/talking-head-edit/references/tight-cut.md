# The cut rules

The goal: it flows like one take, fast, with no stop-start gaps, and no word ever clipped.

## Measure speech on the audio, not just the transcript

Whisper's word times drift, especially around pauses. Use them to find the words, then place every cut using the audio itself:

```bash
ffmpeg -i work/voice.wav -af silencedetect=noise=-38dB:d=0.12 -f null - 2>&1 | grep silence_
```

Treat a stretch as silent only if it's quiet for at least 0.12 s. If the room is noisy, move the threshold up (towards -32 dB) until the gaps between words show up; if quiet words go missing, move it down.

A cut always sits inside silence, never inside a word.

## The numbers

| What | Default |
|---|---|
| Lead-in before the first sound of a kept line | 60 ms (never less) |
| Tail after the last sound of a kept line | 90 to 120 ms (endings like "s", "t" and "k" are quiet, so don't trim them) |
| Gap you hear at a join between two lines | about 0.16 s, never more than 0.22 s |
| Pauses inside a kept line | over 0.25 s gets shortened to about 0.15 s; 0.25 s or under stays |
| Longest silence anywhere | 0.30 s |
| Crossfade at every cut | 20 to 30 ms (stops clicks) |

These make most people land at roughly 180 to 220 words a minute. If it sounds rushed for this person, raise the join gap a little; if it still drags, lower the pause trigger.

## What goes, what stays

- **Goes:** false starts, restarts, dead air, breaths and lip smacks between lines, "hang on", anything said to someone off camera.
- **Stays:** every word of the kept take, including ums and "you know" unless the person asks for them out. Removing filler words inside a sentence often sounds choppy, so leave them by default.
- If a quiet word sits inside a pause you're about to cut, keep the pause.

## Building the cut

Write the final spans (start and end in source seconds, after the pads) to `work/edit-list.json`, then build the cut with ffmpeg (trim each span, crossfade the audio at each join, cut the video on the same frames). Keep the picture and sound cut at the same points so the lips stay in sync.

## Prove it

Re-transcribe the voice-only cut. Every kept word must be there, in order. A missing word means a cut is too tight: widen it by 40 ms and check again. Then run silencedetect on the cut itself: any join over 0.22 s or any silence over 0.30 s gets fixed.

Made by Selr AI.
