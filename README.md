# 🍕 Eastern Coast Pizza Customer Analytics

A Python and Google Colab analysis pipeline for exploring customer spending patterns, ordering times, and product performance across 350 customer records. All monetary values are processed and displayed.

---

## 📌 Project Overview

This repository contains data analysis scripts and visual disclosures based on the `eastern_coast_pizza_customers_2.csv` dataset. The analysis provides actionable business insights into peak revenue windows, top-performing pizza varieties, customer ratings, and regional market shares.

---

## 📊 Key Findings

* **Most Profitable Pizza:** **Meat Lovers** generated the highest total revenue (**₹75,602.18**).
* **Lowest Performing Pizza:** **White Pizza** yielded the lowest revenue (**₹26,197.69**) and the lowest average review score (**1.46 / 5.0**).
* **Peak Revenue Period:** **Dinner** accounted for **₹186,001.66** (over 50% of total revenue).
* **Top Revenue Segment:** **Meat Lovers ordered during Dinner** generated **₹41,830.60**.
* **Largest Regional Share:** **Salem West** represents **27.1%** of the total customer base, followed by **Fairlands (21.4%)**.

---

## 🛠️ Data Visualizations Included

1. **Customer Share by Region (`Pie Chart`):** Displays regional market distribution across Salem West, Fairlands, Omalur, Central Salem, and Mettur.
2. **Spending & Review Distributions (`Histograms`):** Visualizes the spread of average spending amounts (₹) and customer satisfaction scores.
3. **Visit Frequency vs. Average Spend (`Scatter Plot`):** Highlights customer ordering behavior categorized by pizza preference.
4. **Revenue Matrix (`Heatmap`):** Cross-tabulates overall sales revenue (₹) between Pizza Types and Ordering Times (Lunch, Dinner, Late Night).
5. **Cumulative Revenue by Product (`Bar Chart`):** Ranks all 8 pizza varieties by total financial yield.

---

## 🚀 How to Run in Google Colab

### Option 1: Direct Sidebar Upload (Recommended)

1. Open [Google Colab](https://colab.research.google.com/).
2. Click the **Folder Icon (📁)** on the left sidebar.
3. Drag and drop `eastern_coast_pizza_customers_2.csv` into the file explorer section.
4. Copy and paste the execution code below into a code cell and click **Run (▶️)**.

---

## 🐍 Python Execution Code

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset directly from sidebar
file_path = 'eastern_coast_pizza_customers_2.csv'
df = pd.read_csv(file_path)

# Data Cleaning & Feature Engineering
df.columns = df.columns.str.strip()
df['Region'] = df['Region'].astype(str).str.title()
df['TotalRevenue'] = df['AvgSpend'] * df['VisitFrequency']

# Visual Theme Setup
sns.set_theme(style="whitegrid", font_scale=1.1)

# 1. Pie Chart - Regional Share
plt.figure(figsize=(8, 6))
region_counts = df['Region'].value_counts()
plt.pie(region_counts, labels=region_counts.index, autopct='%1.1f%%', startangle=140, 
        colors=sns.color_palette("Set2"), explode=[0.03]*len(region_counts))
plt.title("Customer Share by Region", fontsize=14, fontweight='bold', pad=15)
plt.tight_layout(pad=3.0)
plt.show()

print("\n" + "-"*80 + "\n")

# 2. Histograms - Spend & Reviews
fig, axes = plt.subplots(1, 2, figsize=(14, 5.5))
sns.histplot(df['AvgSpend'], kde=True, ax=axes[0], color='skyblue')
axes[0].set_title("Distribution of Average Spend (₹)", fontsize=13, fontweight='bold', pad=12)
axes[0].set_xlabel("Average Spend (₹)", labelpad=10)
axes[0].set_ylabel("Customer Count", labelpad=10)

sns.histplot(df['Review'], kde=True, ax=axes[1], color='salmon', bins=10)
axes[1].set_title("Distribution of Review Ratings", fontsize=13, fontweight='bold', pad=12)
axes[1].set_xlabel("Review Score (1–5)", labelpad=10)
axes[1].set_ylabel("Customer Count", labelpad=10)

plt.subplots_adjust(wspace=0.35)
plt.tight_layout(pad=3.0)
plt.show()

print("\n" + "-"*80 + "\n")

# 3. Scatter Plot - Frequency vs Spend
plt.figure(figsize=(10, 6.5))
sns.scatterplot(data=df, x='VisitFrequency', y='AvgSpend', hue='PizzaType', style='PizzaType', s=85)
plt.title("Visit Frequency vs. Average Spend (₹) by Pizza Type", fontsize=14, fontweight='bold', pad=15)
plt.xlabel("Visit Frequency (Visits/Month)", labelpad=10)
plt.ylabel("Average Spend (₹)", labelpad=10)
plt.legend(bbox_to_anchor=(1.03, 1), loc='upper left', title="Pizza Type", borderaxespad=0)
plt.tight_layout(pad=3.0)
plt.show()

print("\n" + "-"*80 + "\n")

# 4. Heatmap - Revenue by Pizza & Time
pivot_revenue = df.pivot_table(index='PizzaType', columns='VisitTime', values='TotalRevenue', aggfunc='sum')
plt.figure(figsize=(10, 6.5))
sns.heatmap(pivot_revenue, annot=True, fmt=",.0f", cmap="YlGnBu", 
            cbar_kws={'label': 'Total Revenue (₹)'}, annot_kws={"size": 11})
plt.title("Revenue (₹) Heatmap: Pizza Type vs Visit Time", fontsize=14, fontweight='bold', pad=15)
plt.ylabel("Pizza Type", labelpad=10)
plt.xlabel("Visit Time", labelpad=10)
plt.tight_layout(pad=3.0)
plt.show()

print("\n" + "-"*80 + "\n")

# 5. Bar Chart - Total Revenue
pizza_rev = df.groupby('PizzaType')['TotalRevenue'].sum().sort_values(ascending=False).reset_index()
plt.figure(figsize=(10, 5.5))
sns.barplot(data=pizza_rev, x='TotalRevenue', y='PizzaType', hue='PizzaType', legend=False, palette='viridis')
plt.title("Total Revenue Generated by Pizza Type (₹)", fontsize=15, fontweight='bold', pad=15)
plt.xlabel("Total Revenue (₹)", labelpad=10)
plt.ylabel("Pizza Type", labelpad=10)
plt.tight_layout(pad=3.0)
plt.show()
