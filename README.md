# Corazones y Apuestas — Playable MVP

**NOVA FORGE STUDIO · couples board game (working title)**
Engine codename: **NOVA Board Engine (NBE)** · Final internal-review build.

A premium-feeling 3D couples board game. Two players, **single-device** (pass-and-play)
**or two-device online** (room code, no backend). Spanish UI. Custom prompt editor.

---

## What's in this build

- **Two play modes**
  - *Un solo teléfono* — both players share one device; a "blind pass" veil keeps the guess secret.
  - *Dos teléfonos* — peer-to-peer over WebRTC (PeerJS), room-code based, **no server to run**. Each player uses their own phone; the guess is naturally private. The host device is the authoritative game state; the guest is a thin client sending intents.
- **Signature mechanic** — *Revelar y adivinar* (Reveal & Guess) with dual-track scoring: personal **Chispas** (Sparks) + a shared **Conexión** (Connection) meter. No-loser end framing.
- **3D board** — bigger, touch-controlled: one finger orbits, two fingers pinch-zoom. Tiles show their **type symbol** (❓ Pregunta · 🎭 Reto · 🔥 Apuesta · 💛 Momento · 🎁 Premio) so you know what awaits *before* you land — without spoiling the content.
- **Avatars** — pick an emoji or **use your own photo**; pieces show a glowing ring + avatar.
- **Prompt editor** — choose which prompts are active, create/edit/delete your own, with on-device persistence and a backup/import (export text).
- **Engine/content split** (GDD §4) realized in one file: `MODE_PACK` + `Content` (data) · `Engine` + `hostApply`/`viewForCat` (runtime) · 3D/UI (presentation). A view-sync state machine drives both play modes from the same logic.

## Honest scope (this is a prototype)

- The 3D library and (for online play) the WebRTC broker load from CDN — **internet is required** on first load; online play also needs the network to allow a WebRTC connection (works on most home/mobile networks, not guaranteed on every restricted network).
- **Photo avatars** use your actual photo as the avatar image. *AI-generated 3D avatars from a photo* remain a future, backend-dependent feature.
- In online play, the **active deck is the host's** (the host resolves all prompts). Each device still keeps its own editable deck for when it hosts.
- Persistence is **per-device** (browser storage). Use the editor's backup/import to move custom prompts between phones. Cross-device profile sync is a post-MVP, backend feature.

## Run locally

No build step. Open `index.html` in a modern browser (double-click), or serve the folder:

```
npx serve .        # or: python3 -m http.server
```

## Publish to GitHub Pages

1. Put `index.html` at the **repo root**.
2. Commit. (Replacing an existing `index.html` just overwrites it.)
3. Settings → Pages → Deploy from branch → `main` / `/root` → Save.
4. After ~1 min the site is live at `https://<user>.github.io/<repo>/`.

**Two-device play:** both phones open the **same** published URL. One taps *Dos teléfonos → Crear sala* and reads out the 4-letter code; the other taps *Unirme* and enters it.

## Deploy (optional)

As a static site it can also be hosted on Netlify or a Railway static service. A 3D
mobile *product* would not use Railway as its runtime; Railway is reserved for future
backend/web services (e.g. profile sync or a content API), which this build doesn't need.

## QA notes (final pass)

Automated checks run before delivery: JS syntax validated; a 2000-game headless
simulation confirmed every match terminates, averages ~14 turns, and reaches the
lap-win before the turn cap ~99% of the time. Four logic issues found and fixed:
turn-counter double increment, online handshake message ordering, lobby role state
on avatar/color change, and win-preview/authoritative-win alignment.

*A NOVA FORGE STUDIO product. Built to be the foundation, not a one-off.*
