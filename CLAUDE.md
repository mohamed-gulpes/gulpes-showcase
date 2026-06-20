# CLAUDE.md — Gulpes website (gulpes.com)

## Project overview

Static brand/marketing website for **Gulpes**, a product studio. It showcases
products (flagship app "Self"), testimonials, services, and the founder. The
site is bilingual: English at the root, French under `fr/`.

## Stack

- **Plain static HTML + CSS + a little vanilla JS.** No framework, no bundler,
  no package manager, no dependencies.
- Single global stylesheet: `css/main.css` (~1100 lines) using CSS custom
  properties for theming and BEM-ish component class names.
- Fonts: Google Fonts (Roboto) loaded via `<link>`.
- Inline `<script>` only — the theme toggle (dark/light). There are **no** JS
  files and **no** build/transpile step.
- Images are `.webp` / `.svg` / `.gif` in `img/`.

## How to preview / build

There is **no build step** — the files are served as-is. Preview with any
static server, e.g.:

```bash
python3 -m http.server 8080   # then open http://localhost:8080
```

Opening `index.html` directly via `file://` mostly works, but use a local
server so root-absolute links (`/fr/`, `/img/...` paths) and language
switching behave like production.

## Deployment

Static hosting (the `.htaccess` targets Apache/LiteSpeed, e.g. Hostinger).
Deploy by copying all files to the web root. **Caching:** `.htaccess` sets
no-cache headers, but a CDN may still cache — so after changing `css/main.css`
or any image, **bump the `?v=` query string** on its `<link>`/`<img>` URL in
every HTML file that references it (search for `?v=`).

## Structure

```
index.html              # EN homepage
med.html                # Founder profile (served at med.gulpes.com)
privacy.html            # Privacy policy (EN)
terms.html              # Terms & conditions (EN)
fr/                     # French mirror: index/med/privacy/terms.html
css/main.css            # ALL styles (theme vars, layout, components)
img/                    # logos, icons, assets (.webp/.svg/.gif)
robots.txt, sitemap.xml # SEO
.htaccess               # Apache/LiteSpeed cache headers
```

## Conventions actually used

- **Theming:** dark mode is the default. Colors come from CSS variables on
  `:root`; `[data-theme="light"]` overrides them, and a
  `@media (prefers-color-scheme: light)` block handles OS preference when no
  explicit choice is stored. A tiny inline script in `<head>` applies the
  saved `localStorage.theme` before paint; the toggle script lives before
  `</body>`. Add theme-able colors as variables, not hard-coded hex.
- **CSS:** one file, hyphenated component classes (e.g. `.featured-product`,
  `.product-card--upcoming`, `.section--alt`). Use existing variables/classes
  before inventing new ones.
- **Responsive:** mobile-friendly; breakpoints at `max-width: 768px` and
  `max-width: 480px`. Keep new layout responsive at those widths.
- **i18n:** every EN page has a French twin under `fr/`. The FR pages use
  relative `../css/` and `../img/` paths and `<html lang="fr">`. **When you
  change content/structure on an EN page, mirror it on the FR page** (and vice
  versa), and keep the `hreflang` alternate links consistent.
- **SEO:** pages carry meta description/keywords, Open Graph, Twitter Card,
  canonical + `hreflang`, and JSON-LD structured data. Preserve these when
  editing `<head>`; update `sitemap.xml` when adding a page.
- **Accessibility:** markup uses semantic landmarks (`header`/`main`/`footer`),
  `aria-label`s, alt text, and explicit `width`/`height` on images. Keep them.

## Rules

- Match the existing markup and CSS patterns — vanilla HTML/CSS, no framework,
  no new dependencies or build tooling.
- Keep changes accessible (semantic tags, alt text, aria labels) and responsive
  (test at 768px and 480px).
- Use existing CSS variables/classes; make colors theme-aware (dark + light).
- Keep EN and FR pages in sync; update `sitemap.xml`/`hreflang` for new pages.
- Bump `?v=` on changed asset URLs so caches refresh.

## Commit messages

Do **not** add any `Co-Authored-By: Claude` / Anthropic trailer to commits.
