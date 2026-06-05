# ohwow — front end

The marketing site and pitch decks for **[ohwow.science](https://www.ohwow.science)** —
a meeting place for people doing AI for science. (The `/wonder` plugin and the OhWow
matching service live in a separate repo, **cgreene/wonder**.)

Static HTML, no build step. **Pushing to `main` auto-deploys** to www.ohwow.science
(GitHub Pages; `CNAME` sets the custom domain).

## Pages

| Path | What |
|------|------|
| `index.html` | the landing page (`/`) — pitch, demo, how it works, privacy, community, footer |
| `install/index.html` | `/install` — the ~30-second "get /wonder" walkthrough |
| `together/index.html` | `/together` — currently a near-duplicate of `/install` (see Notes) |
| `deck/index.html` | `/deck/` — the **funder** pitch deck (reveal.js) |
| `deck/scientists.html` | `/deck/scientists.html` — the **scientist-facing** deck (reveal.js) |
| `CNAME`, `favicon.svg` | custom domain + icon |

## Run it locally

No dependencies — it's static. Serve the folder and open it:

```bash
python3 -m http.server 8000
# landing:        http://localhost:8000/
# decks:          http://localhost:8000/deck/  and  /deck/scientists.html
```

Decks and fonts load reveal.js / Google Fonts from CDNs, so those need a network
connection to render.

## Design notes

- **Inline CSS per page.** Each file is self-contained — its own `<style>` block, no
  shared stylesheet. Simple to ship, but the palette is duplicated across pages: change
  a token in one place, change it everywhere.
- **Tokens** (`:root` custom properties): `--ink #2c2622`, `--card #fffdf7`,
  `--bg #f4efe4`, accents `--coral --yellow --lilac --blue --green --plum`. Cards use a
  "neobrutalist" look — `border: 2.5px solid --ink`, hard `box-shadow: 5px 5px 0 --ink`
  (`--pop`), rounded corners. Eyebrow chips are the `✦ LABEL` pills.
- **Fonts:** Figtree (display/body) + JetBrains Mono (mono), via Google Fonts.
- **Decks:** [reveal.js](https://revealjs.com) (CDN), 1180×720, one `<section>` per slide,
  same design system as the landing.
- **Anchors + the fixed nav:** the landing nav is `position: fixed`, so in-page anchor
  links rely on `html { scroll-padding-top: 110px }` to land *below* the bar. If the nav
  height changes, update that offset.

## Notes / cleanup

- **`install/` vs `together/`** are currently near-identical. If `/together` should be its
  own page, give it distinct content; otherwise one of them can go.
- Old deck backups belong in git history, not the tree (e.g. a `*.backup.html`).
