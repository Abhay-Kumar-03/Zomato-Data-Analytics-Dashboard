
# Zomato-Data-Analytics-Dashboard
<div align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/7/75/Zomato_logo.png" alt="Zomato Logo" width="180"/>

# 🍽️ Zomato Data Analytics Dashboard
### Power BI | DAX | Star Schema | Business Intelligence

[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://learn.microsoft.com/en-us/dax/)
[![Data Modeling](https://img.shields.io/badge/Star%20Schema-E23744?style=for-the-badge&logo=databricks&logoColor=white)]()
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)]()

> **An end-to-end interactive Power BI dashboard** built on Zomato's food delivery dataset — analysing ₹987M+ in sales, 150K+ orders, 17K+ users across 150K+ cities with 4 interactive report pages.

</div>

---

## 📂 Dataset & Project Files

All source datasets and the Power BI dashboard file are available on Google Drive.

<div align="center">
Show Image
</div>

How to use:

Click the Drive button above → Download the full folder
Open Zomato-Dashboard.pbix in Power BI Desktop (free to download)
If prompted, re-map the data source path to your local downloaded folder
All 4 dashboard pages will load with full interactivity ✅

---

## 🎯 Project Overview

This project presents a **multi-page interactive Power BI dashboard** designed to help Zomato's business teams make data-driven decisions across sales performance, user behaviour, geographic reach, and restaurant analytics.

| Metric | Value |
|--------|-------|
| 💰 Total Sales (Amount) | ₹987 Million |
| 📦 Total Orders | 1,50,281 |
| ⭐ Total Ratings | 1,48,000+ |
| 👥 Total Users | 17,431 |
| 🏙️ Cities Covered | 1,50,000+ |
| 📄 Dashboard Pages | 4 |

---

## ❓ Business Problem

Without a consolidated analytics layer, Zomato's teams were unable to answer critical questions:

- 📍 Which cities and restaurants are driving the most revenue?
- 📈 Are sales trending up or down year-over-year?
- 👤 What is the demographic profile of active users?
- 🥗 Which food category (Veg / Non-Veg) is most popular?
- 🏆 How do restaurant ratings correlate with order volume?
- 📉 How many customers are being gained vs. lost over time?

This dashboard **centralises all answers** in one place with real-time filtering by city, year, and order type.

---

## 📊 Dashboard Pages

### Page 1 — Index / Landing Page

> A branded splash page with a navigation button to enter the dashboard.

![Index Page]<img width="1920" height="974" alt="zomato1" src="https://github.com/user-attachments/assets/481aebbf-65e6-4fa9-a742-d19b1a8016f0" />


- Clean Zomato-branded design
- Central **"Dashboard"** navigation button
- Sets the professional visual tone for the report

---

### Page 2 — Overview

> Executive-level snapshot of overall platform performance.

![Overview Page]<img width="1920" height="976" alt="zomato3" src="https://github.com/user-attachments/assets/2602617e-83c8-4169-92d5-343adaa16f16" />


**Visuals included:**
- 🔢 KPI Cards — Amount (₹987M), Quantity (2M), Ratings (148K), Orders (150K)
- 📊 **Sales by City** horizontal bar chart with dynamic Top-N slicer (All / Top 5 / 10 / 20 / 50 / 100)
- 📈 **Sales by Year** line chart (2017–2020 trend)
- 🍱 Food category breakdown — **Non-Veg (140K orders / ₹10K rating)**, **Veg (156K / ₹12K)**, **Others (14K / 927)**
- 🔘 Toggle between **Quantity** and **Amount** view

---

### Page 3 — User Performance

> Deep dive into user demographics, acquisition, and churn.

![User Performance Page]<img width="1920" height="976" alt="zomato6" src="https://github.com/user-attachments/assets/9746e157-5370-4e23-a811-4bb0c914ac67" />

**Visuals included:**
- 👤 Active Users (78K), User Count (17K), Ratings (148K), Orders (301K)
- 📈 **Gain Customers** — Male: 1,387 | Female: 1,114 (Total: 3K gained)
- 📉 **Lost Customers** — Male: 3.5K | Female: 2.6K (Total: 6K lost)
- 📊 **Users by Age** — distribution showing peak at ages 22–26
- 🎚️ Cross-filter: clicking a city in the table filters all visuals dynamically

---

### Page 4 — City Performance

> Geographic performance analysis across all Zomato cities.

![City Performance Page]<img width="1920" height="980" alt="zomato9" src="https://github.com/user-attachments/assets/bc3de227-5cff-46ca-b9ab-aa3d71717c37" />

**Visuals included:**
- 🗺️ World map with city distribution overlay
- 📋 **City table** — Sales, Lost Users, Gain Users, Orders per city
- 📊 **Sales by City** bar chart — Tirupati, Electronic City (Bangalore) lead
- ⭐ **Rating by City** — Bikaner, Noida-1, Indirapuram top rated
- 👥 **User by City** — Bikaner, Other, Noida-1 most users
- 🔘 Toggle: Quantity / Amount view

---

## 🗃️ Data Model — Star Schema

> Industry-standard Star Schema designed for optimal query performance and clean DAX.

![Star Schema](zomato_schema.png)

```
                    ┌─────────┐
                    │  users  │
                    │ user_id │
                    └────┬────┘
                         │ 1
           ┌─────────────┼─────────────┐
     1     │             │             │ 1
    ┌───────┴──┐    ┌─────▼──────┐  ┌──┴──────┐
    │restaurant│    │   orders   │  │  menu   │
    │   id     │◄───│   r_id     │  │ menu_id │
    │   name   │  * │   user_id  │* │  r_id   │
    │   city   │    │   f_id     │  │  f_id   │
    │  rating  │    │   Value    │  │  price  │
    └──────────┘    │ order_date │  └────┬────┘
                    │   city     │       │
                    └────────────┘       │ 1
                                   ┌─────▼───┐
                                   │  food   │
                                   │  f_id   │
                                   │  item   │
                                   │veg/nveg │
                                   └─────────┘

    Helper: RankTable (No, Sort, Type) — drives dynamic Top-N filtering
    Helper: Measure_Table — stores all DAX measures (clean model design)
```

| Table | Type | Key Columns | Purpose |
|-------|------|-------------|---------|
| `orders` | ⚡ Fact | r_id, user_id, f_id | All transactions — value, date, city, type, ratings |
| `users` | 📐 Dimension | user_id | Demographics — age, gender, occupation, marital status |
| `restaurant` | 📐 Dimension | id | Restaurant info — name, city, cuisine, ratings |
| `menu` | 📐 Dimension | menu_id, r_id, f_id | Maps restaurant ↔ food, stores price |
| `food` | 📐 Dimension | f_id | Item catalog — name, veg/non-veg flag |
| `RankTable` | 🔧 Helper | No, Sort, Type | Powers dynamic Top-N slicer |
| `Measure_Table` | 📏 Measures | — | All custom DAX measures (clean separation) |

---

## 📐 DAX Measures

All measures are stored in a dedicated `Measure_Table` for clean model organisation.

### Core KPI Measures

```dax
-- Total revenue from all orders
Total Sales = SUM(orders[Value])

-- Total number of orders
Order_Count = COUNT(orders[order_date])

-- Total ratings submitted
Rating_Count = COUNT(orders[Rating_Count])

-- Unique users who placed at least one order
ActiveUser = DISTINCTCOUNT(orders[user_id])
```

### Year-over-Year Comparison

```dax
-- Get latest/selected year
CurrYear = MAX(orders[Year])

-- Sales for current year only
CurrYearSale = CALCULATE([Total Sales], orders[Year] = [CurrYear])

-- Sales for previous year
PrevYearSale = CALCULATE([Total Sales], orders[Year] = [CurrYear] - 1)

-- YoY growth percentage
SalesGrowth% = DIVIDE([CurrYearSale] - [PrevYearSale], [PrevYearSale], 0)

-- Visual indicator for growth/decline
GainLossIndicator = IF([SalesGrowth%] >= 0, "▲ Growth", "▼ Decline")
```

### Dynamic Ranking (Top-N)

```dax
-- Rank restaurants by total sales
RestaurantRank = RANKX(ALL(restaurant[name]), [Total Sales], , DESC, DENSE)

-- Rank cities by total sales
CityRank = RANKX(ALL(orders[city]), [Total Sales], , DESC, DENSE)

-- Filter to only show Top N (driven by RankTable slicer)
TopN_Filter = IF([RestaurantRank] <= SELECTEDVALUE(RankTable[No], 10), 1, 0)
```

### Dynamic Slicer & Subtitle

```dax
-- Capture selected ranking type from slicer
Column = SELECTEDVALUE(RankTable[Type], "Default")

-- Auto-generate context-aware subtitle
Dyanmic_subHeading = 
    "Showing data for: " & 
    IF(ISFILTERED(orders[city]), 
       SELECTEDVALUE(orders[city], "All Cities"), 
       "All Cities") & 
    " | " & [CurrYear]
```

---

## 💡 Key Insights

1. **🏙️ Geographic Concentration** — Tirupati and Electronic City (Bengaluru) lead in total sales; top 3 cities account for a disproportionate share of order value.

2. **📉 Sales Decline Post-2018** — Sales peaked in 2018 at ₹0.41Bn before declining to ₹0.14Bn in 2020, signalling a need to investigate retention and competitive factors.

3. **🥗 Veg Dominates in Quantity** — Vegetarian orders (156K) outnumber Non-Veg (140K) by volume, but revenue comparison varies by city.

4. **👥 User Churn > Acquisition** — Platform lost ~6K customers while gaining only ~3K — a retention red flag for the growth team.

5. **🎂 Young User Base** — Peak users fall in the 22–26 age group, making young professionals and students the primary target segment.

6. **⭐ Rating ≠ Volume** — Bikaner tops city ratings but is not the highest in order volume — suggesting price/cuisine type matters more than ratings alone.

---

## 🛠️ Tech Stack

| Tool | Usage |
|------|-------|
| **Microsoft Power BI Desktop** | Dashboard development, visualisation |
| **DAX (Data Analysis Expressions)** | Custom measures, KPIs, dynamic logic |
| **Power Query (M Language)** | Data cleaning, transformation |
| **Star Schema Design** | Data modelling for performance |
| **Excel / CSV** | Source data format |

---


---

## 🚀 How to Use

1. **Clone this repository**
   ```bash
   git clone https://github.com/your-username/zomato-powerbi-dashboard.git
   ```

2. **Open the dashboard**
   - Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/) (free)
   - Open `Zomato-Dashboard.pbix`

