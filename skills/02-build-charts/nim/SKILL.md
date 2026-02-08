# Skill: NIM Chart

## Chart Type
Vertical bar chart with a **peer average reference line** — one bar per bank, sorted by NIM descending.

## Data Source
`data/bank-metrics.json` → `banks[].metrics.nim`

## Visual Specification

### Layout
- Bars sorted LEFT to RIGHT from highest to lowest NIM
- Y-axis domain: start at 1.0%, max at 2.5%
- Each bar uses the bank's brand color
- Bar corner radius: 6px
- Bar padding ratio: 0.35

### Special Elements
- **Peer average line**: Dashed horizontal line at the average NIM of all 5 banks
  - Style: dashed (6,4), color `#94a3b8`, 1.5px width
  - Label: "Peer avg: X.XX%" right-aligned, 10px, color `--text-secondary`
- **Spread annotation**: For the top performer, show a small annotation arrow or bracket from the peer average to the bar top, labeled with the spread (e.g., "+25bps above avg")

### Labels
- Bank code on x-axis
- Value label (e.g., "2.08%") above each bar
- Crown emoji on #1 performer

### Hover
- Tooltip shows: bank name, NIM value, and bps difference from peer average
  - e.g., "CBA — 2.08% (+25bps vs peer avg)"

### Animation
- Same as ROE chart (staggered bar growth from bottom)
- Peer average line draws from left to right over 600ms after bars finish

### Section Context
- Section tag: "MARGINS"
- Section title: "Net Interest Margin"
- Section subtitle: "NIM captures the spread between what banks earn on loans and pay on deposits — the core engine of bank profitability."

### Mobile
- If bars feel cramped, reduce to 3 decimal places (e.g., 2.08 → 2.1)
- Peer average line label can wrap to 2 lines

## Commentary Trigger
Display commentary from `data/commentary.json` → `nim` key.
