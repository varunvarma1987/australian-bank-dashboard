# Skill: Overview KPI Cards & Summary Table

## Purpose
Generate the hero section, KPI highlight cards with interactive mini bar charts, and full summary comparison table that appears at the top of the dashboard.

## Data Source
`data/bank-metrics.json` → all fields

## Components to Generate

### 1. Hero Section
- Full-viewport height, centered text
- Tag line: "Financial Year [YEAR] · Annual Comparison"
- Title: "Australian Bank Performance Dashboard" (with "Performance Dashboard" in gold gradient)
- Subtitle: Brief description
- Bank pills: Row of 5 pills showing bank code + colored dot
- Scroll indicator at bottom

### 2. View Toggle Icons
**IMPORTANT:** Place toggle icons immediately below the intro text, BEFORE the KPI grid and table.

```html
<div class="view-toggle">
  <div class="view-icon active" id="kpi-view-icon" title="Key Metrics View">
    <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
      <rect x="2" y="3" width="12" height="3" rx="1.5" fill="currentColor"/>
      <rect x="2" y="8.5" width="16" height="3" rx="1.5" fill="currentColor"/>
      <rect x="2" y="14" width="8" height="3" rx="1.5" fill="currentColor"/>
    </svg>
  </div>
  <div class="view-icon" id="table-view-icon" title="Table View">
    <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
      <rect x="2" y="2" width="16" height="16" rx="2" stroke="currentColor" stroke-width="1.5" fill="none"/>
      <rect x="4" y="4" width="12" height="3" rx="1" fill="currentColor"/>
      <line x1="6.5" y1="9" x2="6.5" y2="16" stroke="currentColor" stroke-width="1.5"/>
      <line x1="10.5" y1="9" x2="10.5" y2="16" stroke="currentColor" stroke-width="1.5"/>
      <line x1="14.5" y1="9" x2="14.5" y2="16" stroke="currentColor" stroke-width="1.5"/>
      <line x1="4" y1="11.5" x2="16" y2="11.5" stroke="currentColor" stroke-width="1.5"/>
      <line x1="4" y1="14.5" x2="16" y2="14.5" stroke="currentColor" stroke-width="1.5"/>
    </svg>
  </div>
</div>
```

**Style requirements:**
- Two separate icon buttons (NOT a toggle switch)
- Icons: SVG horizontal bars icon for Key Metrics, SVG table grid icon for Table View
- Size: 44px × 44px
- Background: `--bg-card`, Border: 1px solid `--border`, Border-radius: 10px
- Icon color: `--text-muted` (inactive), dark color for active (contrasts with gold background)
- Active state: Background and border both `--accent-gold`, with gold glow shadow, icon color dark
- Hover: border changes to gold, slight translateY(-2px)
- Centered with 0.75rem gap between icons

**JavaScript behavior:**
- Clicking Key Metrics icon: show `.kpi-grid`, hide `.data-table-wrap`
- Clicking Table icon: show `.data-table-wrap`, hide `.kpi-grid`
- Add/remove `active` class accordingly
- Add `hidden` class to toggle visibility (use `display: none`)

### 3. KPI Highlight Cards with Interactive Mini Bar Charts

Generate 6 cards in a responsive grid (3×2 desktop, 1 column mobile):

| Card Title | Generic Title (when bank selected) | Subtitle | Metric Key | Logic |
|------|-----------|-----------|-----------|-------|
| Highest ROE | ROE | Cash basis, continuing operations | `roe` | Max value = best |
| Widest Margin | Margin | Group NIM including Treasury & Markets | `nim` | Max value = best |
| Best Efficiency | Efficiency | Cost to Income | `cti` | Min value = best (lower is better) |
| Strongest Capital | Capital | CET1 | `cet1` | Max value = best |
| Largest Profit | Profit | Cash NPAT ($m) | `npat` | Max value = best, format as "$X.XB" |
| Highest Dividend | Dividend | Dividend yield | `dividend_yield` | Max value = best, format as "X.X%" |

