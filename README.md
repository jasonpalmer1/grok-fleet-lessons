# Running a Grok Bot fleet next to Claude

Lessons from operating **Grok Bot (Orangutan / Chief of Staff)** alongside an existing Claude Code fleet — written so others can reuse the patterns. Companion spirit to [`running-an-ai-fleet`](https://github.com/jasonpalmer1/running-an-ai-fleet), [`claude-operator-kit`](https://github.com/jasonpalmer1/claude-operator-kit), and [`tiered-agent-memory`](https://github.com/jasonpalmer1/tiered-agent-memory).

No product secrets. No credentials. Just ops.

## Why this exists

Claude already had the hard parts: disk-as-SoT, hub/lane/worker, tiered memory, token ledgers. Grok Bot adds a second runtime (cloud agents, multi-bot rooms, always-on routines). Day one without discipline burns tokens on ack-ping-pong and re-discovery. Day one *with* Claude’s habits — plus a few Grok-specific rules — ships faster and stays shareable.

## What transferred cleanly from Claude

1. **Chat is disposable; disk is durable.** Write decisions to hub/strategy (or equivalent) the moment they lock. Never treat a thread as memory.
2. **Hub / lane / worker.** One Chief of Staff dispatcher; long-lived specialist lanes; short-lived workers with one report.
3. **One owner per repo.** Two agents editing the same working tree is a race, not parallelism.
4. **Director stays thin.** Bulk reads, smash passes, and census work leave the hub. Escalate on verified failure, not vibes.
5. **Memory tiers.** Tiny always-on profile; project docs when in-project; archive retrieve-on-demand (including a Drive mirror Claude can read).

## What Grok Bot taught us (new)

### 1. Machine roles are part of SoT
Infer from evidence early: which machine holds personal projects vs work-only vs cold backup. Do **not** invent a second home for repos because a laptop flapped offline once. Cold backup ≠ day-to-day workspace.

### 2. Token thrift is a product feature
Multi-agent rooms amplify chatter. Default rules that paid off immediately:
- Agents report **state changes only** (preview URL ready, clear/fail, Jason blocker).
- No ack-only pings.
- Batch bugs into one smash report; **cap tip iterations** (e.g. ~2 cycles) then ship “good enough” + follow-up PR for edge-case taxonomy.
- Keep HOLD loops on **1:1 lane chat**, not the whole room.

### 3. Dual-runtime SoT needs an explicit bridge
If Claude disk remains canonical, say so in a dated contract file. Symlink bridges beat “migrate everything.” Grok’s own durable memory can live off-laptop; Claude hub dual-writes when the laptop is up. Optional: **Drive tandem mirror** so Claude (or a human) can read Grok memory without the Grok runtime.

### 4. Prove worth with proactive ops changes
The hub should propose process fixes (room noise, smash caps, T1 diet) — not only execute tickets. Autonomy is earned by catching what a single Claude session missed under parallel load.

### 5. Public writeups > private folklore
If a lesson is real, sanitize it and put it on GitHub. Future-you and strangers both benefit. Credentials never ride along.

## Suggested operating defaults for a Grok hub

| Situation | Do |
|-----------|----|
| Ambiguous machine | Prefer evidence (user dirs, project roots); ask only if still ambiguous |
| Agent FYI with no ask | Stay silent |
| Preview / QA loop | One smash pack per tip; then clear or follow-up PR |
| Group room HOLD | Lanes 1:1; room gets URL + cleared/merged only |
| Memory | T1 tiny; episode → log; archive → Drive/hub |
| Monetization claims | No “edge” sales without proof bar (product-specific) |

## What we are still measuring

- Delegation ratio under Grok (lightweight close-out note vs full Claude ledger).
- Whether smash caps reduce spend without shipping worse search UX.
- Drive mirror freshness vs Claude hub dual-write lag.

## Status

Living document. Started 2026-09-04 while crushing a season sports app + wiring analytics/HQ under a multi-bot Grok fleet.

## License

MIT — reuse freely; keep secrets out of forks.
