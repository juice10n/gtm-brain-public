# Committed Spend Proposal Framework

*Structure for building consumption-to-committed offers: floor setting, discount framing, overage handling, and commitment structure selection. Fill in per account using product data and discovery context.*

| **DOCUMENT TYPE** | Companion Tool — PLG-to-Enterprise Playbook |
| --- | --- |
| **DERIVES FROM** | Tenet 8 — Pricing & Packaging |
| **SUPPORTING TENETS** | Tenet 1 (ICP — account data), Tenet 4 (Discovery — organizational context), Tenet 9 (Metrics — revenue mix impact) |
| **PREREQUISITE** | Account scored via PQA Account Scoring Card. At minimum: current monthly spend, spend trend, and organizational context from discovery conversation. |
| **AUTHOR** | Justin Nychay |
| **VERSION** | 1.0 │ April 2026 |

---

## The Operating Principle

The pricing conversation with a self-serve user is different from a cold enterprise prospect. They already know what they're paying. The conversation is not "here's what it costs" — it is "here's how to get more value for less money by committing."

The anchor is not cost-of-alternative in the traditional sense — they're already using you. The anchor is cost-of-uncertainty: what happens when your usage doubles and you don't have a committed rate? What happens when you need enterprise support and don't have an SLA? What happens when your security team requires a vendor assessment and you're on a self-serve plan?

Frame the commitment as an upgrade, not a lock-in. The buyer gets something they don't have today — predictability, support, enterprise features — in exchange for a commitment they're functionally already making through their usage.

---

## Section 1: Account Data (Pre-Proposal)

Populate from product analytics, billing system, and discovery conversation before building the proposal.

| Field | Data | Source |
| --- | --- | --- |
| **Account name** | | CRM / enrichment |
| **Current monthly spend** | $ | Billing system |
| **3-month spend trend** | $ / $ / $ | Billing system |
| **6-month average monthly spend** | $ | Billing system |
| **Month-over-month growth rate** | % | Billing system |
| **Projected 12-month spend at current trajectory** | $ | Calculated: 6-month average × growth rate × 12 |
| **Number of active users** | | Product analytics |
| **Primary use case(s)** | | Product analytics + discovery |
| **Production vs. sandbox** | | Product analytics |
| **Payment method** | ☐ Credit card ☐ Invoice ☐ Mixed | Billing system |
| **Champion name / title** | | Discovery |
| **Economic buyer identified** | ☐ Yes: __________ ☐ No | Discovery |
| **Budget cycle timing** | | Discovery |
| **Enterprise requirements surfaced** | ☐ SSO ☐ SLA ☐ Data residency ☐ Audit logs ☐ Admin controls ☐ Security review ☐ Other: _____ | Discovery |

---

## Section 2: Floor Setting

The commit floor is the most important number in the proposal. Set it correctly and the commitment is a no-brainer — the buyer is already spending this much. Set it too high and they agonize. Set it too low and you leave revenue on the table.

**The rule: 70-80% of the account's current run-rate.**

| Calculation | Formula | Result |
| --- | --- | --- |
| Current monthly run-rate | (trailing 3-month average) | $ |
| Floor at 70% | Run-rate × 0.70 | $ |
| Floor at 80% | Run-rate × 0.80 | $ |
| **Proposed floor** | | **$** |

**Floor selection guidance:**

| Choose 70% When | Choose 80% When |
| --- | --- |
| First committed deal with this account — make it a no-brainer | Account has strong growth signals — they'll exceed the floor quickly |
| Account has variable usage (spiky, seasonal) | Usage is stable and predictable month-over-month |
| Champion is enthusiastic but economic buyer is risk-averse | Champion has already validated budget holder willingness |
| You want to minimize procurement friction and close fast | You have competitive leverage — the account is locked in |

**The test:** When you present the floor, the buyer should react with "of course we'll commit to that — we're already spending more." If the reaction is hesitation or negotiation, the floor is too high.

---

## Section 3: Discount Structure

The discount must be meaningful enough to justify procurement friction. Below 15%, the savings don't justify the effort of running a contract through legal. Above 25%, you're leaving revenue on the table.