**Title Behavior:**
- When no bank is selected: Show superlative title (e.g., "Highest ROE")
- When a bank is selected by clicking a bar: Show generic title (e.g., "ROE")

#### Card Structure
Each card uses a horizontal layout with two sections:

**Left section (.kpi-left):**
1. **Title**: Dynamic title (Playfair Display, 1.1rem, bold)
   - Shows superlative title when no bank selected (e.g., "Highest ROE")
   - Shows generic title when bank selected (e.g., "ROE")
2. **Value**: Large number (Playfair Display, 2rem, bold, bank color)
3. **Bank code**: 3-letter code of the bank (0.8rem, --text-secondary)
4. **Subtitle**: Context text (0.7rem, --text-muted, e.g., "Cash basis, continuing operations")

**Right section (.kpi-right):**
- **Mini bar chart**: Horizontal bars for all 5 banks (positioned to the right, takes up 50% of card width)

```html
<div class="kpi-card">
  <div class="kpi-left">
    <div class="kpi-title">Highest ROE</div>
    <div class="kpi-value" style="color:#FFD700">13.5%</div>
    <div class="kpi-bank">CBA</div>
    <div class="kpi-subtitle">Cash basis, continuing operations</div>
  </div>
  <div class="kpi-right">
    <div class="mini-bar-chart">
      <!-- bars here -->
    </div>
  </div>
</div>
```

#### Mini Bar Chart Specification
**SIMPLIFIED DESIGN:** Show only colored bars, no text labels (no bank codes, no values)
**SORTING:** Bars are sorted by performance - best to worst (descending for ROE/NIM/CET1/NPAT/DPS, ascending for CTI)

```html
<div class="mini-bar-chart">
  <div class="mini-bar-row" data-bank-idx="0" data-metric="roe">
    <div class="mini-bar-track">
      <div class="mini-bar-fill" style="width: [calculated]%; background: #FFD700;"></div>
    </div>
  </div>
  <!-- Repeat for all 5 banks -->
</div>
```

**Card styling:**
- `.kpi-card`: flex row, gap 1rem, align-items center (gap 0.75rem on mobile)
- `.kpi-left`: flex 1, min-width 0 (takes up exactly 50% of card width on desktop; 60% on mobile with flex 1.2)
- `.kpi-right`: flex 1, min-width 0 (takes up exactly 50% of card width on desktop; 40% on mobile with flex 0.8)
- `.kpi-title`: Playfair Display, 1.1rem, bold, --text-primary
- `.kpi-value`: Playfair Display, 2rem, bold, bank color
- `.kpi-bank`: 0.8rem, --text-secondary
- `.kpi-subtitle`: 0.7rem, --text-muted, margin-top 0.5rem, white-space normal, word-wrap break-word (allows multi-line wrapping)

**Mini bar styling (simplified - no text):**
- `.mini-bar-chart`: flex column, width 100%
- `.mini-bar-row`: flex row, cursor pointer, padding 0, margin-bottom 1rem
- `.mini-bar-row:hover`: opacity 0.8
- `.mini-bar-row.selected .mini-bar-fill`: bar has glow shadow
- `.mini-bar-track`: width 100%, height 6px, background rgba(255,255,255,0.05), border-radius 3px
- `.mini-bar-fill`: height 100%, border-radius 3px, background = bank color, width calculated from 0
- Selected bar glow: `box-shadow: 0 0 10px currentColor`

**Width calculation and sorting for bars:**
Bars start from 0 (not minimum value) and are sorted by performance:
```javascript
const max = Math.max(...metricData);
// Create array and sort: descending for most metrics, ascending for CTI
const bankBars = metricData.map((value, i) => ({ idx: i, value, color: banks[i].color }));
bankBars.sort((a, b) => metricKey === 'cti' ? a.value - b.value : b.value - a.value);
const percent = (value / max) * 100;
const width = Math.max(percent, 5); // Minimum 5% for visibility
```

