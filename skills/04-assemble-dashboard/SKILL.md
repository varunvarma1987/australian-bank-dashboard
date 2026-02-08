# Skill: Assemble Final Dashboard

## Purpose
Combine all chart components, commentary, and data into a single interactive HTML file.

## When to Use
Run as the final step after Agents 1-3 have completed.

## Inputs
- `data/bank-metrics.json` — Structured financial data
- `data/commentary.json` — Generated commentary
- Chart sub-skills from `skills/02-build-charts/` — For style reference

## Output
- `dashboard/index.html` — Single-file interactive dashboard (all CSS/JS inline)

## Assembly Rules

### 1. Single File Architecture
The final dashboard MUST be a single `.html` file with:
- All CSS in a `<style>` block
- All JavaScript inline in a `<script>` block
- D3.js loaded from CDN: `https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js`
- Google Fonts loaded from CDN for Playfair Display and DM Sans
- NO external file dependencies beyond CDNs

### 2. Page Structure (scroll order)
```
[Hero Section]          — Full viewport, title, bank pills, scroll indicator
[Overview Section]      — KPI cards + summary table
[ROE Section]           — Chart + commentary card
[NIM Section]           — Chart + commentary card
[CTI Section]           — Chart + commentary card
[CET1 Section]          — Chart + commentary card
[Footer]                — Data sources, disclaimers
```

### 3. Data Embedding
Embed the bank metrics directly as a JavaScript object at the top of the script:
```javascript
const BANK_DATA = { /* contents of bank-metrics.json */ };
const COMMENTARY = { /* contents of commentary.json */ };
```

### 4. Interaction Features
- **Scroll-snap**: proximity snapping on sections
- **Intersection Observer**: Charts only animate when scrolled into view (lazy rendering)
- **Tooltips**: Follow cursor, show on hover over any chart element
- **Section fade-in**: Each section fades up (opacity 0→1, translateY 30→0) when entering viewport
- **Noise overlay**: Subtle SVG noise texture over entire page for depth

### 5. Shared Legend
A bank color legend should appear once, in the first chart section (ROE), and then be accessible as a floating reference or repeated subtly in subsequent sections.

### 6. Mobile Responsiveness
- Test at 375px width (iPhone SE)
- KPI grid: 2 columns
- Charts: full width with horizontal scroll if needed
- Commentary cards: reduced padding
- Table: horizontal scroll
- Hero title: use `clamp()` for responsive sizing

### 7. Performance
- Charts render only when visible (Intersection Observer with threshold 0.3)
- Keep a `chartBuilt` map to prevent re-rendering
- SVGs use `viewBox` for responsive scaling (no fixed dimensions)
- Minimize DOM operations during scroll

### 8. Accessibility
- All chart SVGs should have `role="img"` and `aria-label` describing the chart
- Color is not the only differentiator (bank names appear in labels)
- Tooltip content is supplementary, not essential

### 9. Footer Content
Include:
- Data source attribution with FY end dates for each bank
- "Cash basis, continuing operations" disclaimer
- "Not financial advice" disclaimer
- "Built with D3.js" credit

## Quality Checklist Before Output
- [ ] All 5 banks appear in every chart
- [ ] Bank colors match the design system exactly
- [ ] Charts animate on scroll (not on page load)
- [ ] Tooltips work on all chart elements
- [ ] Mobile layout is usable at 375px
- [ ] No JavaScript errors in console
- [ ] Commentary cards display correctly
- [ ] Summary table is complete and accurate
- [ ] Footer includes all required disclaimers
- [ ] Page scrolls smoothly between sections
