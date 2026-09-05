# Lesson log

Dated, one lesson per entry. Facts for future operators — not chat transcripts.

## 2026-09-05 — HARD LOCK: thrift is HOW, scope stays FULL
**Symptom:** Quiet rooms were mistaken for a smaller portfolio; loud rooms were mistaken for “being thorough.”
**Change:** Bot = triage / route / real state-change only. One user ping per CLEAR, human blocker, or apex flip. Heavy work goes to Cloud Agents, Claude Code (forms), the job-board lane, or background executors. Lanes keep moving.
**Why share:** Token diet is chat discipline, not a license to drop work. Playbook: [`playbooks/06-bot-token-thrift-and-proactive-cos.md`](./playbooks/06-bot-token-thrift-and-proactive-cos.md).

## 2026-09-05 — Proactive CoS does not wait to be reminded
**Symptom:** PRs, tips, and queues sat idle until the operator asked “any update?”
**Change:** CoS decides when the lock is already on disk, routes immediately, resumes stalled PRs / tips / Cloud Agents, and unblocks queues. Waiting for a reminder is a named miss.
**Why share:** A hub that only answers is a receptionist. Playbook: [`playbooks/06-bot-token-thrift-and-proactive-cos.md`](./playbooks/06-bot-token-thrift-and-proactive-cos.md).

## 2026-09-05 — Roll at Bot weekly ~8% or fat transcript; no second CoS
**Symptom:** Weekly spend climbed while the same CoS chat kept writing; the tempting fix was another CoS body.
**Change:** WATCH around 5–6%; ROLL NOW at ~8% or the existing fat-transcript cut lines. Flush memory and routines first. Spawn-and-redirect. Never Delete. Never two live CoS inboxes.
**Why share:** 8% is a planned roll, not a crash. A duplicate CoS is split-brain. Playbook: [`playbooks/06-bot-token-thrift-and-proactive-cos.md`](./playbooks/06-bot-token-thrift-and-proactive-cos.md).

## 2026-09-05 — CoS rolls are spawn-and-redirect, never Delete
**Symptom:** A fat CoS transcript tempts “just delete it and start over,” which wipes the human audit trail and leaves the fleet posting into a hole.
**Change:** Measurable WATCH / ROLL NOW / CRITICAL cut lines; flush durable memory; spawn a new CoS chat; COSswitch the fleet; leave the old thread archived.
**Why share:** Delete looks like hygiene and behaves like amnesia. Playbook: [`playbooks/01-fleet-chat-hygiene.md`](./playbooks/01-fleet-chat-hygiene.md).

## 2026-09-05 — Spawn agents for new roles only
**Symptom:** Every new task grew a new body in the room; two “CoS” chats and two editors on one repo followed.
**Change:** New standing role → new agent. Existing role → message or worker. One live CoS inbox.
**Why share:** Headcount is not parallelism. Playbook: [`playbooks/01-fleet-chat-hygiene.md`](./playbooks/01-fleet-chat-hygiene.md).

## 2026-09-05 — Bots triage; Cloud Agents ship
**Symptom:** Bot smash loops patched previews in chat, spawned a tip per High, and still missed taxonomy debt.
**Change:** Bots classify / batch / route. Code and ships go through Cursor Cloud Agents or the IDE. One smash pack per tip, ~2 cycles max.
**Why share:** A room is a dispatcher, not a compiler. Playbook: [`playbooks/02-bot-triage-cloud-agents.md`](./playbooks/02-bot-triage-cloud-agents.md).

## 2026-09-05 — COSswitch: one live inbox, state-change only
**Symptom:** After a roll, lanes kept acking in the old chat and dripping Highs one-by-one.
**Change:** Publish the live inbox pointer; fleet reports CLEAR / HIGH / state-change only; batch Highs; silence FYIs.
**Why share:** Split-brain hubs plus ack spam is agents² cost. Playbook: [`playbooks/03-cosswitch-routing.md`](./playbooks/03-cosswitch-routing.md).

## 2026-09-05 — URL factories: taxonomy, hubs, cap, then ping
**Symptom:** Minting every alias as a 200, both slash variants live, sitemap listing previews — crawl budget spent on junk.
**Change:** Taxonomy → schema → hubs-first mint caps → sitemap + IndexNow. Apex + one trailing-slash rule. No flood.
**Why share:** CanAIFeel / Wafergraph / Who’s Starting style surfaces die by thin-page flood, not by too few ideas. Playbook: [`playbooks/04-url-surface-factories.md`](./playbooks/04-url-surface-factories.md).

## 2026-09-05 — Organic-only growth, human views only
**Symptom:** Share-blasts and bot-inflated pageviews get mistaken for demand; the next mint batch ships into empty rooms.
**Change:** SEO + internal deep-links + CTR + crawl. No social spam, bought traffic, or blast campaigns. Track humans vs bot/datacenter/rig at write time.
**Why share:** A sitemap ping is not product-market fit. Playbook: [`playbooks/05-organic-only-growth.md`](./playbooks/05-organic-only-growth.md).

## 2026-09-04 — Tip-smash infinite loops burn the budget
**Symptom:** Each search High spawned a new tip preview and a full room update cycle.
**Change:** Batch Highs; ~2 tip cycles max; then merge + follow-up PR for alias taxonomy.
**Why share:** Multi-agent QA without a cap turns “thorough” into “token incinerator.”

## 2026-09-04 — Offline laptop ≠ use the other machine as SoT
**Symptom:** Personal tip builds parked on a work-only Mini because Air flapped.
**Change:** Mini = cold backup only; Air (or GitHub/cloud) for personal repos.
**Why share:** Convenience under outage creates a second SoT you’ll pay for later.

## 2026-09-04 — Ack-only agent messages are pure waste
**Symptom:** Hub woke on every “Ack — …” with nothing to do.
**Change:** State-change reports only; hub stays silent on FYIs.
**Why share:** Fleet chat volume scales with agents² unless you gate it.

## 2026-09-04 — Drive mirror unblocks the other stack
**Symptom:** Grok memory lived only in Grok’s cloud; Claude couldn’t see it when Air was the Claude SoT.
**Change:** Tandem Google Drive mirror (archive), live write unchanged.
**Why share:** Dual-runtime shops need a readable bridge that isn’t “forward me the chat.”
