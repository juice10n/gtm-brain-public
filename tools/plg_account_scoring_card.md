# PLG Account Scoring Card

*Score a self-serve account's readiness for sales engagement in under two minutes. Derived from the PQA model in the PLG-to-Enterprise Conversion Playbook.*

| **DOCUMENT TYPE** | Companion Tool — PLG-to-Enterprise Playbook |
| --- | --- |
| **DERIVES FROM** | Tenet 1 — ICP & Market Segmentation |
| **PREREQUISITE** | Completed Stakeholder Framework for enterprise personas |
| **AUTHOR** | Justin Nychay |
| **VERSION** | 1.0 │ April 2026 |

---

## How to Use This Card

Score each account across five signal categories (0–3 per category), apply the Negative PQA filter, then check persona reachability. The total score determines tier placement. This card assumes the Stakeholder Framework has been completed — without it, you're scoring signals you haven't validated against the actual enterprise buyer.

**Scoring speed target:** Under two minutes per account once the data sources are accessible.

**When to use:** Week 3 of the 90-day implementation (Step 7 — Segmentation), then ongoing as new accounts cross monitoring thresholds.

---

## Section 1: Behavioral Signal Scoring

Score each category 0–3 based on the criteria below. Calibrate thresholds to your product's specific data — the examples are starting points, not universal benchmarks.

### Usage Velocity (0–3)

Growth rate over time matters more than absolute volume. Sustained velocity over 3+ months separates real adoption from experimentation.

| Score | Criteria | Example Threshold |
| --- | --- | --- |
| 0 | Flat or declining usage | < 5% MoM growth or negative trend |
| 1 | Modest growth, inconsistent | 5–15% MoM, fewer than 3 consecutive months |
| 2 | Steady growth, sustained | 15–30% MoM for 3+ consecutive months |
| 3 | Rapid acceleration | > 30% MoM for 3+ consecutive months |

**Data source:** Product analytics or billing system — monthly consumption trend by account.

**What this tells you:** A 3 here means the account is growing fast enough that they'll organically hit a spend level where commitment makes financial sense. A 0 means the account is stable self-serve — monitor but don't pursue.

---

### Breadth (0–3)

Number of distinct users, features, or use cases. Breadth indicates the product is solving multiple problems or serving multiple teams. A single power user is a fan. Multiple users across teams is an organization adopting.

| Score | Criteria | Example Threshold |
| --- | --- | --- |
| 0 | Single user, single use case | 1 user, 1 feature/endpoint |
| 1 | Single user, multiple use cases OR few users, single use case | 1 user across 3+ features, or 2–3 users on 1 feature |
| 2 | Multiple users, multiple use cases | 4–10 users across 2+ features/endpoints |
| 3 | Team-level adoption across use cases | 10+ users, 3+ distinct use cases, API key proliferation |

**Data source:** Product analytics — distinct users per account domain, feature/endpoint usage distribution.

**What this tells you:** A 3 here means the product has moved from individual tool to team infrastructure. This is the strongest signal that the Stakeholder Framework's "practitioner champion" persona is already present and active.

---

### Depth (0–3)

Usage sophistication and embedding. Depth indicates the product is embedded in real workflows, not being evaluated.

| Score | Criteria | Example Threshold |
| --- | --- | --- |
| 0 | Sandbox or experimentation only | Dev/test environment, no production workloads |
| 1 | Light production usage | Some production workloads, but intermittent or low-volume |
| 2 | Consistent production usage | Sustained production workloads, integrations active |
| 3 | Deeply embedded, mission-critical | Production-critical, advanced features, custom integrations, high uptime dependency |

**Data source:** Product analytics — environment flags (dev/staging/prod), integration usage, uptime patterns.

**What this tells you:** A 3 means switching cost is high — the product is embedded in production workflows. This is leverage in the commitment conversation: "you're already dependent on us in production — a committed agreement adds the SLA and support that matches that dependency."

---

### Organizational Signals (0–3)

Evidence that usage has moved beyond an individual to an organizational footprint. These signal the transition from individual tool to team infrastructure.

| Score | Criteria | Example Threshold |
| --- | --- | --- |
| 0 | Personal email, single user | Gmail/Yahoo domain, no team signals |
| 1 | Corporate email, single user | @company.com domain, but only one user |
| 2 | Corporate email, team spread beginning | 2–5 users from same domain, or team invitations sent |
| 3 | Clear organizational adoption | 5+ users from same domain, shared workspaces, multiple teams visible |

**Data source:** Product analytics — email domain clustering, team invitation events, shared workspace creation.

**What this tells you:** This is the most binary signal. A 0 (personal email, no team) combined with any other high scores likely means hobbyist — flag for Negative PQA review. A 3 means the organization is adopting, which means the Stakeholder Framework's "economic buyer" persona is either aware or will become aware soon.

---

### Financial Signals (0–3)

Spend trajectory and procurement indicators. When someone asks for an invoice, procurement is involved. That's an enterprise signal.

| Score | Criteria | Example Threshold |
| --- | --- | --- |
| 0 | Minimal or free-tier usage | < $100/month or free tier only |
| 1 | Modest spend, credit card payment | $100–$500/month, self-serve billing |
| 2 | Meaningful spend, approaching threshold | $500–$2K/month, or credit card approaching limit |
| 3 | Enterprise-level spend and/or procurement signals | > $2K/month sustained, invoice requested, billing inquiry, corporate card transition |

