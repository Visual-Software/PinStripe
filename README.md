# PinStripe (UXP panel for Photoshop 24+)
A small lightweight Stroke Tool for Photoshop. 

Draw a path with the Pen tool (Path mode), set the two ends, click **Create line**.

Install for testing: UXP Developer Tool > Add Plugin > select `manifest.json` > Load.
All files must be in the plugin folder: manifest.json, index.html, main.js, ps.js, geometry.js, preview.js, svg.js, raster.js.

- The panel has a live preview at the top: it shows the result for the current settings and follows your path
  (re-read every ~0.8 s; "Refresh" forces it). It is scaled to fit the panel and uses the foreground colour.
  It is drawn as a vector image by `svg.js` (sharp at any size). If the panel cannot show SVG, it falls back
  automatically to `raster.js` (PNG, then Photoshop-encoded JPG), drawn at 2-3x size so it stays sharp on high-DPI
  screens. The small button next to "Refresh" shows the current renderer; click it to switch by hand.
- Start / End are independent: Flat, Round or Taper (length, tip width %, shape fat <-> needle).
- Result: a normal shape layer (one undo step), filled with the foreground colour. Your pen path is put back.
- "Replace the last line I made" deletes the previous result first, for quick tweaking.
- By default the outline is the exact offset of your path (many small points, both sides truly parallel). Tick
  "Fewer anchor points" for a few editable Bezier curves instead.
- Corners in the path get round joins. Closed smooth paths become a ring of constant width.
- Writing the outline back into Photoshop uses an undocumented command; the plugin tries several spellings and
  logs each attempt. If something fails: panel > Copy log.
- `dev/test_geometry.js` tests the outline maths in Node: `node dev/test_geometry.js`
- `dev/test_preview.js` tests the preview layout: `node dev/test_preview.js`
- `dev/test_raster.js` tests the pixel renderer and PNG encoder: `node dev/test_raster.js`
- `dev/test_svg.js` tests the SVG renderer: `node dev/test_svg.js`



