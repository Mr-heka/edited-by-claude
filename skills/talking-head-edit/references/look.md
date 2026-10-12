# The look: captions and motion graphics

Clean and minimal. The graphics explain what's being said; they never fight the person for attention.

## Safe zone (Instagram, TikTok, Shorts)

The apps cover parts of a vertical video with buttons and the caption. On a 1080x1920 frame keep text and key graphics:

- out of the bottom 400 px (the caption and buttons),
- out of the right 140 px (likes, comments, share),
- out of the top 200 px (the account name and tabs).

The person's face stays visible unless a full-screen graphic is the point of that moment.

## Captions

- 2 to 4 words per page, one or two lines, never a single word on its own unless it's a punchline.
- The word being spoken is highlighted (a colour or a weight change), the rest stays plain.
- One clean sans-serif font, bold enough to read on a phone, with a subtle shadow or outline only if the background is busy.
- Sit them in the lower-middle of the safe zone, clear of the chin.
- Never carry a caption across a cut. Spell names and brands the way the person confirmed.

## Motion graphics

- **One idea, one visual.** A label, a short list that builds, a simple diagram, a before and after, a number with what it means. Not one per sentence.
- **Use their words.** On-screen text is the person's own words or a 1 to 4 word label of what they said. Never add facts, numbers or claims they didn't say.
- **Calm palette.** A light or dark base, one accent colour, thin lines, lots of space. One font family.
- **Gentle motion.** Eases of 0.3 to 0.5 s, things slide or draw on and keep drifting slightly so the frame never freezes. Nothing flashing, no stickers or emoji.
- **Layouts to mix:** full screen of the person with a label beside the head, graphics behind or around the head, a split with the graphic on top and the person below, and the odd full-screen graphic. Change layout every few seconds so it never sits still.
- **The first second** shows what the video is about in a few words, so it also works as the cover.
- **Logos** only from the person or the company's own brand page, in their real colours. Never a lookalike, and never an Apple logo for "my Mac" (use a plain laptop drawing).

## Building with HyperFrames

HyperFrames turns HTML and animations into an MP4. Its own skills know how to build compositions:

- `/embedded-captions` adds word-synced captions to an existing talking-head video.
- `/talking-head-recut` packages a talking-head video with designed overlays: labels, callouts, kinetic titles, side panels.
- `npx hyperframes preview` opens a live preview; `npx hyperframes check` catches layout problems before a render; `npx hyperframes render` makes the MP4.

Show the person a preview or a few still frames of the look before the full render if it's the first video in a new style.

Made by Selr AI.
