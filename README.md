# Learn Colors

An interactive, single-page color education tool built to train your eye to see subtle differences between shades and understand how human vision perceives color.

**Live demo:** https://mankubhatt.github.io/colors/

---

## What's inside

### Color Families
Browse 8 color families (Reds, Blues, Greens, Purples, Cyans, Oranges, Browns, Grays) with 10 named shades each — from the lightest tint to the darkest tone. Hover any swatch to see its name, hex code, and RGB values.

### Side by Side
16 pairs of commonly confused colors placed directly next to each other — Crimson vs Scarlet, Navy vs Midnight Blue, Coral vs Salmon, and more. Proximity makes the differences visible.

### Gradients
8 smooth spectrum bars showing how a color transitions from light to dark, and how neighboring hues blend into each other.

### Color Quiz
Test yourself: given a hex code and a color swatch, can you pick the correct name from 4 options drawn from the same color family? Tracks your score across rounds.

### Color Blindness Simulator
Simulate 7 types of color vision deficiency side-by-side against normal vision:

| Type | Deficiency | Prevalence |
|---|---|---|
| Protanopia | No red cones (L) | ~1% of men |
| Deuteranopia | No green cones (M) | ~1% of men |
| Tritanopia | No blue cones (S) | ~0.01% |
| Achromatopsia | No cones at all | Very rare |
| Protanomaly | Weak red sensitivity | ~1% of men |
| Deuteranomaly | Weak green sensitivity | ~5% of men |

Also includes 4 **Ishihara-style self-test plates** generated on canvas — hidden numbers revealed only to those with normal color sensitivity in the tested channel.

### Light & Intensity
Drag a slider from Night to Noon Sun and watch four optical effects respond in real time:

- **Purkinje Effect** — At low light, rods dominate and blues appear relatively brighter than reds (rod peak: 507 nm vs cone peak: 555 nm)
- **Hunt Effect** — Colors appear most vivid at mid-range luminance; saturation drops at both dark and bright extremes
- **Bezold-Brücke Shift** — As luminance rises, reds shift toward yellow and blues shift toward cyan; two invariant hues (~478 nm cyan, ~572 nm yellow) stay stable
- **Stevens Effect** — Perceived contrast follows a power law (brightness ≈ L^0.33); dark/light differences feel more extreme in bright conditions

---

## Running locally

No build step. Just open the file:

```bash
open index.html
```
