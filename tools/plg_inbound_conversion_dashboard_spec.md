# Inbound Conversion Dashboard Spec

*Six-metric dashboard layout with data sources, visualization format, alert thresholds, and data pipeline requirements. Ready to hand to ops for implementation.*

| **DOCUMENT TYPE** | Companion Tool — PLG-to-Enterprise Playbook |
| --- | --- |
| **DERIVES FROM** | Tenet 9 — Metrics & Pipeline Hygiene |
| **AUTHOR** | Justin Nychay |
| **VERSION** | 1.0 │ April 2026 |

---

## Purpose

This dashboard answers three questions every week:

1. **Is the product funnel healthy?** — Are enough accounts signing up, activating, and growing to feed the sales motion? (Metrics 1–3)
2. **Is the sales overlay converting?** — Are reps successfully engaging PQAs and converting them to committed deals? (Metrics 4–5)
3. **Is the revenue base becoming more predictable?** — Is the ratio of committed ARR to total revenue improving over time? (Metric 6)

This sits alongside the standard Weekly CEO Dashboard, not replacing it. The CEO Dashboard covers total revenue, pipeline, and forecast. This dashboard covers the product-to-sales conversion engine that feeds it.

**When to build:** Days 61–75 of the 90-day implementation (Step 15), after the first Tier 1 cohort has produced observable conversion data to calibrate against.

---

## Dashboard Layout

The dashboard is organized as a single screen with two rows. Top row: product funnel health (metrics 1–3). Bottom row: sales conversion and revenue mix (metrics 4–6). Reading left to right follows the conversion flow: sign-ups → activation → PQAs → sales-engaged → committed → revenue mix.

```
┌─────────────────────────────────────────────────────────────────────┐
│                  PLG INBOUND CONVERSION DASHBOARD                  │
│                     Week of [date] — [date]                        │
├──────────────────────┬──────────────────────┬──────────────────────┤
│                      │                      │                      │
│   1. NEW SIGN-UPS    │  2. ACTIVATION RATE  │   3. PQA VOLUME     │
│   by source/segment  │                      │   & growth           │
│                      │                      │                      │
│   [stacked bar]      │  [single number +    │   [line chart +      │
│                      │   trend line]        │    single number]    │
│                      │                      │                      │
├──────────────────────┼──────────────────────┼──────────────────────┤
│                      │                      │                      │
│  4. PQA → ENGAGED    │ 5. ENGAGED →         │   6. REVENUE MIX    │
│  conversion rate     │ COMMITTED conv rate  │                      │
│                      │                      │                      │
│  [single number +    │  [single number +    │   [stacked area      │
│   trend line]        │   trend line]        │    chart]            │
│                      │                      │                      │
└──────────────────────┴──────────────────────┴──────────────────────┘
```

---

## Metric Specifications

### Metric 1: New Sign-Ups by Source and Segment

**What it answers:** Where are users coming from? Which sources produce users that eventually convert to committed revenue?

| Field | Specification |
| --- | --- |
| **Definition** | Count of new accounts created per week, segmented by acquisition source and account segment |
| **Primary data source** | Product analytics platform (Amplitude, Mixpanel, Heap) + UTM/attribution data from marketing |
| **Secondary data source** | CRM (if sign-up events are synced) for source attribution enrichment |
| **Update frequency** | Daily aggregation, weekly review |
| **Visualization** | Stacked bar chart — weeks on x-axis, bars segmented by source (organic, paid, referral, direct, partner). Color-coded by source. Include a 4-week trailing average line overlay. |
| **Segmentation** | By source (organic, paid search, paid social, referral, direct, partner, content). Filterable by account segment (corporate domain vs. personal email) to separate enterprise-potential sign-ups from hobbyists. |
| **Time range** | 12-week rolling view. Weekly bars with trailing 4-week average. |

