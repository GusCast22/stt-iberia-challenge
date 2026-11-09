# stt-iberia-challenge

## Who we are :circus_tent:

We are the Short-Term Optimisation team of the Iberia desk within SEM, part of [ENGIE](https://www.engie.com/), one of the largest global energy players.

We cover the activities in Spain & Portugal, working in small teams that mix people with experience in energy markets, IT and modelling. We trade and optimise assets in the [day-ahead](https://en.wikipedia.org/wiki/European_Power_Exchange#Day-ahead_markets) and [intraday](https://en.wikipedia.org/wiki/European_Power_Exchange#Intraday_markets) markets, and we [work with the TSO to balance the grid](https://en.wikipedia.org/wiki/Transmission_system_operator#Electricity_market_operations). A growing part of what we do is making batteries and solar plants earn their keep in these markets: deciding when to charge, when to discharge and which market to sell in, with imperfect information and real physical limits.

## Welcome! :wave:

Below you can find the description of an analysis challenge that we ask people with coding/analysis skills to perform when applying for a job in our team.

The goal is to give you some insight into the business we're in, and an indication of the kind of problems you will be confronted with day to day.

Time is scarce, we know. Therefore, we ask you not to spend more than **4 to 6 hours** on this challenge. We understand it may not be possible to deliver a fully finished and polished result in that time. Even if your submission is not complete, it will give us plenty of material for a good discussion. Tell us what you did not have time to do.

This coding challenge is part of a formal process and is used in collaboration with the recruiting companies we work with. Submitting your work will not automatically trigger the recruitment process.

## The challenge :rocket:

### In short
We are evaluating a battery in Spain, first on its own and then next to a solar plant. Using Spanish market data and a synthetic PV production profile, tell us how much money it can make, how much of that is realistic, and what you would do to make it better.

### The assets :battery:

| Asset | Specification |
|---|---|
| BESS | 10 MW / 20 MWh, round-trip efficiency 88%, one connection point |
| PV | 50 MW |
| Grid | **Injection limit of 40 MW at the connection point, shared by PV + BESS** |

The injection limit is below the PV rated power, so on many sunny hours the PV produces more than the grid can take. That surplus is "free energy" for the battery: energy that would otherwise be curtailed.

A common way to compare the profitability of a battery is in **EUR per installed kW per year**. Please report your results in that unit too, next to the absolute numbers.

Any other technical or commercial parameter (SoC limits, cycling, degradation, fees, grid-import limit, ...) is yours to define and justify.

### The data :chart_with_upwards_trend:

Everything lives in [`test_bess/data/`](test_bess/data), each file as `.parquet` and `.csv`. Prices come from our internal market-data store (OMIE results and our own forecasts); the PV production profile is synthetic. The period covered is 1 January 2025 to 30 June 2026.

**`prices_es_local`**: Spanish market prices, EUR/MWh

| Column | Description |
|---|---|
| `timestamp_local` | Interval start, Spain local clock |
| `da_price_obs` | OMIE day-ahead price, observed |
| `da_price_fcst` | Day-ahead price forecast, as available before the day-ahead gate closure of D-1 |
| `ida1_price_obs` | IDA1 (first intraday auction) price, observed |

**`pv_production_utc`**: PV production

| Column | Description |
|---|---|
| `timestamp_utc` | Interval start, UTC |
| `pv_production_mw` | Average PV power over the interval, MW, before any grid curtailment (it is **not** limited by the injection limit) |

### The questions :mag:

**Part 1: standalone BESS in the day-ahead market.**
What is the annual day-ahead arbitrage value of the 10 MW / 20 MWh battery?
- Give a theoretical upper bound (perfect foresight) and a value you consider realistically capturable.
- Explain the gap between the two.

**Part 2: co-located PV + BESS under the shared 40 MW limit.**
- What is the value of co-location versus operating the two assets separately?
- Compare charging from grid + PV with charging from PV only.

### Want more challenge? :money_with_wings:

**Part 3: think beyond the brief.**
The questions above do not prescribe how to use everything you are given, nor which markets or decision times to look at. This is where we get curious: extend the assessment in the direction you believe adds the most value to a trading desk, and tell us why. Depth on one good idea is worth more than a list of many.

### What we expect you to hand in :package:

1. A memo of 1-2 pages: approach, results, assumptions, limitations and what you would do next.
2. Your code, reproducible end to end (notebooks or scripts, your choice).

Use any tools you like, AI agents included; we are as interested in your judgement as in your numbers. Assumptions that are not stated here are up to you, but they must be justified.

## More info :bank:

 - [OMIE - Mercado de electricidad](https://www.omie.es/es/mercado-de-electricidad)
 - [EPEX SPOT - Day-ahead and intraday markets](https://en.wikipedia.org/wiki/European_Power_Exchange)
