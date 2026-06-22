# Numerocket 🚀📈

A 2D Flappy Bird clone with a **Numerai data-science tournament theme**. Built with vanilla HTML5, CSS, and the Canvas API — zero dependencies, deployable anywhere.

Navigate a pixel-art alligator with a rocket launcher through stock-chart obstacle bars set against a scrolling Tokyo cityscape. Each gap you clear scores `1 NMR ≈ $1`. Hit a bar or the ground and it's Game Over.

## Play

Open `index.html` in any modern browser.

| Control | Action |
|---------|--------|
| **Spacebar** | Jump / Start |
| **Click** | Jump / Start |
| **Tap (mobile)** | Jump / Start |

- Menu shows your **ATH (All-Time High)** score above the title
- Game Over → Menu → Start (no instant restart)

## Visual Theme

- **Background:** Parallax-scrolling Tokyo cityscape at night with stock chart overlay (`background.jpg`, 1200×600)
- **Obstacles:** Candlestick-chart bars with two-tone green gradient (`#00e676` → `#009624`), mirrored direction so light side faces the gap, black border + wicks
- **Player:** Pixel-art alligator in hoodie with rocket launcher (`player.png`, 120×120 visual, 80×80 collision hitbox)
- **Effects:** Sci-fi exhaust smoke trail (radial-gradient particles), tier-coloured player glow disc, dual shockwave rings on level-up, Web Audio chiptune SFX, CRT scanline overlay, gentle screen shake on death
- **Typography:** Courier New monospace — terminal/data-science aesthetic
- **Display:** Auto-resizing canvas fills viewport height at 2:3 ratio, DPR-aware for Retina sharpness

## Customization

All gameplay constants are at the top of the `<script>` section in `index.html`:

| Constant | Default | Effect |
|----------|---------|--------|
| `GRAVITY` | 0.5 | Falling speed (higher = faster fall) |
| `JUMP_VELOCITY` | -8 | Jump strength (negative = upward) |
| `GAP_SIZE_INITIAL_MIN` | 250 | Starting minimum gap between bars (random range) |
| `GAP_SIZE_INITIAL_MAX` | 270 | Starting maximum gap between bars |
| `GAP_SIZE_FLOOR_MIN` | 220 | Hard floor: smallest minimum gap (scales down with score) |
| `GAP_SIZE_FLOOR_MAX` | 240 | Hard floor: smallest maximum gap |
| `GAP_SCALE_INTERVAL` | 5 | Obstacles per gap-shrink step |
| `GAP_SCALE_STEP` | 2 | Pixels gap shrinks each interval |
| `MIN_GAP_DISTANCE` | 100 | Minimum vertical distance between consecutive gaps |
| `COLLISION_PADDING` (in `checkCollision`) | 8 | Collision fairness — higher = easier to dodge |
| `TIER_INTERVAL` | 10 | Score per difficulty tier promotion |
| `SPAWN_INTERVAL_MIN` | 90 | Minimum frames between obstacle spawns |
| `SPAWN_INTERVAL_MAX` | 120 | Maximum frames between obstacle spawns |

**Difficulty tiers:** Apprentice → Contributor → Researcher → Expert → Master → Grandmaster — each increases obstacle speed and changes player glow colour.

## Swapping Assets

Assets live in the `assets/` folder. Edit the source paths at the top of the game script:

```javascript
const PLAYER_IMAGE_SRC = 'assets/player.png';      // 120×120 RGBA PNG
const BACKGROUND_IMAGE_SRC = 'assets/background.jpg'; // wide panoramic, auto-scaled
const OBSTACLE_IMAGE_SRC = null;                     // set to replace candlestick bars
```

- **Player:** Auto-scaled from source dimensions, collision is always 80×80 centered in visual
- **Background:** Auto-detected dimensions, fills canvas height, scrolls at 30% of obstacle speed with seamless wrap

## Deployment (GitHub Pages)

```bash
git add .
git commit -m "v0.5"
git push origin main
```

Then in your repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → main, /root** and save. Your site will be live at `https://<username>.github.io/numerocket/`.

## Changelog

### v0.6.4 — Obstacle skin swaps + polish (current)

