# Ally QR Assist — Progressive Web App (PWA)

An installable, offline-capable version of the Ally QR Assist prototype. It installs
straight from the browser (no app store) and runs full-screen like a native app.

**This build: 10 Sep 2026** — service-worker cache `ally-qr-assist-2026-09-08`.

## Files
- `index.html` — the app (all styling/logic inlined)
- `manifest.webmanifest` — app metadata (name, icons, standalone display, theme)
- `sw.js` — service worker (caches the app shell for offline use)
- `icon-192.png`, `icon-512.png`, `icon-maskable-*.png`, `apple-touch-icon-180.png` — app icons

**Keep all files together in the same folder.**

## Redeploying to GitHub Pages
Replace the files in your repo (or the folder GitHub Pages serves) with the ones in this
package — the key change is the new `index.html` plus the bumped cache name in `sw.js`.

1. Copy all files in this folder into your repo, overwriting the old ones.
2. Commit and push. GitHub Pages redeploys automatically (usually within a minute).
3. On each device, the **new service worker installs on next visit** and clears the old
   cache (because `sw.js`'s `CACHE` name changed). If an already-installed copy still shows
   the old build, close and reopen it once, or pull-to-refresh — it will update.

> A PWA must be served over **HTTPS** (GitHub Pages is), never `file://` — service workers
> won't run from a local file. To test locally first, run `python3 -m http.server 8000`
> from this folder and open `http://localhost:8000/` (localhost counts as a secure context).

## Installing (for reference)
- **Android / Chrome / Edge:** open the hosted URL → an **Install** icon appears in the
  address bar, or use the ⋮ menu → **Install app / Add to Home screen**.
- **iOS / Safari:** open the hosted URL → **Share** → **Add to Home Screen**.
- **Desktop Chrome / Edge:** open the URL → **Install** icon in the address bar.

Once installed it launches from the home screen in its own window, works offline, and
uses the ECI app icon.

## Updating in future
Whenever you change the app, **bump the `CACHE` name in `sw.js`** (e.g. use the next date,
`ally-qr-assist-2026-08-15`) — the new service worker will clear the old cache on next
launch so devices reliably pull the new build. If the cache name is *not* changed, some
installed copies may keep serving the old cached app.

## Note on the live Ally embed
This build still runs the **built-in demo agent** by default (works offline). If you want
to preview the real embedded ECI Ally agent, append `?ally=live` to the URL — but note that
needs your backend token endpoint and CORS/hosting to be live first (see the change log),
and it won't function offline.
