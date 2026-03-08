# CutList

> Browser-based cutting list optimizer using the guillotine algorithm with kerf-awareness for minimal material waste.

---

## Overview

CutList is a practical tool for optimizing how materials (boards, sheet stock, etc.) are cut to produce required pieces with minimal waste. It uses a guillotine cutting algorithm (rectangular cuts without rotation) and accounts for blade kerf (thickness of material removed during cutting).

**Use Case:** Woodworking, CNC routing, laser cutting, or any project requiring optimal cutting layouts from stock material.

---

## Features

- **Guillotine Algorithm** — Efficient rectangular cutting pattern generation
- **Kerf-Aware** — Accounts for blade thickness (customizable per-cut)
- **No Rotation** — Pieces maintain original orientation (for grain direction, symmetry, etc.)
- **JSON Input** — Specify pieces and stock dimensions as JSON
- **SVG Output** — Generates print-ready cutting diagrams
- **Interactive Web UI** — Browser-based with real-time previews
- **Customizable Parameters:**
  - Kerf width (in inches or custom units)
  - Gap multiplier (spacing between pieces)
  - Quantity multiplier (scale quantity for testing)
  - Edge trim (L/R/B/T adjustments for stock irregularities)
  - Render settings (DPI, font size for printing)
- **Print-Optimized** — Generates cutting sheets ready for print with page breaks
- **No Upload Required** — All computation runs locally in browser

---

## How to Use

### 1. Open the Tool

Open `index.html` in a modern web browser (no server required).

### 2. Define Pieces (JSON)

Enter pieces in the "Pieces JSON" field:

```json
[
  {"name": "Leg", "width": 2.5, "height": 18, "qty": 4},
  {"name": "Top", "width": 24, "height": 18, "qty": 1},
  {"name": "Shelf", "width": 23, "height": 12, "qty": 2}
]
```

### 3. Define Stock (JSON)

Enter available stock material:

```json
[
  {"name": "1x24 Board", "width": 24, "height": 96, "qty": 2}
]
```

### 4. Configure Settings

- **Kerf** — Blade thickness (e.g., 0.125" for typical saw blade)
- **Gap Mult** — Extra spacing between cuts (1.0 = kerf width, 0.5 = half kerf, etc.)
- **Qty Mult** — Scale quantities for testing (useful for multiple copies)
- **Trim** — Account for rough edges on stock

### 5. Click "Pack"

Algorithm optimizes cutting layout and displays result.

### 6. Export & Print

- **Print** — Print-ready cutting diagram (scales to Letter or A4)
- **Export JSON** — Save results as JSON for archiving/sharing

---

## Configuration Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| Kerf | 0.125" | Blade thickness |
| Gap Mult | 1.0 | Multiplier for spacing between cuts |
| Qty Mult | 1.0 | Scale all quantities |
| Trim L/R/B/T | 0 | Remove from each edge of stock |
| Units/inch (UPI) | 40 | Pixels per inch for rendering |
| Font px | 11 | Label font size in pixels |
| Stroke px | 0.9 | Line thickness in pixels |

---

## Algorithm

Uses a **guillotine algorithm** for rectangular packing:
1. Start with stock dimensions
2. Place first piece in top-left
3. Divide remaining space into right and bottom regions
4. Recursively pack remaining pieces into available space
5. Account for kerf between cuts

**Constraint:** No piece rotation (useful for grain direction, aesthetics, CNC setup).

---

## Example Workflow

**Scenario:** Building a simple shelf unit from 1×12 boards

**Stock:** Three 1×12×48" boards

**Pieces Needed:**
- 2× Shelves (11.25" × 24")
- 4× Sides (11.25" × 36")
- 2× Backs (23.75" × 36")

**Settings:**
- Kerf: 0.125" (typical saw blade)
- Gap: 1.0 (full kerf spacing)

**Result:** CutList generates a diagram showing optimal cuts on each board, minimizing waste.

---

## Browser Compatibility

- Chrome/Chromium 90+
- Firefox 88+
- Safari 14+
- Edge 90+

(Requires modern ES6 JavaScript support)

---

## Tips

- **Print at correct scale** — Use 40 UPI for Letter/A4, adjust render DPI if needed
- **Test first** — Use Qty Mult = 1 to preview before cutting full quantities
- **Account for setup** — Use Trim values if boards have uneven edges
- **Label output** — Piece names appear in SVG diagram for reference
- **Multiple materials** — Define different stocks for different board dimensions

---

## License

Copyright © Walter Gordy
