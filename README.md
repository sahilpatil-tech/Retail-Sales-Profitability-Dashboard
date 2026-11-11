# Retail Sales & Profitability Dashboard

## 1. Project Overview

The **Retail Sales & Profitability Dashboard** is an interactive business intelligence project developed using Microsoft Power BI. It analyses retail sales transactions to help businesses understand sales performance, profitability, product trends, customer behaviour and regional performance.

The dashboard transforms raw retail data into meaningful business insights through interactive visualisations, KPI cards, slicers, drill-through pages and report-page tooltips.

The project demonstrates practical skills in data cleaning, data modelling, DAX calculations, data visualisation and business analysis.

## 2. Business Problem

Retail businesses generate large amounts of transactional data across products, customers, regions and time periods. However, raw data alone does not provide a clear picture of business performance.

Management needs answers to questions such as:

- How much revenue is the business generating?
- How profitable is the business?
- Which product categories and sub-categories perform best?
- Which products generate losses?
- Which regions contribute the most sales and profit?
- Which customer segments generate the highest revenue?
- How do discounts affect profitability?
- How does sales performance change over time?

This project addresses these questions through an interactive Power BI dashboard.

## 3. Project Objectives

The main objectives are:

1. Analyse overall retail sales and profitability.
2. Identify high-performing and loss-making products.
3. Evaluate category and sub-category performance.
4. Understand customer purchasing behaviour.
5. Compare sales and profit across regions and customer segments.
6. Analyse monthly sales trends.
7. Provide an interactive dashboard for business decision-making.

## 4. Dataset Information

**Dataset:** Sample Superstore

**Source:** Tableau Sample Data

**Dataset link:** https://public.tableau.com/app/learn/sample-data

The dataset contains retail order-level information, including:

- Order ID
- Order Date
- Ship Date
- Customer ID
- Customer Name
- Segment
- Country
- City
- State
- Region
- Product ID
- Category
- Sub-Category
- Product Name
- Sales
- Quantity
- Discount
- Profit

The dataset is used to analyse transactional sales, product performance, customer behaviour and profitability.

*Note: Dataset availability and redistribution rights are subject to the source's terms and licence.*

## 5. Tools and Technologies

| Tool | Purpose |
|---|---|
| Microsoft Power BI Desktop | Dashboard development and visualisation |
| Power Query | Data cleaning and transformation |
| DAX | Measures and business calculations |
| Microsoft Excel | Initial dataset format and inspection |
| GitHub | Project documentation and portfolio hosting |

## 6. Data Cleaning and Preparation

Data preparation was performed using Power Query in Power BI.

The following steps were completed:

1. Imported the Sample Superstore Excel dataset.
2. Reviewed column names and data structure.
3. Verified and corrected data types.
4. Checked column quality and data distribution.
5. Checked for blank values and data errors.
6. Applied Trim and Clean transformations to text fields.
7. Verified date formats for Order Date and Ship Date.
8. Checked Row ID for duplicate records.
9. Renamed the main transaction table to `Fact_Sales`.
10. Applied the transformations using Close & Apply.

The objective was to prepare a consistent dataset for accurate analysis.

## 7. Data Model

The project uses a simple analytical data model with two tables.

### Fact_Sales

Contains transactional sales information, including:

- Order ID
- Row ID
- Order Date
- Customer ID
- Product ID
- Category
- Sub-Category
- Sales
- Profit
- Quantity
- Discount
- Region
- Segment

### Dim_Date

A separate calendar table created using DAX.

It includes:

- Date
- Year
- Month Number
- Month
- Quarter
- Year-Month
- YearMonth Sort

### Relationship

`Dim_Date[Date]` → `Fact_Sales[Order Date]`

- Cardinality: One-to-many (1:*)
- Cross-filter direction: Single
- Relationship status: Active

The calendar table supports time-based analysis and date filtering.

## 8. DAX Measures

The following measures were created to calculate key business metrics.

### Core Business Measures

**Total Sales**
```dax
Total Sales =
SUM(Fact_Sales[Sales])
```

**Total Profit**
```dax
Total Profit =
SUM(Fact_Sales[Profit])
```

**Total Orders**
```dax
Total Orders =
DISTINCTCOUNT(Fact_Sales[Order ID])
```

**Total Quantity**
```dax
Total Quantity =
SUM(Fact_Sales[Quantity])
```

**Profit Margin %**
```dax
Profit Margin % =
DIVIDE([Total Profit], [Total Sales], 0)
```

**Average Order Value**
```dax
Average Order Value =
DIVIDE([Total Sales], [Total Orders], 0)
```

### Product and Profitability Measures

**Total Discount**
```dax
Total Discount =
SUM(Fact_Sales[Discount])
```

**Average Discount**
```dax
Average Discount =
AVERAGE(Fact_Sales[Discount])
```

**Loss Making Products**
```dax
Loss Making Products =
COUNTROWS(
    FILTER(
        VALUES(Fact_Sales[Product Name]),
        CALCULATE([Total Profit]) < 0
    )
)
```

**Loss Making Orders**
```dax
Loss Making Orders =
COUNTROWS(
    FILTER(
        VALUES(Fact_Sales[Order ID]),
        CALCULATE([Total Profit]) < 0
    )
)
```

### Customer Analysis Measures

**Total Customers**
```dax
Total Customers =
DISTINCTCOUNT(Fact_Sales[Customer ID])
```

**Sales per Customer**
```dax
Sales per Customer =
DIVIDE([Total Sales], [Total Customers], 0)
```

