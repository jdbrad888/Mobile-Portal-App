# Ally QR Assist — Progressive Web App (PWA)

An installable, offline-capable version of the Ally QR Assist prototype. It installs
straight from the browser (no app store) and runs full-screen like a native app.

## Files
- `index.html` — the app (all styling/logic inlined)
- `manifest.webmanifest` — app metadata (name, icons, standalone display, theme)
- `sw.js` — service worker (caches the app shell for offline use)
- `icon-192.png`, `icon-512.png`, `icon-maskable-*.png`, `apple-touch-icon-180.png` — app icons

**Keep all files together in the same folder.**

## Hosting (required)
A PWA must be served over **HTTPS** (or `http://localhost`) — service workers do not run
from a `file://` path. Upload the whole folder to any static host, e.g.:
- GitHub Pages, Netlify, Vercel, Cloudflare Pages, Azure Static Web Apps, or any web server.
- To test locally: from this folder run `python3 -m http.server 8000` and open
  `http://localhost:8000/` (localhost counts as a secure context).

## Installing
- **Android / Chrome / Edge:** open the hosted URL → an **Install** icon appears in the
  address bar, or use the ⋮ menu → **Install app / Add to Home screen**.
- **iOS / Safari:** open the hosted URL → **Share** → **Add to Home Screen**.
- **Desktop Chrome / Edge:** open the URL → **Install** icon in the address bar.

Once installed it launches from the home screen in its own window, works offline, and
uses the ECI app icon.

## Updating
Bump the `CACHE` name in `sw.js` (e.g. `ally-qr-assist-v2`) whenever you change the app —
the new service worker will clear the old cache on next launch.
