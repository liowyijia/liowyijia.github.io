# Yi Jia's Quarto Website

Minimal academic website with Home, Research, and Ceramics pages.

## Pages

- **index.qmd** — Home page with photo, bio, and links to Email, LinkedIn, GitHub, CV
- **research.qmd** — Working papers, publications, software
- **ceramics.qmd** — Photo gallery of your pieces

## One-time setup

1. **Install Quarto**: <https://quarto.org/docs/get-started/>
2. **Extract this folder to**:
   `~/Harvard University Dropbox/Yi Jia Liow/GitHub/yijialiow.github.io/`
3. **Exclude `.git/` from Dropbox sync** (important! prevents sync
   conflicts with Git's internal files):
   ```bash
   cd "~/Harvard University Dropbox/Yi Jia Liow/GitHub/yijialiow.github.io"
   xattr -w com.dropbox.ignored 1 .git
   ```
   Do this **after** `git init` below.
4. **Create the GitHub repo** at github.com, named `yijialiow.github.io`
   (not the same as your old `liowyijia.github.io`).
5. **Initialize and push**:
   ```bash
   cd "~/Harvard University Dropbox/Yi Jia Liow/GitHub/yijialiow.github.io"
   git init
   xattr -w com.dropbox.ignored 1 .git    # exclude .git from Dropbox sync
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin git@github.com:liowyijia/yijialiow.github.io.git
   git push -u origin main
   ```
6. **Enable GitHub Pages**: in the repo, **Settings → Pages** and set
   **Source** to the `gh-pages` branch (appears after the first Action
   run).

## Day-to-day workflow

```bash
quarto preview          # live preview while you edit
# ... edit .qmd files ...
git add . && git commit -m "Update research page" && git push
```

GitHub Action auto-renders and publishes within 1-2 minutes.

## Content to customize

Things to replace before first publish:

- `you@example.edu` — your actual email (appears in index.qmd and
  _quarto.yml)
- `liowyijia` — your actual GitHub username if different
- `yijialiow` in LinkedIn URL — your actual LinkedIn handle
- Bio paragraphs in `index.qmd`
- Real working papers/publications in `research.qmd`
- `pics/headshot.jpg` — your headshot
- `files/cv.pdf` — your CV
- `pics/ceramics/piece1.jpg` through `piece6.jpg` — ceramic photos

## Ceramics page notes

The gallery uses Quarto's `layout-ncol=3` (3 columns). Adjust as needed:

- Change to `layout-ncol=2` or `4` for different column counts
- Add `lightbox: true` to the frontmatter for click-to-zoom
- Add/remove photos by editing `ceramics.qmd` — just follow the
  `![caption](path)` pattern

## Custom domain (yijialiow.com) — when ready

1. Buy the domain (Cloudflare Registrar ~$10/yr for .com is cheapest).
2. Add four A records for the apex pointing to:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
   And a CNAME record for `www` pointing to `liowyijia.github.io`.
3. In GitHub **Settings → Pages**, enter `yijialiow.com` as custom
   domain.
4. Enable **Enforce HTTPS** after the certificate provisions.

## About Dropbox + Git

This setup works fine IF you do these two things:

1. **Run `xattr -w com.dropbox.ignored 1 .git`** so Dropbox doesn't try
   to sync the thousands of files in `.git/`.
2. **Don't open the repo on two machines simultaneously** — edit on
   one machine at a time to avoid conflict copies.

If Dropbox sync ever seems to mess up the repo, you can always
reclone from GitHub — that's your real backup.

## Future: migrating off Harvard Dropbox

You'll lose Harvard Dropbox access when you leave. When you migrate:

1. Clone the repo fresh into personal Dropbox (or `~/GitHub/`)
2. Run `xattr -w com.dropbox.ignored 1 .git` again on the new location
3. Delete the Harvard Dropbox copy

Because GitHub holds the canonical version, this migration is safe.

## Project structure

```
yijialiow.github.io/
├── _quarto.yml              # site config (navbar, theme)
├── index.qmd                # Home
├── research.qmd             # Research
├── ceramics.qmd             # Ceramics
├── styles.css               # custom CSS
├── pics/
│   ├── headshot.jpg
│   └── ceramics/            # ceramic photos go here
├── files/
│   └── cv.pdf               # your CV
└── .github/workflows/
    └── publish.yml          # auto-render + publish
```
