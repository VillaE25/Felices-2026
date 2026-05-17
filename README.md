# Felices para siempre 2026 — PWA

A bilingual (ES/EN) installable progressive web app for taking notes at the 2026 regional convention. Works offline once loaded.

## Files in this folder

| File | What it does |
|---|---|
| `index.html` | The app itself — all the program, notes, bookmarks |
| `manifest.json` | Tells phones the app's name, icon, theme color |
| `sw.js` | Service worker that caches everything for offline use |
| `icon.svg` | Vector icon (used by modern browsers) |
| `icon-180.png` | Apple touch icon (iPhone home screen) |
| `icon-192.png` | Android icon |
| `icon-512.png` | Splash screen / high-res icon |
| `icon-512-maskable.png` | Android adaptive icon |

## Deploy to GitHub Pages (free, ~10 minutes)

1. **Create a new GitHub repo.** Name it something like `felices-2026` or `convention-journal-2026`. Public.
2. **Upload all the files in this folder** to the root of the repo (drag & drop on GitHub's web UI works, or `git push` if you prefer).
3. **Enable Pages:** in the repo, go to *Settings → Pages*. Under "Source," select *Deploy from a branch* and pick `main` (or `master`) and `/ (root)`. Save.
4. Wait 1–2 minutes. GitHub will show your live URL — something like `https://YOUR-USERNAME.github.io/felices-2026/`.
5. **Test it:** open the URL on your phone. Tap Share → "Add to Home Screen" (iOS) or the install prompt (Android Chrome). You're done.

## Important: HTTPS is required

PWAs only work over HTTPS (or `localhost` for testing). GitHub Pages gives you HTTPS automatically, so you're fine. If you ever host this somewhere else, make sure HTTPS is on or the service worker won't run and offline mode breaks.

## How offline works

The **first time** someone opens the URL, they need internet — the service worker downloads and caches every file. **After that, it works fully offline.** Notes, bookmarks, and theme preference are saved in the browser's localStorage and persist between sessions.

Tell your users: **open the URL once with wifi before the convention starts.** That's it.

## How to update the program later

If you fix a typo or update something in `index.html`:

1. Edit and re-upload the file to GitHub.
2. **Open `sw.js` and bump the cache version** — change `'felices-2026-v1'` to `'felices-2026-v2'` (and so on). This forces phones to grab the new version instead of serving the old cached copy.
3. Re-upload `sw.js` too.

Users will get the update next time they open the app with internet.

## Custom domain (optional)

If you want a friendlier URL like `felices2026.com`, buy a domain (Namecheap, Cloudflare, etc., usually $10–15/year) and point it at GitHub Pages. GitHub has instructions under *Settings → Pages → Custom domain*.

## Testing locally before deploying

If you want to test before pushing to GitHub, run a local server from this folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser. localStorage and service workers both work on localhost.
