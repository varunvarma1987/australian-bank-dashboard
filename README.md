# Australian Bank Performance Dashboard

A comprehensive, interactive dashboard for comparing key financial metrics across Australia's major banks. Built with D3.js and designed to work with any fiscal year data.

## 📊 Overview

This dashboard visualizes:
- Return on Equity (ROE)
- Net Interest Margin (NIM)
- Cost-to-Income Ratio (CTI)
- CET1 Capital Ratio
- Profit (NPAT)
- Dividend Yield

## 🗂️ Project Structure

```
bank-dashboard/
├── data/
│   └── bank-metrics.json          # Source data (replace for different FY)
├── dashboard/
│   └── index.html                 # Complete dashboard (generated)
├── skills/
│   ├── 01-extract-data/           # Data extraction skill
│   ├── 02-build-charts/           # Chart generation skills
│   │   ├── overview/              # KPI cards & summary table
│   │   ├── roe/                   # ROE chart
│   │   ├── nim/                   # NIM chart
│   │   ├── cti/                   # Cost-to-Income chart
│   │   └── cet1/                  # CET1 chart
│   └── 03-assemble/               # Dashboard assembly skill
└── README.md                      # This file
```

## 🚀 Quick Start for New Fiscal Year

### Step 0: Extract Financial Data (Automated)

**Use Claude Code to automatically extract data:**

```bash
# Tell Claude to extract data from web sources
"Read skills/01-extract-data/SKILL.md and extract the latest FY26
financial data for all 5 Australian banks. Write to data/bank-metrics.json"
```

Claude will search official bank investor relations pages, extract metrics, and generate the JSON file automatically!

### Step 1: (Alternative) Manually Prepare Data

If you prefer manual preparation, replace `data/bank-metrics.json` with your fiscal year data. Follow the exact structure below:

```json
{
  "metadata": {
    "generated_at": "2026-02-08T00:00:00Z",
    "fy_label": "FY26",
    "notes": "Your notes here"
  },
  "banks": [
    {
      "code": "CBA",
      "name": "Commonwealth Bank of Australia",
      "color": "#FFD700",
      "fy_year": "FY26",
      "fy_end_date": "2026-06-30",
      "results_date": "2026-08-12",
      "source_url": "https://...",
      "metrics": {
        "npat_m": 10500,
        "roe": 13.8,
        "nim": 2.10,
        "cti": 44.5,
        "cet1": 12.5,
        "eps": 625.0,
        "dps": 500,
        "dividend_yield": 4.3
      },
      "yoy_changes": {
        "npat_pct": 2,
        "roe_bps": 30,
        "nim_bps": 2,
        "cti_bps": -100,
        "cet1_bps": 20
      },
      "notes": "Your commentary here"
    }
    // ... repeat for NAB, ANZ, WBC, MQG
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

### Step 2: Generate the Dashboard (Using Claude Code)

If using Claude Code CLI, run these commands in sequence:

```bash
# Navigate to project directory
cd bank-dashboard-project/bank-dashboard

# Step 1: Review the data file (optional - just to verify structure)
# The data is already in place at data/bank-metrics.json

# Step 2: Generate Overview KPI Cards & Table
# Tell Claude: "Read skills/02-build-charts/overview/SKILL.md and update
# dashboard/index.html with the overview section using data from
# data/bank-metrics.json"

# Step 3: Generate ROE Chart
# Tell Claude: "Read skills/02-build-charts/roe/SKILL.md and add the ROE
# chart to dashboard/index.html"

# Step 4: Generate NIM Chart
# Tell Claude: "Read skills/02-build-charts/nim/SKILL.md and add the NIM
# chart to dashboard/index.html"

# Step 5: Generate CTI Chart
# Tell Claude: "Read skills/02-build-charts/cti/SKILL.md and add the CTI
# chart to dashboard/index.html"

