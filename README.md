# stt-iberia-challenge

## Who we are :circus_tent:

We are the Short Term Trading (STT) team of the Iberia desk within S&EM, part of [ENGIE](https://www.engie.com/), one of the largest global energy players. Our mission is simple to say and hard to do: **optimise assets and trade in the physical power markets of Spain and Portugal**, maximising the value we generate while keeping imbalances low and respecting regulation.

**What we look after.** A diversified Iberian portfolio: hydro (including pumped storage), wind and solar, gas-fired plants, supply to business customers, and a growing fleet of batteries (BESS).

**Where we trade.** Every day we bid in the [OMIE](https://www.omie.es/en) day-ahead market, adjust positions in the intraday auctions and the continuous intraday market, offer flexibility to the TSO in the balancing and ancillary-service markets, and manage the resulting imbalances. Markets are moving to 15-minute products, so resolution matters.

**How a day looks.** Decisions start the day before delivery, with forecasts, asset availability and constraints feeding the day-ahead bids. From then on we keep re-optimising as new information arrives: updated prices and weather, unplanned outages, market opportunities. A 24/7 shift team in Madrid executes the strategies, while the control centres operate the assets physically.

**Who we are.** Traders and shift operators, an analytics and market intelligence group that builds the models and algorithms behind our strategies, and dedicated IT colleagues who put them into production. We are a small team where people with market, modelling and software backgrounds work side by side.

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
| `ida1_price_obs` | IDA1 (first intraday auction) price, observed |

**`da_price_fcst_es_local`**: day-ahead price forecast, EUR/MWh

| Column | Description |
|---|---|
| `timestamp_local` | Delivery interval start, Spain local clock |
| `da_price_fcst` | Day-ahead price forecast, as available before the day-ahead gate closure of D-1 |

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

Your code, reproducible end to end, as a notebook or scripts (your choice). There is no separate memo: explain your approach, results, assumptions, limitations and what you would do next in the code itself, for example in markdown cells if you use a notebook.

Use any tools you like, AI agents included; we are as interested in your judgement as in your numbers. Assumptions that are not stated here are up to you, but they must be justified.

## More info :bank:

 - [OMIE - Mercado de electricidad](https://www.omie.es/es/mercado-de-electricidad)