| Component | Self-Serve (Current) | Growth Commit | Enterprise Commit |
| --- | --- | --- | --- |
| **Commitment** | None (pay-as-you-go) | Monthly minimum ($2K-$10K/month) | Annual ($50K+ ACV) |
| **Discount off PAYG** | 0% | 15-20% | 20-25% |
| **Billing** | Credit card | Invoice (net-30) | Invoice (net-30 or net-45) |
| **Support** | Standard (self-serve) | Basic SLA | Dedicated support + custom SLA |
| **Account management** | None | Assigned CSM | Dedicated account manager |
| **Enterprise features** | None | Team admin, shared configs | SSO, audit logs, data residency, compliance |

**Discount selection for this account:**

| Question | Answer | Implication |
| --- | --- | --- |
| What tier is this account? | ☐ Growth ☐ Enterprise | Sets the discount band |
| What's the commitment period? | ☐ Quarterly ☐ Annual ☐ Multi-year | Longer commitment = higher discount |
| Is there competitive pressure? | ☐ Yes ☐ No | If yes, lean toward higher end of band |
| Is this a lighthouse / reference account? | ☐ Yes ☐ No | If yes, discount is an investment in proof points |
| **Selected discount** | | **___%** |

---

## Section 4: Commitment Structure Selection

Enterprise procurement needs a number. Three approaches to creating budget certainty for consumption products. Select the one that fits the account's usage pattern and procurement requirements.

### Option A: Fixed Allotment with Rollover (Twilio Model)

| Field | Value |
| --- | --- |
| **How it works** | Buy a block of credits/units. Unused credits roll forward to the next period. |
| **Best for** | Accounts with variable usage who need budget certainty. Buyers who fear "use it or lose it." |
| **Vendor benefit** | Committed revenue upfront. Predictable cash flow. |
| **Buyer benefit** | Budget certainty. No waste — unused credits carry over. Known ceiling for finance. |
| **Risk** | If rollover accumulates, future renewal conversations get harder. Set rollover caps (e.g., max 1 period rollover). |
| **Proposed allotment** | _____ units/credits per [month/quarter/year] |
| **Rollover policy** | Unused units roll forward up to _____ [period]. Expire after _____. |
| **Unit price at committed rate** | $ _____ (vs. $ _____ PAYG) |

### Option B: Minimum Commit with True-Up (Snowflake Model)

| Field | Value |
| --- | --- |
| **How it works** | Commit to a spend floor. Usage above the floor billed at standard PAYG rates. True-up quarterly. |
| **Best for** | High-growth accounts where usage will likely exceed the commit. Accounts that want a safety net but expect to grow. |
| **Vendor benefit** | Guaranteed revenue floor with upside from overages. Natural upsell trigger when overages become consistent. |
| **Buyer benefit** | Budget floor for finance with flexibility to grow. No penalty for exceeding — just standard rates. |
| **Risk** | If overages are punitive (2x rate), buyers under-commit to stay safe. Use standard PAYG rates for overages. |
| **Proposed minimum commit** | $ _____ per [month/quarter] |
| **Overage rate** | Standard PAYG rate ($ _____/unit) — not punitive |
| **True-up frequency** | ☐ Monthly ☐ Quarterly |
| **Right-sizing trigger** | If overages exceed commit by > 30% for 3 consecutive months, propose a right-sized commit |

### Option C: Dedicated Capacity (GPU Reservation Model)

| Field | Value |
| --- | --- |
| **How it works** | Reserve a fixed amount of compute/capacity for a fixed period. Buyer gets guaranteed availability. |
| **Best for** | Infrastructure products where the unit of value is capacity. Accounts with steady, predictable usage who value guaranteed availability. |
| **Vendor benefit** | Predictable infrastructure planning. Premium pricing for guaranteed access. |
| **Buyer benefit** | Guaranteed availability — no throttling, no contention. Predictable performance. |
| **Risk** | If usage drops below reserved capacity, buyer feels locked in. Include scale-down provisions at renewal. |
| **Proposed capacity** | _____ [units of capacity] for _____ [period] |
| **Capacity price** | $ _____ per [unit/period] |
| **Scale-up provision** | Additional capacity available at $ _____ per [unit] |
| **Scale-down provision** | At renewal, can adjust by ± ____% |

**Selected structure for this account:** ☐ A (Fixed Allotment) ☐ B (Minimum Commit) ☐ C (Dedicated Capacity)

**Rationale:** _______________________________________________

---

## Section 5: Proposal Summary

Build the one-page summary that the champion can carry to the economic buyer. This is not the contract — it is the conversation starter that frames the commitment as an upgrade.

### The Narrative Frame

