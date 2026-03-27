# Activity Profit Pool Margin Proxy Estimates

This file provides a proxy operating-margin estimate for each semiconductor activity and converts TAM to estimated operating profit pool.

## How the estimate is derived
1. For each activity, select participating companies (participates=1) from `semiconductor_activity_matrix_long.csv`.
2. Pull each participant's latest full-year company operating margin % (from the linked 10-K/20-F/annual report URLs in the long file).
3. Compute revenue-weighted average margin across participants using activity revenue estimate as weight.
4. Compute median and best-performer participant margin for triangulation.
5. Use a proxy activity margin equal to the weighted average, constrained to not exceed the best performer and not be below median.
6. Profit pool = estimated activity TAM × proxy activity margin.

## Why this is a proxy (not disclosed segment margin)
- Most companies do not publish operating margin by the exact activity taxonomy used in this project.
- Company-wide operating margin from filings is the most consistently available primary metric across all 16 companies.
- Therefore, this method uses comparable-company economics as a practical benchmark for activity margin.

## Output file
- `activity_profit_pool_estimates.csv` with activity-level margin proxies, profit pools, and all source links used.

## Note on requested reference file
- `profit pools.csv` was not found in the repository at generation time, so this method was implemented directly from the available project datasets and filing links.
