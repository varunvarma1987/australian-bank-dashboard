# Skill: ROE Bar Chart

## Chart Type
Grouped vertical bar chart — one bar per bank, sorted by ROE descending (best performer on the left).

## Data Source
`data/bank-metrics.json` → `banks[].metrics.roe`

## Visual Specification

### Layout
- Bars sorted LEFT to RIGHT from highest to lowest ROE
- Y-axis starts at 0%, max at ~16% (or 115% of the highest value)
- Each bar uses the bank's brand color at 90% opacity
- Bar corner radius: 6px (top corners only via `rx`)
- Bar padding ratio: 0.35

### Labels
- Bank code (e.g., "CBA") on x-axis below each bar
- Value label (e.g., "13.5%") centered above each bar, white, 13px, font-weight 600
- Crown emoji (👑) above the #1 performer, 14px, appears with fade-in after 1s

### Grid
- Horizontal grid lines: dashed (2,4), color `--border`
- Y-axis tick format: `d + "%"`
- No visible axis lines (remove `.domain`)

### Hover Interaction
- On hover: bar opacity drops to 0.85
- Tooltip shows: bank full name + ROE value
- Tooltip follows cursor

### Animation
- Bars grow from y=height upward over 800ms, eased with `d3.easeCubicOut`
- Each bar delayed by 100ms × index (staggered entrance)
- Value labels fade in 400ms after bars finish
- Crown fades in at 1000ms

### Section Context
- Section tag: "PROFITABILITY"
- Section title: "Return on Equity"
- Section subtitle: "ROE measures how effectively banks generate profit from shareholders' equity — the ultimate measure of capital efficiency."

### Mobile Adaptations
- Reduce bar padding to 0.25
- Value labels: 11px
- Consider rotating x-axis labels 45° if needed

## Commentary Trigger
After rendering, this chart's section should display a commentary card from `data/commentary.json` → `roe` key.
