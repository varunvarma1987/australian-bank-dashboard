# Australian Bank FY25 Dashboard — Master Orchestration

## Overview
This project builds an interactive financial analytics dashboard comparing Australia's Big 4 banks (CBA, NAB, ANZ, Westpac) and Macquarie Group. It is designed as a **repeatable, agent-driven pipeline** that can be re-run annually with minimal changes.

## How to Run

### Full Pipeline (recommended for first run or annual update)
```
Run the full dashboard pipeline: extract data, build all charts, generate commentary, and assemble the final dashboard.
```

### Individual Agents
```
Run Agent 1: Extract FY25 data for all 5 banks
Run Agent 2: Build all chart components
Run Agent 3: Generate commentary and analysis
Run Agent 4: Assemble the final dashboard
```

### Single Chart Rebuild
```
Rebuild the ROE chart only
Rebuild the NIM chart with updated styling
```

---

## Pipeline Sequence

The pipeline runs in strict order. Each agent reads its own SKILL.md before executing.

### Agent 1 — Data Extraction
- **Skill**: `skills/01-extract-data/SKILL.md`
- **Input**: Web search for latest annual results
- **Output**: `data/bank-metrics.json`
- **What it does**: Searches for the latest FY results for each bank, extracts ROE, NIM, Cost-to-Income, CET1, and NPAT, validates the numbers, and writes structured JSON.

### Agent 2 — Chart Generation
- **Skill**: `skills/02-build-charts/SKILL.md` (master), plus individual chart skills
- **Input**: `data/bank-metrics.json`
- **Output**: Individual chart HTML/JS modules in `dashboard/src/`
- **Sub-skills** (each defines style, format, animation):
  - `skills/02-build-charts/roe/SKILL.md` — ROE grouped bar chart
  - `skills/02-build-charts/nim/SKILL.md` — NIM line/bar hybrid chart
  - `skills/02-build-charts/cti/SKILL.md` — Cost-to-Income horizontal lollipop
  - `skills/02-build-charts/cet1/SKILL.md` — CET1 bullet chart with threshold
  - `skills/02-build-charts/overview/SKILL.md` — KPI cards and summary table

### Agent 3 — Commentary Generation
- **Skill**: `skills/03-generate-commentary/SKILL.md`
- **Input**: `data/bank-metrics.json`
- **Output**: `data/commentary.json`
- **What it does**: Computes YoY changes, peer rankings, identifies leaders/laggards, generates analyst-style commentary per metric.

### Agent 4 — Dashboard Assembly
- **Skill**: `skills/04-assemble-dashboard/SKILL.md`
- **Input**: Chart modules from `dashboard/src/`, commentary from `data/commentary.json`, metrics from `data/bank-metrics.json`
- **Output**: `dashboard/index.html` — Single-file interactive dashboard

---

## Bank Configuration

| Code | Bank Name | Brand Color | FY End Month |
|------|-----------|-------------|--------------|
| CBA | Commonwealth Bank of Australia | #FFD700 | June |
| NAB | National Australia Bank | #E63946 | September |
| ANZ | ANZ Banking Group | #3B82F6 | September |
| WBC | Westpac Banking Corporation | #D5002B | September |
| MQG | Macquarie Group | #8B5CF6 | March |

## Target Metrics

| Metric | Key | Unit | Direction |
|--------|-----|------|-----------|
| Return on Equity | roe | % | Higher is better |
| Net Interest Margin | nim | % | Higher is better |
| Cost-to-Income Ratio | cti | % | Lower is better |
| CET1 Capital Ratio | cet1 | % | Higher (above 10.25% APRA min) |
| Cash Net Profit After Tax | npat | $m | Higher is better |

## Annual Update Checklist
1. Update the FY year reference in `skills/01-extract-data/SKILL.md`
2. Run: `Run Agent 1: Extract data for all 5 banks`
3. Review `data/bank-metrics.json` for accuracy
4. Run: `Run Agent 2, 3, and 4 to rebuild dashboard`
5. Final output: `dashboard/index.html`

## Design System
- **Theme**: Dark mode (#0a0e17 base)
- **Fonts**: Playfair Display (headings), DM Sans (body)
- **Charts**: D3.js v7 with GSAP-style CSS animations
- **Layout**: Full-viewport scrollable sections with scroll-snap
- **Mobile**: Responsive, touch-friendly, swipeable charts
