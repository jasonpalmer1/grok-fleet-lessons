# Lesson log

Dated, one lesson per entry. Facts for future operators — not chat transcripts.

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
