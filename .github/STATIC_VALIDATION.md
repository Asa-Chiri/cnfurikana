# Static asset integrity and JavaScript syntax

Run from the repository root with Git and Node.js 22:

```sh
node .github/scripts/validate-static.cjs
```

CI checks the generated `index.html` script, link, image and tile-image
references, web manifest icons, CSS `url(...)` assets, precache entries, and
service-worker `importScripts` URLs against the case-sensitive Git file list.
Relative and site-root paths are normalized; query strings and fragments are
removed. External URLs, data URLs, anchors and empty dynamic image placeholders
are ignored. Local references outside the asset root fail.

All tracked `.js` files and inline entrypoint scripts are parsed with Node's
JavaScript parser without execution. No packages are installed. This is static
validation of the committed Vue output, not a Vue build, browser test, runtime
compatibility check, or check of network services. The small HTML/CSS extractors
cover the generated markup here; they are not general-purpose parsers. Dynamic
URLs constructed by application JavaScript are outside this check.
