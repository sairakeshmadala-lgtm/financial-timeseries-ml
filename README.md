# Financial Time-Series ML: Leakage-Safe Forecasting & Backtesting

A reproducible learning project exploring next-day return prediction from historical daily OHLCV data.

## What it demonstrates
- Market data download and quality checks
- Lagged-return, moving-average, volatility and volume features
- Chronological train/test split (no random shuffling)
- Walk-forward validation using TimeSeriesSplit
- Baseline versus Random Forest regression
- Illustrative long-only backtest with transaction-cost assumption
- Unit tests for feature generation and time ordering

**Scope:** This is a learning project using daily OHLCV data, not a high-frequency trading system. It does not use tick or order-book data. Historical results do not guarantee future performance and are not investment advice.

## Setup (Windows PowerShell)
```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## Run
```powershell
python -m src.market_ml.run
pytest -q
```

The script downloads SPY daily data using yfinance and writes metrics and predictions to `reports/`. Change ticker/date range in `src/market_ml/run.py` if needed.

## Validation approach
The final 20% of rows are held out chronologically. TimeSeriesSplit is used only within the training period. Features at day t predict the close-to-close return from day t to t+1.

## Limitations
This project does not model order-book dynamics, execution latency, slippage, market impact, borrow costs or taxes. The strategy simulation is illustrative only.
