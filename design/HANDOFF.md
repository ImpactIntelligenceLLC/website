# Handoff: Impact Intelligence, LLC — one-page marketing site

## Overview
A single-page production website for Impact Intelligence, LLC — a single-member data science and
technology consultancy. One scrolling page, five content blocks plus a footer: hero, company
introduction ("The Practice"), services (four cards), about, contact (email only), footer.

The site will be hosted at the client's existing `impact-intelligence.com` domain. It is a static
marketing page: no backend, no forms, no analytics requirement stated. The only interactive elements
are two in-page anchor links and a `mailto:` link.

## About the Design Files
The files in `design/` are **design references created in HTML** — a prototype showing the intended
look and behavior, not production code to copy directly. `Impact Intelligence.dc.html` is authored in
a streaming component format with inline styles; treat it as a visual and structural spec.

The task is to **recreate this design in the target environment**. No codebase exists yet, so pick the
most appropriate stack for a static one-page marketing site — a plain semantic `index.html` +
`styles.css` (recommended: smallest possible surface, trivially hostable, fastest), or Astro / Next.js
static export if the owner wants a framework for future expansion. Do not ship the prototype file as
the site; rebuild it with real stylesheets, semantic markup, meta/OG tags, and a favicon.

Suggested repo layout for the plain-HTML route:

```
/index.html
/styles.css
/assets/           (favicon, OG image)
/README.md
```

Deployment: any static host (Cloudflare Pages, Netlify, GitHub Pages, Vercel) with the apex domain
pointed at it.

## Fidelity
**High-fidelity.** Colors, typography, spacing, and copy are final. Recreate pixel-faithfully. All
values below are exact and taken from the prototype. Every color and font comes from the "Industry"
design system (see `design-system/`); do not substitute.

## Design Tokens

### Color
| Token | Value | Use |
| --- | --- | --- |
| ground | `#f2f2f3` | page background |
| ink | `#1d1f20` | headings, primary text |
| ink-800 | `#2b2b2d` | hero subhead |
| ink-700 | `#424244` | body paragraphs |
| neutral-600 | `#7a7a7d` | small meta text ("Four practice areas") |
| accent (steel) | `#5980a6` | primary button fill, service numbers, mark square, focus ring |
| accent-600 | `#416180` | link color, section labels, primary button hover |
| accent-800 | `#2c455d` | link hover |
| accent-900 | `#1d2d3d` | contact + footer field background |
| accent-400 | `#94bce3` | contact label, email hover, on-dark accents |
| divider | `rgba(29,31,32,0.16)` | all hairline borders and section rules |
| grid line | `rgba(29,31,32,0.055)` | hero blueprint grid |
| registration mark | `rgba(29,31,32,0.55)` | "+" corner marks |
| arc (strong / faint) | `rgba(89,128,166,0.4)` / `rgba(89,128,166,0.22)` | hero circles |
| ring figure (strong / faint) | `rgba(89,128,166,0.5)` / `rgba(89,128,166,0.32)` | about figure |
| selection | `rgba(89,128,166,0.3)` | `::selection` |
| on-dark body | `rgba(242,242,243,0.86)` | contact paragraph |
| on-dark muted | `rgba(242,242,243,0.6)` | footer text |
| on-dark rule | `rgba(242,242,243,0.14)` | footer top border |

### Typography
Google Fonts: `Barlow` (400, 500, 600) and `Barlow Condensed` (400, 500, 600, 700), `display=swap`,
with `preconnect` to fonts.googleapis.com and fonts.gstatic.com.

- Body: Barlow, 17px, line-height 1.55, `-webkit-font-smoothing: antialiased`.
- All headings, labels, buttons, footer: Barlow Condensed 600.

