# anatomy-catalog

The published device catalog for [Anatomy](https://github.com/warpling/Anatomy) —
what each piece of Apple hardware physically is, and where its parts are.

**This repository is public so the file can be fetched over plain HTTPS.**
The package that reads it is private; this is only the data, which is
cutout widths and button positions.

```
https://cdn.jsdelivr.net/gh/warpling/anatomy-catalog@main/devices.json   (CDN, 7-day cache)
https://raw.githubusercontent.com/warpling/anatomy-catalog/main/devices.json   (origin, 5-min cache)
```

**Not GitHub Pages.** `warpling.github.io` has a `CNAME` of `growpixel.com`,
and growpixel.com is served by Netlify, so every GitHub Pages project site on
this account redirects to a domain that 404s it. That affects more than this
repo; it is worth fixing or removing that CNAME someday.

Both URLs above are gzipped (~1.7 KB), carry an `ETag`, and sit behind a CDN.
jsDelivr caches `@main` at the edge for 12 hours — fine for a file that
changes a few times a year, and purgeable on demand:

```
curl https://purge.jsdelivr.net/gh/warpling/anatomy-catalog@main/devices.json
```

Apps fetch it conditionally (`If-None-Match`), at most once a week, and
adopt it only when its `revision` is higher than the one they already have.
An app that never reaches this file keeps the copy compiled into it, so
nothing here is load-bearing for anyone's launch.

## Publishing a change

Edit `Sources/Anatomy/Resources/devices.json` in the Anatomy repo, bump its
`revision`, then run `scripts/publish-catalog.sh` from there. Do not edit
this copy by hand — it is a publication, not a source.

## Rolling back

Publish the old contents under a HIGHER revision number. Apps ignore
anything that is not strictly newer than what they hold, so re-publishing an
older revision does nothing at all.
