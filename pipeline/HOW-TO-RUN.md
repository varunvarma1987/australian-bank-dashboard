# Pipeline Runner — How to Execute in Claude Code / VS Code

## Prerequisites
- Claude Code CLI installed (`npm install -g @anthropic-ai/claude-code`)
- VS Code with terminal access
- This project cloned/opened in VS Code

## Quick Start

### Option 1: Full Pipeline (One Command)
Open your terminal in VS Code and run:
```bash
claude "Read CLAUDE.md and run the full dashboard pipeline. Start by reading each skill file in skills/ before executing that step."
```

### Option 2: Step-by-Step

#### Step 1: Extract Data
```bash
claude "Read skills/01-extract-data/SKILL.md. Search the web for the latest FY results for CBA, NAB, ANZ, Westpac, and Macquarie. Extract ROE, NIM, Cost-to-Income, CET1, NPAT, EPS, and DPS. Write the results to data/bank-metrics.json following the schema in the skill file."
```

#### Step 2: Build Charts
```bash
claude "Read skills/02-build-charts/SKILL.md and ALL sub-skill files in skills/02-build-charts/*/SKILL.md. Using data from data/bank-metrics.json, generate D3.js chart components following the exact specifications in each sub-skill. Write output to dashboard/src/."
```

#### Step 3: Generate Commentary
```bash
claude "Read skills/03-generate-commentary/SKILL.md. Analyse data/bank-metrics.json and generate analyst-style commentary. Write to data/commentary.json."
```

#### Step 4: Assemble Dashboard
```bash
claude "Read skills/04-assemble-dashboard/SKILL.md. Combine chart components from dashboard/src/, commentary from data/commentary.json, and metrics from data/bank-metrics.json into a single interactive HTML file at dashboard/index.html."
```

### Option 3: Rebuild a Single Chart
```bash
claude "Read skills/02-build-charts/cti/SKILL.md. Rebuild the Cost-to-Income chart as a horizontal lollipop chart using data from data/bank-metrics.json. The chart should be sorted from most efficient (top) to least efficient (bottom)."
```

### Option 4: Update for Next Financial Year
```bash
claude "Read CLAUDE.md. It's time to update for FY26. Run Agent 1 to extract the latest data for all 5 banks, then run Agents 2-4 to rebuild the dashboard."
```

## Customisation Commands

### Change chart style
```bash
claude "Read skills/02-build-charts/roe/SKILL.md. Change the ROE chart from a bar chart to a radar/spider chart comparing all 5 banks across ROE, NIM, CTI, and CET1."
```

### Add a new metric
```bash
claude "Add Dividend Yield as a new metric to the dashboard. Update skills/01-extract-data/SKILL.md to include it, create a new chart skill at skills/02-build-charts/div-yield/SKILL.md, and rebuild the dashboard."
```

### Change theme
```bash
claude "Update the design system in skills/02-build-charts/SKILL.md to use a light theme with white backgrounds and dark text. Rebuild all charts."
```

## Tips for Best Results
1. **Always point Claude to the skill file first** — this ensures consistent output
2. **Review data/bank-metrics.json after Agent 1** — verify the numbers before building charts
3. **Use specific chart rebuild commands** when iterating on individual visualisations
4. **The skills are the source of truth** — edit them to change behaviour permanently
