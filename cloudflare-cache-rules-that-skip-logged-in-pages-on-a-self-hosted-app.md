# Cloudflare cache rules that skip logged in pages on a self-hosted app

Putting Cloudflare in front of a self-hosted app and enabling "cache everything" speeds up public pages and can also serve one user's dashboard to another. Caching has to know who is logged in.

Build the rules in order. Bypass cache for any request carrying your session cookie, for example a cookie name that contains `session`. Bypass for paths like `/admin`, `/account` and `/api`. Then cache everything else with an edge TTL that suits how often content changes.

Your origin should help. Send `Cache-Control: private, no-store` on personalised responses and `public, max-age=...` on public ones. Cloudflare respects origin headers unless a rule overrides them, so correct headers are a safety net if a rule is wrong.

Purge on deploy. A CI step that calls the purge API for changed URLs, or everything for small sites, avoids stale pages.

Test logged out and logged in with `curl -I` and look at `cf-cache-status`: you want `HIT` for public pages and `BYPASS` or `DYNAMIC` for private ones. How each service fits is discussed in [Peon and Cloudflare compared](https://peon.sh/compare/peon-vs-cloudflare).
