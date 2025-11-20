# 🧸🎪 Toy Store Performance Analysis & Sales Insight Dashboard

An interactive and analytics-driven Toy Store Performance Dashboard built using **Power BI**, designed to analyze sales, profit, inventory, product performance, and store-level insights across multiple locations.

The dashboard uses a **soft pastel toy-themed design** while maintaining professional BI standards.

---

## 🧩 1. Project Workflow Overview
A complete BI & ETL pipeline:

- **Power Query** → Cleaning & transforming raw CSV data
- **Data Modeling** → Star Schema with Product, Store, Inventory & Calendar dimensions
- **DAX Measures** → KPIs: Total Sales, Profit, Stock On Hand, Avg Sales/Store
- **Dashboard Design** → Pastel theme, icons, rounded KPI cards, subtle gradients

---

## 🧹 2. Data Cleaning & Preparation (Power Query)
### ✔ Datasets Used
- `sales.csv` → Month, Sale_ID, Store_ID, Product_ID, Units
- `products.csv` → Product_ID, Name, Category, Cost, Price
- `inventory.csv` → Product_ID, Store_ID, Stock_On_Hand
- `stores.csv` → Store_ID, Store_Name, Store_City, Store_Location
- `calendar.csv` → Dates, Month, Year

### 🔧 Cleaning Steps
- Removed **$ symbols** from price/cost
- Converted cost/price to **Decimal** type
- Ensured **Product_ID** & **Store_ID** types match
- Applied **Trim & Clean** on text
- Converted **Month** to numeric
- Removed **nulls & duplicates**
- Prepared Fact/Dimension structure

---

## ⭐ 3. Data Modeling – Star Schema
### **Fact Table — `sales`**
- Month
- Sale_ID
- Units
- Product_ID
- Store_ID

### **Dimension Tables**
- **products:** ID, Name, Category, Cost, Price
- **stores:** ID, Name, City, Location, Open_Date
- **inventory:** Product_ID, Store_ID, Stock_On_Hand
- **calendar:** Date, Month, Year

### ⭐ Relationships
- products → sales (1:M)
- stores → sales (1:M)
- products → inventory (1:M)
- stores → inventory (1:M)
- calendar → sales (Date → Month)

✔ Single-direction filters
✔ Clean analytical schema

---

## 🧮 4. DAX Measures
### **💰 Total Sales**
```DAX
Total Sales = 
SUMX(
    sales,
    sales[Units] * RELATED(products[Product_Price])
)
```

### **💵 Total Profit**
```DAX
Total Profit =
SUMX(
    sales,
    sales[Units] * (RELATED(products[Product_Price]) - RELATED(products[Product_Cost]))
)
```

### **📦 Stock In Hand**
```DAX
Stock In Hand = SUM(inventory[Stock_On_Hand])
```

### **🏪 Total Stores**
```DAX
Total Stores = DISTINCTCOUNT(stores[Store_ID])
```

### **📈 Average Sales per Store**
```DAX
Average Sales per Store = DIVIDE([Total Sales], [Total Stores])
```

---

## 🎨 5. Power BI Dashboard Design
### **Theme Features**
- Soft toy-themed background
- Rounded white KPI cards
- Yellow section headers
- Transparent (60–70%) bar/line charts
- Icons for KPIs
- Pastel palette (yellow, pink, peach, blue, purple)

### **Key Dashboard Elements**
#### 🧩 KPI Cards
- Stock In Hand
- Total Sales
- Total Stores
- Avg Sales/Store
- Total Profit

#### 📊 Visuals
- **Bar Chart:** Total Profit by Store
- **Matrix:** Top 10 Best-Selling Products
- **Line Chart:** Monthly Sales & Profit Trend
- **Category Trend Line Chart:** Sales & Profit by Category

#### 🎛 Filters/Slicers
- Category Slicer – Button style
- Month Slicer – Numeric

---

## 📁 6. Dataset Summary
| Metric | Value |
|--------|-------|
| Stores | 50 |
| Products | 40+ |
| Categories | 5 |
| Total Sales | 14M+ |
| Total Profit | 4M+ |
| Inventory Units | 30K+ |
| Time Period | 12 Months |

---

## 🧠 7. Key Business Insights
- **Toys & Electronics** generate maximum profit
- **Xalapa 2** is the most profitable store
- **Rubik’s Cube & PlayDoh Toolkit** are best sellers
- Mid-year shows highest sales volume
- Some products are **overstocked** → need inventory optimization

---

## 🚀 8. Future Enhancements
- Add **sales forecasting**
- Add **store-level drill-throughs**
- Add **Profit vs Stock** scatter chart
- Connect Power BI to **SQL** for auto-refresh
- Build a **weekly refresh pipeline**

---
## 🚀 9.Dataset 
Resource: https://mavenanalytics.io/data-playground/mexico-toy-sales

## 🙌 Conclusion
A vibrant, playful, and analytics-rich **Toy Store Performance Dashboard** that combines:
- Clean Star Schema
- Accurate DAX Measures
- Pastel toy-themed UI
- Clear business insights

