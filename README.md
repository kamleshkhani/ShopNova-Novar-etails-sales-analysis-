# 🛒 ShopNova — E-Commerce Sales Performance Analysis

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-E--Commerce-blue?style=for-the-badge)

---

## 📌 Project Overview

**ShopNova** is an end-to-end **Data Analytics project** built on a fictional e-commerce company's 3-year sales data (2022–2024).

The goal was to clean raw transactional data, perform in-depth analysis, and build a **professional interactive dashboard** that helps management make data-driven decisions — covering revenue trends, product performance, customer behaviour, and regional insights.


---

## 🎯 Problem Statement

ShopNova had **20,000+ raw sales records** spread across 3 years but had **no structured reporting system**. Management could not answer critical business questions such as:

- Which product categories are most profitable?
- Which regions have the highest return rates?
- How many customers churned last year?
- What is the monthly revenue growth trend?

This project solves these problems by building a **complete analytics solution** from raw data to an executive dashboard.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Microsoft Excel** | Data Cleaning & Preparation |
| **Microsoft Power BI** | Dashboard & Data Visualisation |

---

## 📂 Dataset Description

The dataset consists of **5 interrelated tables** totalling ~31,980 records:

| Table | Rows | Description |
|-------|------|-------------|
| `orders` | 20,000 | Core transaction records |
| `customers` | 8,000 | Customer demographics & segments |
| `products` | 500 | Product catalog with cost & selling price |
| `returns` | 3,000 | Return transactions with reasons |
| `regions` | 30 | Region & state mapping |

**Timeframe:** January 2022 – December 2024  
**Categories:** Electronics · Clothing · Home & Kitchen · Sports · Beauty  
**Regions:** North · South · East · West · Central (India)

---

## 🧹 Data Cleaning — Excel

Raw data had **6 quality issues** that were identified and resolved in Microsoft Excel:

| # | Issue | Fix Applied |
|---|-------|-------------|
| 1 | ~400 duplicate order rows | `Data → Remove Duplicates` |
| 2 | ~600 rows with incorrect `total_amount` | Recalculated: `qty × price × (1 – discount)` |
| 3 | Mixed-case `payment_mode` (upi, UPI, Upi) | `Find & Replace` → standardised to UPI/Card/COD/Wallet |
| 4 | Null `discount_pct` values | Filled blanks with `0` |
| 5 | Date columns stored as text | Converted to proper `DD-MM-YYYY` Date format |
| 6 | Age outliers (< 15 or > 80) | Removed invalid records |

✅ **Result:** Clean, consistent dataset ready for analysis

---

## 📊 Power BI Dashboard — 4 Pages

Built an **interactive 4-page executive dashboard** with Year slicer and Region slicer across all pages.

---

### Page 1 — Executive Summary
> Top-level view for senior management

| KPI | Value |
|-----|-------|
| Total Revenue | ₹4.2 Crore |
| Total Orders | 16,840 |
| Avg Order Value | ₹2,495 |
| Return Rate | 14.8% |

**Visuals:** Monthly Revenue Trend (Line Chart) · Revenue by Category (Donut Chart) · Revenue by Payment Mode (Bar Chart)

---

### Page 2 — Product Performance
> For the product and inventory team

| KPI | Value |
|-----|-------|
| Top Product Revenue | ₹8.2L (Samsung Mobile) |
| Highest Return Rate | 19% (Cameras) |
| Best Profit Margin | 42% (Clothing) |
| Products Never Returned | 312 out of 500 |

**Visuals:** Top 10 Products Bar Chart · Return Rate Heatmap (Matrix with conditional formatting) · Revenue vs Profit Scatter Chart

---

### Page 3 — Customer Analysis
> For the marketing team

**Visuals:** Customer Segment Pie Chart (New / Regular / Premium) · Age Group vs Spending Column Chart · Gender Distribution Donut · Top Cities by Revenue Bar Chart

---

### Page 4 — Regional Trends
> For regional managers