| Element | Family / weight | Size | Tracking | Line-height | Transform |
| --- | --- | --- | --- | --- | --- |
| Wordmark ("Impact Intelligence, LLC") | Condensed 600 | 15px | 0.22em | — | uppercase |
| Hero eyebrow | Condensed 500 | `clamp(12px, 1.4vw, 14px)` | 0.26em | — | uppercase |
| H1 "Impact Intelligence" | Condensed 600 | `clamp(52px, 12vw, 148px)` | -0.02em | 0.94 | none, `max-width: 15ch` |
| Hero subhead | Barlow 400 | `clamp(19px, 2.3vw, 26px)` | — | 1.42 | `max-width: 42ch` |
| Buttons | Condensed 600 | 16px | 0.1em | — | uppercase |
| Section labels (The Practice / Services / About / Contact) | Condensed 600 | `clamp(13px, 1.5vw, 15px)` | 0.2em | — | uppercase |
| Section meta ("Four practice areas") | Condensed 400 | 13px | 0.18em | — | uppercase |
| Lead paragraphs (intro, about, contact) | Barlow 400 | `clamp(19–20px, 2.1–2.2vw, 25–27px)` (see sections) | — | 1.45 | — |
| Service card number | Condensed 400 | 13px | 0.2em | — | — |
| Service card title (h3) | Condensed 600 | `clamp(26px, 2.6vw, 33px)` | — | 1.06 | — |
| Email link | Condensed 600 | `clamp(28px, 5vw, 56px)` | -0.01em | 1.1 | — |
| Footer | Condensed 600 | 14px | 0.14em | — | uppercase |

Body paragraphs use `text-wrap: pretty` and measure caps (`max-width: 62ch` for supporting copy).

### Layout & spacing
- Content container: `max-width: 1180px; margin: 0 auto`.
- Horizontal padding, every section: `clamp(22px, 5vw, 64px)`.
- Vertical padding: standard sections `clamp(52px, 8vw, 104px)`; hero `clamp(46px, 9vw, 120px)` top /
  `clamp(52px, 8vw, 104px)` bottom; contact `clamp(56px, 9vw, 116px)`; footer `26px`.
- Section separation: `border-bottom: 1px solid rgba(29,31,32,0.16)` on hero, intro, services, about.
- `box-sizing: border-box` globally; `min-width: 320px` and `overflow-x: hidden` on the page wrapper;
  `scroll-behavior: smooth` and `-webkit-text-size-adjust: 100%` on `html`.
- **Radius is 0 everywhere.** Nothing is rounded (the design system's rule: cards, figures and buttons
  are square-cornered line drawings). No box-shadows are used anywhere on this page.

## Screens / Views

Single view, top to bottom.

### 1. Hero (`<header>`)
Purpose: state who the company is in one screen.
Layout: `position: relative; overflow: hidden`, bottom hairline. Three absolutely positioned
decorative layers behind the content, then the 1180px content column.

Decoration (all `pointer-events: none`, `aria-hidden`):
- **Blueprint grid** (toggleable, default on): `position: absolute; inset: 0`; two linear gradients —
  `linear-gradient(to right, rgba(29,31,32,0.055) 1px, transparent 1px)` and the `to bottom`
  equivalent; `background-size: 68px 68px`; faded out with
  `mask-image: linear-gradient(to bottom, rgba(0,0,0,0.9), transparent 92%)`.
- **Outer arc**: `top: -34vw; right: -20vw; width/height: 74vw` (max 1000px), `border-radius: 50%`,
  `1px solid rgba(89,128,166,0.4)`.
- **Inner arc**: `top: -22vw; right: -8vw; width/height: 50vw` (max 680px), `border-radius: 50%`,
  `1px solid rgba(89,128,166,0.22)`.

Content, in order:
1. Wordmark row — flex, `gap: 14px`, `margin-bottom: clamp(40px, 8vw, 96px)`: an 11×11px square with
   `1px solid #5980a6` border (no fill), then the text `Impact Intelligence, LLC`.
2. Eyebrow: `Data Science & Technology Consulting`, color `#416180`, margin-bottom
   `clamp(16px, 2.5vw, 26px)`.
3. H1: `Impact Intelligence`, margin-bottom `clamp(22px, 3vw, 34px)`.
4. Subhead: `Machine learning, analytics, and engineering applied to decisions that carry weight.`
   color `#2b2b2d`, margin-bottom `clamp(30px, 4.5vw, 46px)`.
5. Button row — flex, wrap, `gap: 14px`:
   - **Primary** `Start a conversation` → `#contact`. Fill `#5980a6`, text `#f2f2f3`,
     `border: 1px solid #5980a6`, padding `15px 30px`, `min-height: 48px`, inline-flex centered.
     Hover: background and border `#416180`.
   - **Secondary** `What we do` → `#services`. Transparent, text `#1d1f20`,
     `border: 1px solid rgba(29,31,32,0.24)`, same padding/height. Hover: border `#5980a6`,
     text `#416180`.

