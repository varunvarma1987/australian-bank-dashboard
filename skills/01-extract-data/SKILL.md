# Skill: Extract Bank Financial Data

## Purpose
Search for and extract the latest annual financial results for Australia's Big 4 banks and Macquarie Group, then output structured JSON.

## When to Use
Run this skill when updating the dashboard with new financial year data, or when any bank releases new results.

## Banks to Extract

| Code | Full Name | FY End | Search Terms |
|------|-----------|--------|--------------|
| CBA | Commonwealth Bank of Australia | June | "CBA full year results", "Commonwealth Bank annual results" |
| NAB | National Australia Bank | September | "NAB full year results", "National Australia Bank annual results" |
| ANZ | ANZ Banking Group | September | "ANZ full year results", "ANZ Group Holdings annual results" |
| WBC | Westpac Banking Corporation | September | "Westpac full year results", "Westpac annual results" |
| MQG | Macquarie Group | March | "Macquarie Group full year results", "Macquarie annual results" |

## Metrics to Extract

For each bank, extract the following on a **cash/continuing operations basis**:

| Metric | JSON Key | Unit | Source Location |
|--------|----------|------|-----------------|
| Cash Net Profit After Tax | `npat_m` | $AUD millions | Results announcement headline |
| Return on Equity (Cash) | `roe` | % | Results announcement KPI summary |
| Net Interest Margin | `nim` | % | Group NIM including Treasury & Markets |
| Cost-to-Income Ratio | `cti` | % | Reported or calculated (opex/income) |
| CET1 Capital Ratio | `cet1` | % | APRA Level 2 basis |
| Earnings Per Share | `eps` | cents | Cash EPS |
| Dividend Per Share | `dps` | cents | Full year total |
| Dividend Yield | `dividend_yield` | % | DPS / share price × 100 (use price at results date) |

## Extraction Process

### Step 1: Search for Results
For each bank, search the web using the search terms above plus the current FY year. Prioritise:
1. Official bank investor relations pages and ASX announcements
2. Results announcement PDFs (profit announcement documents)
3. Reputable financial news analysis (MarketScreener, Motley Fool AU, Livewire)

### Step 2: Cross-Validate
- Each metric should be confirmed from at least 2 sources
- Flag any metric where sources disagree with `"confidence": "low"`
- Note if a metric includes or excludes notable/significant items

### Step 3: Record Metadata
For each bank, also capture:
- `fy_year`: The financial year label (e.g., "FY25")
- `fy_end_date`: The exact end date (e.g., "2025-06-30")
- `results_date`: When results were announced
- `source_url`: Primary source URL

## Output Schema

Write to `data/bank-metrics.json`:

```json
{
  "metadata": {
    "generated_at": "ISO timestamp",
    "fy_label": "FY25",
    "notes": "Any general notes about comparability"
  },
  "banks": [
    {
      "code": "CBA",
      "name": "Commonwealth Bank of Australia",
      "color": "#FFD700",
      "fy_year": "FY25",
      "fy_end_date": "2025-06-30",
      "results_date": "2025-08-12",
      "source_url": "https://...",
      "metrics": {
        "npat_m": 10252,
        "roe": 13.5,
        "nim": 2.08,
        "cti": 45.5,
        "cet1": 12.3,
        "eps": 613.2,
        "dps": 485,
        "dividend_yield": 4.2
      },
      "yoy_changes": {
        "npat_pct": 4,
        "roe_bps": -10,
        "nim_bps": 9,
        "cti_bps": null,
        "cet1_bps": 0
      },
      "notes": "Cash NPAT on continuing operations basis. CET1 APRA Level 2."
    }
  ],
  "apra_cet1_minimum": 10.25,
  "rankings": {
    "roe": ["CBA", "NAB", "MQG", "WBC", "ANZ"],
    "nim": ["CBA", "WBC", "MQG", "NAB", "ANZ"],
    "cti": ["CBA", "NAB", "MQG", "WBC", "ANZ"],
    "cet1": ["MQG", "WBC", "CBA", "ANZ", "NAB"],
    "npat": ["CBA", "NAB", "WBC", "ANZ", "MQG"],
    "dividend_yield": ["ANZ", "WBC", "NAB", "CBA", "MQG"]
  }
}
```

## Validation Rules
- ROE should be between 5% and 20% for Australian majors
- NIM should be between 1.0% and 2.5%
- CTI should be between 35% and 60%
- CET1 should be above 10.25% (APRA minimum)
- NPAT should be positive and in the billions range
- Dividend yield should be between 2% and 8% for Australian majors

If any value falls outside these ranges, flag it and double-check the source.

## Calculating Dividend Yield
```javascript
dividend_yield = (DPS in cents / Share price on results date) × 100
```

Example: CBA announces DPS of 485 cents, share price is $115:
```
dividend_yield = (4.85 / 115) × 100 = 4.22% → round to 4.2%
```

Use the closing share price on the results announcement date, or the previous trading day's close if results are announced after market close.

## Important Notes
- **CBA reports on a June FY** — its "FY25" ends June 2025. The other Big 4 report September FY.
- **Macquarie reports on a March FY** — its "FY25" ends March 2025.
- Macquarie is a diversified financial group, not a pure bank. NIM and CTI may not be directly comparable. Note this in the metadata.
- Always prefer **cash basis** over statutory for profit and ROE.
- For CTI, note whether the figure includes or excludes notable/significant items.
