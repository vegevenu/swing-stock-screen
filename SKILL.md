# Swing stock screen and daily review

Run a repeatable swing trade screen for a 1 to 3 month hold, rank the names that pass, set entry stop and target levels, and score the predictions after the close so the method improves each day. Label every output as analysis, never as a recommendation, and never assume the user bought anything or holds a position.

## Screen the universe in five steps

- Start from a fixed universe of large cap names with one benchmark for comparison, and keep the list in `~/workspace/swing-daily/ALGORITHM.md` so every run screens the same names.

- Add a name the user asks about to the universe and run the same five steps on it, instead of giving an off the cuff verdict from one price check.

- Apply step 1, technicals, to every candidate. Require price above the 50 day and 200 day averages with a rising 50 day average, read RSI(14) with 70 and above treated as extended, read MACD direction, and measure distance above the volume profile point of control, where 21 to 35 percent above value counts as extended and demands a pullback.

- Apply step 2, fundamentals, to every candidate. Compare the latest quarter against consensus on revenue and EPS, record whether guidance was raised held or cut, compare forward P/E and PEG with peers, and flag balance sheet problems such as heavy debt or negative equity.

- Apply step 3, capex and cash, to every candidate. Require free cash flow to be positive and to cover capex plus shareholder returns, and fail any name that is burning cash on heavy capex no matter how strong its revenue growth looks.

- Apply step 4, news and catalysts, to every candidate. Verify each finalist's earnings date from the earnings calendar before publishing anything, because a missed earnings date is the easiest error in this screen, and record deals, approvals, decisions due inside the hold window, and event risk such as earnings binaries or geopolitical exposure.

- Apply step 5, people and sentiment, to every candidate. Record analyst target revisions, institutional positioning, and insider activity, and state plainly when no open market insider buying was found instead of implying support that is not there.

- Admit only names that pass all five steps into the top 5, keep a first reserve, and state every could not verify item in the same message, such as unverified vendor moving average or RSI pages, missing volume tables, missing 13F or Form 4 pulls, and consensus targets that predate the latest earnings.

## Compute indicators and backtest the signals

- Compute indicators from price bars in three windows, about 1 year of daily bars, about 5 years of weekly bars, and monthly bars back to 2006, and append the latest close before recomputing so no run reuses stale indicator values.

- Compute SMA 20, 50, and 200, MACD 12 26 9, RSI(14), Fibonacci retracements of the 1 year range, anchored VWAP from the 1 year low and from earnings dates, volume profile with point of control and 70 percent value area, supply and demand swing zones, open fair value gaps, 90 day liquidity sweeps, 60 day candlestick patterns, and weekly chart patterns.

- Treat pattern detectors as mechanical flags, not confirmations, and report which matches matter, such as double bottoms as bases, rising wedges as compression warnings, and the absence of completed head and shoulders or double tops as no reversal in play.

- Backtest each rule on 20 trading day forward returns with no costs and overlapping signals, and report the sample size beside every win rate, because samples of 2 to 17 signals cannot support strong claims.

- State the data limits in every report. Daily indicator backtests cover about 1 year only, the 7 year read uses monthly bars for trend CAGR and drawdown only, and order flow cannot be tested from daily bars, so use volume at price as the proxy and never claim an order flow read.

- Check price data for label quirks before trusting it, such as a bar whose date label conflicts with the reported high date, and keep Fibonacci levels only when the range endpoints still match the reported 52 week range.

- Run the backtest with the helper script at `~/workspace/backtest/backtest.py` and keep its results beside the report it produced, reusing the script instead of rebuilding the calculations by hand.

## Rank names and set entry stop and target levels

- Rank by trend evidence first using backtest win rates and indicator strength, then by fundamentals, and re-rank after the backtest even when that moves the original research order.

- Set entry zones as limit zones, never as market orders, using good til cancelled limit buys inside the zone, and attach a hold above condition whenever the entry depends on a support level holding.

- Place the stop loss and a limit sell for half the position at target 1 on every fill, and move the stop to the entry price once target 1 hits.

- Size each trade by risk at about 1 percent of the account, and show the arithmetic with a worked example so the share count follows from the entry to stop distance.

- Force pullback only entries with a stated no chase ceiling on any name with RSI at or above 70, and retire a zone as stale when price action moves past it instead of stretching the old zone to fit.

- Name the thesis breaking headline for each name before entry, such as a de-escalation headline for a war driven energy thesis, and treat that headline as an exit even when targets are unmet.

