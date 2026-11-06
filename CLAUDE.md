# colorwerk● website

Marketing site for colorwerk●, a Kreuzberg (Berlin) studio making Garmin Connect IQ watch faces.
Owner: Jim — designer, not a coder. Works fast and iteratively. Keep changes small, explain in a sentence.

## Stack
- Plain static site: `index.html` with all CSS + JS inline, images in `assets/`. No build step, no framework.
- Hosted on GitHub Pages (serves the repo root; `.nojekyll` stops Jekyll processing).
- Font: Albert Sans (Google Fonts).
- Preview locally: `python3 -m http.server` in this folder → http://localhost:8000

## Page structure (top to bottom)
hero (photo + live wall clock) → intro → Pro faces (4-up) → Kreuzberg photo band → Free faces (scrolling rail) → alerts sign-up → footer

## Key files
- `assets/hero-day.jpg`, `assets/hero-night.jpg` — hero photo, day and night grade. Wall clock is an SVG drawn over it.
- `assets/watches/*.webp` — transparent device templates (Fenix 9 ×4 for Pro, `free-black` for Free).
  All share one geometry: 600×760 canvas, screen centred at (300,370), r=165. Faces are clipped to `.screen`.
- `assets/faces/*.jpg` — square face art, 600×600. `<name>-light.jpg` = light-mode version.
- `assets/faces/lunar-wake.gif` — LUNAR sleep-to-wake, played once by the "AOD to wake" button.

## Face data
- `FACES` object in the script at the bottom of `index.html`: code, name, pro, accent colour, store URL, desc, spec chips, variants.
- Add a face in two places: a `.face` card in the grid/rail AND an entry in `FACES` (key = card's #hash).
- `variants` = the switcher in the popup (Dark/Light; FOLIO pro = Digital/Analogue; RASTER pro = Dark/Light/Thin).
- `data-night` on a card's face `<img>` = the image shown in night mode.

## Day / night
- `html.night` class flips tokens. Watch rows (`.band-light`) and the popup stay light at night on purpose.
- Page opens at night then fades to day after ~1.4s (unless the visitor chose night).

## Gotchas
- Wall clock geometry is tied to the hero photo size (1567×1004): `--wx/--wy/--wf` on `.wall-face`. New hero photo = re-place the clock.
- Free faces render 6.5% smaller than Pro (`.tpl[data-tpl="free-black"] + .screen`) for a thicker black border.
- Alerts sign-up is NOT wired to a mailing service yet — shows "Sign-up opens soon." Swap the submit handler for Buttondown/Mailchimp/Kit.
- Generated light modes (not Jim's exports): radius, versal, versal-pro, fahrplan-pro, raster. Replace with real exports when available.
- Garmin product photos are used for the device templates — check Garmin brand guidelines before launch.
