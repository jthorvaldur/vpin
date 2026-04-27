# CLAUDE.md — vpin

**Runtime:** Python 3.12+
**Package manager:** uv
**Status:** tool

## What this is
VPIN (Volume-Synchronized Probability of Informed Trading) implementation. Measures information asymmetry in order flow — detects when informed traders are active before price moves.

## How to run
```bash
uv run python vpin.py --data trades.csv    # compute VPIN from trade data
```

## How it connects
- Used with: alpha_research, tsprojection (quant research stack)
- Reserve trading infrastructure — reactivate when needed

