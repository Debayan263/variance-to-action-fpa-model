# Variance-to-Action FP&A Model

A driver-based FP&A model for a **fictional Indian D2C company** (~₹400 crore revenue). It builds an FY27 budget, compares actuals to a flexed budget, classifies every material variance as **Timing, One-off or Structural**, attaches an action (**Reforecast, Cut spend or Ignore**) and rolls the forecast forward.

> **Disclaimer:** the company is fictional. All history and the Apr–Sep 2026 actuals are synthetic. Cost ratios are benchmarked to public annual-report data from Honasa Consumer (FY26); no real company financials are represented.

**File:** `Variance_to_Action_FPA_Model.xlsx` (9 sheets, about 4,200 formulas, zero formula errors)

---

## 1. The problem it answers

Most budget-vs-actual reports stop at "we are ₹X over". An FP&A analyst has to answer the next question: **what should we do about it?** A late festive campaign, a one-time IT project and a permanent courier price rise can all show up as the same overspend, but they call for three different responses. This model makes that decision explicit and carries it into the forecast.

## 2. Workbook structure

| Sheet | What it does |
|---|---|
| Cover | Snapshot, sheet map, colour code |
| Executive Dashboard | KPI tiles and four live charts: YTD EBITDA bridge, FY27 forecast-vs-budget walk, variance by cause, monthly EBITDA margin |
| Historical Data | 24 months (Apr-24 to Mar-26) across Sales, Operations, Marketing, HR, IT and Finance: orders, AOV, revenue, COGS, 14 cost lines, headcount, operating metrics |
| Assumptions & Budget | Every driver in its own labelled cell; monthly FY27 budget built from them |
| Actual vs Budget | Actuals input, flexed budget, ₹ variances (favourable = positive), revenue volume vs price split |
| Variance-to-Action Log | Materiality test, cause classification, suggested action, analyst override, final action |
| Rolling Forecast | Actuals to date plus a forecast re-based for the log's decisions |
| Summary | YTD result, FY27 outlook, log statistics, largest adverse variances, integrity checks |
| Model Notes | Short method notes inside the workbook |

## 3. Benchmark: Honasa Consumer FY26

Honasa (Mamaearth, The Derma Co) is a D2C-born listed company that reports advertising, employee cost and D&A as separate lines. I used its ratios as **reference ranges**, not values to copy.

| Ratio | Honasa FY26* | Model FY26 | Model FY25 |
|---|---|---|---|
| Gross margin | ~70% | 68.9% | 67.0% |
| Advertising / marketing % of revenue | ~33% | 33.0% | 33.9% |
| Employee cost % of revenue | ~11% | 11.0% | 11.1% |
| Freight & forwarding / fulfilment % of revenue | ~7.6% | 7.5% | 7.2% |
| D&A % of revenue | ~1.9% | ~2.0% | ~2.1% |
| EBITDA margin | ~9.9% | 10.0% | 6.4% |

\*Checked against Honasa's audited consolidated FY26 results filed with NSE on 21 May 2026 (₹ lakh: revenue 2,39,194; advertisement 78,809; employee 26,264; freight 18,214; D&A 4,440). Gross margin uses purchases of stock-in-trade adjusted for inventory change as cost of goods. EBITDA = profit before exceptional items and tax + finance costs + D&A − other income. These are the same audited numbers the annual report carries, but I did not open the annual report PDF itself.

**Why the model differs from Honasa on purpose:** Honasa is about 6x larger, runs several brands and has a large offline mix. A single-brand ₹400 crore D2C company would typically carry heavier marketing intensity. The monthly ratios also move around the benchmark, because a model with exact ratios every month could never produce a variance worth classifying.

## 4. Method

**Budget.** Orders = FY26 orders × (1 + growth) × seasonality. AOV grows monthly from the Mar-26 level. COGS, marketplace fees and marketing are percentages of revenue; fulfilment is cost per order; personnel is planned headcount × cost per head; other lines are the FY26 monthly average × (1 + growth). FY27 budget revenue is about ₹453 crore.

**Flexed budget.** Variable lines (COGS, marketplace fees, fulfilment) are scaled to actual revenue or orders, so extra volume is not mistaken for cost inefficiency. Discretionary marketing is *not* flexed, so overspend stays visible.

**Sign convention.** Every variance is signed so that positive is favourable and negative is unfavourable.

**Materiality.** A line is flagged if either the YTD variance or the recent run-rate variance (last 3 months) breaches both a % threshold (5%) and a ₹ threshold (₹25 lakh). The run-rate test catches problems that only started recently.

**Classification and action.**

| Cause | Meaning | Default action |
|---|---|---|
| Timing | Reverses within the year | Ignore (the reversal is built into the forecast) |
| One-off | Non-recurring | Ignore (excluded from run-rate) |
| Structural | Changes the run-rate | Reforecast |

The analyst can override the default, but **a written reason is required**; the log flags any override without one.

**Rolling forecast.** Closed months use actuals. Open months = budget × volume factor × (1 + adjustment from the log). Reforecast applies the recent variance % to the line. Cut spend applies it net of a recovery assumption (50%). Timing variances reverse evenly over the next 2 months. One-offs do not carry forward.

## 5. Worked examples (from the simulated Apr–Sep 2026 actuals)

**Timing: performance marketing.** Spend ran 8% over budget in August and 17% over in September, because the Diwali campaign was pulled forward. The YTD variance was only −3.8%, below the 5% threshold, but the recent run-rate variance was −8.4%, so the **run-rate test** flagged it. Classified as Timing, the action is Ignore, and the forecast cuts the next two months by the ₹171 lakh pulled forward. Full-year performance marketing lands exactly on budget.

**Structural: fulfilment.** Cost per order rose about 9% from June after a courier rate revision. Against the flexed budget, the YTD variance is −₹95 lakh (−5.9%). Classified as Structural, the action is Reforecast, and the remaining months are raised by the recent run-rate (about +8.5%).

**Override: brand and influencer.** Creator retainers stepped up from June, a −₹197 lakh YTD variance (−9.3%). The default for a structural cause is Reforecast, but the line is discretionary, so the analyst overrode it to **Cut spend**, with the reason documented, and the forecast assumes half of the overspend is recovered.

## 6. Results of the simulated year to date

- Revenue is 0.9% ahead of budget (volume +₹351 lakh, offset by price/mix −₹158 lakh).
- YTD EBITDA is about ₹413 lakh (18%) below budget: a ₹722 lakh operating-cost overrun outweighs a ₹309 lakh gross-profit gain.
- 8 material variances: 5 Structural, 2 One-off, 1 Timing.
- FY27 rolling-forecast EBITDA margin is about 11.3%, against 11.8% in the budget.

## 7. Limitations

- All data is synthetic, so the model shows method, not real-world calibration.
- Revenue timing variances are not reversed in the forecast; headcount and operating metrics are not forecast.
- Seasonality is one index shared across years, and cost per head is blended within each cost centre.
- It is a P&L-level model: no balance sheet or cash flow.
- Deliberately excluded: scenario analysis, LBO/DCF, AI-generated forecasts, Power BI and macros. One compact dashboard of four charts is included.

## 8. Using the model

1. Enter the month's actuals in Block 1 of **Actual vs Budget** (blue cells).
2. Move "Actuals loaded through" in **Assumptions & Budget**.
3. In the **Variance-to-Action Log**, classify any new material line and add overrides with reasons.
4. Read **Summary** and **Rolling Forecast**.

Colour code: blue = input, black = formula, green = link from another sheet, yellow fill = key assumption.
