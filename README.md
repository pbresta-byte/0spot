# TradingView Indicators

Two paired indicators, split so each does one job and reads correctly at any zoom level.

## Currency Strength Meter (`currency-strength-meter.pine`)
MQLTA-style 8-currency strength meter (ROC across 28 majors), rendered as 8 line plots
in their own pane instead of a table — put the currencies you're comparing on one chart,
not a grid of numbers. Includes a corner label with the host chart symbol's base/quote bias.

## Price Hot Zone (`price-hot-zone.pine`)
No pivot levels are drawn — no D/W/M tables, no on-chart lines/fills, not even a debug
toggle. The app's whole job is one marker: the best BUY/SELL price to enter at, scored
from a close-based breakout/respect backtest plus confluence. Internally it still ranks
candidates using classic pivot math, but that ladder is never rendered, only the winner is.
The ladder is built from one user-chosen timeframe (`input.timeframe`) instead of a fixed
D/W/M set, and the respect% backtest window auto-scales to that timeframe, so the same
marker logic works whether you're zoomed into a 1-minute chart or zoomed out to monthly.

Run both indicators on the same chart to cross-reference strength and price action —
they no longer share state (each is a standalone script), so there's no bias-coupling
tint between them the way the old single-file version had.

Source-anchored to price-action/price-levels/pivot-point skills (pl0 corpus).