#### Interactive Behavior
**CRITICAL:** Implement bank selection interaction:

1. **Click handler**: Each `.mini-bar-row` is clickable
2. **State management**: Track `selectedBankIndex` (null = show best-in-class)
3. **Toggle logic**:
   - Click a bank bar → set `selectedBankIndex` to that bank
   - Click same bank again → reset to null (show best-in-class)
4. **Visual feedback**:
   - Add `selected` class to all `.mini-bar-row[data-bank-idx="${selectedBankIndex}"]`
   - Glow effect on selected bars
5. **Update ALL 6 cards**: When a bank is selected, all cards update to show that bank's values
   - Value changes to selected bank's value
   - Bank code changes to selected bank
   - Color changes to selected bank's color
   - All bars with that bank index get highlighted
6. **Re-render**: Call `renderKPICards()` after every selection change

**JavaScript structure:**
```javascript
let selectedBankIndex = null;

function renderKPICards() {
  // For each KPI definition:
  //   - Get metric data
  //   - Display title: selectedBankIndex !== null ? kpi.genericTitle : kpi.title
  //   - Display value: selectedBankIndex !== null ? data[selectedBankIndex] : best value
  //   - Display bank: selectedBankIndex !== null ? banks[selectedBankIndex].code : best bank
  //   - Display color: selectedBankIndex !== null ? banks[selectedBankIndex].color : best bank color
  //   - Create mini bar chart
  //   - Add click handlers to mini bars
  //   - Highlight selected bars if selectedBankIndex !== null
}
```

### 4. Summary Comparison Table

**Table Layout:**
| Column | Data | Format |
|--------|------|--------|
| Bank | Code + colored dot + FY End (stacked) | Bold code, muted FY below |
| Cash NPAT ($m) | `npat_m` | Formatted with commas, highlight best in gold |
| ROE | `roe` | X.X%, highlight best in gold |
| NIM | `nim` | X.XX%, highlight best in gold |
| C/I Ratio | `cti` | X.X%, highlight best in gold (LOWEST value) |
| CET1 | `cet1` | X.X%, highlight best in gold |

**CRITICAL CHANGES:**
1. **No separate FY End column** — FY End is now displayed BELOW the bank code in the Bank column
2. **Highlight ALL best metrics** — not just ROE, but NPAT, ROE, NIM, C/I Ratio, and CET1
3. **C/I Ratio**: Highlight LOWEST value (best efficiency)
4. **Max width**: 1000px (not 1200px) to avoid horizontal scroll on mobile

#### Bank Column Structure
```html
<td>
  <div class="bank-name-cell">
    <div class="bank-name-row">
      <div class="bank-dot" style="background:${b.color}"></div>${b.code}
    </div>
    <div class="bank-fy">${b.fy}</div>
  </div>
</td>
```

**Styling:**
- `.bank-name-cell`: flex column, gap 0.2rem, font-weight 600
- `.bank-name-row`: flex row, align center, gap 0.6rem
- `.bank-fy`: 0.7rem, --text-muted, font-weight 400
- `.metric-best`: font-weight 600, color --accent-gold (applied to best values)

#### Best Value Highlighting Logic
```javascript
const bestNPAT = Math.max(...metrics.npat);
const bestROE = Math.max(...metrics.roe);
const bestNIM = Math.max(...metrics.nim);
const bestCTI = Math.min(...metrics.cti); // Lower is better!
const bestCET1 = Math.max(...metrics.cet1);

// In table cell:
<td class="${metrics.roe[i] === bestROE ? 'metric-best' : ''}">${metrics.roe[i]}%</td>
```

