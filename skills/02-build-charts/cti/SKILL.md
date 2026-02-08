# Skill: Cost-to-Income Lollipop Chart

## Chart Type
**Horizontal lollipop chart** — bars extend from left to right, sorted from BEST (lowest C/I) at the top to WORST at the bottom. This is a distinctly different layout from the other bar charts, providing visual variety.

## Data Source
`data/bank-metrics.json` → `banks[].metrics.cti`

## Visual Specification

### Layout
- **Horizontal orientation**: bank names on Y-axis (left), values extend right
- Sorted TOP to BOTTOM from lowest (best) to highest (worst) C/I ratio
- X-axis domain: 40% to 58%
- Each row shows: a thin line (2px) from the y-axis to the value point, then a circle (dot) at the end

### Lollipop Elements
- **Stem**: Horizontal line, 2px height, bank's brand color at 40% opacity
- **Dot**: Circle at the end of the stem, radius 8px, filled with bank's brand color
- **Value label**: Next to the dot (right side), showing "XX.X%", 12px, white, font-weight 600

### Special Elements
- **Efficiency zone**: Background shading from 40% to 46% in subtle green (`rgba(16, 185, 129, 0.05)`) to visually indicate the "efficient" zone
- **Label**: Small text "Efficient zone" at top-left of the green band, 9px, color `--positive`
- **Peer average**: Vertical dashed line at the average C/I, labeled "Peer avg"

### Y-Axis Labels
- Show full bank names (not codes) on the left: "CBA", "NAB", etc.
- Preceded by a colored dot (8px) matching the bank color
- Font size: 13px, weight 500

### Hover
- On dot hover: enlarge dot to radius 11px, show tooltip
- Tooltip: bank name, C/I value, rank position (e.g., "#1 Most Efficient")

### Animation
- Each lollipop stem grows from left to right, 600ms, staggered 120ms per row
- Dot pops in with a scale animation (0 → 1) when the stem reaches it
- Value labels fade in 200ms after dot appears

### Section Context
- Section tag: "EFFICIENCY"
- Section title: "Cost-to-Income Ratio"
- Section subtitle: "Lower is better — this ratio shows how many cents of every dollar of revenue are consumed by operating costs."
- **Important note**: Include a small footnote below the chart: "Note: ANZ and Westpac FY25 figures include significant restructuring charges. Underlying ratios are approximately 3-5 percentage points lower."

### Mobile
- Reduce dot radius to 6px
- Value labels: 11px
- Bank name labels may abbreviate to codes if width < 400px

## Commentary Trigger
Display commentary from `data/commentary.json` → `cti` key.
