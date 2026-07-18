---
name: xpected2-design
description: The xpected2.com design system and hard rules — tokens, two themes, component vocabulary, layout/voice rules, and the ship checklist. Load before any visual or structural change to the site.
---

# Xpected2.com Design System

A satirical Battlefield 6 squad site styled as a mock corporate/legal firm:
"a fire team, structured as a firm." Every design and copy choice serves the
deadpan-legal voice. It is never winking; it is always filing paperwork.

## Non-negotiables (learned the hard way)

1. **Gamertags only** on public pages. Never real names.
2. **No brand words** in copy ("jeep" incident — use "vehicle", "the Caballo").
3. **No invented testimonials.** Quotes come from the intake log
   (`Obsidian Vault/Xpected2.com/6. Quote Intake 🎙️.md`) — real or clearly
   editorial framing, never fabricated speech attributed to real people.
4. **The joke stands** — canon jokes (Al-V_'s "only ranked match" third place)
   outrank contradicting data. The surgeon motif appears exactly once, on
   CDLsavage's page.
5. **Never push** `stats/players/`, `stats/history.jsonl`, `images/bf6/`,
   `tools/` (all gitignored, local-only).
6. **Homepage is the firm's page**; personal records live on `/xpected2/`.
   Each member's material lives on their own dossier only.
7. **Ask before creating new pages.**
8. Arturo reviews plans as **before → after tables**, not prose. Lead with
   what does NOT change.

## Token architecture

`tokens.css` is the single source of truth — two themes:
- `:root` = light (cream `#ece9df` / olive `#3d4a2e` field-manual brand)
- `:root[data-theme="dark"]` = navy "Battle Group Counsel" (page `#0a0e1a`,
  steel-blue accent `#4a7ba7` fills the olive role)

Rules:
- **Zero raw palette hex outside tokens.css.** Derivations use
  `rgba(var(--ink-rgb), a)` triplet tokens.
- Semantic inversion: `--ink`/`--cream` swap in dark. Small plaques
  (`.ratified`, "He shows up.") intentionally invert to light cards.
- **Large surfaces must NOT blunt-invert.** Accent/stat bands use the
  stage pattern: `--caballo-ground` (olive→deep navy `#131c33`),
  `--band-ground` (ink→navy), with `--on-accent`/`--on-accent-rgb` text.
  Selected/active states use `--olive` + `--cream`, never `--ink` ground.
- On-plaque tokens: `--plaque-gold`, `--plaque-dim`.
- Theme boot: inline head script (localStorage.theme → prefers-color-scheme);
  toggle chip `◐` (`.theme-toggle`) on every page syncs `meta theme-color`
  (`#ece9df` / `#0a0e1a`).

## Type

Fraunces (serif display/body-editorial) · Inter Tight (UI/body) ·
JetBrains Mono (labels, stats, eyebrows — uppercase, letter-spaced) ·
Caveat 500/600 (signatures only, homepage only).

## Component vocabulary

**Homepage (`index.html` + `styles.css`):** sections max-width 1400px,
padding 80px 48px. `.section-header` = 2-col grid: `.section-number`
(mono label "§ 0N / …") | `.section-title` (Fraunces 52px, `em` = italic
olive) — intro copy and stat lines stack *inside the title column*.
Other pieces: KPI band (`.kpi-section` on `--band-ground`), manifesto/letter
(on `--caballo-ground`, signed via `.manifesto-signed` → `.signature` →
`.sig-script`), role cards (`.expertise-grid` hairline-gap grid, `--pair`
variant = 2-col), signature cards (`.sig-cards` 2×2 business cards with
portrait, stat, script signature), El Caballo band, quote cells
(`.testimonials-strip`), channels, 5-col footer.

**Dossier template (`/xpected2|alv|roguerubio|cdlsavage/index.html`,
self-contained inline styles + `video.css` page bar):** classification
banner → dossier-hero with giant watermark (`::before`) → 280px sidebar
(`.side-label/.side-key/.side-val`, hover-reveal `.redacted`) + content
column (`.content-section` + `.section-heading` mono rule-line headings,
`.profile-body` Fraunces 20px, `.filed-exhibit` brass-edged cards,
`.specialty-grid`, `.kpi-row`, `.ratified` plaque) → **loadouts live inside
the content column as the final content-section** (radio-tab
`.loadouts-wrap`; empty state = `.loadout-pending`). Mobile: content column
first, sidebar second.

## Layout rules

- **One grid per page.** Homepage sections align at 1400px; the dossier
  at 1100px with everything in its two columns. A section either sits in
  the established grid or breaks out deliberately full-bleed — never a
  half-width orphan.
- **One heading dialect per page.** Homepage = `.section-header` pattern;
  dossier = `.section-heading` rule-lines. Never introduce a second style
  for one section.
- Stats are editorial and deduplicated: a figure appears in exactly one
  component per page.
- Sources don't mix within a surface (tracker vs in-game); discrepancies
  become reconciliation jokes, not silent edits.

## Ship checklist (every change)

1. Tag-balance check (python `HTMLParser`) on every edited page.
2. **Bump cache-busters** on any CSS change (`styles.css?v=N+1`, etc.) —
   stale CSS has bitten twice. Check current `?v=` in the page head first.
3. **Render before ship**: headless Chrome —
   `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless
   --screenshot=out.png --window-size=1440,<height> <file-or-url>`
   (add `--force-dark-mode` for the dark theme). Eyeball both themes,
   desktop + narrow.
4. Commit → push (Cloudflare Pages deploys main in ~1–2 min) → poll:
   `until curl -s "https://xpected2.com/…?r=$RANDOM" | grep -q '<new marker>'; do sleep 15; done`
5. Log the change in `Obsidian Vault/Xpected2.com/99. Update Log ✅.md`;
   numbers workflow lives in `10. Update Ritual 🔁.md`.
