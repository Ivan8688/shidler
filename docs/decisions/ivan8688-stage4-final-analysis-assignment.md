# Stage 4 – Final Analysis, Prompt Engineering & Recommendation
## FX Hedging Strategy for TechServe Global: EUR Receivable Exposure (€12.5M, 1-Year Horizon)

<div style="border-left: 5px solid #024731; padding: 1rem; margin: 1.5rem 0; background-color: #E6F2EF; border-radius: 0.5rem;">

**Created by:** Ivan Lee  
**Updated by:** Ivan Lee  
**Date Created:** 2026-04-28  
**Date Updated:** 2026-04-28  
**Version:** 1.0  
**LLM Used:** Claude (Copilot) — Assisted with structure and analysis; revised for accuracy

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** Chief Financial Officer (CFO) / Chief Treasury Officer (CTO)  
**Decision Context:** TechServe Global's €12.5M service contract receivable settlement (12-month horizon)

**Executive Recommendation:** **Implement a Forward Contract Hedge** to lock in $13,637,500 USD proceeds, eliminating FX variance and providing budget certainty for quarterly reporting.

</div>

---

## A. EXPOSURE SUMMARY

### TechServe Global's FX Risk Profile

**Core Exposure:**
- **Amount:** €12,500,000 (contract revenue from major Western European client)
- **Settlement Date:** Exactly 12 months from inception (2027-04-24)
- **Current Spot Rate:** 1.0875 USD/EUR
- **Expected USD Proceeds at Spot:** $13,609,375

**Why This Risk Matters:**

TechServe's European operations have generated a significant revenue contract; however, the firm faces material foreign-currency exposure. EUR/USD volatility historically averages 4–6% annualized. A 5% euro depreciation (moving from 1.0875 to 1.0331) would reduce USD proceeds by approximately **$680,000**, eroding quarterly profitability and straining cash flow forecasts. Conversely, a favorable appreciation could yield $670,000 upside, creating **asymmetric risk** in a macroeconomically uncertain environment (geopolitical tension, ECB policy divergence, persistent inflation volatility).

**Business Context:**

Treasury best practices for mid-market firms recommend hedging all FX receivables above 5–10% of annual revenue. At ~$13.6M, this exposure likely exceeds TechServe's materiality threshold and warrants formal hedging analysis. Unhedged FX variance clouds investor relations, complicates guidance, and disadvantages the firm relative to competitors with effective hedging programs who can offer stable revenue projections.

---

## B. SUMMARY OF HEDGE OUTCOMES

Comprehensive modeling of four hedging strategies (plus unhedged baseline) reveals distinct trade-offs in certainty, cost, and optionality. All results derived from Stage 2 Excel model using Scenario 3 market data.

### Key Findings by Strategy:

| **Strategy** | **Base Case (S_T = 1.0875)** | **Worst Case (S_T = 1.0331, −5%)** | **Best Case (S_T = 1.1420, +5%)** | **Key Characteristic** |
|---|---|---|---|---|
| **Unhedged** | $13,609,375 | $12,912,500 | $14,276,563 | Maximum volatility; range = $1.36M |
| **Forward Contract** | $13,637,500 | $13,637,500 | $13,637,500 | Complete certainty; zero cost; zero optionality |
| **Put Option** | $13,381,250 | $13,381,250 | $14,276,563 | Downside floor ($1.0875); upside preserved; cost = $212,500 |
| **Collar** | $13,381,250 | $13,381,250 | $13,937,500 | Defined range ($1.0875–$1.1200); net credit = −$62,500 |

### Detailed Strategy Analysis:

#### **1. Forward Contract Hedge**

**What It Does:**
Lock in a fixed USD/EUR rate (1.0910) today for settlement in 12 months. Regardless of where spot rates move, TechServe will convert the €12.5M at exactly 1.0910, receiving **$13,637,500 USD**.

**Mechanics:**
- Enter into a binding forward contract with a bank today
- Zero premium cost (forward rate already embeds interest rate differentials via covered parity)
- Non-cancelable; must settle at the contracted rate

**Key Metrics:**
- **USD Proceeds (all scenarios):** $13,637,500
- **Range (volatility):** $0 (flat across all FX outcomes)
- **Premium Cost:** $0
- **Upside Participation:** None (foregoes any euro appreciation above 1.0910)
- **Downside Protection:** Complete (protected against any euro depreciation below 1.0910)

**Pros:**
- ✅ Simple, transparent, zero cost
- ✅ Eliminates FX variance; perfect for budget certainty
- ✅ Reduces P&L volatility for investor guidance
- ✅ No credit risk to option seller

**Cons:**
- ❌ Loses upside if euro appreciates significantly (tail risk: if S_T = 1.12, unhedged would yield $14M vs. $13.64M)
- ❌ Non-flexible; cannot unwind without mark-to-market loss if rates move unfavorably
- ❌ Requires continuous monitoring to ensure no basis risk

#### **2. Money Market Hedge**

