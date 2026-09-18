# 3d

A single-file 3D personal page. Six thousand points in five clusters — one per
section — with a camera that flies between them.

**Live:** https://sharkascent-hue.github.io/3d/

## Running it locally

It must be served over HTTP. Browsers block ES modules on `file://`, so
double-clicking `index.html` will show the text but no 3D.

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## How it's built

- **No build step, no framework, no bundler.** One HTML file plus Three.js.
- **No third-party CDN.** `three.module.min.js` is vendored here, so the page
  has no external runtime dependency and works offline.
- **Progressive enhancement.** A plain script renders the text and navigation;
  a module then loads Three.js and adds the 3D. If WebGL is missing or the
  module fails, the page is still fully readable and navigable.
- **Hand-rolled orbit controls** instead of `OrbitControls` — fewer lines than
  wiring up the addon.
- Points are drawn from a single `BufferGeometry` with a small custom shader:
  soft round sprites, distance fog, and a per-cluster dim for whichever
  section isn't active.

## Accessibility

- Every control is reachable by keyboard; `←` / `→` move between sections.
- `prefers-reduced-motion` drops the drift and the fly-through.
- All eight foreground/background colour pairs clear WCAG AA (lowest 5.12:1).
- The canvas is `aria-hidden`; nothing meaningful is conveyed only in 3D.
- No horizontal overflow at 320 / 768 / 1024 / 1440px.

## A note on the visual

The clusters are placed by hand. They are not a projection of any real
embedding — the page says so in its own colophon, and it would be a shame to
imply a computation that never ran.

## Self-check

Append `?test` to the URL and open the console: it asserts the point count and
that every point lands near its cluster centre.

## Licence

MIT for the page itself. Three.js is MIT, © the Three.js authors.
