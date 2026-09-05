# Public-safe publishing

If a lesson is real, sanitize it and put it on GitHub. Credentials never ride along.

This repo is public. Treat every sentence as if a stranger, a crawler, and a future intern will read it.

## Never publish

- Secrets, API keys, tokens, passcodes, `.env` contents, or “just this once” credentials
- Private Cloudflare / GitHub tokens, account IDs, or dashboard deep-links that are not already public
- HQ passcodes, personal emails, machine IDs, serials, or internal agent UUIDs
- Private preview URLs, password-gated HQ paths, or unpublished product endpoints
- Named private infra (internal hostnames, worker names, tunnel IDs, D1 database IDs)

If you need an example, invent a generic one (`hub/strategy.md`, `the live CoS inbox`, `the first-party collector`) instead of pasting the real path.

## Fine to publish

- Patterns and playbooks (hub / lane / worker, roll thresholds, factory mint caps)
- Public product names: Who’s Starting, CanAIFeel, Wafergraph, Iron Strike
- Public apex domains already on the open web (`canaifeel.com`, `wafergraph.com`, `whosstarting.com`)
- Public companion repos and their lessons
- Dated incidents with the secret bits stripped (symptom → change → why share)

## Pre-publish checklist

1. Search the draft for `sk-`, `ghp_`, `cfu_`, `Bearer`, `password`, `@gmail`, UUID-shaped IDs, and `.workers.dev` hosts that are not already in a public README.
2. Replace every private URL with a role (`the live CoS inbox`, `the production apex`).
3. Prefer “a first-party collector that labels bot vs human at write time” over naming the internal dashboard.
4. If a number is only meaningful because it identifies a machine or a person, drop the number.

When in doubt, delete the identifying noun and keep the rule.
