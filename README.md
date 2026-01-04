# SPY Direction Prediction (Baseline-First Walk-Forward Study)

## Overview
This project tests whether simple technical features can improve probabilistic forecasts of SPY direction beyond market drift. Evaluation is done using walk-forward validation and log loss, with a drift baseline computed per training window.

## Data
- SPY daily close prices (Yahoo Finance)

## Features
- Return_1d: daily percent return
- Return_5d: 5-day percent return
- Vol_5d / Vol_20d: rolling std of Return_1d
- Trend_20: (Close / MA_20) - 1

## Targets
- 1-day direction: Close(t+1) > Close(t)
- 5-day direction: Close(t+5) > Close(t)

## Methodology
- Walk-forward validation (time-series safe)
- Metric: log loss (probability calibration)
- Baseline: constant p0 = mean(y_train) per window
- Model: Logistic Regression (with optional StandardScaler pipeline)

## Findings (Summary)
- 1-day direction is noise-dominated under simple linear features.
- 5-day direction shows strong drift; simple technical features did not provide robust incremental improvement beyond baseline.
- Volatility features were misleading for direction (especially after scaling).
- Regime split (Trend_20 > 0 vs <= 0) showed return signals harmful in bull regimes and not reliably beneficial in bear regimes.

## Next Steps
Pivot to risk-focused modeling (volatility forecasting / drawdown probability / risk regime detection).