#### Table Style
- Container max-width: 1000px (not 1200px)
- Overflow-x: auto (horizontal scroll if needed)
- `-webkit-overflow-scrolling: touch` for smooth mobile scrolling
- No outer border, subtle row separators (`--border`)
- Row hover: background `--bg-card-hover`
- Header: uppercase, letter-spacing 0.1em, 0.7rem, `--text-muted`
- Cell padding: 0.85rem 0.8rem (0.8rem horizontal, reduced from 1rem)

## Responsive Breakpoints

### Desktop (> 640px)
- KPI grid: `repeat(auto-fit, minmax(280px, 1fr))`
- Table: full width, max 1000px

### Mobile (≤ 640px)
**KPI Grid:**
- Grid: 1 column (single column layout)
- Card: flex-direction row (keep bars on right, not stacked)
- Card padding: 1rem
- Card gap: 0.75rem
- kpi-left: flex 1.2, min-width 0 (60% of card width)
- kpi-right: flex 0.8, min-width 0 (40% of card width, shrink chart container)
- mini-bar-chart: width 100%
- mini-bar-track: width 100%
- Value font-size: 1.5rem

**Table:**
- Max-width: 100%
- Font-size: 0.75rem
- Header padding: 0.6rem 0.4rem
- Cell padding: 0.7rem 0.4rem
- Header font-size: 0.65rem
- Bank dot: 6px × 6px
- `.bank-fy`: 0.65rem
- `.bank-name-cell` gap: 0.15rem

**Goal:** Avoid horizontal scrolling on mobile by using compact spacing and smaller fonts.

## Implementation Checklist

### CSS Classes to Create
- [x] `.view-toggle` — toggle icon container
- [x] `.view-icon` — individual icon button
- [x] `.view-icon.active` — active state styling
- [x] `.kpi-grid.hidden` — hide KPI grid
- [x] `.data-table-wrap.hidden` — hide table
- [x] `.kpi-card` — horizontal flex layout (left + right sections)
- [x] `.kpi-left` — left section with metric info
- [x] `.kpi-right` — right section with bar chart
- [x] `.kpi-title` — descriptive title (e.g., "Highest ROE")
- [x] `.kpi-value` — large metric value
- [x] `.kpi-bank` — bank code display
- [x] `.kpi-subtitle` — context subtitle
- [x] `.mini-bar-chart` — container for mini bars
- [x] `.mini-bar-row` — each bank's bar row
- [x] `.mini-bar-row.selected` — selected bank highlight
- [x] `.mini-bar-track` — bar background track
- [x] `.mini-bar-fill` — colored bar fill (starts from 0, no text labels)
- [x] `.bank-name-cell` — stacked bank + FY layout
- [x] `.bank-name-row` — bank code + dot row
- [x] `.bank-fy` — FY end date below bank
- [x] `.metric-best` — gold highlight for best metrics

### JavaScript Functions to Implement
- [x] View toggle event listeners (kpi-view-icon, table-view-icon)
- [x] `renderKPICards()` — dynamic card rendering with state
- [x] `createMiniBarChart(metricKey, metricData)` — generate mini bar HTML
- [x] Mini bar click handlers with selection toggle
- [x] Table generation with all best values highlighted

### Data Requirements
- [x] Banks array with `code`, `name`, `color`, `fy`
- [x] Metrics object with `roe`, `nim`, `cti`, `cet1`, `npat`, `dividend_yield`
- [x] KPI definitions array with `title`, `genericTitle`, `subtitle`, `key`, `unit`, `formatValue`, `getBest`

## Color Reference
Always use bank colors from the design system:
- CBA: `#FFD700` (Gold)
- NAB: `#E63946` (Red)
- ANZ: `#3B82F6` (Blue)
- WBC: `#D5002B` (Crimson)
- MQG: `#DADADA` (Light Gray)

## Notes
- Start with Key Metrics view active (table hidden by default)
- Selection state persists until user clicks to deselect or changes view
- All transitions should be smooth (0.2s - 0.3s ease)
- Ensure tooltip works on mini bars if desired, but click interaction is primary