3. **Explore the pages**
   - Start at the **Index** page → click "Dashboard"
   - Navigate between **Overview**, **User Performance**, and **City Performance** tabs
   - Use slicers to filter by city, year, and Top-N ranking

4. **Interact with cross-filters**
   - Click any city in the City Performance table to filter all charts on that page
   - Toggle between **Quantity** and **Amount** views on Overview and City pages

---

## 📌 Resume Highlights

> Copy-paste ready bullets for your CV:

- Developed a **4-page interactive Power BI dashboard** on Zomato food delivery data, analysing ₹987M in sales across 150K+ orders and 17K+ users
- Designed a **Star Schema** data model (1 Fact + 5 Dimension tables) for optimised query performance and clean DAX calculations
- Built **14+ custom DAX measures** including `RANKX` for dynamic Top-N rankings, `CALCULATE` for YoY KPIs, `DISTINCTCOUNT` for active user tracking, and dynamic subtitle generation
- Implemented **Year-over-Year sales comparison** with conditional growth/decline indicators using DAX `IF` and `DIVIDE`
- Created **cross-filter drill-through** functionality enabling city-level deep dives across Sales, Rating, and User visuals simultaneously

---

<div align="center">

**⭐ If you found this project useful, please star the repository!**

Made with ❤️ using Power BI

</div>
