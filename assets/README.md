# SSX Asset Slots

Drop PNG files here. The engine auto-swaps from placeholder to art as soon as the file loads.

---

## `base.png` — Background painting

| Property | Value |
|----------|-------|
| Role | Full scene background, artist-painted at SSX camera angle |
| Dimensions | 1068 × 600 px (matches VIEW_W × VIEW_H exactly) |
| Draw order | First — behind all sprites |
| Camera | Painted at SSX 33° tilt (TILE_HALF_H = 21). If you change TILE_HALF_H, repaint. |
| Fallback | Procedural 14×14 isometric tile grid |

---

## `spritesheet.png` — Player character

| Property | Value |
|----------|-------|
| Layout | 4 rows × 2 columns |
| Frame size | FRAME_W × FRAME_H (32 × 48 px default — change constants in index.html) |
| Total size | 64 × 192 px at defaults |
| Row 0 | Facing DOWN |
| Row 1 | Facing UP |
| Row 2 | Facing LEFT |
| Row 3 | Facing RIGHT |
| Column 0 | Idle frame |
| Column 1 | Walk frame |
| Anchor | Sprite bottom-center aligns to player world position |
| Fallback | Gold glowing isometric diamond |

---

## Object sprites

Each object in `sceneObjects[]` has an `id` field. Drop a PNG named `<id>.png` here.

| File | Object | w × h | anchorY |
|------|--------|--------|---------|
| `obj_console.png` | Terminal console | 80 × 90 px | 78 px from top |
| `obj_crate.png` | Storage crate | 60 × 70 px | 60 px from top |

**anchorY** = pixel distance from the TOP of the sprite image to the point where the object touches the floor tile. This is used to position the sprite correctly in world space. If your sprite has transparent padding at the bottom, measure to the actual base contact point, not the image edge.

---

## Adding new objects

1. Add an entry to `sceneObjects[]` in `index.html` with the correct `id`, `worldX/Y`, `w`, `h`, `anchorY`.
2. Call `loadImg('your_id', 'assets/your_id.png')` near the other `loadImg` calls.
3. Drop the PNG here — engine swaps automatically on next load.

---

## Spritesheet painting guide

The SSX camera tilts at 33° (controlled by TILE_HALF_H = 21 in index.html). When painting character sprites:
- The character should appear to stand on an isometric floor painted at this same angle.
- Sprites face four cardinal directions in isometric perspective (not top-down).
- Keep the idle and walk frames visually consistent in anchor position — the floor contact point should not drift between frames.
