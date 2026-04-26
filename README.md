# VPIN -- Volume-Synchronized Probability of Informed Trading

VPIN is a metric introduced by Easley, Lopez de Prado, and O'Hara (2012) that
measures the toxicity of order flow. It estimates the probability that informed
traders are driving volume in a given market. Elevated VPIN values signal
adverse selection risk -- conditions where market makers face losses to
better-informed counterparties.

## What this code does

`volume_time.py` implements the volume-clock VPIN calculation:

1. **Load and classify trades.** Reads timestamped trade data and classifies
   each trade as buyer- or seller-initiated using the exchange-reported
   direction field.

2. **Resample to time bars.** Aggregates raw trades into one-minute bars for
   volume, price change, and trade direction.

3. **Expand to unit-volume increments.** Each time bar is expanded into
   individual unit-volume records, producing a volume-time series where each
   row represents one unit of volume transacted.

4. **Group into volume buckets.** The unit-volume series is partitioned into
   fixed-size buckets (default: 500 BTC). Within each bucket, order imbalance
   is computed as the absolute difference between buy and sell volume,
   normalized by bucket size.

5. **Compute rolling VPIN.** VPIN is the rolling mean of order imbalance over
   the trailing N buckets (default window: 500 buckets).

6. **Plot results.** Produces VPIN overlaid on price, plus a comparison of
   return distributions under volume-time versus chronological-time sampling
   (volume-time returns are closer to normal, as the theory predicts).

## Data

The included `april_trades.csv.gz` contains Bitcoin/USD trades from Mt. Gox
(April 2013). A separate ticker file (`all_ticker.txt`) provides bid/ask
quotes for mid-price construction, though it is not bundled in this repository.

## Note on Python version

This is archival code from approximately 2013-2014, written for Python 2. It
runs as-is on Python 2.7 with the dependencies listed below. To run on
Python 3, the following changes are needed:

- `izip_longest` (imported but unused) is now `itertools.zip_longest`
- `float32` references need `np.float32`
- `pandas.rolling_mean(series, window=N)` becomes `series.rolling(N).mean()`
- `.resample('1min', how='sum')` becomes `.resample('1min').sum()`
- `.ix[]` becomes `.loc[]`
- `print` statements (if any are added) require parentheses

## Requirements

- Python 2.7 (see above for Python 3 migration notes)
- pandas
- numpy
- matplotlib

## Reference

Easley, D., Lopez de Prado, M., & O'Hara, M. (2012). Flow Toxicity and
Liquidity in a High-frequency World. *Review of Financial Studies*, 25(5),
1457-1493.
