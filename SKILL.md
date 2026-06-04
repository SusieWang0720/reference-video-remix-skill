---
name: reference-video-remix
description: Use when turning a reference video link, social post, YouTube/X/TikTok URL, spreadsheet script, screenshots, or rough product brief into a new product explainer/ad video with visual breakdown, script/storyboard, generated scene assets, licensed background music, voiceover/dialogue, Remotion production, render verification, and source/license documentation.
---

# Reference Video Remix

## Purpose

Create a new product video from a reference video or script without blindly copying it. Extract structure, pacing, scene grammar, visual motifs, and audio strategy; then build an original video with traceable assets, licensed music, voiceover, and a verified render.

Use this with the `remotion` skill for React video production. Use `imagegen` when new scene images or product-style visuals are needed. Use spreadsheet/document skills when the brief arrives as `.xlsx`, `.docx`, slides, or screenshots.

## Operating Rules

- Treat the reference as inspiration and analysis input, not source footage to clone frame-for-frame unless the user owns it or explicitly provides rights.
- If a URL is blocked by login, anti-bot, region, or playback restrictions, try available browser tools or screenshots before calling it unresolved. Record exactly what was verified and what was blocked.
- Never claim music is "copyright-free" unless the source says so. Prefer "royalty-free", "licensed for this use", or the platform's exact license wording.
- Store source links, license notes, track name, artist, and local asset paths in project notes.
- Keep old assets unless cleanup is explicitly requested; do not delete files as part of normal iteration.
- Verify every final claim with fresh commands: typecheck/build/render, `ffprobe`, and at least a few still frames for visual sanity.

## Workspace Pattern

For each video job, create a self-contained folder:

```text
data/video-breakdowns/<slug>/
├── AGENTS.md
├── source/                 # copied input scripts, extracted JSON, source metadata
├── assets/
│   ├── reference/          # screenshots / extracted frames from the reference
│   └── generated/          # generated scene images and reusable visuals
├── notes/
│   ├── breakdown.md        # reference analysis
│   ├── storyboard.md       # timeline, shot list, voice/music directions
│   └── music-source.md     # optional standalone license note
├── remotion/               # standalone Remotion project
└── renders/                # mp4 exports and verification stills
```

If the repository already has an `AGENTS.md`, follow it. If creating a new job folder without local rules, write a short `AGENTS.md` first that defines where sources, generated assets, notes, Remotion code, and renders live.

## Workflow

### 1. Intake

Collect or infer:

- reference link(s), screenshots, or spreadsheet/script files
- target product, landing URL, CTA, brand name, and required claims
- language, voice style, aspect ratio, platform, target duration
- whether the output needs full narration, sparse dialogue, subtitles, or music-only sections

If the product claims are current or external, verify them from official pages before using metrics, URLs, pricing, features, or compliance-sensitive language.

### 2. Reference Access And Breakdown

Use the least fragile path first:

1. Try metadata/download tools such as `yt-dlp` when suitable.
2. Use browser or Chrome inspection for dynamic/social pages.
3. Use screenshots, user-provided frames, or visible metadata when playback is blocked.
4. Extract frames or create a contact sheet when video access is available.

Write `notes/breakdown.md` with:

- hook, scene sequence, pacing, transitions
- visual palette, typography style, card/layout grammar
- audio structure: narration, dialogue, music, sound effects, silence
- reusable principles for the new video
- access limitations and evidence source: script, screenshots, browser observation, downloaded frames, etc.

### 3. Script And Storyboard

Write `notes/storyboard.md` before production. Include:

- exact duration, FPS, resolution
- scene timeline with start/end times
- scene purpose and on-screen copy
- voiceover or dialogue script
- music direction and ducking strategy
- source-backed product claims and URLs
- image generation prompts when needed

Keep product videos dense and specific: show the actual scenario, UI, user, or workflow. Avoid generic landing-page hero pacing when the target is a short ad or social video.

### 4. Visual Asset Production

For scenario videos, generate scene images only when they materially improve the video. Prompts should specify:

- realistic scenario and user role
- lighting, camera, composition, aspect ratio
- no text, no logos, no watermarks unless the user explicitly provides brand assets
- consistent style across all scene images

Copy generated files into `assets/generated/` and the Remotion `public/` tree. Create contact sheets or view representative images before rendering.

### 5. Music

Find real licensed music, not placeholder generated tones, unless the user explicitly accepts procedural music.

Music selection checklist:

- Prefer official source pages such as Mixkit, Pixabay, YouTube Audio Library, Free Music Archive, or a user-provided licensed asset.
- Verify current license terms from the source page before use.
- Prefer tracks that are long enough for the video or can loop cleanly.
- Store original download under `remotion/public/audio/source/`.
- Store the Remotion-ready asset under `remotion/public/audio/`.
- Record title, artist, source page, direct asset URL, license URL/wording, and restrictions in notes.

For music under dialogue, implement ducking. Typical starting volumes:

- music-only sections: `0.16` to `0.24`
- under voice/dialogue: `0.06` to `0.10`
- fade in during first second and fade out over the final 1-2 seconds

### 6. Voiceover And Dialogue

Choose audio structure based on the brief:

- full narration for explainers
- sparse customer-service dialogue for scenario-led product videos
- music-only with captions when the video is meant for silent autoplay

Use the best available voice source. If only local tools are available, macOS `say` can create a draft voice, but label it as system TTS. Keep each spoken clip short enough for its scene and verify clip duration with `ffprobe`.

Store voice assets in `remotion/public/audio/`, using clear names such as:

```text
voiceover.wav
agent-flight.wav
agent-medical.wav
```

### 7. Remotion Production

Use a standalone Remotion project inside the job folder unless an existing project is clearly intended. Follow existing code style.

Implementation expectations:

- define stable composition duration, FPS, width, and height
- use `Sequence` for scene-local audio and visual timing
- keep text readable at 1x playback
- avoid dark style drift if the requested style is white/light
- keep background music and dialogue separate
- avoid nested card-heavy layouts unless the reference requires them

Render the main output to:

```text
renders/<slug>.mp4
```

### 8. Verification

Before claiming completion, run:

- `npm run typecheck` or equivalent build check
- Remotion render command
- `ffprobe` on the final MP4 for duration, video dimensions, frame rate, audio codec, sample rate, and channels
- extract still frames from at least opening, one scenario, one technical/product scene, and closing
- inspect stills for black frames, overlapping text, missing assets, wrong background style, or unreadable UI

If audio changed, verify source audio durations and final output audio track. If music was sourced externally, verify local file presence and note the source/license.

## Final Response Pattern

Keep the user-facing summary short:

- final MP4 path with a local video embed
- what changed: visuals, music, voice/dialogue, CTA
- verification results
- music/license source and any restrictions
- unresolved access limitations, if any

Do not bury failed verification. If something is unresolved, say exactly which step failed and what can still be done.