- Say that a gap at the open can blow through entry conditions, so a limit order without its hold above condition attached is not a valid entry.

- Recommend buying shares with cash as the default for this plan, allow a defined risk bull call spread expiring in the second or third month out only as a small side bet, and never sell naked options.

## Apply the public sentiment danger rule

- Check fresh public sentiment on every morning and evening run for each finalist and each watch only name, covering news headlines from the last 24 hours, social chatter tone on X Reddit and Stocktwits, analyst commentary, and options tone where it can be measured.

- Record the sentiment evidence with its source and timestamp in the picks file, and state plainly when nothing concerning was found instead of assuming a clean read.

- Treat concerning news or clearly low sentiment as a danger flag. Concerning news includes regulatory action, safety issues, guidance cuts, executive departures, fraud or accounting questions, major customer loss, geopolitical escalation hitting the name, or a viral negative narrative. Clearly low sentiment means dominant fear or anger tone, a spike in negative mentions, or heavily negative retail chatter.

- Apply the danger effects at once. A flagged name cannot rank first or second, its entry becomes pullback only with a stated no chase ceiling, its stop tightens to the nearest support below the entry zone, and its size halves. Severe danger, meaning two independent concerning items or a sentiment collapse, drops the name to watch only with the reason stated.

- Address a danger flag on a name from a prior day openly in the evening review by exiting early at the next open or holding to the stop, and never hold it silently.

- Treat sentiment as a veto and a tilt only, and never let positive sentiment promote a name that fails steps 1 to 4.

## Score the predictions and tune the method

- Score each morning pick after the close against the regular session close, recording whether the entry zone triggered, whether the stop or target hit, and where the close sits against the zone.

- Give each pick a verdict of worked, worked barely, no trade by design, or failed, name the correction when the analysis was wrong, and recompute RSI MACD and moving averages with the day's close included before setting the next levels.

- Write the tuned next day levels with their conditions attached, such as an invalidation close below a support level, and treat the tuned levels as the starting point for the next screen, not as the answer, since a fresh screen can replace any name.

- Log the scorecard in `~/workspace/swing-daily/picks/<date>.md` and append tuning notes newest first to the tuning log in `~/workspace/swing-daily/ALGORITHM.md`, so the tuning compounds across days.

- Stay quiet on market holidays with a one line note, and never recycle a prior day's numbers when live quotes or news cannot be verified.

## Present results and keep records

- Open with the fresh list and what changed since the last run, give one short takeaway per name, and put the entry zone stop targets and conditions for all five in one place with exact calendar dates on anything time bound.

- State the earnings calendar for the five names, the unverified items, and the sentiment read in the same message, and keep the presentation self contained rather than a delta that forces the user to re-read yesterday.

- Keep the method and tuning log in `~/workspace/swing-daily/ALGORITHM.md`, the daily picks in `~/workspace/swing-daily/picks/`, and the backtest script and reports under `~/workspace/backtest/`, and point a new run at those files instead of restating the method from memory.

- Deliver the morning screen before 7:00 AM PT and the evening review after the close, and update the public page or heatmap only when the user asks in chat.

## Worked example from the October 30 2026 screen

- Screen 34 large cap names through the five steps and keep 5 that passed all of them, with Visa as first reserve on thin upside, while Google Amazon and Meta failed on cash burn and Nebius and others failed on trend.

- Run the indicator backtest and re-rank on trend evidence, moving Gilead to first on the strongest trend following record and Microsoft to second on the weakest timing, with AbbVie third, Exxon fourth on a fragile geopolitical thesis, and Lilly fifth on overextension.

- Name the corrections the evening review caught, an earnings date error on Exxon, an underestimated fade in Microsoft, and a misstated zone placement for Lilly, and add the rule that every run verifies earnings dates before publishing.

- Run the sentiment danger rule the same evening and change no levels, while recording the evidence per name, including euphoric sentiment plus an RSI near 80 keeping Lilly pullback only at half size.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Websites

- Use `browser.search` with the finance vertical for quotes and price history, and with the news vertical for headlines and earnings coverage, and cite the result lines for every price or figure the user will act on.

- Treat vendor moving average RSI and target pages as unverified unless the same levels are computed from price bars, and prefer the computed values when the two disagree.

## Alternatives for better results

- Widen the universe beyond the standing list only when the user asks, keep the large cap preference stated, and require the added name to pass all five steps with an explicit note on why it entered.

- Re-screen a name from scratch after its earnings report instead of carrying pre earnings levels forward, since the report resets the fundamental and technical picture at once.
