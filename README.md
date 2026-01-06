# Cointegration Pairs Trading

A compact research pipeline (Jupyter) for cointegration‑based pairs trading: pair selection (Engle–Granger), hedge‑ratio estimation, spread modelling, rolling z‑score signals, walk‑forward backtesting with realistic constraints, and a small parameter sweep for robustness.

## Features
- Pair selection via Engle–Granger and half‑life filtering  
- Hedge‑ratio estimation (OLS) and spread construction  
- Rolling z‑score entry / exit / stop signals  
- Walk‑forward out‑of‑sample evaluation with stitched equity curve  
- Transaction costs via turnover; market‑neutral dollar weighting, leverage and per‑leg caps  
- Synthetic data fallback so the pipeline runs without internet

## Quick start
1. Create a virtual environment (recommended) and install deps:
```bash
pip install numpy pandas statsmodels yfinance matplotlib
```
2. Open `main.ipynb` in Jupyter and run cells top‑to‑bottom.

## Configuration
Edit the `ResearchConfig` dataclass in the notebook to change:
- `tickers`, `start` / `end` dates  
- `train_days` / `test_days` (walk‑forward windows)  
- `entry_z`, `exit_z`, `z_lookback`, `gross_leverage`, `cost_bps_per_turnover`

## Outputs
- `pair_table`: candidate pairs from the initial training window  
- `oos_rets`: stitched out‑of‑sample daily returns and equity curve  
- `window_table`: per‑window diagnostics (CAGR, Sharpe, MaxDD, TotalReturn)  
- `sweep`: parameter sweep OOS comparison table

## Notes
- If `yfinance` is unavailable or history is short, the notebook falls back to synthetic cointegrated series.  
- For reproducible runs prefer a pinned `requirements.txt` / conda environment instead of in‑notebook installs.  
- Align synthetic data length with `train_days + test_days` in `ResearchConfig` to avoid insufficient‑history errors.
