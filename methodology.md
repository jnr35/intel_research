# Methodology

## Research process
1. Define canonical company and activity taxonomy.
2. Pull latest full-year company financials from primary filings (10-K/20-F/annual reports).
3. Normalize revenues to USD billions and margins to percentages.
4. Estimate activity-level revenue using disclosed segments, product commentary, and TAM-share triangulation.
5. Build long-form machine-readable table first, then wide matrix.

## Source hierarchy
1. Primary filings and investor relations annual materials.
2. Earnings presentations/shareholder letters.
3. Industry trackers (IDC, Gartner, TrendForce, JPR, SEMI, IFR).
4. Explicitly labeled estimates where direct splits are unavailable.

## Fiscal year normalization logic
- Use each company’s most recent full fiscal year available as of 2026-03-27.
- Cross-company comparison is directional because fiscal-year end dates differ.

## Currency normalization logic
- Non-USD reporters (TSMC, Samsung, SMIC) converted to USD using annual average FX assumptions and rounded.

## Margin normalization logic
- Operating margin = operating income / revenue.
- If a company reports equivalent metrics under different standards, operating margin is standardized to the closest comparable operating-income definition.

## Diversified-company treatment
- Apple, Amazon, Google, Microsoft, Samsung, IBM: keep total company revenue and margin intact, then estimate semiconductor-attributable activity revenue separately using disclosed silicon programs, disclosed segment exposure, and market-share benchmarks.

## Activity-specific revenue estimation
- Assign each disclosed segment/sub-segment to a primary activity bucket.
- Use unit-share and TAM-share checks to avoid implausible allocations.
- Values are estimates when companies do not disclose exact activity-level revenue.

## Rules for participates = 0 or 1
- participates=1 if the company has current commercial products/services materially tied to the activity.
- participates=0 if no meaningful direct commercial footprint is identified in the latest period.

## Overlap handling
- Data Center GPUs vs AI/ML Accelerators: data-center GPUs in GPU bucket; custom AI ASICs and AI-focused acceleration in AI/ML bucket.
- HPC & Scientific Computing vs Data Center GPUs: HPC is separated for supercomputing-specific deployments; avoid re-counting by assigning primary use-case.
- Edge AI vs Embedded Systems: embedded MCU/SoC baseline in Embedded; edge inference acceleration in Edge AI.
- Automotive Infotainment vs Autonomous Vehicles & ADAS: cockpit/IVI in infotainment; ADAS/AV compute in autonomous.

## Known limitations and uncertainty
- Activity splits are modeled estimates for most companies.
- Some TAM sources use differing market boundaries; harmonization introduces uncertainty.
- Non-public transfer-pricing economics for internal silicon (hyperscalers) are approximated.

## Activity margin and profit-pool estimation (new)
- Added `activity_profit_pool_estimates.csv` to estimate per-activity operating margin proxies.
- For each activity, participating companies were selected from the long matrix (`participates=1`).
- Proxy margin is based on a revenue-weighted average of participant company operating margins from latest filings, then triangulated with participant median and best performer.
- Estimated activity operating profit pool is computed as: `estimated_TAM_usd_bn * proxy_operating_margin_used_pct`.
- This is explicitly a comparable-company proxy because exact activity-level operating margins are not broadly disclosed in 10-K/20-F reporting.