# Step 6: Generate CET1 Chart
# Tell Claude: "Read skills/02-build-charts/cet1/SKILL.md and add the CET1
# chart to dashboard/index.html"
```

### Step 3: View Your Dashboard

Open `dashboard/index.html` in a web browser. No server required!

## 📝 Data Field Definitions

### Required Metrics

| Field | Description | Format | Example |
|-------|-------------|--------|---------|
| `npat_m` | Net Profit After Tax (millions) | Number | 10252 |
| `roe` | Return on Equity | Percentage | 13.5 |
| `nim` | Net Interest Margin | Percentage | 2.08 |
| `cti` | Cost-to-Income Ratio | Percentage | 45.5 |
| `cet1` | CET1 Capital Ratio | Percentage | 12.3 |
| `eps` | Earnings Per Share | Cents | 613.2 |
| `dps` | Dividend Per Share | Cents | 485 |
| `dividend_yield` | Dividend Yield | Percentage | 4.2 |

### Bank Codes & Colors

Always use these exact bank codes and colors for consistency:

```javascript
CBA: #FFD700  // Gold
NAB: #E63946  // Red
ANZ: #3B82F6  // Blue
WBC: #D5002B  // Crimson
MQG: #DADADA  // Light Gray
```

### Calculating Dividend Yield

```javascript
dividend_yield = (DPS in cents / Share price at reporting date) × 100
```

Example for CBA:
- DPS: 485 cents
- Share price: ~$115
- Yield: (4.85 / 115) × 100 = 4.22%

## 🎨 Customization Options

### Updating the Hero Section

Edit the year in `dashboard/index.html`:

```html
<div class="hero-tag">Financial Year 2026 · Annual Comparison</div>
<h1>Australian Bank<br><span>Performance Dashboard</span></h1>
```

### Updating Commentary

Each chart section has a commentary card. Update the text to reflect your fiscal year insights:

```html
<div class="commentary-card">
  <h4>🏆 Your Headline Here</h4>
  <p>Your analysis and commentary here...</p>
</div>
```

### Changing Design Colors

Edit CSS variables in `dashboard/index.html`:

```css
:root {
  --bg-primary: #0a0e17;
  --bg-card: #111827;
  --accent-gold: #f59e0b;
  /* ... */
}
```

## 🔧 Skills Reference

Each skill folder contains a `SKILL.md` file with detailed specifications:

### `/skills/02-build-charts/overview/SKILL.md`
- KPI highlight cards with interactive mini bar charts
- Summary comparison table
- View toggle (KPI cards vs table)
- Bank selection interaction

### `/skills/02-build-charts/roe/SKILL.md`
- Vertical bar chart with bank colors
- Animated bars with stagger effect
- Value labels and leader indicator (👑)
- Responsive design

### `/skills/02-build-charts/nim/SKILL.md`
- Similar to ROE chart
- Custom commentary for margin analysis

### `/skills/02-build-charts/cti/SKILL.md`
- Inverted logic (lower is better)
- Different color treatment for best performer

### `/skills/02-build-charts/cet1/SKILL.md`
- Includes APRA minimum threshold line
- Surplus capital callouts

## 📋 Checklist for New Fiscal Year

- [ ] Gather financial data for all 5 banks
- [ ] Calculate dividend yields using current share prices
- [ ] Update `data/bank-metrics.json` with new data
- [ ] Update fiscal year references in HTML
- [ ] Regenerate charts using skills
- [ ] Update commentary sections with new insights
- [ ] Review rankings in the data file
- [ ] Test dashboard in browser
- [ ] Share `dashboard/index.html` (it's a single standalone file!)

## 🌐 Sharing Your Dashboard

The `dashboard/index.html` file is completely self-contained. Share it by:

1. **Email**: Attach the HTML file
2. **Cloud Storage**: Upload to Google Drive, Dropbox, etc.
3. **Web Hosting**: Deploy to GitHub Pages, Netlify, Vercel
4. **Internal Server**: Drop in any web directory

No dependencies, no build process, no server required!

## 🔍 Data Sources

Official investor relations pages:

- CBA: https://www.commbank.com.au/about-us/investors/results.html
- NAB: https://www.nab.com.au/about-us/shareholder-centre
- ANZ: https://www.anz.com.au/shareholder/centre/reporting/
- WBC: https://www.westpac.com.au/about-westpac/investor-centre/
- MQG: https://www.macquarie.com/au/en/investors.html

## 📊 Example Use Cases

1. **Annual Updates**: Run for FY26, FY27, etc.
2. **Peer Comparison**: Compare different fiscal years side-by-side
3. **Trend Analysis**: Track changes over multiple years
4. **Investment Research**: Share with colleagues for analysis
5. **Educational**: Teach financial analysis and data visualization

## 🛠️ Technical Details

- **Framework**: Vanilla JavaScript + D3.js v7
- **Styling**: CSS3 with CSS Grid and Flexbox
- **Fonts**: Google Fonts (Playfair Display, DM Sans)
- **Compatibility**: Modern browsers (Chrome, Firefox, Safari, Edge)
- **Mobile**: Fully responsive design

## 📄 License

This project is for educational and analytical purposes. Financial data sources are publicly available from bank investor relations pages.

## 🤝 Contributing

To extend or improve the dashboard:

1. Add new metrics to `data/bank-metrics.json`
2. Create new skill files in `/skills/`
3. Update chart generation logic
4. Test thoroughly with different data sets

## 📞 Support

For questions or issues:
- Review the skill files for detailed specifications
- Check data structure matches the template
- Verify all required fields are present
- Ensure bank codes and colors are consistent

---

**Built with Claude Code** • Data as of FY25 • Not financial advice
