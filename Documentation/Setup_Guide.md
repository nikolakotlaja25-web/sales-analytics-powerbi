# 🚀 Setup Guide - Step by Step

## 📋 Before You Begin

### Required Software:
- ✅ Power BI Desktop ([Download](https://powerbi.microsoft.com/desktop/))
- ✅ Excel or CSV reader
- ✅ Git (optional, for cloning the repo)

### Prerequisites:
- Windows 10/11 (Power BI Desktop is Windows-only)
- 4GB RAM minimum
- 2GB free disk space

---

## 📥 STEP 1: Download the Project

### Option A: Git Clone (Recommended)
```bash
git clone https://github.com/nikolakotlaja25-web/sales-analytics-powerbi.git
cd sales-analytics-powerbi
```

### Option B: Download ZIP
1. Go to the GitHub repo
2. Click **Code** → **Download ZIP**
3. Extract to your desired folder

---

## 📊 STEP 2: Review the Data

1. **Open the Excel file**:
   - Navigate to `Data/SalesData.xlsx`
   - Open in Excel

2. **Check the sheets**:
   - ✅ **Sales_Data** - 100 rows of transactions
   - ✅ **Products** - 10 products
   - ✅ **Customers** - 20 customers

3. **Understanding the data**:
   ```
   Sales_Data: OrderID | Date | ProductID | CustomerID | Quantity | UnitPrice
   Products: ProductID | ProductName | Category | CostPrice
   Customers: CustomerID | CustomerName | City | Country
   ```

---

## 🔧 STEP 3: Open Power BI Desktop

1. **Launch Power BI Desktop**
2. Click **Get Data** (start screen)
3. Select **Excel** from the list
4. Navigate to `Data/SalesData.xlsx`
5. Click **Open**

---

## 📦 STEP 4: Load Tables

### Import Wizard:
1. **You'll see the Navigator panel** with sheets
2. ✅ Check all three sheets:
   - ☑️ Sales_Data
   - ☑️ Products
   - ☑️ Customers
3. Click **Transform Data** (NOT Load!)

---

## 🔄 STEP 5: Power Query Transformations

### Sales_Data Transformations:
1. **Check Data Types**:
   - OrderID → Whole Number
   - Date → Date
   - ProductID → Text
   - CustomerID → Text
   - Quantity → Whole Number
   - UnitPrice → Decimal Number

2. **Rename columns** (if needed):
   - Right-click on column → Rename

### Products Transformations:
1. **Data Types**:
   - ProductID → Text
   - ProductName → Text
   - Category → Text
   - CostPrice → Decimal Number

### Customers Transformations:
1. **Data Types**:
   - CustomerID → Text
   - CustomerName → Text
   - City → Text
   - Country → Text

### Finish Transformations:
- Click **Close & Apply** (top left)

---

## 🔗 STEP 6: Create Relationships (Model View)

1. **Click the Model View icon** (left sidebar)

2. **Create Relationship 1**:
   - Drag `Sales_Data[ProductID]` → `Products[ProductID]`
   - Cardinality: Many to One (*)
   - Cross filter: Single

3. **Create Relationship 2**:
   - Drag `Sales_Data[CustomerID]` → `Customers[CustomerID]`
   - Cardinality: Many to One (*)
   - Cross filter: Single

4. **Verify Relationships**:
   ```
   Sales_Data (*) -----> (1) Products
   Sales_Data (*) -----> (1) Customers
   ```

---

## 📐 STEP 7: Create DAX Measures

1. **Create Measures Table**:
   - Home tab → Enter Data
   - Leave table empty, name: `_Measures`
   - Click Load

2. **Add Measures (in _Measures table)**:

   **Measure 1: Total Sales**
   ```dax
   Total Sales = 
   SUMX(
       Sales_Data,
       Sales_Data[Quantity] * Sales_Data[UnitPrice]
   )
   ```
   - Select `_Measures` in Fields
   - Home → New Measure
   - Paste formula
   - Format: Currency ($)

   **Measure 2: Total Cost**
   ```dax
   Total Cost = 
   SUMX(
       Sales_Data,
       Sales_Data[Quantity] * RELATED(Products[CostPrice])
   )
   ```
   - Format: Currency ($)

   **Measure 3: Profit**
   ```dax
   Profit = 
   [Total Sales] - [Total Cost]
   ```
   - Format: Currency ($)

   **Measure 4: Profit Margin %**
   ```dax
   Profit Margin % = 
   DIVIDE([Profit], [Total Sales], 0) * 100
   ```
   - Format: Percentage (2 decimals)

   **Measure 5: Total Orders**
   ```dax
   Total Orders = 
   DISTINCTCOUNT(Sales_Data[OrderID])
   ```
   - Format: Whole Number

   **Measure 6: Average Order Value**
   ```dax
   Average Order Value = 
   DIVIDE([Total Sales], [Total Orders], 0)
   ```
   - Format: Currency ($)

---

## 📊 STEP 8: Create Report View (Dashboard)

### Page 1: Sales Overview

1. **Rename page** → "Sales Overview"

2. **Top Cards (KPI section)**:
   - Insert → Card (4 times)
   - Arrange horizontally at the top
   
   **Card 1**: Total Sales
   - Drag `Total Sales` measure
   - Format → Callout value → Font size: 36
   
   **Card 2**: Profit
   - Drag `Profit` measure
   
   **Card 3**: Profit Margin %
   - Drag `Profit Margin %` measure
   
   **Card 4**: Total Orders
   - Drag `Total Orders` measure

3. **Line Chart - Sales Trend**:
   - Insert → Line Chart
   - X-axis: `Sales_Data[Date]` (Month level)
   - Y-axis: `Total Sales`
   - Title: "Sales Trend Over Time"

4. **Pie Chart - Sales by Category**:
   - Insert → Pie Chart
   - Legend: `Products[Category]`
   - Values: `Total Sales`
   - Title: "Sales by Category"

5. **Map - Sales by City**:
   - Insert → Map
   - Location: `Customers[City]`
   - Size: `Total Sales`
   - Title: "Sales by City"

6. **Slicer - Date Range**:
   - Insert → Slicer
   - Field: `Sales_Data[Date]`
   - Slicer settings → Between (range slider)

---

### Page 2: Product Analysis

1. **Add new page** → "Product Analysis"

2. **Table - Top Products**:
   - Insert → Table
   - Columns:
     - `Products[ProductName]`
     - `Total Sales`
     - `Profit`
     - `Profit Margin %`
   - Sort by `Total Sales` DESC
   - Title: "Top Products by Sales"

3. **Clustered Bar Chart**:
   - Insert → Clustered Bar
   - Y-axis: `Products[ProductName]`
   - Values: `Total Sales`, `Total Cost`
   - Title: "Sales vs Cost by Product"

4. **Clustered Column Chart**:
   - Insert → Clustered Column
   - X-axis: `Products[Category]`
   - Values: `Total Sales`, `Profit`
   - Title: "Performance by Category"

---

### Page 3: Customer Insights

1. **Add new page** → "Customer Insights"

2. **Table - Top Customers**:
   - Insert → Table
   - Columns:
     - `Customers[CustomerName]`
     - `Customers[City]`
     - `Total Sales`
     - `Total Orders`
   - Sort by `Total Sales` DESC

3. **Map - Customer Distribution**:
   - Insert → Map
   - Location: `Customers[City]`
   - Size: `Total Orders`

4. **Matrix - Sales by Customer & Category**:
   - Insert → Matrix
   - Rows: `Customers[CustomerName]`
   - Columns: `Products[Category]`
   - Values: `Total Sales`

---

## 🎨 STEP 9: Formatting and Theme

1. **Apply Theme**:
   - View tab → Themes → Executive
   
2. **Background**:
   - Format pane → Canvas background
   - Color: #F5F5F5 (light gray)

3. **Titles Formatting**:
   - All visuals → Format → Title
   - Font: Segoe UI
   - Size: 14pt
   - Color: #333333

4. **Margins & Alignment**:
   - Format pane → General → Effects
   - Background: White
   - Border: None
   - Shadow: On

---

## 💾 STEP 10: Save the Project

1. **Save As**:
   - File → Save As
   - Navigate to `Reports/` folder
   - Name: `SalesAnalytics.pbix`
   - Save

2. **Auto-save**:
   - File → Options → Save
   - ✅ Enable AutoRecover

---

## 📸 STEP 11: Screenshot for GitHub

1. **Full Screen Mode**:
   - View → Full Screen

2. **Take Screenshot**:
   - Windows: `Win + Shift + S`
   - Screenshot the entire page

3. **Save**:
   - Paste in Paint/Photoshop
   - Save as `dashboard_preview.png`
   - Copy to `Screenshots/` folder

---

## 🔄 STEP 12: Refresh Data

### If you change Excel data:

1. **In Power BI Desktop**:
   - Home tab → Refresh
   - All visuals update automatically

2. **If you add new columns**:
   - Home → Transform Data
   - Add new transformations
   - Close & Apply

---

## ✅ STEP 13: Quality Check

### Before posting to GitHub:

- ✅ All relationships are connected
- ✅ All DAX formulas work (no errors)
- ✅ Visuals display correct data
- ✅ No blank visuals
- ✅ All titles are clear
- ✅ Screenshot is added

---

## 🐛 Troubleshooting

### Problem: "Cannot find ProductID in related table"
**Solution**: Check that relationships are properly created in Model View

### Problem: DAX formula returns BLANK
**Solution**: Check that Data Types are correct (Decimal instead of Text)

### Problem: Visual doesn't show data
**Solution**: Check Filters pane → Are there any conflicts?

### Problem: "Circular dependency detected"
**Solution**: Check that you don't have measures referencing each other in a loop

---

## 📚 Next Steps

1. **Publish to Power BI Service** (optional):
   - Home → Publish
   - Sign in with Microsoft account
   - Share dashboard with others

2. **Optimize Performance**:
   - Use Aggregations for large files
   - Implement Incremental Refresh

3. **Add More Analysis**:
   - What-If parameters
   - Forecast analysis
   - Clustering

---

## 🎓 Further Learning

### Recommended Courses:
- Microsoft Learn: Power BI Data Analyst
- SQLBI: Mastering DAX
- Guy in a Cube (YouTube channel)

### Documentation:
- [Power BI Docs](https://docs.microsoft.com/power-bi/)
- [DAX Guide](https://dax.guide/)

---

**🎉 Congratulations! You've completed the Power BI project! 🎉**

Now you can:
- Push to GitHub
- Add to your portfolio
- Share with potential employers

---

**Questions?** Open an Issue on the GitHub repo!
