# Clerk It

A trading tournament on HashKey Chain, built for HSK Chain Horizon, Track 1 (AI Agent Trading).

Four software clerks paper trade the same HSKSwap V3 pool (WHSK/USDT, 0.3 percent fee tier) under rules that were frozen before any data existed. Every shadow fill is priced through the real QuoterV2 at a fixed 50 USDT size, with the pool fee and price impact inside the quote and real gas deducted per fill, so the paper record carries honest costs.

Each clerk watches the pool's spot price against its own one hour TWAP anchor and trades mean reversion at a different band: 75, 125, 200 and 350 basis points. A clerk earns promotion only with at least 5 closed trades and a positive net P and L after costs. The leader, and only the leader, may trade live at 10 USDT per trade, and only through ClerkVault, an on chain contract that enforces a 25 USDT maximum trade, a 5 USDT daily loss cap and a one hour cooldown. The agent cannot widen its own limits; only the owner can change them, and the owner can pause the vault at any time.

## What lives here

`index.html` is the public dashboard: a live price chart with the one hour TWAP anchor and the four entry bands, the tournament leaderboard with equity sparklines, the pool composition visual, the vault guardrails, and a conversational interface that answers questions from the live standings and the hash chained tournament log.

`standings.json`, `activity.json` and `history.json` are the dashboard's data files. They are refreshed from the tournament engine every 15 minutes by `sync_data.py` and republished by `publish.py`. `history.json` carries the price history series (tournament log cycles merged with the spread watch log), a per clerk equity series reconstructed from the log's exit fills, and a pool snapshot read live from the chain (with the Phase 0 census as fallback).

`sync_data.py` copies the engine's standings and builds the trimmed activity extract from the tournament log. `publish.py` commits changed files through the Git Data API.

## Links

Dashboard: https://godson-droid.github.io/clerk-it/

The pool on Blockscout: https://hsk.blockscout.com/address/0x4ff515761864e7838B0AdB8b5b2B8B7A068905dC

Built by Godson.
