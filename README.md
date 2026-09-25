# Retail Inventory Forecast Dashboard

## 📌 Project Overview

The **Retail Inventory Forecast Dashboard** is an Excel + Tableau data analytics project designed to help retail inventory planners identify which store × SKU combinations are at risk of a stockout or an overstock, and what action (reorder, transfer, or hold) to take for each.

The project follows an end-to-end workflow:

**Raw Sales Data → Data Cleaning & Validation (Excel Power Query) → Calculated Fields → Demand Forecast & Inventory Risk Logic → Interactive Dashboard (Tableau)**

## 🛒 Industry

**Retail — Multi-Store Inventory Planning**

## 💡 Business Problem

Retailers running multiple stores with overlapping SKUs often see the same product run out in one store while sitting overstocked in another. Static reorder points and manual, store-by-store judgment do not reflect changing demand, seasonality, or promotions, so inventory ends up misallocated across the network.

## 🎯 Objective

Forecast **SKU-level demand per store**, compare it against current inventory, classify risk, and recommend an action by evaluating:

* Rolling 30-day average demand
* Seasonal index
* Current inventory level
* Inventory coverage (days of forecast on hand)

## ✨ Key Features

* Interactive two-tab Tableau dashboard (Overview + Recommendation)
* 9 KPI tiles: Total SKUs, Total Stores, Total Units Sold, Net Sales, Forecast Demand, Stockout Risk, Overstock Risk, Stockout Shortfall Units, Overall Forecast Bias
* Store Inventory Risk map (geospatial, store-level)
* Demand Forecast Trend (actual vs. forecast, with cutoff marker)
* Forecast Detail table with Forecast Bias % per store × SKU
* Store × SKU Action Map (color-coded inventory coverage)
* Reorder Priority and Hold List tables
* Risk-by-category breakdown
* Top 5 Demand SKUs ranking
* 6 interactive filters: Promotion Status, Category, Region, Seasonality, Forecast Risk Status, Weather Condition

## 📊 Dataset

The project uses a **public Kaggle synthetic retail dataset containing 76,000 rows** across 18 fields.

Key fields include:

* Date, Store ID, Product ID, Category, Region
* Inventory Level, Units Sold, Units Ordered
* Price, Discount, Competitor Pricing
* Weather Condition, Seasonality, Promotion, Epidemic
* Demand, Rolling 30 Day Avg Demand, Seasonal Index

**Coverage:** 01-Jan-2022 to 30-Jan-2024 (760 days) · **5 stores** (S001–S005) · **20 SKUs** (P0001–P0020) · **5 categories** · **4 regions** · **4 weather conditions** · **4 seasons**

The dataset is synthetic and is not associated with any real retailer.

## 🧹 Data Cleaning & Validation (Excel Power Query)

Phase 1 of the workflow validates the raw dataset before any calculation is built:

1. Data-type checks across all 18 fields
2. Categorical-value checks (Category, Region, Weather Condition, Seasonality, Store ID, Product ID)
3. Binary-field checks (Promotion, Epidemic)
4. Business-rule consistency checks (Demand, Units Sold, Inventory Level, Units Ordered ≥ 0; Price and Competitor Pricing > 0; Discount 0–25; Seasonal Index < 2)

**Result:** 0 missing values, 0 exact duplicates, 0 invalid numerical values — all checks passed, so no rows were removed. The validated 76,000 × 18 dataset moved forward to Tableau unchanged.

## 🧮 Forecast Method & Risk Logic (Tableau)

**Forecast = Rolling 30 Day Avg Demand × Seasonal Index**

**Forecast Bias % = SUM(Forecast) ÷ SUM(Demand) − 1**

### Risk Classification (per store × SKU pair)

| Status | Rule (inventory vs. forecast) | Recommended Action |
|---|---|---|
| Stockout Risk | Inventory below 1 day of forecast | Reorder / Transfer In |
| Overstock Risk | Inventory above 4 days of forecast | Hold Orders / Transfer Out |
| Healthy | Everything else | No Action |

*Note: the forecast is in-sample — the 30-day average includes the current day's demand — so it is best read as a demand-monitoring signal rather than a validated out-of-sample prediction.*

## 📈 Dashboard Outputs (as of 30 Jan 2024)

* **20** Total SKUs · **5** Total Stores
* **6,750,876** Total Units Sold (Jan 2022 – Jan 2024)
* **$412,590,590** Net Sales (Jan 2022 – Jan 2024)
* **9,772** Forecast Demand
* **9 pairs** Stockout Risk · **285.0** Stockout Shortfall Units
* **28 pairs** Overstock Risk · **15,351** units on hand (hold candidates)
* **63 pairs** Healthy — no action
* **0.62%** Overall Forecast Bias
* Transfer-first insight: 5 SKUs (P0006, P0011, P0015, P0018, P0020) are red in one store and orange in another — moving stock between them covers 169 of the 285 short units, leaving 116 units needing a normal reorder

## 🛠️ Technology / Tools

* **Microsoft Excel** (Power Query) — data cleaning and validation
* **Tableau** — calculated fields, forecast and risk logic, dashboard, visual analytics
* **PowerPoint** — project presentation
* **Git & GitHub** — version control and project showcase

## 🔄 Project Workflow

```text
Raw Sales Dataset (Kaggle CSV)
      ↓
Data Cleaning & Validation (Excel Power Query)
      ↓
Calculated Fields (Tableau)
      ↓
Demand Forecast & Inventory Risk Logic (Tableau)
      ↓
Interactive Dashboard: Overview + Recommendation (Tableau)
      ↓
Presentation (PowerPoint)
      ↓
GitHub Repository
      ↓
LinkedIn Showcase
```

## 📁 Project Structure

```text
Retail-Inventory-Forecast-Dashboard/
│
├── sales_data.csv
├── sales_data.xlsx
├── Retail-Inventory-Forecast-Dashboard.mp4
├── Retail-Inventory-Forecast-Dashboard.twbx
├── Retail-Inventory-Forecast-Dashboard.pptx
├── Retail-Inventory-Forecast-Dashboard.jpg
├── Retail-Inventory-Detailed-Data-Validation-Cleaning.jpg
├── Retail-Inventory-Forecast-Dashboard(1).jpg   (Overview tab)
├── Retail-Inventory-Forecast-Dashboard(2).jpg   (Recommendation tab)
└── README.md
```

## 🎯 Business Value

This solution can help retail inventory teams:

* Reduce stockouts and the lost sales that come with them
* Reduce capital tied up in overstocked inventory
* Prioritize which store × SKU pairs need attention first
* Prefer store-to-store transfers over new purchases when possible
* Monitor inventory risk at a glance with color-coded KPIs and filters

For retail businesses, the approach can also support future enhancements such as true out-of-sample forecasting, transfer cost and lead-time optimization, and automated reorder triggers.

## 🚀 Future Enhancements

* Rebuild the forecast on a lagged (out-of-sample) rolling average and validate against actuals
* Add error metrics such as MAE and MAPE per store × SKU
* Incorporate transfer cost and lead time into the reorder/transfer recommendation
* Replace illustrative store map coordinates with real store locations
* Automate reorder-quantity calculation and alerting
* Extend the model with machine-learning-based demand forecasting

## 📌 Project Deliverables

* Working Tableau dashboard (.twbx)
* Cleaned and validated dataset (Excel, Power Query)
* Demand forecast and inventory-risk logic
* Dashboard visualizations (Overview + Recommendation)
* Project workflow / architecture diagram
* PowerPoint presentation
* GitHub repository documentation
