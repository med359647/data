# Roblox Game Monetization (as of October 2026)

> **Source note:** In this session, direct fetches of create.roblox.com, about.roblox.com, devforum.roblox.com and sec.gov failed (DNS/proxy). Instead I read the official Creator Hub docs from Roblox's public docs repo **github.com/Roblox/creator-docs**, which is the source of create.roblox.com/docs. I cloned it at commit `65621e8`, last committed **2026-10-21**, so those facts are current. Doc links below use the create.roblox.com URL for each page, and every one was read from that repo. Financial and benchmark figures come from web search snippets and are labeled. "3P" means a third-party estimate.

## 1. Monetization tools: what each one is, the rules, and what it pays

### Takeaway
The core toolkit has not changed: passes, developer products, subscriptions and private servers, with a 70% creator share. Five things changed in 2025–26:
- **Creator Rewards** replaced Premium Payouts (July 24, 2025).
- **Roblox Plus** replaced Premium for new sign-ups (April 30, 2026). It brings new creator incentives: subscriber referrals, private-server time pay, and a cut of Robux transfers.
- **Managed Pricing** combined regional pricing and price optimization, on by default for new items.
- **External "Listed" Shop surfacing** depends on a correct ProcessReceipt.
- **Cross-game developer product sales** were disabled on May 30, 2026.

