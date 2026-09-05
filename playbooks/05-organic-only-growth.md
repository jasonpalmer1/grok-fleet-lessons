# Organic-only growth

Growth here means **humans found a useful page and stayed**. It does not mean a spike you bought, blasted, or faked.

This matches the already-public posture on [jasonwpalmer.com](https://jasonwpalmer.com): products and earlier education work grown without paid acquisition theater.

## Allowed levers

| Lever | What it is | What it is not |
|-------|------------|----------------|
| **SEO** | Real pages for real queries; hubs; canonical discipline; sitemap + IndexNow | Keyword stuffing, doorway pages, minted stubs |
| **Internal deep-links** | Hubs → leaves → related leaves (see [URL factories](./04-url-surface-factories.md)) | Nav spam, 80-item footers, sitewide identical blocks |
| **CTR** | Titles and leads that match the query; honest snippets | Clickbait that bounces |
| **Crawl** | Fast 200s at the apex; stable URLs; crawlable HTML | Infinite calendars, faceted traps, preview hosts |

Ship the next factory batch only when the last batch is crawlable, indexed, and earning honest clicks.

## Forbidden growth tactics

Do not use these for growth goals — not “just to seed,” not “just this launch”:

- Social spam (mass follows, reply-spam, group drops, bot accounts)
- Bought traffic, click farms, paid view pods
- Share-post blasts (coordinated “everyone post this”) aimed at fooling a ranker or a vanity counter
- Fake engagement on your own properties
- Cloaking a thin factory page as something it isn’t

If a tactic’s main job is to look popular to a machine, it is out of bounds.

Distribution that is actually a product (a public MCP, a certificate, a playable page) is fine. Asking a friend who already cares is fine. A press email to someone who covers the topic is fine. A blast to strangers so the graph moves is not.

## Honest human-view tracking

Count **humans**, or do not use the number to make growth decisions.

Minimum bar for a first-party collector (pattern, not a named private host):

- Classify at write time: `human` vs `bot` vs `datacenter` vs your own QA/`rig` traffic
- Do not treat crawler 200s as product-market fit
- Do not celebrate a spike that is only sitemap fetch + answer-engine crawl
- Prefer session trails and referrers you can explain over a single vanity pageview
- No cross-site identity; no scraping form fields; DNT/GPC honored for content-bearing events

Public implementation sketch of that posture: [`visit-log-worker`](https://github.com/jasonpalmer1/visit-log-worker) (bot/datacenter/rig labels, no third-party vendor). Use the pattern; do not paste private database IDs or collector hosts into this repo.

**Growth review uses human rows only.** Crawl and bot traffic can live in a separate crawl-health view so you do not “optimize” for Googlebot pretending to be a fan.

## How a factory batch earns the next mint

A batch is allowed to expand when **all** of these are true:

1. Canonical URLs 200 at the apex with the slash rule.
2. Sitemap lists those URLs; IndexNow (or equivalent) was sent once for the batch.
3. Search console (or logs) show discovery — not just your own pings.
4. Human CTR / human sessions on the hub **or** on a sample of leaves beat “nobody came.”
5. Thin-page rejects stayed rejected (no synonym flood).

If humans are not on the hub, minting more leaves is not growth. It is a larger sitemap.

## Reporting to CoS

Growth updates are **state changes**, batched:

```text
CLEAR · canaifeel · batch 2: 40/40 canonical 200, sitemap updated, human sessions +N on hub
HIGH  · wafergraph · leaf CTR flat; hold batch 3? (one-tap: hold / mint 25)
```

No daily “we posted again” notes. No bot-inflated graphs.

## Anti-patterns

- “We’ll buy a little traffic so the charts aren’t empty.”
- Posting every new slug to every network the same hour (share-blast).
- Using total pageviews (bots included) as the north star.
- Opening a Cloud Agent to build a spam tool. That is not a product ship.
