# Infosys Ltd (NSE: INFY) - Stock Valuation Model

A full DCF + relative valuation model built in Excel, using real 5-year financials for
**Infosys Ltd**, one of India’s largest IT services companies. 

---

## Headline result

| **Intrinsic Value / Share (Base Case)** | ₹1,018 |
| --- | --- |
| **Current Market Price** (16-Jul-2026) | ₹1,183 |
| **Implied Upside/(Downside)** | -13.9% |
| **WACC** | 13.2% |
| **Terminal Growth (g)** | 4.0% |
| **Terminal Value as % of EV** | 67.4% |
| **Peer P/E Comps Value/Share** | ₹1,388 |
| **Peer EV/EBITDA Comps Value/Share** | ₹1,381 |

(All figures are outputs of the model , change any assumption on the Inputs tab and every
number above recalculates. This is a training/portfolio exercise, not investment advice.)

---

## Folder structure

```
stock-valuation-model/
├── data/
│   └── Infosys_raw_financials.xlsx    ← raw P&L, Balance Sheet, Cash Flow, peer comps
├── model/
│   └── Infosys_DCF_Model.xlsx   ← the main workbook (Inputs → Historicals → Beta Calc →
│                                    Forecast → DCF → Comps → Output)
├── output/
│   └── valuation_summary.pdf    ← one-page KPI + football field export
│           
└── README.md                  
```

## How the model is built

| Tab | What it does |
| --- | --- |
| **Inputs** | Every assumption in one place - revenue growth, margins, tax rate, WACC build (CAPM), terminal growth, and a Bull/Base/Bear scenario toggle. |
| **Historical** | FY2021A–FY2026A actuals pulled from `data/Infosys_raw_financials.xlsx`, plus the ratio analysis (growth %, margins, cost of debt) that feeds the forecast. |
| **Beta Calc** | 5-year weekly INFY vs NIFTY 50 returns and a `SLOPE()` regression to derive beta. |
| **Forecast** | 5-year (FY27E–FY31E) driver-based P&L and Free Cash Flow to Firm (FCFF) .  |
| **DCF** | Discounts the explicit FCFF, adds a Gordon Growth terminal value, bridges Enterprise Value → Equity Value → Value per Share, and a WACC × terminal-growth sensitivity grid. |
| **Comps** | Peer P/E and EV/EBITDA multiples (TCS, HCLTech, Wipro, Tech Mahindra) applied to Infosys forward numbers, as a cross-check on the DCF. |
| **Output** | The one-page summary - KPI row, and a football-field chart comparing DCF, both comps methods, and the current price. |

## Output

<img width="1390" height="856" alt="image" src="https://github.com/user-attachments/assets/a65a4b69-7414-4a3d-b08f-61df4ad9324f" />


## Data sources

- **Financial statements (FY2021-FY2026):** Screener.in, accessed 18-Jul-2026  Infosys’ free, exportable Consolidated P&L, Balance Sheet, Cash Flow and ratios.
- **Peer comps (TCS, HCLTech, Wipro, Tech Mahindra):** Screener.in company pages, accessed 16 -18 Jul 2026.
- **Weekly price series for the beta regression:** Investing.com -5Y weekly regression, INFY vs Nifty 50, 09-Aug-2021 to 09-Aug-2026

## Key assumptions (Base Case)

- Revenue growth tapers from ~10% (FY27E) to 6% (FY31E, terminal-ish rate), reflecting FY26A actual growth of 9.6% decelerating toward the industry’s long-run rate.
- EBITDA margin expands gradually from 23.8% to 24.5%, in line with Infosys own “Project Maximus” efficiency commentary.
- WACC = 13.2% (Cost of Equity 13.4% via CAPM with β≈0.91, Rf 6.8%, ERP 7.3%; post-tax Cost of Debt 3.5%; ~98% equity-weighted capital structure).
- Terminal growth = 4.0% Kept ≤ long-run India nominal GDP growth ,maintains >8 pt spread to WACC per Gordon Growth convention.

## Known simplifications

- **Net Working Capital** is proxied from Screener’s “Working Capital Days” ratio (Revenue ×
Days ÷ 365) rather than a full receivables/payables schedule, since the free Screener export
doesn’t break those out separately.
- **Capex** isn’t a separate published Screener line; it’s derived as Cash from Operating
Activity − Free Cash Flow (both of which Screener does publish).
- **Comps “EPS”** uses forecast NOPAT (unlevered) rather than reported net income, to stay
consistent with the unlevered FCFF build used in the DCF.
- **Peer EBITDA margins** are estimates, not pulled line-by-line from each peer’s own P&L

## Tools used

Excel,  Screener.in for source data , GitHub for hosting.

## What this project demonstrates

- 3-statement linkage and driver-based forecasting
- WACC derivation from first principles (CAPM, beta regression, capital weights)
- Terminal value mechanics and why it dominates the answer
- Two-way sensitivity analysis
- Cross-checking a DCF against peer trading multiples like a working analyst

## Color Convention

| **Color** | **Meaning** |
| --- | --- |
| Blue text | A hardcoded input - a typed number , sourced from Screener or a market data provider |
| Black text | A formula that calculates something from other cells |
| Green text | A formula that links to a different tab |
| Yellow fill | A key assumption  |
