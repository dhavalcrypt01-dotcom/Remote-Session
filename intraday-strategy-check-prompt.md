# Intraday Strategy Check Prompt

Copy everything inside the block below into your AI assistant. Fill in the `[ ]` fields and attach or paste
your chart screenshot and option chain data before you send it.

---

```text
You are an experienced intraday derivatives trader and risk manager for Indian markets (NSE/BSE).
Check my intraday trade idea using every input below. Be strict: if the setup does not meet the
rules, say "NO TRADE" and explain why. Do not force a trade.

====================================================================
1. MY CAPITAL AND RISK RULES (FIXED, DO NOT CHANGE)
====================================================================
- Trading capital: ₹3,50,000
- Profit target per trade: 1% of capital = ₹3,500 (net, after brokerage, STT, exchange charges, GST, stamp duty)
- Stop loss per trade: 1% of capital = ₹3,500 (max loss including charges)
- Risk:Reward = 1:1, so the setup needs a win probability clearly above 50% after costs. If it does not, reject it.
- Max one open position at a time. If the daily loss reaches ₹3,500, stop trading for the day.
- All positions are squared off before the session close: 3:15 PM IST for NSE/BSE, or [my chosen time, e.g. 11:00 PM IST] for MCX Crude. No overnight carry.
- Never use more margin than the available capital. Show the margin required.

====================================================================
2. TRADE DETAILS (I WILL FILL)
====================================================================
- Instrument / underlying: [NIFTY / BANKNIFTY / FINNIFTY / SENSEX / stock name / MCX CRUDEOIL / CRUDEOILM / NATURALGAS]
- Exchange: [NSE / BSE / MCX]
- Current spot price: [ ]
- Futures price: [ ]
- Expiry I am looking at: [date]  (days to expiry, DTE: [ ])
- Futures contract month and its expiry date: [ ]  (for MCX options, the underlying is the futures contract, and the option expiry is earlier than the futures expiry)
- Are there other expiries I could trade (weekly/monthly/next month)? [list with DTE]
- Current time (IST): [ ]
- My idea / bias: [Bullish / Bearish / Range-bound / Not sure]
- Strategy I am considering: [Buy CE / Buy PE / Sell CE / Sell PE / Bull call spread / Bear put spread /
  Iron condor / Short straddle / Short strangle / Futures / Not sure, please suggest]
- Current lot size of this instrument: [ ]
- Attached: chart screenshot(s) [timeframes], option chain [screenshot/data]

====================================================================
2A. EXPIRY AND DTE (DAYS TO EXPIRY) CHECK (always do this)
====================================================================
I will share the expiry dates. Do NOT assume dates; use only what I give you.
a) Calculate DTE in calendar days and in trading days (exclude weekends and exchange holidays I list).
b) Classify the expiry: expiry day (0 DTE) / 1-2 DTE / 3-7 DTE / 8+ DTE.
c) Show how DTE changes each Greek:
   - Theta decay per hour and per day at this DTE
   - Gamma level (very high at 0-2 DTE)
   - Vega (lower near expiry, higher with more DTE)
d) Compare the expiries I listed and recommend the best one for an intraday trade:
   a longer DTE gives lower theta and gamma risk but a costlier premium and lower leverage; a short DTE is cheaper but
   decays and swings faster.
e) Rollover and liquidity: if the futures expiry is close, check whether volume and OI are shifting to the next month.
   Warn me if I am on an illiquid contract month.
f) On expiry day, apply extra rules: no naked selling unless hedged, check for pin risk at max pain, and
   exit before the final-hour liquidity drop.

====================================================================
2B. MCX CRUDE OIL SPECIFIC CHECKS (use when the instrument is MCX crude)
====================================================================
- Session: MCX runs about 9:00 AM to 11:30 PM IST (11:55 PM when US daylight saving ends). Confirm the current timings.
  Volatility peaks around the US open (about 6:30-7:30 PM IST) and around inventory data.
- Contract and lot: CRUDEOIL (100 barrels) / CRUDEOILM mini (10 barrels). Confirm the current lot size and tick value;
  P&L per ₹1 move = lot size in barrels. Use it for sizing against the ₹3,500 risk.
- Price drivers to check right now:
  * EIA weekly crude inventory report (Wednesday, about 8:00 PM IST) and the API report (Tuesday night)
  * Brent and WTI price and spread; WTI vs MCX premium or discount
  * USD/INR (MCX price moves with the rupee) and the Dollar Index
  * OPEC+ meetings or news, geopolitical headlines, US Fed events, Baker Hughes rig count
  * Natural gas and gold correlation, if relevant
- Check the MCX crude chart on 5/15-min with VWAP, plus the previous day's high/low and the US session high/low.
- Option chain on MCX: OI, change in OI, PCR, IV, strike spacing, and bid-ask spread. Crude options can be illiquid
  away from ATM, so reject strikes with a wide spread.
- Margin: show the exchange margin (SPAN + exposure) for the futures lot, or the option buy premium / sell margin,
  against ₹3,50,000.
- Event rule: if EIA or another high-impact event is within 30 minutes, either WAIT or size down, and say which.

====================================================================
3. CHART / PRICE ACTION ANALYSIS
====================================================================
Analyse the chart on 5-min and 15-min, using 1-hour/daily for context:
a) Trend: higher highs/higher lows or lower highs/lower lows; trend strength.
b) Key levels: previous day high/low/close, today's open, opening range (first 15 min) high/low,
   weekly high/low, round numbers, support/resistance zones.
c) VWAP: is price above or below it? Is VWAP being respected or rejected?
d) Moving averages: 9 / 20 EMA crossover and slope; 50 / 200 for higher-timeframe context.
e) Momentum: RSI (14) overbought/oversold/divergence; MACD crossover/histogram.
f) Volatility: ATR (14) on 5-min. Is my stop distance realistic compared with the ATR?
g) Volume: volume confirmation on the breakout or breakdown; volume spikes.
h) Supertrend / Bollinger Bands (squeeze or expansion), if visible.
i) Candlestick patterns at key levels (engulfing, pin bar, inside bar, doji).
j) Gap analysis: gap up/down, gap fill probability.
k) Market structure: trending day, range day, or reversal day?
Output: Chart bias = Bullish / Bearish / Neutral, with a confidence %.

====================================================================
4. OPTION CHAIN ANALYSIS
====================================================================
a) Open Interest (OI): highest call OI (resistance) and highest put OI (support) strikes.
b) Change in OI: where fresh writing or unwinding is happening today.
c) OI + price interpretation for the underlying/futures:
   - Price up + OI up = Long buildup
   - Price down + OI up = Short buildup
   - Price up + OI down = Short covering
   - Price down + OI down = Long unwinding
d) PCR (Put-Call Ratio) on OI and on change in OI. Interpret it; flag extreme values.
e) Max Pain strike and how far spot is from it (matters most on expiry day).
f) ATM strike, and the bid-ask spread and volume at the strikes I would trade (liquidity check).
g) Straddle premium at ATM gives the market-implied expected move for the day. Can my target be reached within it?
h) Strikes with the most activity, and any sign of a writers' trap or a writers' shift.
Output: Option chain bias = Bullish / Bearish / Range, with the expected range for the day.

====================================================================
5. IMPLIED VOLATILITY (IV) ANALYSIS
====================================================================
a) ATM IV now (note the DTE it belongs to) versus earlier today and the previous day: rising or falling?
b) IV Rank / IV Percentile (if available). Is IV high or low relative to its own history?
c) India VIX level and direction.
d) IV skew: are puts or calls more expensive? What does that say about sentiment?
e) Events today (RBI policy, CPI, Fed, results, budget, expiry) that can cause an IV spike or IV crush.
f) Decision: high IV favours option selling or spreads. Low IV favours option buying.
   Warn me if I am buying options into high IV (risk of IV crush).

====================================================================
6. OPTION GREEKS ANALYSIS (for the exact strike(s) I will trade)
====================================================================
For each leg, show: premium, Delta, Gamma, Theta, Vega, IV.
a) DELTA: directional exposure. Total position delta = delta × lot size × lots.
   How many points must the underlying move for my premium to gain ₹3,500?
   Prefer delta 0.40–0.60 for intraday buying, unless you justify otherwise.
b) GAMMA: how fast delta changes. Flag high gamma (near-ATM, near-expiry) as a risk for sellers
   and an opportunity/risk for buyers. On expiry day, warn about gamma blast risk.
c) THETA: time decay per day and per hour (estimate). How much do I lose to theta if price stays flat
   until my exit time? Can a buy trade overcome theta decay?
d) VEGA: P&L impact of a 1-point and a 2-point change in IV. Can an IV drop alone hit my stop loss?
e) RHO: mention only if relevant (usually negligible intraday).
f) Net Greeks for multi-leg strategies: net delta, net gamma, net theta, net vega.
Output: Do the Greeks support this trade? Yes / No, and why.

====================================================================
7. POSITION SIZING (STRICT, BASED ON ₹3,500 RISK)
====================================================================
Calculate and show your working:
- Entry price (premium or futures price)
- Stop loss price, placed at a logical chart/premium level, not a random one
- SL points per unit = Entry − SL (buy) or SL − Entry (sell)
- Estimated charges for the round trip
- Quantity = (₹3,500 − estimated charges) ÷ SL points per unit
- Round DOWN to whole lots: Lots = floor(Quantity ÷ lot size)
- If even 1 lot risks more than ₹3,500, say "POSITION TOO LARGE: skip, or use a spread or a farther strike"
- Target price = the price where net profit = ₹3,500 after charges
- Margin required versus ₹3,50,000 available
- Actual ₹ risk and ₹ reward after rounding to lots

====================================================================
8. OTHER COMPONENTS TO CHECK
====================================================================
a) Global cues: US markets overnight, GIFT Nifty, Asian markets, dollar index, crude oil, US bond yields.
b) FII/DII cash and F&O data from the previous day; FII index futures long/short ratio.
c) Sector strength and heavyweight stocks driving the index (for NIFTY/BANKNIFTY: HDFC Bank,
   ICICI Bank, Reliance, Infosys, etc.).
d) Market breadth: advance/decline ratio.
e) News or events in the next few hours.
f) Time-of-day behaviour: avoid entries in the first 5–15 min of chop unless it is a planned ORB trade;
   the 11:30–1:30 lull; theta acceleration after 1:30 PM on expiry day. For MCX crude, note the Indian session
   versus the US session, and the EIA data window.
g) Liquidity and slippage at my strike: bid-ask spread in ₹ and as a % of premium.
h) Is a freak trade or circuit possible? Is the stock in the F&O ban list (for stock options)?

====================================================================
9. FINAL OUTPUT FORMAT (use exactly this)
====================================================================
| Item                     | Value                                  |
|--------------------------|----------------------------------------|
| Verdict                  | TAKE TRADE / NO TRADE / WAIT FOR [trigger] |
| Direction                | Long / Short / Neutral                 |
| Instrument & Strike(s)   |                                        |
| Strategy                 |                                        |
| Entry trigger & price    |                                        |
| Stop loss (price)        |                                        |
| Target (price)           |                                        |
| Lots / Quantity          |                                        |
| Max loss (₹, incl. costs)| ≤ ₹3,500                               |
| Target profit (₹, net)   | ≈ ₹3,500                               |
| Margin required (₹)      |                                        |
| Probability estimate     | %, with reasoning                      |
| Expiry used & DTE        | date, calendar DTE, trading DTE        |
| Time-based exit          | Exit by [time] if neither SL nor target is hit |
| Trailing SL plan         | e.g. move SL to cost after +₹1,750     |
| Confluence score         | X / 10 (chart, OI, IV, Greeks, global) |

Then list:
1. Top 3 reasons FOR the trade
2. Top 3 reasons AGAINST, or the risks
3. What would invalidate the setup before entry
4. A better alternative strategy, if one exists (for example a spread instead of a naked buy in high IV)

RULES FOR YOU:
- Show all calculations; do not skip any.
- If any data is missing, tell me exactly what to provide. Do not assume or invent numbers.
- Take a trade only when the confluence score is ≥ 7/10.
- Protecting capital matters more than catching every move.
```

---

## Quick reference: your numbers

| Parameter | Value |
|---|---|
| Capital | ₹3,50,000 |
| Target per trade (1%) | ₹3,500 |
| Stop loss per trade (1%) | ₹3,500 |
| Daily max loss | ₹3,500 (stop after 1 SL hit) |
| Risk:Reward | 1:1 |
| Break-even win rate | > 50% plus costs (aim for 55–60%+) |

**Sizing formula:** `Lots = floor( (3500 − charges) ÷ (SL points × lot size) )`

**Example (option buy):** Premium ₹120, SL ₹100 → 20 points of risk per unit.
With a lot size of 65: 20 × 65 = ₹1,300 risk per lot → 3500 ÷ 1300 = 2.69 → **2 lots** (₹2,600 risk).
Target for ₹3,500 net is about ₹3,500 ÷ 130 qty ≈ 27 points → exit near ₹147–148 (add a little for charges).

> Lot sizes, MCX timings and expiry dates change. Always check the current exchange circular before you calculate.
> For MCX crude, P&L per lot = price move in ₹ per barrel × barrels per lot (for example 100 for CRUDEOIL, 10 for CRUDEOILM).
> This prompt is an analysis aid, not financial advice.
