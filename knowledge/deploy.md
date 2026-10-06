# How GitOrange is deployed

- One Cloudflare Worker serves the API, the SPA and the git endpoint. `yarn deploy` runs `vite build && wrangler
deploy`.
- Each deployer keeps their own `wrangler.jsonc` (gitignored), copied from `wrangler.jsonc.example`. New bindings
  must be added to it by hand before deploying, or the feature runs without them (some fall back, some fail).
- Deploy `main` from a clean checkout of `origin/main`, never from a feature branch.
- Migrations: `yarn db:migrate:prod` (D1 `--remote`). Additive migrations go before the deploy. A migration that
  drops something the deployed code still reads goes after the deploy — or in a later release.
- Secrets: `wrangler secret put NAME`. R2 pre-signing needs `R2_ACCESS_KEY_ID` / `R2_SECRET_ACCESS_KEY`.
- Durable Objects need both a binding and an `exports` entry with `storage: "sqlite"`.
- Containers (Actions runner) build from `actions/runner/Dockerfile` at deploy time; Docker must be running.
- A daily cron runs Actions retention and stale-review recovery.
- Typegen: `yarn cf-typegen` reads `wrangler.jsonc.ci`.
