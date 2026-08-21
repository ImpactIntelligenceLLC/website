# Impact Intelligence, LLC — website

Static marketing site for [impact-intelligence.com](https://impact-intelligence.com), hosted on GitHub Pages.

## Structure

```
index.html          the whole site (single scrolling page)
styles.css           all styles — tokens in :root, then section-by-section
assets/fonts/        self-hosted Barlow & Barlow Condensed (woff2, latin subset)
assets/img/          favicon, apple touch icon, OG/share image
design/              the original design handoff — reference only, not shipped behavior
  HANDOFF.md           full spec: copy, tokens, layout notes
  prototype.dc.html    the approved visual prototype (open in a browser)
  design-system/       the "Industry" design system this site is built on
CNAME                 GitHub Pages custom domain config
```

No build step, no JavaScript, no dependencies. Edit `index.html` and `styles.css` directly.

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
