# Taiwan Supply Chain Research — AI Agent Skills

> [繁體中文](README.md)

An AI agent skill that tracks AI compute supply chain trends through Taiwan's MOPS (Market Observation Post System) monthly revenue data, using the [Culpium methodology](https://www.culpium.com/p/how-to-use-taiwan-monthly-data-to).

## What it does

- Fetches monthly revenue data from Taiwan-listed companies (TSMC, Foxconn, Quanta, etc.)
- Applies analytical rules: YoY growth, Jan+Feb combo, rolling 12-month, USD conversion
- Maps revenue signals across 4 supply chain tiers (Upstream → Mid-Stream → Downstream → Capex)
- Outputs structured research reports with timeline implications

## Data source

**MOPS (Market Observation Post System)**: https://mops.twse.com.tw

All Taiwan-listed companies are required to publish monthly revenue by the 10th of the following month.

## Methodology

Based on the [Culpium guide to Taiwan monthly data](https://www.culpium.com/p/how-to-use-taiwan-monthly-data-to):

1. **YoY growth** — always compare to same month last year
2. **Jan+Feb combo** — Lunar New Year shifts between months
3. **Rolling 12-month** — smooths seasonality
4. **USD conversion** — removes TWD fluctuation noise
5. **Seasonality awareness** — Q1 weak for semis, Q4 strong for consumer