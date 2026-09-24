# Agile Networks website (v3.1)

Marketing site for Agile Networks (agilenet.works).

## Files
- `index.html` - the whole site: all pages, styles and scripts. Pages are shown by URL hash (`#services`, `#firms`, `#chatterbox`, and so on).
- `public/substack.json` - latest Chatterbox posts from Substack. Generated automatically; don't edit by hand.
- `public/linkedin.json` - recent LinkedIn posts shown on Chatterbox. Edit by hand (see below).
- `scripts/fetch-substack.mjs` - reads the Substack RSS feed and writes `public/substack.json`.
- `.github/workflows/substack-refresh.yml` - runs that script every day at 7am Eastern and commits any new posts.
- `package.json` - runs and builds the site with Vite. `npm run build` refreshes Substack posts first.

## Chatterbox: how it stays fresh

**Substack (automatic).** Publish on Substack as normal. Within a day the GitHub Action picks up the new post and the Chatterbox page shows the latest three. To refresh right away: GitHub > Actions > "Refresh Substack posts" > Run workflow.

If you move Substack to a custom domain (e.g. chatterbox.agilenet.works), change `SUBSTACK_URL` at the top of `scripts/fetch-substack.mjs`.

**LinkedIn (about 30 seconds, by hand).** LinkedIn doesn't offer a public feed, so edit `public/linkedin.json` in GitHub (pencil icon) when you post something worth featuring. The page shows the three newest entries.

    {
      "profile": "https://www.linkedin.com/in/your-profile",
      "posts": [
        { "date": "2026-10-01", "text": "First line or two of the post.", "url": "https://www.linkedin.com/feed/update/..." },
        { "date": "2026-09-23", "text": "Older post...", "url": "https://www.linkedin.com/feed/update/..." }
      ]
    }

Newest first. Keep the commas and quotes exactly as shown. If the file is empty or broken, the page falls back to a "Follow on LinkedIn" link instead of breaking.

## Run locally
    npm install
    npm run dev

## Build
    npm run build   (output goes to dist/)

## Before going live
- Remove the "Build notes (preview only)" footer link and the `#notes` page.
- Replace placeholders: logo, photos, videos, client logos, testimonial, phone, email, booking link, pricing.
- Connect the contact form to a real form handler. It currently shows a "preview only" message and sends nothing.
- For better SEO, split the hash-based pages into separate pages with their own URLs.
