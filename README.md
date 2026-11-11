# Impact Intelligence, LLC — website

Static marketing site for [impact-intelligence.com](https://impact-intelligence.com), hosted on GitHub Pages.

## Structure

```
index.html          the whole site (single scrolling page)
styles.css           all styles — tokens in :root, then section-by-section
assets/fonts/        self-hosted Rubik 400/500/600 (woff2, latin subset; OFL.txt is its license)
assets/img/          logos (horizontal, reversed, mark), favicons, apple touch icon, OG/share image
design/              the ORIGINAL 2026 "Industry" design handoff — superseded by the November 2026
                     rebrand; kept for history only
CNAME                 GitHub Pages custom domain config
```

No build step, no JavaScript, no dependencies. Edit `index.html` and `styles.css` directly.

## Brand

The November 2026 rebrand (logo files live in the company Google Drive under Business/Branding).
Tokens are in the `:root` block of `styles.css`:

- Navy `#0A2540`, blue `#1F6FEB`, lime `#84CC16`, ground `#F2F6FB` — from the logo files
- `#1A5FCC` is the brand blue darkened for small text on the light ground (contrast)
- Lime is an accent only (bars, underlines) on light backgrounds — too light for text there
- Service bullets reuse the logo's two-circle mark: blue left, navy overlap, and a per-service
  right circle — teal `#0D9488`, orange `#F97316`, pink `#EC4899`, purple `#8B5CF6`
- Type: Rubik (closest match to the wordmark)

## Local preview

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

## Deployment

Pushing to `main` publishes via GitHub Pages (Settings → Pages → source: `main` branch, `/` root).

The custom domain is set via the `CNAME` file in this repo. DNS lives at Squarespace — see below.

### DNS (Squarespace → GitHub Pages)

At the Squarespace domain's DNS settings for `impact-intelligence.com`, add:

**Apex domain** — four `A` records pointing `@` to GitHub Pages' IPs:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**www subdomain** (optional, recommended) — one `CNAME` record:
```
www  →  ImpactIntelligenceLLC.github.io
```

Then in the GitHub repo: Settings → Pages → Custom domain → enter `impact-intelligence.com` → Save,
wait for DNS check to pass, then enable **Enforce HTTPS**.

Email (Google Workspace MX records) is unrelated to these `A`/`CNAME` records and does not need to
change.
