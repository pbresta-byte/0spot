# 0SPOT Currency Strength

TradingView Pine Script indicator displaying real-time relative strength of 8 major currencies (EUR, USD, GBP, JPY, AUD, NZD, CAD, CHF) on a single chart.

## Installation

### Method 1: Copy-Paste (Fastest)
1. Open **TradingView** → **Pine Editor** (bottom panel)
2. Delete existing code
3. Copy entire contents of `0spot-currency-strength.pine`
4. Paste into Pine Editor
5. Click **"Add to Chart"**

### Method 2: Import Layout
1. Save `0spot-currency-strength.pine` locally
2. TradingView → **Indicators** → **"Invite-only scripts"** (or **Personal**) → **"Import"**
3. Select the `.pine` file
4. Add to any chart

## Usage

- **Best on:** EURUSD, GBPUSD, USDJPY, or any major FX pair (OANDA provider)
- **Timeframe:** Daily (default) / Weekly / Monthly — set via indicator settings
- **Overlay:** Plots directly on price chart (lines scaled to visible range)
- **Legend:** Bottom-left table showing live 0-100 strength per currency

## Data Source

- **28 OANDA pairs** (all major crosses)
- **ROC(14)** on selected timeframe → cumulative weighted index
- **EMA-smoothed** (alpha = 1/3) → normalized 0-100 scale
- **Relative to chart's quote currency** (on EURUSD: USD = 50 baseline)

## Color Key

| Currency | Color |
|----------|-------|
| EUR | Blue |
| USD | Green |
| GBP | Yellow |
| JPY | Red |
| AUD | Orange |
| NZD | Light Green |
| CAD | Deep Orange |
| CHF | Cyan |

## Reference Lines

- **50** = Neutral baseline
- **>70** = Strong
- **<30** = Weak

---

**No external dependencies. Pure Pine Script v6. Works on free TradingView accounts.**