- 🖼️ **Obstacle skin swaps** — ~12% of non-red obstacles render with sprite-based art (`column_rc_top.png` / `column_rc_bot.png`) instead of gradient candlesticks, at natural size clipped to bar bounds
- 🎨 **3px black outline** — sprite-edge outline via pre-rendered black sprite offset blit (replaced `brightness(0)` filter for iOS Safari compatibility)
- 🟢 **Green start** — first 2 obstacles always green, no skin, for a smooth opening
- 📊 **Minimum bar height** — bumped to 90px for better sprite visibility on short bars
- 🔤 **Tier symbols updated** — Apprentice=-, Contributor=●, Researcher=▲, Expert=■, Master=◆, Grandmaster=★
- 🏷️ Version footer bumped to v0.6.4

### v0.6.3 — Red Streak: 3 red bars per tier

- 🔴 **Red Streak** — 3 red obstacles appear in every tier at a random position (bars 2-5), with tighter spawn interval (65-85 frames) for a sudden burst of pace
- 🟢 **Green start** — first 3 obstacles in Apprentice tier are always green for a smooth opening
- 📐 **Clustered gaps** — red bar gaps stay at the same height (no drift), making them easier to navigate
- 🏷️ Version footer bumped to v0.6.3

### v0.6.2 — Tier-coloured exhaust & glow

- 🔥 **Aggressive smoke tint** — exhaust smoke stages tinted 80% with tier colour, fire core stays orange
- 🔥 **Dual-radial glow** — every particle gets a warm orange centre + tier-coloured outer rim via pre-rendered glow overlays
- 🎆 **Tier-coloured additive sparks** — continuous stream of tier-coloured embers from rocket nozzle
- 🏷️ Version footer bumped to v0.6.2

### v0.6.1 — Bugfixes, accessibility, code quality & polish

**Phase 1 (Bugfixes):**
- 🐛 **Version footer ghost fixed** — stroked "v0.5" text removed, now renders clean "v0.6.1"
- 🐛 **Score-pop rainbow glow fixed** — `rainbowHue` now cycles through colours instead of staying red
- 🐛 **Dead code removed** — unused `game.streaks` and orphaned `game.ripples` rendering cleaned out
- 🐛 **Alternative jump keys added** — Arrow Up and `W` now work alongside Space
- 🐛 **Right-click context menu blocked** on canvas
- 🐛 **Touch input hardened** — `{ passive: false }` on touchstart prevents Chrome console warning
- 🐛 **Audio creation hardened** — `new AudioContext()` wrapped in try/catch
- 🐛 **Image loading errors logged** — `onerror` handlers added for player and background images

**Phase 2 (Accessibility):**
- ♿ **ARIA labels** — `role="img"` and `aria-label` added to canvas for screen readers
- ♿ **prefers-reduced-motion** — screen shake, CRT scanlines, and particles now respect the user's motion preference

**Phase 3 (Code Quality & Mobile):**
- 🔧 **Magic number extracted** — `16.667` replaced with named `DT_TO_MS` constant
- 🔧 **getTier() caching** — redundant per-frame calls eliminated
- 📱 **touch-action: manipulation** — CSS added to eliminate 300ms mobile tap delay
- 📱 **Landscape overlay** — prompts users to rotate to portrait on narrow screens
- 🔧 **Resize debounced** — `resizeCanvas` now debounced at 100ms to prevent flicker
- 🔧 **bgOffset clamped** — unbounded growth wrapped with modulo

**Phase 4 (Performance & Polish):**
- 🎨 **Particle gradients cached** — pre-rendered gradient palette replaces 12,000 per-frame gradient creations
- 🎨 **CRT scanlines pre-rendered** — offscreen canvas replaces 150 draw calls with single `drawImage`
- 📱 **Minimum canvas size guard** — clamped at 200×300 for small viewports
- ♿ **Tier-name symbols** — geometric shapes alongside tier names for colour-blind accessibility
- 📱 **PWA manifest** — `manifest.webmanifest` + iOS `apple-mobile-web-app-capable` meta tags
- 🏷️ Version footer bumped to v0.6.1

