# MHSG Pine Scripts (public)

TradingView Pine Script (v6) indicators for the MHSG chart setup, plus Tradytics-driven dark pool and net flow overlays.

This repository is automatically mirrored from a private source. Only the published scripts below are included.

## Scripts

| File | Type | Pane | Description |
|------|------|------|-------------|
| `MHSG_Chart_Suite.pine` | Indicator | Main (overlay) | MHSG Main — weekly BB (20,3,3), chart-TF Fib EMA ribbon, daily 89/144 HMA |
| `MHSG_Chart_MegaStoch.pine` | Indicator | Below | MegaStoch — TSI + Stochastic on one shared 0..100 axis + volume |
| `MHSG_Tradytics_DarkPool_Levels.pine` | Indicator | Main (overlay) | Dark pool levels (embedded Tradytics snapshot) |
| `MHSG_Tradytics_NetFlow.pine` | Indicator | Below | Options net flow (embedded Tradytics snapshot) |

## Recommended chart layout

- `MHSG_Chart_Suite.pine` — main overlay (weekly BB, Fib EMA ribbon, daily 89/144 HMA)
- `MHSG_Chart_MegaStoch.pine` — combined TSI + Stochastic + volume pane

Optional overlays (same symbol must exist in embedded data):

- `MHSG_Tradytics_DarkPool_Levels.pine` — dark pool horizontal levels on the price chart
- `MHSG_Tradytics_NetFlow.pine` — call/put net premium + scaled price (use 5–30 min chart)

## Install

1. Remove old BB / EMA / Stoch / TSI built-ins from the chart if you use the suite.
2. TradingView → Pine Editor → New indicator → paste each script → Save → Add to chart.

Notes:

- Trendlines: draw manually (cyan).
- Tradytics overlays ship with **embedded data snapshots** updated on the private side; re-add the indicator after pulling a new version to refresh on-chart data.

## License

MIT — see [LICENSE](LICENSE).
