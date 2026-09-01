# 🛡️ Shield Insurance - Strategic Business & Growth Analysis

> A Power BI decision-support solution analyzing revenue, policy and customer concentration, sales channels, geography, and profitability to guide Shield Insurance toward more diversified, profitable growth.

[![Status](https://img.shields.io/badge/status-complete-brightgreen)]()
[![Type](https://img.shields.io/badge/type-BI%20dashboard-blue)]()
[![Industry](https://img.shields.io/badge/industry-insurance-informational)]()
[![Tool](https://img.shields.io/badge/tool-Power%20BI-yellow)]()

---

## 🎥 Presentation

📺 **Video Walkthrough:** [Watch the presentation here](https://1drv.ms/v/c/19725ec71c13534e/IQDScF_osm7BRpDS_svxM1E1AcNg1uNt3h1sW52NZ1xIKww?e=El42zI)

---

## 📖 Background & Overview

Shield Insurance operates across multiple markets, customer segments, and sales channels. As the business grows, management needs visibility into **where revenue comes from, which customers/policies/channels drive it, and whether that revenue is actually profitable** and not just where concentration and diversification risks exist.

This project transforms transactional insurance data into an interactive Power BI solution built to address the bottlenecks and answer strategic business questions.

---

## 🗂️ Data Structure Overview

The model uses a relational **semantic model** with fact tables, dimension tables, and a dedicated measures table.

### Fact Tables

| Table | Contents |
|---|---|
| `fact_premiums` | Primary transactional table — date, customer, policy, sales mode, final premium; derives customer age/age group, settlement %, estimated settlement, and profit |
| `fact_settlements` | Settlement assumptions by customer age — used to estimate settlement exposure and profitability |

### Dimension Tables

| Table | Purpose |
|---|---|
| `dim_customer` | Customer code, date of birth, city |
| `dim_date` | Date, month, week attributes |
| `dim_policies` | Policy ID, base coverage, base premium |
| `dim_age` / `dim_age_group` | Age and standardized age-group classification |

### Measures Table - `key_measures`
Important DAX measures: Total Revenue, Total Customers, Daily Revenue/Customer Generation, Revenue & Customer Split %, Expected Settlements, Profit, Profit Margin %, and month-over-month change metrics.

### Data Model


---

## 💡 3. Executive Summary

Shield Insurance generates **~₹989.25M in total revenue at a 39.06% profit margin** — a strong core business, but one that's heavily concentrated. **Delhi NCR + Mumbai drive ~64.8% of revenue**, the **top 3 policies alone generate 62.72%** of revenue from just 22.18% of customers, and **agents account for 55.67%** of sales versus 28.87% from digital. Segment quality also varies sharply: the **31–50 age group** is the profitable core (62.2% of customers, 53.8% of revenue), while the **65+ segment** brings in outsized revenue per customer but the **lowest margin (27.99%)** of any age group.

The takeaway: **the priority isn't more revenue — it's protecting the profitable core while diversifying away from concentrated geography, policies, and channels.**

---

## 📊 4. Key Business Insights

### 4.1 Strong Core, Concentrated Everywhere
₹989.25M in revenue at a 39.06% margin reflects a healthy core business — but that revenue is concentrated across time, geography, policies, and channels, which is the real strategic risk to manage.

### 4.2 Revenue Concentration Is the Central Risk
- **Geography:** Delhi NCR alone = 40.6% of revenue; **Delhi + Mumbai = 64.8%**
- **Policies:** Top 3 policies = **62.72%** of revenue from just 22.18% of customers, while the bottom 3 serve 44.69% of customers for only 11.61% of revenue
- **Channel:** Agents drive **55.67%** of revenue vs. 28.87% from digital

A shock to any one of these — one city, one policy, one channel — would hit revenue disproportionately.

### 4.3 March Is a Revenue Spike, Not a Trend
March revenue hits **~₹264M (+84.6% vs. February)**, then drops **-41.7% in April**. This looks like a renewal/policy-cycle burst rather than sustained momentum, and needs a root-cause check before being treated as growth.

### 4.4 Revenue ≠ Profitability at the Segment Level
The **31–50 group** is both the largest and most profitable segment (62.2% of customers, 53.8% of revenue, highest absolute profit). The **65+ group** generates outsized revenue per customer (21.6% of revenue from just 8.9% of customers) but carries the **lowest margin (27.99%)** — high revenue here doesn't mean high value.

### 4.5 Indore Signals a Smarter Growth Path
While Delhi NCR wins on scale, **Indore has the highest revenue per customer** — suggesting expansion should be guided by customer value, not just market size.

---

## 🎯 5. Recommendations

| # | Recommendation | Why It Matters |
|---|---|---|
| 5.1 | 🛡️ **Protect the core** | Prioritize renewals, retention, and service quality for top-performing policies and the 31–50 segment — the engine behind most of today's revenue and profit. |
| 5.2 | 🌍 **Diversify geography & policy base** | Reduce dependence on Delhi NCR/Mumbai and the top-3 policies; evaluate Indore and similar high-revenue-per-customer markets for expansion. |
| 5.3 | 🔍 **Root-cause the March spike** | Trace it through renewals → segment → channel → geography → policy type, and explore smoothing activity across the year. |
| 5.4 | ⚖️ **Balance agent and digital channels** | Enable agents with digital tools while scaling digital acquisition to reach younger customers — grow digital without cannibalizing agents. |
| 5.5 | 📉 **Fix the 65+ margin gap** | Review settlement rates and pricing for high-revenue, low-margin segments; judge them on risk-adjusted profit, not premium revenue alone. |

---

## 🛠 6. Tech Stack

| Category | Tools / Techniques |
|---|---|
| **Business Intelligence** | Microsoft Power BI — dashboards, semantic modeling, cross-filtering, KPI reporting |
| **Data Transformation** | Power Query / M — CSV ingestion, cleaning, type transformation |
| **Data Modeling** | Power BI Semantic Model — fact/dimension tables, relationships, calculated columns, dedicated measures table |
| **Analytics** | DAX — revenue & customer metrics, settlement estimation, profit & margin, MoM comparisons, age-group classification |
| **Source Data** | Structured CSVs — customers, policies, premium transactions, settlements, dates |

---

## 🏗️ 7. Dashboard Architecture

The PBIP report contains four pages:

| Page | Focus |
|---|---|
| **Home** | Executive entry point and navigation |
| **Overview** | Revenue, customers, trends, cities, policies, age groups, sales modes |
| **Sales Mode** | Agent vs. digital performance, revenue/customer contribution, monthly & geographic trends, policy performance |
| **Age Group** | Customer distribution, revenue by age group, settlement exposure, profit & margin, policy and sales-mode interaction |

Bookmarks and interactive filtering support navigation and exploration throughout.

---

## 📐 8. DAX & Analytical Logic

```DAX
total_revenue =
SUM(fact_premiums[final_premium_amt(INR)])

expected_settlements =
SUM(fact_premiums[Estimated Settlement amt])

profit =
fact_premiums[final_premium_amt(INR)]
    - fact_premiums[Estimated Settlement amt]

% profit margin =
DIVIDE([profit_margin], [total_revenue], 0)

revenue split % =
DIVIDE(
    [total_revenue],
    CALCULATE([total_revenue], ALL(fact_premiums[sales_mode])),
    0
)
```

Other core DAX functions used: `CALCULATE`, `DIVIDE`, `DATEADD`, `DATEDIFF`, `RELATED`, `RELATEDTABLE`, `SWITCH`, `HASONEVALUE`, `FORMAT`.

---

## ⚠️ 9. Caveats & Assumptions

- **Customer count** (`COUNT(fact_premiums[customer_code])`) counts customer-code *records*, not distinct customers.
- **Profit is estimated** — calculated as Final Premium minus an age-based *estimated* settlement, not audited accounting profit.
- **Settlement % is age-based**; actual outcomes may vary due to factors outside the model.
- **Concentration ≠ underperformance** — it can also reflect strong product-market fit; the risk is concentration *without* diversification.
- **March seasonality and other patterns are descriptive, not causal** — root causes need validation against operational data.

---

## 💼 10. Business Value

```
                 INSURANCE PERFORMANCE
                          │
       ┌──────────────────┼──────────────────┐
       ▼                  ▼                  ▼
    REVENUE           CUSTOMERS          PROFITABILITY
       │                  │                  │
   Policies           Age Groups        Settlement
   Cities             Sales Mode        Estimated Profit
   Trends             Geography         Margin %
       │                  │                  │
       └──────────────────┼──────────────────┘
                          ▼
                   STRATEGIC DECISIONS
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
     PROTECT           OPTIMIZE         DIVERSIFY
```

The dashboard moves Shield Insurance from descriptive reporting toward **strategic portfolio management**.

---

## 🏆 11. Strategic Takeaway

> **Shield Insurance has a strong revenue-generating core, but growth is concentrated across specific policies, geographies, channels, and customer segments.**

The priority shifts from pure revenue growth to: **Protect** the high-performing policy portfolio and 31–50 segment → **Optimize** low-value policies and low-margin segments → **Diversify** away from Delhi NCR/Mumbai and the dominant policy base → **Scale** digital and younger-customer acquisition alongside, not instead of, the agent network.

---

## 🧠 Skills Demonstrated

Business Intelligence · Power BI · Semantic Modeling · Power Query / M · DAX · Relational Data Modeling · KPI Development · Revenue & Insurance Analytics · Customer Segmentation · Geographic & Policy Portfolio Analysis · Sales Channel Analysis · Profitability & Settlement Analysis · Concentration Risk Analysis · Executive Dashboard Design

---

## 📁 Project Classification

| | |
|---|---|
| **Domain** | Insurance |
| **Primary Tool** | Microsoft Power BI |
| **Supporting Technologies** | Power Query, DAX |
| **Data Format** | Structured CSV |
| **Analysis Areas** | Revenue, Customers, Policies, Sales Channels, Geography, Age Segmentation & Profitability |

---

## 👤 Author

**[Your Name]** | [LinkedIn](#) | [Portfolio](#)
<!-- Replace # with your actual profile links -->