**Alert thresholds:**
- **Yellow:** Weekly sign-ups drop below trailing 4-week average by more than 20%.
- **Red:** Weekly sign-ups drop below trailing 4-week average by more than 40%, or sign-ups from the highest-converting source drop more than 30%.

**What to do when the alert fires:** A sign-up decline is a product funnel problem, not a sales problem. Investigate: did a marketing campaign end? Did a product change break the onboarding flow? Did a competitor launch? Did a pricing page change increase friction? The answer determines whether this is a temporary dip or a structural change.

---

### Metric 2: Activation Rate

**What it answers:** Of the accounts that sign up, what percentage reach meaningful first usage? This is the most important product health metric — a sign-up that doesn't activate is not in the funnel.

| Field | Specification |
| --- | --- |
| **Definition** | Percentage of new sign-ups that complete the defined activation event within [X] days of sign-up. The activation event must be tied to the Leading Indicator of Retention — the specific behavior that predicts a user will still be active at 90 days. |
| **Primary data source** | Product analytics platform — requires a defined activation event instrumented in the product |
| **Update frequency** | Weekly (with a cohort lag — this week's activation rate reflects sign-ups from [X] days ago) |
| **Visualization** | Single large number (current week's rate) with a 12-week trend line below it. The number should be color-coded: green if above target, yellow if within 5% of target, red if below target. |
| **Cohort definition** | Weekly cohorts. Each cohort is measured at the same number of days post-sign-up for apples-to-apples comparison. |
| **Time range** | 12-week rolling cohort view. |

**Defining the activation event:** This is company-specific and must be determined during Week 1 of the 90-day implementation. The activation event should satisfy two criteria: (1) it predicts 90-day retention better than any other early behavior, and (2) it's observable within the first [X] days. Examples: first production API call (not sandbox), first integration connected, first team member invited, first workflow completed that produces an output the user values. If no activation event has been defined, this is a Week 1 priority — the metric is meaningless without it.

**Alert thresholds:**
- **Yellow:** Activation rate drops below 80% of the trailing 8-week average.
- **Red:** Activation rate drops below 60% of the trailing 8-week average, or below an absolute floor (company-specific — typically 15–25% for consumption products).

**What to do when the alert fires:** Activation rate declines are almost always product or onboarding problems. Investigate: did a product release change the onboarding flow? Did the sign-up source mix shift toward lower-intent channels? Is a specific step in the activation path showing increased drop-off? Segment by source — if paid sign-ups activate at 8% while organic activates at 30%, the problem is targeting, not product.

---

### Metric 3: PQA Volume and Growth

**What it answers:** Are enough accounts crossing the scoring threshold to feed the sales pipeline? This is where the product funnel meets the sales funnel.

| Field | Specification |
| --- | --- |
| **Definition** | Count of accounts crossing the PQA scoring threshold (from the Account Scoring Card) per week, plus the cumulative PQA pool that hasn't yet been engaged by sales |
| **Primary data source** | Data warehouse — scoring model query combining product analytics + enrichment data + billing system. Or product analytics platform if scoring is implemented there with custom events. |
| **Secondary data source** | CRM — to exclude accounts already in active sales engagement from the "unengaged PQA pool" count |
| **Update frequency** | Weekly |
| **Visualization** | Dual display: (1) Line chart showing new PQAs per week over 12 weeks with a target line overlay. (2) Single number showing total unengaged PQA pool — accounts that have qualified but haven't been contacted by sales yet. |
| **Time range** | 12-week rolling for the trend line. Cumulative for the pool. |

**Alert thresholds:**
- **Yellow:** New PQA volume drops below the pipeline arithmetic requirement for 2 consecutive weeks. (From the worked example: if you need 160 PQAs/year, that's ~3/week. Yellow fires at < 2/week for 2 weeks.)
- **Red:** New PQA volume drops below pipeline arithmetic requirement for 4 consecutive weeks, or cumulative unengaged PQA pool exceeds 3x weekly engagement capacity (meaning PQAs are being generated but not contacted — a sales capacity problem, not a funnel problem).

**What to do when the alert fires:** Low PQA volume means the product funnel isn't producing enough enterprise-ready accounts. Two root causes: not enough growing accounts (Metric 2 problem — activation or retention), or scoring thresholds are too tight (recalibrate the Account Scoring Card). High unengaged pool means sales isn't keeping up — either capacity is insufficient or the first touch motion isn't efficient.

---

### Metric 4: PQA-to-Sales-Engaged Conversion Rate

**What it answers:** Are reps successfully initiating conversations with PQAs? This is the handoff metric — where the product funnel becomes the sales funnel.

| Field | Specification |
| --- | --- |
| **Definition** | Percentage of PQA-qualified accounts where a sales rep has successfully initiated a conversation (defined as: first meeting held, or substantive email exchange — not just an outreach email sent) |
| **Primary data source** | CRM — requires PQA-qualified accounts to be routed into CRM with stage tracking. "Sales-engaged" is a defined CRM stage (S1 in the PLG sales process). |
| **Secondary data source** | Product analytics (for PQA qualification timestamp) to calculate time-to-engagement |
| **Update frequency** | Weekly |
| **Visualization** | Single large number (current trailing 4-week rate) with a 12-week trend line. Add a secondary metric: median days from PQA qualification to first sales engagement. |
| **Time range** | 12-week rolling. Trailing 4-week average smooths weekly volatility. |

**Alert thresholds:**
- **Yellow:** Conversion rate drops below 30% (trailing 4-week), or median time-to-engagement exceeds 14 days.
- **Red:** Conversion rate drops below 20% (trailing 4-week), or median time-to-engagement exceeds 21 days.

**What to do when the alert fires:** Low PQA-to-engaged conversion means one of three things: (1) the first touch isn't working — reps are reaching out but getting no response, which is a messaging or channel problem; (2) the PQA definition is too generous — accounts are crossing the threshold but aren't actually ready for a sales conversation, which means the Account Scoring Card needs recalibration; or (3) rep capacity — too many PQAs, not enough reps, and accounts age out before contact. The median time-to-engagement metric disambiguates: if time is long but eventual conversion is high, it's capacity. If time is short but conversion is low, it's targeting or messaging.

---

### Metric 5: Sales-Engaged-to-Committed Conversion Rate

**What it answers:** Are conversations converting to committed deals? This measures the effectiveness of the sales motion — discovery, business case building, pricing conversation, and procurement navigation.

| Field | Specification |
| --- | --- |
| **Definition** | Percentage of sales-engaged accounts (S1+) that convert to a committed deal (S6 — closed-won with committed contract) |
| **Primary data source** | CRM — deal pipeline stages from S1 (sales-engaged) through S6 (closed-won) |
| **Secondary data source** | Billing system — to validate that committed contracts are actually being invoiced and paid |
| **Update frequency** | Weekly pipeline review, monthly conversion rate calculation (deal cycles are longer than weekly) |
| **Visualization** | Single large number (trailing 90-day conversion rate) with quarterly trend. Add a secondary view: stage-by-stage waterfall showing where deals drop out (S1→S2 drop rate, S2→S3 drop rate, etc.) to pinpoint the breakdown point. |
| **Time range** | Trailing 90 days for the conversion rate (to smooth for deal cycle length). Quarterly trend for the directional view. |

**Alert thresholds:**
- **Yellow:** Conversion rate drops below 20% (trailing 90-day), or any single stage shows > 50% drop-off.
- **Red:** Conversion rate drops below 15% (trailing 90-day), or S4 (business case) → S5 (negotiation) drop-off exceeds 60% (signals the pricing/commitment conversation is breaking down).

**What to do when the alert fires:** The stage waterfall tells you where to focus. High drop-off at S1→S2 (discovery to scoping) means the initial conversation isn't uncovering a real enterprise need — recalibrate PQA scoring or discovery questions. High drop-off at S4→S5 (business case to negotiation) means the commitment framing or pricing isn't landing — revisit the floor setting, discount structure, or champion arming materials. High drop-off at S5→S6 (negotiation to close) means procurement is killing deals — build the procurement-readiness materials (security packet, compliance docs, standard contract).

---

### Metric 6: Revenue Mix

**What it answers:** What percentage of total revenue comes from committed ARR versus self-serve consumption? This is the "predictability ratio" — the north star for whether the sales overlay is accomplishing its mission.

| Field | Specification |
| --- | --- |
| **Definition** | Monthly revenue split between three categories: committed ARR (contracted, high confidence), consumption above commit (overage on committed accounts), and self-serve consumption (pay-as-you-go, no contract) |
| **Primary data source** | Billing system (Stripe, Chargebee) — for actual consumption revenue by account |
| **Secondary data source** | CRM — for committed contract values and terms |
| **Update frequency** | Monthly |
| **Visualization** | Stacked area chart — months on x-axis, three revenue layers stacked. Committed ARR on the bottom (most stable), consumption above commit in the middle, self-serve on top (most volatile). Include a target line for committed ARR as percentage of total. |
| **Time range** | 12-month rolling view. Quarterly annotations for major milestones (first committed deal, Tier 2 nurture launch, etc.). |

**Alert thresholds:**
- **Yellow:** Committed ARR percentage is flat or declining for 2 consecutive months.
- **Red:** Committed ARR percentage declines for 3 consecutive months, or self-serve consumption contracts while committed ARR doesn't grow (indicates base erosion, not conversion success).

**What to do when the alert fires:** If committed ARR isn't growing, the conversion motion isn't producing deals — look at Metrics 4–5 for the breakdown point. If self-serve is contracting, the product funnel is shrinking — look at Metrics 1–2. The healthy pattern is: self-serve grows (product funnel is healthy) AND committed ARR grows faster (conversion is working), so the ratio shifts over time. If total revenue is growing but entirely on self-serve, the sales overlay isn't converting — which means the company is growing but not becoming more predictable.

---

## Supplementary Metrics (Same Dashboard, Below the Fold)

These four metrics don't get their own primary dashboard tile but should be accessible on the same page as a detail view.

### Net Revenue Retention (NRR)

| Field | Specification |
| --- | --- |
| **Definition** | Revenue from existing accounts this period ÷ revenue from those same accounts in the prior period. Includes expansion, contraction, and churn. |
| **Data source** | Billing system — cohort-based calculation |
| **Update frequency** | Monthly |
| **Visualization** | Single number with 6-month trend. Color-coded: green > 110%, yellow 100–110%, red < 100%. |
| **Why it matters** | NRR above 100% means the existing base is a growth engine. Below 100% means adding new logos is filling a leaky bucket. This is the single most important metric in PLG after the conversion engine is running. |

### Logo Churn vs. Revenue Churn

| Field | Specification |
| --- | --- |
| **Definition** | Logo churn: percentage of accounts that go to $0. Revenue churn: percentage of revenue lost from accounts that contract or churn. |
| **Data source** | Billing system |
| **Update frequency** | Monthly |
| **Visualization** | Dual line chart — logo churn rate and revenue churn rate on the same axes. Divergence between the two tells a story. |
| **Why it matters** | You can retain logos but lose revenue if usage declines. A customer dropping from $10K/month to $2K/month hasn't churned by logo count — but the revenue impact is significant. If revenue churn exceeds logo churn, you have a contraction problem, not just a retention problem. |

### Expansion Revenue Ratio

| Field | Specification |
| --- | --- |
| **Definition** | New ARR from existing accounts (expansion) ÷ total new ARR (expansion + new logos) |
| **Data source** | CRM + billing system |
| **Update frequency** | Monthly |
| **Visualization** | Single percentage with 6-month trend. Healthy PLG companies: 30–50%+ from expansion. |
| **Why it matters** | If new logo revenue dominates, the product doesn't expand within accounts — or the expansion motion hasn't been built. The committed deal is the beginning, not the end. |

### Pipeline Arithmetic Health

| Field | Specification |
| --- | --- |
| **Definition** | Current PQA volume, engagement rate, and conversion rate mapped against the backward-math requirements for the committed ARR target |
| **Data source** | CRM + product analytics + billing |
| **Update frequency** | Weekly |
| **Visualization** | Three-row table: Required vs. Actual for growing accounts, PQAs, and committed deals. Color-coded red/yellow/green per row. |
| **Why it matters** | This is the operational health check. If required PQAs = 160/year and you're producing 80, the gap is visible immediately. If PQAs are on track but committed deals are behind, the gap is downstream. |

---

## Data Pipeline Requirements

The dashboard requires four systems to be connected. If they're siloed, building the pipeline is a Week 1 priority.

| System | What It Provides | Integration Method |
| --- | --- | --- |
| **Product analytics** (Amplitude, Mixpanel, Heap, or internal) | Sign-ups, activation events, feature usage, team-spread signals, usage depth | Event stream to data warehouse, or direct API for real-time PQA scoring |
| **Billing system** (Stripe, Chargebee, or internal) | Spend by account, payment method, invoice requests, consumption trends | API sync to data warehouse on daily cadence |
| **Enrichment tool** (Clearbit, ZoomInfo, or manual) | Company identification from email domain, firmographic data, contact data | Triggered on sign-up (automated) or manual enrichment for top accounts |
| **CRM** (Salesforce, HubSpot) | Deal stages, sales engagement tracking, pipeline management, committed contract values | Bi-directional sync with data warehouse; PQA scores pushed in, deal stages pulled out |

**The glue:** A data warehouse (Snowflake, BigQuery, Redshift) or a reverse ETL tool (Census, Hightouch) that combines product analytics + billing + enrichment into account-level records, scores them against the PQA model, and pushes qualified accounts into the CRM. Without this integration layer, Metrics 3–6 require manual assembly — which means they won't be maintained.

**Minimum viable version:** If the full pipeline can't be built in Week 1, start with a spreadsheet. Pull the top 50 accounts manually from billing data, score them with the Account Scoring Card, and track engagement in the CRM. The dashboard can be a weekly Google Sheet that gets upgraded to an automated dashboard once the data pipeline is built. Don't let perfect infrastructure delay the first Tier 1 cohort.

---

## Implementation Checklist

| Step | Owner | Target |
| --- | --- | --- |
| Define activation event (Metric 2) | Product + GTM leader | Week 1 |
| Confirm data source accessibility for all 6 metrics | Rev Ops / Data Eng | Week 1–2 |
| Build PQA scoring query in data warehouse | Rev Ops / Data Eng | Week 2–3 |
| Set up CRM stage tracking for PLG pipeline (S0–S6) | Rev Ops | Week 5 |
| Build automated PQA → CRM routing | Rev Ops / Data Eng | Week 5–6 |
| Build dashboard v1 (top 6 metrics, manual refresh) | Rev Ops | Day 65 |
| Add supplementary metrics (NRR, churn split, expansion ratio, pipeline arithmetic) | Rev Ops | Day 75 |
| Automate refresh cadence | Data Eng | Day 80 |
| Calibrate alert thresholds against first 4 weeks of observed data | GTM leader + Rev Ops | Day 90 |

---

*This spec operationalizes the six-metric PLG dashboard from the PLG-to-Enterprise Conversion Playbook. Alert thresholds are starting points — calibrate against observed data after the first Tier 1 cohort produces conversion signal. The dashboard is designed for a weekly operating cadence: review metrics 1–5 every Monday, review metric 6 monthly, and use the supplementary metrics for quarterly business reviews. The data pipeline requirements are listed in priority order: product analytics and billing are prerequisites, enrichment and CRM integration follow. If the full pipeline can't be built immediately, start with manual assembly for the top 50 accounts — imperfect data reviewed weekly beats perfect data that doesn't exist yet.*
