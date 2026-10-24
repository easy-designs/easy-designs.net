# Easy Designs historical archive

This repository preserves the former Easy Designs landing page as a static,
explicitly historical archive. Deploy **only `public/`**. No PHP server,
database, build dependencies, or active business/contact form is required.

## Hosting

GitHub Actions validates and deploys **only `public/`** from `main` to GitHub
Pages. In Settings > Pages, choose GitHub Actions as the source: branch
publishing accepts only `/` or `/docs`, not `/public`. Pull requests validate
and upload an artifact but do not deploy.
Although the landing page looks like a single page, its mobile/no-JavaScript
portfolio links originally rendered nine distinct query-driven detail pages.
All nine are preserved under `/portfolio/`, with query-specific JavaScript
redirects in the custom 404 page.
The obsolete random-quote endpoint leads to an archival notice; its polling
timer and contact form have been removed. The initial quote remains visible.

GitHub Pages cannot supply arbitrary HTTP redirects. Old PHP URLs initially
return HTTP 404, then redirect with JavaScript while preserving queries and
fragments. Without JavaScript, the 404 page links to the archive home. Unknown
portfolio projects fall back to the homepage's work section; unknown paths
remain on the 404 page. Canonical archive pages work without JavaScript.
`netlify.toml` and `public/_redirects` remain available for an optional Netlify
deployment with true HTTP redirects; Pages ignores those rules.

The custom domain is `easy-designs.net`, recorded in `public/CNAME` and Pages
settings. Set the apex A records to `185.199.108.153`, `185.199.109.153`,
`185.199.110.153`, and `185.199.111.153`; set `www` CNAME to
`easy-designs.github.io`. Enable HTTPS enforcement after certificate issuance.
Keep the old server until live DNS, TLS, and representative content checks
pass. Preserve unrelated DNS and mail records.

## Maintenance and validation

The archive contains downloaded HTML, CSS, JS, portfolio detail pages,
thumbnails and full-size lightbox images, and fonts. The existing licensed
jQuery dependency is local rather than fetched from a third-party CDN.
`migration-manifest.json` records original
URLs, local paths, media types, and output hashes. Edit the frozen public files
directly; do not restore a dependency on the retired origin.

```sh
python3 -m http.server 8080 --directory public
```

The local standard-library server does not serve the custom 404 automatically. GitHub
Actions checks the deployment boundary and forbidden dynamic/CDN dependencies.
Validate old PHP routes on Pages before accepting the cutover. The separate blog
at `blog.easy-designs.net` is not included in this archive and must be audited
before retiring a server that also hosts it.
