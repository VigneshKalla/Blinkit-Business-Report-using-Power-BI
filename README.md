# Blinkit-Business-Report-using-Power-BI

# 📊 Blinkit BI Dashboard — Product & Outlet Performance Analysis

## 🔹 Project Overview
This project analyzes **Blinkit’s sales, product performance, outlet operations, and customer satisfaction** using **Power BI**.  
The dashboard provides actionable insights to improve **profitability, product availability, and operational efficiency**.

## 🔹 Business Problem
Blinkit management observed:
- Certain product categories underperform despite consistent demand.
- Outlet performance varies across **Tier 1, 2, and 3** cities.
- Sales are impacted by **item visibility** and **fat content labeling**.
- Customer satisfaction and repeatability require close monitoring.

👉 Goal: Build an interactive dashboard to **identify improvement areas and support data-driven decision-making**.

---

## 🔹 Dataset
The dataset contains **8,500+ sales records** with supporting dimension tables.

**Key fields include:**
- `Item Identifier` — Unique product code  
- `Item Type` — Product category (Fruits, Household, Frozen, etc.)  
- `Item Fat Content` — Regular or Low Fat  
- `Item Weight` — Weight in kg  
- `Item Visibility` — Shelf visibility percentage  
- `Sales` — Total sales value  
- `Rating` — Customer satisfaction score (out of 5)  
- `Outlet Identifier` — Unique outlet code  
- `Outlet Size` — Small, Medium, High  
- `Outlet Type` — Grocery, Supermarket (Type 1/2/3)  
- `Outlet Location Type` — Tier 1/2/3  
- `Outlet Establishment Year` — Year opened  

---

## 🔹 Data Cleaning & Transformation
Performed in **Power Query**:
- Handled missing values (`Item Weight`, `Sales`, `Fat Content`).  
- Standardized categorical fields (`LF` → `Low Fat`, `reg` → `Regular`).  
- Removed duplicates (`Item Identifier + Outlet`).  
- Created calculated columns:
  - `Sales per Kg = Sales ÷ Item Weight`
  - `Years of Operation = Current Year – Establishment Year`

---

## 🔹 Data Model (Star Schema)
- **Fact Table**: Sales (Sales, Rating, Weight, Visibility, etc.)  
- **Dimension Tables**: Items, Item Content, Outlets, Outlet Location, Cities  
- Relationships:  
  - `Sales[Item_ID] → Items[Item_ID]`  
  - `Sales[Fat_Content] → ItemContent[Fat_Content]`  
  - `Sales[Outlet_ID] → Outlets[Outlet_ID]`  
  - `Outlets[Location_ID] → OutletLocation[Location_ID]`  

---

## 🔹 DAX Measures
Some key measures:
```dax
Total Sales = SUM(Sales[Sales])

Avg Sales per Outlet = 
DIVIDE([Total Sales], DISTINCTCOUNT(Outlets[Outlet_ID]))

Avg Item Rating = AVERAGE(Sales[Rating])

Sales per Kg = 
DIVIDE(SUM(Sales[Sales]), SUM(Sales[Item_Weight]))

