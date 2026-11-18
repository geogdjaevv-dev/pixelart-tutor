# PixelArt Tutor

**A local-first pixel art editor and visual drawing tutor for PC and iPad.**

Create game-ready pixel art sprites with precise, pixel-by-pixel guidance, from the initial silhouette to the finished character.

PixelArt Tutor compares your working sprite with a target PNG and highlights exactly which pixels to add, remove, or recolor. Draw directly in the editor, refine your references, and export finished assets to LibreSprite for animation.

## Features

- **Target preparation:** resize concept art to sprite resolution, restrict colors to a palette, clean up transparency and noise, and align the target with an existing silhouette.
- **Pixel editor:** pencil, eraser, eyedropper, guided drawing, undo and redo, with exact pixel coordinates and palette color numbers.
- **Drawing stages:** store up to 20 target images per project, switch between them, rename, reorder, import, and export them. Generate a silhouette from a target and prepare other stages manually.
- **Target editing:** edit the reference on the right canvas without changing your working sprite. Target editing has its own undo history.
- **Project library:** manage multiple named projects locally with thumbnails, autosave, and JSON backups.
- **Quality checks:** identify off-palette colors, partially transparent pixels, isolated pixels, and small disconnected clusters.
- **Export:** PNG, CSV, JSON, and `.ase` (single-frame RGBA sprite with a palette, optional hidden references, and empty Armor and Weapon layers).
- **Tablet-friendly workspace:** dual canvases, synchronized navigation, touch and stylus input, and a pen-draws / finger-pans mode.
- **Offline support:** installable progressive web app (PWA), with the application cached after the first successful online launch over HTTPS.

## Quick start

1. Open `index.html` on your computer or visit the deployed website in your browser.
2. Load your source PNG and target PNG. Use the target preparation module for high-resolution concept art.
3. Import a palette (PAL, GPL, or PNG), or use the built-in Skeleton A palette.
4. Open the project library and save your project under a name.
5. In the drawing stages panel, save the current target, create a monochrome silhouette, or import separate stage PNGs. All stages must have the same dimensions.
6. Draw on the left canvas using the pixel-by-pixel guides. To refine the reference itself, enable target editing and draw on the right canvas, then return to your working sprite.
7. Review your work and export an `.ase` file for animation in LibreSprite.

Recommended workflow: **Silhouette > Anatomy > Flat colors > Light and shadow > Details**.

PixelArt Tutor does not generate anatomy or guarantee artistic quality. Intermediate targets should be prepared and reviewed separately.

The current application interface is in Russian; this documentation uses English names for its tools and controls.

## Deploy to GitHub Pages

1. Create a public GitHub repository, for example `pixelart-tutor`.
2. Extract the release archive and upload its **contents** to the repository root: `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, and `README.md`. Do not upload only the ZIP archive.
3. Open **Settings > Pages**. Under Source, select **Deploy from a branch**, choose `main` and `/(root)`, then click Save.
4. Once deployment is complete, open the URL displayed in Settings > Pages. It will usually look like `https://<username>.github.io/pixelart-tutor/`.
5. Wait for the offline-ready indicator. On iPad, open the site in Safari and select **Share > Add to Home Screen**. Launch the installed app online at least once and wait for the offline-ready indicator again.
6. To test offline mode, enable Airplane Mode, fully close and reopen the app, open a saved project, and make a test stroke.

To update the app, replace the application files in the same repository. Developers should increment the cache version in `sw.js` when updating the application shell. If an update fails, export a JSON backup before reloading the site online. Do not clear website data without a backup.

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| B | Pencil |
| E | Eraser |
| I | Eyedropper |
| G | Guided drawing (left canvas) |
| Ctrl / Cmd + Z | Undo |
| Ctrl / Cmd + Y or Cmd + Shift + Z | Redo |
| Ctrl / Cmd + S | Export project JSON |

## Storage and privacy

Images and projects are processed locally in your browser. They are not uploaded to a server. GitHub Pages serves the public application code, not your private project library.

Named projects and the last session are saved in IndexedDB. A localStorage copy is also maintained when storage quotas allow. Progress is saved after drawing strokes and periodically. JSON backups include the working sprite, target, palette, drawing stages, and settings, so you can transfer projects between devices. Undo history is not included.

Browser data may be lost if website data is cleared, storage runs low, or the device fails. Autosave cannot guarantee recovery after a power outage. Export JSON backups regularly. Automatic disk backups require File System Access API support and may be unavailable in Safari. There is no cross-device synchronization.

## Limitations and testing

- Working sprites: up to 512 x 512 pixels. Concept images for target preparation: up to 4096 x 4096 pixels and 16 million pixels total. A resolution of 64–128 pixels is recommended for comfortable drawing.
- PWA functionality requires HTTPS or localhost. Opening a local HTML file directly does not register a service worker.
- `.ase` export contains a single frame. Animation is handled in LibreSprite. Direct `.ase` import is not supported.
- Compatibility with physical iPads, Apple Pencil, offline Safari launches, and opening exported files in LibreSprite still needs on-device verification.
- Version 6.0 is an experimental build. Export your existing projects as JSON before upgrading; local HTML files and deployed websites use separate browser storage.

## Repository structure

```text
index.html            # Application, CSS, and JavaScript
sw.js                 # Offline application cache
manifest.webmanifest  # PWA installation settings
icon-192.png          # App icon
icon-512.png          # High-resolution app icon
README.md             # Documentation
```

No external libraries, backend, or build tools are required.

To test the PWA locally, run the following command from the project directory:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000/`.