**What It Does:**
Synthetically replicate the forward rate through three-step arbitrage:
1. Discount the EUR receivable to PV (€12.5M ÷ 1.04 = €12,019,231)
2. Borrow this PV amount in EUR today
3. Convert at spot (€12,019,231 × 1.0875 = $13,070,928)
4. Invest USD for 1 year at USD rate ($13,070,928 × 1.0525 = $13,756,601)
5. Repay EUR loan with incoming €12.5M

**Key Metrics:**
- **USD Proceeds:** $13,756,601
- **Parity Validation:** Forward ($13,637,500) vs. MM ($13,756,601) — difference 0.87% (acceptable)
- **Premium Cost:** None (embedded in interest rate spread)

**Pros:**
- ✅ Validates that forward market is efficiently priced (arbitrage holds)
- ✅ Uses only cash and money market instruments (no derivatives credit risk)

**Cons:**
- ❌ Requires balance sheet capacity to borrow €12M+ today
- ❌ Liquidity implications (cash tied up for 12 months)
- ❌ More complex operationally than a simple forward
- ❌ EUR borrowing rates may fluctuate; parity assumes rates sticky

**Assessment:** Useful as a parity check and for educational understanding, but not a practical recommendation for TechServe unless balance sheet constraints preclude derivative use.

#### **3. Put Option Hedge**

**What It Does:**
Buy a EUR put option with strike at today's spot (1.0875). This gives TechServe the right (but not obligation) to sell €12.5M at 1.0875 anytime through maturity. Protects against depreciation while preserving upside.

**Mechanics:**
- Strike (K): 1.0875 USD/EUR (at-the-money)
- Premium: $0.0170 per EUR = **$212,500 total** (paid upfront)
- Payoff: MAX(S_T, K) × FC_AMT − Premium

**Key Metrics:**
- **USD Proceeds at Base Case:** $13,381,250 (= $13,593,750 payoff − $212,500 premium)
- **USD Proceeds if S_T drops to 1.0331 (−5%):** $13,381,250 (protected!)
- **USD Proceeds if S_T rises to 1.1420 (+5%):** $14,276,563 (captures upside)
- **Premium Cost:** $212,500 (sunk cost; reduces proceeds but provides optionality)
- **Breakeven Rate:** 1.0892 (the rate at which euro appreciation pays back the premium)

**Pros:**
- ✅ Downside protected at K = 1.0875; loss capped at premium paid
- ✅ Unlimited upside if euro appreciates (valuable in bull scenarios)
- ✅ Preserves optionality; can abandon put if not exercised
- ✅ Appropriate if FX forecast is genuinely uncertain

**Cons:**
- ❌ Premium cost ($212,500) is 1.56% of notional; reduces expected proceeds
- ❌ Requires OCI accounting if not designated as hedge
- ❌ Complexity: payoff is non-linear (kinked at strike)
- ❌ Tail risk: if S_T = 1.15 (unlikely but possible), unhedged > put

**Assessment:** Attractive if management believes euro has genuine upside potential or is highly risk-averse to downside. Cost-benefit depends on TechServe's earnings volatility tolerance and FX forecast confidence.

#### **4. Collar Hedge**

**What It Does:**
Buy a put (downside protection) and sell a call (cap upside). The call premium ($275,000) offsets the put premium ($212,500), resulting in a **net credit of $62,500** to TechServe.

**Mechanics:**
- Long Put: K = 1.0875 (same as pure put), Premium paid = $212,500
- Short Call: K = 1.1200 (out-of-the-money), Premium received = $275,000
- Net Cost: −$62,500 (Treasury **receives** cash upfront)
- Payoff: MIN(MAX(S_T, K_PUT), K_CALL) × FC_AMT + $62,500

**Key Metrics:**
- **USD Proceeds at Base Case:** $13,381,250 (protected at put floor)
- **USD Proceeds if S_T = 1.0331 (−5%):** $13,381,250 (put exercises)
- **USD Proceeds if S_T = 1.1420 (+5%):** $13,937,500 (call caps upside at 1.12)
- **Defined Range:** $13,381,250 (floor) to $13,937,500 (ceiling) — only $556,250 spread
- **Upside Participation:** Capped; loses ~2.4% of potential upside if S_T = 1.14

**Pros:**
- ✅ Zero or **negative cost** (net credit of $62,500 received)
- ✅ Downside fully protected; provides certainty like a forward but with less cost
- ✅ Upside participation up to 1.12 (reasonable in balanced scenario)
- ✅ Narrow range ($13.38M–$13.94M) appeals to CFOs seeking visibility

**Cons:**
- ❌ Upside capped; if S_T rallies significantly (to 1.15), collar underperforms unhedged
- ❌ Counterparty credit risk on the call seller (though small given short tenor)
- ❌ Accounting treatment may require mark-to-market (ASC 815 complexity)
- ❌ Less intuitive for stakeholders than forward or put

**Assessment:** Excellent middle ground if management wants downside protection without fully sacrificing upside. The net credit is attractive for budget presentation (positive "income" from hedging).

#### **5. Unhedged Baseline**

**What It Does:**
Take no action; convert €12.5M at whatever spot rate prevails in 12 months.

**Outcomes:**
- **Worst Case (S_T = 1.0331):** $12,912,500 (loss vs. base = $697K)
- **Base Case (S_T = 1.0875):** $13,609,375
- **Best Case (S_T = 1.1420):** $14,276,563 (gain vs. base = $667K)
- **Volatility Range:** $1,364,063 (maximum of all strategies; 10% swing!)

