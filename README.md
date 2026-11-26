# Pine indicators

TradingView indicators written in Pine Script v6. The repo currently holds one script, the Coil Hunter Suite (`coil_hunter_suite.pine`): a single chart overlay that combines a Bollinger/Keltner squeeze, an AMD (accumulation, manipulation, distribution) daily profile, and the Coil Hunter signal with a confidence score and alerts. Built by Gio ([Built-By-Gio](https://github.com/Built-By-Gio)).

For education and chart study, not financial advice.

## Status (2026-11-25)

- Written for Pine v6 (`//@version=6`). It compiles and loads in TradingView.
- I have not backtested the signals yet, so there are no results or performance figures.
- Still to add: chart screenshots.

## What it shows

Each module has its own settings group and a master on/off.

- **Preset.** One dropdown (`Instrument`) picks NQ, ES, SPX, QQQ, GC or Manual. "Auto" reads the chart symbol (MNQ maps to NQ, MES to ES, MGC to GC) and falls back to Manual. The preset sets the band lengths and multipliers, minimum squeeze length, OBV lookback, stop buffer, TP2 multiple, and the AMD tick thresholds.
- **Bands (visual).** Bollinger Bands and Keltner Channels on the same length and basis, both off by default. A squeeze is when the Bollinger Bands sit inside the Keltner Channels. The background is shaded during a squeeze, and dots on the basis line turn orange (squeeze on) or green (off).
- **Coil Hunter.** When a squeeze starts, a yellow box tracks its range. After the minimum number of squeeze bars, a "spring" (wick below the range low, close back inside, up candle) with rising OBV slope gives a pre-breakout BUY, and an "upthrust" (the mirror case) with falling OBV slope gives a pre-breakout SELL. Each signal shows a confidence score: 50, plus 25 for OBV slope agreement, 15 if price is on the near half of the range, 10 if volume is above its 20-bar average. Optional lines mark the stop (signal bar extreme plus an ATR buffer), TP1 (the opposite side of the range) and TP2 (a measured move). Signals can be limited to the New York session and filtered by a minimum confidence. A diamond marks squeeze start and a lightning mark shows when the coil is armed.
- **AMD daily profile (visual only).** Draws the Asia session range, then marks a liquidity sweep of the Asia high or low that closes back inside as "Manipulation", and a displaced break of structure the other way as "Distribution (RBOS)". Optional inducement (IDM) markers, fair value gap box, and flip handling when both sides get swept. It never blocks Coil Hunter signals.
- **Status panel.** A table in the top right with the active preset, symbol, squeeze count, OBV bias, AMD phase, AMD bias, which session led the manipulation, and the minimum confidence setting.

## What you need

- A TradingView account with access to the Pine Editor.
- A chart with volume data (OBV and the volume part of the score use it). Presets are tuned for NQ, ES, SPX, QQQ and GC; other symbols use Manual settings.

## How to use

1. Open a chart in TradingView.
2. Open the Pine Editor at the bottom of the screen.
3. Copy the full contents of `coil_hunter_suite.pine` and paste it in, replacing the default code.
4. Click "Add to chart".
5. Open the indicator settings. Groups: Preset, Manual overrides (used only when Preset is Manual), Coil Hunter, Bands (visual), AMD Daily Profile (LIT), AMD style & sessions (session times in New York time), Display.
6. To get alerts, create an alert on the indicator and pick one of these conditions: `Coil BUY`, `Coil SELL`, `Squeeze started`, `AMD Manipulation`, `AMD Distribution`. The script also fires `alert()` messages for Coil BUY and SELL once per bar close, with the confidence and price.

## Repo layout

```
coil_hunter_suite.pine   the indicator (Pine Script v6)
README.md
LICENSE
```

## Roadmap / future plans

Other indicators (Apex Liquidity Engine, Velocity Scalper, Universal Backtest Harness) may be added later.

## Credits and license

Gio ([Built-By-Gio](https://github.com/Built-By-Gio)). The script uses standard indicator formulas (Bollinger Bands, Keltner Channels, OBV) and TradingView's built-in Pine functions.

MIT License. See `LICENSE`.
