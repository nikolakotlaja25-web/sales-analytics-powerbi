# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-04-12

### Added
- Initial version of Sales Analytics Dashboard
- 100 rows of sales transactions (January-March 2024)
- 10 products across 3 categories (Accessories, Electronics, Furniture)
- 20 customers from 6 cities in Serbia
- Excel data source with 3 connected tables (Sales_Data, Products, Customers)
- Star schema data model with relationships
- 6 basic DAX measures:
  - Total Sales
  - Total Cost
  - Profit
  - Profit Margin %
  - Total Orders
  - Average Order Value
- 3 dashboard pages:
  - Sales Overview (KPIs, trend, category breakdown, map)
  - Product Analysis (top products, sales vs cost)
  - Customer Insights (top customers, distribution map)
- Interactive filters (date slicer, category filter)
- Documentation:
  - README.md with complete project overview
  - DAX_Formulas.md with detailed explanations
  - Setup_Guide.md with step-by-step instructions
  - GitHub_Upload_Guide.md with Git instructions
- .gitignore for Power BI and Excel temp files

### Technical Details
- Data period: 2024-01-01 to 2024-03-31
- Total transactions: 100
- Average Order Value: varies by product
- Power BI Desktop version: 2.125+ (April 2024)

---

## [Unreleased]

### Planned for v1.1.0
- [ ] Time Intelligence DAX measures (YTD, MoM, YoY)
- [ ] Additional customer segmentation analysis
- [ ] Product category drill-through page
- [ ] Forecasting visual (sales prediction)
- [ ] What-if parameter for scenario analysis
- [ ] Custom tooltips with additional metrics
- [ ] Mobile layout optimization

### Planned for v1.2.0
- [ ] Integration with Power BI Service
- [ ] Row-level security (RLS) for multi-user scenarios
- [ ] Incremental refresh setup
- [ ] Performance tuning and aggregations
- [ ] Additional data sources (web scraping, API)

### Future Ideas
- [ ] Python visuals for advanced analytics
- [ ] R script integration for statistical analysis
- [ ] Q&A natural language queries
- [ ] Bookmark navigator for predefined views
- [ ] Automated email reports

---

## Versioning

**MAJOR.MINOR.PATCH**

- **MAJOR**: Major changes that are not backward compatible
- **MINOR**: New features that are backward compatible
- **PATCH**: Bug fixes and minor changes

---

## How to Contribute

If you want to contribute to the project:

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## Maintenance

Project maintained by: Nikola Kotlaja

Last updated: April 12, 2024
