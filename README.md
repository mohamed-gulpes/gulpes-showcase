# Gulpes — Official Website

Source code for [gulpes.com](https://gulpes.com), the brand site for Gulpes digital products.

## Overview

Gulpes is a product studio that designs and ships practical tools for personal growth, motivation, and real life. This repository contains the static website that serves as the public-facing brand hub — showcasing products, services, and the team behind Gulpes.

## Pages

| File | URL | Purpose |
|------|-----|---------|
| `index.html` | gulpes.com | Homepage — products, testimonials, services, founder |
| `med.html` | med.gulpes.com | Mohamed Douaré's profile page |
| `privacy.html` | gulpes.com/privacy.html | Privacy policy |
| `terms.html` | gulpes.com/terms.html | Terms & conditions |

## Features

- **Dark / Light mode** — defaults to dark, toggleable with OS preference detection and `localStorage` persistence
- **SEO-optimized** — Open Graph, Twitter Cards, JSON-LD structured data (Organization, SoftwareApplication, Person, WebSite), canonical URLs, sitemap, robots.txt
- **Fully static** — no build step, no framework, no dependencies
- **Responsive** — mobile-first layout with media queries

## Structure

```
├── index.html          # Homepage
├── med.html            # Founder profile
├── privacy.html        # Privacy policy
├── terms.html          # Terms & conditions
├── robots.txt          # Crawler directives
├── sitemap.xml         # Sitemap for search engines
├── css/
│   └── main.css        # All styles (theme variables, layout, components)
└── img/                # Logos, icons, and assets
```

## Local Development

Serve the files with any static server:

```bash
python3 -m http.server 8080
```

Then open [http://localhost:8080](http://localhost:8080).

## Deployment

This is a fully static site. Deploy by copying all files to any web server or static hosting provider (Netlify, Vercel, Cloudflare Pages, S3 + CloudFront, etc.).

## License

All rights reserved — Gulpes 2026.
