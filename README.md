# Breath Ritual PWA

A mobile-first, framework-free pranayama routine builder and breathing player. All app CSS and JavaScript live in `index.html`; the only external runtime resource is the Google Fonts stylesheet for Fraunces. The app works with Georgia/system fallbacks when offline.

## Files

- `index.html` — complete app UI, routine editor, player, Wake Lock, Web Audio, localStorage, service-worker registration
- `manifest.json` — installable PWA manifest
- `sw.js` — cache-first offline app-shell service worker
- `icon-192.png` — 192×192 app icon
- `icon-512.png` — 512×512 app icon
- `icon-maskable-512.png` — 512×512 maskable Android icon

## Run locally

Service workers require HTTP(S), so do not open `index.html` directly from the filesystem.

```bash
python -m http.server 8080
```

Then open `http://localhost:8080` from inside this folder.

## Host on GitHub Pages

1. Create a new GitHub repository.
2. Upload all files from this folder to the repository root and commit them.
3. In GitHub, open **Settings → Pages**.
4. Choose **Deploy from a branch**, select your main branch and `/ (root)`, then save.
5. Open the HTTPS Pages URL GitHub gives you and test the app there.

Because all manifest and service-worker paths are relative, the app also works when GitHub Pages serves it from a repository subpath.

## Host on Netlify

1. Sign in to Netlify.
2. Use **Add new site → Deploy manually** and drag this entire folder into the deploy area, or connect the GitHub repository.
3. Open the HTTPS Netlify URL after deployment.

No build command or publish transform is needed; this is a static site.

## Create an Android package with PWABuilder

1. Deploy the app first over HTTPS using GitHub Pages, Netlify, or another static host.
2. Go to `https://www.pwabuilder.com/`.
3. Enter the deployed **HTTPS URL** for Breath Ritual and start the PWA analysis.
4. Fix any host-specific warnings PWABuilder reports, if any.
5. Choose the Android packaging option and generate the Android package.
6. Download the package and follow PWABuilder's signing/publishing guidance for sideloading or Google Play.

PWABuilder may offer more than one Android packaging path depending on its current tooling. The hosted URL, manifest, HTTPS service worker, and valid icons are the important inputs.

## Notes

- Routine data is saved locally in the browser using `localStorage`, guarded with `try/catch`.
- Timing is driven by `performance.now()` plus `requestAnimationFrame`, so it remains timestamp-based rather than interval-count based.
- Screen Wake Lock is requested while the routine is actively playing where supported.
- Sound is synthesized with the Web Audio API; no sound files are included.
- Vibration depends on browser/device support and can be unavailable on some desktop browsers or iOS versions.
