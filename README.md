# anatomy-catalog

The published device catalog for [Anatomy](https://github.com/warpling/Anatomy) —
what each piece of Apple hardware physically is, and where its parts are.

**This repository is public so the file can be fetched over plain HTTPS.**
The package that reads it is private; this is only the data, which is
cutout widths and button positions.

```
https://warpling.github.io/anatomy-catalog/devices.json
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
