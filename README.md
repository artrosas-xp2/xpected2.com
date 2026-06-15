# xpected2.com

Static site for **xpected2.com** — a tactical engagement consultancy.

## Structure

```
xpected2.com/
├── index.html        ← landing page
├── styles.css        ← (currently empty; styles inline in index.html)
├── scripts.js        ← (currently empty)
├── images/
│   ├── el-caballo.jpg
│   └── el-caballo2.jpg
├── stats/
│   └── index.html    ← /stats/ subpage
├── .gitignore
└── README.md
```

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

Open `index.html` in your browser — no build step needed.
