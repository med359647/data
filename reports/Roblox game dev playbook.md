# Win Roblox Discovery by Engineering Return Visits

As of October 2026, Roblox's Home "Recommended for You" (RFY) algorithm works in two stages. In the first, **any handful of plays from any source** makes a game a candidate. In the second, Roblox ranks candidates using **only players who found the game organically through RFY**, scoring them on eight per-player averages. The four that count most are play-through rate, first-play bounce, play days and playtime (playtime is capped at 60 minutes per player per day). Since June 2026 these are measured across Day 1, Days 2–7 and Days 8–28 ([Roblox Docs: Discovery](https://create.roblox.com/docs/discovery)). In practice the algorithm rewards three things: a game that delivers fun in the first minute, that players come back to on many different days for four weeks, and where they buy small things often. One big launch spike counts for little. For a small team with limited Luau skills, the most dependable route is a factory rather than a single bet. Build cheap remixes of proven loops in 3–10 days on one reusable code template. Clear the new 2026 age-gated publishing tiers. Buy a few thousand cheap test plays. Then kill or scale each game against fixed metric gates: roughly D1 ≥ 10% and an average session of 8–10 minutes or more, measured against Roblox's own similar-game benchmark. The 2025 mega-hits (Grow a Garden, Steal a Brainrot, 99 Nights in the Forest) came from teams of about three people who built in days to months. Each then grew through weekly updates, scheduled live events and, often, an operator with capital. Several 2025–2026 platform changes matter to any plan. Age-tiered publishing now requires 250 highly engaged plays before a game reaches under-16s. The DevEx rate is $0.0038 per Robux, or $0.0054 for spending by verified U.S. adults. Creator Rewards replaced Premium Payouts. Roblox Plus replaced Premium. Knit is archived, and Roblox has shipped Unified Lighting, the new Audio API and Server Authority. Together they reward teams that take care of compliance, mobile performance and clean architecture from the first day.

**How to read the labels.** Throughout, **(official)** means Roblox's own documentation, newsroom or financial filings. **(third-party)** means an agency, tracker, analyst or community estimate. **(inference)** means a recommendation drawn from the evidence, which nobody has stated as fact. Most official doc text was read from Roblox's public creator-docs repository, current to October 21, 2026. Some DevForum and investor-relations items were available only as search summaries and are flagged where it matters.

## RFY ranks only organic players, on eight per-player signals

### Retrieval lets you in; ranking decides how far you go

