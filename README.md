# ☕ Portfolio Project: Sunrise Coffee Chain Performance Analytics in Power BI

**By Olaomo Favour Fiyinfoluwa**

![Sunrise Coffee Hero Image]<p align="center">
  <a href="Screenshots\Dashboard1.png">
    <img src="Screenshots\Dashboard1.png" alt="HR Analytics Project " width="100%">
  </a>
</p> *(Tip: Replace this link with a screenshot of your actual dashboard or a nice coffee-themed stock photo!)*

---

## 🌟 Introduction

The **Sunrise Coffee Chain** dataset covers a two-year trading period from **January 1, 2023, to December 31, 2024**, tracking the operations of 60 stores across various regions in the UK. Despite steady growth over the past five years, the commercial team identified potential performance divergences across different store formats—*High-Street, Retail-Park, and Transport-Hub*—and geographic regions.

This project delivers a comprehensive performance review of the 2023–2024 trading period to directly inform the 2025 site selection and expansion planning cycle. 

**The resulting Power BI dashboard is designed to:**
* Assess the effectiveness of the customer loyalty programme.
* Identify product category trends.
* Highlight which regions and store formats to prioritize for future growth.

---

## 🎯 Problem Statement

> *"Which stores are driving our business forward, and is our loyalty programme actually working?"*

Despite steady historical growth, the commercial team suspects that performance is diverging sharply across different store formats and UK regions. Furthermore, there is significant uncertainty regarding two key areas:
1. **Loyalty ROI:** Does the loyalty programme generate measurable incremental spend that outweighs its redemption costs?
2. **Revenue Mix:** How is the revenue mix across core product categories (espresso, filter, food, retail beans) shifting over time?

---

## 🏗️ Data Architecture & Modeling

  <a href="Screenshots\Schema Image.png">
    <img src="Screenshots\Schema Image.png" alt="HR Analytics Project " width="100%">
  </a>
</p> 
To ensure optimal performance and intuitive analysis, the Power BI data model utilizes a **Star Schema**, comprising three dimension tables and two fact tables:

| Table Name | Type | Description |
| :--- | :--- | :--- |
| `dim_date` | Dimension | A calendar table of 730 rows (2023–2024), featuring custom UK trading calendar classifications and bank holiday flags. |
| `dim_store` | Dimension | Contains 60 rows detailing store format, geographic region, seating capacity, monthly rent, staffing costs, and baseline loyalty adoption rates. |
| `dim_product` | Dimension | Outlines the product catalogue across 40 rows and six categories, tracking unit price, cost, and gross margin. |
| `fact_daily_sales` | Fact | Records 10,000 rows of granular daily trading metrics at the store-by-day level (transactions, footfall, loyalty activity, category revenue). |
| `fact_store_monthly_profitability`| Fact | A monthly P&L roll-up of 1,440 rows tracking total revenue, COGS, fixed operational costs, loyalty redemption costs, and net profit. |

  <a href="Screenshots\Table format.png">
    <img src="Screenshots\Table format.png" alt="HR Analytics Project " width="100%">
  </a>
</p> 

---

## 🧮 Core DAX Measures

The analytical engine relies on explicit DAX measures to dynamically calculate revenue, profitability, and operational efficiency. Here are the core formulas powering the dashboard:

  <a href="Screenshots\Screenshot 2026-10-24 130819.png">
    <img src="Screenshots\Screenshot 2026-10-24 130819.png" alt="HR Analytics Project " width="100%">
  </a>
</p> 
### 💰 Revenue & Profitability
```dax
Total_revenue = SUM(fact_daily_sales[total_revenue_gbp])

Total_monthly_revenue = SUM(fact_store_monthly_profitability[total_monthly_revenue_gbp])

Total_daily_gross_profit = SUM(fact_daily_sales[daily_gross_profit_gbp])

Total_net_profit_gbp = SUM(fact_store_monthly_profitability[net_profit_gbp])

monthly_cogs_gbp = SUM(fact_store_monthly_profitability[total_monthly_cogs_gbp])

AVG_rent = AVERAGE(fact_store_monthly_profitability[monthly_rent_gbp])
```

### 🚶 Transaction & Footfall
```dax
Total_transaction_sum = SUM(fact_daily_sales[total_transactions])

AVG_transaction_value_gbp = AVERAGE(fact_daily_sales[avg_transaction_value_gbp])

Total_footfall = SUM(fact_daily_sales[footfall])

Total_loyalty_transactions = SUM(fact_daily_sales[loyalty_transactions])
```

### 🥐 Product Category Revenue
```dax
Total_espresso_revenue = SUM(fact_daily_sales[espresso_revenue_gbp])

Total_filter_revenue = SUM(fact_daily_sales[filter_revenue_gbp])

Total_food_revenue = SUM(fact_daily_sales[food_revenue_gbp])
```

