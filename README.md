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
| `fact_premiums` | Primary transactional table - date, customer, policy, sales mode, final premium; derives customer age/age group, settlement %, estimated settlement, and profit |
| `fact_settlements` | Settlement assumptions by customer age - used to estimate settlement exposure and profitability |

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
<img width="1497" height="703" alt="data_model" src="https://github.com/user-attachments/assets/52e9e1e9-b3b5-4aa5-afda-624c3fea7d34" />


---

## 💡 Executive Summary

Shield Insurance generates **~₹989.25M in total revenue at a 39.06% profit margin**, a strong core business, but one that's heavily concentrated. **Delhi NCR + Mumbai drive ~64.8% of revenue**, the **top 3 policies alone generate 62.72%** of revenue from just 22.18% of customers, and **agents account for 55.67%** of sales versus 28.87% from digital. Segment quality also varies sharply: the **31-50 age group** is the profitable core (62.2% of customers, 53.8% of revenue), while the **65+ segment** brings in outsized revenue per customer but the **lowest margin (27.99%)** of any age group.

The takeaway: **the priority isn't more revenue it is protecting the profitable core while diversifying away from concentrated geography, policies, and channels.**

<img width="1726" height="970" alt="general" src="https://github.com/user-attachments/assets/c3f4de96-1c5e-4592-8859-a606015ecc2f" />

---

## 📊 Key Insights

### Strong Core
- ₹989.25M in revenue at a 39.06% margin reflects a healthy core business, but that revenue is concentrated across time, geography, policies, and channels, which is the real strategic risk to manage.

### Revenue Concentration
- **Geography:** Delhi NCR alone = 40.6% of revenue; **Delhi + Mumbai = 64.8%**
- **Policies:** Top 3 policies = **62.72%** of revenue from just 22.18% of customers, while the bottom 3 serve 44.69% of customers for only 11.61% of revenue
- **Channel:** Agents drive **55.67%** of revenue vs. 28.87% from digital

A shock to any one of these - one city, one policy, one channel would hit revenue disproportionately.

### March Spike
- March revenue hits **~₹264M (+84.6% vs. February)**, then drops **-41.7% in April**. This looks like a renewal/policy-cycle burst rather than sustained momentum, and needs a root-cause check before being treated as growth.

### Revenue ≠ Profitability at the Segment Level
- The **31–50 group** is both the largest and most profitable segment (62.2% of customers, 53.8% of revenue, highest absolute profit). The **65+ group** generates outsized revenue per customer (21.6% of revenue from just 8.9% of customers) but carries the **lowest margin (27.99%)** - high revenue here doesn't mean high value.

### Indore has Growth Potential
- While Delhi NCR wins on scale, **Indore has the highest revenue per customer**, suggesting expansion should be guided by customer value, not just market size.

---

## 🎯 Recommendations

| Recommendation | Why It Matters |
|---|---|
| **Protect the core** | Prioritize renewals, retention, and service quality for top-performing policies and the 31–50 segment which is the engine behind most of today's revenue and profit. |
| **Diversify geography & policy base** | Reduce dependence on Delhi NCR/Mumbai and the top-3 policies; evaluate Indore and similar high-revenue-per-customer markets for expansion. |
| **Root-cause the March spike** | Trace it through renewals, segment, channel, geography, policy type, and explore smoothing strategies across the year. |
| **Balance agent and digital channels** | Enable agents with digital tools while scaling digital acquisition to reach younger customers — grow digital without cannibalizing agents. |
| **Fix the 65+ margin gap** | Review settlement rates and pricing for high-revenue, low-margin segments; judge them on risk-adjusted profit, not premium revenue alone. |

---

## 🛠 Tech Stack

- Microsoft Power BI - dashboards, semantic modeling, cross-filtering, KPI reporting
- Power Query / M - CSV ingestion, cleaning, type transformation
- Power BI Semantic Model - fact/dimension tables, relationships, calculated columns, dedicated measures table
- DAX - revenue & customer metrics, settlement estimation, profit & margin, MoM comparisons, age-group classification

---

## ⚠️ Caveats & Assumptions

- **Customer count** (`COUNT(fact_premiums[customer_code])`) counts customer-code *records*, not distinct customers.
- **Profit is estimated**, calculated as Final Premium minus an age-based *estimated* settlement.
- **age-based estimated settlement** is calculated as Final Premium * Settlement %
- **Settlement % is age-based**; actual outcomes may vary due to factors outside the model.
- **March seasonality and other patterns are descriptive, not causal**, root causes need validation against operational data.

---

## 📋 Dashboard Architecture

The report contains four pages:

1. **Home** - Executive entry point and navigation

<img width="1729" height="970" alt="home" src="https://github.com/user-attachments/assets/eb693876-d92a-41c1-bbdd-680fd553aa41" />

2. **Overview** - Revenue, customers, trends, cities, policies, age groups, sales modes

<img width="1726" height="970" alt="general" src="https://github.com/user-attachments/assets/2330b1cc-567b-4eec-832c-610cf4c702b5" />

3. **Sales Mode** - Agent vs. digital performance, revenue/customer contribution, monthly & geographic trends, policy performance

<img width="1726" height="970" alt="sales_mode" src="https://github.com/user-attachments/assets/d57b8f3d-f59d-4f8d-ae81-7cc13afd0be5" />

4. **Age Group** - Customer distribution, revenue by age group, settlement exposure, profit & margin, policy and sales-mode interaction

<img width="1728" height="973" alt="age_group" src="https://github.com/user-attachments/assets/8f01aa7c-9ce3-45f0-806c-1bd0699a9f12" />

---








