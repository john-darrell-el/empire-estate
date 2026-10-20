# Empire of Morocco — Website Estate (Four-Site Monorepo)

Single repository carrying the complete deployed tree of all four public sites.
Edition: **2026-10-20** · 141 files · 215,541,159 bytes · full-tree SHA-256 manifest: `MANIFEST-SHA256_2026-10-20.txt`

## Folder ↔ site ↔ host mapping

| Folder | Domain | Cloudflare Pages project | Deploy method (current) |
|---|---|---|---|
| `tribunal/` | tribunal.empireofmorocco.org | tribunal Pages project | Direct-upload zip (full tree) |
| `main/` | empireofmoroccotrade.com | main-site Pages project | Direct-upload zip (full tree) |
| `aop/` | aop.empireofmoroccotrade.com | aop Pages project | Direct-upload zip (full tree) |
| `store/` | store.empireofmoroccotrade.com | store Pages project | Direct-upload zip (full tree) |

All four are pure static sites — no build step, no dependencies.

## Deploy discipline (standing)

1. **Every deployment carries the complete tree of that site, never a delta.**
2. Hash-verify before handover; the manifest at this root is the reference of record.
3. Superseded deploy artifacts are renamed `SUPERSEDED-YYYY-MM-DD__…`, never deleted — and kept **out of this repository** (see `.gitignore`).
4. `/cdn-cgi/…` references inside some HTML are Cloudflare runtime injections (email protection). They are not files, are served by Cloudflare at runtime, and are expected to be absent from the repo.
5. `main/downloads/` carries frozen prior versions (e.g. v4.1 PDFs) deliberately — present of record even when no page links them.
6. `tribunal/` carries of-record companion files (prior editions, errata, manifests) that are intentionally unlinked but served at stable URLs.

## Using this repo as backup (current mode)

After any deploy: copy that site's deployed tree into its folder here, commit, push.
Verify first: `sha256sum --check MANIFEST-SHA256_2026-10-20.txt` (regenerate the manifest when the tree changes).

## Optional later: push-to-deploy (git integration)

Cloudflare Pages supports monorepos — up to 5 projects per repository. If you ever switch:
- Create a **new** Pages project per site (Direct-Upload projects cannot be converted in place).
- Build settings per project: Framework preset = None · Build command = *(empty)* · Build output directory = the site's folder (`tribunal`, `main`, `aop`, or `store`).
- Set **build watch paths** per project to its own folder, so a change to one site doesn't redeploy the others.
- Move each custom domain: remove from the old project → add to the new one → verify HTTPS → retire the old project.
Until then, direct-upload from the dashboard remains the deployment path and this repo is the versioned backup.

## Provenance

Assembled 2026-10-20 from the verified staging trees of record. Every file byte-verified
(SHA-256) against its source at assembly; every internal download link in every HTML page
verified present at assembly (audit: 0 missing across all four sites).
