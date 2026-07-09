# Strait of Hormuz Crisis: Oil Flow, LNG Flow, Ship Traffic, and Brent Prices

### Political-Economic Impact Analysis

A portfolio data analysis project combining political science and data analysis to examine how the 2026
Strait of Hormuz crisis is reflected in crude oil flow, LNG flow, ship traffic, and Brent crude oil prices.

## 1. Project Summary

This project asks whether the crisis around the Strait of Hormuz is visible in physical energy flows, ship
traffic, and Brent oil prices, and what those patterns suggest politically and economically. It is a
**descriptive, evidence-based political-economy analysis** — not a causal model, not a forecasting tool, and
not built on machine learning. All quantitative claims are traced back to four source datasets; news sources are
used only to label political benchmark dates and provide context.

## 2. Research Question

How did the Strait of Hormuz crisis affect crude oil flows, LNG flows, ship traffic, and Brent crude oil prices
across the war onset, peak disruption, ceasefire, and renewed-tension periods?

## 3. Why the Strait of Hormuz Matters

The Strait of Hormuz is one of the world's most important maritime oil and gas chokepoints, connecting Persian
Gulf producers to global markets (see EIA background: https://www.eia.gov/international/analysis/special-topics/World_Oil_Transit_Chokepoints).
A sustained disruption there has the potential to affect global energy security, shipping and insurance risk,
and — via oil prices — inflation and supply-chain conditions well beyond the region.

## 4. Data Sources

| Dataset | Role | Frequency | Coverage used in this analysis |
|---|---|---|---|
| `crude_oil_export_voy_intake_index.csv` | Crude oil flow indicator | Daily | 2025-01-01 to 2026-07-08 |
| `lng_export_voy_intake_index.csv` | LNG flow indicator | Daily | 2025-01-01 to 2026-07-08 |
| `arrivals-of-ships.csv` | Ship traffic indicator (5 vessel categories) | Daily | 2019-01-01 to 2026-07-05 |
| `RBRTEd.xls` (EIA, Europe Brent Spot FOB) | Market price / response variable | Trading days | 1987-05-20 to 2026-06-29 |

News sources (Reuters, CNBC, AP News) are used only for political context and benchmark labeling, never as
quantitative data. Source hierarchy: uploaded datasets = primary empirical evidence; Reuters = primary political
and maritime event context; EIA = official chokepoint background; AP/CNBC = supporting market and political
context.

## 5. Political Benchmark Timeline

| Date | Event | Data support after check |
|---|---|---|
| 2026-02-28 | War / disruption onset | visible |
| 2026-03-03 | Shipping disruption visible / peak disruption begins | visible |
| 2026-04-08 | Ceasefire announcement / fragile pause | partially visible |
| 2026-07-08 | Ceasefire breakdown / renewed tensions | cannot assess due to data range |

## 6. Hypotheses

- **H1 — Energy flow disruption:** crude oil and LNG flow indicators decline during the crisis vs. the pre-war baseline.
- **H2 — Ship traffic disruption:** ship arrivals decline, with tankers expected to be more affected than other categories.
- **H3 — Brent market reaction:** Brent price, returns, and volatility move more strongly during escalation/peak disruption.
- **H4 — Price-flow divergence / risk premium:** if Brent normalizes while flow stays weak, this may suggest expectations/risk-premium pricing.
- **H5 — Political-economic transmission framework:** an interpretive framework connecting H1-H4 to energy security, chokepoint risk, market risk, and broader vulnerability channels.

## 7. Methodology

All analysis is in a single notebook, `01_hormuz_crisis_full_analysis.ipynb`, run top to bottom in one
continuous flow: load and inspect each dataset -> clean and standardize to a common `date` column -> build a
political benchmark timeline -> label every row with an analysis period (P0 pre-war baseline, P1 war onset, P2
peak disruption, P3 ceasefire/fragile normalization, P4 ceasefire breakdown) -> compute descriptive statistics,
percentage changes, and simple correlations per hypothesis -> synthesize into an evidence matrix. No machine
learning, GARCH, Granger causality, or advanced econometrics are used, by design.

## 8. Key Findings

1. Crude oil and LNG flow collapsed by roughly 95-99% at peak disruption and did not recover during the ceasefire period.
2. LNG's collapse appears earlier and more complete than crude oil's.
3. Ship traffic fell broadly (~94% at peak) across all 5 vessel categories, not primarily in tankers.
4. Brent price rose ~58% and return volatility roughly tripled at peak disruption, then only partially eased during the ceasefire.
5. Physical flow and Brent price diverge during the ceasefire period -- consistent with, though not proof of, risk-premium or expectations-driven pricing.
6. Flow-vs-price correlation looks like a shared regime shift (strong level correlation, near-zero return correlation), not a tight day-to-day relationship.
7. The most recent reported escalation (2026-07-08) falls outside the Brent and ship-arrivals data ranges and cannot be verified quantitatively in this project.

See Section 12 of the notebook for the full findings list with supporting numbers.

## 9. Evidence Matrix Summary

| Hypothesis | Verdict |
|---|---|
| H1 - Energy flow disruption | Supported |
| H2 - Ship traffic disruption | Partially supported |
| H3 - Brent market reaction | Supported for escalation/peak; not directly testable for the 2026-07-08 marker |
| H4 - Price-flow divergence / risk premium | Partially supported |
| H5 - Political-economic transmission framework | Not directly testable / interpretive framework |

Full detail (dataset, indicator, method, evidence, interpretation, limitation) is in
`05 Reports/tables/evidence_matrix.csv` and Section 11 of the notebook.

## 10. Political-Economic Interpretation

The findings are consistent with a severe, broad disruption to Hormuz-linked energy flow and shipping, and with
markets pricing meaningfully higher risk during the acute phase of the crisis. They are also consistent with
several downstream political-economic risk channels commonly discussed for maritime chokepoints -- energy
security exposure for import-dependent economies, elevated shipping and insurance risk, potential inflationary
pressure transmitted through oil prices, and supply-chain uncertainty (see Section 10 and
`political_economic_transmission_framework.csv`). These are stated as interpretations consistent with the data,
not as proven causal claims, and downstream effects like inflation or insurance pricing are not directly tested
here.

## 11. Limitations

See Section 13 of the notebook for the full list. The most important ones: political benchmark dates are not
causal proof; Brent data ends 2026-06-29, before the 2026-07-08 benchmark, so the most
recent reported escalation cannot be verified in this data; `arrivals-of-ships.csv` has no geography metadata;
correlation is not causation; and this project does not control for other global oil-market shocks.

## 12. How to Reproduce

1. Clone this repository and install the packages in `requirements.txt` (`pip install -r requirements.txt`).
2. Place the four source files in `02 Data/original/` using the names referenced in the notebook (or the
   closest-matching files, as described in Section 2).
3. Open `01_hormuz_crisis_full_analysis.ipynb` and run all cells top to bottom.
4. Cleaned datasets are written to `02 Data/prepared/`, figures to `05 Reports/figures/`, tables to
   `05 Reports/tables/`, and this README/LinkedIn draft to `05 Reports/`.

Note: `RBRTEd.xls` is a legacy Excel format; the notebook tries `xlrd` first and falls back to a pre-extracted
CSV mirror if `xlrd` is not installed, so it should run in most standard Python/Jupyter environments.

## 13. Suggested Next Steps

- Extend the Brent series once EIA publishes data through the 2026-07-08 benchmark and beyond, to actually test the renewed-tension market reaction.
- Obtain port/geography metadata for the ship-arrivals data to confirm (or replace) it as a Hormuz-specific traffic indicator.
- Add an LNG price series if one becomes available, to test LNG market reaction alongside physical flow.
- Consider a weekly-resampled version of the analysis as a robustness check against the daily results.
