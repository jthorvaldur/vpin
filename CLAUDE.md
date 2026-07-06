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

## Data-First Protocol
When answering questions about data, facts, documents, conversations, or history:
1. **Query the vector DB first.** Use `devctl search "query"` or direct Qdrant search before answering from memory or general knowledge. The DB has 2M+ vectors across legal docs, chats, sessions, and facts.
2. **Know the search scopes.** `devctl search` defaults to ingested docs, court files, facts, and algorithms — AI-assistant chats are excluded (they carry questions and assertions, not ground truth). Use `--claude` for AI chat history (Claude Code, Claude.ai, ChatGPT), `--facts` for the fact registry / case facts, `--algos` for algorithms, `--all` to include everything.
3. **Cite the source.** Include collection name, confidence level, and date when referencing DB results.
4. **Distinguish confidence levels.** A bank statement (verified) is not the same as an email claim (asserted). Never present asserted facts as verified.
5. **Log new facts.** When you discover or confirm a fact during work, log it: `devctl log-fact --fact "..." --source-type X --confidence Y --domain Z`

## Agent rules
- This is archival code — do not refactor without explicit instruction
- Preserve Python 2 compatibility notes in README
- Do not commit .env or secret files
- The compressed trade data (`april_trades.csv.gz`) is part of the repo and should stay
