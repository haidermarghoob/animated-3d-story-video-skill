# animated-3d-story-video — a Hark skill for 3D animated story Shorts

Make a ~60 second vertical (9:16, 1080x1920) 3D cartoon story Short just by chatting with Hark.
White round-head stick-limb characters with ink outlines and line-art faces, realistic HDRI-lit worlds built from free
CC0 assets, a moving camera with many shots and punchy cuts, word-by-word captions, sound effects and music that stops
dead at the twist. Everything is generated in code (three.js + Remotion + headless Chrome) on Hark's computer —
no Blender, no After Effects, no software on your phone or laptop.

![style](reference/ww1_style_frames.jpg)

## What you need
- A **Hark** account (phone app or website). That's it.
- A voice-over: make it free in **Google AI Studio** (text-to-speech) and send the file to Hark, record it yourself, or
  let Hark make it (with your free Gemini API key, or a free built-in voice).

## Install in Hark (2 minutes)
1. Download `animated-3d-story-video-skill.zip` (from the video description or this repo's Releases / the green *Code →
   Download ZIP* button).
2. In Hark, make a project for your videos, e.g. type: *"Ek naya project banao 3D Shorts naam se"*.
3. Upload the zip in the Hark chat and write: **"Is skill ko save kar lo"** (or "Save this skill").
4. Done. Hark unpacks it and sets up its render tools by itself.

## Make a video — three ways
| | type this in Hark |
|---|---|
| Copy the *style* of a Short you like | `<paste link>` *"Is video ko study karo aur isi andaaz me kisi doosri cheez pe nayi video banao 3d video skill ka use karke"* |
| Your own topic | *"Restaurants ne pager kyun use karne shuru kiye, is pe video banao 3d video skill ka use karke"* |
| No idea yet | *"Mujhe 3 topic ideas do"* |

Hark works one stage at a time and after each stage asks **"Theek hai? Aage chalun?"** — say *haan* to continue or tell
it exactly what to change ("scene 4 me dukaandar ka chehra bohot chhota hai, bada karo").

1. **Idea chalega?** — is there a clever schemer and a simple person who beats him with something new?
2. **Kahani** — title + ~1 minute script. Read it carefully; this is the foundation.
3. **Characters ka huliya** — every character's look, colours, faces; the places and the joke signs in the background.
4. **Pehli jhalak** — the characters and the main set rendered in real 3D.
5. **Storyboard + voice script** — every shot planned; the voice script with the emotion of each part. Make the voice
   (AI Studio, your own, or Hark's) and send the file.
6. **5 second trailer** — the first 5 seconds for real, to check the look before the long render.
7. **Awaaz + video sync** — Hark times every word so actions and captions land on the voice; slow reads are tightened.
8. **Video, hissa hissa** — rendered act by act with sound effects and music; check each act.
9. **Aakhri check** — black frames, frozen shots, cut-off text, loudness (-14 LUFS for YouTube) → your finished mp4.

Tips: check every stage; be specific; one new project per video; you can do it all from your phone.

## What's inside
```
SKILL.md                  the instructions Hark follows (stages, style rules, commands)
setup.sh                  one-time setup: Remotion + three.js (pinned), headless Chrome, Python venv, whisper model
new_project.sh            new video project from the template
smoke_test.sh             proves the whole pipeline works on a machine (~15 min)
engine/template/          the project template
  src/                    3D engine: characters (chars3d.js), worlds (world.js), camera/shot list, post-processing, captions
  tools/                  assets fetch, voice prep, TTS (Gemini / Edge), word timing (whisper), stills, preview, chunked render, QA
  audio/                  procedural SFX + music + mixer (no samples, no licence worries)
examples/ww1_sniper/      the full code of the reference Short "How Soldiers Beat Snipers in World War 1"
reference/                style frames of the reference Short
```
Run it yourself (Linux/macOS/WSL with Node 18+, Python 3.9+, ffmpeg):
```bash
bash setup.sh
bash new_project.sh ~/videos/test && cd ~/videos/test
.venv/bin/python tools/fetch_assets.py
python3 tools/est_timing.py script.json words.json && python3 tools/write_timing.py words.json src/timing.js
bash tools/stillrun.sh look chars 9 90        # out/chars3d.png, out/sheet_look.jpg
SCALE=1.5 bash tools/render.sh && bash tools/finish.sh "My Short"   # GL=angle on a GPU machine
```

## Credits & licences
- Code: MIT (see `LICENSE`). `audio/dsp.py` is MIT from *claude-animated-shorts* (see `THIRD_PARTY_NOTICES.md`).
- Rendering: [Remotion](https://www.remotion.dev) (free for individuals and small teams — check its licence if your
  company has more than 3 people), [three.js](https://threejs.org) (MIT).
- 3D assets: [Poly Haven](https://polyhaven.com) — CC0, downloaded at build time, not bundled.
- Font: Poppins (SIL OFL) via Google Fonts. Word timing: faster-whisper (MIT).
- Voices: your own account on Google AI Studio / ElevenLabs / Cartesia, or Microsoft Edge voices — follow their terms.

---

## Roman Urdu me (short)
**Ye kya hai?** Ek Hark skill (recipe) jo sirf chat se 3D cartoon Shorts banati hai — safed gol sar wale characters,
asli jaisi 3D duniya, chalta camera, captions, aawazein aur music. Koi software, coding ya mehnga computer nahi chahiye.

**Install:** zip download karo → Hark chat me upload karo → likho **"Is skill ko save kar lo"** → bas.

**Video banwao:** link paste karke *"Is video ko study karo aur isi andaaz me nayi video banao 3d video skill ka use
karke"*, ya apna topic likho, ya *"Mujhe 3 topic ideas do"*. Har qadam ke baad Hark poochega **"Theek hai? Aage chalun?"**
— haan bolo ya saaf batao kya badalna hai.

**Awaaz:** Google AI Studio me script daalo, awaaz banao, file download karke Hark ko bhej do — ya Hark khud bana dega.
