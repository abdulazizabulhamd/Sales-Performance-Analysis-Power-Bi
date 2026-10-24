Sales Performance Analysis Dashboard | Power BI
1. Project Overview
This project focuses on analyzing sales performance using Microsoft Power BI. The objective was to transform raw sales data into an interactive dashboard that provides insights into revenue, profitability, product performance, customer behavior, geographical performance, sales trends, and product returns.
The project involved several stages, starting with data preparation and transformation using Power Query, followed by data modeling, DAX measure development, and interactive dashboard design.
Throughout the process, I encountered data preparation challenges that required understanding the underlying business logic to ensure accurate calculations and reliable analytical results.
Project Objectives
- Analyze overall sales performance and key business KPIs.
- Evaluate revenue, cost, profit, and gross profit margin.
- Identify top-performing products and product categories.
- Analyze sales performance across geographical regions.
- Understand customer purchasing behavior and order frequency.
- Examine sales trends over time.
- Analyze product returns and return quantities.
Tools and Technologies
- Microsoft Power BI: Data modeling, DAX calculations, and dashboard development.
- Power Query: ETL, data transformation, merging queries, and data preparation.
- DAX (Data Analysis Expressions): Measures, KPI calculations, and time intelligence.
- Data Modeling: Relationships between fact and dimension tables.
- Data Visualization: Interactive reports and business performance analysis.
2. Data Source and Structure
The project started with a collection of nine Excel files containing data related to sales transactions, customers, products, geographical information, product costs, and returns.
The files contained data organized across multiple related tables, requiring transformation and integration before they could be used effectively for analysis.
The dataset included the following tables:
Table	Purpose
Customers	Customer-related information
Geography	Geographical attributes
Products	Product information
Product Cost History	Product cost information
Product Subcategory	Product subcategory information
Region	Regional information
Sales Details	Transaction-level sales data
Sales Header	Order-level information
Sales Returns	Product return information


