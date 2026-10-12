---
name: talking-head-edit
description: Edit a raw talking-head clip (a selfie video, a piece to camera) into a tight vertical reel with Claude Code - keeps the best take of each line, cuts the pauses and false starts close to the words, adds word-synced captions and clean motion graphics with HyperFrames, sets the sound level, renders, then checks nothing got clipped. Use when someone says "edit this video", "cut my talking-head clip", "make this a reel", "tighten the pauses", "caption this", "add motion graphics to my video", or "edited by Claude".
---

# Talking-head edit

You film it. Claude does the rest: picks the takes, cuts it tight, captions it, puts clean motion graphics on screen and renders the reel. This is a starter skill. It gets a good first edit; it gets great when the person teaches it their style (step 9).

**Done when:** a 1080x1920 MP4 is in the project's `output/` folder, every word they meant to keep is still in it (checked by re-transcribing), the captions and graphics are inside the phone safe zone, and they've been told what was cut and what to look at.

Never change, move or re-encode over the original clip. Work on a copy.

## 0. Before you start

Read [the cut rules](references/tight-cut.md) and [the look](references/look.md). Check the tools are there: `ffmpeg -version`, `node -v` (22 or newer) and `npx hyperframes --version`. If one is missing, install it (or give the person the one command to run if it needs their password), then carry on.

Ask for the clip path if they haven't given it. Make a project folder beside the clip called `<clip name> edit/` with `work/` and `output/` inside. Read `references/my-style.md` if it has anything in it, and follow it over the defaults.

## 1. Make a working copy

Probe the clip with `ffprobe`: size, rotation, frame rate, length, colour (HDR if the transfer is `arib-std-b67` or `smpte2084`; phone footage often is).

Make `work/source.mp4`: 1080x1920 portrait (apply the rotation), H.264, standard colour (tone-map HDR to SDR), the source frame rate if it's 24, 25 or 30 (else 30), 48 kHz audio. Also extract `work/voice.wav` (mono, 16 kHz) for transcribing and measuring.

## 2. Transcribe with word timings

```bash
npx hyperframes transcribe work/source.mp4 --model medium.en --json
```

The first run downloads the speech model. Read the transcript it writes. Whisper mishears names and brands, so list any proper nouns you're unsure of for step 3.

## 3. Pick the takes and show the cut

People repeat lines when they film. For each line, keep the **last clean, complete take** and drop the false starts, restarts ("let me do that again"), and stray words between takes. Keep the person's own words and order. Never rewrite what they said or splice half a sentence from one take onto another.

Write `work/edit-list.json`: the kept spans in source time, each with its text. Then show the person a plain table: the kept lines in order, what was cut, the expected length, and any names you weren't sure Whisper heard right. Wait for their OK or fixes.

## 4. Cut it tight

Apply [the cut rules](references/tight-cut.md): cuts land in silence, close to the words, with short joins, no breaths or dead air between lines, and a tiny crossfade so nothing clicks. Render the voice-only cut to `work/cut-preview.wav`.

**Check without ears:** re-transcribe `work/cut-preview.wav` and compare it with the kept text. Every kept word must come back, in order. If a word is missing or clipped, widen that cut by 40 ms and try again. List anything you couldn't fix.

## 5. Captions

Word-synced captions, built with HyperFrames (its `/embedded-captions` workflow, or by hand). The defaults are in [the look](references/look.md): 2 to 4 words per page, the spoken word highlighted, never across a cut, inside the safe zone. Use the corrected spellings from step 3.

## 6. Motion graphics with HyperFrames

Plan the graphics before building them: one visual for each key idea, not one per sentence. Write the plan as a short list (time, what's said, what appears) and show it with the cut if the person wants to approve it.

Build them as a HyperFrames composition over the cut footage (its `/talking-head-recut` workflow is made for this). Follow [the look](references/look.md): clean, minimal, moving gently, never covering the face. Only use real logos the person supplies or ones from the company's own brand page, never a lookalike.

## 7. Sound

Voice first. Normalise to about **-14 LUFS** integrated with a true peak no higher than **-1.5 dBTP** (`ffmpeg` `loudnorm`). If they want music, use only a track they have the rights to, kept well under the voice. Little clicks or pops for graphics are optional and quiet.

## 8. Render and check

Render 1080x1920, H.264, AAC, to `output/<clip name> - edited.mp4`. Then run [the checks](references/checks.md): length, every word back in order, a contact sheet of frames to catch text over the face or off the safe zone, the first frame shows what the video is about, and the loudness. Fix and re-render anything that fails.

Hand over: the file path, the final length, a short list of what was cut, and anything you'd like them to look at.

## 9. Teach it your style

After they watch it, ask what they'd change. Turn each note into one plain rule (for example "cut even tighter between sentences", "no captions on the first two seconds", "brand colour is #1E5EFF") and, on their yes, add it to `references/my-style.md` in this skill's folder. Read that file at the start of every edit. That's how this goes from a starter edit to their edit: you don't buy it, you teach it.

Made by Selr AI.

<!-- Provenance marker: sk-l9xx0l --><!-- Provenance signature: ⁠​‌​‌​​‌‌​‌​​​‌​‌​‌​​‌‌​​​‌​‌​​‌​​​‌‌​​​‌⁠ -->