### Cited Findings
**Passes and developer products (70/30)**
- The creator receives 70% of Robux spent; the other 30% is Roblox's Marketplace Fee. Robux must still go through DevEx to become cash. — [Creator Hub: Monetization overview](https://create.roblox.com/docs/get-started/monetization)
- A pass is a one-time purchase. A developer product can be bought repeatedly (currency, ammo, potions). Product prices run from 1 Robux to 1 billion Robux. — [Developer Products](https://create.roblox.com/docs/production/monetization/developer-products)
- Cross-game developer product sales were disabled on May 30, 2026. Roblox told developers who relied on them to switch to Robux transfers. — [Developer Products](https://create.roblox.com/docs/production/monetization/developer-products)
- Roblox shows **Listed** developer products and passes outside the game: on the homepage, in search, and on the post-Robux-purchase page. Developer products only appear there if ProcessReceipt is implemented correctly. Roblox audits this continuously and flags and delists broken products in Creator Hub › Monetization › Shop. Passes need no ProcessReceipt. — [Developer Products](https://create.roblox.com/docs/production/monetization/developer-products); [Shop](https://create.roblox.com/docs/production/monetization/shop)
- The in-game **Shop** can also surface Robux packages that bundle your items. Purchases made through Shop earn the standard rate. — [Shop](https://create.roblox.com/docs/production/monetization/shop)
- Store personalization APIs:
  - `RankProductsAsync` orders products per user. It has a strict rate limit, so call it once at join.
  - `RecommendTopProductsAsync` returns up to 50 likely buys. It returns nothing if the game has had no sales in the last 28 days.
  - — [Developer Products](https://create.roblox.com/docs/production/monetization/developer-products)

**Subscriptions (in-experience)**
- Subscriptions auto-renew monthly. A user can own all of a game's subscriptions at once; mutually exclusive tiers like Bronze/Silver/Gold are not supported. — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)
- **Priced in Robux:** minimum 49 Robux. Regional pricing is forced on. The creator earns 70% every month. The price can change only once every 60 days, and an increase needs 30 days' notice to users. Robux subscriptions cannot be refunded. — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)
- **Priced in local currency:** fixed tiers of $2.99, $4.99, $7.99, $9.99 and $14.99. The creator is paid in Robux at $0.01 = 1 Robux of the base price after platform fees: 70% in month 1, then **100% from month 2 on**. Example: a $5 subscription pays 350 Robux in month 1 and 500 Robux per month after that. Earnings are held for 30 days. The price cannot be changed, and deleting the subscription refunds all current subscribers. — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)
- Rules:
  - Benefits must be honored for the full term.
  - No extra tasks (such as social posts) can be required to unlock paid benefits.
  - Battle passes may be sold and marketed as subscriptions.
  - The game must not direct users to buy on another platform.
  - Ownership must be checked server-side with `GetUserSubscriptionStatusAsync`.
  - — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)

**Premium Payouts are gone; Creator Rewards replaced them**
- Engagement-Based Payouts (Premium Payouts) were deprecated on **July 24, 2025** and replaced by Creator Rewards. The old method paid from the share of Premium members' playtime, aggregated over 28 days. — [Engagement-based payouts](https://create.roblox.com/docs/production/monetization/engagement-based-payouts)
- **Daily Engagement Reward:** 5 Robux per Active Spender per day. To count, the Active Spender must play your experience for 10+ minutes that day, and it must be one of the first three experiences they launch that day.
  - An Active Spender has made at least $9.99 of Qualifying Purchases (Robux, Premium, or UGC subscriptions) in the last 60 days.
  - New and reactivated users don't count during their first 60 days.
  - — [Creator Rewards](https://create.roblox.com/docs/creator-rewards)
- **Audience Expansion Reward:** 35% revenue share on the first $100 of Qualifying Purchases a New or Reactivated user (lapsed 60+ days) makes anywhere on Roblox in their first 60 days.
  - The user must arrive through your Share Link, a direct link, or a search for the game name; it must be their first session that day; and they must play 10+ minutes.
  - The experience must average 100+ DAU for the following 60 days.
  - Requires an ID-verified creator account.
  - — [Creator Rewards](https://create.roblox.com/docs/creator-rewards)
- Rewards are paid as Earned Robux after a 60-day hold. Bots, teleport manipulation, alt-account farming and high chargeback rates lead to forfeits. Paid-access games are eligible. — [Creator Rewards](https://create.roblox.com/docs/creator-rewards)

**Roblox Plus (replaced Premium for new subscribers on April 30, 2026; $4.99/month, no Robux stipend; 3P news)**
- Launch date, price, stipend removal, and the end of Premium's 10% Robux bonus on May 30, 2026 are reported by third-party news. — [PlayToEarn](https://playtoearn.com/news/roblox-plus-launches-april-30-at-499-monthly-replacing-premium-with-discount-first-model); [PCGamesN](https://www.pcgamesn.com/roblox/plus-subscription)
- Plus subscribers get 10% off eligible purchases, rising to 20% from the third month. **Roblox pays the discount**, so the creator still earns 70 Robux on a 100-Robux item. The effective creator share of what the user actually pays is 78% at 10% off and 88% at 20% off. — [Roblox Plus](https://create.roblox.com/docs/production/monetization/roblox-plus)
- **Hard-coded UI prices will show the wrong price to Plus subscribers.** Read prices from `GetProductInfoAsync` or `GetDeveloperProductsAsync` instead; they return `PriceDiscountDetails`. — [Roblox Plus](https://create.roblox.com/docs/production/monetization/roblox-plus)
- **Plus referral:** a user who subscribes through your game's `PromptRobloxSubscriptionPurchase` earns you 250 Robux per month for their first 3 paid months, up to 750 Robux. Free trials don't count, and earnings have a 60-day hold. — [Roblox Plus](https://create.roblox.com/docs/production/monetization/roblox-plus)
- **Private servers:** Plus subscribers get paid private servers free. The creator earns up to 100 Robux per subscriber per month (70% of the server price, capped at 100) if the subscriber spent 60+ cumulative minutes in a server they own in your game over the 30 days before renewal, and that server is one of their top 5 across Roblox. — [Roblox Plus](https://create.roblox.com/docs/production/monetization/roblox-plus)
- **Robux transfers:** your game earns 10% of a transfer between Plus subscribers made through `PromptRobuxTransferAsync`. Transfers must be 10–500 Robux. The game's cut is DevEx-eligible, but the Robux the recipient gets are not. Handle receipts with `BindReceiptHandler` (RobuxTransferSender/Receiver). — [Robux transfers](https://create.roblox.com/docs/production/monetization/robux-transfers)
- The Help Center says parents can set monthly spending limits, and default transfer limits are 500 Robux/day and 1,000 Robux/month (from search summary). — [Roblox Parental Controls Overview](https://en.help.roblox.com/hc/en-us/articles/30428310121620-Parental-Controls-Overview)

**Private servers**
- Paid private servers are a monthly Robux subscription. **Changing the price cancels every active private-server subscription.** They can't be combined with paid access. Under-13s may be blocked from joining by their parental settings. — [Private servers](https://create.roblox.com/docs/production/monetization/private-servers)

**Paid access**
- **In Robux:** 25–1,000 Robux, one-time payment. Requires an account at least 30 days old with a verified email. Earnings are held in escrow up to 7 days. No refunds. Not available on Xbox and can't be combined with private servers. — [Paid access in Robux](https://create.roblox.com/docs/production/monetization/paid-access-robux)
- **In local currency (paid in cash through Tipalti, not DevEx):**
  - Creator share by price tier: $9.99 → 50%, $29.99 → 60%, $49.99 → 70%, minus taxes and VAT.
  - Users have 48 hours to request a refund.
  - Earnings are held 60+ days and paid monthly.
  - Can only be bought on desktop or web.
  - Unavailable to buyers in AR, CN, CO, IN, ID, RU, TW, TR, UAE, UA and VN.
  - Requires an ID-verified creator aged 13+.
  - Has an optional **demo mode**.
  - Cannot paywall parts of the game behind extra Robux, though in-game passes and products are allowed.
  - — [Paid access in local currency](https://create.roblox.com/docs/production/monetization/paid-access-local-currency)

**Ads: immersive ads and rewarded video**
- Publisher eligibility:
  - The game is public.
  - The creator is 13+, ID-verified, and has 2FA on.
  - The Maturity & Compliance Questionnaire has been approved.
  - The game has **2,000+ unique visitors per month**.
  - — [Immersive ads](https://create.roblox.com/docs/production/monetization/immersive-ads)
- How immersive ads pay:
  - Click-to-play video pays per 15-second view.
  - Autoplay video pays per impression (0.5s on screen, 1.5% of the viewport).
  - Image ads pay per 1-second impression.
  - Portal ads pay per completed teleport.
  - Payment arrives on the 25th of the following month.
  - Use `PolicyService.AreAdsAllowed` to hide ad units from ineligible users.
  - — [Immersive ads](https://create.roblox.com/docs/production/monetization/immersive-ads)
- **Rewarded video:**
  - Full-screen ad of 6–30 seconds.
  - The reward must be a **developer product**. It cannot be Robux or a random item.
  - Roblox recommends rewards worth 3–10 Robux, placed in lobbies or at natural breaks.
  - Earnings = EPM × impressions.
  - Uses `AdService:GetAdAvailabilityNowAsync`, `CreateAdRewardFromDevProductId` and `ShowRewardedVideoAdAsync`, and is granted through ProcessReceipt.
  - — [Rewarded video ads](https://create.roblox.com/docs/production/promotion/rewarded-video-ads)
- Roblox does not publish an EPM. One third-party site claims a $6–12 eCPM and 5–15% of game revenue; this is unverified. — [rolearn.dev (3P)](https://rolearn.dev/insights/rewarded-video-ads-new-revenue-stream)
- Rewarded video launched with Google in April 2025. Roblox plans a no-code Studio plug-in in Q4 2026. — [MediaPost](https://www.mediapost.com/publications/article/417959/roblox-plans-expanded-placement-options-for-rewar.html); [eMarketer](https://www.emarketer.com/content/roblox-expands-rewarded-video-tools-creators-advertisers)

**Commerce (physical goods through Shopify)**
- Creator requirements:
  - Must be 18+.
  - Must link a Shopify store.
  - Only US users can buy: 13+ in most states, 18+ in Texas.
  - Up to 500 products per game.
  - — [Commerce products](https://create.roblox.com/docs/production/monetization/commerce-products)
- Bundling a digital item with a physical product requires either 100k+ average DAU and more than 1M Robux average monthly earnings over 90 days, or a $50k+ ad-spend agreement. The bundled item must be new, not Robux or in-game currency, and not random. — [Commerce products](https://create.roblox.com/docs/production/monetization/commerce-products)

**UGC avatar items sold in-game**
- When a Marketplace item sells inside a game, the item creator gets 30%, the **game owner gets 40%** (affiliate share), and Roblox keeps 30%. If you sell your own UGC in your own game you collect 70%. — [Monetization overview](https://create.roblox.com/docs/get-started/monetization); [Marketplace fees](https://create.roblox.com/docs/marketplace/marketplace-fees-and-commissions)
- Costs: upload fee of 80 Robux per item (500 with an emissive mask), plus a refundable publishing advance; the docs table shows 13,000. — [Marketplace fees](https://create.roblox.com/docs/marketplace/marketplace-fees-and-commissions)

**Managed Pricing (regional pricing plus price optimization)**
- One opt-in covers both. **New games and new items are enrolled by default.** Subscriptions, private servers and developer servers are regionalized automatically. — [Managed pricing](https://create.roblox.com/docs/production/monetization/managed-pricing)
- Regional prices fall between **30% and 100%** of the default price. They are based on economic location, which accounts for VPN use, billing history and account history. Passes are enabled by default. Developer products require dynamic pricing plus `GetUsersPriceLevelsAsync`, which returns a level from 1 to 1000, to guard trades and gifts against arbitrage. — [Regional pricing](https://create.roblox.com/docs/production/monetization/regional-pricing)
- In early 2025 tests, regional pricing raised the share of users spending by about 17% in Mexico, 26% in Brazil and 52% in the Philippines (Roblox, top games only). — [Roblox newsroom, April 2025](https://about.roblox.com/newsroom/2025/04/roblox-launches-regional-pricing-for-in-experience-items)
- How price optimization tests work:
  - The game needs about **60,000 transactions in 30 days** to qualify.
  - A test runs about 3 weeks and splits users into price cohorts.
  - New prices are applied only if total revenue rises.
  - Tests re-run automatically at least every 90 days.
  - Covers passes and developer products only.
  - **Hard-coded prices break it.** Use the Dynamic Price Check tool (price-pinned or location-pinned test accounts) to find them.
  - — [Price optimization](https://create.roblox.com/docs/production/monetization/price-optimization)

### Inferences
- A small new game will not qualify for price optimization (60k transactions/month) or Audience Expansion until it is past roughly 100 DAU. It can still use regional pricing, ads (once it has 2k monthly visitors), Plus referrals and Daily Engagement rewards from the start.
- Write every price label through `GetProductInfoAsync` from day one. Regional pricing, Plus discounts and price tests all depend on dynamic prices.
- Local-currency subscriptions are the best-paying recurring tool after month 1: 100% of $0.01/Robux, versus 70% for Robux-priced subscriptions.

### Gaps
- Roblox publishes no EPM or CPM for ads.
- Whether Plus bundles that include Robux have launched could not be confirmed.
- I couldn't fetch the DevForum announcement texts directly.

## 2. Revenue math: fee split, DevEx, and net USD

### Takeaway
On the standard rate, every 1,000 Robux a player spends on your pass or product becomes **700 earned Robux → $2.66**. That is about 27% of what a web buyer paid and about 21% of what a mobile buyer paid. The U.S. 18+ rate raises it to $3.78 for qualifying purchases.

### Cited Findings
- **DevEx standard rate: $0.0038 per earned Robux** ($114 per 30,000), in effect since September 5, 2025 at 10am PT. Robux earned before then cash out first at the old $0.0035 rate. — [DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange)
- **U.S. 18+ rate: $0.0054 (+42%)**, effective June 8, 2026. All of these conditions must hold:
  - The purchase is a developer product, pass, subscription or private server.
  - The buyer is a U.S. player age-verified as 18+ by face estimation or government ID.
  - The game qualifies on characters: **R15-only** with no R6 at any point, or custom human characters with enough articulation, or non-human or no-character games.
  - Roblox runs background compliance checks. Group payouts take the 18+ portion first.
  - — [U.S. 18+ exchange rate](https://create.roblox.com/docs/production/monetization/18-plus-devex-rate); [Roblox newsroom, April 2026](https://about.roblox.com/newsroom/2026/04/roblox-fuels-high-fidelity-games-over-18-players-increases-qualifying-devex-rate-42)
- **DevEx eligibility:**
  - Age 13+.
  - 30,000 Earned Robux minimum.
  - Verified email, a DevEx portal account (Tipalti), and a W-9 or W-8 form.
  - Full compliance with the ToS and Community Standards.
  - One completed cash-out per calendar month.
  - Processing takes about 10 business days the first time and about 5 after that.
  - **Premium or Plus is not listed as a requirement**, although some third-party guides say it is.
  - — [DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange)
- Earned Robux excludes Robux that were bought, stipends, trading or resale, Robux received by transfer, gift cards, and passes on template games with no real visits. — [DevEx](https://create.roblox.com/docs/production/monetization/developer-exchange)
- **Robux purchase prices (3P, consistent across guides):**

  | Price | Web | Mobile |
  |---|---|---|
  | $4.99 | 500 | 400 |
  | $9.99 | 1,000 | 800 |
  | $19.99 | 2,000 | 1,700 |
  | $49.99 | 5,250 | 4,500 |
  | $99.99 | 11,000 | 10,000 |

  — [Gamsgo](https://www.gamsgo.com/blog/robux-prices); [Epinpay](https://www.epinpay.com/en/blog/robux-price-cost-per-dollar-guide)
- **Platform level (Q2 2026):**
  - DevEx fees were $363M, up 15% year over year, which Roblox ties to the September 2025 rate increase (official 8-K, quoted in search).
  - Bookings were about $1,557M, up 8% (3P).
  - DAU was 123M.
  - Bookings growth slowed because monetization per hour fell, mainly among younger cohorts in the U.S. and Canada.
  - — [Roblox Q2 2026 8-K](https://www.sec.gov/Archives/edgar/data/0001315098/000162828026051059/ex991-robloxq22026earnin.htm); [Aardvark Labs](https://research.aardvarklabs.co/research/rblx/earnings/2026-q2/rblx-2026-q2-recap); [Music Ally](https://musically.com/2026/07/31/roblox-ended-q2-2026-with-123-million-daily-active-users/); [Shareholder letter PDF](https://s27.q4cdn.com/984876518/files/doc_financials/2026/q2/Roblox-Q2-2026-Earnings-Shareholder-Letter.pdf)
- ABPDAU was about $12.66 per quarter (3P; another source says $13.35, which is likely a mislabel). Monthly unique payers were about 27M (3P, unconfirmed). — [Aardvark Labs](https://research.aardvarklabs.co/research/rblx/earnings/2026-q2/rblx-2026-q2-recap); [Quartr](https://quartr.com/events/roblox-corporation-rblx-q2-2026_ozGBeOYG)

### Inferences (worked math using the official rates above)
- **Per 1,000 Robux spent on your item:** you earn 700 Robux, which is $2.66 at the standard rate or $3.78 at the U.S. 18+ rate. Per 1,000 earned Robux, that is **$3.80 standard or $5.40 U.S. 18+.**
- **Share of the player's dollar:** a web buyer pays about $9.99 per 1,000 Robux, so you keep about 26.6%. A mobile buyer pays about $12.49 per 1,000, so you keep about 21.3%. This matches third-party estimates of "roughly a quarter."
- **Local-currency subscription at $4.99:** about 350 Robux in month 1 (≈ $1.33), then about 500 Robux per month (≈ $1.90/month). That is about 38% of the price from month 2, versus about 27% for a Robux subscription. These are approximations: the docs say "after platform fees" without defining the base.
- **Paid access in local currency at $49.99:** about $35 before tax, paid in cash and not through DevEx. That is the best per-sale rate on the platform, but it limits reach.
- **Creator Rewards:** 5 Robux ≈ $0.019 per qualifying Active Spender-day. 1,000 such users a day ≈ $570 a month.
- **Plus referral:** 750 Robux ≈ $2.85 per converted subscriber.
- **DevEx minimum:** 30,000 Robux ($114) means about 42,900 Robux of player spend before the first cash-out.
- **Platform average:** $363M in DevEx ÷ (123M DAU × 91 days) ≈ **$0.032 in DevEx per DAU per day**, or about **$32 per 1,000 DAU per day** (~$970/month). Bookings are about $0.139 per DAU-day. This is an average across all experiences and is heavily skewed toward hits, so a median game will earn much less.

### Gaps
- Roblox's own current Robux price table could not be retrieved.
- The exact definition of the local-currency subscription conversion ("base platform price ... after platform fees") is not spelled out in the docs.

## 3. Benchmarks: conversion, ARPPU, ARPDAU, genre, whales

### Takeaway
Roblox publishes definitions but no genre benchmarks. Third-party figures cluster around 1–4% daily payer conversion and roughly $0.01–$0.15 ARPDAU, with simulators at the top and obbies at the bottom. Spending is highly concentrated. Treat every figure here as directional only.

### Cited Findings
- Roblox's definitions: conversion = % of DAU who pay; ARPPU = average revenue per paying user; ARPDAU = conversion × ARPPU. "A high ARPPU and low ARPDAU suggest revenue comes from a limited user subset." — [Monetization analytics (official)](https://github.com/Roblox/creator-docs/blob/main/content/en-us/production/analytics/monetization.md)
- The price optimization dashboard reports ARPPU and paying users. Creator Rewards shows 50th–90th percentile benchmarks against similar experiences for "daily rewarded active spender %". This is the only official peer benchmark available to creators. — [Price optimization](https://create.roblox.com/docs/production/monetization/price-optimization); [Creator Rewards](https://create.roblox.com/docs/creator-rewards)
- **3P ARPDAU by genre** (Bloxg, 2026, "850+ promoted games"): simulator $0.08, RPG $0.06, tycoon $0.05, horror $0.03, obby $0.01. It is unclear whether this is gross spend or creator net. — [Bloxg](https://bloxg.com/statistics/roblox-game-revenue-statistics)
- **3P conversion:** community postmortems give about 4.0% for simulators, 2.5% for RPGs, 1.5% for shooters and 0.8% for obbies. Another source says 1–3% on average and about 8% for top titles. — [CalculatorsUniverse](https://calculatorsuniverse.com/blog/roblox-game-revenue-genre-conversion-explained); [zehn-studio26 glossary](https://zehn-studio26.com/glossary/conversion-rate/)
- **Whales (GameAnalytics 2026, tracked games only):** the top 1% of payers spend about $86.36 a year, more than 4× the 95th percentile. GameAnalytics' 2023 report found over half of payers spent under $1 a year. — [GameAnalytics 2026 Roblox report](https://www.gameanalytics.com/reports/2026-roblox-report)
- **Creator distribution (3P coverage of Roblox data):** creators earned about $1.7B over the past year, the top 10 averaged about $65M each, and the 2024 median creator earned $1,575. — [TechSpot](https://www.techspot.com/news/113855-roblox-top-creators-making-65-million-year-while.html)

### Inferences
- Planning template: monthly creator USD ≈ DAU × conversion × daily ARPPU in Robux × 0.7 × 0.0038 × 30. Example: 1,000 DAU × 2% × 150 Robux × 0.7 × 0.0038 × 30 ≈ $239 a month, plus Creator Rewards and ads. All inputs are assumptions; replace them with your own analytics after launch.
- If the third-party ARPDAU figures are gross player spend, a simulator at $0.08 means about $2.1 of creator DevEx per 1,000 DAU per day (×0.266). The platform average is $32 per 1,000 DAU per day (section 2). The two can't be reconciled from the sources, so plan conservatively.

### Gaps
- No Naavik, Deconstructor of Fun, Dubit or GameRefinery genre benchmark data was found.
- No reliable source gives the top-1% share of a game's revenue.

## 4. Design patterns that work, and their effect on discovery signals

### Takeaway
The Recommended For You (RFY) algorithm ranks on **"spend days per user"** and **"Robux spent per user"**, measured only on users who arrived organically from RFY. That rewards cheap, repeatable purchases spread over many days: consumables, daily-relevant boosts, subscriptions and battle passes. One-off big purchases help less. The breakout hits of 2025–26 used random-pet or brainrot collection, time-skips and cheap impulse consumables.

### Cited Findings
- RFY signals:
  - "Most important": play-through rate, first-play bounce rate (a negative signal), play days per user, and playtime per user (capped at 60 minutes per user per game per day).
  - "Important": intentional co-play days, qualified play sessions, **spend days per user**, and **Robux spent per user**.
  - Each is measured over D1, D2–7 and D8–28.
  - Only users who joined organically from RFY count. Users from ads, friends or search are excluded from ranking.
  - — [Discovery](https://create.roblox.com/docs/discovery)
- Discovery uses "explore and expand": if a new cohort engages and monetizes well, Roblox recommends the game to more cohorts like it. — [Discovery](https://create.roblox.com/docs/discovery)
- **Giveaway metadata penalty:** "Metadata that implies any type of monetary reward is not prioritized for recommendations." For example, a game titled "Robux! Play now!" gets less exposure. — [Discovery](https://create.roblox.com/docs/discovery); [Discovery FAQ](https://create.roblox.com/docs/discovery-faq)
- Rewarded video at natural breaks with a 3–10 Robux-equivalent reward ("Watch for 2x coins") is Roblox's own recommended pattern. — [Rewarded video ads](https://create.roblox.com/docs/production/promotion/rewarded-video-ads)
- Battle passes are explicitly allowed as subscriptions. — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)
- **Gifting and trading** under regional pricing should be gated with `GetUsersPriceLevelsAsync`. Example rules: let higher-price-level users gift down, and allow trades only between users at the same level. — [Regional pricing](https://create.roblox.com/docs/production/monetization/regional-pricing)
- **Donation and tip boards:** these can now use Robux transfers, which only Plus subscribers can send. The game earns 10%. — [Robux transfers](https://create.roblox.com/docs/production/monetization/robux-transfers)
- Premium and Plus perks should not paywall the game or give a "tactical gameplay advantage." This is Roblox's own best-practice guidance. — [Engagement-based payouts (legacy page)](https://create.roblox.com/docs/production/monetization/engagement-based-payouts)
- **Grow a Garden (3P analysis):** "Smart Friction" (inventory limits, rare seed scarcity), monetized through time-skips; estimated $12M+ a month at its May 2025 peak. Other trackers put it at about $1.75M a month more recently. — [TickerTrends](https://blog.tickertrends.io/p/rblx-escape-tsunami-brainrot-impact-analysis); [GameDaily](https://gamedaily.com/games/everything-about-grow-a-garden-the-cozy-idle-sim-revolutionizing-roblox-revenue); [RoWatcher](https://rowatcher.com/games/7436755782/grow-a-garden)
- **Steal a Brainrot (3P):** peaked at about 20M CCU in August 2025. It monetizes through cheap impulse consumables, power-ups and multiplier boosts. Estimated $2.0–3.5M a month (modeled). — [Wikipedia](https://en.wikipedia.org/wiki/Steal_a_Brainrot); [BloxPrices](https://www.bloxprices.com/stats/steal-a-brainrot/)
- Naavik argues that the Grow a Garden and brainrot wave "monetized far above anything Roblox could reasonably expect to repeat." — [Naavik digest](https://naavik.co/digest/robloxs-expensive-year-of-good-intentions/); [Naavik State of UGC Games 2026](https://naavik.co/deep-dives/the-state-of-ugc-games-2026/)
- **Blox Fruits (3P, single source):** estimated $50–100M a year, mainly from passes and Robux products. — [FourWeekMBA](https://fourweekmba.com/roblox-revenue/)

### Inferences
- A suggested shelf for a small team:
  - A 2x currency pass and a VIP pass (permanent).
  - Cheap consumables at 5–50 Robux (luck, speed, skips) to drive spend days.
  - A one-time starter pack, discounted, for first-session conversion.
  - Limited-time or event items for re-engagement spikes.
  - A battle pass sold as a subscription.
  - Rewarded-video boosts for non-payers.
  - A paid private server.
- Gacha, eggs and pets are high-yield but carry compliance overhead (section 5). Build the non-random fallback from the start.
- Trading drives engagement, but it requires price-level gating and an `IsPaidItemTradingAllowed` check.

### Gaps
- No primary-source breakdowns were found for the monetization of 99 Nights in the Forest, Dress to Impress or Adopt Me. No official per-game revenue exists; all game revenue figures are third-party models.

## 5. Policy limits

### Takeaway
Paid random items need full numeric odds disclosed before purchase, and they must be gated per user with PolicyService. They are blocked for under-18s in the UK and Australia, and for under-18s or unverified adults in Brazil (2026). The age-check rollout is shifting where spending comes from: older, verified users are worth more (U.S. 18+ rate), while younger cohorts' monetization per hour is falling.

### Cited Findings
- **What counts as a paid random item:**
  - Covers random outcomes bought with Robux, or with currency bought with Robux: capsules and eggs, random enhancements, combining items, and probability modifiers (luck boosts, **pity systems**, rate-ups).
  - Every outcome and its numeric percentage must be shown before purchase. Percentages must sum to 100%.
  - An "(i)" icon alone is not enough; it needs a word such as "Info" or "Details".
  - Odds must update dynamically when a luck boost is active, or when a one-per-user outcome has already been obtained.
  - Free rewards earned through gameplay need no disclosure.
  - — [Paid random items](https://create.roblox.com/docs/production/monetization/paid-random-items)
- **When `ArePaidRandomItemsRestricted` is true**, the game must do one of the following:
  - Offer an earnable, unpaid path.
  - Use a deterministic sequence that is disclosed in advance.
  - Sell outcomes directly at a price based on expected value (e.g. 10 Robux at 5% → 200 Robux).
  - Hide or block the item with a message.
  - Teleport the user out of the area.
  - Separately, if `IsPaidItemTradingAllowed` is false, the user cannot trade paid items.
  - — [Paid random items](https://create.roblox.com/docs/production/monetization/paid-random-items)
- **UK under-18s** have been restricted since August 2024 and **Australia** since September 2024. — [DevForum UK](https://devforum.roblox.com/t/update-on-paid-random-items-restriction-for-uk-users-under-18/3072183); [DevForum AU](https://devforum.roblox.com/t/update-on-paid-random-items-restriction-for-australian-users/3153602)
- **Brazil (ECA Digital law):**
  - Under-18s have been blocked since March 17, 2026; unverified 18+ users since March 31, 2026.
  - A game that declares paid random items but doesn't use PolicyService is made unplayable for Brazilian under-18s.
  - Roblox audits declarations.
  - — [Roblox Help: Brazil Digital ECA Updates](https://en.help.roblox.com/hc/cs/articles/48706630819476-Brazil-Digital-ECA-Updates); [Bloxy News](https://x.com/Bloxy_News/status/2034153291899408514)
- A DevForum thread titled "Clarifying Requirements for Paid Random Items" exists. A third-party summary says rules on odds and region-gating were tightened from May 26, 2026; this is unverified. — [DevForum](https://devforum.roblox.com/t/clarifying-requirements-for-paid-random-items/4654622?page=4); [ZehnStudio (3P)](https://zehn-studio26.com/news/paid-random-items-odds-disclosure/)
- **Subscription rules:** no scams or misleading offers, no gating paid benefits behind extra tasks, and no off-platform purchase links. Violating games are taken down. — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)
- **Refunds:**
  - No refunds for Robux paid access or Robux subscriptions.
  - Local-currency paid access can be refunded within 48 hours.
  - Deleting a local-currency subscription refunds all subscribers.
  - Developer product purchases that are never resolved are not refunded after escrow; they stay pending.
  - — [Paid access (Robux)](https://create.roblox.com/docs/production/monetization/paid-access-robux); [Paid access (local currency)](https://create.roblox.com/docs/production/monetization/paid-access-local-currency); [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions); [ProcessReceipt reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#ProcessReceipt)
- **Age (Q2 2026):** 57% of global DAU are age-checked (over 70% in the U.S. and Australia). Of those checked, 35% are under 13, 38% are 13–17 and 27% are 18+. Facial age checks have been required for chat since January 2026 (3P). — [Q2 2026 shareholder letter](https://s27.q4cdn.com/984876518/files/doc_financials/2026/q2/Roblox-Q2-2026-Earnings-Shareholder-Letter.pdf); [Anapol Weiss (3P)](https://www.anapolweiss.com/blog/roblox-just-changed-everything-what-parents-need-to-know-about-the-new-age-checks/)
- Parents can set monthly spending caps on under-13 accounts covering Robux and game subscriptions; gift cards are exempt. — [Parental Controls Overview](https://en.help.roblox.com/hc/en-us/articles/30428310121620-Parental-Controls-Overview)
- **Creator Rewards abuse rules:** no bots, no encouraging alt accounts, no impersonation, and no high chargeback rates. — [Creator Rewards](https://create.roblox.com/docs/creator-rewards)
- **Ad fraud:** Robux can be clawed back and games suspended. — [Immersive ads](https://create.roblox.com/docs/production/monetization/immersive-ads)

### Inferences
- I found no blanket rule banning the sale of gameplay advantage to under-13s. The relevant limits are per-region rules on random items, parental spending caps, and Roblox's guidance against pay-to-win Premium or Plus perks.

### Gaps
- I could not read the full Community Standards "Roblox economy" section directly. Whether 2026 brought further under-13 spending limits for in-experience purchases is unconfirmed.

## 6. Scripting basics: receipts and ownership

### Takeaway
Grant developer products only inside `ProcessReceipt`, or the newer `BindReceiptHandler`, never in `PromptProductPurchaseFinished`. Make the handler **idempotent** by keying on `PurchaseId`, and **save to DataStore before returning PurchaseGranted**. The same receipt can run on two servers at once, can be re-delivered, and can fail to record even after you return PurchaseGranted.

### Cited Findings
- Set `ProcessReceipt` **once, in one server Script**, and handle every product in it. If no callback is set, receipts are auto-acknowledged and lost. — [ProcessReceipt reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#ProcessReceipt)
- **When the callback is called:** on purchase, when the prompt shows success, and when the user joins a server. There is no timed retry. A `NotProcessedYet` receipt is only retried on the user's next purchase or rejoin. There is no timeout, so the callback may yield. — [ProcessReceipt reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#ProcessReceipt)
- **Pitfalls stated in the docs:**
  - The order of multiple pending receipts is non-deterministic.
  - The user must be in the server for the callback to fire.
  - **The same purchase may run on two servers at once** if the user hops servers.
  - The result may fail to record even after you return PurchaseGranted, leaving the purchase unresolved and due to be re-delivered.
  - — [ProcessReceipt reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#ProcessReceipt)
- `receiptInfo` contains: `PurchaseId` (unique per transaction), `PlayerId`, `ProductId`, `PlaceIdWherePurchased`, `CurrencySpent` (the actual price paid, including under price tests), `CurrencyType` and `ProductPurchaseChannel`. — [ProcessReceipt reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#ProcessReceipt)
- `PromptProductPurchaseFinished` firing **does not** mean the purchase succeeded; don't grant from it. Roblox keeps no per-user developer product history, so you must store your own. — [Developer Products](https://create.roblox.com/docs/production/monetization/developer-products)
- **`BindReceiptHandler(ReceiptType, handler, filter?)`** is the newer alternative. It supports a per-product filter or a catch-all, returns `Enum.ReceiptDecision.Processed/NotProcessedYet`, and falls through to `ProcessReceipt` if no bound handler matches. It is required for Robux transfer receipts. — [MarketplaceService.BindReceiptHandler](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#BindReceiptHandler)
- **Passes:**
  - Prompt with `PromptGamePassPurchase`.
  - Check with `UserOwnsGamePassAsync(userId, passId)`. The result is cached and refreshed when `PromptGamePassPurchaseFinished` fires.
  - A pass bought outside the game mid-session can take several minutes to show up.
  - It always returns true on the first join after a purchase.
  - — [UserOwnsGamePassAsync reference](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService#UserOwnsGamePassAsync); [Passes](https://create.roblox.com/docs/production/monetization/passes)
- Subscription ownership must be checked on the server (`GetUserSubscriptionStatusAsync`). Watch `Players.UserSubscriptionStatusChanged`, and revoke benefits when a subscription lapses. — [Subscriptions](https://create.roblox.com/docs/production/monetization/subscriptions)
- **Community-reported bugs:** duplicate grants on rejoin when the handler doesn't return a value if the player leaves mid-grant. A read-then-SetAsync dedupe is not atomic. — [DevForum: player keeps getting reward on rejoin](https://devforum.roblox.com/t/player-keeps-getting-developer-product-reward-when-rejoining/1700799); [DevForum: ProcessReceipt vs PromptProductPurchaseFinished](https://devforum.roblox.com/t/2462225)

### Inferences (recommended pattern, built from the guarantees above)
1. Look up the player. If they are not in this server, return NotProcessedYet.
2. Run one atomic `UpdateAsync` on the player's save key (or a session-locked profile, e.g. ProfileStore). In it:
   - If `PurchaseId` is already in the stored `processedReceipts`, return the data unchanged and treat the receipt as granted.
   - Otherwise apply the reward to the **saved data** and add the `PurchaseId`, trimmed to the last N entries.
3. Only after the save succeeds, update the in-memory/leaderstats values and return PurchaseGranted. If the save fails, return NotProcessedYet.
4. Wrap each step in `pcall`, and never yield the UI on it.
5. Use a handler table keyed by ProductId. An unknown ProductId should return NotProcessedYet and log, not grant.

**Common ways purchases get lost:**
- Granting in `PromptProductPurchaseFinished`.
- Setting `ProcessReceipt` in multiple scripts (the last one wins).
- Returning PurchaseGranted before the DataStore write.
- A handler that errors or returns nil.
- Hard-coded prices, which break regional pricing, Plus discounts and price tests.
- Changing a private-server price, which cancels all its subscriptions.
- Granting rewarded-video rewards outside ProcessReceipt.

### Gaps
- The official code sample `ProcessReceipt-Example` is not in the docs repo, so I couldn't quote Roblox's current exact sample.

## 7. Case studies (top grossers of 2025–26)

### Takeaway
Hard data is limited to third-party models. The common pattern: a simple, social, collectible loop, plus random collectible acquisition (seeds, pets, brainrots), plus time-skip and luck consumables, plus limited events. Revenue peaks are huge but decay fast.

### Cited Findings
- **Grow a Garden:**
  - About $12M in May 2025 (CreatorExchange via GameDaily, 3P).
  - Idle "patience" monetization with time-skips, plus scarcity of seeds and inventory space.
  - Recent tracker estimate about $1.75M a month (3P).
  - — [GameDaily](https://gamedaily.com/games/everything-about-grow-a-garden-the-cozy-idle-sim-revolutionizing-roblox-revenue); [TickerTrends](https://blog.tickertrends.io/p/rblx-escape-tsunami-brainrot-impact-analysis); [RoWatcher](https://rowatcher.com/games/7436755782/grow-a-garden); [Wikipedia](https://en.wikipedia.org/wiki/Grow_a_Garden)
- **Steal a Brainrot:**
  - About 20M peak CCU in August 2025.
  - Cheap impulse consumables and multipliers.
  - Volatile economy with admin-event rarities.
  - $1.4–3.5M a month (3P models).
  - — [Wikipedia](https://en.wikipedia.org/wiki/Steal_a_Brainrot); [BloxPrices](https://www.bloxprices.com/stats/steal-a-brainrot/); [RoWatcher](https://rowatcher.com/games/7709344486/steal-a-brainrot); [u4gm comparison (fan blog)](https://www.u4gm.com/grow-a-garden/blog-grow-a-garden-vs-steal-a-brainrot)
- **Blox Fruits:** $50–100M a year from passes and Robux products (single 3P source). — [FourWeekMBA](https://fourweekmba.com/roblox-revenue/)
- **Platform-level effect:** Roblox's Q2 2026 slowdown in bookings came from lower monetization per hour among younger U.S. and Canadian cohorts. A third-party summary says engagement shifted toward lower-monetizing games. — [Investing.com](https://www.investing.com/news/company-news/roblox-q2-2026-slides-bookings-growth-slows-to-8-amid-user-decline-93CH-4826401); [SQ Magazine](https://sqmagazine.co.uk/roblox-statistics/)

### Inferences
- The hits rely on random collectibles, which conflicts with the 2026 restrictions in the UK, Australia and Brazil. New games should ship odds UI and non-random fallbacks from day one.

### Gaps
- No reliable monetization breakdowns were found for 99 Nights in the Forest, Dress to Impress or Adopt Me. Their pass and product lineups would need first-hand inspection of each game's Store tab.