### 👥 Staffing & Operations
```dax
Total_staff_hours = SUM(fact_daily_sales[total_staff_hours])

AVG_staff_counts = AVERAGE(fact_daily_sales[staff_count])

Avg Hours per Staff = DIVIDE([Total_staff_hours], [AVG_staff_counts])
```

---

## 📈 Dashboard Visualizations & Insights

The dashboard is strategically structured to guide stakeholders from high-level executive summaries down to granular operational insights.

  <a href="Screenshots\Dashboard2.png">
    <img src="Screenshots\Dashboard2.png" alt="HR Analytics Project " width="100%">
  </a>
</p> 
### 📌 Executive KPIs
* **Primary Dashboard KPIs:** Displays the high-level business metrics driving the chain, including **Monthly Revenue (44.98M)**, **Net Profit (8.47M)**, **Net Margin (18.84%)**, Total Transactions (1M), Total Footfall (2M), and Total Staff Cost (13.89M). Each card features a month-over-month performance indicator showing positive growth.
* **Secondary Operational KPIs:** Provides a granular view of specific cost, operational, and category drivers, including average fixed costs like Rent (5.16K) and Staff Cost (12.07K), alongside specific revenue streams for Espresso (77.56K), Filter (30.44K), and Food (44.46K).

  <a href="Screenshots\Primary Kpi.png">
    <img src="Screenshots\Primary Kpi.png" alt="HR Analytics Project " width="100%">
  </a>
</p> 



### 📊 Trend & Distribution Analysis
* **Monthly Profitability Distribution:** A donut chart categorizing the 720 store-month records. The largest proportion is *“Profitable”* at **42.5%**, followed by *“Break-Even”* (23.75%) and *“Highly-Profitable”* (21.94%). *“Loss-Making”* and *“Structural-Loss”* represent a combined 11.8%.
* **Monthly Inflow Trend:** A dynamic line graph tracking metrics across the calendar year. Notably, Loyalty Revenue fluctuates with a distinct peak in July and a significant dip in November.
* **Total Revenue By Shift Pattern:** The *“Full-Day”* shift pattern accounts for the highest revenue at **4.3M**, followed by *“Split-Shift”* at 2.6M, while *“Skeleton”* shifts produce the least at 0.8M.

  <a href="Screenshots\Screenshot 2026-10-24 123526.png">
    <img src="Screenshots\Screenshot 2026-10-24 123526.png" alt="HR Analytics Project " width="100%">
  </a>
</p> 

### 🗓️ Calendar & Loyalty Behaviors
* **Day to Day Inflow:** Wednesdays and Mondays experience the highest volume of loyal customer activity, while Saturdays see the lowest.
* **Loyal Transaction by Trading Calendar:** *“Standard-Trading-Day”* dominates total transaction volumes, significantly outpacing activity during School Holidays, Christmas Periods, and Bank Holidays.
* **Total Transaction Distribution:** Non-Bank Holidays account for a **60.22%** majority share of transaction volumes.

  <a href="Screenshots\Screenshot 2026-10-24 123648.png">
    <img src="Screenshots\Screenshot 2026-10-24 123648.png" alt="HR Analytics Project " width="100%">
  </a>
</p>

### 🗺️ Granular & Geographic Insights
* **Top Products:** A beautifully balanced donut chart highlighting the four most sold products, showing an even **25% distribution** among *Banana Bread, Croissant, Mocha,* and the *Sunrise Keep Cup*.
* **Staff Counts:** Tracks average staff counts against the store’s opening year (2010–2024), featuring interactive slicers for Store Status, Region, and Location Type.
* **Store Performance Table:** A detailed matrix providing store-level metrics (Loyalty Txns, Peak Staff, Net Profit, Conversion %, Net Margin %) complete with a categorized Profitability Status.
* **Store Map Location:** A geographic map plotting global store locations sized by Gross Profit. While the heavy concentration highlights the UK core market, outlying locations across North America and Africa are also visible.

  <a href="Screenshots\Screenshot 2026-10-24 124129.png">
    <img src="Screenshots\Screenshot 2026-10-24 124129.png" alt="HR Analytics Project " width="100%">
  </a>
</p>

---

## 🔗 Explore the Dashboard

* 📂 **Medium:** [Product Demand & Inventory Analytics Repository](https://medium.com/@olaomofavour/product-demand-inventory-analytics-27497883edc3)


## 🔗 Project Links
Ready to interact with the data? Check out the live Power BI dashboard below:

* 🌐 **Interactive Dashboard:** [View Live Power BI Report](https://app.fabric.microsoft.com/view?r=eyJrIjoiNzQ1NTNkZTQtMDYwZC00MmJiLTk3ZDUtYmM0YTFiYjZhZDZkIiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9&pageName=cd9b2da33be5e9294245)



---
*Thank you for reading! If you found this analysis insightful, feel free to connect with me or leave a comment below.*