# Sales Performance Analysis Dashboard | Power BI

## 1. Project Overview

This project focuses on analyzing sales performance over a four-year period across multiple geographical regions using Microsoft Power BI.

The main objective is to transform raw sales data into an interactive dashboard that helps stakeholders understand business performance, identify sales trends, evaluate product and regional profitability, analyze product returns, and gain insights into customer behavior.

The project covers the complete data analysis workflow, including data preparation, data modeling, DAX measure development, dashboard design, and business insights.

## 2. Data Source and Structure

The project uses an Excel dataset containing nine related tables in a normalized structure.

The original dataset includes information about:

- Sales transactions and order details
- Customers and geographical locations
- Products and product categories
- Historical product costs
- Sales returns

The data was imported into Power BI, where Power Query was used to prepare and transform it for analysis.

## 3. Data Preparation and ETL

### Power Query Transformations

The initial data preparation process involved cleaning and transforming the source tables to create a more analysis-friendly structure.

The main steps included:

- Importing the source tables into Power BI.
- Transforming the normalized source data into a structure suitable for reporting.
- Merging related tables to bring the required business attributes into the sales data.
- Handling historical product costs and order-level discounts.
- Preparing the final tables for data modeling and analysis.

### Challenge 1: Integrating Historical Product Costs

Product costs were stored in a separate table and varied according to the product, country, year, and month.

To retrieve the correct cost for each sales record, I merged the sales data with the product cost history using four matching fields:

- Product
- Country
- Year
- Month

This approach helped associate sales records with the relevant historical product costs instead of applying a single cost value across different periods or locations.

### Challenge 2: Allocating Order-Level Discounts

The Sales Header table contained order-level information, including the total discount, while the Sales Details table contained individual order line items.

Merging these tables introduced a potential double-counting issue because the same order-level discount could be repeated across multiple sales lines.

To address this, I used each line item's share of the order's total sales value to allocate the order-level discount proportionally across its line items.

This approach was designed to distribute the discount according to each line item's contribution to the order and reduce the risk of overstating total discounts.

## 4. Data Modeling

After completing the data preparation process, I organized the data model around the following tables:

### Dimension Tables
- **Products:** Product-level information used for product and category analysis.
- **Customers:** Customer information used to analyze customer behavior and performance.

### Fact Tables
- **Sales Details:** Transaction-level sales information used to calculate sales, costs, quantities, and profitability.
- **Sales Returns:** Returned product information used to analyze return quantities and values.

### Calendar Table

I created a dedicated Calendar table using DAX with the `CALENDARAUTO()` function to support time-based analysis.

Relationships were established between the relevant tables to enable consistent filtering and analysis across products, customers, sales, returns, and dates.

## 5. DAX Measures and KPIs

I developed DAX measures to evaluate business performance and support the dashboard's analytical requirements.

The key measures include:

- Revenue
- Cost
- Profit
- Gross Margin
- Quantity Sold
- Number of Customers
- Number of Orders
- Average Order Value (AOV)
- Year-over-Year (YoY) Analysis
- Month-over-Month (MoM) Analysis
- Variance and Variance Percentage
- Customer Purchase Frequency
- Customer Churn Analysis
- Returned Quantity and Return Value

These measures support comparisons across different periods, products, customer groups, and geographical regions.

## 6. Dashboard Pages

The final Power BI dashboard consists of six analytical pages.

### Page 1: Main Dashboard

Provides an overview of overall business performance across the four-year period.

Key metrics and analyses include:

- Revenue, Profit, Cost, and Gross Margin
- Quantity Sold, Customers, and Orders
- Quarterly sales performance
- Revenue by product subcategory
- Revenue by continent
- Performance by business type

### Page 2: Location Analysis

Examines sales and profitability across geographical regions.

Key analyses include:

- Annual geographical performance
- Top-performing cities and states by sales
- Sales and quantity comparisons across countries
- Sales and profit comparisons across countries

### Page 3: Returns Analysis

Focuses on product returns and their potential business impact.

