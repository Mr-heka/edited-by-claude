# Set up Talking-Head Edit

You are installing this kit on the user's machine. Paths that don't start with `~` are relative to this repo.

## 1. Check the tools

These three are needed. Check each, and install what's missing:

| Tool | Check | If missing |
|---|---|---|
| FFmpeg | `ffmpeg -version` | Mac: `brew install ffmpeg` (needs Homebrew from brew.sh). Windows: `winget install Gyan.FFmpeg` |
| Node.js 22 or newer | `node -v` | Mac: `brew install node`. Windows: `winget install OpenJS.NodeJS.LTS`. Or the installer from nodejs.org |
| HyperFrames | `npx hyperframes --version` | Nothing to install: `npx` fetches it on first use |

If an install needs the user's password or admin rights, tell them the one command to run, wait, then check again.

## 2. Add the HyperFrames skills

HyperFrames (open source, by HeyGen) turns HTML and animations into MP4 video. Its skills teach the agent how to build captions and overlays. Install the core set:

```bash
npx hyperframes skills update
```

## 3. Install this skill

Copy `skills/talking-head-edit/` to `~/.claude/skills/talking-head-edit/`, replacing an older copy of this same skill if one is there. Create `~/.claude/skills/` if it's missing. If the user already has a `references/my-style.md` in their installed copy, keep theirs: it holds the rules they've taught it.

If Codex is installed (`~/.codex` exists), copy the same folder to `~/.codex/skills/talking-head-edit/` as well (same rule for `my-style.md`).

Change nothing else.

## 4. Check

1. `~/.claude/skills/talking-head-edit/SKILL.md` exists and matches this repo's copy.
2. `ffmpeg -version`, `node -v` and `npx hyperframes --version` all answer.

## 5. Report

Tell the user, briefly:

- the skill is installed (and where), and which tools were already there or got installed;
- the first transcription downloads a speech model, so the first edit takes longer;
- next step: start a new session and say "Edit this video" with the path to a talking-head clip filmed vertically.

## Removing

Delete `~/.claude/skills/talking-head-edit/` (and `~/.codex/skills/talking-head-edit/` if present). FFmpeg, Node and the HyperFrames skills stay; remove them separately if you want.