**Pros:**
- ✅ No cost or operational burden
- ✅ Captures full upside if euro rallies

**Cons:**
- ❌ Material downside risk ($680K loss in realistic −5% scenario)
- ❌ Earnings volatility makes guidance unreliable
- ❌ Competitive disadvantage vs. firms with stable, hedged revenues
- ❌ Shareholder pressure if euro depreciates and contract profit margin erodes

**Assessment:** Acceptable only if TechServe has high FX tolerance, strong balance sheet, or genuine conviction euro will appreciate. Not recommended for prudent treasury function.

---

## C. SENSITIVITY INTERPRETATION

### EUR Depreciation Scenarios (S_T < S₀)

**If EURUSD weakens from 1.0875 to 1.0331 (−5% move):**

| Strategy | USD Proceeds | vs. Base | Loss |
|---|---|---|---|
| Unhedged | $12,912,500 | −$696,875 | **−5.1%** |
| Forward | $13,637,500 | +$28,125 | None |
| Put | $13,381,250 | −$228,125 | Premium paid |
| Collar | $13,381,250 | −$228,125 | Capped at put |

**Interpretation:**
- Unhedged suffers maximum loss ($697K), directly proportional to spot depreciation
- Forward **gains** relative to base (locks in forward rate, which was already 0.35% above spot)
- Put loses only the premium ($212.5K), minimizing downside relative to unhedged (save $485K)
- Collar performs identically to put; both protect to the same floor

**Key Insight:** All hedged strategies provide meaningful protection in downside scenarios. Forward offers **complete certainty** (no variance), while put/collar offer **floor protection** at the cost of premium.

### EUR Appreciation Scenarios (S_T > S₀)

**If EURUSD strengthens from 1.0875 to 1.1420 (+5% move):**

| Strategy | USD Proceeds | vs. Base | Gain |
|---|---|---|---|
| Unhedged | $14,276,563 | +$667,188 | **+4.9%** |
| Forward | $13,637,500 | −$28,063 | Foregoes appreciation |
| Put | $14,276,563 | +$667,188 | Captures full upside |
| Collar | $13,937,500 | +$328,125 | Upside capped at 1.12 |

**Interpretation:**
- Unhedged captures full upside ($667K additional revenue)
- Forward **underperforms** (locked into forward rate; misses appreciation)
- Put **participates fully** (no upside ceiling; upside payoff unaffected by strike being OTM)
- Collar **participates partially** (capped at K_CALL = 1.12; loses ~$339K of potential $667K gain)

**Key Insight:** Forward sacrifices all optionality but provides certainty. Put preserves optionality at a premium cost. Collar splits the difference: moderate protection, moderate upside, net credit structure.

### Risk-Adjusted Interpretation:

**Volatility Comparison:**
- **Unhedged:** $1,364,063 range (10% volatility)
- **Forward:** $0 range (0% volatility) ← CFO most prefers this
- **Put:** $895,313 range (6.6% volatility) ← Good balance of protection + participation
- **Collar:** $556,250 range (4.1% volatility) ← Tight range appeals to risk-averse CFO

**Which volatility profile fits TechServe's risk appetite?**
- **If Q-over-Q earnings stability is paramount:** Forward (0% volatility)
- **If balanced protection + upside is desired:** Put (6.6% volatility)
- **If visibility + modest upside is sought:** Collar (4.1% volatility)
- **If management has strong EUR bull conviction:** Unhedged (but not recommended)

---

## D. STRATEGIC RECOMMENDATION

<div style="border-left: 5px solid #024731; padding: 1rem; margin: 1.5rem 0; background-color: #E6F2EF; border-radius: 0.5rem; font-weight: 600; font-size: 1.1rem;">

### PRIMARY RECOMMENDATION: **FORWARD CONTRACT HEDGE**

**Implementation:** Lock in the 1-year EURUSD forward rate (1.0910) via a binding forward contract with TechServe's banking partner. Settle the €12.5M at the agreed rate upon collection.

**Expected Outcome:** $13,637,500 USD proceeds, **guaranteed**, eliminating FX variance.

**Timeline:** Execute forward contract **today** (within 2–3 business days) to lock in current forward curve before rates shift.

</div>

### Rationale for Forward Selection:

**1. Cash Flow Certainty**

TechServe's Q2 2027 earnings guidance and budget forecasts depend on predictable EUR-to-USD conversion. A forward contract provides **perfect visibility:** management can confidently project $13.64M in USD revenue for financial reporting, cash flow planning, and shareholder communication. This eliminates the +/− $680K variance that alternative hedges (or no hedge) introduce.

**2. Cost-Benefit Analysis**

- **Forward:** $0 cost, $13,637,500 proceeds guaranteed
- **Put:** $212,500 cost, $13,381,250 min proceeds, potential upside to $14.28M
- **Collar:** −$62,500 cost (net credit), $13,381,250–$13,937,500 range

