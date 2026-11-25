---
name: copycat-story-video
description: Creates ~65-second vertical (9:16) 3D low-poly animated story videos in the warm "tinyplanetlab" TikTok style, for any user topic, with Bahasa Melayu captions by default. Use when the user wants an animated story video, a TikTok/Reels short, or mentions the copycat story style. Output is ONE self-contained HTML file (Three.js) that plays and records the video in the browser. No installs required.
---

# Copycat-Style 3D Story Video

Turn any topic into a ~65s vertical 3D story video with the exact style DNA in
references/style-guide.md. You are the director; assets/engine.html is the studio.
Never rewrite the engine — only inject a story config into it.

## Workflow — follow in order

### Step 1 — Intake (ask only what's missing)
- Topic + EXACT title wording (keep the user's grammar). Pick 1 highlight word (gold).
- Characters — offer this picker, default = 1:
  1. Kau dewasa + kau umur 6 (default)
  2. Abang/kakak + adik
  3. Dua kawan baik
  4. Mak/ayah + anak
  5. Kau + kucing/anjing
  6. Custom (user describe)
- Caption language: ms (default) / manglish / en
- Duration: 65s default (allowed 60–70s)

### Step 2 — Beat sheet (CHECKPOINT — wait for user approval)
Map the topic onto the 9 beats in references/beat-template.md.
Write captions per references/caption-voice.md.
Show the user a table: time | visual | caption | HUD. Do NOT build until approved.

### Step 3 — Build story.json
Schema (engine contract — do not rename keys):

{
  "meta": { "title": "...", "highlight": "...", "fps": 30, "audio": true },
  "characters": {
    "a": { "name":"...", "height":1.0, "skin":"#F2C49B", "hair":"bob",
           "hairColor":"#4A2E1E", "shirt":"#E8B33C", "shirtStyle":"collar",
           "pants":"#4A6B8A", "bag":"#3E8E8C" },
    "b": { "height":0.62, "shirtStyle":"stripes", "...":"..." }
  },
  "shots": [
    { "id":"hook", "start":0, "end":6, "set":"bathroom",
      "camera":{ "pos":[0,1.4,4.2], "look":[0,1.15,0], "push":0.06 },
      "actors":[
        { "char":"a", "pos":[-0.55,0], "rot":0, "action":"brush", "emotion":"tired" },
        { "char":"b", "pos":[0.55,0], "rot":0, "action":"brush", "emotion":"excited", "delay":0.15 }
      ],
      "caption":"...", "caption2":null,
      "hud":{ "l1":"UMUR 6", "l2":"GEMBIRA 100%" },
      "transition":"cut" }
  ],
  "endcard": { "line":"...", "cta":"...", "question":"..." }
}

Valid sets: bathroom, kitchen, hallway, door, room_night, outside_rain
Valid actions: idle, brush, pour, eat, walk, run, wave, phone, hug, jump, fade, stand
Valid emotions: neutral, happy, excited, annoyed, tired, sad, soft
Valid hair: bob, short, long, bun
Valid shirtStyle: collar, stripes, plain
Actor pos = [x, z]; rot = degrees (0 = facing camera). "delay" = sync-gag offset (0–0.2s).
"push" = slow dolly-in fraction over the shot (0 = static). caption2 = optional second
line shown in the last 40% of the shot. hud = optional, null if none.

### Step 4 — Build the HTML
1. Read assets/engine.html
2. Replace exactly the token  /*__STORY_JSON__*/null  with the JSON (ensure_ascii=False)
3. Save as <topic-slug>.html and give the user the downloadable file.
   Fallback if file output is unavailable: print the FULL html in one code block
   with instructions to save as .html (UTF-8).

### Step 5 — Delivery instructions (always include)
1. Double-click the .html → opens in Chrome/Edge (no install needed)
2. Press ▶ Preview to watch; press ● Record to capture (real-time ~65s, keep tab visible)
3. Video auto-downloads. If it saves .webm and you want TikTok: import to CapCut →
   export mp4 → add trending sound in CapCut/TikTok (engine audio is a soft ambient bed only).

### Step 6 — QC checklist (verify before delivering)
- [ ] 9 beats, total 60–70s; first & last shot mirror the SAME set + action (loop)
- [ ] Captions lowercase, ≤ ~40 chars each, "kau" voice, Malay default
- [ ] Title highlight word set; NO handle/watermark anywhere
- [ ] Citation is REAL (you are confident it exists) — otherwise use a plain true
      statement with no citation. NEVER fabricate a study.
- [ ] story.json parses; every shot uses valid sets/actions/emotions/chars

## Hard rules
- Never fabricate citations, statistics, or studies.
- Never add watermarks, handles, or TikTok logos.
- Keep the user's exact title wording, even if grammatically quirky.
- Emotional arc is mandatory: annoying/funny → separation → longing → reunion → role reversal.