### v0.6 — Game Over Panel Refinement + Menu Refresh + Visual Overhaul
- 🔲 **Heavier obstacle outlines** — candlestick black border increased 2→3px for better visibility
- 🏆 **Menu: "Best Score" label** — ATH on menu screen renamed to "Best Score: 1 NMR ≈ $" and moved to top of screen (30px from top edge)
- 🖼️ **New background** — `assets/background.jpg` replaced with an updated tile
- 🏷️ Version footer bumped to v0.6
- 🟣 **Tier-coloured player glow disc** — radial gradient behind player sprite (24% steady, 60% on level-up), guaranteed visible on all devices
- 🔵 **Dual shockwave rings** — two concentric tier-coloured rings on level-up (main 220px, secondary 180px staggered), sweep over 35 frames with configurable per-ring alpha/width
- 🟠 **Screen flash fix** — warm orange tint now lasts 8 frames (~133ms) instead of <1 frame (unit mismatch bug)
- 🐛 **Ring timing fix** — shockwave rings now last 35 frames (~583ms) instead of 2 frames due to `dt * 16.667` unit mismatch; same bug fixed for screen flash
- 🎵 **Web Audio chiptune SFX** — jump (boing), score (triple blip), death (sad trombone), start arpeggio, level-up sweep

### v0.5 — Start Screen Overhaul + Repo Rename

- 🏙️ New seam-free background image — seamless tiling, no visible wrap seam
- 🔧 Background tile overlap reduced from 6px → 2px (cleaner with new image)
- 🚀 Browser tab icon changed to rocket emoji (inline SVG favicon)
- 🐊 Player alligator sprite displayed on start screen above title
- 🎬 Subtitle: "Ride the market and send NMR to the moon" (18px, white + black outline)
- 🏷️ "Prototype v0.5" version footer at bottom of menu (14px, 60% opacity, black outline)
- 📝 Customization table now documents `OVERLAP` constant
- 🔄 Repo renamed from `numerbird` → `numerocket`

**Bug fix (v0.5f1):** Fixed crash on start — `const tier = getTier()` was used 53 lines before its declaration (Temporal Dead Zone), causing `ReferenceError` when entering PLAYING state. Game now renders correctly in all states.

### v0.4 — Candlestick Gradients + Easier Collision

- 🟢 Green candlestick gradient: two-tone vertical gradient (`#00e676` → `#009624`)
- 🔄 Mirrored gradient — top bars light near gap, bottom bars light near gap
- 🎯 Collision padding increased (2 → 8) for noticeably easier gameplay

### v0.3 — Sci-fi Exhaust Smoke Trail

- ✨ Radial-gradient particle system replaces grey squares
- 🔥 Colour curve matched to sprite muzzle flash: `#FF8800` → `#FF5500` → dark/light gray → transparent
- 💨 Size grows 4-5px → 16px with staged expansion
- 🌪️ Turbulence jitter for natural billowing
- 🎯 Spawn position centred on rocket nozzle muzzle flash
- ⚡ 200 particle cap, ~100 steady-state

### v0.2 — Parallax + Retro Feel + Polished UX

- ✨ Parallax background (Tokyo cityscape at night with stock chart overlay)
- 🎨 Pixel-art alligator with rocket launcher (120×120 visual, 80×80 collision)
- 🔲 CRT scanline overlay and pixel-perfect rendering
- 📉 Score displays as `1 NMR ≈ $X` in-game and on Game Over
- 🏆 Session ATH tracking displayed on title screen
- 🎮 Proper menu flow (GAME_OVER → MENU → PLAYING)
- 📐 Auto-resize canvas with Retina DPR support
- 📊 Minimum 5% bar height on obstacles

### v0.1 — First Working Prototype

- Core gameplay loop with delta-time physics
- Stock-chart-bar obstacles with AABB collision
- Numerai diamond player placeholder
- Dark data-science grid background
- Desktop + mobile input
- Responsive canvas with CSS aspect-ratio scaling
- Zero dependencies — single `index.html` file

## Tech Stack

- **HTML5** — semantic structure
- **CSS3** — dark theme, responsive viewport, no-scroll layout
- **JavaScript** — Canvas 2D API with `requestAnimationFrame` game loop
- **Delta-time physics** — frame-rate-independent gravity and obstacle spawn timing
- **Zero dependencies** — no frameworks, no build tools, no npm

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.
