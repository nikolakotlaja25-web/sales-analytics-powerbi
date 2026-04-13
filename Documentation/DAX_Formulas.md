# 📐 DAX Formulas - Complete Documentation

## 📋 Table of Contents
1. [Basic Measures](#basic-measures)
2. [Advanced Measures](#advanced-measures)
3. [Time Intelligence](#time-intelligence)
4. [Calculated Columns](#calculated-columns)
5. [Best Practices](#best-practices)

---

## 🎯 Basic Measures

### 1. Total Sales
**Purpose**: Total revenue from sales

```dax
Total Sales = 
SUMX(
    Sales_Data, 
    Sales_Data[Quantity] * Sales_Data[UnitPrice]
)
```

**Explanation**:
- `SUMX` - iterates through each row of Sales_Data table
- For each row, multiplies Quantity by UnitPrice
- Sums all results

**Result**: Dynamic measure that adapts to filters

---

### 2. Total Cost
**Purpose**: Total cost of goods sold

```dax
Total Cost = 
SUMX(
    Sales_Data,
    Sales_Data[Quantity] * RELATED(Products[CostPrice])
)
```

**Explanation**:
- `RELATED` - follows relationship from Sales_Data to Products table
- Gets CostPrice from Products table for each product
- Multiplies by Quantity and sums

**Important**: This measure requires an active relationship between tables!

---

### 3. Profit
**Purpose**: Net profit

```dax
Profit = 
[Total Sales] - [Total Cost]
```

**Explanation**:
- Simple subtraction of two measures
- Inherits filter context from both measures

**Alternative with comment**:
```dax
Profit = 
-- Net profit = Revenue - Costs
[Total Sales] - [Total Cost]
```

---

### 4. Profit Margin %
**Purpose**: Profitability percentage

```dax
Profit Margin % = 
DIVIDE(
    [Profit], 
    [Total Sales], 
    0  -- default value if Total Sales = 0
) * 100
```

**Explanation**:
- `DIVIDE` - safe division that avoids division by zero
- Third argument (0) is the default value
- Multiply by 100 to get percentage

**Formatting**: In Power BI, apply "Percentage" format

---

### 5. Total Orders
**Purpose**: Count of unique orders

```dax
Total Orders = 
DISTINCTCOUNT(Sales_Data[OrderID])
```

**Explanation**:
- `DISTINCTCOUNT` - counts only unique values
- Ignores duplicates (if any)

**Difference from COUNT**:
- `COUNT` - counts all rows (including duplicates)
- `DISTINCTCOUNT` - counts only unique values

---

### 6. Average Order Value (AOV)
**Purpose**: Average order value

```dax
Average Order Value = 
DIVIDE(
    [Total Sales], 
    [Total Orders], 
    0
)
```

**Explanation**:
- AOV is a key metric in e-commerce
- Shows average spending per order

**Usage**: Tracking AOV over time shows success of upsell/cross-sell strategies

---

## 🚀 Advanced Measures

### 7. Sales vs Previous Month
**Purpose**: Comparison with previous month

```dax
Sales vs Previous Month = 
VAR CurrentSales = [Total Sales]
VAR PreviousMonthSales = 
    CALCULATE(
        [Total Sales],
        DATEADD(Sales_Data[Date], -1, MONTH)
    )
RETURN
    CurrentSales - PreviousMonthSales
```

**Explanation**:
- `VAR` - defines variables for cleaner code
- `CALCULATE` - modifies filter context
- `DATEADD` - shifts date by -1 month back
- `RETURN` - returns the difference

**Result**: Positive number = growth, negative = decline

---

### 8. Sales Growth %
**Purpose**: Sales growth percentage

```dax
Sales Growth % = 
VAR CurrentSales = [Total Sales]
VAR PreviousSales = 
    CALCULATE(
        [Total Sales],
        DATEADD(Sales_Data[Date], -1, MONTH)
    )
VAR Growth = 
    DIVIDE(
        CurrentSales - PreviousSales,
        PreviousSales,
        0
    )
RETURN
    Growth * 100
```

**Formula**: ((Current - Previous) / Previous) * 100

---

### 9. Top 3 Products by Sales
**Purpose**: Sum of sales for top 3 products

```dax
Top 3 Products Sales = 
CALCULATE(
    [Total Sales],
    TOPN(
        3, 
        ALL(Products[ProductName]), 
        [Total Sales], 
        DESC
    )
)
```

**Explanation**:
- `ALL` - removes existing filters from Products table
- `TOPN` - returns top 3 rows
- `DESC` - descending sort (largest to smallest)

---

### 10. Running Total
**Purpose**: Cumulative sum over time

```dax
Running Total = 
CALCULATE(
    [Total Sales],
    FILTER(
        ALL(Sales_Data[Date]),
        Sales_Data[Date] <= MAX(Sales_Data[Date])
    )
)
```

**Explanation**:
- `ALL` - removes filter from dates
- `FILTER` - returns only dates <= current date
- Sums from start to current date

**Visualization**: Line chart with Running Total

---

## ⏰ Time Intelligence

### 11. YTD Sales (Year-to-Date)
**Purpose**: Sales from start of year

```dax
YTD Sales = 
TOTALYTD(
    [Total Sales], 
    Sales_Data[Date]
)
```

**Explanation**:
- `TOTALYTD` - automatically calculates from January 1st to current date
- Requires Date table or Date column

---

### 12. Month-over-Month % Change
**Purpose**: Percentage change from previous month

```dax
MoM % = 
VAR CurrentMonth = [Total Sales]
VAR PreviousMonth = 
    CALCULATE(
        [Total Sales],
        DATEADD(Sales_Data[Date], -1, MONTH)
    )
RETURN
    DIVIDE(
        CurrentMonth - PreviousMonth,
        PreviousMonth,
        0
    ) * 100
```

---

### 13. Same Period Last Year
**Purpose**: Same period from previous year

```dax
Sales LY = 
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(Sales_Data[Date])
)
```

**Usage**: Year-over-year performance comparison

---

## 🔢 Calculated Columns

### 14. Total Revenue (per row)
**Note**: This is a **calculated column**, not a measure!

```dax
TotalRevenue = 
Sales_Data[Quantity] * Sales_Data[UnitPrice]
```

**When to use column vs measure**:
- **Column**: Calculated once when data is loaded
- **Measure**: Calculated dynamically at each interaction

**Rule**: Use measures whenever possible (better performance)!

---

### 15. Month Name
**Purpose**: Extract month name from date

```dax
MonthName = 
FORMAT(Sales_Data[Date], "MMMM")
```

**Result**: "January", "February", etc.

**For other languages**:
```dax
MonthName = 
FORMAT(Sales_Data[Date], "MMMM", "sr-RS")  -- Serbian
```

---

## ✅ Best Practices

### 1. Naming
```dax
-- ✅ GOOD: Clear and descriptive
Total Sales = ...
Profit Margin % = ...

-- ❌ BAD: Unclear
TS = ...
PM = ...
```

### 2. Comments
```dax
-- ✅ GOOD: With comments
Sales YTD = 
    -- Total sales from start of year
    TOTALYTD([Total Sales], Sales_Data[Date])

-- ❌ BAD: No context
Sales YTD = TOTALYTD([Total Sales], Sales_Data[Date])
```

### 3. VAR for complex formulas
```dax
-- ✅ GOOD: Use VAR for readability
Profit Margin % = 
VAR Sales = [Total Sales]
VAR Cost = [Total Cost]
VAR Profit = Sales - Cost
RETURN
    DIVIDE(Profit, Sales, 0) * 100

-- ❌ BAD: Everything in one line
Profit Margin % = DIVIDE([Total Sales] - [Total Cost], [Total Sales], 0) * 100
```

### 4. DIVIDE instead of /
```dax
-- ✅ GOOD: Safe division
Average = DIVIDE([Total Sales], [Total Orders], 0)

-- ❌ BAD: Can throw error
Average = [Total Sales] / [Total Orders]
```

### 5. Measures vs Columns
```dax
-- ✅ GOOD: Use measure for aggregations
Total Sales = SUMX(...)

-- ❌ BAD: Column for aggregation (large files)
TotalSales = SUMX(...)  -- as column
```

---

## 🎓 Additional Resources

1. **DAX Guide**: https://dax.guide/
2. **SQLBI**: https://www.sqlbi.com/
3. **Power BI Documentation**: https://docs.microsoft.com/dax/

---

## 📊 Testing Formulas

### How to test DAX measures:

1. **Create test table**:
```dax
Test Table = 
UNION(
    ROW("Measure", "Total Sales", "Value", [Total Sales]),
    ROW("Measure", "Profit", "Value", [Profit]),
    ROW("Measure", "Profit %", "Value", [Profit Margin %])
)
```

2. **Use DAX Studio** for performance testing

3. **Verify results** manually on a few examples

---

**💡 Pro tip**: Always test DAX formulas on a small dataset before applying to production!
