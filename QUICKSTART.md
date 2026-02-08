# Quick Start Guide - Running the Dashboard for a New Fiscal Year

This guide shows you how to generate a complete bank performance dashboard for **any fiscal year** using Claude Code.

## Prerequisites

- Claude Code CLI installed
- Bank financial data for your target fiscal year

## Step-by-Step Process

### 1️⃣ Extract Your Data (Automated with Claude Code)

**Option A: Automatic Extraction (Recommended)**

Use Claude Code to automatically extract financial data from bank reports:

```
Read skills/01-extract-data/SKILL.md and extract the latest FY26
financial data for all 5 banks (CBA, NAB, ANZ, WBC, MQG).

Search the web for their latest annual results, extract the required
metrics, and write to data/bank-metrics.json following the schema.
```

Claude will:
- Search for latest results from official sources
- Extract all required metrics (NPAT, ROE, NIM, CTI, CET1, etc.)
- Calculate dividend yields
- Generate rankings
- Write properly formatted JSON

**Option B: Manual Preparation**

If you prefer to prepare data manually:

1. Copy the template file:
   ```bash
   cp data/TEMPLATE-bank-metrics.json data/bank-metrics.json
   ```

2. Fill in the financial data for all 5 banks from their investor relations pages

3. Calculate dividend yields: (DPS in cents / Share price) × 100

4. Update rankings based on your data

### 2️⃣ Generate the Dashboard (Using Claude Code)

Open Claude Code in your project directory and run these prompts:

#### **Prompt 1: Setup**
```
I have a bank dashboard project. Please read the file at:
skills/02-build-charts/SKILL.md

This explains the overall structure. I want to generate a complete
dashboard for FY26 data.
```

#### **Prompt 2: Generate Overview Section**
```
Read skills/02-build-charts/overview/SKILL.md and generate the overview
section in dashboard/index.html using data from data/bank-metrics.json.

This should include:
- Hero section with FY26 title
- KPI highlight cards with interactive mini bar charts
- Summary comparison table
- View toggle icons
```

#### **Prompt 3: Add ROE Chart**
```
Read skills/02-build-charts/roe/SKILL.md and add the ROE chart section
to dashboard/index.html. Include the commentary card with analysis.
```

#### **Prompt 4: Add NIM Chart**
```
Read skills/02-build-charts/nim/SKILL.md and add the NIM chart section
to dashboard/index.html. Include the commentary card with analysis.
```

#### **Prompt 5: Add CTI Chart**
```
Read skills/02-build-charts/cti/SKILL.md and add the Cost-to-Income
chart section to dashboard/index.html. Include the commentary card.
```

#### **Prompt 6: Add CET1 Chart**
```
Read skills/02-build-charts/cet1/SKILL.md and add the CET1 capital chart
section to dashboard/index.html. Include APRA minimum threshold line.
```

#### **Prompt 7: Update Commentary (Optional)**
```
Update all commentary cards in dashboard/index.html to reflect the
FY26 data insights based on the metrics in data/bank-metrics.json.
```

### 3️⃣ Customize (Optional)

Update fiscal year references:
```
Find and replace "FY25" with "FY26" in dashboard/index.html
Find and replace "2025" with "2026" in relevant sections
```

### 4️⃣ View Your Dashboard

```bash
# Open in default browser
open dashboard/index.html

# OR on Windows:
start dashboard/index.html

# OR on Linux:
xdg-open dashboard/index.html
```

## Alternative: One-Shot Generation

If you prefer, you can ask Claude to generate everything at once:

```
I need to generate a complete bank performance dashboard for FY26.

Please:
1. Read data/bank-metrics.json for the data
2. Read skills/02-build-charts/SKILL.md for the design system
3. Read each sub-skill file (overview, roe, nim, cti, cet1)
4. Generate a complete dashboard/index.html with all sections

The dashboard should include:
- Hero section with FY26 title
- Overview KPI cards with interactive mini bar charts
- Summary comparison table
- ROE chart with commentary
- NIM chart with commentary
- CTI chart with commentary
- CET1 chart with APRA threshold
- Footer with data sources

Follow all design specifications from the skill files.
```

## What You Get

A single `dashboard/index.html` file containing:
- ✅ Interactive KPI cards
- ✅ Five detailed chart sections
- ✅ Bank selection functionality
- ✅ Responsive mobile design
- ✅ Professional dark theme
- ✅ Smooth animations
- ✅ No dependencies (works offline!)

## Sharing Your Dashboard

The generated `dashboard/index.html` is a **standalone file**. Share it by:

1. **Email**: Attach the HTML file directly
2. **Cloud**: Upload to Google Drive, Dropbox, OneDrive
3. **Git**: Commit and push to GitHub
4. **Hosting**: Deploy to GitHub Pages, Netlify, or Vercel

The recipient just opens the HTML file in any browser - no installation needed!

## Troubleshooting

**Charts not appearing?**
- Check browser console for errors
- Verify data/bank-metrics.json is valid JSON
- Ensure all required metrics are present

**Wrong data showing?**
- Verify metrics arrays in HTML match your data file
- Check that bank order is [CBA, NAB, ANZ, WBC, MQG]

**Colors wrong?**
- Ensure bank colors match exactly:
  - CBA: #FFD700
  - NAB: #E63946
  - ANZ: #3B82F6
  - WBC: #D5002B
  - MQG: #DADADA

## Next Steps

- Update commentary to reflect your FY insights
- Customize the design theme if needed
- Add additional metrics or charts
- Create year-over-year comparison dashboards

---

**Need Help?** Check the detailed README.md file for more information.
