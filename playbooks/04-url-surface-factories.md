# URL surface factories

Factory sites mint many URLs from a taxonomy. Done well, they earn crawl and clicks. Done badly, they flood the index with thin near-duplicates and spend the crawl budget on junk.

Public examples of the pattern (not a dump of private generators):

- **CanAIFeel** (`canaifeel.com`) — a map of questions people already search, each question a playable page, hubs first (the map, the course).
- **Wafergraph** (`wafergraph.com`) — entity + segment graph: hubs (map, segments, tools), then company pages.
- **Who’s Starting** (`whosstarting.com`) — sport hubs → team pages → player pages.
- **Iron Strike** — same discipline if it exposes a public URL surface: taxonomy before mint, hubs before leaves.

## Pipeline (do not skip steps)

```text
taxonomy  →  factory schema  →  hubs-first mint (capped)  →  sitemap + IndexNow
```

1. **Taxonomy.** Name the types and the edges. Questions, companies, teams, players, segments. If you cannot draw the types on one page, you are not ready to mint.
2. **Factory schema.** Every mintable row has the same required fields: slug, title, hub parent, canonical path, uniqueness key, and a “why this is a real page” bar (search demand, entity exists, not a synonym of an existing slug).
3. **Hubs first, then leaves.** Ship the map / index / segment pages before you mint the long tail. Leaves inherit internal links from hubs; hubs must not wait for 10k leaves.
4. **Mint caps.** A batch has a number. Hit the cap, measure indexation + CTR, then mint the next batch. No flood.
5. **Sitemap + IndexNow.** New canonical URLs enter the sitemap in the same ship. Ping IndexNow (or equivalent) for the batch, not one URL per second all afternoon.

## Canonical discipline

Pick one public hostname per product — the **apex** if that is already the public face (`canaifeel.com`, not a `www` twin, not a workers.dev host). Everything else 301s there.

Pick one slash rule and keep it. These public sites already read as **trailing-slash directories** on content pages (`/can-ai-feel/`, `/team/notre-dame/`). Then:

- Apex + `https` only
- Trailing slash **or** no slash — never both as 200s
- One slug per entity; aliases 301 to the canonical
- Query strings are not a second page (`?utm=` does not get a sitemap row)
- Preview / paid / data endpoints stay out of the sitemap (`/_paid/`, `/data/` style disallows are fine; do not invent private paths here)

Canonical tags, redirects, sitemap locs, and internal links must agree. A sitemap that lists both `/foo` and `/foo/` is a flood of your own making.

## Hubs-first mint caps

| Batch | What ships | Cap (starting default) |
|-------|------------|------------------------|
| 0 | Apex + one hub that explains the taxonomy | 1 hub |
| 1 | Remaining hubs (maps, segments, leagues, course) | Small — count the real hubs, not “and also these 40 landing pages” |
| 2 | First leaf tier (highest-demand questions / teams / companies) | Tight cap (tens, not thousands). Example order of magnitude: **25–100** leaves |
| 3+ | Next leaf tier only if batch 2 is indexed and earning clicks | Same cap width until crawl + CTR say expand |

Caps are a brake, not a KPI to max out. If batch 2 is not in the sitemap index, do not mint batch 3.

Thin-page bar (fail = do not mint):

- Synonym or near-duplicate of an existing slug
- No hub parent (orphan URL)
- No unique content beyond a template and a name
- “Coming soon” as the whole page (list it on the hub; don’t mint the leaf yet)

## Sitemap + IndexNow

- Sitemap lists **canonical** URLs only, at the apex, with the chosen slash rule.
- One sitemap index if you outgrow a single file; do not shard by whim.
- `robots.txt` points at the sitemap. Allow crawlers you actually want (search + answer engines). Disallow non-pages.
- IndexNow (or the search console equivalent) fires **per batch**, after the URLs return 200 at the canonical location.
- Do not submit URLs that still 302, still 404, or still disagree on slash/host.

No flood: no submitting the entire archive every deploy, no minting thousands of stubs so the ping looks busy.

## Anti-patterns

- Minting every alias as its own page (“will AI replace programmers” and “is AI going to replace programmers” as two 200s without a 301 plan)
- Publishing leaf pages before the hub that should deep-link them
- Letting `www`, apex, and a pages.dev host all 200
- Treating a smash-loop preview URL as a public surface
- Measuring success by URL count

## Where the code lives

The factory, redirects, and sitemap builder are **Cloud Agent / IDE work**. Bots may propose taxonomy rows and cap numbers as a one-tap card. They do not smash-mint in chat.
