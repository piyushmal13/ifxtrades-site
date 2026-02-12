# IFX Trades Site

High-conversion static marketing website for IFX Trades products and events.

## What this repository contains

- `index.html` — Main landing page with hero, products, events strip, events grid, and lead form.
- `prime.html` — IFX Prime product page.
- `suite.html` — IFX Suite product page.
- `algos.html` — IFX Labs / algorithmic automation page.
- `event.html` — Dynamic event detail page loaded by `?slug=...`.
- `sx66.html` — Legacy standalone concept page (not the primary production entry point).
- `1743840678265.jpg` — Local image asset.

## Architecture

This site is intentionally lightweight and ships as static HTML files:

- TailwindCSS via CDN
- Lucide icons via CDN
- GSAP animations via CDN
- Supabase JS client for dynamic links and events

No build step is required.

## Dynamic data dependencies (Supabase)

The pages use a Supabase project to hydrate runtime content:

- `button_links` table: sets CTA destinations by `data-link` key.
- `events` table: powers event strip, events grid, and `event.html` detail rendering.

If these tables are unavailable, core static content still renders, but dynamic links/events may be hidden or fallback.

## Local preview

From repo root:

```bash
python3 -m http.server 8080
```

Then open:

- `http://localhost:8080/index.html`

## Hosting (production)

You can deploy this repo to any static host.

### Option 1: Netlify (fastest)

1. Push this repo to GitHub.
2. In Netlify: **Add new site → Import from Git**.
3. Build settings:
   - Build command: *(leave empty)*
   - Publish directory: `/` (repo root)
4. Deploy.
5. Add custom domain and enable HTTPS.

### Option 2: Vercel

1. Import repo in Vercel.
2. Framework preset: **Other**.
3. Build command: none.
4. Output directory: `.`
5. Deploy and connect your custom domain.

### Option 3: GitHub Pages

1. Commit files to default branch.
2. Enable **Pages** in repository settings.
3. Source: deploy from branch root.
4. Use custom domain via CNAME if needed.

## Business go-live checklist

- Replace placeholders like `YOUR_PHONE` and any temporary links.
- Verify all `data-link` keys have active rows in `button_links`.
- Confirm event rows include valid `slug`, `event_time`, and registration/live links.
- Validate mobile UX for `index`, `prime`, `suite`, `algos`, and `event` pages.
- Set SEO essentials (title, description, OG image) for each page.
- Add analytics + conversion tracking (Meta Pixel / Google Ads / GA4).

## Immediate roadmap

1. Add one shared JS file for common logic (menu, Supabase client, link hydration).
2. Add one shared CSS token file for brand consistency.
3. Split long inline scripts in `index.html` into maintainable modules.
4. Replace `sx66.html` or remove from production nav if legacy.
