# PoE Logbook Accumulator

A helper tool for **Path of Exile 2 Expedition** that automatically scans your logbook's Island Rumours tooltip and rates the logbook's overall quality in real time.

---

## What it does

When you hover over a logbook in-game and press the scan hotkey, the tool reads the **Island Rumours** listed in the tooltip. It then looks up each rumour in a local database, scores them, and displays a tier rating for the whole logbook — so you can quickly decide whether it's worth using.

---

## Features

- **Hotkey scanning** — hover over a logbook icon and press `F11` to scan, `F12` to reset (both configurable)
- **Two detection methods:**
  - **OCR** (EasyOCR) — reads the text directly from the screen; works without pre-made templates
  - **Template matching** — faster, pixel-perfect matching using reference images (works best with 2k res)
- **Tier rating system** — each rumour has a score; the whole logbook gets rated `D 💀` through `S+ 👑`
- **Priority mode** — boosts the score of either maps or bosses, depending on what you're farming
- **Two display modes:**
  - **Advanced** — full breakdown per rumour with tier, destination, and score
  - **Simple** — section-level summary only (maps / unique maps / bosses)
- **Always-on-top window** — stays visible while you play
- **Auto-update check** — checks GitHub for new releases on startup
- **Persistent config** — all settings saved to `config.json`

---


## Getting started

1. Clone or download the repository.
2. Make sure `rumors_db.json` is in the **same folder** as `scanner.pyw`.
3. Run:
4. In-game, hover your cursor over a logbook's ship icon.
5. Press `F11` — the tool captures the area above your cursor and identifies the rumours.
6. Press `F12` to clear the current results and start fresh.

---

## Tier system

Logbooks are rated based on the number of rumours and their average score:

| Tier | Requirement |
|------|-------------|
| S+ 👑 | 6+ rumours, avg ≥ 4.0 |
| S 🔥 | 5+ rumours, avg ≥ 3.7 |
| A+ 🚀 | 4+ rumours, avg ≥ 3.5 |
| A 👍 | 4+ rumours, avg ≥ 3.0 |
| B+ 👌 | 3+ rumours, avg ≥ 2.8 |
| B 😐 | 3+ rumours, avg ≥ 2.2 |
| C 📉 | 2+ rumours, avg ≥ 1.8 |
| D 💀 | everything else |

The final score also gets a small bonus for diversity (mix of map/unique/boss rumours) and the presence of high-tier individual rumours.

---

## Rumour database (`rumors_db.json`)

Each entry looks like this:

```json
"Fallen Stars": {
    "type": "map",
    "score": 6,
    "tier": "S+",
    "desc": "Moor [Runestones]"
}
```

- `type` — `"map"`, `"unique"`, or `"boss"`
- `score` — raw value used for tier calculation (1–6)
- `tier` — individual rumour tier label
- `desc` — destination map and notable modifier

You can edit this file freely to add or update rumours.

---

## Settings

Open the ⚙ settings panel inside the app to change:

- Scan hotkey and reset hotkey
- Detection method (OCR / Template)
- Priority mode (Maps / Bosses)
- Display mode (Simple / Advanced)
- Scan area dimensions and offset (for non-standard resolutions)
- Debug logging on/off

All settings are saved automatically to `config.json`.

---

## Scan area calibration

If the tool isn't capturing the tooltip correctly (e.g. on ultrawide or high-DPI displays), use the **calibration mode** in settings to adjust the capture width, height, and offset until the debug screenshot (`debug_screenshot_ocr.png`) shows the tooltip cleanly.

---

## Logging

When logging is enabled, every scan is written to `scan_log.txt` in the app folder. This includes the raw OCR output, each match attempt, and the final result — useful for debugging missed or wrong detections.

---
