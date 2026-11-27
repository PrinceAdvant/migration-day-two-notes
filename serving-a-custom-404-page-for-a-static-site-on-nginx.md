# Serving a custom 404 page for a static site on nginx

Most static site generators build a `404.html` file, but nginx does not use it unless you tell it to. Without the setting, visitors who follow a broken link see the plain nginx error page, which looks like the whole site is down.

Add `error_page` to the server block:

```
server {
    listen 80;
    root /usr/share/nginx/html;
    error_page 404 /404.html;
    location = /404.html {
        internal;
    }
    location / {
        try_files $uri $uri/ $uri.html =404;
    }
}
```

The `internal` line stops people from loading `/404.html` directly with a 200 status. The `try_files` order lets clean URLs like `/about` find `about.html`, and ends with `=404` so missing pages return a real 404 status instead of a 200 with error content. That status matters: search engines treat a 200 error page as a soft 404, which wastes crawl budget.

Do not combine this with an SPA fallback to `index.html` unless the site really is a single page app, or every missing URL will return 200.

Test with `curl -sI https://example.com/does-not-exist` and expect `404`. Then load it in a browser to check that CSS paths in the 404 page are absolute. Build and serve options for static sites are in [static site deployment in Peon](https://peon.sh/docs/static-sites).
