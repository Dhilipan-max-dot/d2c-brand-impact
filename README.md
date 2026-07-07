# 📊 D2C Brand Impact Reporting — GlowGlam

![Power BI](https://img.shields.io/badge/Power%20BI-DAX%20%7C%20Power%20Query-yellow?style=flat&logo=powerbi)
![SQL](https://img.shields.io/badge/SQL-MySQL%20%7C%20SQLite-blue?style=flat&logo=mysql)
![Python](https://img.shields.io/badge/Python-pandas%20%7C%20numpy-blue?style=flat&logo=python)
![Status](https://img.shields.io/badge/Status-Complete-green?style=flat)

---

## 📌 Business Problem

GlowGlam, a D2C beauty brand, sells across three channels — its own D2C platform, DCart, and Nile marketplace. The CEO, CFO, and CMO each needed answers the existing static Excel reports couldn't provide:

- **CEO:** How is the business performing across channels and categories?
- **CFO:** What is our true gross margin after vendor costs and volume discounts? Can I model what happens if we change discount thresholds?
- **CMO:** Which campaigns are actually driving revenue? How do I attribute sales accurately across platforms?

**My Role:** Business Analyst responsible for requirements gathering from the executive transcript, gap analysis across three data sources, data architecture design, DAX measure development, and delivery of a 4-page Power BI solution.

---

## 🏗️ Solution Architecture

```
Stakeholder Requirements (CEO / CFO / CMO transcript)
        ↓
Gap Analysis — D2C + DCart + Nile data sources
        ↓
Data Model — Star Schema (8 tables)
  · Fact_Sales
  · Dim_Product · Dim_Date · Dim_AdCampaign · Dim_AdBudget
  · _Measures (DAX) · Volume_Threshold · Attribution_Pct
        ↓
Power Query — Data Cleaning & Integration
        ↓
  ┌──────────────────────────────────────┐
  │  Power BI Dashboard (4 Pages)        │
  │  · Sales Command Centre              │
  │  · Cost & Margin                     │
  │  · Marketing Performance             │
  │  · Executive Dashboard               │
  └──────────────────────────────────────┘
        ↓
What-If Parameters → CFO discount modelling + CMO attribution
```

---

## 🔍 Business Requirements Translated

| Stakeholder | Requirement | Delivered |
|-------------|-------------|-----------|
| CEO | Revenue performance by channel and category | Sales Command Centre — Revenue by Channel (bar), Revenue by Category & Channel (clustered column) |
| CFO | True margin after costs and discounts | Cost & Margin — Gross Margin %, Revenue vs Cost trend, Vendor Payment Summary table |
| CFO | Volume discount threshold modelling | What-If parameter: `Volume_Threshold` slicer — dynamically recalculates Net Payable |
| CMO | Campaign performance with conversion funnel | Marketing Performance — Impressions → Clicks → Add to Cart funnel, CTR & Conversion Rate table |
| CMO | Adjustable sales attribution across platforms | What-If parameter: `Attribution_Pct` slicer — CMO controls attribution split |
| All | Single executive summary view | Executive Dashboard — 6 KPI cards + Revenue & Margin Trend + Channel + Category |

---

## 📊 Dashboard Pages

### Page 1 — Sales Command Centre
KPI cards: **Total Revenue · Total Units · Total Orders · Avg Order Value**

- Revenue Trend by Month (line chart)
- Revenue by Channel — D2C vs DCart vs Nile (bar chart)
- Revenue by Category & Channel (clustered column)
- Product × Channel pivot table
- Month slicer for period filtering

### Page 2 — Cost & Margin
KPI cards: **Total Revenue · Total Cost · Gross Margin · Gross Margin %**

- Revenue vs Cost by Month (dual-line chart)
- Gross Margin by Category (bar chart)
- Vendor Payment Summary — full detail table with Volume Discount and Net Payable columns
- **What-If parameter:** `Volume_Threshold` — CFO adjusts discount threshold; Net Payable recalculates dynamically across all visuals

### Page 3 — Marketing Performance
KPI cards: **Total Ad Spend · Total Impressions · Total Clicks · ROAS**

- Campaign Performance funnel: Impressions → Clicks → Add to Cart
- Full campaign table: Medium · Platform · Category · CTR · Conversion Rate · Ad Spend
- Ad Spend by Category (bar chart)
- **What-If parameter:** `Attribution_Pct` — CMO adjusts sales attribution % across platforms

### Page 4 — Executive Dashboard
KPI cards: **Total Revenue · Gross Margin % · ROAS · Total Orders · Total Ad Spend · Net Payable**

- Revenue & Margin Trend (combined line chart)
- Revenue by Channel (donut)
- Revenue by Category (bar chart)
- Single-page summary designed for board/investor reporting

---

## 🧮 DAX Measures

Key measures built in the `_Measures` table:

| Measure | Logic |
|---------|-------|
| `Total Revenue` | SUM of sales across all channels |
| `Total Cost` | SUM of vendor/product costs |
| `Gross Margin` | Total Revenue − Total Cost |
| `Gross Margin %` | DIVIDE(Gross Margin, Total Revenue) |
| `Volume Discount` | Dynamic discount based on Volume_Threshold parameter |
| `Net Payable` | Total Cost − Volume Discount |
| `Total Ad Spend` | SUM across all campaigns |
| `Total Impressions` | SUM across ad platforms |
| `Total Clicks` | SUM across ad platforms |
| `CTR` | DIVIDE(Total Clicks, Total Impressions) |
| `ROAS` | DIVIDE(Total Revenue, Total Ad Spend) |
| `Conversion Rate` | DIVIDE(Total Add to Cart, Total Clicks) |

---

## 🗂️ Data Model

**8-table star schema connecting:**

```
Fact_Sales ──── Dim_Product
     │ ──────── Dim_Date
     │
Dim_AdCampaign ─ Dim_AdBudget
     │
_Measures (DAX measure table)
Volume_Threshold (What-If parameter table)
Attribution_Pct  (What-If parameter table)
```

Multi-source integration: D2C platform + DCart + Nile marketplace unified through Power Query transformations with documented field mapping and validation rules.

---

## 🗂️ Project Structure

```
d2c-brand-impact-reporting/
├── Dhilipan_Shelly_M_D2C_Phase_1.pbix   # Power BI dashboard file
└── README.md
```

---

## 🛠️ Tech Stack

| Layer | Tools |
|-------|-------|
| Requirements | Stakeholder transcript analysis, functional specification |
| Data Integration | Power Query (multi-source merge, cleaning, mapping) |
| Data Modelling | Star schema, 8-table relationships |
| Measures | DAX (12+ measures including dynamic What-If logic) |
| Visualisation | Power BI Desktop |
| Supporting Analysis | Python (pandas), SQL |

---

## 💡 Key Analytical Decisions

**Why What-If parameters instead of fixed discount rules?**
The CFO needed to model multiple discount scenarios in real time without requesting new reports each time. The `Volume_Threshold` parameter lets the CFO drag a slicer and see the impact on Net Payable instantly — replacing a 3-day manual Excel modelling cycle.

**Why a separate Executive Dashboard page?**
The CEO and investors needed a single-page summary they could present without navigating drill-downs. All four key metrics (Revenue, Margin %, ROAS, Orders) are visible above the fold with trend context beneath.

**Why a funnel chart for Marketing Performance?**
The CMO's core question was where in the purchase journey spend was being lost. A funnel — Impressions → Clicks → Add to Cart — makes drop-off points immediately visible without needing to read a table.

---

## 👤 Author

**Dhilipan Shelly M**
MBA in AI & Data Science · Data & Business Analyst

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/dhilipan-shelly-94799b231)
[![Email](https://img.shields.io/badge/Email-Contact-red?style=flat&logo=gmail)](mailto:dhilipanshelly@gmail.com)
