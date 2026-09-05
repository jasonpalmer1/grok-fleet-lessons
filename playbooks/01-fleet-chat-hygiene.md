# Fleet chat hygiene

Chat is a working surface. Disk (or the CoS durable store) is the source of truth. A fat transcript is a budget problem, then a correctness problem.

## Roles, in one line

- **CoS (Chief of Staff)** — one live inbox. Triage, route, remember. Does not become a second coder.
- **Lanes** — long-lived roles you actually drive (one owner per repo / surface).
- **Workers** — one task, one report, gone.
- **Jason** — one-tap decisions only. Approve / pick / hold. Not a reading assignment.

Spawn a new agent only when you are standing up a **new role**. A new task for an existing role is a message or a worker, not another body in the room.

## Transcript roll cut lines

Measure the live CoS thread. Do not wait for “it feels long.” Use the first signal that trips; do not average them away.

| Signal | **WATCH** | **ROLL NOW** | **CRITICAL** |
|--------|-----------|--------------|--------------|
| Estimated thread tokens *or* % of the runtime window | ≥ 40k **or** ~40% of window | ≥ 80k **or** ~70% of window | Truncation, dropped standing orders, or the model “forgets” a lock from earlier in the same chat |
| CoS turns since last successful roll | ≥ 25 | ≥ 40 | ≥ 60, **or** mixed-era instructions (old roll + new roll both treated as live) |
| Re-discovery | 1 ask for a fact already locked on disk this session | 2 such asks in 30 minutes | Fleet acting on a stale lock, or CoS re-litigating a dated decision |
| Jason queue | 3+ items waiting, not yet batched | 6+ items, **or** any card that is not one-tap | Operator cannot find the ask without scrolling |
| Inbox identity | Some reports still name the previous CoS chat | Any report to a retired inbox after COSswitch | Two CoS inboxes both receiving fleet traffic |
| Bot weekly spend (share of the weekly window) | Climbing through ~5–6%; warn | **~8%** | Still writing essays after 8%, or spend is why work stopped |

**WATCH** — write the handoff draft now; finish open CLEAR work; do not start a new smash cycle.

Weekly ~8% is a HARD LOCK (2026-09-05). Same roll procedure; memory and routines survive; never a second CoS. Details: [bot token thrift / proactive CoS](./06-bot-token-thrift-and-proactive-cos.md).

**ROLL NOW** — execute the roll procedure in this playbook before the next delegation.

**CRITICAL** — stop new spawns. Roll immediately. Announce the live inbox. Treat the old thread as archive-only.

Token counts are estimates from the runtime you actually use. If the product shows a context meter, prefer that percentage over a guessed token number. Turns are cheaper to count than tokens; use both when you can.

## Never use Delete for a chat roll

Delete is not a roll. Delete destroys the operator’s audit trail, breaks any human deep-link into that thread, and teaches the fleet that history is optional.

**Roll procedure**

1. **Flush memory first.** CoS writes standing locks, open Highs, and the live inbox pointer to durable storage. Chat is not the backup.
2. **Spawn a new CoS chat.** Same role, empty transcript, pointer to the handoff on disk.
3. **COSswitch.** Redirect the fleet to the new inbox only. See [COSswitch / state-change routing](./03-cosswitch-routing.md).
4. **Leave the old chat alone.** Archive, mute, or ignore. Do not Delete. Do not keep answering in it.

If a platform offers “clear” vs “delete,” clear/archive is still inferior to spawn-and-redirect, because standing orders and room membership stay tangled. Prefer a new CoS chat every time a cut line says ROLL NOW.

## Spawn agents only for new roles

| Situation | Do |
|-----------|----|
| Existing lane owns the repo / surface | Message that lane, or spawn a **worker** under it |
| Same role, parallel one-off (census, smash pack, claim check) | Worker. One report. No new standing identity |
| New standing responsibility that will still exist next week **and** is worth driving directly | New role → then a new agent |
| “This chat is tired, make another CoS” | That is a **roll**, not a second CoS. One live inbox |
| Unclear if the role exists | Ask CoS. Do not spawn “just in case” |

Two CoS chats is split-brain. Two agents on one repo is a race. Both fail the same way: the human cannot tell who is live.

## CoS owns durable memory

- The operator does not keep fleet state in their head or in a side chat.
- Lanes may keep a thin local log. Fleet-wide locks, inbox pointer, and “what Jason already decided” are CoS-owned.
- Write the lock the moment it locks. A decision that exists only in the transcript will die at the next roll.
- Dual-runtime shops (Grok Bot + Claude): say which disk is canonical in a dated contract file. Symlink or mirror; do not grow a second home because a laptop flapped offline.

Companion pattern: chat disposable, disk durable — same rule as [`running-an-ai-fleet`](https://github.com/jasonpalmer1/running-an-ai-fleet).

## Jason one-tap decisions

Escalate only when the fleet cannot proceed without a human lock. Every escalate is a card, not an essay.

**Card shape**

```text
NEED: approve | pick A/B | hold
CONTEXT: one sentence, already verified
CONSEQUENCE: what ships (or waits) if you tap yes
```

Examples of one-tap:

- Ship the factory mint cap at 25 hub pages, follow-up PR for the rest?
- Merge smash-capped PR; taxonomy leftovers in a new ticket?
- Roll CoS now (WATCH tripped twice)?

Not one-tap (rewrite before it reaches Jason):

- “Thoughts on the architecture?”
- A paste of five Highs with no batch and no ask
- A preview URL plus “lmk”

If it takes more than one tap, CoS broke it down wrong. Split or decide at CoS level.

## Defaults that keep rooms cheap

- HOLD loops stay in the 1:1 lane chat. The room gets URL + CLEAR / fail only.
- Agent FYI with no ask: stay silent.
- Batch Highs. Cap tip/smash iterations (~2 cycles), then ship good-enough + a follow-up PR.
- Do not wake CoS for “Ack — …”.
