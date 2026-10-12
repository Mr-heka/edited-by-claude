# The checks before you hand it over

Run all of these on the final file. Fix and re-render anything that fails. Report each one in a line.

1. **It plays and it's the right shape.** `ffprobe` shows 1080x1920, the expected frame rate, H.264 video and AAC audio, and a length within a second of the cut.
2. **Every word is still there.** Re-transcribe the final MP4. Every word from the approved edit list comes back, in order. List any that don't.
3. **No stop-start gaps.** Measure silences on the final audio: no join over 0.22 s, no silence over 0.30 s.
4. **Nothing covers the face or falls off the phone.** Make a contact sheet, one frame every 2 seconds:
   ```bash
   ffmpeg -i "output/<name> - edited.mp4" -vf "fps=1/2,scale=270:-1,tile=6x6" -frames:v 1 output/contact-sheet.png
   ```
   Look at it. Text over the face, text in the bottom 400 px or the right 140 px, a cut-off word, or a frozen graphic is a fail.
5. **The first frame works as a cover.** Frame 0 shows what the video is about.
6. **Loudness.** `ffmpeg -i "output/<name> - edited.mp4" -af loudnorm=print_format=summary -f null -` reads about -14 LUFS integrated and a true peak no higher than -1.5 dBTP.
7. **Sync.** Spot-check three moments: the captioned word matches the mouth.

You can't hear, so say so: tell the person these checks passed and that they should still watch it once with sound before posting.

Made by Selr AI.