Think of RFY as a two-step funnel. **Retrieval** narrows every eligible game to a shortlist for each user. Plays from ads, curation, search, charts, friends, teleports, notifications or social media "can accelerate your consideration", and "even a small number of people playing" is enough to signal that the game is worth testing (official, [Discovery](https://create.roblox.com/docs/discovery)). **Ranking** then orders **roughly 100 games** for each user's Home page (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)). This is the stage that decides how many impressions you get, and it is strict. "Roblox doesn't count the engagement, monetization, or retention of users first acquired from ads, curation, friends, search, social media, or any other source in the ranking stage" (official, [Discovery](https://create.roblox.com/docs/discovery)). Ads, YouTubers and Discord can open the door, but only the behaviour of strangers who clicked your tile on Home decides whether Roblox shows the game to more strangers.

Roblox describes the growth mechanic as **explore and expand**. It tests the game on a small cohort every day. If that cohort retains and spends well, Roblox recommends the game to more cohorts like it. A content update often produces a spike of new RFY players, and the expansion continues only if those players behave well (official, [Discovery](https://create.roblox.com/docs/discovery)). There is **no permanent penalty** for a weak start, because the signals use a moving window and the game is re-tested daily (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)). That gives a small team its biggest strategic freedom: a failed launch is not a death sentence, and an update can bring a game back. Every signal is a **per-user average rather than a total**, so small games are not disadvantaged against big ones (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)).

### The official signal table, and what each one asks you to build

| Priority (official) | Signal | Window | What it asks of your game (inference) |
|---|---|---|---|
| Most important | Play-through rate (clicks ÷ RFY impressions) | First session | A thumbnail and title that are honest and appealing |
| Most important | First-play bounce rate (negative) | <60 s and 61–180 s | Gameplay within seconds, no long loading or intro |
| Most important | Play days per user | D1, D2–7, D8–28 | Reasons to come back tomorrow and next week |
| Most important | Playtime per user (capped at **60 min/user/game/day**) | D1, D2–7, D8–28 | Sessions that fill up to an hour, not five |
| Important | Intentional co-play days (join, invite, private server) | D1, D2–7, D8–28 | Invites, party bonuses, private servers |
| Important | Qualified play sessions per user | D1, D2–7, D8–28 | Many real sessions, not accidental clicks |
| Important | Spend days per user | D1, D2–7, D8–28 | Cheap, repeatable purchases |
| Important | Robux spent per user | D1, D2–7, D8–28 | A shelf of items that still sell later in the player's life |

Signal list and windows: (official, [Discovery](https://create.roblox.com/docs/discovery)).

Roblox weighs the windows "both separately and combined together to decide impression volume". A new game does not have to wait 28 days. PTR and bounce count from the first session, then D1, then D2–7, then D8–28 (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)). PTR and bounce cover only the first session of RFY-acquired players. When those same players later return through Continue, their D2–7 and D8–28 behaviour **still counts** (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)). Two consequences follow. Playtime above 60 minutes a day earns nothing, so it is better to design for more days than for longer marathons. And because bounce is scored at the 60-second and 180-second marks, the first three minutes are the most valuable design real estate in the whole game (inference).

On retention versus revenue, Roblox gives a clear order of priority: "If retention is low, focus on core gameplay first. Once retention is strong, improving monetization can help you increase your Home impressions". Games strong in both "might receive broader distribution" (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)). Genre is not a ranking factor, and finite or story games "are not penalized" for low D8–28. Wrong genre tags still hurt indirectly, because they cause bounces (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)).

### How the algorithm got here (2025–2026)

The signal set has changed several times, so advice from 2024 or early 2025 is unreliable. In March/April 2025 Roblox introduced per-user averaged signals, the co-play signal and a Home Recommendations analytics tab ([DevForum 3587441](https://devforum.roblox.com/t/boost-your-discovery-with-the-improved-recommended-for-you-algorithm-and-analytics-for-creators/3587441), official, search summary). On March 26, 2026, "How we are improving Home this year" made three changes ([DevForum 4502571](https://devforum.roblox.com/t/how-we-are-improving-home-this-year/4502571), official, search summary):

- "Today's Picks" became **Standout Games**, a hand-curated sort with a creator nomination form.
- A "deep play-through rate" signal was announced.
- Roblox said RFY weighting would become "dynamic and personalized… there will not be a single global formula".

The biggest change came in **June 2026** (newsroom dated June 15). Signals moved "from a 7-day window to a 28-day window, measured across Day 1, Day 2–7, and Day 8–28". Qualified PTR was replaced by plain PTR plus first-play bounce, and signal contributions were added to Creator Analytics ([Roblox Newsroom](https://about.roblox.com/newsroom/2026/06/optimizing-discovery-great-games-reach-millions-players-roblox); [DevForum 4684575](https://devforum.roblox.com/t/recommended-for-you-algorithm-improvements-that-better-value-long-term-retention/4684575), official, search summary). On **October 12, 2026**, Roblox changed how impressions, clicks and plays are recorded. It says this does not change recommendations, but **PTR may look slightly lower**, so do not compare PTR from before October 12 with PTR after it ([DevForum 4930122](https://devforum.roblox.com/t/improved-discovery-measurement-in-creator-analytics/4930122), official, search summary). A secondary summary of RDC 2026 (September) reports that ranking is now age-aware: younger players see shorter, fast-turnover games, older players see games with retention depth, and a video-first "Moments" tab is live in the U.S. ([Panstag](https://www.panstag.com/2026/09/rdc-solo-creator-guide.html), third-party, not confirmed officially). The "deep play-through rate" announced in March does not appear in the October 2026 docs. It was probably folded into the June redesign, but that is unconfirmed (inference).

These changes had real business effects. Roblox's Q2 2026 shareholder letter said the near-term impact of the algorithm changes on younger cohorts was "larger than we anticipated", and that bookings growth slowed to about 8% as monetization per hour fell among younger U.S. and Canadian players ([Roblox Q2 2026 letter](https://www.sec.gov/Archives/edgar/data/0001315098/000162828026051059/ex991-robloxq22026earnin.htm), official). The algorithm moved away from rewarding quick-churn spikes toward rewarding four-week habits, and Roblox accepted a revenue cost to do it. Expect it to stay that way (inference).

### What quietly kills reach

Some cuts to reach are mechanical. A game with only the default thumbnail is **not eligible for Home recommendation impressions at all** (official, [Discovery](https://create.roblox.com/docs/discovery)). Metadata that "implies any type of monetary reward" (e.g. "Robux! Play now!") is deprioritized. So is metadata that doesn't match the gameplay, and so are "non-unique" games whose metadata or place files closely resemble existing ones. On clones, Roblox highlights "the game that first added the unique metadata and/or placefile", not the one created first (official, [Discovery](https://create.roblox.com/docs/discovery); [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)). Repeated or irrelevant keywords in descriptions "may result in demotion" (official, [Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places)). Skipping the maturity questionnaire leads Roblox to "automatically restrict the playability of the game… for all players" (official, [Content maturity](https://create.roblox.com/docs/production/promotion/content-maturity)). The rule for a remix factory follows: **remix the loop, never the assets or metadata.** Each game needs its own place file, art and description (inference).

### Ads buy entry to the candidate pool, not ranking

Ads Manager now runs on Home and Search together, with three objectives (official, [Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)):

- **Plays** is for "initial traffic to help recommendation systems learn what's working and qualify your game for Recommended For You".
- **Earnings** reports return on ad spend.
- **Engagement** buys age-checked, highly engaged players who count toward the Kids/Select threshold.

Users acquired through ads are credited to the ad for 30 days (7 days for players resurrected after a lapse) (official, same). They are excluded from RFY ranking and "will generally not subsequently see your game in RFY". RFY impressions can therefore **dip while total players rise**, and Roblox says this is "not an ad penalty" (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)).

Cost estimates disagree sharply. Roblox's November 2025 benchmarks put average cost per play at **$0.0073–$0.0187** ([DevForum 4084863](https://devforum.roblox.com/t/ads-manager-updates-home-search-combined-new-benchmarks-and-sunsetting-the-classic-flow/4084863), official, search summary). An agency sample of 850+ promoted games claims about **$0.45 per play** ([BLOXG](https://bloxg.com/statistics/roblox-advertising-benchmarks), third-party, commercially motivated). One developer reports D1 of about 3% with ads on versus 5–8% with ads off, and argues that ad traffic drags down discovery metrics. That is a single unconfirmed bug report ([DevForum](https://devforum.roblox.com/t/sponsored-ads-traffic-degrades-the-engagement-metrics-used-for-discovery-causing-paid-acquisition-to-harm-organic-ranking/4838351), third-party). The practical rule: use small Plays campaigns to clear retrieval and test thumbnails. Judge quality only in the **Home Recommendations tab**, which shows each signal by window against similar-game benchmarks (official, [Discovery](https://create.roblox.com/docs/discovery)). Never judge it from ad-cohort retention (inference).

### Other surfaces worth the effort

Home is "usually where the vast majority of users find games" (official, [Acquisition analytics](https://create.roblox.com/docs/production/analytics/acquisition)). Around RFY, a few cheap levers are well documented:

- **Thumbnail personalization.** Activate **2–5 Home thumbnails**. In testing this raised average qualified PTR by **+8.5%**, and by up to +50% for some games. Refresh the set with each major update, then leave it alone (official, [Thumbnails](https://create.roblox.com/docs/production/publishing/thumbnails)). Thumbnails are 16:9 (ideally 1920×1080). Icons are at least 512×512 but display near 150×150, so check them small (official, [Experience icons](https://create.roblox.com/docs/production/publishing/experience-icons)).
- **Experience Events and update announcements.** Announcements are limited to 60 characters and **once every three days** (official, [Experience events](https://create.roblox.com/docs/production/promotion/experience-events)).
- **Experience notifications.** Opt-in prompts are available to users 13+, and a user can't be re-prompted for **30 days** (official, [Experience notifications](https://create.roblox.com/docs/production/promotion/experience-notifications)).
- **Semantic search.** The first sentence of the description should summarize the game in natural language (official, [Discovery](https://create.roblox.com/docs/discovery)).
- **Standout Games nominations**, for genuinely novel games only (official, [DevForum 4502571](https://devforum.roblox.com/t/how-we-are-improving-home-this-year/4502571), search summary).

Instrument the first three minutes with funnel events, track currency sources and sinks with economy events, and use the built-in **Experiments** tool. Experiments run for 14–60 days with up to two variants plus a control, and playtime, payer conversion and ARPU update every 5 minutes for the first 24 hours as an early-harm check (official, [Experiments](https://create.roblox.com/docs/production/experiments); [Funnel events](https://create.roblox.com/docs/production/analytics/funnel-events)). With low player counts, only big changes will show a detectable effect, so small games should test big swings such as onboarding flow or first-reward timing (inference).

## Ten platform changes from 2025–2026 that rewrite older advice

The table below collects the changes that make pre-2025 tutorials wrong or incomplete. Every row is official unless marked otherwise.

| Change | Date | What it means for you | Source |
|---|---|---|---|
| **Publishing eligibility**: ID-verified *or* a real-money purchase since Jan 1, 2025, plus a maturity label | Dec 2025 | Every publishing account must qualify | [DevForum 4143953](https://devforum.roblox.com/t/new-requirements-to-publish-and-update-public-experiences/4143953) |
| **Age-tiered audiences**: Roblox Kids (5–8), Roblox Select (9–15), Roblox (age-checked 16+) | From June 2026 | New games launch to age-checked 16+ only, then must earn under-16 reach | [Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select); [Newsroom, Apr 2026](https://about.roblox.com/newsroom/2026/04/introducing-roblox-kids-and-select-accounts) |
| **Under-16 evaluation**: **250 unique plays by highly engaged age-checked users within 60 days**, plus a safety review; or a **50,000 Robux** refundable expedited fee | 2026 | The real launch milestone; plan ads and creators around it | [Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select) |
| **Creator requirements for Kids/Select**: ID or face verification, 2FA, questionnaire rating Minimal/Mild/Moderate, and a **1,000 Robux refundable fee or 2+ months of Plus/Premium** (refunded if the game keeps 25 highly engaged players for 60 days) | 2026 | Budget the fee; keep content at Moderate or below | [Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places) |
| **28-day RFY window**; PTR plus bounce replace qualified PTR | June 2026 | Retention through week 4 is now ranked | [Newsroom](https://about.roblox.com/newsroom/2026/06/optimizing-discovery-great-games-reach-millions-players-roblox) |
| **DevEx** standard rate **$0.0038/Robux** (from Sept 5, 2025); **U.S. 18+ rate $0.0054** (+42%) from June 8, 2026 for qualifying games | 2025–26 | R15-only character choice can raise cash-out by 42% on adult U.S. spend | [DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange); [18+ rate](https://create.roblox.com/docs/production/monetization/18-plus-devex-rate) |
| **Creator Rewards** replaced Premium Payouts | July 24, 2025 | Paid for daily-habit play by Active Spenders and for bringing in new spenders | [Creator Rewards](https://create.roblox.com/docs/creator-rewards) |
| **Roblox Plus** replaced Premium for new subscribers; cross-game developer product sales disabled | Apr 30 / May 30, 2026 | Read prices dynamically; new referral and transfer income | [Roblox Plus](https://create.roblox.com/docs/production/monetization/roblox-plus); [Developer products](https://create.roblox.com/docs/production/monetization/developer-products) |
| **Reward-driven media feeds** (feed + autoplay/infinite scroll + rewards for watching) removed from Kids/Select | Aug 25, 2026 | Do not build "watch reels for coins" mechanics | [DevForum 4829188](https://devforum.roblox.com/t/roblox-kids-and-select-new-restrictions-on-reward-driven-media-feeds/4829188) |
| **Unified Lighting** (LightingStyle + PrioritizeLightingQuality replace Technology) | July 23, 2025 | Old "Future vs ShadowMap" tutorials are outdated | [Technology enum](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/reference/engine/enums/Technology.yaml) |
| **Audio API** (AudioPlayer/Emitter/Listener/Wire) is the recommended system; Sound/SoundGroup discouraged | 2025–26 | Build buses with AudioFader | [Audio objects](https://create.roblox.com/docs/audio/objects) |
| **Server Authority** generally available (opt-in, `AuthorityMode = Server`) | July 2026 | Free character anti-cheat for games that fit it | [Newsroom, Jul 2026](https://about.roblox.com/newsroom/2026/07/creating-responsive-cheat-resistant-games-roblox-server-authority) |
| **Knit archived** (July 31, 2024); **ProfileService unsupported** in favour of ProfileStore | 2024 (still ignored by many tutorials) | Use plain modules + ProfileStore | [Knit](https://github.com/Sleitnick/Knit); [ProfileStore](https://github.com/MadStudioRoblox/ProfileStore) |
| **Official Studio MCP server**, with Feb 2026 playtest tools | 2025–26 | AI agents can read the DataModel, run Luau and playtest | [Studio MCP](https://create.roblox.com/docs/studio/mcp); [MoguraVR](https://www.moguravr.com/roblox-studio-mcp-server-agentic-update/) (third-party) |

Some sources disagree, and the official docs win. Several guides say Kids/Select needs **500** engaged players. The current docs say **250**, and the Creator Updates page notes the requirement was halved ([Creator Updates](https://create.roblox.com/updates), official). Some guides list Premium or Plus as a DevEx requirement. The DevEx page does not ([DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange), official). The age gate also changes who your first players are. Early RFY cohorts are age-checked 16+ players, so they skew older than the eventual core audience of a kid-friendly game. Read early metrics with that bias in mind (inference).

Age checks also shape co-play. Since January 2026, chat worldwide requires a facial age estimate or ID, and players can chat only with the same or adjacent age bands ([Roblox IR](https://ir.roblox.com/news/news-details/2026/Roblox-Requires-Users-Worldwide-to-Age-Check-to-Access-Chat/default.aspx), official). By Q2 2026, **57% of global DAU** were age-checked (over 70% in the U.S.) ([Q2 2026 letter](https://s27.q4cdn.com/984876518/files/doc_financials/2026/q2/Roblox-Q2-2026-Earnings-Shareholder-Letter.pdf), official). Games for younger players will probably see weaker co-play signals, so they should lean on non-chat social features such as party bonuses, emotes and shared goals (inference). Team Create collaboration is likewise limited to age-checked users of similar ages and trusted friends ([Roblox IR](https://ir.roblox.com/news/news-details/2026/Roblox-Requires-Users-Worldwide-to-Age-Check-to-Access-Chat/default.aspx), official), so every team member should complete an age check early.

## Monetize for spend days: many cheap purchases beat one big pass

### The toolkit and what each tool pays

The creator keeps **70% of Robux spent** on passes and developer products. The other 30% is Roblox's marketplace fee (official, [Monetization overview](https://create.roblox.com/docs/get-started/monetization)). The main tools:

- **Passes** are one-time purchases.
- **Developer products** can be bought repeatedly (currency, boosts, skips).
- **Subscriptions** cost at least 49 Robux and pay 70% every month. Local-currency subscriptions come in fixed tiers of $2.99–$14.99 and pay **70% in month 1, then 100% from month 2**. Battle passes may be sold as subscriptions (official, [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)).
- **Paid private servers.** Changing their price **cancels every active subscription** (official, [Private servers](https://create.roblox.com/docs/production/monetization/private-servers)).
- **Rewarded video ads.** Players choose to watch a 6–30-second ad. The reward must be a developer product worth 3–10 Robux. The game needs 2,000+ unique monthly visitors, and the creator must be 13+ and ID-verified (official, [Rewarded video ads](https://create.roblox.com/docs/production/promotion/rewarded-video-ads)).
- **Immersive ads**, with the same visitor threshold (official, [Immersive ads](https://create.roblox.com/docs/production/monetization/immersive-ads)).
- **UGC items sold in your game**, where the game owner earns a **40% affiliate share** (official, [Marketplace fees](https://create.roblox.com/docs/marketplace/marketplace-fees-and-commissions)).

**Creator Rewards** pays two ways (official, [Creator Rewards](https://create.roblox.com/docs/creator-rewards)):

- **Daily engagement:** 5 Robux per Active Spender per day. An Active Spender has spent at least $9.99 in the past 60 days. To count, they must play 10+ minutes, and your game must be one of the first three they launch that day.
- **Audience expansion:** 35% of the first $100 that a new or returning user spends anywhere on Roblox in their first 60 days. They must arrive through your share link, a direct link or a search for the game's name, and the game must average 100+ DAU over the following 60 days.

Both pay out after a 60-day hold. Both reward the same daily-habit design that RFY ranks (inference).

**Roblox Plus** started April 30, 2026 at a reported $4.99/month with no Robux stipend ([PlayToEarn](https://playtoearn.com/news/roblox-plus-launches-april-30-at-499-monthly-replacing-premium-with-discount-first-model), third-party). It adds three creator income streams and one trap (official, [Roblox Plus](https://create.roblox.com/docs/production/monetization/roblox-plus); [Robux transfers](https://create.roblox.com/docs/production/monetization/robux-transfers)):

- **Referrals:** 250 Robux a month, for up to 3 months, for each player who subscribes through your game's prompt.
- **Private servers:** up to 100 Robux a month for each Plus subscriber who uses a private server in your game.
- **Robux transfers:** a 10% cut of transfers between Plus subscribers made inside your game.
- **The trap:** Plus members get 10–20% off, and **Roblox pays the discount**, so you still earn your full share. But **hard-coded price labels show Plus players the wrong price.**

**Managed Pricing** (regional pricing plus price optimization) is **on by default for new games and items**. Regional prices fall between 30% and 100% of the base price (official, [Managed pricing](https://create.roblox.com/docs/production/monetization/managed-pricing); [Regional pricing](https://create.roblox.com/docs/production/monetization/regional-pricing)). In 2025 tests on top games, regional pricing raised the share of users spending by 17% in Mexico, 26% in Brazil and 52% in the Philippines ([Roblox Newsroom](https://about.roblox.com/newsroom/2025/04/roblox-launches-regional-pricing-for-in-experience-items), official). Price optimization needs about **60,000 transactions in 30 days**, so small games won't qualify for a while. Hard-coded prices break it as well (official, [Price optimization](https://create.roblox.com/docs/production/monetization/price-optimization)). The single most important monetization coding rule is therefore: **every price label reads from `GetProductInfoAsync`, never from a typed number** (inference from the three official pages).

### Revenue math, in plain numbers

Every **1,000 Robux a player spends** on your item becomes **700 earned Robux**. At the standard DevEx rate that is **$2.66**. At the U.S. 18+ rate, which applies to qualifying purchases by age-verified U.S. adults in games that are **R15-only (never R6)** or use other qualifying characters, it is **$3.78** (inference from official rates in [DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange) and the [18+ rate](https://create.roblox.com/docs/production/monetization/18-plus-devex-rate)). A web buyer pays about $9.99 per 1,000 Robux and a mobile buyer about $12.49 ([Gamsgo](https://www.gamsgo.com/blog/robux-prices), third-party). You therefore keep roughly **21–27% of the player's dollar** (inference). Cashing out requires **30,000 earned Robux ($114)**, an age of 13+, a verified email and tax forms (official, [DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange)).

For planning, use: **monthly USD ≈ DAU × payer conversion × daily ARPPU (Robux) × 0.7 × 0.0038 × 30**. For example, 1,000 DAU × 2% × 150 Robux works out to about **$239 a month**, before Creator Rewards and ads (inference; all inputs are assumptions). The platform-wide average is about **$32 of DevEx per 1,000 DAU per day**, derived from Q2 2026 DevEx fees of $363M across 123M DAU ([Roblox Q2 2026 8-K](https://www.sec.gov/Archives/edgar/data/0001315098/000162828026051059/ex991-robloxq22026earnin.htm), official, search summary; division is inference). That average is heavily skewed by hits, and a typical game earns far less.

Third-party benchmarks are rough guides only. GameAnalytics' 2026 report covers games with 1M+ MAU. It finds **3.8%** of players paid anything over the year, with a median ARPPU of **$0.70** ([GameAnalytics 2026](https://www.gameanalytics.com/reports/2026-roblox-report), third-party). Agency genre figures put ARPDAU at about $0.08 for simulators and $0.01 for obbies ([Bloxg](https://bloxg.com/statistics/roblox-game-revenue-statistics), third-party). Creator earnings are extremely concentrated. Coverage of Roblox data reports that the top 10 creators averaged about $65M each, while the 2024 median creator earned **$1,575** ([TechSpot](https://www.techspot.com/news/113855-roblox-top-creators-making-65-million-year-while.html), third-party). A repeatable process matters precisely because most individual games earn little.

### The shelf a small team should ship

Because RFY ranks **spend days** as well as Robux spent, a shelf built around frequent small purchases helps both revenue and reach (inference from [Discovery](https://create.roblox.com/docs/discovery)). The 2025 hits fit this pattern. Grow a Garden sold time-skips against "smart friction" such as inventory limits and seed scarcity, and Steal a Brainrot sold cheap impulse consumables and multipliers ([TickerTrends](https://blog.tickertrends.io/p/rblx-escape-tsunami-brainrot-impact-analysis); [BloxPrices](https://www.bloxprices.com/stats/steal-a-brainrot/), third-party). Recommended default shelf (inference):

| Slot | Example | Why |
|---|---|---|
| Permanent multiplier pass | 2x Cash | Classic best-seller; one-time |
| VIP pass | Chat tag, VIP area, small bonus | Status; no tactical pay-to-win |
| Cheap consumables, 5–50 Robux | Luck potion, speed boost, restock skip | Drives **spend days** |
| Starter pack (one-time, discounted) | Shown after the first "aha" moment | First-session conversion |
| Limited-time event items | Seasonal seeds or pets | Re-engagement spikes |
| Battle pass as a subscription | Monthly track | Recurring; 100% from month 2 if local-currency |
| Rewarded video | "Watch for 2x coins" (3–10 Robux value) | Monetizes non-payers |
| Paid private server | Monthly | Also feeds co-play days and Plus private-server income |

Roblox advises that paid perks should not grant a "tactical gameplay advantage" ([Engagement-based payouts legacy page](https://create.roblox.com/docs/production/monetization/engagement-based-payouts), official). Use the store personalization APIs: `RankProductsAsync`, called once at join, and `RecommendTopProductsAsync`, which returns nothing until the game has sales in the last 28 days (official, [Developer products](https://create.roblox.com/docs/production/monetization/developer-products)).

### Policy fences around random items and kids

Random rewards (eggs, gacha, luck boosts, pity systems) bought with Robux must show **every outcome with its numeric odds** before purchase. The odds must sum to 100%, update live when a luck boost is active, and the disclosure needs a word such as "Info" next to it, since an icon alone is not enough. When `PolicyService` reports `ArePaidRandomItemsRestricted`, the game must offer an alternative: an earnable path, a disclosed fixed sequence, direct sale at an expected-value price, or a block (official, [Paid random items](https://create.roblox.com/docs/production/monetization/paid-random-items)). Restrictions apply to under-18s in the UK (since August 2024) and Australia (since September 2024) ([DevForum UK](https://devforum.roblox.com/t/update-on-paid-random-items-restriction-for-uk-users-under-18/3072183), official). In Brazil, under-18s have been blocked since March 17, 2026 and unverified adults since March 31, 2026. A game that declares random items but skips PolicyService becomes **unplayable for Brazilian minors** ([Roblox Help: Brazil](https://en.help.roblox.com/hc/cs/articles/48706630819476-Brazil-Digital-ECA-Updates), official). Because every recent hit relied on random collectibles, the template should ship the odds UI and a non-random fallback **before** the first egg (inference).

### Purchases that never get lost

Grant developer products **only** inside `ProcessReceipt` or the newer `MarketplaceService:BindReceiptHandler`. Never grant from `PromptProductPurchaseFinished`, which fires even when a purchase fails (official, [Developer products](https://create.roblox.com/docs/production/monetization/developer-products)). Roblox documents four hazards: the same receipt can run **on two servers at once**, it can be redelivered, pending receipts arrive in no fixed order, and a purchase can fail to record even after you return PurchaseGranted (official, [ProcessReceipt reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#ProcessReceipt)).

The safe pattern, in plain words, has five steps (inference built on those guarantees):

1. Look up the player. If they aren't in this server, answer "not yet".
2. In one atomic save of the player's data, check whether this `PurchaseId` was already handled. If it was, report success without granting again.
3. If it wasn't, add the item and record the `PurchaseId`.
4. Report success only after that save succeeds.
5. Keep all product logic in one table keyed by ProductId, set up in **exactly one** server script.

`BindReceiptHandler` is required for Robux-transfer receipts. Its `ReceiptDecision` reference page was updated October 15, 2026 (official, [ReceiptDecision](https://create.roblox.com/docs/en-us/reference/engine/enums/ReceiptDecision.md)).

## A beginner-proof code template that survives many Claude sessions

### Plain modules replace Knit

Knit's repository "was archived by the owner on Jul 31, 2024". Its author explains that a services architecture "is easy to replicate, as ModuleScripts themselves can already work in this way out of the box". Network data still "requires runtime type-checking", because Luau types don't check what arrives over the wire ([Knit](https://github.com/Sleitnick/Knit); [ARCHIVAL.md](https://raw.githubusercontent.com/Sleitnick/Knit/main/ARCHIVAL.md), official from the author). Flamework requires TypeScript (roblox-ts) ([Flamework](https://flamework.fireboltofdeath.dev/docs/introduction)). The ECS library jecs suits simulation-heavy games ([jecs-template](https://github.com/LocalPulse/jecs-template)), but it is a conceptual hurdle for beginners.

The recommended foundation is deliberately boring (inference):

- **One server bootstrap script.** It requires every ModuleScript in a `Services` folder, calls each module's `Init()` (wiring only, no waiting), then starts each module's `Start()`.
- **One client bootstrap script** that does the same with `Controllers`.

This is about 30 lines of code. It gives a predictable load order and full type checking, because every service is a plain `require`.

Put `--!strict` at the top of every module. Luau's new type solver has left beta, which makes strict mode practical even for beginners ([Release notes 675](https://create.roblox.com/docs/release-notes/release-notes-675), official; GA date unverified). Keep modules **under about 300 lines**, each with a header comment saying what it owns. Small, typed, documented modules are what let a fresh Claude session, or a new teammate, work safely without re-reading the whole codebase (inference).

### The template's reusable modules

| Module | Job | Built on |
|---|---|---|
| Loader (Main.server / Main.client) | Init → Start lifecycle | Plain ModuleScripts |
| Net | The only place remotes are defined; validates types, ranges, rate limits | Blink IDL ([DevForum](https://devforum.roblox.com/t/blink-an-idl-compiler-written-in-luau-for-roblox-buffer-networking-0185/2959671)) or a thin RemoteEvent wrapper |
| DataService | Load and save, defaults, version migrations, session lock | ProfileStore ([GitHub](https://github.com/MadStudioRoblox/ProfileStore)) |
| PurchaseService | ProductId → grant table; idempotent receipts; passes and subscriptions | `BindReceiptHandler` |
| Signal, Trove | Events and leak-free cleanup | sleitnick packages via Wally ([RbxUtil](https://docsearch.algolia.com/mcp/docs/repo/sleitnick/rbxutil)) |
| UIController + state store | Plain table plus Changed signal | Studio-built UI |
| AudioController | Music/SFX/UI buses | Audio API faders |
| AnalyticsService wrapper | Same funnel and economy events in every game | Roblox AnalyticsService |
| Config | Prices (as IDs, not numbers), tuning values, feature flags | ReplicatedStorage/Shared |

Table assembled from the scripting notes; module choices are inference except where linked.

**Data.** ProfileStore "loads and caches data… on one game server and blocks other servers from accessing that data too early by establishing a session lock". It is "not designed… for in-game leaderboards" (official from the author, [ProfileStore](https://github.com/MadStudioRoblox/ProfileStore)). Its predecessor ProfileService is no longer supported ([DevForum](https://devforum.roblox.com/t/profilestore-save-your-player-data-easy-datastore-module/3190543/)). The official DataStore limits are 4 MB per key and a 50-character maximum for names and keys ([Data store limits](https://create.roblox.com/docs/cloud-services/data-stores/error-codes-and-limits.md), official). Store a `Version` number in every profile and run migration functions on load. Never save on every stat change. Use OrderedDataStore for leaderboards and MemoryStoreService only for short-lived cross-server state (inference). Use a separate DataStore name for development, such as `PlayerData_DEV`, so testers can never damage real saves (inference).

**Security.** Roblox's docs start from the principle that the client cannot be trusted ([Security tactics](https://create.roblox.com/docs/scripting/security/security-tactics), official), and Roblox provides no general anti-cheat ([DevForum](https://devforum.roblox.com/t/do-you-use-anti-cheat-apis/3933116)). Defences for each common attack (inference):

- **Spam:** a per-player rate limit on every remote.
- **Tampering:** a type and range check on every argument, rejecting NaN and infinity.
- **Damage and currency:** the client sends intent ("I swung at target T") and the server checks cooldown and range before applying anything.
- **Fake purchases:** grant only from the receipt handler.
- **Movement exploits:** **Server Authority**, generally available since July 2026, makes the server the arbiter of character physics, with client prediction and rollback. It blocks "flings, wall clips, or speed hacks", and simple games can enable it with `AuthorityMode = Server`. Complex custom gameplay may need rewrites, and remote events aren't synced to its timeline ([Roblox Newsroom](https://about.roblox.com/newsroom/2026/07/creating-responsive-cheat-resistant-games-roblox-server-authority); [DevForum](https://devforum.roblox.com/t/full-release-ship-fair-and-competitive-games-with-server-authority/4727993), official, search summary). Turn it on for any new game whose movement is standard.

`UnreliableRemoteEvent` payloads over 900 bytes are dropped ([UnreliableRemoteEvent](https://create.roblox.com/docs/reference/engine/classes/UnreliableRemoteEvent), official).

**Performance.** Profile before optimizing. The MicroProfiler shows per-frame cost and works on mobile through a web UI. `debug.profilebegin` labels your own code, and a rising LuaHeap or InstanceCount in the Developer Console signals a leak ([MicroProfiler](https://create.roblox.com/docs/en-us/performance-optimization/microprofiler.md); [Improve performance](https://create.roblox.com/docs/en-us/performance-optimization/improve), official). Template rules (inference):

- Use `task.wait`, `task.spawn` and `task.delay`, never the deprecated `wait`, `spawn` or `delay`.
- Run one shared Heartbeat loop per system, not one per object.
- Clean up every connection through a Trove on respawn and when a UI closes.
- Pool projectiles and effects.
- Assume StreamingEnabled means parts may be missing on the client.

### Tooling: start in Studio, graduate to files

There are two workable setups. **Studio-first** uses Team Create plus Roblox's built-in **Script Sync**, which links Studio scripts to files on disk so they can be edited in VS Code and kept in Git ([Script Sync](https://create.roblox.com/docs/scripting/sync), official, search excerpt). **Filesystem-first** uses Rokit (the toolchain manager that replaces Foreman and Aftman), Rojo, Wally or pesde, and Git as the source of truth ([Rokit](https://github.com/rojo-rbx/rokit); [Rojo](https://www.github.com/rojo-rbx/rojo)). A Luau-light team should start Studio-first, then move to Rojo once one person is comfortable with the command line. Rojo pays off once the same template repository is cloned for every new game (inference).

Roblox now ships an official **Studio MCP server** that lets an AI client explore the data model, write scripts, execute Luau and run play-mode tests ([Studio MCP](https://create.roblox.com/docs/studio/mcp), official, search excerpt). A February 2026 update added tools to start and stop playtests and read console output, and the Studio Assistant gained bring-your-own-key support for external LLMs, including Claude ([MoguraVR](https://www.moguravr.com/roblox-studio-mcp-server-agentic-update/), third-party). Open Cloud **Luau Execution** runs headless test scripts against a specific place version in CI (tasks up to 5 minutes, 10 concurrent per place), and Roblox publishes a reference repository, `place-ci-cd-demo` ([Luau Execution](https://create.roblox.com/docs/en-us/cloud/reference/features/luau-execution.md), official). Jest-Lua is the maintained test framework; TestEZ is archived ([jest-environment-roblox](https://classic.yarnpkg.com/en/package/@jsdotlua/jest-environment-roblox)).

### Working across multiple Claude sessions

None of this section comes from a Roblox source. It is a practical protocol inferred from the tooling above, built to solve the "every session starts cold" problem:

- **Keep a `docs/` folder at the repository root** with four files:
  - `STATE.md`: what works, what's broken, the next three tasks.
  - `DECISIONS.md`: dated, one line each, such as "chose ProfileStore over raw DataStore".
  - `ARCHITECTURE.md`: a map of services, controllers and remotes.
  - `METRICS.md`: the latest D1, session length, conversion and gate decision.
- **Start every session** by reading `STATE.md` and `ARCHITECTURE.md`. **End every session** by updating `STATE.md` and committing to Git with a descriptive message.
- **Give each session one bounded task**, such as "add the daily reward service", that touches as few modules as possible.
- **Never let an agent hold publish credentials for the production place.** Agents work in the Dev place and its DataStore scope. A human publishes to production after review.
- **Run the same checks on AI-written code as on human code**: strict types, linting, and a smoke playtest through Studio MCP.

## Art, UI, VFX and audio budgets are set by the cheapest phone

### Building and 3D art

The standard pipeline is to block out in Studio, model repeated and hero assets in Blender, and import them as MeshParts with SurfaceAppearance PBR materials. The hard limits are **20,000 triangles per mesh** and textures up to **4096×4096**. Meshes should be watertight, use quads, have one UV set and use at most 4 bone influences per vertex ([Specifications](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/specifications.md); [Texture specifications](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/art/modeling/texture-specifications.md), official). Export from Blender at **0.01 scale** and set Scale Unit = Stud on import ([Blender docs](https://create.roblox.com/docs/art/blender), official, search excerpt). The real constraint is memory, not the caps. A 1024² texture uses **4× the memory** of a 512². Images "rarely need more than 512²" and minor ones should be under 256². Tint a single texture with SurfaceAppearance.Color and use trim sheets ([Improve performance](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md), official). Aim for roughly 500–5,000 triangles on props that repeat many times (inference).

The rendering rules worth memorizing all come from the same official performance page:

- **Upload each mesh once and duplicate it in Studio.** Identical meshes share a single draw call only if their textures also match. Reimporting a map can give copies different IDs and break this.
- Anchor everything static.
- Give decorative parts **Box** collision with CanCollide, CanTouch and CanQuery off.
- Turn off CastShadow on small and moving parts.
- Keep **StreamingEnabled** on (it is on by default, and the docs call it "the highest-impact" memory improvement).
- Set `Model.LevelOfDetail = SLIM`. SLIM, announced at RDC 2025, replaces the old model LOD.

Organize maps as many small Models (one building = one Model) rather than giant containers. Have the **group own every upload** from day one, so permissions don't break when someone leaves (inference from [Creator Store / asset privacy](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/production/creator-store.md)). Free models are a malware risk. Roblox prohibits `loadstring`, remote loading and obfuscation in them, and you should right-click → **Disable Scripts** before inspecting any insert (official, same).

Roblox's generative tools are useful for prototypes and filler but not yet for hero art:

- **Cube 3D** text-to-mesh launched in beta in March 2025.
- **4D generation** (functional cars and bodies) arrived in February 2026.
- The **Texture Generator** is still beta.
- **Accessory Auto-Setup** entered beta in March 2026.

Sources: [TechCrunch](https://techcrunch.com/?p=2981320); [MoguraVR](https://www.moguravr.com/roblox-cube-foundation-model-4d-generation-4k-texture/); [DevForum](https://devforum.roblox.com/t/client-beta-in-experience-accessory-auto-setup/4358192). Run AI output through a cleanup step (triangle count, Box/Hull collision, consistent texel density) before it enters the kit (inference).

**Lighting changed in 2025.** `Lighting.Technology` "has been superseded by LightingStyle and PrioritizeLightingQuality". The old choices map as follows: Future = Realistic + priority on, ShadowMap = Soft + on, Voxel = Soft + off. Unified Lighting has been fully live since July 23, 2025 ([Technology enum](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/reference/engine/enums/Technology.yaml), official; [DevForum](https://devforum.roblox.com/t/let-there-be-unified-light-unified-lighting-is-fully-live/3401512)). For mobile-heavy audiences, use Soft with priority off unless lighting is central to the mood, as in horror. Build the mood with Atmosphere, ColorGrading and a Sky rather than many dynamic lights (inference). The default art direction for a factory is stylized low-poly on one shared 512–1024 trim-sheet atlas, tinted per object. It instances well, stays light on memory and ships fast (inference consistent with the official performance guidance).

**Characters.** R15 is required for layered clothing and, under the June 2026 rule, for the higher U.S. 18+ DevEx rate. A game that used R6 at any point does not qualify ([18+ rate](https://create.roblox.com/docs/production/monetization/18-plus-devex-rate), official). Animations made for R15 do not work on R6, and the reverse is also true. Animations must be owned by, or shared with, the game's owner ([DevForum](https://devforum.roblox.com/t/sharing-animation-assets-with-connections-and-groups/3892540)). Choose R15 in the template unless an R6 style is essential to the concept (inference).

### UI that works on a phone, a tablet and a TV

Build every interface mobile-first:

- Use **Scale, not Offset** for position and size. Roblox warns that pixel layouts vary arbitrarily across devices ([Cross-platform](https://create.roblox.com/docs/projects/cross-platform), official).
- Use AnchorPoint for alignment, UIListLayout (flex) or grid layouts for structure, UIAspectRatioConstraint on square icons, and 9-slice images for panels ([Position and size](https://create.roblox.com/docs/ui/position-and-size); [9-slice](https://create.roblox.com/docs/ui/9-slice), official).
- Leave `ScreenGui.ScreenInsets` at its default **CoreUISafeInsets** for anything tappable, so notches and Roblox's top bar never cover a button ([On-screen containers](https://create.roblox.com/docs/ui/on-screen-containers), official).
- Use `GuiService.ViewportDisplaySize` (Small/Medium/Large) to adapt layouts.
- Handle touch, gamepad and keyboard through the **Input Action System**. `InputActionLabel` shows button prompts that update automatically when the player switches device ([Input Action System](https://create.roblox.com/docs/input/input-action-system), official).

Roblox's CSS-like **styling system** handles consistent styling: StyleSheets, tokens, themes, and queries by screen size, input type and reduced motion. The Style Editor is still in **beta**, so mirror tokens in a ModuleScript as a fallback ([UI styling](https://create.roblox.com/docs/ui/styling), official; fallback is inference). For a Luau-light team, plain Studio-built UI plus styling is the low-risk path. Fusion or Vide are lighter reactive options. React-Lua, which Roblox maintains, suits large dynamic UIs but has a steep learning curve. Roact is outdated ([React-Lua](https://github.com/Roblox/react-lua); [Fusion](https://github.com/dphfox/Fusion); [Vide](https://github.com/centau/vide); [DevForum](https://devforum.roblox.com/t/how-to-react-roblox/2964543?page=2)). Figma import plugins such as RoImport and UILint exist, but imports usually arrive in Offset and need converting to Scale ([DevForum](https://devforum.roblox.com/t/importing-ui-from-figma-sucks/3381689)).

The official UX guidance is concrete. Put close buttons top-right. Grey out unusable items, use a lock icon for locked ones, and show unaffordable prices in red. Make the best-value bundle visually larger. Give every action feedback, such as a hover color, a press animation or a "cha-ching" on purchase ([UI and UX design](https://create.roblox.com/docs/production/game-design/ui-ux-design), official). Onboarding should "get to the fun quickly", because "new players typically decide their interest in a game within minutes". Use contextual tutorials that appear on first use, and timed hints only for stuck players. For example, if most players press a button within 10 seconds, highlight it at 11 seconds, once. End onboarding on a designed "moment of joy" ([Onboarding](https://create.roblox.com/docs/production/game-design/onboarding); [Onboarding techniques](https://create.roblox.com/docs/production/game-design/onboarding-techniques), official). This is the design answer to the 60-second and 180-second bounce signals.

**Accessibility and localization:**

- Respect `GuiService.PreferredTextSize`, `PreferredTransparency` and `ReducedMotionEnabled`.
- Never rely on color alone ("over 5% of people… have some form of color blindness") or on sound alone ([Accessibility](https://create.roblox.com/docs/production/publishing/accessibility), official).
- Automatic Text Capture plus auto-translation localizes UI strings for free, within quotas. Turn AutoLocalize off on names and signs ([Automatic translation](https://create.roblox.com/docs/production/localization/automatic-translations), official).
- Leave 30–40% extra room for translated text (inference).

### VFX on a budget

ParticleEmitters, Beams, Trails and Highlights are the core toolkit. Official limits:

- A single emitter produces at most **400 particles per second (100 on mobile)**.
- Large on-screen particles cost GPU fill-rate, and overlapping transparent layers cause overdraw.
- Clients "automatically deactivate flipbooks when they are low on memory, which is likely for older mobile phones".
- Flipbooks come in 2×2, 4×4 or 8×8 grids, with padding between frames.
- LightEmission 1 gives additive glow.
- The client shows at most **255 Highlights**.

Sources: [Particle emitters](https://create.roblox.com/docs/effects/particle-emitters); [Highlighting](https://create.roblox.com/docs/effects/highlighting). Particles also batch poorly and add draw calls ([Improve performance](https://create.roblox.com/docs/performance-optimization/improve), official). The standard architecture: the **server validates and fires a tiny message, and each client spawns the effect locally**. Rate-limit those remotes, and replay persistent effects for players who join late ([DevForum](https://devforum.roblox.com/t/correct-way-of-scripting-vfx/2439994); [DevForum](https://devforum.roblox.com/t/how-should-i-prevent-exploiters-spamming-my-remoteevent-for-vfx-replication/4749010), community). Template rules (inference):

- Emit in bursts (`:Emit(n)`) rather than at a high continuous rate.
- Share a few 512² flipbook sheets across effects.
- Pool emitters.
- Gate camera shake and flashes behind ReducedMotionEnabled.

Roblox has no official camera-shake API. Keep shake small, and use hit-stop of about 50–100 ms for heavy hits ([Wayline](https://www.wayline.io/learn/game-feel/1), third-party).

### Audio with the new API

Roblox says "Sound, SoundGroup, and SoundEffect objects are now discouraged in favor of… audio objects". In the new system, AudioPlayer is the source, AudioEmitter and AudioListener handle 3D position, AudioDeviceOutput is the speakers, and **Wire** connects them. Effects include Equalizer, Compressor, Reverb, Fader and Analyzer ([Audio objects](https://create.roblox.com/docs/audio/objects); [Audio effects](https://create.roblox.com/docs/audio/effects), official). Upload rules (official, [Audio assets](https://create.roblox.com/docs/audio/assets)):

- You must hold the legal rights to the audio.
- Files must be under **20 MB and under 7 minutes**, at 48 kHz or less.
- Verified creators get **2,000 free uploads per 30 days**; unverified creators get 100.
- The Creator Store offers **100,000+ licensed tracks and sound effects**. Copy the asset ID into an AudioPlayer, because clicking inserts a legacy Sound.

Since March 2022 most user audio has been private, so use your own uploads or the licensed catalog ([DevForum](https://devforum.roblox.com/t/1701697), official). The template setup: one AudioFader per bus (Music, SFX, UI), wired to a single output and controlled from a settings menu. UI sounds should be short, slightly pitch-varied, and paired with a `HapticEffect` of type UIClick on mobile (inference; haptics from [Mobile input](https://create.roblox.com/docs/input/mobile)).

## Recent hits share a loop shape, a tiny team and weekly live events

### What the 2025–2026 breakouts actually looked like

**Grow a Garden** was reportedly built by a teenager "in like three days" ([Yahoo/PC Gamer](https://tech.yahoo.com/gaming/articles/roblox-farming-game-made-teenager-002326583.html), third-party). It had about **1,000 CCU** when Splitting Point took it over and moved about 12 of its 19 developers onto it. It went on to peak around 22M concurrent players in August 2025 ([Wikipedia](https://en.wikipedia.org/wiki/Grow_a_Garden); [GamesBeat](https://gamesbeat.com/janzen-madsen-interview/), third-party). Its live-ops rhythm was:

- Major updates on Saturdays, preceded by an "Admin Abuse" event that starts 30–60 minutes before the drop (special weather, shop restocks, exclusive items).
- A "Watering Wednesday" mid-week mini event.

Source: [Grow a Garden Wiki](https://growagarden.fandom.com/wiki/Admin_Abuse), community.

**Steal a Brainrot** combined collect, defend and steal, and is the only Roblox game to pass 25M CCU. It then fell about 99% to around 215K CCU in 2026, and every event spike was followed by a sharper fall ([RoWatcher](https://rowatcher.com/news/is-the-brainrot-trend-dying-what-ccu-data-from-three-top-games-reveals), third-party).

**99 Nights in the Forest** came from a trio. It was planned as a one-week project, took three months, and peaked at 14M CCU ([DevForum Creator Spotlight](https://devforum.roblox.com/t/creator-spotlight-the-story-behind-99-nights-in-the-forest/4036940), official spotlight, search summary).

**Dead Rails** came from RCM Games, a group with about **70 titles** ([RoMonitor](https://romonitorstats.com/experience/116495829188952/), third-party). Roblox's own channels promoted it before large YouTubers picked it up ([GameAnalytics](https://www.gameanalytics.com/blog/dead-rails-and-the-hit-makers-formula), third-party).

In 2026, **Steal an Egg** peaked around 14M CCU. Roblox briefly pulled it for a rewarded "Reels" feed and relisted it without that feature ([RoStats](https://rostats.io/records); [Slashdot](https://games.slashdot.org/story/26/08/28/0027222/roblox-is-cracking-down-on-games-that-reward-kids-for-doomscrolling), third-party). Within weeks it spawned remixes such as Clone to Steal Eggs ([Rolimons](https://www.rolimons.com/game/76943966208523)).

All revenue figures for these games are tracker models that conflict by up to 10×. For example, Steal a Brainrot's current revenue is estimated anywhere from $1.4M to $3.5M a month ([RoWatcher](https://rowatcher.com/games/7709344486/steal-a-brainrot); [profitable.app](https://profitable.app/roblox/games/steal-a-brainrot), third-party).

The shared recipe has five parts (inference):

1. A trending noun or meme.
2. An idle or collect loop that pays out while the player is away.
3. A social conflict or co-op twist.
4. Scarcity through timed restocks.
5. A weekly appointment ("be online Saturday at X").

The most important lesson is structural. **Hits came from volume and fast remixing, then were scaled by an operator with staff and capital.** Do Big and Voldex buy rising games from independent developers ([Tubefilter](https://www.tubefilter.com/2025/07/14/indie-game-creators-are-making-millions-selling-their-roblox-worlds/), third-party), and funds such as the Gamefam Creator Fund ($1K–$100K+, applicants 18+) exist ([Gamefam](https://gamefam.com/creatorfund)). For a small team that cannot staff weekly live ops indefinitely, partnering with or selling to an operator is a legitimate planned exit (inference).

### Why most new games fail

The community diagnosis is consistent:

- Weak first-session retention: long tutorials, an unclear loop, poor performance on low-end devices ([DevForum: Why games fail](https://devforum.roblox.com/t/why-games-fail-and-how-to-fix-it-a-comprehensive-tutorial/1588819)).
- The cold-start problem, because Roblox won't promote a game with no players ([DevForum](https://devforum.roblox.com/t/why-has-our-game-failed/2921427)).
- Adding features before the core loop is finished ([DevForum](https://devforum.roblox.com/t/plugin-why-you-never-finish-roblox-games/4223242)).
- Technical quality the algorithm never sees ([DevForum](https://devforum.roblox.com/t/why-your-technically-superior-game-isn%E2%80%99t-succeeding-on-roblox-and-why-the-algorithm-ignores-it/4461606)).

Struggling games commonly report D1 of 2–2.5% and 3–5.5 minutes of playtime ([DevForum](https://devforum.roblox.com/t/how-do-i-improve-average-playtime-and-day-1-retention/4565940)). 2026 adds new ways to fail: missing the publishing eligibility or age-tier steps, and shipping now-restricted mechanics such as rewarded media feeds (inference). Treat clones as a fact of life. Even Fortnite copied Steal a Brainrot's mode ([Mein-MMO](https://mein-mmo.de/en/fortnite-steal-the-brainrot-internet-culture,1532127)). The defence is speed and weekly updates, not secrecy (inference).

## The repeatable pipeline: eight phases, hard gates, one template

Everything below is **inference** that combines the official facts above with the third-party benchmarks. Roblox publishes no official kill criteria. Its own guidance is to get D1 and session time "comparable or above your similar game benchmarks" in Creator Analytics ([Acquisition](https://create.roblox.com/docs/production/analytics/acquisition), official). Treat that in-dashboard benchmark as the primary yardstick, with the numbers below as fallbacks.

### Metric gates and kill criteria

| Metric | Kill or pivot | Iterate (1–2 cycles) | Scale | Basis |
|---|---|---|---|---|
| D1 retention | < 5% | 5–10% | ≥ 10% (stretch 15–22%) | GameAnalytics median 10.3%, p99 22.2% ([GA 2026](https://www.gameanalytics.com/reports/2026-roblox-report)); DevForum "≥10%" rule ([DevForum](https://devforum.roblox.com/t/suggestions-to-improve-average-playtime-d1-retention/3883895)) |
| Average session | < 5 min | 5–8 min | ≥ 8–10 min (stretch 12+) | GA median 9.8 min; 0–6 min games "fragile", 19+ min "hits" ([GA 2025](https://www.gameanalytics.com/reports/2025-roblox-report)) |
| D7 retention | < 1% | 1–2% | ≥ 2–3% | GA median 1.6% |
| First-play bounce (<60 s) | Above similar-game benchmark after a fix | Near benchmark | Below benchmark | Home Recommendations tab ([Discovery](https://create.roblox.com/docs/discovery)) |
| Payer conversion | ~0 after shelf is live | < 1% | 2–4% | Third-party genre ranges ([CalculatorsUniverse](https://calculatorsuniverse.com/blog/roblox-game-revenue-genre-conversion-explained)) |

Evaluate gates after **7–14 days and at least a few thousand visits**. Kill only when D1 **and** session length both sit in the kill column. Compare ad cohorts against organic and friend cohorts before killing, because ad traffic may understate quality. Since June 2026, never scale on D1 alone: D7 and the D8–28 window now drive impressions.

### The phases

| Phase | Time box | Goal | Checklist | Exit gate |
|---|---|---|---|---|
| **0. Setup (once)** | 1–2 weeks | Factory ready | Group owns all assets; every member age-checked or ID-verified with 2FA; template repo (below) with loader, Net, DataService, PurchaseService, AudioController, Analytics; Dev and Prod DataStore names; `docs/STATE.md` protocol; Studio MCP connected | A blank game boots, saves, sells a test product idempotently |
| **1. Concept** | 1–2 days | Pick a loop worth remixing | Proven loop from current top charts + one twist + a theme; one-sentence pitch; note the age target (Kids/Select vs 16+/18+, and R15 for the 18+ DevEx rate); check for random items and plan the odds UI and fallback | Pitch passes "would I click this thumbnail?" with 3 outsiders |
| **2. Vertical slice** | 3–10 days | First 3 minutes are fun | Spawn into gameplay in seconds; contextual tutorial; first reward within 60 s; "moment of joy" by 3 min; one daily-return hook; Scale-based UI with safe insets; trim-sheet art; SLIM and streaming on; juice on every action | Friends playtest (up to 10 pre-release testers): most reach minute 3 unprompted |
| **3. Launch prep** | 2–4 days | Eligible and instrumented | Maturity questionnaire; 3–5 honest thumbnails + 512² icon; keyword-honest description; funnel events for minutes 0–3 and shop; economy events; price labels via `GetProductInfoAsync`; PolicyService checks; Server Authority if movement is standard; MicroProfiler pass on a low-end phone | Zero errors in console on mobile emulator; receipts tested twice |
| **4. 16+ soft launch** | 7–14 days | Read real metrics | Public to age-checked 16+; $50–200 of **Plays** ads (official CPP ~ $0.01) to clear retrieval; read Home Recommendations tab; fix bounce at 60 s and 180 s | Apply the gate table |
| **5. Kids/Select unlock** (if targeting under-16) | ≤ 60 days | 250 highly engaged plays | **Engagement** ads campaign; creator and Discord pushes; Kids/Select creator requirements (fee or Plus); content at Moderate or below; no rewarded media feeds | Audience Reach dashboard shows threshold met |
| **6. Scale** | 4–8 weeks | Expand RFY cohorts | Weekly update (Saturdays match Home's weekly peak); pre-update live/admin event; Experience Event + announcement; new thumbnail set per major update; notification opt-in after a positive moment; invites and party bonus for co-play; add consumables and battle pass; Standout nomination only if novel | D7 and D8–28 windows at or above benchmark |
| **7. Live ops or exit** | Ongoing | Harvest the 28-day window | Monthly roadmap; seasonal events (Halloween drives all-time peaks); Experiments on big changes only; watch for update regressions; decide: keep, hand to an operator, or sunset | Revenue covers update cost, or exit |

Sources behind the phase details: Saturday weekly Home peak (official, [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)); pre-release preview with up to 10 friends and the Kids/Select steps (official, [Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places); [Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select)); Halloween peaks for Forsaken and Dress to Impress ([Rolimons](https://www.rolimons.com/game/18687417158), third-party); post-update drops ([DevForum](https://devforum.roblox.com/t/sudden-drop-on-playtime-and-retention-with-update/3880064)).

A sensible cadence for a small team is to run **two to four concepts in parallel through Phases 1–4**, spending a few hundred dollars on ads in total, and to carry forward only those that pass the gate. This follows the volume logic of RCM Games' ~70 titles (inference). A typical team shape: one designer-producer who owns metrics and live ops, one scripter who owns the template, and a freelance pool for builds, UI and VFX. Freelance rates run about $15–90 an hour by role ([Game-Ace](https://game-ace.com/blog/how-to-hire-the-best-roblox-game-developer/); [Innovecs](https://www.innovecsgames.com/blog/roblox-game-developers-for-hire/), third-party).

### Reusable template folder structure

The layout below follows Roblox's trust boundary. Anything in ReplicatedStorage or on the client can be read and modified by exploiters, so authoritative logic stays in ServerScriptService and ServerStorage (inference consistent with [Security tactics](https://create.roblox.com/docs/scripting/security/security-tactics)). It matches the Rojo default layout, and it works equally well as the Studio Explorer tree if you use Script Sync instead.

```
my-roblox-template/
├── docs/                         # read first, update last, every session
│   ├── STATE.md                  # what works, what's broken, next 3 tasks
│   ├── DECISIONS.md              # dated one-line decisions
│   ├── ARCHITECTURE.md           # services, controllers, remotes map
│   ├── METRICS.md                # D1 / session / D7 / conversion + gate verdict
│   └── LAUNCH_CHECKLIST.md       # phases 3–5 checklists, ticked per game
├── src/
│   ├── server/                   # -> ServerScriptService/Server
│   │   ├── Main.server.luau      # loader: require Services, Init all, Start all
│   │   └── Services/
│   │       ├── DataService.luau      # ProfileStore, defaults, Version migrations
│   │       ├── PurchaseService.luau  # BindReceiptHandler, PurchaseId dedupe
│   │       ├── RewardService.luau    # daily rewards, streaks, restock timers
│   │       ├── AnalyticsService.luau # funnel + economy events wrapper
│   │       ├── PolicyService.luau    # paid-random-item and ads gating
│   │       └── <Game>Service.luau    # game-specific logic, one per system
│   ├── client/                   # -> StarterPlayer/StarterPlayerScripts/Client
│   │   ├── Main.client.luau
│   │   └── Controllers/
│   │       ├── UIController.luau
│   │       ├── InputController.luau  # Input Action System bindings
│   │       ├── AudioController.luau  # Music/SFX/UI faders
│   │       └── VFXController.luau    # pooled, client-spawned effects
│   ├── shared/                   # -> ReplicatedStorage/Shared
│   │   ├── Config/
│   │   │   ├── Products.luau     # product/pass IDs only, never prices
│   │   │   ├── Economy.luau      # tuning numbers
│   │   │   └── Flags.luau        # feature toggles
│   │   ├── Net.luau              # all remotes + validators + rate limits (or Blink output)
│   │   ├── Types.luau
│   │   └── Util/
│   └── storage/                  # -> ServerStorage (maps, server-only assets)
├── assets/                       # source art, NOT synced to Roblox
│   ├── blender/  textures/  ui/  vfx/  audio/
├── tests/                        # Jest-Lua specs for migrations, economy, validators
├── Packages/                     # Wally/pesde output -> ReplicatedStorage/Packages
├── default.project.json          # Rojo mapping
├── rokit.toml  wally.toml  selene.toml  stylua.toml
└── .github/workflows/ci.yml      # lint, type-check, tests via Luau Execution, publish to Staging
```

In Studio's Workspace, mirror this discipline. Have one `Map` folder of small, compact Models (Atomic for interactables, Persistent only for the spawn), one `Interactables` set tagged with CollectionService, and a "decor" convention: Anchored, no CanCollide/CanTouch/CanQuery, Box collision, no CastShadow. A short command-bar script can enforce it (inference from the official [streaming](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/workspace/streaming/index.md) and [performance](https://raw.githubusercontent.com/Roblox/creator-docs/main/content/en-us/performance-optimization/improve.md) docs).

### Uncertainties to keep in view

Several things remain unknown or unsettled:

- Roblox does not publish signal weights, and since 2026 it says they are personalized per user. No public PTR or bounce benchmarks exist outside each game's dashboard.
- No official Roblox data quantifies the impression lift from an update, the effect of YouTuber coverage, or acquisition prices for games.
- The steep official-versus-agency gap in ad costs (about 50×) is unresolved.
- Ad-cohort metrics may understate a game's organic quality.
- The RDC 2026 claims about age-aware ranking and Moments come from a secondary summary.
- Some 2026 Kids/Select requirements still differ between official docs and third-party guides, so check the Creator Hub on the day you publish.

## Conclusion

The June 2026 shift to a 28-day, organic-only, per-user ranking model means a Roblox game is no longer judged mainly by its launch. It is judged by what a stranger does on day 1, in week 1 and in weeks 2–4. That favours a different kind of team than the one that chased meme spikes in 2025. The winning small team runs a **factory with a quality-control line**. It reuses one hardened code template, so saves, purchases, security and analytics are solved once. It spends days, not months, on each concept, and lets cheap ad plays and fixed metric gates decide which games deserve weekly live ops. Monetization, discovery and retention now reinforce one another: cheap repeatable purchases raise spend days, daily hooks raise play days and Creator Rewards, and both raise impressions.

The underrated levers are mostly compliance and engineering hygiene, and most competitors still neglect them. Reading prices dynamically protects regional pricing, Plus discounts and price tests. Odds UI with PolicyService fallbacks keeps random-item games playable in the UK, Australia and Brazil. An R15-only character choice can add 42% to adult U.S. cash-outs. Planning for the 250-engaged-play Kids/Select gate turns a silent blocker into a scheduled milestone. A `docs/STATE.md` discipline lets every new Claude session start warm instead of cold. A team that gets these right on its first game gets them for free on every game after it, and that compounding advantage is the repeatable route to a hit.
