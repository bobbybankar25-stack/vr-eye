# Virtual Eyewear Studio

Browser virtual glasses try-on: photo mode (2D overlay on MediaPipe landmarks) and live mode (3D procedural frames posed with the MediaPipe face transformation matrix, rendered by Three.js). Frames are generated in code (`src/glasses.js`), so there are no GLB files to go missing. No backend; photos and camera frames never leave the browser.

## Windows setup
1. Install Node.js LTS from https://nodejs.org (accept defaults), then reopen your terminal.
2. Unzip this folder, e.g. to `C:\projects\virtual-eyewear-studio`.
3. Open PowerShell: `cd C:\projects\virtual-eyewear-studio`
4. `npm install`
5. `npm run dev`
6. Open http://localhost:5173 in Chrome (localhost counts as secure, so the camera works).

Cloud option: upload the folder to StackBlitz or GitHub Codespaces and run the same two commands.

## Use
- Photo: choose "Photo", upload a front-facing selfie, switch frames/colours, adjust sliders, "Download preview".
- Live: choose "Live camera", click Start, allow camera. Move your head; switch models while running; Stop releases the camera.

## Files
`src/catalogue.js` products, colours, per-style live alignment (edit here) · `src/glasses.js` models (origin = bridge, +Z forward, +Y up, ~13 cm wide) · `src/photo.js` 2D drawing and landmark placement · `src/main.js` UI, camera, tracking.

## Troubleshooting
- `npm` not recognised: reinstall Node, reopen PowerShell.
- Camera blocked: click the lock icon in the address bar, allow Camera, reload.
- "Could not load face-tracking model": the WASM (jsDelivr) and model (storage.googleapis.com) download at runtime; check your connection. To self-host, put them in `public/` and change `WASM`/`MODEL` in `src/main.js`.
- Glasses too high/low/far in live mode: tune `ALIGN` in `src/catalogue.js` or use the sliders.

## Deploy (HTTPS)
`npm run build`, then upload the `dist` folder to Netlify, Vercel or Cloudflare Pages (all serve HTTPS).

## Status and limits
Not yet run or tested: it was written in an offline environment, so `npm install`, MediaPipe loading and the live alignment constants are unverified. No occlusion, no depth-accurate fit, and a photo is not a 360° view.
