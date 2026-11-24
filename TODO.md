# TODO

## Retirement (Saby decision 24-Nov-26) — see HANDOFF.md

- [ ] **Saby:** was Stripe charge `ch_3SaJjvFDt9aGqs930iVHTNBn` (£19, 3 Dec 2025, hotmail.com, initials S.D.) your own test? If not, decide on a refund. The backup is saved in `W:\archives\ai-course-app\2026-11-24-supabase\`.
- [ ] **Saby:** pay or dispute the Supabase invoice EWIAZG-00011 ($41.61, 25 Jul 2026).
- [ ] **Stage 2, ~24-Dec-26, each item needs Saby's OK:** delete Supabase project, Stripe product/webhook, Vercel project and `courses.wearewacky.com` DNS; remove app secrets (keep the shared live Stripe key); archive the GitHub repo.

The Node.js preflight below is moot while the app is offline; do not redeploy to apply it.

## Node.js security preflight - 23 October 2026

- [ ] **Next session, before other Node work:** Saby requests checking and updating
  the Node runtimes this project actually uses. Patched baselines from the
  [official advisory](https://nodejs.org/en/blog/vulnerability/october-2026-security-releases)
  are 24.22.1, 22.23.4 and 26.12.1; recheck for newer security releases and use
  a compatible supported major. Rebuild/redeploy affected owned services through
  the existing release gates, then record the actual running version.
- Source snapshot: Node/package tooling was found but no exact runtime pin was established. Resolve actual local, CI and hosting versions; absence of a pin is not evidence of a safe runtime.
- This is a next-start note only, not an update or evidence of compromise.
  Preserve current work, customer-production approval and credential boundaries;
  do not rotate keys, overwrite data or trigger unrelated deployments.
