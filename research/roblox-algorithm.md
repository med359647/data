# Roblox Discovery Algorithm: Research Notes (Oct 2026)

Shared notes for the **money** Cowork session. Source of truth is Roblox's own docs
([discovery.md](https://github.com/Roblox/creator-docs/blob/main/content/en-us/discovery.md),
[discovery-faq.md](https://github.com/Roblox/creator-docs/blob/main/content/en-us/discovery-faq.md)),
pulled 2026-10-22. Anything marked *(3rd-party)* is not from Roblox.

## How it works (Home → "Recommended for You", RFY)

1. **Retrieval:** from all eligible games, picks a per-user shortlist. It needs only a
   *very low* number of plays from **any** source (ads, friends, search, socials).
2. **Ranking:** orders roughly 100 games per user. It **only counts users who joined
   organically from RFY**. Ad, friend, search and social users never count here, even
   if they later come back via Home.
3. **Explore → expand:** a game is tested on a small cohort daily. If that cohort
   retains and spends, it expands to similar cohorts. There's no permanent penalty, and the
   window moves, so a fixed game gets re-tested.

All signals are **per-user averages**, not totals, so small games aren't disadvantaged.

## Ranking signals (official priority)

| Priority | Signal | Window |
|---|---|---|
| Most important | Play-through rate (PTR): clicks ÷ RFY impressions | first session |
| Most important | First-play bounce rate (**negative**) | <60 s, 61–180 s |
| Most important | Play days per user | D1, D2–7, D8–28 |
| Most important | Playtime per user (**capped 60 min/user/day**) | D1, D2–7, D8–28 |
| Important | Intentional co-play days (join/invite/private server) | D1, D2–7, D8–28 |
| Important | Qualified play sessions per user | D1, D2–7, D8–28 |
| Important | Spend days per user | D1, D2–7, D8–28 |
| Important | Robux spent per user | D1, D2–7, D8–28 |

The windows are scored both separately and combined. A new game doesn't wait 28 days:
PTR and bounce count right away, then D1, then D2–7, then D8–28.

## What hurts reach

- Titles or thumbnails that lead with giveaways ("Free Robux!") are deprioritized.
- Metadata that doesn't match gameplay is filtered from RFY and ranks lower in search.
- Clone titles, visuals or place files get no priority. The first game to add unique metadata wins.
- **No custom thumbnail means no RFY impressions at all.**
- Genre is **not** a ranking factor. Wrong tags still hurt, because they cause bounces.

## Ads: the money angle

- Ad users are **excluded** from RFY signals and treated as "already acquired". RFY impressions
  can dip after ads even though total players rise. Roblox says this is not a penalty.
- Ads still help **retrieval**, because any plays get the game considered for RFY.
- Roblox says: fix retention first. Once retention is strong, monetization **adds** reach.
  Games strong in both get the broadest distribution.
- Money signals are **spend days** (how often people pay) as well as **Robux per user**. Many small,
  repeatable purchases beat one big pass for the algorithm.

## Build checklist (what to do in Luau/Studio)

1. **First 60 s:** spawn straight into gameplay. Cut long loading screens and intro cutscenes,
   because bounce under 60 s is a top negative signal.
2. **Thumbnail and title match the gameplay** (raises PTR without raising bounce).
3. **Reasons to return tomorrow:** daily rewards, streaks, timed restocks. These drive play days
   in D2–7 and D8–28.
4. **Session target of about 60 min/day.** Time beyond that doesn't count, so favor more days over longer sessions.
5. **Friends:** invite prompts (`SocialService:PromptGameInvite`), party bonuses, private
   servers. These feed co-play days.
6. **Experience notifications** to bring lapsed players back (play days).
7. **Monetize for frequency:** cheap consumables or daily offers (spend days), on top of passes and subscriptions.

## Unverified / 3rd-party claims

- A June 2026 DevForum update extended retention scoring from 7 to 28 days *(3rd-party:
  [Dubit](https://dubit.io/library/what-makes-a-new-roblox-game-take-off)). This is consistent with the current docs.*
- Benchmarks such as "D1 retention > 20%" come from older guides *(3rd-party:
  [bloxg](https://bloxg.com/guides/roblox-algorithm))* and are not official.
- Roblox doesn't publish exact weights, and says weights will change.
