# Building a redirect map before you switch website builders

Changing website builders is mostly a design decision, but it quietly becomes an SEO decision the moment URLs change. Old pages that 404 lose the links pointing at them.

Start with a list of every URL that matters: the sitemap, pages with backlinks, and pages that get search traffic in your analytics. Put them in a two column file:

```
/blog/launch-notes      /blog/launch-notes-2026
/pricing.html           /pricing
/features/teams         /teams
```

Then implement each line as a permanent 301 in the new builder or at the reverse proxy. After launch, crawl the old list and confirm every entry returns a single 301 hop to a 200 page, not a chain.

Keep titles, headings and internal links close to the old versions for the first few weeks so you can tell redirect problems from content changes. A broader look at [comparing website builders for SEO](https://peon.sh/blogs/tempo-vs-framer-website-deployment-seo-comparison) covers deployment and performance trade-offs.