### 2. The Practice (`<section>`)
Purpose: brief company introduction.
Layout: `display: flex; flex-wrap: wrap; gap: clamp(28px, 5vw, 72px); align-items: flex-start`.
Left column `flex: 1 1 180px; max-width: 280px` holds the label. Right column `flex: 3 1 400px;
min-width: 0` holds the copy. Below roughly 700px the copy wraps under the label — that is the
intended mobile stack. (Do not reimplement this with `repeat(auto-fit, …)`; that produced empty
columns at mid widths.)

Copy (verbatim):
- Label: `The Practice`
- Lead (`clamp(20px, 2.2vw, 27px)`, margin-bottom 22px): "Impact Intelligence is a boutique data
  science and technology practice. We build the models, pipelines, and analysis that turn an
  organization's data into decisions it can defend."
- Body (`#424244`, 62ch): "Engagements are sized for mid-market companies, startups, nonprofits, and
  consulting partners that need senior technical work without a large program built around it. Every
  engagement is delivered hands-on, from problem framing through the system that runs in production."

### 3. Services (`<section id="services">`)
Purpose: the four practice areas, one line each.
Header row: flex, `align-items: baseline; justify-content: space-between; gap: 20px`, margin-bottom
`clamp(28px, 4vw, 48px)` — label `Services` left, meta `Four practice areas` (`#7a7a7d`) right.

Card grid: `display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
gap: clamp(14px, 2vw, 22px)`. Each card is its own bordered object — **do not** draw the rules with a
tinted container background and 1px gaps (empty cells then paint as a gray block).

Each card (`<article>`): `position: relative; border: 1px solid rgba(29,31,32,0.16);
padding: clamp(26px, 3.4vw, 40px) clamp(22px, 2.6vw, 32px); display: flex; flex-direction: column;
gap: 12px`. Contents: number (`#5980a6`, toggleable), `<h3>` title, one-line `<p>` in `#424244`.

Registration marks: small "+" glyphs, `font: 400 15px/1 'Barlow Condensed'`,
`color: rgba(29,31,32,0.55)`, `aria-hidden`, absolutely positioned just outside the card edge —
`top: -7px`, `bottom: -8px`, `left: -7px`, `right: -6px`. Placement per card is deliberate and
asymmetric (this reads as a plate of drawn objects, not a repeated motif):

| # | Title | One-liner | Marks |
| --- | --- | --- | --- |
| 01 | Data Science | Framing the real question, then building the analysis or experiment that answers it. | top-left, bottom-right |
| 02 | Machine Learning & AI | Model development and deployment, from prototype through systems that hold up in production. | bottom-right |
| 03 | Analytics & Business Intelligence | Pipelines, metrics, and reporting that give a team one reliable view of its operations. | bottom-right |
| 04 | Technical Consulting | Architecture, tooling, and delivery guidance for teams building their own data capability. | top-right, bottom-right |

### 4. About (`<section id="about">`)
Same flex label/copy structure as The Practice.

Left column: label `About` (margin-bottom 20px) above a drawn figure — `aria-hidden`,
`width: 100%; max-width: 260px; aspect-ratio: 1; border: 1px solid rgba(29,31,32,0.16)`, containing
four absolutely positioned children: a circle at `inset: 18%` with `1px solid rgba(89,128,166,0.5)`
and `border-radius: 50%`; a circle at `inset: 34%` with `1px solid rgba(89,128,166,0.32)`; a 1px
horizontal line at `top: 50%` spanning full width in `rgba(29,31,32,0.14)`; a 1px vertical line at
`left: 50%` spanning full height in the same color.

Copy (verbatim — factual claims are the owner's; **do not embellish, and do not add clients,
testimonials, statistics, addresses, certifications, or company history anywhere on this site**):
- Lead (`clamp(19px, 2.1vw, 25px)`, margin-bottom 22px): "A single-member practice, led by a machine
  learning PhD with applied experience across energy and utilities, healthcare equipment, and
  large-catalog retail operations."
- Body 1 (`#424244`, 62ch, margin-bottom 16px): "Those are environments where the data is imperfect,
  the constraints are operational, and a model only matters if the people who rely on it can act on
  what it says. That shapes how the work gets done: understand the business problem first, keep the
  method appropriate to it, and leave behind something a client's own team can run."
- Body 2 (`#424244`, 62ch): "Engagements range from focused analysis and model development to
  longer-term advisory work alongside internal teams."

