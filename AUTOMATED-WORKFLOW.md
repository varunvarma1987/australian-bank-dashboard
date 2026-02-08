# Fully Automated Workflow - Zero Manual Data Entry

This dashboard can be generated **100% automatically** using Claude Code. No manual data entry required!

## Complete Automation Steps

### Step 1: Extract Financial Data (Automated)

**Claude Code Prompt:**
```
Read skills/01-extract-data/SKILL.md and extract the latest FY26
financial results for all 5 Australian banks (CBA, NAB, ANZ, WBC, MQG).

Search official investor relations pages and ASX announcements, extract
all required metrics including dividend yields, and write the complete
data/bank-metrics.json file following the schema.
```

**What Claude Does:**
- 🔍 Searches web for latest bank results
- 📊 Extracts NPAT, ROE, NIM, CTI, CET1, DPS
- 📈 Calculates dividend yields from share prices
- 🏆 Generates performance rankings
- 💾 Writes properly formatted JSON

**Time:** ~2-3 minutes

---

### Step 2: Generate Dashboard (Automated)

**Claude Code Prompt:**
```
Read skills/02-build-charts/SKILL.md and generate a complete FY26
dashboard using the data from data/bank-metrics.json.

Generate all sections:
1. Overview KPI cards (read skills/02-build-charts/overview/SKILL.md)
2. ROE chart (read skills/02-build-charts/roe/SKILL.md)
3. NIM chart (read skills/02-build-charts/nim/SKILL.md)
4. CTI chart (read skills/02-build-charts/cti/SKILL.md)
5. CET1 chart (read skills/02-build-charts/cet1/SKILL.md)

Write the complete dashboard to dashboard/index.html following all
design specifications and interactive behaviors.
```

**What Claude Does:**
- 📋 Builds interactive KPI cards with mini bar charts
- 📊 Generates all 4 detailed chart sections
- 🎨 Applies consistent design system
- 📱 Makes it fully responsive
- ✨ Adds smooth animations and interactions
- 📄 Creates single standalone HTML file

**Time:** ~3-5 minutes

---

### Step 3: View & Share

```bash
# Open in browser
open dashboard/index.html

# Share as single file
# Email, Dropbox, GitHub, or any file sharing method
```

**What You Get:**
- ✅ Complete, professional dashboard
- ✅ Accurate, verified financial data
- ✅ Interactive visualizations
- ✅ Mobile responsive design
- ✅ Zero dependencies
- ✅ Works offline

---

## Total Time: ~5-8 minutes

From zero to complete dashboard with:
- Automated data extraction from web sources
- Automated chart generation
- Automated rankings calculation
- Automated dividend yield calculation
- Professional design and interactions

## Example: FY26 → FY27 Update

When FY27 results come out, just run:

```bash
# 1. Extract new data
"Extract FY27 financial data for all 5 banks and update data/bank-metrics.json"

# 2. Regenerate dashboard
"Regenerate the complete dashboard using the new FY27 data"

# 3. Done! Open dashboard/index.html
```

## Even Faster: One-Shot Command

Combine both steps:

```
Extract the latest FY26 financial data for CBA, NAB, ANZ, WBC, and MQG
from their official results announcements. Then generate a complete
interactive dashboard with all KPI cards and chart sections.

Read skills/01-extract-data/SKILL.md for data extraction specs.
Read skills/02-build-charts/SKILL.md and all sub-skills for chart specs.

Write data to data/bank-metrics.json and dashboard to dashboard/index.html.
```

**Result:** Complete dashboard in one command!

---

## Data Sources (Automated)

Claude searches these official sources:

- **CBA**: https://www.commbank.com.au/about-us/investors/results.html
- **NAB**: https://www.nab.com.au/about-us/shareholder-centre
- **ANZ**: https://www.anz.com.au/shareholder/centre/reporting/
- **WBC**: https://www.westpac.com.au/about-westpac/investor-centre/
- **MQG**: https://www.macquarie.com/au/en/investors.html

Plus ASX announcements and financial news for cross-validation.

---

## Quality Assurance

Claude automatically:
- ✅ Cross-validates metrics from multiple sources
- ✅ Checks values against expected ranges
- ✅ Flags inconsistencies
- ✅ Uses cash basis (not statutory)
- ✅ Includes metadata and source URLs
- ✅ Calculates accurate dividend yields

---

## Advantages of Full Automation

### vs Manual Data Entry:
- ⚡ **10x faster** - minutes vs hours
- 🎯 **More accurate** - no transcription errors
- 🔄 **Repeatable** - same process every time
- 📚 **Documented** - sources tracked automatically
- 🤖 **Consistent** - follows exact schema

### vs Spreadsheet Dashboards:
- 🎨 **Better design** - professional, interactive
- 📱 **Mobile friendly** - works on any device
- 🚀 **Easier to share** - single HTML file
- 💾 **No dependencies** - no Excel/Tableau needed
- 🌐 **Web ready** - can be hosted anywhere

---

## Customization After Generation

If you want to tweak the automated result:

1. **Update commentary**: Edit the analysis text in `index.html`
2. **Change colors**: Modify CSS variables
3. **Add metrics**: Update skills and regenerate
4. **Adjust layout**: Modify responsive breakpoints

But 99% of the time, the automated output is perfect as-is!

---

## Distribution

Share the complete package:

```
bank-dashboard/
├── skills/           ← Automation instructions
├── data/             ← Example data
├── dashboard/        ← Generated dashboard
└── *.md              ← Documentation
```

Anyone with Claude Code can:
1. Run the extraction for their fiscal year
2. Generate their own dashboard
3. Share it with colleagues

**No coding required. No manual data entry. Just results.**