**Profit per Customer**
```dax
Profit per Customer =
DIVIDE([Total Profit], [Total Customers], 0)
```

**Customer Orders**
```dax
Customer Orders =
DISTINCTCOUNT(Fact_Sales[Order ID])
```

These measures respond dynamically to the report's filter context, allowing users to analyse performance by date, product, customer, segment and region.

## 9. Dashboard Pages and Features

The report contains five pages, including three main analytical pages and two supporting pages.

### Page 1: Executive Overview

Provides a high-level summary of business performance.

**Key KPIs:**
- Total Sales
- Total Profit
- Total Orders
- Profit Margin %

**Visualisations:**
- Monthly Sales Trend
- Sales by Category
- Sales by Region
- Year, Region and Segment slicers

**Purpose:** Help management understand overall business performance and identify important sales trends.

### Page 2: Product & Profitability

Focuses on product-level performance and profitability.

**Visualisations:**
- Top 10 Products by Sales
- Profit by Sub-Category
- Discount vs Profit Analysis
- Product Performance Matrix

**Key metrics:**
- Total Sales
- Total Profit
- Profit Margin %
- Average Discount
- Loss-making products and orders

**Purpose:** Identify profitable products, loss-making products and the relationship between discounting and profit.

### Page 3: Customer & Regional Analysis

Provides insights into customer and geographical performance.

**Key KPIs:**
- Total Customers
- Total Sales
- Sales per Customer
- Profit per Customer

**Visualisations:**
- Top 10 Customers by Sales
- Sales and Profit by Customer Segment
- Regional Sales and Profit Performance
- Customer Performance Matrix

**Purpose:** Understand customer contribution, compare customer segments and evaluate regional performance.

### Page 4: Product Details

An interactive drill-through page that provides additional information about an individual product.

**Features:**
- Selected Product Name
- Category and Sub-Category
- Total Sales
- Total Profit
- Profit Margin %
- Product-level sales trends and details

**Purpose:** Allow users to move from summary-level analysis to detailed product-level investigation.

### Page 5: Product Tooltip

A report-page tooltip that displays additional product performance information when users hover over supported visuals.

**Information displayed:**
- Total Sales
- Total Profit
- Profit Margin %

**Purpose:** Provide additional context without navigating away from the main report page.

## 10. Interactive Features

The dashboard includes the following interactive capabilities:

- **Page Navigator:** Navigate between report pages.
- **Slicers:** Filter data by Year, Region and Segment.
- **Synchronized Slicers:** Maintain consistent filters across the main analytical pages.
- **Drill-through:** Open detailed product information from summary visuals.
- **Report-page Tooltips:** Display additional product metrics on hover.
- **Conditional Formatting:** Highlight positive and negative profitability.
- **Dynamic DAX Measures:** Recalculate KPIs based on selected filters.

These features make the dashboard easier to explore and support detailed business analysis.

## 11. Key Business Questions Answered

The dashboard is designed to answer the following questions:

1. What are the overall sales and profit figures?
2. How does monthly sales performance change over time?
3. Which product category generates the highest sales?
4. Which sub-categories generate the highest and lowest profits?
5. Which products contribute to business losses?
6. How are discounts associated with profitability?
7. Which regions contribute the most sales and profit?
8. Which customer segments generate the highest sales?
9. Who are the top 10 customers by sales?
10. How does individual product performance compare?

## 12. Business Recommendations

The dashboard can support decisions such as:

- Review loss-making products and investigate their cost and pricing structure.
- Evaluate discount strategies to avoid unnecessary reductions in profitability.
- Focus on high-performing categories and sub-categories.
- Investigate regional differences in sales and profit.
- Develop customer retention strategies for valuable customers.
- Monitor monthly sales trends to support business planning.
- Use product-level analysis to identify opportunities for improving margins.

Recommendations should be validated against the actual figures and business context before implementation.

## 13. Project Structure

```text
Retail-Sales-Profitability-Dashboard/
│
├── Dataset/
│   └── Source_Data.xlsx
│
├── Dashboard-Screenshots/
│   ├── 01_Executive_Overview.png
│   ├── 02_Product_Profitability.png
│   ├── 03_Customer_Regional_Analysis.png
│   └── 04_Product_Details.png
│
├── Documentation/
│   └── Project_Documentation.md
│
├── Retail_Sales_Profitability_Dashboard.pbix
│
└── README.md
```

The source dataset should only be included if redistribution is permitted by its licence. Otherwise, users can obtain it from the original source.

## 14. Skills Demonstrated

This project demonstrates practical skills in:

- Data cleaning and transformation
- Power Query
- Data modelling
- Calendar table creation
- DAX measures and calculations
- KPI development
- Sales and profitability analysis
- Product performance analysis
- Customer segmentation
- Regional analysis
- Interactive dashboard development
- Drill-through and report-page tooltips
- Conditional formatting
- Business insight generation
- GitHub project documentation

## 15. Future Improvements

Potential enhancements include:

- Year-over-year sales and profit analysis
- Sales growth percentage
- Month-over-month performance
- Customer retention and repeat purchase analysis
- Shipping performance analysis
- Advanced forecasting
- More detailed product profitability analysis

## 16. Author
**Developed By** - Sahil Patil

**Project:** Retail Sales & Profitability Dashboard

**Developed using:** Microsoft Power BI

**Purpose:** Data Analyst Portfolio Project

This project was developed to demonstrate practical business intelligence and data analytics skills using a retail sales dataset.

---

**Thank you for exploring this project!**