### 5. Contact (`<section id="contact">`)
Full-width steel field: `background: #1d2d3d; color: #f2f2f3`, padding `clamp(56px, 9vw, 116px)`
vertical.
- Label `Contact` in `#94bce3`, margin-bottom `clamp(24px, 4vw, 40px)`.
- Paragraph (`clamp(19px, 2.1vw, 25px)`, `rgba(242,242,243,0.86)`, `max-width: 46ch`, margin-bottom
  `clamp(28px, 4vw, 40px)`): "Describe the problem you're working on and we'll tell you honestly
  whether it's a fit."
- Email link: `inline-block`, `href="mailto:carl@impact-intelligence.com"`, text
  `carl@impact-intelligence.com`, color `#f2f2f3`, no underline,
  `border-bottom: 1px solid rgba(148,188,227,0.5)`, `padding-bottom: 6px`, `word-break: break-word`.
  Hover: text and border `#94bce3`.

### 6. Footer
`background: #1d2d3d`, `color: rgba(242,242,243,0.6)`,
`border-top: 1px solid rgba(242,242,243,0.14)`, padding `26px` vertical.
Flex, `flex-wrap: wrap`, `gap: 12px 28px`, `justify-content: space-between`, `align-items: center`.
Left: `© 2026 Impact Intelligence, LLC`. Right: `Data Science & Technology Consulting`.

## Interactions & Behavior
- Two in-page anchors (`#contact`, `#services`) with `scroll-behavior: smooth` on `html`.
- One `mailto:` link. No forms, no JS behavior required — the page can ship with zero JavaScript.
- Hover states as specified per element above; no transitions were specified (a 120–150ms
  `background-color, border-color, color` ease is acceptable if you want them).
- Focus: `:focus { outline: none }` plus
  `:focus-visible { outline: 2px solid #5980a6; outline-offset: 3px }`. Never leave the browser
  default ring. On the dark contact field, `#94bce3` is the better focus color.
- `::selection { background: rgba(89,128,166,0.3) }`.
- Responsive: entirely fluid via `clamp()` and the flex/grid rules above — no media queries in the
  prototype. Verify 320, 375, 768, 924, 1180, and 1440px; 924px was where the earlier grid approach
  broke, so check it specifically. Minimum tap target 48px (the buttons).
- Reduced motion: nothing animates, but consider
  `@media (prefers-reduced-motion: reduce) { html { scroll-behavior: auto } }`.

## State Management
None. Static page.

Two content/appearance switches exist in the prototype as component props; in a static rebuild they
are simply authoring decisions (keep both on, matching the approved design):
- `email` — the address shown and used in the `mailto:` (`carl@impact-intelligence.com`).
- `showGrid` — hero blueprint grid overlay (on).
- `showNumbers` — 01–04 numbers on the service cards (on).

## Assets
- No images, photographs, or icons are used. All decoration is CSS (borders, radial borders,
  gradient grid) and typographic "+" glyphs.
- Fonts: Google Fonts Barlow and Barlow Condensed. Self-hosting them is recommended for a production
  site (subset to latin, `font-display: swap`).
- Still needed from the owner: favicon, an OG/Twitter share image, and the final `<title>`/description
  if different from the prototype's:
  - title: `Impact Intelligence, LLC — Data Science & Technology Consulting`
  - description: `Impact Intelligence is a boutique data science and technology consultancy
    specializing in machine learning, AI, analytics, and business intelligence.`

## Design system
This page is built on the **Industry** design system — steel-blue on a light technical ground,
Barlow Condensed over Barlow, square corners, hairline borders, "+" registration marks, no fills on
cards or figures, and no decorative color beyond the steel accent. `design-system/styles.css` is the
system's token + component stylesheet and `design-system/industry-readme.md` is its guide. Take
colors, type, and spacing from the tokens rather than re-deriving them; if you build with a CSS
framework, map the tokens to it rather than adopting the framework's defaults.

## Files
- `design/Impact Intelligence.dc.html` — the approved design prototype (open in a browser).
- `design-system/styles.css` — Industry design tokens and component classes.
- `design-system/industry-readme.md` — Industry design system guide.

## Suggested first commits
1. Repo init, README, license/owner note, static host config.
2. `index.html` skeleton with real semantic landmarks (`header`, `main`, `section`, `footer`) and the
   final copy verbatim from this document.
3. `styles.css` — token `:root` block first, then section-by-section styles.
4. Meta/OG tags, favicon, self-hosted fonts.
5. Accessibility and responsive pass at the widths listed above (target: axe clean, all text at least
   4.5:1 — note the steel accent is only rated for large text and chrome, which is how it is used here).
