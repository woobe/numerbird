# Numerbird 🐊📈

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
- **Obstacles:** Stock-market chart bars in teal (`#00d4aa`) with glowing borders and candle wicks
- **Player:** Pixel-art alligator in hoodie with rocket launcher (`player.png`, 120×120 visual, 80×80 collision hitbox)
- **Effects:** CRT scanline overlay, grey soft-glow edge on player, gentle screen shake on death
- **Typography:** Courier New monospace — terminal/data-science aesthetic
- **Display:** Auto-resizing canvas fills viewport height at 2:3 ratio, DPR-aware for Retina sharpness

## Customization

All gameplay constants are at the top of the `<script>` section in `index.html`:

| Constant | Default | Effect |
|----------|---------|--------|
| `GRAVITY` | 0.5 | Falling speed (higher = faster fall) |
| `JUMP_VELOCITY` | -8 | Jump strength (negative = upward) |
| `SPEED` | 3 | Obstacle scroll speed |
| `GAP_SIZE` | 270 | Vertical gap between bars (smaller = harder) |
| `SPAWN_INTERVAL_MIN` | 90 | Minimum frames between obstacle spawns |
| `SPAWN_INTERVAL_MAX` | 120 | Maximum frames between obstacle spawns |

## Swapping Assets

Assets live in the `assets/` folder. Edit the source paths at the top of the game script:

```javascript
const PLAYER_IMAGE_SRC = 'assets/player.png';      // 120×120 RGBA PNG
const BACKGROUND_IMAGE_SRC = 'assets/background.jpg'; // wide panoramic, auto-scaled
const OBSTACLE_IMAGE_SRC = null;                     // set to replace teal bars
```

- **Player:** Auto-scaled from source dimensions, collision is always 80×80 centered in visual
- **Background:** Auto-detected dimensions, fills canvas height, scrolls at 30% of obstacle speed with seamless wrap

## Deployment (GitHub Pages)

```bash
git add .
git commit -m "v0.2"
git push origin main
```

Then in your repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → main, /root** and save. Your site will be live at `https://<username>.github.io/numerbird/`.

## Changelog

### v0.3 — Sci-fi Exhaust Smoke Trail (current)

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
