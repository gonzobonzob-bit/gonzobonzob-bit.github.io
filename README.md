# gonzobonzob-bit.github.io

User-site repo. Its only real job is to serve **one file**:

```
https://gonzobonzob-bit.github.io/robots.txt
```

## Why this repo exists

Crawlers fetch `robots.txt` only from the **root of a host**. A `robots.txt` committed
inside a project-site repo — `pv-tools/robots.txt`, `pv-ct-review/robots.txt` — is served
at `gonzobonzob-bit.github.io/pv-tools/robots.txt`, a path no crawler ever requests. Those
files are inert.

Every GitHub Pages project site under this account shares the hostname
`gonzobonzob-bit.github.io`. This repo is the *only* one that can publish a file at that
host's root, so the `robots.txt` here is the only one that has any effect — and it governs
every project site at once:

| Path | Repo |
|---|---|
| `/pv-tools/**` | `pv-tools` — PW3 String Analyzer, Lynx, Magpie |
| `/pv-ct-review/**` | `pv-ct-review` — Lynx, standalone/legacy |
| `/magpie-notes/**` | `magpie-notes` — Magpie, standalone/legacy |
| `/my-games/**` | `my-games` |
| `/solar-reference/**` | `solar-reference` |

The policy is a host-wide `Disallow: /` plus ~30 named AI and dataset crawlers, several of
which ignore a wildcard rule but honor their own named block.

`index.html` is a deliberately empty placeholder. **It does not link to the tools** — a
public root page listing their URLs would make them more discoverable, which is the
opposite of the point.

## What this does and does not do

**Does:** keeps every page on this host out of search engine results, for crawlers that
honor the standard.

**Does not:** make anything private. Three gaps worth understanding:

1. **`robots.txt` is voluntary.** It is a request. Crawlers that ignore it — and scrapers
   generally do — are unaffected. The per-page `<meta name="robots" content="noindex">`
   tags are the stronger control, since a crawler that has already fetched the page still
   sees them.
2. **The repo list is public.** Anyone can view github.com/gonzobonzob-bit and read off
   every repo name, and a project site's URL follows mechanically from its repo name. The
   Pages URLs are effectively enumerable by anyone looking at the account — they are not
   secrets. Making the tool repos private would close this path, but on a free plan that
   also disables Pages.
3. **GitHub controls github.com headers.** The repository pages themselves stay indexable
   on github.com regardless of anything in this repo.

Practical upshot: treat these URLs as unlisted, not confidential. Don't put customer
names, addresses, or site data into any of the tools.

## Deploy

GitHub Pages, branch `main`, root `/`. After enabling Pages, verify with:

```bash
curl -sI https://gonzobonzob-bit.github.io/robots.txt   # expect 200
curl -s  https://gonzobonzob-bit.github.io/robots.txt   # expect the policy, not a 404 page
```

A 404 means Pages is not enabled or has not finished its first deploy.
