# Easy Designs historical archive

This repository preserves the former Easy Designs landing page as a static,
explicitly historical archive. Deploy **only `public/`**. No PHP server,
database, build dependencies, or active business/contact form is required.

## Hosting

Connect this repository to Netlify, use branch `main`, and publish `public`.
The repository's `netlify.toml` supplies the publish directory.
`public/_redirects` preserves `/index.php` and `/portfolio.php` as HTTP redirects.
Although the landing page looks like a single page, its mobile/no-JavaScript
portfolio links originally rendered nine distinct query-driven detail pages.
All nine are preserved under `/portfolio/`, with query-specific redirects.
The obsolete random-quote endpoint leads to an archival notice; its polling
timer and contact form have been removed. The initial quote remains visible.

Netlify is used because GitHub Pages cannot supply these arbitrary server
redirects. This also avoids treating an unchanged consulting landing page as
an active business hosted by Pages. Do not use GitHub Pages A records for this
Netlify deployment.

Add `easy-designs.net` and `www.easy-designs.net` to the Netlify site, choose the
apex as primary, and use the DNS values Netlify supplies. Keep the old server
running until the user changes DNS and HTTPS and representative pages/assets
pass live checks. Preserve unrelated DNS and mail records.

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

The local standard-library server does not emulate Netlify redirects. GitHub
Actions checks the deployment boundary and forbidden dynamic/CDN dependencies.
Validate redirects in a Netlify preview before DNS cutover. The separate blog
at `blog.easy-designs.net` is not included in this archive and must be audited
before retiring a server that also hosts it.
