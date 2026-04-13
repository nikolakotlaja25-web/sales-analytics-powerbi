# Power BI Dashboard File

## 📊 SalesAnalytics.pbix

This is the main Power BI dashboard file for the Sales Analytics project.

**File size:** 1.98 MB  
**Power BI Desktop version:** 2.125+ (April 2024)

---

## 🚀 How to Use

### Option 1: Download and Explore
1. Download `SalesAnalytics.pbix` from this folder
2. Open in Power BI Desktop
3. Explore all 3 pages:
   - Page 1: Sales Overview
   - Page 2: Product Analysis
   - Page 3: Customer Insights

### Option 2: Refresh Data
If you modify the Excel data file:
1. Open `SalesAnalytics.pbix`
2. Home tab → **Refresh**
3. All visuals update automatically

---

## 📐 What's Inside

### Data Model:
- 3 tables: Sales_Data, Products, Customers
- Star schema with relationships
- 6 DAX measures in _Measures table

### Dashboard Pages:
- **Page 1: Sales Overview** - KPIs, trends, geographic distribution
- **Page 2: Product Analysis** - Product performance and profitability
- **Page 3: Customer Insights** - Customer analytics and segmentation

### DAX Measures:
- Total Sales
- Total Cost
- Profit
- Profit Margin %
- Total Orders
- Average Order Value

See [DAX_Formulas.md](../Documentation/DAX_Formulas.md) for complete documentation.

---

## 🔧 Requirements

- **Power BI Desktop** (free download from Microsoft)
- Windows 10/11
- 4GB RAM minimum

---

## 📝 Notes

- Data source: `../Data/SalesData.xlsx`
- All data is relative - no hardcoded paths
- Works out of the box after download
- No gateway or cloud connection required

---

## 🎓 Learning Path

If you want to build this from scratch:
1. Read [Setup_Guide.md](../Documentation/Setup_Guide.md)
2. Load data from Excel
3. Create relationships
4. Add DAX measures
5. Build visuals
6. Compare with this file!

---

**Happy exploring!** 🎉
