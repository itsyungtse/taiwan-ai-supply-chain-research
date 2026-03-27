---
name: taiwan-supply-chain-research
description: |
  Research Taiwan monthly revenue data (MOPS) to track AI compute supply chain trends.
  Fetches company/sector revenue from Taiwan's Market Observation Post System, applies
  Culpium methodology (YoY growth, rolling 12-month, Jan+Feb combo, USD conversion),
  and maps findings to upstream/midstream/downstream/capex tiers.
  Use when asked to "track supply chain", "taiwan revenue", "MOPS data",
  "AI compute trends", "semiconductor supply chain", or "taiwan monthly data".
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - WebFetch
  - WebSearch
  - AskUserQuestion
---

# Taiwan Supply Chain Research

Research and analyze Taiwan monthly revenue data to track AI compute supply chain trends,
based on the Culpium methodology: https://www.culpium.com/p/how-to-use-taiwan-monthly-data-to

## Primary Data Source

**MOPS (Market Observation Post System)**: https://mops.twse.com.tw

All Taiwan-listed companies must publish monthly revenue by the 10th of the following month.
Data is available in both Chinese and English with CSV export.

## Step 1: Identify Target Companies

Map the user's research question to the correct supply chain tier:

| Tier | Role | Key Companies | What It Tells You |
|------|------|---------------|-------------------|
| **Upstream** | Chip manufacturing, passive components | TSMC (2330), UMC (2303), MediaTek (2454), ASE (3711) | Chip demand, fab utilization |
| **Mid-Stream** | Module/system assembly | Gigabyte (2376), Cooler Master (3017), Hon Hai/Foxconn (2317), Delta (2308) | Server/GPU module demand |
| **Downstream** | Final product assembly | Wistron (3231), Quanta (2382), Inventec (2356), Compal (2324) | End-customer pull-through |
| **Equipment/Capex** | Machinery, testing equipment | Gudeng (3680), Hermes-Epitek (3605), Scientech (3553) | Future capacity expansion |

### Timeline Lag (construction to product):
- **36 months**: Construction start → finished product
- **24 months**: Equipment installation
- **12-18 months**: Chip production begins
- **3-6 months**: Module assembly
- **0-6 months**: Final assembly

Use these lags to interpret what current revenue signals mean for future supply.

## Step 2: Fetch Revenue Data

Use WebFetch or WebSearch to retrieve monthly revenue data from MOPS.

**English MOPS portal**: https://emops.twse.com.tw/server-java/t58query

Search approaches:
1. **By company**: Search stock ticker (e.g., "2330" for TSMC) on MOPS
2. **By industry group**: MOPS categorizes companies by sector for aggregate views
3. **Web search fallback**: Search `site:mops.twse.com.tw {company} monthly revenue` or use financial data aggregators

Also check these supplementary sources:
- **TSIA (Taiwan Semiconductor Industry Association)**: Aggregate semiconductor revenue
- **Company investor relations pages**: Often have English monthly revenue PDFs
- **Financial news**: MoneyDJ (moneydj.com), DIGITIMES, Nikkei Asia for context

## Step 3: Apply Analytical Rules

**CRITICAL**: Follow these rules strictly to avoid misleading conclusions.

### Rule 1: Default to Year-over-Year (YoY) Growth
Month-over-month is too volatile. Always compare to the same month last year.

```
YoY Growth = (Current Month Revenue - Same Month Last Year) / Same Month Last Year * 100
```

### Rule 2: Combine January + February
Lunar New Year shifts between Jan and Feb each year. Always sum Jan+Feb and compare the combined period YoY.

```
Jan+Feb 2026 combined vs Jan+Feb 2025 combined
```

### Rule 3: Use Rolling 12-Month Sums for Trends
Smooths out seasonality and gives the clearest trend signal.

```
Rolling 12M = Sum of most recent 12 months of revenue
Compare to prior 12-month period for growth rate
```

### Rule 4: Convert Exporters to USD
Taiwan dollar fluctuations distort revenue for export-heavy companies. Use TWD/USD rate for the period.

```
USD Revenue = TWD Revenue / Average TWD/USD Rate for the month
```

### Rule 5: Recognize Sector Seasonality
- **Semiconductors**: Q1 typically weakest, Q3-Q4 strongest (new product launches)
- **Servers/AI**: Can be lumpy — large hyperscaler orders create spikes
- **Consumer electronics**: Q4 holiday pull-in, Q1 post-holiday dip

## Step 4: Structure the Analysis

Output the research as a structured report:

```markdown
# Taiwan Supply Chain Research Report
**Date**: {current date}
**Focus**: {user's research question}
**Period**: {months analyzed}

## Key Findings
- {Top 3 bullet points — the "so what"}

## Revenue Data

### {Tier Name} — {Company Name} ({Ticker})
| Month | Revenue (TWD M) | YoY Growth | Rolling 12M |
|-------|----------------|------------|-------------|
| ...   | ...            | ...        | ...         |

## Supply Chain Signal
- **Upstream**: {what chip revenue tells us}
- **Mid-Stream**: {what module/assembly revenue tells us}
- **Downstream**: {what final assembly tells us}
- **Capex/Equipment**: {what equipment orders tell us about future capacity}

## Timeline Implications
Based on the {X}-month lag from {tier} to end product:
- {What current data implies for future quarters}

## Methodology Notes
- Data source: MOPS (mops.twse.com.tw)
- Currency: {TWD or USD-converted, with rate used}
- Jan/Feb combined: {yes/no, if applicable}
- Seasonality context: {any relevant seasonal factors}
```

## Step 5: Save Results

Save the report to the project directory:
- `research/taiwan-supply-chain/{YYYY-MM-DD}-{topic}.md`

If the directory doesn't exist, create it.

## Interactive Mode

If the user doesn't specify a focus, ask:

1. **Which tier?** Upstream (chips), Mid-stream (modules), Downstream (assembly), Capex (equipment), or All?
2. **Which companies?** Specific tickers, or use defaults for the tier?
3. **Time period?** Most recent month, last 3 months, last 12 months?
4. **AI compute focus?** Specifically tracking AI/GPU server supply chain, or broader tech?

## Quick Reference: AI Compute Supply Chain

For AI-specific tracking, prioritize these companies:

| Company | Ticker | Role in AI Compute |
|---------|--------|--------------------|
| TSMC | 2330 | Fabricates NVIDIA/AMD AI chips (CoWoS packaging) |
| Hon Hai (Foxconn) | 2317 | Assembles NVIDIA GB200/GB300 AI servers |
| Quanta | 2382 | #1 AI server ODM for hyperscalers |
| Wistron / Wiwynn | 3231/6669 | AI server design & assembly |
| Delta Electronics | 2308 | Power supplies for AI data centers |
| Gigabyte | 2376 | GPU server systems |
| ASE Technology | 3711 | Advanced chip packaging (CoWoS partner) |
| Gudeng | 3680 | FOUP/wafer carriers — capex signal |
