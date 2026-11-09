# BESS arbitrage on the Spanish market – technical test

**Context.** You join the Iberia short-term trading desk. We are evaluating a battery in Spain, first standalone and then co-located with a solar plant. You are given one year (2025) of market data and a synthetic PV profile. You may use any tools, including AI agents; we assess your judgement as much as your numbers.

## Assets

| Asset | Specification |
|---|---|
| BESS | 10 MW / 20 MWh, round-trip efficiency 88%, one connection point |
| PV | 50 MW AC (about 65 MWp DC), southern Spain, synthetic profile |
| Grid | **Injection limit of 50 MW at the connection point, shared by PV + BESS** |

Any other technical or commercial parameter (SoC limits, cycling, degradation, fees, grid-import limit, …) is yours to define and justify.

## Data (`data/`, each file as `.parquet` and `.csv`)

**`prices_es_2025_local`** – Spanish market prices, EUR/MWh

| Column | Description |
|---|---|
| `timestamp_local` | Interval start, Spain local clock |
| `da_price_obs` | OMIE day-ahead price, observed |
| `da_price_fcst` | Day-ahead price forecast, as available before the day-ahead gate closure of D-1 |
| `ida1_price_obs` | IDA1 (first intraday auction) price, observed |

**`pv_potential_2025_utc`** – PV potential generation

| Column | Description |
|---|---|
| `timestamp_utc` | Interval start, UTC |
| `pv_potential_mw` | Average PV power over the interval, MW. Unclipped potential at the DC side: it can exceed 50 MW and is **not** limited by the grid limit |

## Questions

**Part 1 – Standalone BESS in the day-ahead market.**
What is the annual day-ahead arbitrage value of the 10 MW / 20 MWh battery?
- Give a theoretical upper bound (perfect foresight) and a value you consider realistically capturable.
- Explain the gap between the two.
- Show at least two sensitivities (e.g. on the parameters or the assumptions that matter most).

**Part 2 – Co-located PV + BESS under the shared 50 MW limit.**
- What is the value of co-location versus operating the two assets separately?
- Compare charging from grid + PV with charging from PV only.
- What is the impact on the PV capture price?

**Part 3 – Think beyond the brief.**
The questions above do not prescribe how to use all the data you are given, nor which markets or decision times to consider. Extend the assessment in the direction you believe adds the most value to a trading desk, and explain why. Depth on one idea is worth more than a list of many.

## Deliverables

1. A memo of 1–2 pages: approach, results, assumptions, limitations, and what you would do next.
2. Your code, reproducible end to end.
3. Your agent prompts / interaction log.

Timebox: 4–6 hours. Be explicit about what you did not have time to do.
