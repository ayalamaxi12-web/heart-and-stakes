# Heart &amp; Stakes — Core-Loop Prototype

**NOVA FORGE STUDIO · COUPLES BOARD GAME (working title)**
Engine codename: **NOVA Board Engine (NBE)**

---

## What this is (and is not)

This is a **playable, end-to-end prototype of the core gameplay loop** — built in Release Mode to get the game into your hands fast and validate that the loop is *fun* on a single shared device.

It is **not** the full production MVP described in the GDD. To be transparent about scope:

| In this prototype | Deferred to the real MVP (per GDD) |
|---|---|
| Full turn loop: roll → move → land → resolve → score → win → recap | Unity / store-grade 3D, haptics, full art & audio |
| Signature **Reveal &amp; Guess** mechanic with the **blind-pass** (phone hand-off) | All other modes (Romance, Hot, Adventure, Party, Trivia, Escape) |
| **Dual-track scoring** (personal Sparks + shared Connection meter) | Persistent Couple Profile, cosmetics, AI avatars |
| No-loser end framing | Cloud sync / profile resilience |
| Names + colors personalization | Localization, accessibility pass, full safety/consent system |
| A 3D board (Three.js) glowing on a dark table | Tuned content depth, anti-repetition at scale |
| A miniature of the GDD **engine/content split** (see below) | |

Two QA-critical findings from the GDD review are **already resolved here**: the
"private guess on a shared device" contradiction is solved by the **blind-pass**
ritual, and every sensitive/optional beat (wagers) is opt-in with a free,
penalty-less skip.

> Profile **persistence is intentionally absent** in this prototype (browser
> storage is out of scope here). Data resilience for the real personalization
> feature is a tracked MVP requirement, not a prototype concern.

---

## How to run locally

No build step. No install.

1. Open `index.html` in any modern browser (double-click works), **or** serve the folder:
   ```
   npx serve .          # or: python3 -m http.server
   ```
2. Hold the phone/tablet between two people and play.

> Internet is needed on first load for the Three.js library and fonts (loaded
> from CDN). To run fully offline, vendor `three.min.js` locally and swap the
> `<script>` / font `<link>` tags for local files.

**Best experience:** a phone or small tablet, portrait, two people in the same room.

---

## How to play

1. **Begin** → enter both names and pick a color each (or **Quick start**).
2. On your turn, **Roll the die** — your piece travels around the board.
3. The tile you land on decides what happens:
   - **Reveal &amp; Guess** — the *signature*. One partner secretly guesses the
     other's answer. The phone asks you to look away and hand it over (the
     **blind pass**). Both score: guessing right means you're *in sync*; a wild
     answer means you *surprised* each other — and that scores too. Nobody loses.
   - **In sync?** — a quick this-or-that; matching earns Sparks for both.
   - **Playful** — a light dare, judged by your partner.
   - **A quiet moment** — a scoreless connection beat.
   - **Wager** — optional stakes; saying no is always free.
   - **Reward** — a little Sparks gift.
4. Two scores rise together: your personal **Sparks** (the friendly rivalry) and
   the shared **Connection** meter (the thing you build *together*).
5. First piece around the board ends the round. The recap celebrates **both** of
   you — whoever led on Sparks, and whether you reached **Deep Connection**.

---

## The engine/content split (why this matters)

Open `index.html` and you'll find the JavaScript organized in three blocks that
mirror **GDD §4**:

- **`MODE_PACK`** — pure content: the board layout, the decks of prompts, the
  scoring profile and win condition, the theme. *This is data.*
- **`Engine`** — content-agnostic runtime: roll, advance, draw, score, win-check,
  turn handoff. *It knows nothing about romance or trivia.*
- **3D / UI** — presentation.

Swapping `MODE_PACK` for a different one (e.g. a Trivia or Adventure pack) would
change the game **without touching the engine** — the platform thesis, proven in
miniature. This is the seed of the future `forge` graduation candidate.

---

## Deployment note (Railway)

Per ADR-0001 and Release-Mode guidance, Railway deployment is **optional, not
blocking** for this prototype. As a static site it can be hosted anywhere
(GitHub Pages, Netlify, or a Railway static service). A 3D mobile *product* MVP
would not target Railway as its runtime — Railway is the studio's home for
backend/web services (e.g. a future profile-sync or content API), which this
prototype does not yet need.

---

## Status &amp; next steps

- **Phase:** built in Release Mode from Phase-2 design (GDD v0.1).
- **Recommended path forward:** validate the loop with a real couple, fold
  learnings back into **GDD v1.0**, then run the compressed Phases 3–7 (UX,
  Technical Architecture / stack ADR-0002, Visual Direction, Roadmap, GitHub
  setup) before the production MVP build.

*A NOVA FORGE STUDIO product. Built to be the foundation, not a one-off.*
