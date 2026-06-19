# Numerbird 🐦📈

A 2D Flappy Bird clone with a **Numerai data-science theme**. Built with vanilla HTML5, CSS, and the Canvas API — zero dependencies, deployable anywhere.

Navigate a glowing diamond through volatile stock-market obstacle bars in a dark, data-grid arena. Each gap you clear scores a point. Hit a bar or the ground and it's Game Over.

## Gameplay

| Control | Action |
|---------|--------|
| **Spacebar** | Jump / Start / Restart |
| **Click** | Jump / Start / Restart |
| **Tap (mobile)** | Jump / Start / Restart |

- Guide the **Numerai diamond** through gaps in stock-chart obstacles
- Each gap passed = **1 point**
- Hit an obstacle or the ground → Game Over
- One press restarts immediately

## Visual Theme

- **Background:** Dark science-grid (`#0a0e17` with subtle 40px grid lines)
- **Obstacles:** Stock-market chart bars in teal/green (`#00d4aa`) with glowing borders and candle wicks
- **Player:** A red/orange Numerai diamond with glow effect
- **Typography:** Courier New monospace — terminal/data-science aesthetic

## Customization

All gameplay constants are at the top of the `<script>` section in `index.html`:

| Constant | Default | Effect |
|----------|---------|--------|
| `GRAVITY` | 0.5 | Falling speed (higher = faster fall) |
| `JUMP_VELOCITY` | -8 | Jump strength (negative = upward) |
| `SPEED` | 3 | Obstacle scroll speed |
| `GAP_SIZE` | 150 | Vertical gap between bars (smaller = harder) |
| `SPAWN_INTERVAL_MIN` | 90 | Minimum frames between obstacle spawns |
| `SPAWN_INTERVAL_MAX` | 120 | Maximum frames between obstacle spawns |

## Swapping Assets

To replace the placeholder graphics with custom sprites, edit the asset constants at the top of the game script:

```javascript
const PLAYER_IMAGE_SRC = null;     // ← set to URL/path of player sprite
const OBSTACLE_IMAGE_SRC = null;   // ← set to URL/path of obstacle sprite
const BACKGROUND_IMAGE_SRC = null; // ← set to URL/path of background image
```

When set to a valid image source, wire them into `drawGame()` in the rendering section to replace the canvas-drawn shapes.

## Deployment (GitHub Pages)

```bash
# Push to main branch
git add index.html README.md
git commit -m "Initial release"
git push origin main
```

Then in your repo **Settings → Pages → Build and deployment → Source: Deploy from a branch → main, /root** and save. Your site will be live at `https://<username>.github.io/numerbird/`.

## Changelog

### v0.1 — First Working Prototype

Initial release. Core gameplay loop is functional:

- Gravity-based player movement with jump on Space / tap / click
- Stock-chart-bar obstacles that spawn from the right and scroll left
- Score counter that increments on each gap passed
- AABB collision detection (obstacles + ground)
- Game Over screen with score and instant restart
- Three game states: MENU → PLAYING → GAME_OVER
- Dark data-science grid background
- Numerai diamond player placeholder (easy sprite swap)
- Frame-rate-independent physics (delta-time)
- Responsive canvas (desktop + mobile)
- Zero dependencies — single `index.html` file

## Tech Stack

- **HTML5** — semantic structure
- **CSS3** — dark theme, responsive viewport, no-scroll layout
- **JavaScript** — Canvas 2D API with `requestAnimationFrame` game loop
- **Delta-time physics** — frame-rate-independent gravity and obstacle spawn timing
- **Zero dependencies** — no frameworks, no build tools, no npm

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.