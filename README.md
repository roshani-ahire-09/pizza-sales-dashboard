# 🍕 Pizza Sales Analytics Dashboard
### Tableau · Business Intelligence · 2015 Full Year

![Tableau](https://img.shields.io/badge/Tableau-E97627?style=flat&logo=tableau&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-2ECC71?style=flat)
![Year](https://img.shields.io/badge/Data-2015-3776AB?style=flat)

---

## 📌 Project Overview

A full-year **2015 sales analytics dashboard** for a pizza restaurant, built entirely in **Tableau**.  
The dashboard gives a restaurant manager a single view to answer three questions instantly:

- *When do we sell the most?*
- *What do we sell the most?*
- *How much are we making per transaction?*

**Total Revenue: $817,860 · Total Orders: 21,350 · Avg Order Value: $38.31**

---

## 📊 Key Results at a Glance

| Metric | Value |
|--------|-------|
| Total Annual Revenue | **$817,860** |
| Total Orders | **21,350** |
| Total Pizzas Sold | **48,620** |
| Average Order Value | **$38.31** |
| Peak Day | **Friday — 8,106 orders** |
| Avg Pizzas per Order | **2.28** *(derived)* |
| Avg Revenue per Pizza | **$16.82** *(derived)* |
| Avg Daily Orders | **58/day** *(derived)* |

---

## 🔍 Top 6 Findings

| # | Finding | Data |
|---|---------|------|
| 1 | **Friday is 140x the daily average** | 8,106 orders vs 58/day average |
| 2 | **Large pizza dominates** | 38.1% of all pizzas sold |
| 3 | **XL is nearly absent** | Only 1.1% — 35x less popular than Large |
| 4 | **Classic category leads revenue** | ~$200K+ estimated from chart scale |
| 5 | **Two daily rush windows** | 12–1PM lunch · 5–7PM dinner |
| 6 | **Thu–Sat drives ~55-60% of weekly revenue** | Weekend concentration pattern |

---

## 📸 Dashboard Preview

> The dashboard PDF is included in this repository.  
> Open `Pizza_Sales_Dashboard.pdf` to view the full interactive layout.

**Dashboard contains 7 panels:**
- 4 KPI cards — Revenue, Orders, Avg Order Value, Pizzas Sold
- Monthly Sales Trend *(dual-axis: revenue + orders)*
- Hourly Revenue Chart *(11AM–8PM operating window)*
- Revenue by Category *(Classic · Supreme · Chicken · Veggie)*
- Size Distribution *(S · M · L · XL)*
- Weekly Pattern *(day-of-week revenue and order count)*

---

## 🗂️ Dataset

- **Source:** Pizza restaurant transactional data (practice dataset)
- **Period:** Full year 2015
- **Records:** 21,350 orders · 48,620 pizzas sold
- **Key fields:** `order_id`, `order_date`, `order_time`, `pizza_id`, `pizza_category`, `pizza_size`, `total_price`

---

## 🛠️ Tool

```
Tableau Desktop
├── KPI Cards         — calculated fields for Revenue, Orders, AOV, Pizzas
├── Dual-axis charts  — Revenue (bar) + Orders (line) on same chart
├── Hourly breakdown  — DATEPART('hour', order_time) calculation
├── Size distribution — pie chart with percentage labels
└── Day-of-week       — DATENAME('weekday', order_date) calculation
```

---

## 📁 Repository Structure

```
pizza-sales-dashboard/
│
├── Pizza_Sales_Dashboard.pdf    ← exported dashboard (view here)
├── README.md                    ← this file
```

---

## 🔬 Deeper Insights — Beyond the Dashboard

These numbers are **not on the dashboard** but derived from visible KPIs:

```
Avg pizzas per order  =  48,620 ÷ 21,350  =  2.28 pizzas
Avg revenue per pizza =  $817,860 ÷ 48,620  =  $16.82
Avg daily orders      =  21,350 ÷ 365  =  58 orders/day
Friday multiplier     =  8,106 ÷ 58  =  140x the daily average
```

> Friday isn't just "a busy day" — it operates at **140x** the typical daily volume.  
> That requires completely separate inventory and staffing planning.

---

## 📈 Size Distribution Analysis

| Size | Share | Insight |
|------|-------|---------|
| Large | 38.1% | Most popular — best stock availability needed |
| Medium | 31.7% | Close second |
| Small | 29.1% | Nearly equal to Medium |
| XL | 1.1% | Almost never ordered — pricing or awareness issue |

**Key question this raises:** If XL is on the menu but only 1.1% order it, is the price too high?  
Converting even 5% of Large orders to XL would meaningfully increase average order value.

---

## ⏰ Hourly Revenue Insights

Two clear peaks visible in the hourly chart:

```
Lunch rush  :  12PM – 1PM   (highest hourly revenue of the day)
Dinner rush :  5PM  – 7PM   (second peak, sustained over 2–3 hours)
Slow hours  :  11AM and 8PM (opening and closing — lowest traffic)
```

**Operational implication:** These two windows likely generate 60%+ of daily revenue  
despite being only 3 out of 9 operating hours — staff accordingly, not evenly.

---

## 📅 Weekly Pattern

| Day | Pattern |
|-----|---------|
| Friday | Peak — 8,106 orders (highest single day) |
| Thursday | High — part of the Thu–Sat rush |
| Saturday | High — weekend demand |
| Monday | Lowest — significantly below average |
| Tuesday | Low — second slowest day |

**Business opportunity:** Monday/Tuesday promotions could shift demand to slow days  
and reduce operational strain on the Thu–Sat window.

---

## 🗄️ SQL Equivalent Queries

The same insights could be extracted via SQL from the raw orders table:

```sql
-- Peak day analysis
SELECT DATENAME(weekday, order_date) AS day_name,
       COUNT(DISTINCT order_id)      AS total_orders,
       SUM(total_price)              AS total_revenue
FROM   orders
GROUP BY DATENAME(weekday, order_date)
ORDER BY total_orders DESC

-- Hourly revenue
SELECT DATEPART(hour, order_time)  AS hour,
       COUNT(DISTINCT order_id)    AS orders,
       SUM(total_price)            AS revenue
FROM   orders
GROUP BY DATEPART(hour, order_time)
ORDER BY hour

-- Size distribution
SELECT pizza_size,
       COUNT(*)                              AS quantity,
       ROUND(COUNT(*) * 100.0
             / (SELECT COUNT(*) FROM orders), 1) AS pct_share
FROM   orders
GROUP BY pizza_size
ORDER BY quantity DESC
```

---

## ⚠️ Dashboard Issues & Fixes Applied

| Issue | Fix |
|-------|-----|
| Title typo: "Peerformance" | Corrected to "Performance" |
| Two charts appeared identical | Differentiated with separate breakdowns |
| Vague recommendations | Replaced with data-backed specifics |
| No value labels on category bars | Added percentage annotations |

---


## 👤 Author

**Roshani Dadaji Ahire**  
Data Analyst — Python · SQL · Tableau  
📧 roshaniahire1@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/roshaniahire)  
---

*Portfolio project built on a practice dataset.*  
*Dashboard designed for non-technical business stakeholders.*
