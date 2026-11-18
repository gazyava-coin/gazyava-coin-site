# Monthly Season Pass

The game has a monthly season pass, based on server-recorded daily taps.

## Schedule and progress
- Season boundaries use UTC calendar months.
- Progress is the sum of `daily_progress.taps` rows for the current UTC month.
- Client-side taps, score balance, boosters and local storage do not directly grant pass progress.

## Reward track
| Milestone | Monthly taps | Reward |
|---|---:|---:|
| Первый росток | 100 | 25 points |
| Облачный странник | 300 | 75 points |
| Мятный герой | 700 | 175 points |
| Повелитель бури | 1,500 | 400 points |
| Корона сезона | 3,000 | 1,000 points |

Each reward is claimable once per player and UTC season. The unique key `(telegram_id, season_start, tier_id)` prevents duplicate claims. Claiming and balance credit happen in one database transaction.

## Backend and security
- `player_season_pass_claims` has RLS enabled and no public/anon/authenticated grants.
- `get_player_season_pass(bigint)` and `claim_player_season_pass_reward(bigint,text)` are executable only by `service_role`.
- Edge Function `game` exposes `season_pass_status` and `claim_season_pass_reward` after validating Telegram initData. JWT verification remains enabled.
- The frontend displays progress and claim state from the server; it does not calculate or award rewards locally.

## Verification
- SQL transaction test: a test player with 350 current-month taps saw the track state and successfully claimed the 100-tap reward; score increased by 25. Test transaction rolled back.
- RLS and role grants checked: RLS enabled, `anon` execute denied, `service_role` execute allowed.
- Frontend inline JavaScript syntax check passed.
- Telegram live UI test has not been performed.
