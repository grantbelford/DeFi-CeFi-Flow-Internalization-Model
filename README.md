# DeFi (1inch) - CeFi (Binance) Flow Internalization

**WETH/USDT 1inch Fusion Flow | Hedge vs. Warehouse Decision**

**📄 Download the full research note: [`Flow-Internalization-Report.pdf`](Flow-Internalization-Report.pdf)** (4 pages)

## What this is

- Decides whether each fill should be hedged on Binance or warehoused.
- Goal: avoid toxic-flow losses while preserving edge from benign flow.

## Main takeaway

- Hedge-vs-warehouse is mostly loss avoidance, not standalone alpha.
- Bigger opportunity is upstream: intent pricing, fill selection, and avoiding toxic large flow.

## Key findings

- Hedging is cheap when executable; depth-limited fills and stress regimes remain caveats.
- Size is the clearest toxicity axis; short-window price correlation is not predictive.
- Mid-size flow is benign; fills above 10 ETH carry the main warehouse risk.
- Policy replay: selective `-$704` vs always hedge `-$1,247` vs always warehouse `-$5,426`; hindsight best-case `+$8,391`.

## Rule of thumb

- Warehouse mid-size flow: `0.3–1.29 ETH`.
- Hedge large flow: model starts hedging near `2.9 ETH`; automatically hedge above `10 ETH`.
- Do not use short-window price correlation as a decision signal yet; it was tested and was not reliable in this sample.

## Data used

- Pair: `WETH/USDT`.
- Sources: 1inch Fusion Dune query `4966942` plus Binance ETH/USDT snapshots.
- Window: May 5–7, 2025.
- Sample: 1,017 fills, 6,600 snapshots, 858 replay fills with valid 60-minute bars.

## Decision model

- Compares expected hedge PnL vs warehouse PnL for each fill.
- Inputs: size, mid price, captured edge, taker fee, slippage, toxicity, hedge delay.
- Captured edge cancels in the branch comparison; hedge costs vs toxicity drive the decision.

## Current parameters

- Binance taker fee: `6.66 bps`.
- Slippage curve: `0.021 + 0.0056 * size_ETH` bps.
- Hedge delay: `33 seconds`.
- Toxicity curve: size-based, using 60-minute markouts.

## Dashboard

- Self-contained HTML; no external dependencies.
- Includes backtest summary, decision calculator, live fill data, Binance depth, and recommendations.

## Live updater

- Runs every 5 minutes.
- Pulls Binance depth via public REST and recent Fusion fills via Dune.
- Uses stale-data guards and live-to-last-known fallback.
- Python and JavaScript engines run the same decision logic; test cases must match before live output is published.

## Limitations

- Small sample: 2 days, 1 pair, 1 venue, rallying ETH regime.
- Model settings are based on this 2-day sample and should be refreshed regularly with new live data.
- Stress liquidity, queue position, and real hedge latency are not fully modeled.
- Funding, borrow, transfer costs, and capital usage are excluded.
- Inventory is assumed pre-positioned on both venues.

## Next steps

- Add rolling calibration for toxicity and slippage.
- Keep collecting live snapshots; train LSTM after 60+ days of data.
- Extend to more pairs and improve queue/impact simulation.
- Keep spread stat-arb closed after failed replication.

## Status

- Research memo: final.
- Dashboard and live updater: implemented.
- Rolling calibration: planned.
- Multi-pair expansion and queue/impact model: candidates.
