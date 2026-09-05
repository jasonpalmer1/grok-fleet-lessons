# Bot triage / Cloud Agents default

Bots coordinate. Cloud Agents (and the IDE) ship.

A Grok Bot room is a good dispatcher and a bad compiler. Using bots to smash-loop code is how you burn the budget and still miss the edge case.

## Default routing

| Work | Who | Done looks like |
|------|-----|-----------------|
| Intake, classify, batch, watch roll cut lines | Bot / CoS | One card or one batched High. No code. |
| “Is this a new role or an existing lane?” | CoS | Route, don’t spawn. |
| Real code, tests, refactors, migrations | Cursor Cloud Agent or IDE | PR with a tip SHA. Not a chat paste. |
| Preview / visual QA | One smash pack per tip, then stop | CLEAR, or a follow-up PR — not another tip |
| Deploy / merge | Human one-tap or the lane that owns the repo | Live URL + state change. No ack. |
| Docs-only public writeups (this repo) | Cloud Agent or IDE | PR. Bots may draft the outline only. |
| Form-shaped / structured desktop work | Claude Code (or the desktop executor that owns that surface) | Checklist done. Not a bot smash. |
| Job-board cards | Job-board lane | Claim, finish, one CLEAR. CoS is not the board. |
| Long jobs / census / harvest | Background executor | Expectation set; missed SLA noticed. No room poll. |

If a bot is about to edit an app, stop. Open a Cloud Agent (or the IDE) against the repo that owns the working tree. **One owner per repo.**

HARD LOCK (2026-09-05): thrift is how, not what; CoS stays proactive. See [bot token thrift / proactive CoS](./06-bot-token-thrift-and-proactive-cos.md).

## Why bots don’t smash-ship

- Multi-bot rooms amplify chatter. Each “quick fix” is another preview, another room update, another CoS wake.
- Bots lack a durable working tree you can tip, revert, and review. Cloud Agents do: branch, commit, PR, SHA.
- Smash loops hide taxonomy debt. The existing lesson still holds: batch Highs, ~2 tip cycles, then merge + follow-up PR for aliases.

```text
WRONG:  High → bot patch → new preview → High → bot patch → …
RIGHT:  Highs batched → Cloud Agent PR → one smash pack on that tip → CLEAR or follow-up PR
```

## CoS / bot jobs (stay here)

- Read the paste. Split into items. Discard FYIs.
- Tag each item: CLEAR (state change, no Jason), HIGH (needs a ship), BLOCKED (one-tap card).
- Pick the owning lane. Refuse a second owner on the same repo.
- Watch [fleet chat hygiene](./01-fleet-chat-hygiene.md) cut lines and call the roll.
- After a roll, run [COSswitch](./03-cosswitch-routing.md).

## Cloud Agent / IDE jobs (go there)

- Any file that will be committed
- Tests, lint, browser verification for UI
- Factory mint implementations, sitemap / IndexNow hooks, canonical redirects
- “Good enough” merge plus a follow-up ticket for the long tail

Bots may **describe** the change and attach the PR URL. They do not become a second editor on the branch.

## Smash cap (unchanged, restated)

1. Collect Highs into one pack. No per-bug previews.
2. One Cloud Agent tip implements the pack.
3. One smash pass on that tip (lane 1:1, not the whole room).
4. CLEAR or open a follow-up PR. Do not start cycle 3 “just to be thorough.”

Thorough without a cap is a token incinerator.

## Anti-patterns

- “The bot can just tweak the CSS in chat.”
- Two bots, one working tree.
- A third Cloud Agent “to go faster” on a repo that already has an owner.
- Using Delete on the CoS chat because the smash loop made it unreadable. Roll instead.
