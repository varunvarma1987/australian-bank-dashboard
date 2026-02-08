# Skill: CET1 Capital Ratio Bullet Chart

## Chart Type
**Vertical bar chart with regulatory threshold line** — emphasising the buffer each bank holds above APRA's minimum CET1 requirement.

## Data Source
`data/bank-metrics.json` → `banks[].metrics.cet1` and `apra_cet1_minimum`

## Visual Specification

### Layout
- Bars sorted LEFT to RIGHT from highest to lowest CET1
- Y-axis domain: 10% to 14%
- Each bar uses the bank's brand color

### Critical Element: APRA Threshold Line
- Horizontal line at **10.25%** (APRA minimum CET1 requirement)
- Style: dashed (6,4), color `#ef4444` (red), 1.5px width
- Label: "APRA Minimum 10.25%" right-aligned, 10px, color `#ef4444`
- This line is the KEY visual anchor — it should be prominent

### Buffer Annotation
- For each bar, calculate the buffer: `cet1 - 10.25`
- Show a subtle bracket or annotation on the bar indicating the buffer
- Alternative: color the portion of each bar BELOW 10.25% in a muted version of the bank's color (20% opacity), and the portion ABOVE in full opacity — this creates a visual "split" showing the safety margin

### Labels
- Bank code on x-axis
- Value label (e.g., "12.8%") above each bar
- Crown emoji on #1 performer
- Optionally show buffer in small text below value: "(+2.55pp)"

### Hover
- Tooltip shows: bank name, CET1 value, buffer above APRA minimum
  - e.g., "Macquarie — 12.8% (buffer: +2.55pp above minimum)"

### Animation
- APRA threshold line draws first (400ms, left to right)
- Bars then grow upward from 10.25% baseline (not from 0), 800ms staggered
- This creates the visual effect of bars "emerging" above the regulatory floor

### Section Context
- Section tag: "CAPITAL STRENGTH"
- Section title: "CET1 Capital Ratio"
- Section subtitle: "Common Equity Tier 1 ratio measures the bank's core capital buffers — the critical safety net above APRA's minimum requirements."
- **Context note**: "APRA announced in July 2025 plans to phase out AT1 capital from January 2027, which will increase CET1 targets by ~25bps."

### Mobile
- Reduce label sizes
- Buffer annotations can be omitted on mobile — just show the threshold line and values

## Commentary Trigger
Display commentary from `data/commentary.json` → `cet1` key.
