
---

# Data Warehousing & Business Intelligence –
## 🧾 Overview

This project showcases a complete **Data Warehousing (DW)** and **Business Intelligence (BI)** lifecycle applied to the Olist e-commerce dataset. From setting up a star schema, building a DW cube, and using BI tools like Power BI and Excel, the project aims to uncover insights about sales, payments, customer types, and delivery performance across Brazil.

---

## 1️⃣ Data Warehousing – ETL & Snowflake Schema Design

### 💽 Data Source

* **Olist Dataset** (CSV files or SQL tables)

  * Orders, Customers, Products, Payments, Reviews, Geolocation

### 🏗️ Star Schema Components

* **Fact Table**: `FactOrder`

  * Measures: Sales (PaymentValue), Delivery Delay, Installments, Order Count
  * Keys: DateKey, CustomerSK, ProductSK, PaymentType

* **Dimension Tables**:

  * `DimDate` – Full date hierarchy
  * `DimCustomer`
  * `DimProduct`
  * `DimGeolocation` – State, city, ZIP code
  * `DimCategory`
  * `DimPayment`

### 🧹 ETL Steps (Using SQL Server & Power Query)

* Clean nulls and inconsistent entries (e.g., blank `CategoryName`)
* Transform dates into standard formats
* Generate surrogate keys
* Create calculated columns:

  * `OrderMonthOnly` (e.g., `"Jul"`)
  * `CustomerFirstPurchaseMonth`
  * `CustomerType` (`New` or `Repeat`)
* Join Fact and Dimension tables with proper foreign keys

---

## 2️⃣ OLAP Cube Creation

### 🧊 DW Cube Setup (SSAS)

* Cube created with **SQL Server Analysis Services (SSAS)**
*A Multidimensional OLAP (MOLAP) cube was created using SQL Server Analysis Services (SSAS) to enable fast, analytical querying on top of the star schema model.

✅ Cube Structure
Cube Name: OlistSalesCube

Data Source: SQL Server Data Warehouse

Storage Mode: Multidimensional (MOLAP)
* Measures:

  * `Total Sales (SUM)`
  * `Avg Delivery Days (AVG)`
  * `Total Installments (SUM)`
  * `Order Count`
* Dimensions:

  * `Date` Hierarchy (Year → Month)
  * `State`, `Payment Type`, `CategoryName`

### Drill Actions

* Enabled **Drillthrough** for order-level details
* Configured **Drill Down** and **Roll Up** in hierarchies

---

## 3️⃣ Power BI Dashboard

### 🎨 Key Visuals Created

| Visual Type       | Title                                                         |
| ----------------- | ------------------------------------------------------------- |
| Card              | Total Sales, Avg Delivery Days, Total Orders, Avg Order Value |
| Line Chart        | Sales Over Time, Avg Delivery Days by Month                   |
| Bar Chart         | Avg Delivery Delay by Month, Total Orders by Category         |
| Donut / Pie Chart | Payment Type Distribution, Sales by Category                  |
| Map               | Orders and Sales by State                                     |
| Matrix            | PaymentValue by State and PaymentType                         |
| Scatter Plot      | Delivery Delay vs Sales by Payment Type and Category          |

### ⚙️ Advanced Techniques Used

* **Hierarchies**: Year → Month
* **Drillthrough**: Category, State → Order details
* **Slicers**: Month, Payment Type, Customer Type, Category
* **Tooltips**: Show KPIs like average delivery, total sales, installments


---

## 4️⃣ Excel Integration (BI Front-End)

### 📊 Pivot Table Setup

* Fields Used:

  * **Rows**: State, CategoryName
  * **Columns**: PaymentType
  * **Values**:

    * Sum of `PaymentValue`
    * Average `Installments`
    * Count of `OrderID`

### 🎯 Matrix Report

* Created pivot-style matrix views
* Simulated roll-up/down using grouped rows and filtering

---

## 5️⃣ Debugging & Data Quality

* **Power BI Blank Visuals Fix**:

  * Resolved model relationship issues
  * Checked for duplicate entries using:

    ```sql
    SELECT OrderID, COUNT(*) FROM FactOrder GROUP BY OrderID HAVING COUNT(*) > 1
    ```
  * Used `DISTINCT` in SQL to deduplicate rows

* **Hierarchy Not Working**:

  * Fixed by ensuring `Date` fields in `DimDate` were properly linked via `DateKey`
  * Verified drill options were enabled in Power BI visual headers

---

## 📌 Final Dashboard Title 

 E-commerce BI Dashboard – Sales, Delivery, and Payment Analytics”**

## 🧠 Key Learnings Demonstrated

* Full **ETL process**
* Star schema modeling
* **SSAS Cube** development
* Advanced **Power BI** visualizations with slicing, dicing, rollup/rolldown
* Excel integration for matrix and tabular analysis
* Handling BI design challenges (e.g., drillthrough not working, blank visuals)

##To get the files of dashboard,backup files vistit :"https://drive.google.com/drive/folders/1HWKQgnILKXOKJwm39d7PYsJk8gfmBmDq?usp=sharing"

##Thank you

