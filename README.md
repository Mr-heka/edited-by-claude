# Edited by Claude: the talking-head starter skill

Film a talking-head clip on your phone. Claude Code does the rest:

- **Picks the best take** of each line and drops the false starts.
- **Cuts it tight**, close to the words, so it flows like one take with no stop-start gaps.
- **Captions every word**, synced and inside the phone safe zone.
- **Adds clean motion graphics** with HyperFrames: one simple visual for each key idea, never covering your face.
- **Sets the sound level** and renders a 1080x1920 reel.
- **Checks its own work**: re-transcribes the finished video to prove no word got clipped, and looks at every few seconds of it.

It shows you the cut before it renders, so you stay in control.

## It's a starter. Teach it your style.

It didn't just work out of the box for us either. The edits you see on our page took hours of teaching: the right cuts, the colours, the framing, the text. After every video, tell it what you'd change and it saves that as a rule in `my-style.md`. Each edit gets closer to yours. You don't buy it, you teach it.

## Install

Copy the prompt in [SETUP-PROMPT.md](SETUP-PROMPT.md) into a new Claude Code or Codex session. Then start a new session and say:

> Edit this video: /path/to/my-clip.mov

**You need:** Claude Code or Codex, FFmpeg and Node.js 22 or newer (the setup checks and installs them). Everything runs on your own computer.

## What's inside

| File | What it does |
|---|---|
| `skills/talking-head-edit/SKILL.md` | The step-by-step edit |
| `references/tight-cut.md` | The cut rules and the numbers behind a tight edit |
| `references/look.md` | Captions, safe zones and the clean motion-graphics look |
| `references/checks.md` | The checks before it hands the video over |
| `references/my-style.md` | Your rules, added as you teach it |

## Built on

- [Claude Code](https://code.claude.com/docs) to run it.
- [HyperFrames](https://github.com/heygen-com/hyperframes) (open source, Apache 2.0, by HeyGen) for captions, motion graphics and the render, including its built-in Whisper transcription.
- [FFmpeg](https://ffmpeg.org) for cutting and sound.

Made by Selr AI.
