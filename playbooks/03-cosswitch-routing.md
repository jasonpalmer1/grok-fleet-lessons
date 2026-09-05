# COSswitch / state-change-only routing

COSswitch is the cutover after a CoS chat roll: there is exactly one live inbox, and the fleet reports only there.

The room is not a heartbeat monitor. If nothing changed, say nothing.

## After a roll

1. CoS publishes the **live inbox pointer** on disk (durable memory). That pointer is the only address that matters.
2. CoS tells every lane and worker: report here; the previous chat is archive.
3. Lanes acknowledge **once**, in the new inbox, with a state line — not “Ack.” Example: `LANE search · live · next: smash pack on tip abc1234`.
4. Anyone still posting in the old chat is redirected once, then ignored. Do not run two hubs.

Split-brain (two CoS inboxes receiving work) is CRITICAL under [fleet chat hygiene](./01-fleet-chat-hygiene.md). Stop spawns until one pointer wins.

## What may be sent to the live CoS inbox

| Severity | Meaning | Example |
|----------|---------|---------|
| **CLEAR** | Verified state change. No decision needed. | Preview URL live. PR opened. Mint batch 2/4 indexed. Smash pack CLEAR. |
| **HIGH** | Something needs a ship or a Jason tap. | Auth regression on the apex. Factory about to exceed the hub mint cap. |
| **State change** | The world is different than last report. | Lane idle → blocked. Blocked → unblocked. Owner moved. Cut line tripped WATCH → ROLL NOW. |

If the message is not CLEAR, HIGH, or a state change, do not send it.

## What must not be sent

- “Ack — on it”
- “Still working”
- “Got it” / “will do” / emoji-only
- A second copy of a High already in this inbox
- Progress that does not change state (“read three files”)
- Reports to a retired CoS chat after switch

Ack-only traffic is pure waste. Fleet volume scales with agents² unless you gate it.

## Batch Highs

Highs are a pack, not a drip.

- Hold Highs for a short window (same smash cycle, same tip, same surface) and send **one** pack.
- One pack → one Cloud Agent tip when code is required ([bot triage](./02-bot-triage-cloud-agents.md)).
- Do not spawn a preview per High.
- After ~2 tip cycles, ship good-enough and file the long tail. Do not keep the room open for alias taxonomy.

**Pack shape**

```text
HIGH PACK · <surface> · <tip or 'needs agent'>
- 1. …
- 2. …
ASK: smash / follow-up PR / Jason one-tap
```

## CLEAR is a fact, not a vibe

CLEAR means a human or a fresh check verified the new state (URL loads, test ran, sitemap lists the new slugs). “I intended to deploy” is not CLEAR.

Companion: verify the artifact landed — same rite as [`running-an-ai-fleet`](https://github.com/jasonpalmer1/running-an-ai-fleet).

## Room vs 1:1

| Channel | Allowed |
|---------|---------|
| Fleet / CoS room | CLEAR, batched HIGH, state changes, COSswitch announcements |
| Lane 1:1 | HOLD loops, smash notes, draft cards |
| Retired CoS chat | Nothing. Archive. |

## Defaults

- Agent FYI with no ask: stay silent.
- After COSswitch, the first lane message is a state line, not an ack.
- If you are unsure whether something is a state change, it isn’t. Wait until it is.
