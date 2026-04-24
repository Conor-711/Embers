# Embers · Public Docs Site

The `docs/` folder is authored in the main app repo
(`Conor-711/lovepaint`) but **published** via GitHub Pages from a
separate public repo, [`Conor-711/Embers`](https://github.com/Conor-711/Embers),
so the hosted URL carries the **Embers** brand instead of the
internal codename.

| Page | Public URL |
|---|---|
| Landing | `https://conor-711.github.io/Embers/` |
| Terms of Service | `https://conor-711.github.io/Embers/terms.html` |
| Privacy Policy | `https://conor-711.github.io/Embers/privacy.html` |
| Contact Support | `https://conor-711.github.io/Embers/support.html` |

These URLs are **the single source of truth** and are referenced
from `Lovelee/Core/Links/LegalLinks.swift`. If you ever move to a
custom domain (e.g. `embers.app`), update that one file + App Store
Connect metadata — nothing else in the client will drift.

## Enabling GitHub Pages (first-time setup)

1. Create the public repo `Conor-711/Embers` on GitHub (empty, no
   license/README preset required).
2. From this repo's root, sync the `docs/` folder into the Embers
   repo — easiest one-shot (run at project root):
   ```bash
   # 1. Clone the empty Embers repo next to this one
   git clone https://github.com/Conor-711/Embers.git ../Embers

   # 2. Mirror docs/ into it
   rsync -av --delete docs/ ../Embers/docs/

   # 3. Commit & push
   cd ../Embers
   git add docs
   git commit -m "chore(pages): publish Terms / Privacy / Support"
   git push origin main
   ```
   From then on, re-run the `rsync` + commit step whenever the copy
   changes. (Optional: turn this into a GitHub Action in the main
   repo that pushes to `Conor-711/Embers` on every `docs/` diff.)
3. In the **`Conor-711/Embers`** repo UI: **Settings → Pages**.
4. Under **Build and deployment**:
   - **Source:** `Deploy from a branch`
   - **Branch:** `main` · `/docs`
5. Click **Save**. The site is live in ~60 s at the URL above.
6. Verify each of the four URLs in a browser.

The `.nojekyll` file at the root of `docs/` disables Jekyll processing
so GitHub serves the static HTML verbatim — no build step, no Ruby,
no surprise rewrites of filenames starting with an underscore.

## File structure

```
docs/
  index.html       ← landing / hub (3-card grid)
  terms.html       ← Terms of Service
  privacy.html     ← Privacy Policy
  support.html     ← Contact Support + self-serve help
  assets/
    styles.css     ← shared stylesheet (mirrors app design tokens)
  .nojekyll        ← tells GitHub Pages to skip Jekyll
  README.md        ← this file (ignored by Pages, served as 404-style)
  ARCHITECTURE.md  ← internal project arch doc (not part of the Pages IA)
  PRIVACY.md       ← Chinese-language draft (internal)
  TERMS.md         ← Chinese-language draft (internal)
```

Note: `ARCHITECTURE.md`, `PRIVACY.md`, and `TERMS.md` predate the
HTML site and remain in the folder as internal working drafts. They
are **not** linked from the public pages, so users won't stumble into
them.

## Editing the legal text

The canonical legal copy lives in the `.html` files. To change the
Terms, Privacy Policy, or Support text:

1. Edit the relevant `.html` file directly. Pure semantic HTML — no
   templating, no includes.
2. Bump the `Effective date` / `Last updated` line at the top.
3. Push to `main`. GitHub Pages rebuilds automatically.
4. If the change is **material** (Apple's bar: something a user would
   care about, e.g. new data collection, new refund policy), trigger
   an in-app notice — currently the app just links out, so plan an
   empty banner sweep when you ship the change.

## Contact

Support email (also surfaced in the app + on the site):
[zfy3712z@gmail.com](mailto:zfy3712z@gmail.com)
