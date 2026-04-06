# Sales-Analysis-Dashboard
This project presents an end-to-end Sales &amp; Profit Analysis Dashboard built in Microsoft Power BI, using two years of transactional sales data  joined with customer master data. The dashboard provides actionable business intelligence across KPIs, regional performance, customer segmentation, target achievement tracking, and trend analysis 
The dashboard replicates real-world retail analytics use cases including target vs. achievement monitoring, profitability analysis, and geospatial sales distribution.

## 🎯 Problem Statement
 
Customer and transactional data for FY 2018 and FY 2019 were provided separately. The objective was to:
 
1. **Consolidate** two years of Sales & Profit data into a single unified fact table.
2. **Join** this fact table with the Customer Details master table using `Order ID` as the key.
3. **Transform** the data (discount as percentage, null row removal, etc.).
4. **Build a single-page interactive dashboard** for April 2019, consolidated across all regions and categories, with the following requirements:
 
---
 
## 📐 Dashboard Requirements & Features
 
### ✅ 1. KPI Cards
| KPI | Description |
|-----|-------------|
| **Sales Target** | Company-set target of ₹50,000 |
| **Sales Achievement** | Actual sales value for the selected period |
| **Profit** | Total profit for the selected period |
| **Average Discount** | Mean discount (displayed as percentage) |
| **Profitability** | Profit ÷ Sales × 100 (%) |
| **Total Orders** | Count of distinct orders |
| **Total Order Quantity** | Sum of all units ordered |



 

 
## **Target Achievement Status**
The company had set a sales target of ₹50,000. Based on how much was actually achieved, the dashboard automatically shows a status label like:
- ✅ Target Achieved / Exceeded
- 🎯 Close to Target (95%+)
- ⚠️ 50–70% Target Achieved
- ❌ Less than 50% Target Achieved
...and everything in between
 
**Regional Sales — Pie Chart**
Shows which region (South, East, West, Central) contributed how much to total sales.
 
**Sales & Profit Trend Lines**
Two line charts showing how sales and profit moved day by day throughout April. Useful for spotting dips or spikes.
 
**Top 5 Customers**
A bar chart showing the top 5 customers by sales, with their segment (B2B, B2C, B2G) shown as different colors.
 
**US State Map**
A geographic map showing sales spread across states, color-coded by region.
 
**Filters on the page**
You can slice the data by Year, Category, and Region directly from the dashboard — no need to go anywhere else.


---
 
## How I prepared the data
 
- Combined the 2018 and 2019 sales tables into one using **Append Queries** in Power Query
- Removed any rows with null/blank Order IDs
- Changed the Discount column to show as a proper percentage
- Joined the combined sales table with the Customer Details table using **Order ID** as the common key
- Fixed data types — dates as Date, numbers as Decimal
 
---


## DAX I used
 
```dax
-- What % of target was achieved
Sales Achievement % = DIVIDE([Total Sales], 50000, 0) * 100
 
-- Profitability
Profitability % = DIVIDE([Total Profit], [Total Sales], 0) * 100
 
-- Dynamic status label
Achievement Status =
SWITCH(
    TRUE(),
    [Sales Achievement %] >= 100, "Target Achieved",
    [Sales Achievement %] > 100,  "Target Exceeded",
    [Sales Achievement %] >= 95,  "Close to Target Achievement",
    [Sales Achievement %] >= 90,  "90-95% Target Achieved",
    [Sales Achievement %] >= 80,  "80-90% Target Achieved",
    [Sales Achievement %] >= 70,  "70-80% Target Achieved",
    [Sales Achievement %] >= 50,  "50-70% Target Achieved",
                                  "Less than 50% Target Achieved"
)
```
 
---
 
## Tools used
 
- Power BI Desktop
- Power Query for data cleaning and merging
- DAX for measures and KPIs
- Excel as the data source
 
---
 
