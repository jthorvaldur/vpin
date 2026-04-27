# vpin

> Read `INTENT.md` before acting. It governs all work in this repo.

**Runtime:** Python 3.12+
**Package manager:** uv
**Status:** tool

## Overview
VPIN (Volume-Synchronized Probability of Informed Trading) implementation based on Easley, Lopez de Prado, O'Hara (2012). Measures order flow toxicity — detects when informed traders are active before price moves. Uses Mt. Gox April 2013 Bitcoin/USD trade data.

## How to run
```bash
uv run python vpin.py --data trades.csv    # compute VPIN from trade data
```

## Key files
- `volume_time.py` — complete VPIN implementation: trade classification, volume-clock resampling, bucket imbalance, rolling VPIN
- `april_trades.csv.gz` — compressed Mt. Gox April 2013 trade data

## How it connects
- Used with: alpha_research, tsprojection (quant research stack)
- Reserve trading infrastructure — reactivate when needed

## Agent rules
- This is archival code — do not refactor without explicit instruction
- Preserve Python 2 compatibility notes in README
- Do not commit .env or secret files
- The compressed trade data (`april_trades.csv.gz`) is part of the repo and should stay
