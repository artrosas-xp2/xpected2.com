# xpected2.com

Static site for **xpected2.com** — a tactical engagement consultancy.

## Structure

```
xpected2.com/
├── index.html          ← landing page (markup only; styles in styles.css)
├── tokens.css          ← shared design tokens (palette) for all pages
├── styles.css          ← landing-page stylesheet (ordered to match the page)
├── video.css           ← shared stylesheet for the channel pages
├── favicon.svg         ← emoji favicon
├── scripts.js          ← (currently empty)
├── images/
│   ├── el-caballo.jpg  ← hero photo (optimized, 1600px)
│   └── og-card.jpg     ← social-share card (og:image)
├── el-caballero/ · reconnaissance/ · shenanigans/ · maneuvers/
│   └── index.html      ← channel subpages (use ../tokens.css + ../video.css)
├── stats/
│   └── index.html      ← /stats/ placeholder
├── .gitignore
└── README.md
```

Every page loads `tokens.css` (the palette) before its page stylesheet.
The only intentional token divergence: `--line` is solid ink on the
landing page and a 20%-alpha hairline on channel pages.

## Deploy

Hosted on **Cloudflare Pages**, connected to this GitHub repo
(`artrosas-xp2/xpected2.com`). Every push to `main` builds and deploys
automatically — no manual upload step.

Cloudflare Pages build settings (static site, no build step):

| Setting | Value |
|---------|-------|
| Production branch | `main` |
| Framework preset | None |
| Build command | *(empty)* |
| Build output directory | `/` |

To ship a change: edit, `git commit`, `git push`. Cloudflare deploys in
~30s.

## Local preview

Preferred: `python3 -m http.server 8000` from the repo root, then open
<http://localhost:8000>. Opening `index.html` directly (file://) also
works — all asset paths are relative.
