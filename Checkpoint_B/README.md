# MSDS 451 — Term Project Checkpoint B

## Machine Learning–Enhanced Adaptive Momentum ETF

This checkpoint documents the market data and preliminary analysis for the six-product investment universe (SPY, XLF, XLV, IEF, GLD, SHY). It continues the investment philosophy introduced in Checkpoint A.

**Checkpoint B is data preparation, not a strategy backtest.** The saved monthly allocations are a *signal preview*, not executed trades, realized strategy returns, or evidence that the ML component outperforms a baseline.

## Files

- `Checkpoint_B_Research_Report.pdf` — report, tables, charts, citations, and limitations.
- `Checkpoint_B_Data_Preparation.ipynb` and `Checkpoint_B_Data_Preparation.html` — executed notebook and HTML export.
- `data/raw/` — original Yahoo Finance daily history per product.
- `data/processed/` — aligned adjusted prices, daily simple/log returns, `source_download_provenance.json`, and `data_provenance.json`.
- `outputs/tables/` — coverage, risk/return, correlation, monthly signal previews, and lookback sensitivity.
- `outputs/figures/` — adjusted-return proxy, SPY drawdown, and correlation heat map.
- `requirements.txt` — required Python packages.

## Data and methodology

Data were obtained on October 26, 2026 from Yahoo Finance via `yfinance`. We use `Adj Close` as an *approximation* to distributions-reinvested total return, and do not claim independent provider data auditing. The common window is November 18, 2004 through October 26, 2026 (5,518 daily price observations, 5,517 daily returns). The first full 200-day momentum/trend signal is in 2005. Historical single-ETF risk metrics are not returns for the proposed actively managed fund.

The notebook uses:
- `100 * ln(AdjClose[t] / AdjClose[t-1])` for percentage log returns.
- Sample daily standard deviation multiplied by `sqrt(252)` for annualized volatility.
- 126-trading-day returns plus a 200-day simple moving average for the main signal preview.
- 63-, 126-, and 252-day lookbacks for signal sensitivity; these are not backtests.

October 26, 2026 is **not a complete month end**. The reproducibility-adjusted notebook excludes October 2026 from completed month-end signals. September 30, 2026 is the final completed monthly decision date.

## How to run and test

1. Clone the public term-project repository and open this checkpoint folder in Jupyter.
2. Install packages: `python -m pip install -r requirements.txt`
3. Run `Checkpoint_B_Data_Preparation.ipynb` from top to bottom with `DOWNLOAD_FRESH=False` (the archived raw data are provided). This requires no internet and reproduces the original market-data vintage.
4. To refresh prices from Yahoo Finance, set `DOWNLOAD_FRESH=True`. Refreshed prices will change the analysis date and may change the statistics.
5. Inspect the CSV results in `outputs/tables/` and images in `outputs/figures/`.
6. Check that the aligned dataset has 5,518 rows and no missing values, that simple/log returns agree with the adjusted-price ratios, that all monthly target weights sum to 1, and that the 126-day complete-month preview contains 253 dates through 2026-09-30.

## Boundaries and next steps

No strategy trades were simulated and no ML model was trained in this checkpoint. Next steps are next-day execution, trading and management costs, walk-forward evaluation, Monte Carlo sensitivity, and the comparison of SPY buy-and-hold, rule-based momentum, and ML-assisted risk management.

## AI Assistance

I used ChatGPT to help plan the notebook workflow, check calculations, and draft and edit the research report. The saved market-data files and the executed notebook were used to verify the reported figures. The assumptions, limitations, and code usage are disclosed here.
