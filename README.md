# 🛍️ Customer Shopping Behavior Analysis

> **7,900+ Transactions | 20 SQL Queries | End-to-End Data Analysis**

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![MySQL](https://img.shields.io/badge/MySQL-Database-orange?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi&logoColor=white)](https://powerbi.microsoft.com/)
[![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-green?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-lightgrey)](LICENSE)

---

## 🌟 Situation

Retail businesses generate thousands of transactions daily, yet many struggle to translate raw sales data into actionable strategy. Without structured analysis, critical questions go unanswered — which customer segments drive the most revenue? Do discounts actually improve satisfaction? Are loyal subscribers worth the programme investment?

This project began with a real-world e-commerce dataset of **7,900+ customer transactions** covering demographics, product categories, purchase amounts, shipping preferences, discount usage, subscription status, and review ratings. The data arrived in a raw, inconsistent state: missing review ratings, non-numeric frequency fields, redundant columns, and unstandardised column naming — all of which would corrupt any downstream analysis without deliberate cleaning.

The challenge was to build a complete, production-quality analytics pipeline: from messy CSV to a clean relational database, through 20 SQL business queries, to a Power BI executive dashboard that non-technical stakeholders could act on immediately.



Live Dashboard link:- https://app.powerbi.com/view?r=eyJrIjoiOTY0NjJkMmEtMzlmZC00MDNkLTkyZTYtOWM3OTA3MzllOThhIiwidCI6IjVjZTE4MWM3LTA1NTktNDUzYS1hNGJjLWIwNDMxN2RkMzIzZiJ9


![image alt](https://github.com/ParthPatilAnalyst/Customer_Behavior_Analysis-Data_Analysis_Project-/blob/a56f5b969694bb3e7bfc036391cfd302af03e78a/Screenshot%202025-11-11%20231115.png)
![image alt](https://github.com/ParthPatilAnalyst/Customer_Behavior_Analysis-Data_Analysis_Project-/blob/a56f5b969694bb3e7bfc036391cfd302af03e78a/Screenshot%202025-11-11%20231151.png)
![image alt](https://github.com/ParthPatilAnalyst/Customer_Behavior_Analysis-Data_Analysis_Project-/blob/a56f5b969694bb3e7bfc036391cfd302af03e78a/Screenshot%202025-11-11%20231223.png)
---

## 🎯 Task

The project was scoped around five core business objectives:

1. **Revenue profiling** — Identify which demographics, age groups, locations, and seasons generate the most revenue.
2. **Discount & pricing impact** — Determine whether discounts drive higher spend and whether they affect review ratings positively or negatively.
3. **Loyalty & subscription analysis** — Quantify the spend and engagement difference between subscribers, loyal, returning, and new customers.
4. **Product & category performance** — Surface the top-rated products, best-selling items per category, and highest-discount products.
5. **Operational insights** — Compare shipping types by spend and rating; identify preferred payment methods; analyse colour/size combinations by sales volume.

Deliverables: a cleaned dataset exported to MySQL, 20 structured SQL queries covering the above objectives, and an interactive Power BI dashboard with KPIs for executive review.

---

## ⚙️ Action

### 1. Data Cleaning & Feature Engineering (Python)

A structured preprocessing pipeline was applied before any analysis:

| Step | Action |
|---|---|
| **Missing values** | Imputed missing `Review Rating` using **category-wise median** — preserving per-segment distribution rather than a blunt global mean |
| **Column standardisation** | Lowercased and snake_cased all column names; renamed `purchase_amount_(usd)` → `purchase_amount` |
| **Age segmentation** | Created `age_group` using `pd.qcut` into four equal-frequency bands: *Young Adults, Adults, Middle Age, Senior* |
| **Frequency mapping** | Converted text-based purchase frequency (`Weekly`, `Fortnightly`, `Monthly`, etc.) into a numeric `purchase_frequency_days` column |
| **Redundant column removal** | Confirmed `discount_applied` and `promo_code_used` were 100% identical; dropped `promo_code_used` |
| **Database export** | Loaded the clean DataFrame into MySQL via SQLAlchemy (`mysql+pymysql`) for structured querying |

### 2. SQL Analysis (20 Queries — MySQL)

Queries were written across four analytical tiers:

**Revenue & Demographics**
- Total revenue by gender
- Revenue contribution by age group
- Revenue by location (top 5)
- Revenue by season

**Discount & Pricing**
- Customers who used discounts yet still exceeded average spend (CTE)
- Top 5 products by discount usage percentage
- Review rating comparison: discount users vs. non-discount users
- Average purchase amount by gender × category

**Loyalty & Subscription**
- Customer segmentation: New / Returning / Loyal (by previous purchases, using CTE + CASE)
- Subscriber vs. non-subscriber spend and count comparison
- Repeat buyer likelihood to subscribe (previous purchases > 5)
- Average purchase frequency (days) per customer segment

**Product & Operations**
- Top 5 products by average review rating
- Top 3 products per category (window function: `ROW_NUMBER OVER PARTITION BY`)
- Average purchase amount: Standard vs. Express shipping
- Review rating by shipping type
- Most used payment methods
- Best-selling colour × size combinations (top 10)
- Average review rating by category
- Average purchase amount by age group

### 3. Power BI Dashboard (`customer_behavior_analysis.pbix`)

An interactive executive dashboard was built with:

- **KPI cards** — Total revenue, average purchase amount, total customers, average review rating
- **Loyalty segment breakdown** — New / Returning / Loyal customer counts and revenue share
- **Top products & categories** — Revenue and rating rankings with slicer interactivity
- **Demographic filters** — Gender, age group, location, and season slicers
- **Discount impact panel** — Side-by-side comparison of discounted vs. non-discounted spend and ratings
- **Subscription performance** — Revenue and customer count split by subscription status

### 4. Tools & Stack

```
Python        pandas · numpy · matplotlib · seaborn · SQLAlchemy
MySQL         20 structured business queries
Power BI      Interactive KPI dashboard (.pbix)
Jupyter       Reproducible cleaning + EDA notebook
```

---

## 📊 Result

### Key Findings

| # | Finding | Recommendation |
|---|---|---|
| 1 | **Male and female customers** contribute nearly equal revenue — no dominant segment | Target both equally; personalise by category preference, not gender |
| 2 | **Loyal customers** (11+ previous purchases) generate disproportionately high revenue vs. their count | Invest in loyalty programme retention — the LTV gap is material |
| 3 | **Subscribed customers** spend more on average and account for a larger revenue share | Subscription conversion campaigns have a measurable ROI |
| 4 | **Discount users who still exceed average spend** represent a high-value segment | Identify and nurture this cohort — they respond to offers without needing heavy incentivisation |
| 5 | **Review ratings are marginally lower for discount users** | Discounts may attract lower-intent buyers; consider targeted rather than blanket discounting |
| 6 | **Fall season** drives the highest total revenue | Concentrate promotional budgets and inventory planning around Q3–Q4 |
| 7 | **Standard and Express shipping** show similar average purchase amounts | Shipping speed is not a spend differentiator — compete on other value drivers |
| 8 | **Top 3 products per category** account for a concentrated share of purchases | Apply a long-tail rationalisation strategy; double down on proven performers |

### Strongest Predictors of High Customer Spend

```
1. Subscription status   2. Loyalty tier (previous purchases)   3. Discount usage pattern   4. Age group
```

### Dashboard Impact

The Power BI dashboard reduced time-to-insight for business stakeholders from hours of manual reporting to **real-time, slicer-driven exploration** across demographics, seasons, and product categories — with KPIs updating dynamically on every filter selection.

---

## 📁 Repository Structure

```
├── Customer_shoping_behavior_analysis.ipynb          # Cleaning, feature engineering & DB export
├── Sql_data_analysis_customer_behavior_analysis.sql  # 20 business SQL queries
├── customer_behavior_analysis.pbix                   # Power BI executive dashboard
└── README.md                                         # This file
```

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn sqlalchemy pymysql jupyter
```

### Run the Notebook

```bash
git clone https://github.com/your-username/customer-shopping-behavior.git
cd customer-shopping-behavior
jupyter notebook Customer_shoping_behavior_analysis.ipynb
```

> **Note:** Update the CSV path in Cell 2 and your MySQL credentials in the database export cell before running.

### Run the SQL Queries

Import the cleaned table into MySQL, then open and run `Sql_data_analysis_customer_behavior_analysis.sql` in MySQL Workbench or any compatible client.

### Open the Power BI Dashboard

Open `customer_behavior_analysis.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) and refresh the data source connection if prompted.

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