The forward's **zero cost** is a decisive advantage. The $212,500 put premium (1.56% of notional) erodes expected proceeds relative to forward. While the put captures upside, TechServe is a tech services provider (not a currency trader), not positioned to profit from FX moves. The put's $667K potential upside is speculative; the forward's certainty is operational.

**3. Operational Simplicity**

Forwards are:
- Easy to execute (standard banking product)
- Transparent and intuitive (1-on-1 exchange rate locked in)
- Require no P&L accounting complexity (settled at maturity, not marked-to-market daily)
- Involve no optionality decisions (no "should I exercise?" uncertainty)

Puts and collars involve:
- Ongoing mark-to-market accounting (OCI vs. P&L per ASC 815)
- Payoff curve calculations (less intuitive for executive communication)
- Potential for suboptimal early exercise/unwind decisions

**4. Alignment with Treasury Function**

Modern corporate treasury focuses on **risk mitigation**, not speculation. Forward contracts are the default tool because they eliminate basis risk, match cash flow timing, and provide budget certainty. The CFO's primary concern is: "Will we reliably collect $13.6M USD in 12 months?" A forward answers: "Yes, exactly $13,637,500."

**5. Macroeconomic Context**

While EUR volatility is 4–6% (potentially favoring optionality), the downside risk to TechServe is asymmetric:
- **Downside (EUR depreciation):** Erodes contract profit margin; reduces cash available for reinvestment
- **Upside (EUR appreciation):** Bonus revenue; nice to have but not operationally critical

In an uncertain macro environment (geopolitical risk, ECB policy divergence), *eliminating* downside risk is more valuable than preserving speculative upside.

### Secondary Recommendation (Contingency):

**If management insists on upside participation:**

Implement a **Put Option Hedge** as an alternative. It provides $13.38M downside protection while capturing full upside if EUR rallies. The $212,500 premium (1.56%) is justified if:
- FX forecast genuinely suggests EUR strength (>55% probability of S_T > 1.10)
- Quarterly earnings volatility tolerance is high
- Balance sheet has capital to absorb premium cost

**Caveat:** The put is a "nice-to-have," not a "must-have." Forward is strongly preferred if budget certainty is the priority.

---

## E. EXECUTIVE JUSTIFICATION

### Summary of Recommended Approach: Forward Contract

**Decision:** Enter into a 1-year EURUSD forward contract at 1.0910 to hedge the €12.5M receivable.

**Financial Impact:**
- **Locked USD Proceeds:** $13,637,500
- **Range of Outcomes:** $13,637,500 ± $0 (zero variance)
- **Premium Cost:** $0
- **Impact on Q2 2027 Earnings:** Perfect revenue visibility; no FX variance P&L shock

**Risk Profile:**
- **Downside Risk:** Eliminated (protected against EUR depreciation)
- **Upside Opportunity:** Foregone (no participation if EUR appreciates)
- **Trade-off:** Certainty in exchange for optionality

**Management-Level Reasoning:**

1. **Cash Flow Stability**  
   The €12.5M contract is a revenue anchor for TechServe's European expansion. A forward locks in USD proceeds, enabling reliable cash flow forecasting and debt servicing. This reduces treasurer stress and improves credit metrics.

2. **Budget Certainty**  
   Finance can confidently guide Q2 2027 earnings assuming $13.64M conversion. This facilitates:
   - Quarterly guidance to analysts and investors (fewer FX surprises)
   - Budget vs. actual variance analysis (FX variance isolated and explained)
   - M&A and capital allocation planning (clear cash available)

3. **Liquidity Impact**  
   Forward contracts require **no upfront cash outlay** (unlike put premiums). A $0 cost hedge is superior to a $212.5K premium if the risk mitigation value is equivalent.