| Current State | Committed State | Delta |
| --- | --- | --- |
| Spending $___/month on pay-as-you-go | Committing $___/month (floor) | Saving ___% ($___/month) |
| Self-serve support | [Basic SLA / Dedicated support] | [Response time guarantee] |
| No account management | [Assigned CSM / Dedicated AM] | Named point of contact |
| Standard features | [Enterprise features: SSO, audit logs, etc.] | [Specific enterprise capabilities gained] |
| Credit card billing | Invoice billing (net-30) | Procurement-friendly, budget-trackable |
| Usage uncertainty | Budget certainty | Finance can forecast this line item |

### Cost-of-Uncertainty Framing

Use these when the buyer asks "why should I commit when pay-as-you-go works fine?" The anchor is not what it costs today — it is what happens when things change.

| Scenario | Question to Ask | What It Surfaces |
| --- | --- | --- |
| Usage growth | "At your current growth rate, you'll be spending $___/month by [date]. Without a committed rate, that's $___/year at PAYG. With a commit, it's $___/year — saving $___ annually." | The savings scale with growth — the faster they grow, the more the commitment saves. |
| Enterprise requirements | "When your security team runs a vendor review — and at your usage level, they will — you'll need an account manager, SOC 2 documentation, and an SLA. On self-serve, those don't exist." | Enterprise features are not a nice-to-have — they're a requirement the buyer doesn't know they need yet. |
| Support criticality | "You're running production workloads. If something breaks at 2am, self-serve support means a ticket queue. A committed plan means a phone call to someone who knows your setup." | Criticality should match support level. Production workloads on self-serve support is a risk. |
| Budget predictability | "Your CFO can't budget an expense line that changes every month. A committed rate gives finance a known number they can plan against." | This speaks the economic buyer's language — predictability and controllability. |

### The One-Page Summary Template

```
COMMITTED AGREEMENT PROPOSAL — [Account Name]

Current State
  Monthly spend (trailing 3-month avg):  $______
  Projected 12-month spend at PAYG:      $______
  Active users:                          ______
  Primary use cases:                     ______

Proposed Commitment
  Structure:          [Fixed Allotment / Min Commit / Dedicated Capacity]
  Commitment period:  [Quarterly / Annual / Multi-year]
  Monthly floor:      $______
  Discount:           ___% off PAYG
  Projected 12-month cost at committed rate:  $______
  
Savings
  Annual savings vs. PAYG:  $______  (___%)
  
What Changes
  ☐ Volume pricing locked at committed rate
  ☐ [Support SLA: response time guarantee]
  ☐ [Account management: named point of contact]
  ☐ [Enterprise features: SSO / audit logs / admin controls / etc.]
  ☐ [Billing: invoice, net-30]
  ☐ [Overages: standard PAYG rate, not punitive]
  
Next Steps
  1. _______________________________________
  2. _______________________________________
  3. _______________________________________
```

---

## Section 6: Negotiation Guardrails

Define the walk-away points and flexibility zones before entering the pricing conversation.

| Parameter | Floor (minimum acceptable) | Target | Ceiling (best case) |
| --- | --- | --- | --- |
| Commitment amount | $ _____ /month | $ _____ /month | $ _____ /month |
| Discount | ___% | ___% | ___% |
| Commitment period | ☐ Quarterly | ☐ Annual | ☐ Multi-year |
| Payment terms | Net-60 | Net-30 | Prepaid annual |

**What you can offer to close:**
- Increase the discount by 2-3% if the buyer extends commitment period (quarterly → annual).
- Add rollover or true-up flexibility if the buyer increases the commit floor.
- Include onboarding or migration support at no additional cost for annual commitments.

**What you don't give away:**
- Enterprise features should not be discounted — they are included at the enterprise tier, not negotiated individually.
- Support SLA is not a negotiation lever — it comes with the tier. If they want dedicated support, they commit at enterprise level.
- Don't create custom pricing structures that can't be replicated across accounts. Every exception becomes a precedent.

---

*This framework operationalizes Section 8 (Consumption-to-Committed Pricing) of the PLG-to-Enterprise Conversion Playbook. Fill in Sections 1-2 from product data and billing history before the pricing conversation. Fill in Sections 3-4 based on the account's usage pattern and organizational context from discovery. Build the Section 5 summary as the deliverable the champion carries to the economic buyer. Define the Section 6 guardrails before entering negotiation so the rep knows their flexibility zone without needing approval on every concession.*
