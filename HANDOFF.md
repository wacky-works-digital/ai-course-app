# AI Course App — Handoff

## Session

`AI Course App | S01 | 24-Nov-26 | Retirement stage 1 — taken offline`

## Context

Saby decided on 24 November 2026 that this app (live at
`courses.wearewacky.com`, Next ^16.0.10, unpatched since December 2025) should
go offline: there were no real course buyers. Stage 1 is reversible only;
nothing has been deleted.

## Stage 1 — what was done (24-Nov-26)

| Resource | Old state | New state | Verified | Undo |
|---|---|---|---|---|
| Vercel project `ai-course-app` (`prj_lZVNglX2cyc4lVst2EssUFVDF0hm`, team `wackyworksdigital`) | Live, serving `courses.wearewacky.com` (200) | **Paused** | `paused:true` via API; `courses.wearewacky.com` and `ai-course-app-tau.vercel.app` return 503 `DEPLOYMENT_PAUSED` | `vercel api "/v1/projects/prj_lZVNglX2cyc4lVst2EssUFVDF0hm/unpause?teamId=team_sNLQPIDCEgJyRqJyF1NzJwNf" --method POST --input <file containing {}>` or Vercel dashboard → project → Settings → resume |
| Stripe product `prod_TXO1KccvCGLn9u` "Introduction to AI" (live account `acct_1SVuhTFDt9aGqs93`, shared with Spellito, wearewacky.com and Custom Canvas Collective) | Active, 14 prices | **Archived** (`active=false`); prices untouched | API response `active=false` | Stripe dashboard → Products → Archived → Unarchive, or `POST /v1/products/prod_TXO1KccvCGLn9u active=true` |
| Stripe webhook `we_1SaJPSFDt9aGqs93wYHf6dwf` → `courses.wearewacky.com/api/webhook/stripe` | Already **disabled** before this session | Unchanged (disabled) | API `status=disabled` | Stripe dashboard → Developers → Webhooks → enable |
| Supabase project `ylunzqegctexvatirpmx` | Unknown: hostname already returns NXDOMAIN (Azure DNS and 8.8.8.8) | **Not changed — needs Saby** | No backup possible: no API reachable, no Supabase CLI/token, dashboard needs Saby's sign-in | n/a |

Not touched: the other three webhooks on the shared Stripe account, DNS,
GitHub repository, Google OAuth client, keys.

Finding: the price IDs in the Vercel env (`price_1SX…FaWAVKdu3u…`) do not
exist in the live Stripe account (`resource_missing`), so live checkout was
already broken; they belong to another Stripe account or test mode.

## Saby — Supabase steps (stage 1 still open)

1. Sign in at https://supabase.com/dashboard and open project
   `ylunzqegctexvatirpmx`.
2. If it shows **Paused**: the app is already offline there. To keep a backup,
   use the paused project's **Download backup** option (or Restore it, then
   Database → Backups → download, then Pause again). Save it to
   `W:\archives\ai-course-app\2026-11-24-supabase\` (outside git).
3. If it is **Active**: Database → Backups → download the latest backup (or
   Project Settings → Database → copy the URI and run `supabase db dump`), save
   as above, then Project Settings → General → **Pause project**.
4. If it no longer exists: record that here; nothing to back up.

## Stage 2 — after about 24 December 2026, each item needs Saby's explicit OK

- [ ] Delete the Supabase project (only after a backup exists or Saby confirms none is needed).
- [ ] Delete the Stripe product `prod_TXO1KccvCGLn9u` and webhook `we_1SaJPSFDt9aGqs93wYHf6dwf` (or leave archived).
- [ ] Revoke/rotate keys this app held: the live Stripe secret key is **shared with other WWD apps** — do not revoke it, instead remove it from this Vercel project's env; remove `STRIPE_WEBHOOK_SECRET`, `SUPABASE_SECRET_KEY`, `AUTH_SECRET`; delete the Google OAuth client used here.
- [ ] Delete the Vercel project `ai-course-app`.
- [ ] Remove the `courses.wearewacky.com` DNS record.
- [ ] Archive the GitHub repository `wacky-works-digital/ai-course-app`.

## Next steps

1. Saby: Supabase steps above.
2. Around 24-Dec-26: review stage 2 with Saby.
