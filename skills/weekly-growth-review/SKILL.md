---
name: weekly-growth-review
description: Use when the user asks how their site is doing, what to do next for more visits or sales, or wants a weekly growth/SEO review using QueryAction (GA4, Search Console, PageSpeed, research, Work).
---
# Weekly growth review with QueryAction

Only report numbers that QueryAction tools return. Never invent data. Never ask the user for a token or password: sign-in happens in the browser via OAuth.

1. **Orient.** Call `get_started`, then `list_sites`. Pick the site the user means; if none exists, offer `add_site`.
2. **Context.** Call `get_site_context`. If the goal or conversion is missing, ask one short question and save it with `update_site_context`.
3. **Connections.** If Search Console or GA4 is not connected, offer `begin_gsc_connection` / `begin_ga4_connection` (each returns a browser link), then check `get_gsc_connection_status` / `get_ga4_connection_status`.
4. **This week's data.** Call `get_weekly_report`, plus `get_tracking_snapshot` (Search Console) and `get_ga4_tracking_snapshot` (GA4). Use `get_tracking_breakdown` for the pages or queries that moved.
5. **Choose a method.** Read a playbook with `get_playbook` (no name lists them; e.g. `decide-next-move`, `new-site`, `early-traction`, `consolidated`) before recommending anything.
6. **Research only what the question needs.** First reuse recent results from `list_research` / `list_opportunities`. New research (`request_pagespeed_audit`, `request_keyword_opportunities`, `request_competitor_comparison`, `request_backlink_opportunities`, `request_ai_visibility`, ...) runs in the background: poll `get_research` or `get_opportunity` with `waitSeconds: 25` until final. Do not resend the same request. Say which calls you ran.
7. **One move.** Recommend one concrete move with how to measure it. If the user agrees, track it with `propose_work`; review progress with `list_work` / `get_work_evaluation`.

Output: a short summary (what changed, why it matters, the one move, how we'll measure it) in the user's language.
