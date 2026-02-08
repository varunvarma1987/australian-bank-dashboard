# Skill: Generate Financial Commentary

## Purpose
Analyse the extracted bank metrics and generate professional, analyst-style commentary for each metric section of the dashboard.

## When to Use
Run after Agent 1 has produced `data/bank-metrics.json`.

## Input
`data/bank-metrics.json`

## Output
`data/commentary.json`

## Analysis Process

### Step 1: Compute Rankings
For each metric, rank all 5 banks:
- ROE: highest is #1
- NIM: highest is #1
- CTI: lowest is #1
- CET1: highest is #1

### Step 2: Compute Peer Statistics
For each metric:
- `peer_average`: simple average of all 5 banks
- `peer_median`: median value
- `spread`: difference between #1 and #5
- `std_dev`: standard deviation (to gauge dispersion)

### Step 3: Identify Key Stories
For each metric, identify:
- **Leader**: Who's #1 and by how much over #2
- **Laggard**: Who's #5 and what explains it (check `notes` field)
- **Movers**: Any significant YoY changes (use `yoy_changes` if available)
- **Outliers**: Values that are notably different from peers (>1 std dev from mean)

### Step 4: Generate Commentary
Write 2-4 sentences per metric following this structure:
1. **Lead with the headline**: Who leads and their value
2. **Context**: Why they lead (competitive advantage, strategic decisions)
3. **Peer comparison**: How others compare, especially notable gaps
4. **Caveat/nuance**: Any important context (e.g., significant items, different business models)

## Tone & Style Guidelines
- **Voice**: Professional financial analyst — confident but not promotional
- **Length**: 80-120 words per metric commentary
- **NO**: Bullet points, exclamation marks, or subjective praise
- **YES**: Specific numbers, basis point changes, peer comparisons
- **Use phrases like**: "leads the peer group", "down Xbps from FY24", "widening the gap over", "reflecting", "driven by", "partly offset by"
- **Macquarie caveat**: Always note Macquarie's different business model when its metrics diverge significantly from the Big 4

## Commentary Card Format
Each commentary should have:
- `emoji`: A single emoji icon (🏆 for ROE, 📊 for NIM, ⚡ for CTI, 🛡️ for CET1)
- `headline`: Bold one-line summary (max 60 chars)
- `body`: The full commentary paragraph

## Output Schema

```json
{
  "generated_at": "ISO timestamp",
  "roe": {
    "emoji": "🏆",
    "headline": "CBA Dominates with 13.5% ROE",
    "body": "Commonwealth Bank continues to lead the peer group...",
    "leader": "CBA",
    "laggard": "ANZ",
    "peer_average": 10.8,
    "spread_1_to_5": 5.4
  },
  "nim": {
    "emoji": "📊",
    "headline": "CBA's Margin Premium Widens to 2.08%",
    "body": "...",
    "leader": "CBA",
    "laggard": "ANZ",
    "peer_average": 1.86,
    "spread_1_to_5": 0.53
  },
  "cti": {
    "emoji": "⚡",
    "headline": "CBA Stays Leanest at 45.5% Despite Investment Surge",
    "body": "...",
    "leader": "CBA",
    "laggard": "ANZ",
    "peer_average": 49.4,
    "spread_1_to_5": 7.7
  },
  "cet1": {
    "emoji": "🛡️",
    "headline": "All Banks Comfortably Above Regulatory Minimums",
    "body": "...",
    "leader": "MQG",
    "laggard": "NAB",
    "peer_average": 12.3,
    "spread_1_to_5": 1.1
  },
  "overall_summary": "A 2-3 sentence overall market summary for the hero section."
}
```

## Important Comparability Notes to Include
1. ANZ's reported ROE of 8.1% was distorted by $1.1bn in significant items (restructuring + ASIC settlement). Underlying ROE was materially higher.
2. Westpac's CTI of ~53% included $273m in UNITE restructuring charges.
3. Macquarie's business model (asset management, advisory, commodities trading) makes NIM and CTI comparisons with pure retail/commercial banks less meaningful.
4. CBA reports June FY, others September (NAB/ANZ/WBC), Macquarie March. Metrics are not for identical time periods.
