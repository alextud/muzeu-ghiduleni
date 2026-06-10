# Muzeul din Ghiduleni — site

Static brochure site for a history & ethnography museum in Ghiduleni (Rezina, Moldova).
Content is in Romanian.

## Stack & deploy
- **Jekyll** site hosted on **GitHub Pages** (default "deploy from branch" build — no Actions workflow).
- Live at **https://muzeu-ghiduleni.eu** (`CNAME` + `url` in `_config.yml`).
- GitHub Pages builds it server-side, so its whitelisted plugins (e.g. `jekyll-sitemap`) work without a Gemfile.
- `_site/` is the build output and is gitignored — never edit or commit it.

## Local build
No local Jekyll toolchain — build with Docker:
```
docker run --rm -v "$PWD":/srv/jekyll -w /srv/jekyll jekyll/jekyll:4 jekyll build
```

## Structure
- Pages are top-level `.html` files (`index`, `despre`, `colectii`, `evenimente`, `satul-ghiduleni`), each with its own `<head>` and an empty `---` front-matter block so Jekyll processes Liquid.
- `_includes/` holds the shared `header.html` (nav) and `footer.html` — the head is NOT shared.
- `assets/` holds all images and `assets/css/site.css` (shared stylesheet).

## Conventions
- Each page carries its own Open Graph tags + a dedicated 1200x630 `assets/og-*.jpg` share image (kept under ~300KB for WhatsApp).
- Canonical URLs use `{{ page.url | absolute_url }}`.
- Homepage carries `Museum` JSON-LD structured data.

## Known follow-ups
- Images are heavy (~24MB total, several >1MB). Convert to WebP, resize, add `loading="lazy"` and `width`/`height`. Optional: responsive `srcset` on hero images.
