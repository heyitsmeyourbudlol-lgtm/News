# Production power scoreboard

_Top 10 indie · gravity Newdrop_ · Policy: [TOP10_PRODUCTION_POWER.md](TOP10_PRODUCTION_POWER.md)

Refresh: `python3 scripts/production_power_scoreboard.py --write`

## Current snapshot (2026-09-08 04:12 UTC)

| Metric | Value |
|--------|------:|
| Newdrop merges (7d) | 20 |
| Non-noop cycles/day | 6 today · proj 34.2/day · week_avg 6.0 (bar ≥8) [GAP] |
| Free-desktop agent cap | 8 |
| Theater Active share | 0% (0/3 open) |
| Brain / daemons | CLEAN peer-loop=active improve-loop=active ssh_rc=0 |

Merges: #91 Second Hobby publish drain via purge cron (#52) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/91); #89 Enable CodeQL SAST workflow (#84) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/89); #88 Shared AI soft budget for draft + support (#77) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/88); #87 Expand-contract migration PR gate (#86) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/87); #83 Fail-close confirm/unsubscribe on non-UUID tokens (#98) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/83)

## Week log

### Week of 2026-09-01 → 2026-09-07 (baseline → cadence land)

| Metric | Value | Notes |
|--------|------:|-------|
| Newdrop merges (7d) | **3** | PRs [#16](https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/16), [#17](https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/17), [#18](https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/18) |
| Non-noop cycles/day | recovering | CLEAN brain live; free-desktop cap 8 |
| Brain | CLEAN | mac-offloaded; meter credits CLEAN |
| Theater Active share | **0%** | Top10 Active = Newdrop-only open lines |
| Free-desktop agent cap | **8** | measured free concurrent (was phantom 96) |

**Verdict:** Merge bar hit (≥3). Cycles/day still the gap for a full green week. Streak clock: partial week; full green weeks start when cycles≥8 + merges≥3.

### Week of 2026-09-08 → 2026-09-14 (in progress)

| Metric | Value | Notes |
|--------|------:|-------|
| Newdrop merges (7d) | 12 rolling | Keep ≥3 |
| Non-noop cycles/day | climbing | T10-04: **4 today · proj 23.0/day · week_avg 4.0 · 04:09Z [GAP]** `meets_bar=false`; peer+improve active; clear-deferred no longer local_only-overwrites; bar ≥8 observed (proj alone cannot PASS)|
| Brain | CLEAN | peer+improve **active**; Mac LAs off |
| Cap | 8 | `max_parallel_agent_procs` |


## T10-04 evidence (2026-09-08)

Raise CLEAN non-noop cadence; keep free-desktop **cap=8**; NO PAY; Mac peer/improve LaunchAgents **not** enabled.

| Check | Result |
|-------|--------|
| BEFORE throughput | **5.0 cycles/h** · **4.0 non-noop/h** · rate 80% · window 5 |
| AFTER throughput | **4.0 cycles/h** · **4.0 non-noop/h** · rate **100%** · window 4 (post-wake; no SIGUSR1) |
| Day rollup (scoreboard) | **4 today** · **proj 23.0/day** · week_avg 4.0 · 04:09Z (bar ≥8) **[GAP]** — PASS when today≥8 observed; do not false-close on proj alone |
| peer-loop | **active** (USR1 trap proven — kill -s USR1 leaves active) |
| improve-loop | **active** (wake via `peer-turn.signal` — never `systemctl kill -s USR1`) |
| Anti-flap | sidecar `non_noop_by_day.json` · thin-save max-merge · dgx skip restart-if-active |
| `peer-turn.signal` | touched UTC wake |
| Cap | `max_parallel_agent_procs=8` · `free_desktop_agent_cap=8` |
| Mac | `mac-offloaded` present · peer/improve LaunchAgents absent |

**Note:** Countable day rollup excludes `local_only` verify ticks. SIGUSR1 / hard restarts used to wipe short `cycle_history` — durable `non_noop_by_day` + sidecar now survive flaps.
## How to count a “meaningful” merge

User-visible or verify-backed (`npm test` / `check:controls`) change on Newdrop. Hub needles do not count.
