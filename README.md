# AI Insider

AI Insider is a source-linked AI technology newsroom designed for Cloudflare Workers.

## Features
- Responsive editorial homepage and article routes.
- Five launch articles covering AI agents, specialist enterprise models, open-model transparency, robotics, and AI infrastructure.
- All six supplied Adsterra placements are included in the homepage template.
- Worker API for article listing and individual article retrieval.
- Cloudflare Workers AI-assisted daily article generation from RSS sources.
- Cloudflare KV persistence and a daily 09:00 UTC Cron Trigger.
- Token-protected manual publish and seed endpoints.

## Cloudflare bindings
- `ARTICLES`: KV namespace.
- `AI`: Workers AI binding.
- `ASSETS`: static assets binding.
- `ADMIN_TOKEN`: Worker secret for admin endpoints.

## Deploy
1. Create a Cloudflare KV namespace and replace the placeholder id in `wrangler.toml`.
2. Deploy `src/worker.js` with the contents of `public/` as assets, and bind the KV namespace as `ARTICLES`, Workers AI as `AI`, and static assets as `ASSETS`.
3. Add the secret `ADMIN_TOKEN`.
4. Configure Cron Trigger `0 9 * * *` (09:00 UTC daily).
5. Seed the initial five launch articles by POSTing to `/api/admin/seed` with `Authorization: Bearer <ADMIN_TOKEN>`.

The daily job reads public RSS feeds and uses the Workers AI binding. It publishes only when it can cite at least one source item; it skips a run rather than inventing an article when feeds or generation fail.

## Manual publish
`POST /api/admin/publish` with `Authorization: Bearer <ADMIN_TOKEN>`.

## Notes
- The editorial launch articles are dated 31 October 2026 and include source links.
- The homepage ad tags are supplied by the site owner. Ad delivery, account approval, and publisher compliance remain subject to Adsterra's terms.
- No paid API key is hard-coded.
