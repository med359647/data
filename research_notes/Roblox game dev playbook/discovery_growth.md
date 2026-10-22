# Roblox Discovery & Growth (as of Oct 22, 2026)

Method note: Roblox's official docs were read directly from the open-source repo github.com/Roblox/creator-docs (HEAD commit dated **Oct 21, 2026**). These are cited below by their create.roblox.com/docs URLs. DevForum, gameanalytics.com and IR pages could **not** be fetched from this environment (DNS/proxy block). Claims from those sources come from search-engine summaries of the pages. They are marked "(search summary)" and should be spot-checked. "(3rd-party)" marks non-Roblox sources.

## 1. Recommended for You (RFY): retrieval vs. ranking, signals, windows, 2025–2026 changes

### Takeaway
RFY has two stages. **Retrieval** needs only a very low number of plays from *any* source. **Ranking** of about 100 games per user scores only users who joined *organically from RFY*, using per-user averages. The current (Oct 2026) official signal table is PTR, first-play bounce (<60 s and 61–180 s), play days and playtime (capped at 60 min/day), then co-play days, qualified sessions, spend days and Robux per user. It is scored over D1, D2–7 and D8–28. The windows went from 7 to 28 days in June 2026, and Roblox says weighting is becoming personalized per user.

### Cited Findings
**Mechanics (official, current docs)**
- Two stages. **Retrieval** selects a per-user subset "based on key signals like engagement, retention, and monetization". **Ranking** orders that subset per user. Signals from "sponsored ads, curation, search, charts, friends, teleport, notifications, curated games, and other social media sharing can accelerate your consideration". "Even a small number of people playing" signals the game is worth considering. — [Roblox Docs: Discovery](https://create.roblox.com/docs/discovery)
- Ranking excludes everything non-RFY: "Roblox doesn't count the engagement, monetization, or retention of users first acquired from ads, curation, friends, search, social media, or any other source in the ranking stage." — [Discovery](https://create.roblox.com/docs/discovery)
- Funnel size: the algorithm "starts with all eligible games and narrows down to roughly 100 games shown on a user's Home page", and "continuously explores" by introducing new games to new users. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Old or failed games can regrow. "The retrieval stage requires only a very low minimum number of plays from any source… The algorithm tests your game daily, and if it sees improving performance, it increases impressions." "There is no penalty for games that did not perform well at first. The signals use a moving window." — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Explore/expand: "you might see a spike in new users from recommendations (explore) after a content update. If that new user cohort has good engagement and monetization, Roblox is more likely to continue to recommend your game to more such user cohorts (expand)." — [Discovery](https://create.roblox.com/docs/discovery)
- **Official signal table (verified in the raw markdown, Oct 21, 2026):**
  - *Most important:* (1) **Play-through rate** (no time segment). (2) **First-play bounce rate**, a negative signal, segmented "< 60 seconds average rate" and "61–180 seconds average rate". (3) **Play days per user**. (4) **Playtime per user**, with "a maximum of 60 minutes per user, per game, per day".
  - *Important:* (5) **Intentional co-play days per user** ("join, invites, or private servers"). (6) **Qualified play sessions per user**, which filters accidental clicks and quick bounces. (7) **Spend days per user**. (8) **Robux spent per user**.
  - Signals 3–8 are segmented D1 / D2–7 / D8–28. — [Discovery](https://create.roblox.com/docs/discovery)
- Windows are "considered both separately and combined together to decide impression volume". D2–7 play days = the average number of the 6 days in the window that RFY-acquired users played. Playtime = total playtime ÷ users. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- New games don't wait 28 days. Signal order is PTR and bounce (first session) → D1 (playtime, play days, Robux spend, co-play) → D2–7 → D8–28. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- PTR and bounce measure only RFY-acquired users' **first session**. Returning traffic comes via Continue and doesn't count as RFY impressions. Later D2–7 and D8–28 behavior of RFY-acquired users *does* count even if they return via Continue. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Per-user averages, not totals, so small games aren't disadvantaged. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Retention vs. monetization: "If retention is low, focus on core gameplay first. Once retention is strong, improving monetization can help you increase your Home impressions." Games strong in only one area still get impressions. "Games that perform well in both… might receive broader distribution." — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Genre isn't an explicit ranking factor; the model learns it from behavior. Story or finite games "are not penalized" for low D8–28. Wrong genre tags hurt indirectly through bounces. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Four impression drivers: your changes, algorithm changes, Home traffic (weekly peak on **Saturday**, summer/back-to-school, holidays) and competitors. Example: "you update your game and drive your signals up 50%. However, competitors… improve their signals more than 50%" → minimal growth. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- PTR temporarily drops when impressions expand. This is "normal". — [Discovery](https://create.roblox.com/docs/discovery)
- A custom thumbnail is required. "If your game only has a default thumbnail, it is not eligible" for Home recommendation impressions. — [Discovery](https://create.roblox.com/docs/discovery)

**2025–2026 timeline (DevForum; search summaries, not directly fetched)**
- **Mar/Apr 2025 (older):** "Boost Your Discovery with the Improved RFY Algorithm and Analytics" introduced per-user averaged signals, the intentional co-play signal and the Home Recommendations analytics tab. — [DevForum 3587441](https://devforum.roblox.com/t/boost-your-discovery-with-the-improved-recommended-for-you-algorithm-and-analytics-for-creators/3587441) (search summary)
- **Dec 2025:** An improved RFY was released globally with signals including *qualified* PTR, 7-day playtime per user, play days, spend days, Robux spent and co-play days. — [Roblox Creator Updates](https://create.roblox.com/updates) / [DevForum search results](https://devforum.roblox.com/t/testing-more-recommended-for-you-algorithm-signals/4568033) (search summary)
- **Mar 26, 2026, "How we are improving Home this year":**
  - Today's Picks becomes **Standout Games**, a hand-curated sort with a creator nomination form.
  - A new signal, **"Deep play through rate"**, was added.
  - RFY is moving to "dynamic and personalized weighting… there will not be a single global formula".
  - Roblox is testing a flyout for Continue and Favorites; Continue can rank higher for users who habitually play from it.
  - Tests expanded into RFY on May 14, 2026. — [DevForum 4502571](https://devforum.roblox.com/t/how-we-are-improving-home-this-year/4502571) (search summary)
- **Mar 2026:** A "7-day qualified play sessions per user" signal was added. — [DevForum 4568033](https://devforum.roblox.com/t/testing-more-recommended-for-you-algorithm-signals/4568033) (search summary)
- **Apr 2026:** Roblox tested longer signal horizons. Developers objected that new games lack long-term data (a chicken-and-egg problem). — [DevForum 4568033](https://devforum.roblox.com/t/testing-more-recommended-for-you-algorithm-signals/4568033) (search summary)
- **June 2026, "RFY Algorithm Improvements That Better Value Long-Term Retention":**
  - Signals were extended "from a 7-day window to a 28-day window, measured across Day 1, Day 2–7, and Day 8–28".
  - **Qualified PTR was dropped; PTR and first-play bounce rate were added.**
  - Signals and their relative contribution were brought into Creator Analytics. — [DevForum 4684575](https://devforum.roblox.com/t/recommended-for-you-algorithm-improvements-that-better-value-long-term-retention/4684575) (search summary). This matches the Oct 2026 docs table.
- **Aug 2026:** Chief Growth Officer John Ciancutti said Roblox was testing an update to "better recognize long-term player value". The Creator Updates page logged an RFY update going live. — [Roblox Creator Updates](https://create.roblox.com/updates) (search summary)
- **Oct 12, 2026, "Improved Discovery Measurement in Creator Analytics":** The way impressions, clicks and plays are recorded changed. Roblox says this does **not** change how RFY recommends games, but **PTR may look slightly lower**. — [DevForum 4930122](https://devforum.roblox.com/t/improved-discovery-measurement-in-creator-analytics/4930122) (search summary)
- **Business context:** Roblox's Q2 2026 call attributed a bookings shortfall partly to engagement shifting toward lower-monetizing games and "changes to its Recommended for You algorithm" among younger U.S./Canada users. — [Roblox Q2 2026 call transcript](https://s27.q4cdn.com/984876518/files/doc_financials/2026/q2/32789865_2009724400_3775763_Transcript_EditedCopy_20260730233208.pdf) (search summary)

### Inferences
- Treat the docs table as current. "Deep play through rate" (Mar 2026) is not in the Oct 2026 docs. It was likely folded into the June redesign, where PTR + bounce + qualified sessions replaced QPTR, but this is unconfirmed.
- Because weights are now per-user and dynamic, chasing one metric is less useful than improving the whole funnel: impression → click → first 3 minutes → D1 → week 1 → weeks 2–4.
- A practical first-3-minutes target follows from the bounce segments: keep players past **60 s**, then past **180 s**.
- Do not compare PTR from before Oct 12, 2026 with PTR after it.

### Gaps
- Exact signal weights aren't published. Roblox says Creator Analytics now shows "relative contribution", but the values weren't retrievable here.
- No official PTR or bounce benchmarks exist outside each game's own benchmark panel.
- The June and Oct 2026 DevForum posts weren't read in full (fetch blocked).

## 2. Other discovery surfaces

### Takeaway
Home is "usually where the vast majority of users find games". Outside RFY the main levers are:
- multiple personalized thumbnails (+8.5% avg qualified PTR)
- accurate keyword-rich descriptions for semantic search
- Experience Events and update announcements (once per 3 days)
- notification opt-in prompts
- curation nomination for Standout Games
- Continue and Friends, which are fed by retention and social features

### Cited Findings
- Acquisition sources tracked in Creator Analytics:
  - **Continue Play** (Home)
  - **Friends** (Friend Activity on Home)
  - **Search** (organic search + "Recommended Experiences" on the details page)
  - **Charts** (all sorts)
  - **Sponsored ads** (sponsored experiences + Sponsored Takeovers)
  - **Search ads**
  - Other or unattributed traffic, including external. — [Docs: Acquisition analytics](https://create.roblox.com/docs/production/analytics/acquisition)
- "Among all Roblox sources, **Home** is usually where the vast majority of users find games." — [Docs: Acquisition](https://create.roblox.com/docs/production/analytics/acquisition)
- Other Home sorts:
  - Continue Playing, Friends List, Sponsored, Curated Sorts
  - **Standout Games**: hand-curated "novel games… unique and in-depth gameplay mechanics, distinctive visual styles, or… underrepresented genre"
  - **Live Events**: limited-time quest events — [Discovery](https://create.roblox.com/docs/discovery)
- Today's Picks evolved into Standout Games. Creators submit via the Curation team's nomination form. — [DevForum 4502571](https://devforum.roblox.com/t/how-we-are-improving-home-this-year/4502571) (search summary)
- **Search:** semantic search across all officially supported languages for natural-language queries like "food games". — [Discovery](https://create.roblox.com/docs/discovery)
- Description guidance: summarize the game in the first sentence and include relevant keywords. "Avoid repeating keywords or adding irrelevant keywords. This may result in demotion." — [Docs: Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places)
- **Discover / Charts:** top and trending sorts were redesigned. — [Discovery](https://create.roblox.com/docs/discovery); [DevForum 2954676](https://devforum.roblox.com/t/testing-an-enhanced-discover-page-top-charts-and-new-sorts/2954676) (2024, older)
- **Game details page:**
  - Keep Experience Events current, maintain Groups, and add passes and subscriptions.
  - The page shows "similar games".
  - An accurate gameplay video "helps set the right expectations". — [Discovery](https://create.roblox.com/docs/discovery); [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- **Experience Events:**
  - Up to 5 event thumbnails plus a primary event type.
  - Players click "Notify Me" to get stream and push notifications when the event starts.
  - **Update announcements** are limited to **60 characters** and **once every three days**. They are tracked by visit rate and unfollow rate. — [Discovery](https://create.roblox.com/docs/discovery); [Docs: Experience events](https://create.roblox.com/docs/production/promotion/experience-events)
- **Experience notifications:**
  - Sent server-side to opted-in users, with optional `launchData` (max 200 bytes).
  - The in-game opt-in prompt `ExperienceNotificationService:PromptOptIn()` is available for users **13+**.
  - A user who saw the prompt can't be re-prompted within **30 days**. — [Docs: Experience notifications](https://create.roblox.com/docs/production/promotion/experience-notifications)
- **Thumbnails:**
  - 16:9, ideally **1920×1080**, under 3 MB; up to **10** images or videos on the details page.
  - Video uploads have a quota of **3/month**. Rejected videos count against it.
  - Videos may not use voice-over or lyrics, misrepresent gameplay, or show promo text like "50% off" / "Free UGC!". — [Docs: Thumbnails](https://create.roblox.com/docs/production/publishing/thumbnails)
- **Thumbnail personalization (built-in Home A/B):**
  - Activate **2–5** Home thumbnails.
  - In testing it gave "+8.5%" average qualified PTR, with "some games… +50%".
  - Keep several active rather than picking a single winner.
  - Test new sets with each major update, then leave them unchanged until the next update.
  - A performance table (impressions, qualified plays) populates after a few hours. — [Docs: Thumbnails](https://create.roblox.com/docs/production/publishing/thumbnails)
- Reusing your own old thumbnails or icons (including across your group network) "shouldn't negatively affect discoverability". — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- **Icons:** square, at least **512×512**. They scale down to about **150×150**, so preview them small. — [Docs: Experience icons](https://create.roblox.com/docs/production/publishing/experience-icons)
- **Social and invites:**
  - Invite prompts (`SocialService:PromptGameInvite`), a referral system, share links (trackable in the acquisition dashboard) and social media links are all documented promotion tools.
  - Co-play through join, invites and private servers feeds an RFY signal. — [Docs: Promotion index](https://create.roblox.com/docs/production/promotion); [Discovery](https://create.roblox.com/docs/discovery)

### Inferences
- For a small team the cheapest high-leverage moves are:
  - Ship 3–5 distinct, accurate Home thumbnails at launch and on each update.
  - Prompt notification opt-in after a positive moment, once per 30 days.
  - Schedule an Experience Event for each update and use the once-per-3-days announcement slot.
  - Apply to Standout Games only if the game is genuinely novel.

### Gaps
- No public numbers on traffic share by surface (e.g., % from Search vs. RFY).
- No official icon CTR guidance beyond size.
- Sponsored Takeovers pricing isn't public.

## 3. Ads Manager (Sponsored, Search ads, Rewarded video, ad credits, RFY interaction)

### Takeaway
Ads appear on Home and Search together.
- **Objectives:** Plays (seeds retrieval), Earnings (ROAS) and Engagement (buys progress toward the Kids/Select threshold).
- **Official CPP benchmarks (Nov 2025):** about $0.007–0.019 per play.
- **Agency figures:** much higher, around $0.45 CPP.
- **Attribution:** ad-acquired users never count toward RFY ranking, so RFY impressions can dip after ads. Roblox says this is not a penalty.

### Cited Findings
- **Objectives:**
  - **Plays**: "testing new ideas with a wide audience, or want initial traffic to help recommendation systems learn what's working and qualify your game for Recommended For You".
  - **Earnings**: players likely to spend; reports **ROAS**.
  - **Engagement**: "age-checked highly engaged players whose sessions count toward your highly engaged player threshold for Roblox Kids and Select". It has a higher CPP and does not auto-pause at the threshold. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Bidding:** auto-bidding; "If your game is engaging for users, you can get even better performance through ads system discounts." The first 24 h is a learning phase. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Placement and creatives:**
  - Campaigns show automatically on **both Home and Search results**.
  - Up to **10 thumbnails** per campaign, evenly rotated, 16:9.
  - An AI generator makes 3 variations from a text prompt; there's an asset library.
  - Advanced targeting covers location, age, gender, genre and device.
  - Clone-like games "might not be effective" as campaigns. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Launch data:** can be attached to campaigns to tailor onboarding, e.g. a tutorial for New Players or "Welcome back" for Lapsed users. It's visible in the URL and shareable. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Payments and ad credits:**
  - Requires age 13+ and a verified email. Cards are for 18+ only, with a $1 verification hold.
  - First-time card campaigns are charged $5 upfront.
  - Billing runs on a rising threshold (e.g. $100) or monthly.
  - Any 13+ user can convert Robux to **ad credits** (minimum 1 credit; irreversible). Robux earned at the U.S. 18+ rate converts first.
  - Unused credits are refunded at campaign end; auto-reload is available.
  - Fraud review happens 14 days after a campaign ends, with refunds at 16 days. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Attribution windows:**
  - New users: plays and spend credited to the ad for **30 days**.
  - Resurrected users (≥7 days lapsed): credited for **7 days**.
  - Reporting can lag up to **48 h**. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Search ads:**
  - Up to **10 keywords** per Ad Set, exact match, shown at the top of results (after the exact-title tile).
  - No audience targeting; they reach all regions, ages 13+ and all devices.
  - Separate keyword auction. — [Docs: Search ads](https://create.roblox.com/docs/production/promotion/search-ads)
- **Official cost benchmarks (DevForum, Nov 2025; older than 2026):** average cost-per-play **$0.0073 Maximize Plays, $0.0113 Drive Retention, $0.011 Reactivate Users, $0.0187 Acquire New Users**. Roblox notes these "may vary based on your game and user base size". The same update combined Home + Search and sunset the classic flow. — [DevForum 4084863](https://devforum.roblox.com/t/ads-manager-updates-home-search-combined-new-benchmarks-and-sunsetting-the-classic-flow/4084863) (search summary). Objective names have since changed to Plays/Earnings/Engagement per current docs.
- **(3rd-party, BLOXG agency, Mar 2026, 850+ promoted games):** Sponsored Experiences average CPP **$0.45**, average CPC **$0.25**, Immersive Ads CPM **$3.50**, and an "average Roblox Ads CPM" of $6.50, which is internally inconsistent. These figures are commercially motivated and diverge about 50× from the official CPP. — [BLOXG Advertising Benchmarks](https://bloxg.com/statistics/roblox-advertising-benchmarks)
- **Ads vs. RFY (official):**
  - "Engagement, retention, and monetization from users acquired through ads are excluded from RFY ranking signals."
  - An ad-acquired user "will generally not subsequently see your game in RFY", so "RFY impressions dip even while total acquisition increases". This is "not an ad penalty".
  - Sponsored tiles are blended into RFY and labeled. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Official worked example: 10k daily players from 25k RFY impressions, plus 5k from 20k Sponsored impressions, gives 15k. RFY traffic holds as long as RFY-cohort behavior is unchanged. — [Discovery](https://create.roblox.com/docs/discovery)
- **Rewarded video ads (monetization side):**
  - 6–30 s full-screen ads with the reward as a **developer product**; randomized rewards are not allowed.
  - Recommended reward value is **3–10 Robux**.
  - Eligibility: 13+, ID-verified, public game with **≥2,000 unique visitors/month**.
  - Earnings = EPM × impressions.
  - Gate with `AdService:GetAdAvailabilityNowAsync(Enum.AdFormat.RewardedVideo)`. — [Docs: Rewarded video ads](https://create.roblox.com/docs/production/promotion/rewarded-video-ads)

### Inferences
- Run a small **Plays** campaign at launch purely to clear retrieval and test thumbnails. At official CPP of about $0.01, $50–100 buys thousands of plays.
- Judge success by RFY-cohort signals in the Home Recommendations tab, not by ad-cohort retention.
- Use **Engagement** campaigns as a budgeted path to the 250-player Kids/Select threshold (see section 7).

### Gaps
- No official 2026 CPM/CPC/CPP update was found.
- No public EPM figures for rewarded video.
- Search-ad keyword prices aren't published.

## 4. Benchmarks seen in practice

### Takeaway
The most defensible broad benchmarks are GameAnalytics' 2026 report on 500+ games with ≥1M MAU:
- median D1 **10.3%**, D7 **1.6%**, D30 **0.5%**
- median session **9.8 min**
- platform payer share **3.8%**
- median ARPPU **$0.70**

Agency "D1 20%/30%/40%" bands describe promoted, successful games and are aspirational. Roblox itself only provides per-game similar-game benchmarks in Creator Analytics.

### Cited Findings
- **Official:** Creator Analytics compares your game against a "set of similar games" listed on the page. Benchmarks "do not impact the Recommended for You algorithm in any way", and the benchmark group changes as your game scales. — [Discovery](https://create.roblox.com/docs/discovery); [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- **Official:** Roblox advises getting session time and **D1 retention** "comparable or above your similar game benchmarks", and the same for payer conversion and ARPPU. — [Docs: Acquisition](https://create.roblox.com/docs/production/analytics/acquisition)
- **Official spender segments:** within-game percentiles (Top 15%, Intermediate 35%, Casual 50%, Lapsed, Never). Platform "Active" spenders have spent **≥$9.99 on Roblox in the last 60 days**. — [Docs: Analytics dashboard](https://create.roblox.com/docs/production/analytics/analytics-dashboard)
- **(3rd-party) GameAnalytics 2026 Roblox Benchmark Report** (500+ titles with ≥1M MAU, Aug 1 2025–Jul 31 2026):
  - D1 median 10.3% (p25 8.4%, p99 22.2%)
  - D7 median 1.6% (p25 1.0%, p99 9.1%)
  - D30 median 0.5% (p25 0.3%, p99 4.7%)
  - Session length median 9.8 min, p75 12, p90 14.7, top 5% 16.6, top 1% 21.1
  - ARPPU median $0.70, top 10% $2.33, top 5% $4.80, top 1% $55.31
  - 3.80% of players paid anything over the year (vs. 4.2% two years earlier); median payer spent $0.81 over the year
  - GA says the common "20% good / 40% excellent" D1 claims come from small samples of promoted games, and that including sub-1M-MAU games would lower all metrics. — [GameAnalytics 2026 report](https://www.gameanalytics.com/reports/2026-roblox-report); [Mellow/gamedevreports summary](https://gamedevreports.substack.com/p/gameanalytics-key-roblox-and-roblox-game) (search summary; full report not fetched)
- **(3rd-party, BLOXG agency, promoted-game sample):** D1 "Good 20%, Great 30%, Excellent 40%+"; genre D1 e.g. Simulator 32%, Obby 18%. — [BLOXG retention benchmarks](https://bloxg.com/statistics/roblox-retention-benchmarks). This conflicts with GameAnalytics medians.
- **Platform scale (official IR):**
  - Q2 2026: DAU about **123M** (+~10% YoY), revenue $1.47B (+36%), bookings +8% at the low end of guidance, average bookings per DAU about $12.66.
  - Q3 2026 bookings guided to $1.58–1.65B (−14% to −18% YoY).
  - KPIs are "subject to methodological refinements for bot mitigation and age verification".
  - Q3 2026 results were not yet published as of Oct 22, 2026. — [Roblox Q2 2026 earnings 8-K](https://www.sec.gov/Archives/edgar/data/0001315098/000162828026051059/ex991-robloxq22026earnin.htm) (search summary)
  - A secondary outlet reported "152M DAU / 29B hours" for Q2. This **conflicts** with the 123M figure and is unverified. — [Outlook Respawn](https://respawn.outlookindia.com/gaming/gaming-news/roblox-q2-2026-revenue-soars-36-to-15b-despite-bookings-miss)

### Inferences
- Reasonable small-team targets, using GameAnalytics as the floor:
  - D1 ≥ 10% (median), stretch 15–22%
  - D7 ≥ 2–3%
  - average session ≥ 10–12 min
  - payer conversion of a few % per game
- Use the in-dashboard similar-game benchmark as the primary yardstick, since that is what Roblox compares against.

### Gaps
- No credible public **ARPDAU** benchmark was found.
- No public PTR or first-play-bounce benchmarks (only the in-dashboard ones).
- Dubit, Gamefam, Naavik, RoMonitor and Rolimons 2026 stats were not retrieved in this pass (fetch limits).

## 5. Practical launch playbook

### Takeaway
1. Get the 16+ age-checked trial audience to 250 highly engaged plays to unlock under-16 audiences (or pay the 50k Robux expedited fee).
2. Seed retrieval with cheap Plays ads plus creator and social traffic.
3. Let RFY test RFY cohorts.
4. Iterate onboarding and thumbnails per update.

Each meaningful update can trigger an explore spike, but updates must improve RFY-cohort signals or impressions settle back.

### Cited Findings
- **Pre-launch testing:**
  - Invite up to **10 similar-aged friends** to preview before public release.
  - For under-16 reach: ID or face verification, 2FA, a questionnaire rating of Minimal/Mild/Moderate, and a **1,000 Robux refundable publishing fee** *or* 2+ months of Roblox Plus/Premium.
  - The fee is refunded if the game "maintains **25 highly engaged players for 60 days**" without moderation. — [Docs: Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places); [Docs: Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select)
- **Evaluation for under-16 (new since 2026):**
  - The game first launches only to **age-checked users 16+**.
  - It must reach **250 unique plays by highly engaged age-checked users within 60 days**, judged on account age, play history and spend to exclude bots, and evaluated hourly.
  - It also gets a safety review. Progress shows in the **Audience Reach** dashboard.
  - Alternative: a **50,000 Robux refundable expedited review fee** for timed or off-platform launches, refundable after 90 days if the game keeps 25 highly engaged players. — [Docs: Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select); [Docs: Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places)
- Ads Engagement objective = "a more direct path" to that threshold. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)
- **Update cadence:** a content update can produce an explore spike of new RFY users. Expansion continues only if that cohort engages and monetizes. — [Discovery](https://create.roblox.com/docs/discovery)
- Quality status is "reclassified… with every update". — [Discovery](https://create.roblox.com/docs/discovery)
- Thumbnails: refresh the personalization set with each major update. — [Docs: Thumbnails](https://create.roblox.com/docs/production/publishing/thumbnails)
- **External:** Roblox suggests partnering with similar-game creators and with YouTube/Twitch influencers. Share links are trackable as an acquisition view. — [Docs: Acquisition](https://create.roblox.com/docs/production/analytics/acquisition); [Docs: Share links](https://create.roblox.com/docs/production/promotion/share-links)
- **(3rd-party, BLOXG agency):**
  - 8-week pre-launch: Discord + TikTok/YouTube devlogs; contact **20–40 creators** with early access; prepare 15–20 clips.
  - Launch day: stagger creator posts over hours alongside sponsored ads for a concurrent spike.
  - Micro-influencers (10K–50K followers) are claimed to give better ROI. — [BLOXG launch strategy](https://bloxg.com/guides/roblox-game-launch-strategy). This is commercially motivated and unverified.
- **(3rd-party) Dubit:** reported the June 2026 7→28-day retention-window change. — [Dubit](https://dubit.io/library/what-makes-a-new-roblox-game-take-off) (from background notes; not re-fetched)

### Inferences
Suggested sequence for a small team:
1. Private test with up to 10 friends.
2. Public 16+ soft launch with $50–200 in Plays ads plus 3–5 thumbnails.
3. Fix bounce under 60 s and 180 s using funnel events.
4. Run an Engagement campaign and creator pushes toward 250 engaged plays.
5. Unlock Kids/Select.
6. Ship a content update every 1–2 weeks with an Experience Event, announcement and new thumbnails.

Note that the 16+-only trial means early RFY cohorts skew older than the eventual core audience.

### Gaps
- No official data on how much impression lift a typical update generates.
- No verified CPMs for influencer deals.
- No official guidance on optimal update frequency.

## 6. Analytics and experimentation tools

### Takeaway
The Home Recommendations tab (Analytics → Acquisition) shows every RFY signal by window against similar-game benchmarks. Funnel, custom and economy events via AnalyticsService instrument the first 3 minutes. Built-in Experiments run 14–60-day A/B tests on configs, with D1/D7, playtime, ARPU and payer conversion as goal metrics.

### Cited Findings
- **Home Recommendations dashboard** (Creator Hub → Analytics → Acquisition → Home Recommendations):
  - Shows impressions and plays trends, plus signal charts per window D1, D2–7 and D8–28 with below-benchmark highlighting.
  - Diagnose the "most important" signals first, then co-play, qualified sessions and spend. — [Discovery](https://create.roblox.com/docs/discovery)
- The Creator Dashboard shows a **daily-updated banner** if a game has reduced exposure for quality reasons. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- **Custom events:**
  - Up to **100** custom events; tracking them unlocks the **Explore** page.
  - Up to **3 custom fields** (CustomField01–03).
  - Prefer custom fields over many event names because of tighter cardinality limits on names. — [Docs: Custom events](https://create.roblox.com/docs/production/analytics/custom-events); [Docs: Custom fields](https://create.roblox.com/docs/production/analytics/custom-fields)
- **Funnel events** (onboarding and shop funnels): repeated steps are ignored but still count toward the global rate limit. **Economy events** track currency sources and sinks. — [Docs: Funnel events](https://create.roblox.com/docs/production/analytics/funnel-events); [Docs: Economy events](https://create.roblox.com/docs/production/analytics/economy-events)
- **Experiments:**
  - Run for **14–60 days**, with up to **two variants + control** for in-game config experiments.
  - Matchmaking experiments allow up to 3 variants, recommend 100% rollout and split players equally.
  - Optional targeting by country, tenure or spender tier raises the minimum detectable effect.
  - Metrics: D1, D7, playtime, ARPU, ARPPU, payer conversion and session time. Playtime, payer conversion and ARPU update every 5 min in the first 24 h as "early harm" checks.
  - The configuration can't be edited after scheduling.
  - Roblox recommends simple 50/50 tests on large rollouts. — [Docs: Experiments](https://create.roblox.com/docs/production/experiments)
- Ads Manager reporting views: All, New, Recent (<7 d), Lapsed (7–29 d) and Resurrected (30+ d) users; ROAS for Earnings campaigns. — [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)

### Inferences
- With low DAU, the minimum detectable effect will be large. Small games should test big changes only (onboarding flow, first reward timing) and rely on the 5-min early-harm view to catch regressions.

### Gaps
- No rate-limit numbers were extracted for AnalyticsService (see event-types doc "Event tracking limitations").
- Whether Experiments can target only RFY-acquired users is not documented.

## 7. What reduces reach

### Takeaway
Reach is cut by:
- giveaway or monetary metadata
- metadata that mismatches gameplay
- clone metadata or place files (the first to add unique metadata wins, not the first created)
- keyword spam
- a missing custom thumbnail (zero RFY)
- a missing maturity questionnaire (restricted playability)
- sensitive-issue primary themes (16+ only, not recommended)

The 2026 age-tier system means new games reach under-16s only after the 250-engaged-play evaluation.

### Cited Findings
- **Limits on exposure:**
  - "Leading with giveaways" (e.g. "Robux! Play now!").
  - "Mismatched metadata and content" is "not recommended… and is less visible in search".
  - "Non-unique games" whose metadata or place files "closely resemble existing games" are not prioritized. — [Discovery](https://create.roblox.com/docs/discovery)
- **Clone rule:** "we're not prioritizing discoverability based on which game was first created. Rather we're making sure we highlight the game that first added the unique metadata and/or placefile." Enforcement uses models plus human review. — [Discovery FAQ](https://create.roblox.com/docs/discovery-faq); [DevForum 3299107](https://devforum.roblox.com/t/improving-user-experience-by-reducing-exposure-of-low-quality-content/3299107) (older, late 2024)
- Keyword repetition or irrelevant keywords "may result in demotion". — [Docs: Publish games](https://create.roblox.com/docs/production/publishing/publish-games-and-places)
- **Maturity labels:**
  - With no questionnaire, Roblox "automatically restricts the playability of the game… for all players".
  - "Content May Vary" = age-checked 16+ only.
  - Primary sensitive-issue themes = 16+ and not recommended.
  - Maturity info is used to recommend games on Home and Charts. — [Docs: Content maturity](https://create.roblox.com/docs/production/promotion/content-maturity)
- **Age tiers (rolled out from early June 2026):**
  - **Roblox Kids** (5–8; Minimal/Mild content)
  - **Roblox Select** (9–15, including self-declared 9+ until age-checked; up to Moderate)
  - **Roblox** (age-checked 16+)
  - Chat is off for self-declared accounts. — [Docs: Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select); [Roblox Newsroom, Apr 2026](https://about.roblox.com/newsroom/2026/04/introducing-roblox-kids-and-select-accounts)
- **Age-check penetration:** Q2 2026 is 57% global, about 70% U.S., 75% U.S. under-18. Chat is limited to age-checked users. — [Roblox Q2 2026 8-K](https://www.sec.gov/Archives/edgar/data/0001315098/000162828026051059/ex991-robloxq22026earnin.htm) (search summary)
- An April 2026 announcement cited ">50% global / 65% U.S. DAU" age-checked. — [Roblox IR, Apr 2026](https://ir.roblox.com/news/news-details/2026/Roblox-Introduces-New-Age-Based-Accounts-and-Expanded-Parental-Controls-for-Users-Under-16/default.aspx) (search summary)
- **Conflict:** BloxBot and a search summary mention "500 engaged players". The current official docs say **250 unique plays by highly engaged age-checked users in 60 days**. Use the docs. — [Docs: Kids and Select](https://create.roblox.com/docs/production/publishing/kids-and-select); [BloxBot](https://bloxbot.ai/guide/roblox-new-publishing-requirements-2026)
- Ads: Roblox "prevents surfacing games identified as clickbait or spam" in search ads. Clone-like games' campaigns "might not be effective". — [Docs: Search ads](https://create.roblox.com/docs/production/promotion/search-ads); [Docs: Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)

### Inferences
- Because chat and co-play depend on age checks, games aimed at younger players may see weaker co-play signals. This is an inference; no official data was found.
- Teams should complete the full maturity questionnaire and aim for Minimal/Mild/Moderate to keep the whole audience reachable.

### Gaps
- No public data on traffic changes for individual games after the June 2026 age-tier rollout.
- No public list of what triggers the "reduced exposure" banner beyond the documented categories.
