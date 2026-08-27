# Eastern Coast Pizza Customer Analytics

This project provides an exploratory data analysis (EDA) pipeline designed to evaluate customer purchasing habits, item revenue performance, visit patterns, and review distributions for an Eastern Coast pizza chain.

The pipeline cleans raw operational data, derives financial metrics, produces modular data visualizations, and calculates central tendency statistics across menu items.

---

## Project Context & Objectives

Understanding customer spending patterns and menu reception is essential for optimizing promotional schedules, staffing levels, and menu pricing. This repository handles end-to-end data processing for customer visit records, answering key operational questions:

- **Revenue Drivers:** Which pizza varieties generate the highest overall sales revenue?
- **Timing & Preference:** How do ordering habits change across time slots (Lunch, Afternoon, Dinner, Late Night)?
- **Customer Satisfaction:** How do customer ratings vary across individual menu offerings when evaluated by Mean, Median, and Mode?
- **Demographic Distribution:** How are customers distributed geographically across regional territories?

---

## Dataset Schema

The script expects a CSV file named `eastern_coast_pizza_customers_2.csv` containing customer transaction data. The pipeline automatically sanitizes column header formatting and standardizes string fields.

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Region` | String | Geographical region of the customer (standardized to title case). |
| `AvgSpend` | Float | Average order spend per customer visit (in ₹). |
| `VisitFrequency` | Integer | Recorded number of customer visits per month. |
| `PizzaType` | String | Specific pizza variety ordered (e.g., Pepperoni, Margherita). |
| `VisitTime` | String | Time slot of the visit (Lunch, Afternoon, Dinner, Late Night). |
| `Review` | Integer | Customer rating score ranging from 1 to 5 stars. |
| `TotalRevenue` | Float | **Derived field:** Calculated as `AvgSpend * VisitFrequency`. |

---

## Pipeline Overview

The script performs data manipulation, numerical calculations, visual output rendering, and summary reporting in a single linear workflow:

1. **Data Ingestion & Cleaning:** Reads the source file, trims whitespace from header strings, standardizes regional casing, and derives total customer revenue.
2. **Visual Explorations:** Generates 6 distinct, styled Seaborn and Matplotlib charts covering proportions, distributions, interactions, heatmaps, revenue rankings, and metric breakdowns.
3. **Statistical Aggregation:** Computes group-level summary metrics (Mean, Median, Mode) for customer ratings grouped by pizza type.
4. **Console Output:** Prints clear key performance indicators (KPIs) and tabular rating statistics.

---

## Key Findings & Metrics Summary

Based on the execution output from the primary dataset:

### Financial Performance
- **Most Profitable Pizza:** Pepperoni (₹66,497.10)
- **Lowest Revenue Pizza:** Margherita (₹35,552.51)
- **Peak Time Zone by Sales:** Dinner (₹76,370.45)
- **Top Time & Product Pair:** Pepperoni ordered during Dinner (₹30,046.00)

### Review Ratings Breakdown (1–5 Scale)

| Pizza Type | Mean Rating | Median Rating | Mode (Most Frequent) |
| :--- | :---: | :---: | :---: |
| **Margherita** | 3.53 | 4.0 | 5 |
| **BBQ Chicken** | 3.12 | 3.0 | 1 |
| **Hawaiian** | 3.04 | 3.0 | 2 |
| **Pepperoni** | 2.86 | 3.0 | 1 |
| **Veggie Supreme** | 2.79 | 3.0 | 1 |

*Note: While Pepperoni is the largest revenue contributor, Margherita leads in customer satisfaction with a modal rating of 5 and a mean score of 3.53.*

---

## Visualization Breakdown

The code produces six visualizations sequentially:

1. **Customer Share by Region:** Pie chart depicting demographic distribution across regions.
2. **Spend & Review Histograms:** Side-by-side distribution plots for average transaction value and overall rating counts.
3. **Visit Frequency vs. Average Spend:** Scatter plot displaying spend behavior categorized by pizza type.
4. **Revenue Heatmap:** Pivot matrix highlighting total sales revenue across pizza types and ordering time slots.
5. **Total Revenue Bar Chart:** Ranked horizontal bar chart detailing total earnings by pizza variety.
6. **Rating Statistics by Pizza Type:** Grouped bar chart comparing Mean, Median, and Mode rating scores for every menu item, annotated with exact decimal values.

---

## Installation & Setup

### Prerequisites
Ensure Python 3.8+ is installed on your environment along with the required analytical libraries:

```bash
pip install pandas numpy matplotlib seaborn