The Sales Details table served as the primary sales fact table, containing transaction-level information such as product identifiers, quantities, unit prices, and sales amounts.
The Sales Header table contained order-level information, including discount amounts, while the remaining tables provided additional context for analyzing sales by product, customer, geography, and other dimensions.
The initial challenge was to integrate these data sources while preserving the correct business meaning of each field.
3. Data Preparation and ETL Using Power Query
I used Power Query to perform the ETL process, which involved extracting data from the Excel files, transforming the tables, and preparing the resulting dataset for analysis.
The main objective was to integrate the required information into a consistent structure while addressing data issues that could affect the accuracy of the final calculations.
3.1 Integrating Product Cost Information
One of the first challenges was retrieving product cost information.
The cost data was stored separately in the Product Cost History table, while the Sales Details table contained the sales transactions required for profitability analysis.
To calculate profit correctly, the relevant cost information had to be integrated into the sales data.
However, I discovered that product cost was not necessarily constant. It varied depending on the product and the country.
This meant that matching records using the product identifier alone would not always retrieve the appropriate cost.
Solution:
I used Power Query's Merge Queries functionality to combine the relevant tables using multiple matching fields, including the information required to identify the appropriate product and country.
This allowed me to retrieve the corresponding cost information for the sales records and prepare the data for subsequent profitability calculations.
Key learning: Data integration requires understanding the business rules behind the data, not simply matching tables using a single identifier.
3.2 Integrating Sales Header and Sales Details
Another important challenge involved combining the Sales Header and Sales Details tables.
The two tables operated at different levels of detail:
- Sales Header: Contained order-level information, with each order represented by a single record.
- Sales Details: Contained transaction-line information, where an order could contain multiple product lines.
The Sales Details table included information such as unit price, unit cost, and quantity, while the Sales Header table contained the total discount associated with an order.
I merged the two tables in Power Query to bring the required order-level information into the sales details.
However, this introduced a potential double-counting problem.
3.3 Challenge: Preventing Discount Duplication
After merging the tables, I noticed that the total discount for an order was repeated across every sales detail row belonging to that order.
For example, consider an order with a total discount of $100 and ten product lines.
Before the merge, the order-level discount appeared once in Sales Header.
After the merge, the same $100 discount appeared on all ten rows in Sales Details.
If these values were summed directly, the resulting discount would be $1,000 instead of the correct $100.
This would inflate the total discount and could distort subsequent financial calculations.
Solution: Allocating the Order-Level Discount Across Product Lines
To address this issue, I used the sales value of each product line to determine its proportion of the total order sales.
The objective was to allocate the order-level discount proportionally across the individual product lines rather than repeating the full discount on every row.
The allocation logic can be expressed as follows:
Step 1: Calculate the proportion of each line's sales value within the order.
\[
\text{Line Sales Share}
=
\frac{\text{Line Sales Value}}
{\text{Total Order Sales Value}}
\]
Step 2: Calculate the discount allocated to each line.
\[
\text{Line Discount}
=
\text{Order Discount}
\times
\text{Line Sales Share}
\]
For example, suppose an order has the following characteristics:
- Total order sales: $1,000
- Total order discount: $100
- Product line sales value: $200
The product line represents 20% of the order's total sales.
Its allocated discount would therefore be:
\[
100 \times \frac{200}{1000} = \$20
\]
The allocated discounts across all product lines should add up to the original $100 order discount, assuming the allocation uses the complete set of order lines and the same sales-value basis.
This approach prevents the full order-level discount from being counted repeatedly and provides a more appropriate line-level discount value.
The transformation was performed during the data preparation stage using Power Query, before developing the DAX measures.
Key learning: Understanding the granularity of a dataset is essential when combining tables. Order-level values must be handled differently from transaction-level values to avoid double counting.
4. Data Modeling
After completing the ETL and data preparation stages, I established relationships between the relevant tables in Power BI.
The objective was to create a data model that supported consistent calculations and enabled analysis across multiple business dimensions.
4.1 Establishing Relationships
I created relationships between the sales data and the supporting tables, including product, customer, geographical, and other relevant information.
This enabled the report to analyze sales performance from different perspectives without requiring every descriptive attribute to be stored directly in the fact table.
The Sales Details table served as the central source for transaction-level sales analysis.
4.2 Creating a Calendar Table
I created a dedicated Calendar table to support time-based analysis and DAX Time Intelligence calculations.
A separate date table makes it possible to analyze sales performance across different periods and compare results between years or other time intervals.
It also provides a consistent date dimension for time-based filtering and reporting.
This enabled the development of measures comparing current-period performance with the corresponding period in the previous year.
5. DAX Measures and KPI Development
After preparing the data and establishing the model relationships, I started developing DAX measures to calculate the main business performance indicators.
These measures were used to support the dashboard's financial analysis and comparisons across different dimensions.
The measures included calculations related to:
- Revenue
- Cost
- Profit
- Gross Profit Margin
- Quantity Sold
- Previous-Year Revenue
- Revenue Variance
- Revenue Variance Percentage
Year-over-Year Analysis
Using the Calendar table and DAX Time Intelligence functions, I developed calculations to compare current performance with the corresponding period in the previous year.
The general logic for revenue variance is:
\[
\text{Revenue Variance}
=
\text{Current Revenue}
-
\text{Previous-Year Revenue}
\]
The variance percentage is:
\[
\text{Variance \%}
=
\frac{\text{Revenue Variance}}
{\text{Previous-Year Revenue}}
\times 100
\]
These calculations help evaluate whether revenue increased or decreased relative to the previous year.
The same general comparison approach can be applied to other metrics when the corresponding measures and comparison periods are defined appropriately.
6. Dashboard Development
After completing the data preparation, modeling, and calculation stages, I developed six report pages in Power BI.
Each page focused on a different aspect of business performance.
6.1 Main Dashboard
The main dashboard provides an overview of overall business performance through key performance indicators and visualizations.
It serves as the starting point for understanding the overall sales results.
6.2 Time Analysis
The time analysis page focuses on sales performance over time.
It supports the examination of sales trends and comparisons between different periods, helping identify changes in business performance.
6.3 Product Analysis
The product analysis page examines performance across products and product categories.
It supports comparisons involving revenue, cost, profit, and other relevant product-level metrics.
6.4 Location Analysis
The location analysis page explores sales performance across geographical areas.
It helps compare markets and identify differences in sales results between countries and regions.
6.5 Customer Analysis
The customer analysis page focuses on customer-related metrics and purchasing behavior.
It includes analysis of customer distribution and order frequency to help understand how customers interact with the business.
6.6 Returns Analysis
The returns analysis page examines product returns and return quantities.
It helps identify products associated with higher return volumes and provides an additional perspective on product performance.
7. Key Analytical Areas
The report was designed to explore several business questions.
Sales Performance
- How is overall revenue performing?
- How has revenue changed compared with the previous year?
- Which products and categories contribute most to revenue?
Profitability
- How do revenue, cost, and profit compare across products?
- Which products or geographical areas contribute most to profit?
- How does gross profit margin vary across the business?
Customer Behavior
- How are customers distributed across the dataset?
- How frequently do customers place orders?
- Which customer-related patterns can be observed in the available data?
Geographical Performance
- Which countries generate the highest revenue?
- How does profitability differ across geographical areas?
Product Returns
- Which products have the highest return quantities?
- What patterns can be observed in the available returns data?
These questions provide a framework for exploring the dataset and interpreting the results presented in the dashboard.
8. Challenges and Lessons Learned
This project provided practical experience in addressing data preparation challenges that could affect the reliability of a business intelligence solution.
The main challenges included:
1. Integrating data from multiple Excel files
Combining information from nine files required understanding the structure and purpose of the individual tables.
2. Handling product cost variations
Product cost depended on both the product and the country, requiring multiple matching fields when integrating cost information.
3. Preventing discount double counting
Merging order-level discount information into a transaction-level fact table caused the discount to repeat across multiple product lines. Allocating the discount according to each line's share of order sales addressed this issue.
4. Preparing the data model for analysis
Establishing table relationships and creating a dedicated Calendar table provided the foundation for multidimensional and time-based analysis.
5. Translating data into business reporting
Developing six report pages helped organize the analysis into distinct business perspectives, making it easier to explore sales, profitability, customers, geography, time, and returns.
The project reinforced the importance of understanding data granularity, validating calculations, and considering business logic before drawing conclusions from analytical results.
9. Conclusion
This project represents my first end-to-end practical data analysis project using Microsoft Power BI.
It provided an opportunity to apply data preparation, ETL, data modeling, DAX, and data visualization skills to a sales dataset.
Beyond building the dashboards, one of the most valuable parts of the experience was identifying and addressing data issues that could distort financial calculations.
The project strengthened my understanding of how a reliable business intelligence report depends on both technical implementation and a clear understanding of the underlying business data.
I look forward to continuing to develop my data analysis skills through additional projects and more advanced analytical challenges.
10. Project Screenshots
Screenshots of the six report pages will be included below to demonstrate the dashboard's structure and analytical capabilities.
Dashboard Page	Description
Main Dashboard	Overall business performance and KPIs
Time Analysis	Sales trends and period comparisons
Product Analysis	Product and category performance
Location Analysis	Geographical sales performance
Customer Analysis	Customer distribution and order frequency
Returns Analysis	Product returns and return quantities