**Data source:** Billing system — monthly spend by account, payment method, billing inquiries (support tickets or in-app requests).

**What this tells you:** A 3 with an invoice request is one of the strongest individual signals in PLG — it means procurement is already aware. A billing inquiry from someone other than the original sign-up means a new Stakeholder Framework persona has surfaced.

---

## Section 2: Negative PQA Filter

Before calculating the total score, check for disqualification signals. If any Negative PQA criteria are present, suppress the account from sales routing regardless of behavioral score. Every minute a rep spends on a disqualified account is a minute not spent on a Tier 1 account.

| Negative Signal | How to Identify | Action |
| --- | --- | --- |
| **Hobbyist / Researcher** | Personal email, no team spread, irregular usage patterns. Often academics, students, personal projects. | Suppress — no sales routing. Monitor only if usage pattern changes. |
| **Tire-Kicker** | Burst of activity followed by 30+ days of silence. Evaluated for a specific project and moved on. | Suppress — account is dormant. Re-evaluate only if usage resumes. |
| **Price-Only Buyer** | Minimal feature adoption, pricing page visits, comparison searches in support docs. Shopping competitors. | Suppress — no product loyalty. Will churn at the first discount from a competitor. |
| **Single-Use-Case Experimenter** | Using one narrow feature with no expansion path. Account will never grow beyond current spend. | Suppress or downgrade to Watch. Spend ceiling is visible. |
| **Free-Tier Staller** | Extended free-tier usage with no conversion signal. Has found a way to extract value without paying. | Suppress — conversion probability is near zero without a product-side forcing function. |

---

## Section 3: Persona Reachability Check

High behavioral scores without persona reachability produce wasted sales effort. This check validates that the Stakeholder Framework personas can be reached before committing sales resources.

| Check | Question | Pass / Fail |
| --- | --- | --- |
| **Champion identified** | Can you identify the practitioner who adopted the product? Do you have a name, title, and contact path? | ☐ Pass ☐ Fail |
| **Economic buyer reachable** | Can you identify the budget holder (VP, CTO, Director) at the account? Is there a path to them — either through the champion or directly? | ☐ Pass ☐ Fail |
| **Organization mappable** | Can you determine the company, its size, industry, and funding stage from the sign-up domain or enrichment data? | ☐ Pass ☐ Fail |

**Scoring adjustment:** If all three pass, score stands. If champion is identified but economic buyer is not reachable, downgrade one tier. If organization is not mappable (personal email, no enrichment possible), flag for Negative PQA review regardless of behavioral score.

---

## Section 4: Total Score and Tier Placement

### Calculate

| Category | Score (0–3) |
| --- | --- |
| Usage Velocity | ___ |
| Breadth | ___ |
| Depth | ___ |
| Organizational Signals | ___ |
| Financial Signals | ___ |
| **Total** | ___ / 15 |

### Negative PQA Filter

| Any negative signals present? | ☐ No — proceed to tier placement ☐ Yes — suppress from sales routing |

### Persona Reachability

| Champion identified? | ☐ Yes ☐ No |
| Economic buyer reachable? | ☐ Yes ☐ No |
| Organization mappable? | ☐ Yes ☐ No |

### Tier Placement

| Tier | Score Range | Persona Check | Sales Action |
| --- | --- | --- | --- |
| **Tier 1 — Harvest** | 10–15 | Champion + economic buyer reachable | Proactive sales outreach. Dedicated rep time. First cohort: 10–20 accounts. |
| **Tier 2 — Nurture** | 6–9 | Champion identifiable, economic buyer unclear | Automated touches triggered by usage milestones. No dedicated sales time. Goal: accelerate signals toward Tier 1. |
| **Tier 3 — Watch** | 0–5 | Partial or no persona visibility | No sales involvement. Automated scoring monitors for signal changes. Self-serve revenue is still revenue. |

**Override rules:**
- Financial signal = 3 (invoice request or billing inquiry) overrides total score — move to Tier 1 regardless. Procurement has surfaced; you need to be in the conversation.
- Organizational signal = 0 (personal email, single user) caps tier at Watch regardless of total score. No organizational footprint means no enterprise conversion path.
- Total score ≥ 10 but economic buyer not reachable → Tier 2, not Tier 1. Strong usage without a path to the budget holder is a nurture play, not a harvest play.

---

## Section 5: Account Summary (One Per Account)

| Field | Entry |
| --- | --- |
| **Account name** | |
| **Domain** | |
| **Current monthly spend** | |
| **Spend trend (3-month)** | |
| **Active users** | |
| **Primary use case(s)** | |
| **Champion name / title** | |
| **Economic buyer identified?** | |
| **Total PQA score** | ___ / 15 |
| **Negative PQA flags** | |
| **Tier placement** | ☐ Harvest ☐ Nurture ☐ Watch ☐ Suppressed |
| **Recommended first action** | |
| **Engagement trigger (if applicable)** | |
| **Date scored** | |

---

*This scoring card operationalizes the PQA model from the PLG-to-Enterprise Conversion Playbook. The behavioral signals (Section 1) are calibrated against the Stakeholder Framework personas — not scored in isolation. The Negative PQA filter (Section 2) prevents volume from overwhelming quality. The persona reachability check (Section 3) ensures sales effort is deployed against accounts where the enterprise buying committee is accessible. Threshold calibration is company-specific: retroactively score the top 50 accounts and adjust thresholds until the tier placement matches your intuitive ranking of which accounts you'd want to talk to first.*
