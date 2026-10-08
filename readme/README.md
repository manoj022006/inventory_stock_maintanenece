# Inventory & Stock Dashboard

An end-to-end Power BI project that turns raw inventory, sales, and purchase data into an interactive dashboard for tracking stock health, supplier performance, and reorder priorities.

---

## Project Overview

This project analyses the inventory operations of a multi-category retail/wholesale business. It brings together product, supplier, sales, purchase, and stock data into one clean data model and presents the results across three report pages:

- **Inventory and Stock Analytical Dashboard**: the main overview of stock, sales, purchases, and turnover
- **Supplier Analysis**: purchase value and units by supplier
- **Inventory Details**: a drill-down table with stock status, cost, and sales by product

The report covers the period **01-07-2026 to 19-08-2026**.

---

## Business Problem

Inventory is one of the biggest sources of tied-up capital in any trading business. Without a clear view of what is selling, what is running out, and what is being over-purchased, businesses face:

- **Stock-outs** on fast-moving products, which means lost sales
- **Overstocking** of slow-moving products, which means blocked cash and storage costs
- **No visibility** into which suppliers contribute most to purchase spend
- **Manual, reactive reordering** instead of data-driven replenishment

---

## Objectives

- Monitor **current stock, stock value, units sold, and purchase value** in one view
- Identify **low-stock products** that have fallen below their reorder level
- Measure **stock turnover** to judge how efficiently inventory is converting to sales
- Compare **sales value vs. purchase value** month by month
- Analyse **supplier performance** by purchase value and units purchased
- Build a **normalized data model** that supports accurate, flexible filtering by date, category, and supplier

---

## Dataset

The data is organised into six related tables:

| Table | Description | Key Fields |
|---|---|---|
| **Products** | Product master data | ProductID, ProductName, Category, SupplierID, UnitCost, SellingPrice, ReorderLevel |
| **Suppliers** | Supplier master data | SupplierID, SupplierName, ContactPerson, City |
| **Sales** | Sales transactions | SaleID, Date, ProductID, Quantity, SellingPrice |
| **Purchases** | Purchase transactions | PurchaseID, Date, ProductID, SupplierID, Quantity, UnitCost |
| **Inventory** | Current stock position | ProductID, CurrentStock, Stock Status |
| **Date** | Calendar table | Date, Day, DayName, DayType, Month, MonthName, Quarter, WeekNumber, Year |

**Scale:** 50 suppliers, 10 product categories, and about 2,900 units in stock.

---

## Data Model

The model follows a **star-schema style design** with normalized dimension and fact tables.

- **Dimension tables:** Products, Suppliers, Date
- **Fact tables:** Sales, Purchases, Inventory
- **Relationships:**
  - Suppliers → Products (one-to-many)
  - Products → Sales (one-to-many)
  - Products → Purchases (one-to-many)
  - Products → Inventory
  - Date → Sales and Date → Purchases (one-to-many)
  - Suppliers → Purchases (one-to-many, inactive)

Separating master data (Products, Suppliers) from transactions (Sales, Purchases) removes redundancy and keeps every figure traceable to a single source.

---

## Tools Used

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Data modelling, DAX, and report design |
| **DAX** | Measures, calculated columns, and conditional logic |
| **Power Query** | Data loading and transformation |
| **Excel / CSV** | Source data |

---

## KPIs

| KPI | Value | What it tells us |
|---|---|---|
| **Current Stock** | ~3K units | Total units on hand |
| **Stock Value** | ₹827.37K | Capital held in inventory |
| **Units Sold** | 371 | Sales volume in the period |
| **Purchase Value** | ₹760.95K | Total spend on purchases |
| **Stock Turnover** | 0.14 | How quickly stock is converting to sales |
| **Low Stock Items** | 12 | Products below their reorder level |
| **Suppliers Count** | 50 | Active supplier base |
| **Purchase Units** | ~2K | Total units purchased |

---

## Dashboard Features

- **KPI cards** for stock, value, sales, purchases, turnover, and low-stock count
- **Stock by Category**: bar chart of current stock across categories
- **Top Selling Products**: top 10 products by units sold
- **Purchase Trend**: monthly line chart of purchase value
- **Sales vs. Purchase Value**: monthly clustered column comparison
- **Low Stock Table**: products with current stock vs. reorder level, highlighted in red
- **Supplier Analysis page**: purchase value and units purchased by supplier
- **Inventory Details page**: product-level table with category, supplier, stock status, unit cost, sales value, and units sold
- **Conditional formatting**: Healthy (green) and Low Stock (red) status
- **Low Stock Alert** card for quick attention
- **Slicers** for Date, Category, Supplier, and Stock Status

### DAX examples

```DAX
Stock Status =
IF ( Inventory[CurrentStock] < RELATED ( Products[ReorderLevel] ), "Low Stock", "Healthy" )

Stock Turnover =
DIVIDE ( [Units Sold], [Current Stock] )

Low Stock Items =
CALCULATE ( COUNTROWS ( Inventory ), Inventory[Stock Status] = "Low Stock" )
```

> Replace these with the exact measures from your report if they differ.

---

## Business Insights

1. **Low stock turnover (0.14):** Purchase value (₹760.95K) is far higher than sales value (about ₹1.63 lakh) for the period, which points to **overstocking and capital tied up in inventory**.
2. **Purchases are slowing:** Monthly purchase value dropped from roughly ₹0.47M in July to ₹0.29M in August (August covers data only up to the 19th, so part of this drop is a shorter period).
3. **Best sellers are at risk:** Several top-selling products, including **Badminton Racket, Sugar 5kg, Glass Tumbler Set, and Resistance Band**, are also on the **low stock list**. These should be reordered first.
4. **Critical shortages:** Sugar 5kg (8 units vs. reorder level 40) and Shoe Rack (1 unit vs. reorder level 5) are the most severe gaps.
5. **Stock is concentrated:** Stationery, Cleaning Supplies, and Groceries hold the highest stock levels, which makes them the first categories to review for overstock.
6. **Supplier concentration:** **Malar Wholesale** has the highest purchase value, while **Cauvery Agencies** supplies the most units. This suggests very different cost-per-unit profiles and a good starting point for price negotiation.
7. **Top seller:** Herbal Shampoo 340ml leads unit sales, followed by Lunch Box Set and Basmati Rice 5kg.

---

## Skills Demonstrated

- **KPI design:** choosing metrics that reflect real business health (turnover, low-stock count, purchase vs. sales value)
- **DAX:** writing measures, calculated columns, and conditional logic
- **Data modelling and normalization:** building related dimension and fact tables with the right relationships
- **Data visualization:** selecting suitable charts, KPI cards, and conditional formatting to tell a clear story
- **Business analysis:** linking inventory data to cash flow, supplier performance, and replenishment decisions
- **Interactivity:** slicers and drill-down tables for self-service exploration
- **Data storytelling:** turning raw numbers into actionable insights

---

## How to Use

1. Download the `.pbix` file from this repository.
2. Open it in **Power BI Desktop**.
3. Use the slicers (Date, Category, Supplier, Stock Status) to explore the data.

---

## Author

**Your Name**
[LinkedIn](https://www.linkedin.com/manoj2006bigdata ) | [GitHub](https://github.com/manoj022006)
