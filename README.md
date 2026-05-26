# TheEclipse_SkullportEscape
Pirate themed treasure hunt
# ☠ SKULLPORT ESCAPE — Pirate's Eye
Published link: https://v0-skullport-escape.vercel.app/
A single-file, browser-based 3D stealth game built with [Three.js](https://threejs.org/) and the Web Audio API. No build tools, no dependencies to install — just open the HTML file.

---

## Gameplay

You are a cursed pirate. Haunted frog-demons stalk every shadow. Your goal each level is to:

1. **Collect 2 Keys and 1 Gem** scattered around the arena.
2. **Insert the Gem into the correct key** (a 50/50 puzzle — wrong choice triggers an alarm).
3. **Grab the Treasure Chest** once the gem-key is forged.
4. **Reach the Exit** before your Panic Meter fills to 100%.

---

## Controls

| Key | Action |
|---|---|
| `W A S D` / Arrow Keys | Move |
| `Shift` (hold) | Sneak (slower, quieter) |
| `Space` | Crouch / Hide |
| `E` | Interact (pick up items, open boxes, insert gem) |
| `C` | Cycle camera mode |
| `M` | Toggle minimap |

---

## HUD Elements

- **Score** — increases on pickups, level completions, and surviving guards.
- **Level** — current level (1–5).
- **Keys & Gem slots** — shows which items have been collected (top centre).
- **Panic Meter** — fills when guards spot you or the demon gets close. Reaches 100% → Game Over.
- **Noise Indicator** — vertical bar on the left; rises when running, triggers guard alertness.
- **Minimap** (bottom-right) — shows your position (green), keys (gold), gem (purple), treasure (orange), exit (green), guards (red/orange by alert state), and ship boxes (brown).
- **Mission Notification** (top-right) — animated objective card, updates when goals change.
- **Camera Badge** (top-right) — shows current camera mode.
- **Spotted Indicator** — flashes `👁 SEEN!` when a guard has line-of-sight on you.
- **Carrying Banner** (bottom-centre) — appears when you're hauling the treasure.

---

## Camera Modes (press `C` to cycle)

| Mode | Description |
|---|---|
| **Overhead** | Top-down follow camera |
| **Shoulder** | Third-person over-the-shoulder |
| **Pirate's Eye** | First-person view from the player |

---

## Levels

| # | Name | Theme | Guards |
|---|---|---|---|
| 1 | Port Skullport | Port & Ship | 2 |
| 2 | Cursed Seashore | Seashore | 4 |
| 3 | The Great Hall | Multi-floor Hall | 5 |
| 4 | The Dark Forest | Forest | 6 |
| 5 | Pyramid of the Damned | Ancient Temple | 7 |

Difficulty scales per level: guards move faster, have wider vision cones, the panic meter rises quicker, and the ambient audio becomes more ominous.



### Guards
- Patrol set waypoints; speed and vision increase each level.
- Have a cone of vision — crouch or hide in shadows to avoid detection.
- Alert level is visualised on the minimap (green → orange → red).
- Spotting you raises the Panic Meter and triggers a `⚠ SPOTTED!` screen flash.

### The Demon Frog
- Spawns mid-game and actively hunts the player.
- Visible as a green sprite (canvas-processed from a JPEG with background removal).
- Getting close triggers an escalating heartbeat audio effect and a demon warning overlay.
- Causes heavy panic increase on contact.

---

## Hiding Mechanics

- **Crouch** (`Space`) reduces your noise footprint and panic rise rate.
- **Sneak** (`Shift`) slows movement but dramatically reduces footstep noise.
- **Hiding spots** (barrels, crates, shadows) are scattered around each arena — move into one and crouch to become nearly invisible to guards.

---

## Sound Engine

All audio is **procedurally generated** using the Web Audio API — no audio files are loaded. Sounds include:

- Looping ambient ocean/wind/dungeon atmosphere (theme changes per level)
- Footsteps (run vs. sneak vs. crouch)
- Guard alert stings
- Heartbeat (scales with panic and demon proximity, with sub-bass thump + crackle layers)
- Demon croak (sawtooth sweep + wet noise + high screech)
- Friendly frog-pet chirp (periodic ribbit from your shoulder companion)
- Gem insertion shimmer chord
- Wrong key buzz
- Level start boom
- Game over descending horn

   ├── Minimap      Per-frame 2D canvas draw
    └── Game loop    requestAnimationFrame — update → render
```
