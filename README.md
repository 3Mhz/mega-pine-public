# MHSG Pine Scripts

TradingView Pine Script (v6) indicators for the MHSG chart setup: a main price overlay, a lower-pane momentum/volume panel, and optional dark pool / options flow overlays with embedded ticker snapshots.

## Quick start

**Recommended layout (two panes):**

1. `MHSG_Chart_Suite.pine` — main chart overlay
2. `MHSG_Chart_MegaStoch.pine` — lower pane (TSI + Stochastic + volume)

**Optional overlays** (only render when your chart symbol is in the embedded data — see ticker lists below):

3. `MHSG_DarkPool_Levels.pine` — horizontal levels on the price chart
4. `MHSG_NetFlow.pine` — options net flow panel (use a **5–30 minute** chart)

**Install:** TradingView → Pine Editor → New indicator → paste script → Save → Add to chart.

Draw cyan trendlines manually. MegaStoch includes volume columns — you can hide TradingView's built-in volume if you prefer.

---

## MHSG_Chart_Suite.pine (main overlay)

**Pane:** price chart (overlay, behind candles)

Combines long-term structure, medium-term trend, and short-term ribbon context on one chart.

### Weekly Bollinger Bands (cyan dashed)

- Computed on the **weekly** timeframe (20-period SMA ± 3σ).
- Upper and lower bands print as thick cyan dashed lines on whatever intraday/daily chart you use.
- **Squeeze highlight:** when band width is near its recent minimum, the background tints yellow — volatility contraction / potential expansion setup.

### Daily Hull MAs (89 / 144)

- **Green (89)** and **red (144)** solid lines from **daily** Hull moving averages, drawn on your chart timeframe.
- Use crossovers and separation for trend context against the weekly BB and ribbon.

### Fibonacci EMA ribbon (chart timeframe)

- Dotted rainbow ribbon on **your chart's timeframe** (not weekly): EMAs 8, 13, 21, 34, 55, 89, 144, 233.
- Slowest EMAs (144, 233) can be toggled off to reduce clutter.
- Use for short-term trend alignment and pullback context against the daily HMAs and weekly BB.

### Settings worth knowing

- **MTF gap fill (BB only):** how weekly band values fill between weekly bar boundaries.

---

## MHSG_Chart_MegaStoch.pine (lower pane)

**Pane:** separate panel below price (fixed 0–100 scale)

Three layers on one shared 0–100 axis:

### Stochastic (solid green / red)

- Default **14, 2, 3** (%K / smoothing / %D).
- Color flips green when %K > %D, red when bearish.
- Overbought / oversold bands at 80 / 20 with optional shaded zone.

### TSI — True Strength Index (cyan / orange)

- Default **13 / 25 / 13** (short / long / signal).
- Mapped onto 0–100 either by **percentile rank** (default — uses full pane visually) or **fixed scale** (raw TSI ±N → 0/100).
- 50 midline marks neutral momentum.

### Volume (bottom third of pane)

- Semi-transparent columns normalized to the bottom ~30% of the 0–100 scale.
- Green/red coloring by buy/sell pressure (close position within the bar range).
- Optional volume MA in yellow.

**Tip:** If the pane scale drifts after manual Y-drag, double-click the pane Y-axis or use indicator ⋮ → Reset chart view.

---

## MHSG_DarkPool_Levels.pine (price overlay)

**Pane:** main chart (horizontal lines behind price)

Plots **dark pool and block trade levels** as horizontal lines with optional labels (`$XM Buy/Sell`, type tags). Data is **embedded in the script** — no live API at runtime.

### How it works

1. Open a symbol that exists in the embedded ticker list (below).
2. Add the indicator. Lines appear at prices where large off-exchange prints were recorded (~1 week lookback in the snapshot).
3. **Line color:** green gradient from dark (smaller notional) to bright (largest print on that chart).
4. **Merge nearby levels:** optional — combines lines within a dollar tolerance (default $0.10) into one weighted-average level.
5. **Today only / min notional / extend days:** filter and style in indicator settings.
6. Check **Data updated** in the indicator data window for snapshot date.

If your chart symbol is **not** in the list, nothing draws — switch symbol or wait for an updated release.

### Embedded tickers (dark pool snapshot)

Data last updated: see `DATA_UPDATED` in the script (currently **2026-06-17**).

```
AAPL, AGX, AMZN, AN, AROC, ASTS, BTI, BUD, CART, CAVA, CELH, CODI, CRM, CVS,
DIS, FRMI, GME, IIPR, IRTC, KRE, LC, LOCO, MELI, MTCH, NFLX, OSCR, PBI, PDD,
QQQ, QYLD, RACE, SPY, STNE, TAC, TGT, TIC, TOI, TQQQ, U, VELO, VTI, XP
```

**42 tickers** · **717 levels** in the current snapshot.

---

## MHSG_NetFlow.pine (lower pane)

**Pane:** separate panel below price

Shows **intraday options net premium flow** plus a scaled price line for shape comparison.

### How it works

1. Use a **5–30 minute** chart so bar times align with embedded timestamps.
2. Open a symbol from the embedded list below.
3. **Green line** — cumulative **call** net premium ($).
4. **Red line** — cumulative **put** net premium ($).
5. **White line** — stock price rescaled onto the same axis as flow (comparison only, not a second price scale).
6. On-chart label shows rolling window length and update date when data is present.

Flow values are minute-level snapshots merged into a rolling archive (~30 calendar days max in the generator; public snapshots may include fewer days until the archive fills).

If your symbol is missing or has sparse history, the pane may be empty.

### Embedded tickers (net flow snapshot)

```
AAPL, AGX, AMZN, ASTS, BTI, BUD, CAVA, CELH, CRM, CVS, DIS, FRMI, GME, KRE,
MELI, NFLX, OSCR, PDD, QQQ, RACE, SPY, TGT, TQQQ, U, VELO, XP
```

**26 tickers** in the current snapshot (tickers need sufficient history to plot).

---

## Files in this repo

| File | Pane | Purpose |
|------|------|---------|
| `MHSG_Chart_Suite.pine` | Overlay | Weekly BB, daily HMAs, Fib EMA ribbon |
| `MHSG_Chart_MegaStoch.pine` | Below | TSI + Stochastic + volume on 0–100 |
| `MHSG_DarkPool_Levels.pine` | Overlay | Dark pool / block print levels (embedded) |
| `MHSG_NetFlow.pine` | Below | Call/put net flow + scaled price (embedded) |

Embedded overlay data is refreshed periodically; re-paste or reload the script after updates to pick up new snapshots.

## License

MIT — see [LICENSE](LICENSE).