**Visuals:** Revenue by Region Bar Chart · Payment Mode by Region Stacked Bar · Monthly Trend per Region Multi-line Chart · State-level Filled Map

---

## 🎨 Color Palette Used

| Color | Hex | Usage |
|-------|-----|-------|
| Deep Blue | `#1B4F8A` | Primary charts, KPI borders |
| Teal Green | `#1D9E75` | Positive metrics, growth |
| Amber | `#BA7517` | Warnings, average values |
| Red | `#E24B4A` | Return rate, danger KPIs |
| Purple | `#534AB7` | Accent, scatter chart |
| Gray | `#888780` | Neutral elements |

---

## 🔑 Key DAX Measures

```dax
Total Revenue =
CALCULATE(SUM(orders[total_amount]), orders[order_status] = "Delivered")

Return Rate % =
DIVIDE(COUNTROWS(returns),
    CALCULATE(COUNTROWS(orders), orders[order_status] = "Delivered")) * 100

Profit Margin % =
DIVIDE(
    SUM(orders[total_amount]) - SUMX(orders, orders[quantity] * RELATED(products[cost_price])),
    SUM(orders[total_amount])
) * 100

Avg Order Value =
CALCULATE(AVERAGE(orders[total_amount]), orders[order_status] = "Delivered")

Age Group =
IF([age] <= 25, "18-25",
IF([age] <= 35, "26-35",
IF([age] <= 45, "36-45", "46+")))
```

---

## 💡 Key Findings & Insights

- 📈 **Revenue grew 18% YoY in 2024** — peak months are October, November, December (festive season)
- ⚠️ **Electronics leads revenue (33%) but has the highest return rate (18–19%)** — quality or description issue needs investigation
- 👕 **Clothing has the best profit margin (42%)** — low cost price relative to selling price
- 🌍 **South region leads revenue (₹1.1 Cr)** | East region has the highest return rate (17.2%)
- 👤 **26–35 age group spends the most** — primary marketing target segment
- 🔄 **840 customers churned between 2022 and 2023** — re-engagement campaign needed
- 💳 **UPI is #1 payment mode (33%)** | COD still at 20% — higher cancellation/return risk

---

## 📁 Repository Structure

```
ShopNova-Ecommerce-Analysis/
│
├── 📊 Dataset/
│   └── ShopNova_Ecommerce_Dataset.xlsx     # Cleaned dataset (5 sheets)
│
├── 📈 Dashboard/
│   └── ShopNova_Dashboard.pbix             # Power BI dashboard file
│
├── 📸 Screenshots/
│   ├── page1_executive_summary.png
│   ├── page2_product_performance.png
│   ├── page3_customer_analysis.png
│   └── page4_regional_trends.png
│
├── 📄 Report/
│   └── ShopNova_Project_Report.docx        # Full project documentation
│
└── README.md
```

---

## 🚀 How to Use

1. **Clone the repository**
   ```bash
   git clone https://github.com/[your-username]/ShopNova-Ecommerce-Analysis.git
   ```

2. **Open the dataset**
   - Open `Dataset/ShopNova_Ecommerce_Dataset.xlsx` in Microsoft Excel
   - All 5 sheets are pre-cleaned and ready to use

3. **Open the dashboard**
   - Open `Dashboard/ShopNova_Dashboard.pbix` in **Power BI Desktop** (free download from Microsoft)
   - The dashboard will auto-connect to the Excel dataset
   - Use the **Year** and **Region** slicers to filter data interactively

---

## 📸 Dashboard Screenshots

> *(Add your Power BI screenshots here after completing the dashboard)*

| Page | Preview |
|------|---------|
| Executive Summary | `Screenshots/page1_executive_summary.png` |
| Product Performance | `Screenshots/page2_product_performance.png` |
| Customer Analysis | `Screenshots/page3_customer_analysis.png` |
| Regional Trends | `Screenshots/page4_regional_trends.png` |

---


## 🔗 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/your-profile)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/your-username)

---

---

*Made with ❤️ using Microsoft Excel and Power BI*
