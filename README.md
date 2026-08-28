# TradingView Indicators

**Single combined indicator** with three calculation modes (Pivot / Gann / Both-conf) for multi-currency relative-strength analysis on one chart.

## Main Indicator
- **`pivot-breakout-heatmap.pine`** — Relative Currency Strength Matrix
  - **Calculation Type** dropdown: `Pivot` | `Gann` | `Both` (confluence)
  - 8-currency ROC strength meter (28 OANDA pairs) plotted as **relative lines vs quote currency**
  - Gann Square-of-9 levels (East cardinal `4n²−3n+1`) + HLC pivot bands overlay
  - Adaptive risk labels: violation-pip-delta → projected TP/SL + RR filter + macro-event star reference
  - COT adjustment placeholder (toggle OFF until live feed)

## TradingView Layout
- **`relative-strength-matrix-layout.json`** — Importable single-chart layout (EURUSD, no watchlist)

## Backtest Results
- **`backtest_results.csv`** — 28 major pairs × 3 modes (Pivot / Gann / Both)
  - Gann: fewer trades (~11K total), highest PF (2.6–4.3), lowest drawdown
  - Both: ~71K trades, best efficiency per trade
  - Pivot: max opportunity (~131K trades), more noise

## Quick Start
1. Copy `pivot-breakout-heatmap.pine` → TradingView Pine Editor → **Add to chart**
2. Or import `relative-strength-matrix-layout.json` → Layouts → Import
3. Works on any EURUSD chart (OANDA:EUR_USD, FX:EURUSD, TVC:DXY for DXY overlay)

## Source Anchors
- Gann Square-of-9 math: `book-catalog.csv` row 1401 (Master Stock Market Course) → `skills/gann-square-of-nine/SKILL.md`
- 28-pair ROC strength: `proposal-currency-strength-index-skill.md` (MQLTA)
- Pivot ladder + respect%: `skills/pivot-points/SKILL.md`, `skills/price-levels/SKILL.md`