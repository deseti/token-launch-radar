# token-launch-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/deseti/token-launch-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/deseti/token-launch-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

A token launch radar: every rankable pre-token protocol in a sealed DefiLlama snapshot, ranked by an implied value computed from the snapshot's own figures, with a 7-step farm plan for each protocol and a static dashboard (board, detail view, filters) that renders with no network.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <path-to-snapshot.json>
```

Then open `out/dashboard/index.html` (it reads `out/data.js` beside it).

## Method

- Source: the sealed snapshot at `input/snapshot.json` — DefiLlama `https://api.llama.fi/protocols`, fetched 2026-11-14T01:18:33.201Z, 758 protocols, watchlist floor $50,000,000.
- Rankable = records no token (no market cap, no CoinGecko id, no symbol) and is not a wrapped / staked / bridged product of a token that already trades, not a centralised exchange, and not a versioned pool. That is the house watchlist rule applied to the whole snapshot: 197 rows, covering all 40 watchlist protocols.
- Implied value: `TVL x liveMultiple x growthMult x maturityMult x breadthMult`, where `liveMultiple` is the median market-cap / TVL of the snapshot's live-token protocols (computed at run time, not hardcoded), growth is the 7-day TVL change clamped to -50..+100%, maturity grows with age since first listing (unknown age = 365 days), and breadth adds 3% per extra chain (capped at 5).
- "No token" means the snapshot records no token — it is not proof a protocol has none. Implied value is a model, not a price, and does not predict whether or when a token is issued.
- Live-token protocols are set aside with their market caps, never mixed into the ranking.

---

<sub>Entered on [make.fun](https://make.fun/?ref=&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
