# Keeping an old domain alive as a redirect after a rebrand

After a rebrand, the old domain still carries links, bookmarks and search rankings. Letting it expire or pointing it at a parked page throws that away. The right setup is a permanent redirect that preserves the path, served with a valid certificate.

Keep the old domain registered for years and leave its DNS pointing at your server. Then add a redirect at the proxy that keeps the path and query string:

```
old-name.com, www.old-name.com {
    redir https://new-name.com{uri} permanent
}
```

The `{uri}` part matters. Without it, every old deep link lands on the new homepage, which frustrates users and loses the page level ranking signal.

The old hostnames still need certificates, because most links are https and the browser checks the certificate before it sees the redirect. Make sure HTTP challenges for those names reach the proxy.

Test a few deep links with `curl -sI https://old-name.com/blog/post?x=1` and confirm a single 301 or 308 hop to the exact new URL, not a chain. Then update canonical tags and the sitemap on the new site and use the Change of Address tool in Search Console. How to attach several domains to one service is described in [custom domains and SSL in Peon](https://peon.sh/docs/domains-and-ssl).
