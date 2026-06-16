# CEX/DEX Arb Dashboard

**Real-time Ethereum Uniswap vs MEXC (and optional Gate.io) arbitrage — screen hundreds of pairs, monitor one coin live, and auto-execute two-leg trades with MEV-protected on-chain swaps.**

The **CEX/DEX Arb Dashboard** is an operator trading workstation for **Ethereum mainnet Uniswap V2/V3 ↔ centralized exchange** arbitrage. MEXC is the primary CEX; Gate.io is optional per coin. The UI combines a live price and pool monitor, ranked pair scanner, dual-direction arb tables at multiple trade sizes, automatic two-leg execution, manual 1inch swaps with MEV bundle submission, and deep feed-health visibility — all over WebSocket with REST fallback.

Built for **hands-on operators** who run their own ETH RPC, CEX API keys, and wallet — not a retail mobile app. Keys and wallet material stay in local config; this overview describes product behaviour only.

**Made by [Logic Encoder](https://logicencoder.com)**

Private source: [logicencoder/cex-dex-arb](https://github.com/logicencoder/cex-dex-arb)

---

## What you can do

| Area | In plain language |
|------|-------------------|
| **Command bar** | Live pills for MEXC, Gate, server WS, ETH, Uniswap, monitor, scanner, and connected clients |
| **Pool monitor** | Discover pools by token, load TVL and reserves, start/stop per-coin live feeds |
| **Active coins** | Save monitored pairs as tabs; one-click reload of pool, symbol, and tuners |
| **Auto trading** | Min profit, cooldown, CEX order type, gas modes; two-leg arb with swap gate |
| **ARB scanner** | Rank stored pairs by net USD/ROI; ignore list; new-coin discovery; Pool lab onboarding |
| **Dual arb tables** | Sell UniV3→CEX and Buy CEX→UniV3 at multiple USD notionals with sortable Net/ROI |
| **Manual MEV swap** | 1inch quotes, slippage control, parallel blast to multiple builders, on-chain cancel |
| **Orderbooks** | MEXC and Gate depth, your arb legs, public trade tape |
| **TradingView chart** | MEXC, Gate, or DEX price context with configurable interval |
| **Settings** | Layout, sounds, RPC/CEX test panels, scanner handoff, privacy mask for balances |

Prices, arb rows, balances, scanner ranks, and MEV stats push over **WebSocket**; HTTP polling covers degraded paths.

---

## Feature examples (two per capability)

#### Command bar and feed health
1. MEXC TRD is green but OB is red — you know orderbook WebSocket is down while trades still flow.
2. CLI shows 3 connected clients; SVR red triggers WebSocket reconnect from settings.

#### Pool load and monitor setup
1. You paste a token address, **Discover pools**, pick pool plus `PEPEUSDT`, **Start monitor** — live stats populate.
2. You stop the monitor before switching coin — feeds tear down per-coin WS without killing the scanner.

#### Active coins and persistence
1. You save a monitored coin to **Active Coins** — one-click tab reloads pool, MEXC symbol, and tuners.
2. You **Refresh** the stored list after Pool lab **Add** — the new pair appears in tabs and the scanner Stored tab.

#### Live stats and price gap
1. MEXC last trade moves — **Price gap** updates vs UniV3 buy/sell legs on the stats card.
2. Dual mode: a Gate row appears when the coin has a Gate pair — three-way price comparison.

#### Pool info and TVL
1. Monitor start fills **Total TVL** and per-token reserves over WebSocket.
2. Low-TVL pool is visible before trading — you avoid illiquid arb on a shallow pool.

#### Automatic trading controls
1. You set min profit $5, cooldown 15s, enable **AUTO TRADE** and **APPLY** — the system fires when Net exceeds threshold on advanced rows.
2. You toggle off during volatile gas — **Disabled** chip shows; tables still update without execution.

#### Balance and portfolio view
1. **REFRESH** pulls chain plus MEXC plus Gate balances — portfolio total for sizing the next leg.
2. Privacy **mask** hides balances during screen share without stopping feeds.

#### ARB scanner — broad screening
1. You **Scan** over 150 stored pairs — **Best arb** ranks top 10 by a $100 simulated trade.
2. You filter `DNX` in search — narrow the list without stopping the scanner loop.

#### Scanner → monitor handoff (Load / GO)
1. You click **Load** on a ranked row — panels bootstrap from scanner RAM for fast first paint.
2. With **Scanner Load → start monitor** enabled, **GO** also starts the full monitor loop.

#### Ignore list and delist handling
1. A pair is delisted on MEXC but the pool is fine on-chain — it appears in ignore with reason; you avoid false signals.
2. You manually ignore `SCAMUSDT` with a note — excluded until removed from saved ignores.

#### New coins and Pool lab onboarding
1. **New coins → MEXC**, ERC20-only, min volume $50k — you queue promising listings to Pool lab.
2. Pool lab **Test all** with min TVL $10k — best V3 pool **Add** lands in stored coins.

#### Dual arbitrage tables (loaded coin)
1. You enable $100 and $500 chips — compare Net across sizes for the slippage curve.
2. Dual CEX: the same row shows whether MEXC or Gate wins on the sell leg.

#### Buy/sell tuners
1. You nudge **Buy tuner** +0.0001 — conservative DEX buy quote in the arb table.
2. You apply a larger **Sell tuner** decrease — stress-test edge before enabling auto-trade.

#### TradingView and orderbook context
1. You switch the chart to **Gate** during a MEXC outage — still see CEX candles.
2. **All Trades** tape shows aggressive MEXC sells into your ask — explains spread collapse.

#### Manual MEV swap
1. You **Sell** 50% token balance via **Swap via MEV** — 1inch quote plus builder blast.
2. A pending tx sticks — **Cancel current swap (max ~$5)** replaces with a cancel transaction.

#### Auto-trade two-leg execution
1. A profitable **uni_to_mexc** $200 row fires — chain leg then MEXC market sell.
2. Cooldown blocks re-fire for 15s after confirm — prevents double-spend on the same signal.

#### CEX order and price method choice
1. **Bid/ask** method plus **Limit GTC** — passive CEX leg at book price.
2. **Last trade** plus **Market** — fastest taker fill when the UniV3 gap is wide.

#### Gas modes and profitability
1. **% of profit** at 12% — high-edge trades pay more gas; thin trades skip auto-fire.
2. **Fixed GWEI** during quiet network — predictable chain cost in the arb table.

#### MEV builder observability
1. After a swap, the MEV table shows Titan **First** at 42ms — you tune which builders stay enabled.
2. **Last on-chain** shows mined hash differs from blast hash — rebroadcast path succeeded.

#### My trades and arb leg history
1. **My Trades** tab lists your completed CEX legs next to the orderbook for the active symbol.
2. You correlate a failed CEX leg in the log with a partial-arb warning after chain confirm.

#### Settings, diagnostics, and operator UX
1. **ETH RPC tests** in settings — pick a working WS endpoint before the session.
2. **Sound on arb opportunity** plus header toast when Net exceeds min — desk alert without staring at the table.

#### Notifications and activity log
1. You enable header toasts for auto-trade completion — glance confirmation without scrolling.
2. You filter the activity log to trades-only — quiet auto-trade spam during scanner runs.

#### Dual CEX (Gate.io)
1. You set per-coin CEX to Gate when MEXC spread is wider — arb table shows the CEX column.
2. Spread chips compare MEXC vs Gate vs delta for the loaded coin in the arb section header.

#### Deposit/withdraw and quoter gates
1. Scanner shows D/W badges — you skip pairs where MEXC deposit is disabled before sizing inventory.
2. **Quoter OK** gate filters ranked rows — only quoter-verified DEX paths appear in top ranks.

---

## What it does not do

- **Not** a mobile or multi-user SaaS — single-operator workstation with local keys
- **Not** cross-chain — Ethereum mainnet Uniswap V2/V3 vs CEX spot
- **Not** guaranteed profit — screening and execution tools; risk and capital are yours
- **Not** custodial — you hold wallet keys and CEX API credentials on your machine

API keys, wallet material, and trade logs stay local — not published in this overview repo.

---

## Tech stack

| Layer | Technologies |
|-------|----------------|
| Runtime | Python 3, asyncio |
| API server | FastAPI, Uvicorn |
| Frontend | Vanilla HTML/CSS/JS |
| Charts | TradingView embed |
| Blockchain | Web3.py, eth-account, eth-abi, eth-defi |
| DEX | Uniswap V2/V3 on-chain quoter and pool discovery |
| Swap routing | 1inch AggregationRouter v6 |
| MEV | eth_sendBundle to multiple builders plus Flashbots Fast raw |
| CEX — MEXC | REST v3, protobuf WebSocket |
| CEX — Gate | Spot v4 REST + WebSocket |
| Serialization | orjson, Pydantic, protobuf |
| Persistence | JSON files (stored coins, ignore list, caches) |

---

## Quick start

```bash
pip install -r requirements.txt
cp .env.example .env          # wallet keys
cp mexc_keys.json.example mexc_keys.json   # CEX API
./run_cex_dex_arb.sh          # default http://localhost:8000
```

Requires a reachable Ethereum RPC/WebSocket hub and MEXC API access. See the private repo README for full configuration and [REPOS.md](REPOS.md) for repository links.

---

## Related repositories

| Repository | Role |
|------------|------|
| [cex-dex-arb](https://github.com/logicencoder/cex-dex-arb) | Private application code |
| [cex-dex-arb-overview](https://github.com/logicencoder/cex-dex-arb-overview) | This product overview |

See [REPOS.md](REPOS.md).

---

**Made by [Logic Encoder](https://logicencoder.com)** · [GitHub](https://github.com/logicencoder) · [Contact](https://logicencoder.com/contact/)
