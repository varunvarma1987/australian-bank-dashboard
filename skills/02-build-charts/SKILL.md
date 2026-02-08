# Skill: Build Chart Components

## Purpose
Generate D3.js chart components for each financial metric, reading data from `data/bank-metrics.json` and outputting modular chart files to `dashboard/src/`.

## When to Use
Run after Agent 1 (data extraction) has produced `data/bank-metrics.json`.

## Sub-Skills
Each chart type has its own skill file defining the exact style, format, animation, and layout. **Always read the relevant sub-skill before building that chart.**

| Chart | Skill File | Output File |
|-------|-----------|-------------|
| Overview KPIs | `skills/02-build-charts/overview/SKILL.md` | `dashboard/src/overview.html` |
| ROE | `skills/02-build-charts/roe/SKILL.md` | `dashboard/src/roe-chart.html` |
| NIM | `skills/02-build-charts/nim/SKILL.md` | `dashboard/src/nim-chart.html` |
| Cost-to-Income | `skills/02-build-charts/cti/SKILL.md` | `dashboard/src/cti-chart.html` |
| CET1 | `skills/02-build-charts/cet1/SKILL.md` | `dashboard/src/cet1-chart.html` |

## Shared Design System

All charts MUST follow these design tokens:

### Colors
```css
--bg-primary: #0a0e17;
--bg-card: #111827;
--bg-card-hover: #1a2235;
--border: #1e293b;
--text-primary: #f1f5f9;
--text-secondary: #94a3b8;
--text-muted: #64748b;
--accent-gold: #f59e0b;
```

### Bank Colors (ALWAYS use these exact values)
```css
--cba: #FFD700;    /* Gold */
--nab: #E63946;    /* Red */
--anz: #3B82F6;    /* Blue */
--wbc: #D5002B;    /* Crimson */
--mqg: #DADADA;    /* Light Gray */
```

### Typography
- Headings: `'Playfair Display', serif` — weight 600 or 700
- Body/labels: `'DM Sans', sans-serif` — weight 400 or 500
- Axis text: `'DM Sans'` at 11px, color `--text-muted`
- Value labels on bars: `'DM Sans'` at 13px (11px mobile), weight 600

### Chart Container
Every chart must be wrapped in:
```html
<div class="chart-container">
  <div class="chart-title">[Title]</div>
  <div class="chart-subtitle">[Subtitle]</div>
  <div class="chart-area" id="[chart-id]"></div>
</div>
```

### Responsive Rules
- Use `viewBox` on SVGs, never fixed width/height
- Minimum chart width: 300px
- Mobile breakpoint: 640px
- On mobile: reduce padding, font sizes, bar spacing
- Charts must be horizontally scrollable if needed

### Animation Standards
- Bars: grow from bottom, 800ms, `d3.easeCubicOut`, staggered 100ms per bar
- Value labels: fade in after bars finish (400ms delay)
- Leader indicator (crown emoji): fade in after 1000ms
- Use Intersection Observer — charts only animate when scrolled into view

### Tooltip Standard
```html
<div class="tooltip-d3" id="tooltip">
  <div class="tt-bank">[Bank Name]</div>
  <div class="tt-val">[Value with unit]</div>
</div>
```
- Position: fixed, follows cursor with 14px x-offset
- Background: #1e293b, border: #334155, border-radius: 10px
- Appears on mousemove, disappears on mouseleave

### D3.js Version
Always use D3 v7: `https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js`

## Execution Order
1. Read `data/bank-metrics.json`
2. Read each sub-skill SKILL.md
3. Generate each chart component
4. Write files to `dashboard/src/`