Key analyses include:

- Total returned quantity
- Return value
- Monthly return trends
- Returns by product category
- Returned quantity by product

### Page 4: Time Analysis

Evaluates business performance over time and highlights changes in sales.

Key analyses include:

- Monthly, quarterly, and yearly sales trends
- Year-over-Year revenue comparisons
- Month-over-Month revenue comparisons
- Time-based performance analysis using a matrix visual

### Page 5: Product Analysis

Evaluates product performance and profitability to identify opportunities for improvement.

Key analyses include:

- Top 10 products by sales
- Sales and profit comparisons across product categories
- Cost and gross margin comparisons across categories
- Differences in sales performance between products

### Page 6: Customer Analysis

Explores customer purchasing behavior, frequency, and retention patterns.

Key analyses include:

- Customer purchase frequency
- Customer churn analysis
- Customers who become inactive or stop purchasing
- Customer activity across countries
- Customer counts and the profit associated with customers in each country

## 7. Key Insights and Business Opportunities

The analysis highlighted several findings and opportunities for further investigation.

### Sales Performance and Growth
- Sales increased substantially across the analyzed years.
- Quarterly sales totals were relatively similar across the four-year period, while overall annual sales showed considerable growth.
- Sales performance varied significantly between products, indicating opportunities to review underperforming products and explore bundles or promotions where appropriate.

### Product Returns
- The total return value approached 7 million in the dataset's reporting units, making returns an important area for further investigation.
- June showed the highest return activity and the lowest sales during the observed three-year period, suggesting a potential seasonal pattern worth examining.

### Geographical Performance
- Brazil had the fourth-highest customer count but relatively low profitability compared with its customer base. Further analysis of product mix, pricing, and costs could help explain this result.
- France showed strong product profitability, suggesting an opportunity to investigate potential market expansion.
- Germany and the United Kingdom, along with Brazil and France, were identified as markets worth exploring for additional growth opportunities.

### Customer Retention
- The analysis indicated substantial year-to-year customer losses alongside the acquisition of new customers.
- This pattern highlights the importance of investigating customer retention, repeat purchasing behavior, and the factors associated with customer inactivity.

These findings can support further analysis and help stakeholders prioritize potential business actions. The proposed opportunities should be validated with additional investigation before implementation.

## 8. Challenges and Lessons Learned

This project provided practical experience in solving data preparation and analytical challenges, including:

- Integrating historical product costs using multiple matching fields.
- Handling differences in granularity between order-level and line-item-level data.
- Allocating order-level discounts to individual sales lines.
- Building a relational data model for analytical reporting.
- Developing DAX measures for financial and time-based analysis.
- Designing a multi-page dashboard to explore business performance from different perspectives.
- Translating analytical findings into potential business recommendations.

## 9. Tools and Technologies

- **Microsoft Power BI** — Dashboard development and data visualization
- **Power Query** — Data transformation and preparation
- **DAX** — Calculated measures and time-based analysis
- **Microsoft Excel** — Source data

## 10. Project Objectives

The project demonstrates the practical application of data analytics skills to a business-oriented sales dataset, with a focus on:

- Data cleaning and transformation
- Data modeling
- Business KPI development
- Sales and profitability analysis
- Time-series analysis
- Product returns analysis
- Customer behavior and retention analysis
- Interactive dashboard design
- Insight generation and business recommendations

## 11. Project Screenshots

Dashboard screenshots will be added here to demonstrate the final report pages and key visualizations.

## 12. Conclusion

This project demonstrates an end-to-end Power BI workflow, from preparing raw data and building a data model to developing DAX measures and delivering an interactive sales performance dashboard.

By analyzing sales trends, profitability, product returns, geographical performance, and customer behavior, the project illustrates how data analytics can help identify business patterns, investigate performance issues, and highlight opportunities for improvement.

**Project Type:** Sales Performance Analysis  
**Tool:** Microsoft Power BI  
**Focus Areas:** Data Preparation, Data Modeling, DAX, Business Intelligence, and Data Visualization