4. **Optionality Value Assessment**  
   The put's $667K potential upside (if EUR reaches 1.1420) is:
   - Unlikely (only ~5% probability of ±5% move in either direction)
   - Speculative (conflicts with TechServe's core business of tech services, not FX trading)
   - Costly ($212.5K premium = insurance premium paid for optionality)

   Treasury's role is to **eliminate hedgeable risks**, not to profit from FX moves. A forward accomplishes this at zero cost.

5. **Accounting & Audit Simplicity**  
   Forward contracts settled at maturity are straightforward:
   - Record at inception as off-balance-sheet derivative
   - No daily mark-to-market (avoid P&L volatility)
   - At settlement, record the exchange at locked rate
   - Auditors favor forwards for simplicity and hedge effectiveness documentation

6. **Competitive Positioning**  
   Competitors with effective hedging programs can guide stable revenue, strengthening investor relations and market valuation. TechServe's hedged position improves predictability.

### Cost-Benefit Summary Table:

| Factor | Forward | Put | Collar | Unhedged |
|---|---|---|---|---|
| **Upfront Cost** | $0 | ($212.5K) | −$62.5K credit | $0 |
| **Worst-Case Proceeds** | $13.64M | $13.38M | $13.38M | $12.91M |
| **Best-Case Proceeds** | $13.64M | $14.28M | $13.94M | $14.28M |
| **Earnings Visibility** | Excellent | Good | Good | Poor |
| **P&L Accounting Complexity** | Low | Medium | Medium | None |
| **Recommended?** | **✓ YES** | ✓ Alt | ✓ Alt | ✗ No |

---

## F. STRUCTURED AI PROMPT FOR SPREADSHEET REGENERATION

### Purpose:

The following prompt instructs an AI (Claude, ChatGPT, or equivalent) to generate a fully functional FX hedging Excel workbook matching the Stage 3 specification. This prompt is a **reusable template** for TechServe's treasury function—analysts can swap scenario variables (Scenario 1–4) and regenerate the model on demand.

### AI Prompt (Copy-Paste Ready):

Create a complete, production-ready Excel workbook that models hedging strategies for a EUR-denominated receivable. The workbook must include:

- Input section with named ranges (color-coded)
- Forward hedge calculation
- Money market hedge (3-step synthetic forward)
- Put option hedge
- Call option hedge (for collar construction)
- Collar hedge (put + call combined)
- Sensitivity analysis table (11 scenarios: spot movement ±5%)
- Verification checks (forward vs. money market parity, formula consistency)

**Audience:** Treasury analysts at TechServe Global  
**Required format:** Single worksheet, professionally formatted, color-coded, with clear section headers

---

## INPUT VARIABLES (USE EXACT VALUES – NO INFERENCE)

| Variable | Value | Unit / Description |
|----------|-------|---------------------|
| **FC_AMT** | 12,500,000 | Euro notional (€) |
| **S0_in** | 1.0875 | Current spot USD/EUR |
| **F0_in** | 1.0910 | 1-year forward USD/EUR |
| **R_USD** | 5.25% | US dollar interest rate (annual) |
| **R_FC** | 4.00% | Euro interest rate (annual) |
| **K_PUT** | 1.0875 | Put option strike (ATM) |
| **K_CALL** | 1.1200 | Call option strike (OTM) |
| **PREM_PUT** | 0.0170 | Put premium (USD per EUR) |
| **PREM_CALL** | 0.0220 | Call premium (USD per EUR) |
| **T_DAYS** | 365 | Time to maturity (days) |

**Important:** Do not calculate, infer, or substitute any of these values. Use them exactly as shown.

---

## NAMED RANGE CONVENTIONS

Create the following named ranges in the Excel Name Manager. These names must be usable in formulas throughout the workbook.

| Named Range | Refers To |
|-------------|-----------|
| FC_AMT | Input cell containing 12,500,000 |
| S0_in | Input cell containing 1.0875 |
| F0_in | Input cell containing 1.0910 |
| R_USD | Input cell containing 5.25% |
| R_FC | Input cell containing 4.00% |
| K_PUT | Input cell containing 1.0875 |
| K_CALL | Input cell containing 1.1200 |
| PREM_PUT | Input cell containing 0.0170 |
| PREM_CALL | Input cell containing 0.0220 |
| T_DAYS | Input cell containing 365 |

**Naming convention:** Use underscore separators. All names are UPPER_CASE.

---

## SPREADSHEET REQUIREMENTS

### Section 1: Input & Assumptions Area (Rows 1–25)

**Layout:**
- **Rows 1–2:** Section header "INPUTS & ASSUMPTIONS"
- **Rows 3–12:** Variable labels in Column A, values in Column B
- **Row 14–15:** Section header "DERIVED VALUES"
- **Rows 16–18:** Derived calculations (see below)

**Color Coding (strict):**
- **Yellow fill (RGB 255,255,0):** All input cells where user enters values (FC_AMT, S0_in, F0_in, R_USD, R_FC, K_PUT, K_CALL, PREM_PUT, PREM_CALL, T_DAYS)
- **Blue fill (RGB 0,112,192):** Assumption cells (e.g., "T_DAYS = 365" – this is a fixed assumption, not a model output)
- **Green fill (RGB 0,176,80):** Formula cells (derived values, hedge calculations, any cell containing `=`)
- **Gray fill (RGB 128,128,128):** Output cells (final USD proceeds per strategy)

**Derived Values to Calculate:**
| Derived Value | Formula |
|---------------|---------|
| **FV factor USD** | `=(1+R_USD)^(T_DAYS/365)` |
| **FV factor EUR** | `=(1+R_FC)^(T_DAYS/365)` |
| **Forward from parity** | `=S0_in * (FV_USD/FV_EUR)` |

---

### Section 2: Forward Hedge (Rows 30–45)

**Layout:**
- Row 30: Section header "FORWARD CONTRACT HEDGE"
- Row 32: Label "Forward Rate Used" → Value: `=F0_in`
- Row 33: Label "USD Proceeds (All Scenarios)" → Value: `=FC_AMT * F0_in`
- Row 34: Label "Premium Cost" → Value: `0`
- Row 35: Label "Net USD Proceeds" → Value: `=FC_AMT * F0_in`

**Color coding:** All formula cells green (except output cell gray).

**Verification note:** Add a comment in Row 37: "Forward rate locked today; no optionality; zero premium."

---

### Section 3: Money Market Hedge (Rows 50–70)

**Layout:**
- Row 50: Section header "MONEY MARKET HEDGE (Synthetic Forward)"
- Row 52: Label "Step 1: PV of EUR Receivable" → Formula: `=FC_AMT / (1+R_FC)^(T_DAYS/365)`
- Row 53: Label "Step 2: Borrow EUR (PV amount)" → Formula: `=FC_AMT / (1+R_FC)^(T_DAYS/365)`
- Row 54: Label "Step 3: Convert EUR to USD at Spot" → Formula: `= (FC_AMT / (1+R_FC)^(T_DAYS/365)) * S0_in`
- Row 55: Label "Step 4: Invest USD for 1 year" → Formula: `= (FC_AMT / (1+R_FC)^(T_DAYS/365)) * S0_in * (1+R_USD)^(T_DAYS/365)`
- Row 56: Label "Step 5: Repay EUR loan with receivable" → Label only (no formula)
- Row 57: Label "Net USD Proceeds" → Formula: `= (FC_AMT / (1+R_FC)^(T_DAYS/365)) * S0_in * (1+R_USD)^(T_DAYS/365)`

**Color coding:** All formula cells green; final output (Row 57) gray fill.

**Add comment on Row 60:** "Money market hedge replicates forward. Difference vs. forward rate indicates arbitrage or rounding."

---

### Section 4: Put Option Hedge (Rows 75–100)

**Layout:**
- Row 75: Section header "PUT OPTION HEDGE (Downside Protection)"
- Row 77: Label "Put Strike (K_PUT)" → Value: `=K_PUT`
- Row 78: Label "Put Premium (per EUR)" → Value: `=PREM_PUT`
- Row 79: Label "Total Premium Paid" → Formula: `=FC_AMT * PREM_PUT`
- Row 80: Label "Strike USD Proceeds (if exercised)" → Formula: `=FC_AMT * K_PUT`

**Payoff formula for Row 82 (Label "Payoff at Spot (S_T)"):**
- Create a sensitivity cell where user inputs S_T (reference cell E82)
- Payoff formula: `=MAX(K_PUT, S_T) * FC_AMT`

**Net USD Proceeds formula:** `= (MAX(K_PUT, S_T) * FC_AMT) - (FC_AMT * PREM_PUT)`

**Add explanatory text in Row 85:** "Put option establishes floor at K_PUT. Premium reduces net proceeds but preserves upside."

---

### Section 5: Call Option Hedge (Rows 105–130)

**Layout:**
- Row 105: Section header "CALL OPTION HEDGE (For Collar Construction)"
- Row 107: Label "Call Strike (K_CALL)" → Value: `=K_CALL`
- Row 108: Label "Call Premium (per EUR)" → Value: `=PREM_CALL`
- Row 109: Label "Total Premium Received (if sold)" → Formula: `=FC_AMT * PREM_CALL`

**Payoff formula (Row 111):** `=MIN(K_CALL, S_T) * FC_AMT`

**Note (Row 113):** "This section models a short call position (sold call). Used in collar to offset put premium."

---

### Section 6: Collar Hedge (Rows 135–165)

**Layout:**
- Row 135: Section header "COLLAR HEDGE (Put + Short Call)"
- Row 137: Label "Long Put Premium Paid" → Formula: `=FC_AMT * PREM_PUT`
- Row 138: Label "Short Call Premium Received" → Formula: `=FC_AMT * PREM_CALL`
- Row 139: Label "Net Premium (Cost) / Credit" → Formula: `=(FC_AMT * PREM_PUT) - (FC_AMT * PREM_CALL)`

**Payoff formula (Row 141):**
- Label "Collar Payoff at S_T"
- Formula: `= (MAX(K_PUT, MIN(K_CALL, S_T))) * FC_AMT`

**Net USD Proceeds (Row 143):**
- Formula: `= (MAX(K_PUT, MIN(K_CALL, S_T))) * FC_AMT + (FC_AMT * PREM_CALL) - (FC_AMT * PREM_PUT)`

**Alternative simplified:** `= Collar_Payoff + Net_Premium_Credit`

**Add note (Row 146):** "Net credit = $62,500 when S_T ≥ K_CALL. Range defined: floor at K_PUT, cap at K_CALL."

---

### Section 7: Sensitivity Analysis Table (Rows 175–210)

**Layout:**
- Row 175: Section header "SENSITIVITY ANALYSIS – USD PROCEEDS BY SPOT RATE"
- Row 177: Column headers:

| A | B | C | D | E | F |
|---|---|---|---|---|---|
| Scenario | Spot Rate (S_T) | Unhedged | Forward | Put Option | Collar |

**Spot Rate scenarios (Rows 178–188):**

| Row | Scenario | Spot Rate | Formula |
|-----|----------|-----------|---------|
| 178 | −5.0% | `=S0_in * (1-0.05)` | |
| 179 | −4.0% | `=S0_in * (1-0.04)` | |
| 180 | −3.0% | `=S0_in * (1-0.03)` | |
| 181 | −2.0% | `=S0_in * (1-0.02)` | |
| 182 | −1.0% | `=S0_in * (1-0.01)` | |
| 183 | 0% (Base) | `=S0_in` | |
| 184 | +1.0% | `=S0_in * (1+0.01)` | |
| 185 | +2.0% | `=S0_in * (1+0.02)` | |
| 186 | +3.0% | `=S0_in * (1+0.03)` | |
| 187 | +4.0% | `=S0_in * (1+0.04)` | |
| 188 | +5.0% | `=S0_in * (1+0.05)` | |

**Formula references for each column:**

- **Unhedged (Column C):** `=FC_AMT * [Spot Rate cell]`
- **Forward (Column D):** `=FC_AMT * F0_in` (identical for all rows)
- **Put Option (Column E):** `=(MAX(K_PUT, [Spot Rate cell]) * FC_AMT) - (FC_AMT * PREM_PUT)`
- **Collar (Column F):** `=(MAX(K_PUT, MIN(K_CALL, [Spot Rate cell])) * FC_AMT) + (FC_AMT * PREM_CALL) - (FC_AMT * PREM_PUT)`

**Formatting:** Use green fill for all formula cells. Add conditional formatting to highlight the worst-case and best-case USD proceeds per column.

---

### Section 8: Verification Checks (Rows 220–240)

**Layout:**
- Row 220: Section header "VERIFICATION CHECKS"
- Row 222: Label "Forward Rate from Interest Rate Parity" → Formula: `=S0_in * ((1+R_USD)^(T_DAYS/365) / (1+R_FC)^(T_DAYS/365))`
- Row 223: Label "Given Forward Rate (F0_in)" → Value: `=F0_in`
- Row 224: Label "Difference (Parity Check)" → Formula: `=ABS([Forward from parity] - F0_in)`
- Row 225: Label "Parity Pass/Fail" → Formula: `=IF([Difference] < 0.0001, "PASS", "FAIL")`

**Additional check (Row 227):**
- Label "Money Market vs. Forward Difference"
- Formula: `=[Money Market Net Proceeds] - (FC_AMT * F0_in)`
- Tolerance: Difference < 0.1% of notional → acceptable

**Add check (Row 229):**
- Label "Put-Call Parity (Collar) Check"
- Formula: `= ([Put Premium] + K_CALL) vs. ([Call Premium] + K_PUT)` — conceptual check only

---

### Section 9: Summary Output Table (Rows 245–260)

**Layout:**
- Row 245: Section header "HEDGE STRATEGY SUMMARY – BASE CASE (S_T = S0)"
- Create a clean summary table:

| Strategy | USD Proceeds | Upfront Cost | Downside Protected? | Upside Captured? |
|----------|--------------|--------------|---------------------|------------------|
| Unhedged | [formula] | $0 | No | Yes |
| Forward | [formula] | $0 | Yes (full) | No |
| Put Option | [formula] | [formula] | Yes (floor) | Yes |
| Collar | [formula] | [formula] | Yes (floor) | Capped |

**Color coding:** Output cells (USD Proceeds column) = gray fill. All other cells = green fill (formulas) or yellow fill (if manual entry required).

---

## HIERARCHICAL STRUCTURE REQUIREMENTS

Organize the worksheet using **bold section headers** with consistent formatting:

- **Font:** Calibri, 12pt for body, 14pt bold for section headers
- **Section header format:** Dark blue text, light gray background, underline
- **Row grouping:** Insert a blank row (height = 5) between each major section

**Section order (top to bottom):**
1. INPUTS & ASSUMPTIONS
2. FORWARD CONTRACT HEDGE
3. MONEY MARKET HEDGE
4. PUT OPTION HEDGE
5. CALL OPTION HEDGE
6. COLLAR HEDGE
7. SENSITIVITY ANALYSIS
8. VERIFICATION CHECKS
9. HEDGE STRATEGY SUMMARY

---

## EXPORT FORMAT

Generate the workbook in **Excel (.xlsx) format** with:

- One worksheet named "FX_Hedging_Model"
- All formulas live (no hard-coded values except inputs)
- Named ranges defined in Name Manager
- Conditional formatting applied to sensitivity table (color scale: green = high proceeds, red = low proceeds)
- Print area set to Rows 1–260, Columns A–F
- Page layout: Landscape orientation, fit to 1 page wide

---

## FINAL VERIFICATION CHECKLIST

Before delivering the spreadsheet, confirm:

- [ ] All input values match the table in Section 2 exactly (no inferred or rounded values)
- [ ] Named ranges are case-sensitive and use underscores
- [ ] Color coding matches specification (Yellow = Inputs, Blue = Assumptions, Green = Formulas, Gray = Outputs)
- [ ] Forward hedge locks proceeds at `FC_AMT * F0_in`
- [ ] Money market hedge includes all 5 steps with visible formulas
- [ ] Put option payoff uses `MAX(K_PUT, S_T)`
- [ ] Collar payoff uses `MAX(K_PUT, MIN(K_CALL, S_T))`
- [ ] Sensitivity table has 11 rows with formulas referencing S0_in dynamically
- [ ] Verification checks include parity validation
- [ ] No circular references
- [ ] No #REF! or #NAME? errors

**Deliverable:** A single Excel file ready for TechServe treasury analysts to use with Scenario 3 data.
---
## Extra Credit: Areas for Further Study & Improvement

### 1. AI Skills & Automation – Live Market Data, On‑Demand Rebuilding, and Monte Carlo Simulations

The structured prompt developed in Stage 4 is the foundation for a fully automated FX hedging engine. By integrating AI tools (e.g., Claude Skills or ChatGPT Code Interpreter) with live market data APIs (Bloomberg, Refinitiv, OANDA, ECB), TechServe's treasury team could:

- **Pull real‑time data** – spot rates, forward points, interest rate curves – and automatically populate the named ranges (`S0_in`, `F0_in`, `R_USD`, `R_FC`, etc.).
- **Regenerate the model on demand** – daily or weekly – without manual entry, using the exact same prompt template.
- **Run Monte Carlo simulations** – model thousands of EUR/USD paths (geometric Brownian motion with realistic volatility) and output probability distributions of USD proceeds for each hedge strategy. The AI could then recommend a strategy based on user‑defined risk tolerance (e.g., “minimize 5% value‑at‑risk”). This turns a static spreadsheet into an adaptive, data‑driven risk management tool.

**Connection to the project:** The prompt already defines all variables and sensitivity ranges. Automating data ingestion and probabilistic simulation would elevate the analysis from deterministic scenarios to robust risk‑adjusted decision support.

---

### 2. Multi‑File Reasoning – Maintaining Consistency Across Spec, Model, and Prompt

AI models with extended context (Claude 3.5 Sonnet, ChatGPT with file uploads) can read **three artifacts simultaneously** – the Stage 1–3 specification, the Stage 4 prompt, and the generated Excel workbook – to ensure consistency.

- **Cross‑reference checking:** The AI can verify that the spec’s exposure (€12.5M, 12 months, Scenario 3 data) matches the prompt’s input variables and the model’s formulas. Discrepancies (e.g., interest rate differential rounding) are flagged and corrected.
- **Automated model rebuilds:** If TechServe signs a new €15M, 6‑month contract, the analyst updates only the spec file. The AI reads the new spec, infers changed variables (`FC_AMT = 15,000,000`, `T_DAYS = 180`), and regenerates a complete workbook while preserving all formula logic and formatting.
- **Dashboard generation:** The AI can create a Power BI or Excel Power Query dashboard that pulls historical hedging outcomes from multiple regeneration runs, showing actual USD proceeds vs. locked‑in forward rates over time – a powerful feedback loop for treasury performance.

**Connection to the project:** The structured prompt is already designed as a reusable template. Multi‑file reasoning enables seamless adaptation to new exposures without re‑writing the entire model.

---

### 3. GitHub & Version Control – Auditability and Reproducible Model Regeneration

Committing the Stage 1–3 specs, the Stage 4 prompt, and the generated Excel workbook to a **GitHub repository** creates an immutable, timestamped record of every decision and calculation.

- **Reproducibility:** An auditor clones the repo, re‑runs the exact prompt using an AI with the same configuration, and regenerates the model. If the output matches the committed workbook, the hedge accounting entries (e.g., the $13,637,500 forward value) are validated.
- **Change tracking:** GitHub’s diff view shows exactly which inputs changed and when – critical for hedge effectiveness testing under ASC 815. The spot and forward rates on the designation date are traceable back to the committed spec.
- **Collaboration & approval:** Pull request workflow allows the treasury analyst to propose a new model version, the CFO to review the changed prompt, and only after approval can the model be regenerated and merged. This prevents unauthorized changes.
- **Audit evidence:** The repository becomes a legally defensible record that TechServe followed a systematic, documented, and reproducible hedging process – superior to scattered emails or one‑off spreadsheets.

**Connection to the project:** Stages 1–3 document the qualitative reasoning (exposure analysis, market scenarios, strategy design). GitHub ties that reasoning to the quantitative implementation (the prompt and Excel model), creating a closed‑loop audit trail.

---

### 4. Accounting & Audit Integration – Hedge Documentation, OCI vs. P&L, and GitHub as Evidence

The project’s hedge strategies have distinct accounting treatments under IFRS 9 or ASC 815. The structured prompt can be extended to enforce compliance.

- **OCI vs. P&L impact:** For the recommended forward contract (cash flow hedge), the AI could generate two additional columns: “OCI impact (mid‑period)” and “P&L impact at settlement,” showing how earnings volatility is smoothed.
- **Option accounting flag:** For the put option (if not designated as a hedge), the AI would automatically flag that the $212,500 premium is immediately recognized in P&L – a disadvantage – and add a note: “Consider effectiveness testing to qualify for hedge accounting.”
- **Documentation requirements:** ASC 815 requires contemporaneous documentation of the hedging relationship, risk management objective, and effectiveness assessment. The GitHub repository (timestamps, commit messages) serves as digital audit evidence that documentation was prepared before or at hedge inception. The Stage 4 markdown file – containing executive recommendation, rationale, and market data snapshot – is a perfect “memorandum to file.”
- **Reproducibility for audits:** An auditor takes the exact prompt from GitHub, runs it through an AI using the same market data snapshot, and verifies that the model’s outputs match the journal entries. If TechServe uses a third‑party AI service, auditor review of system logs (if available) confirms no unauthorized modifications.

**Connection to the project:** Combining AI‑driven spreadsheet generation with GitHub version control transforms a one‑off hedging analysis into an auditable, repeatable, and compliant treasury workflow – directly aligned with the executive recommendation and Stage 4’s focus on risk mitigation and budget certainty.


