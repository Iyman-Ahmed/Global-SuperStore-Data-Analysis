# Global-SuperStore-Data-Analysis
This project involves analyzing the Global Superstore 2 dataset to create a comprehensive Power BI dashboard that presents insights into sales, profit, customer behavior, and product performance. To explore key business metrics, trends, and patterns in an interactive and visually engaging manner. 
This project involves analyzing the Global Superstore 2 dataset to create a comprehensive Power BI dashboard that presents insights into sales, profit, customer behavior, and product performance. The dashboard allows users, including recruiters and hiring managers, to explore key business metrics, trends, and patterns in an interactive and visually engaging manner.

Dataset
The dataset used for this project is the Global Superstore 2 dataset, which contains sales transaction data from a global retail store. The dataset includes the following columns:

Order Date: The date when the order was placed.
Ship Date: The date when the order was shipped.
Customer ID: Unique identifier for each customer.
Customer Name: The name of the customer.
Segment: The business segment (e.g., Consumer, Corporate, Home Office).
Product Category: The category of products (e.g., Furniture, Technology, Office Supplies).
Product Sub-Category: More specific product grouping (e.g., Chairs, Phones).
Sales: The total sales value of the order.
Profit: The profit earned from the order.
Discount: Discount applied to the product.
Quantity: Quantity of products sold.
Market: The region where the sale took place (e.g., APAC, EMEA).
Region: The specific geographical region (e.g., Central, East).
Shipping Cost: The cost incurred to ship the product.


# Analysis and Data Processing
## 1. Data Cleaning & Preparation
Date Formatting: The Order Date and Ship Date fields were converted to the appropriate date format for time-series analysis.
Missing Values: We identified and handled missing values, such as missing postal codes, while ensuring key metrics like sales and profit remained intact.
Unique Customer Key: We created a composite key called Customer Country Key, which combines Customer Name and Country to account for cases where multiple Customer IDs were assigned to the same customer.



## 2. Sales and Profit Analysis
We performed an in-depth analysis of the overall sales and profit across different segments:

Total Sales & Profit: We created measures to calculate the sum of total sales and total profit across all regions.
Yearly Comparison: Calculated sales for 2013 and 2014 using DAX measures.
Percentage Growth: A measure was created to calculate the percentage growth between 2013 and 2014 to show year-over-year performance:
DAX
Copy code
Sales Growth % = 
DIVIDE(
    [Sales 2014] - [Sales 2013], 
    [Sales 2013], 
    0
)
Monthly Sales Trend: We extracted month numbers from the Order Date and displayed the monthly sales trend using a line chart, where each month was represented by its number (1 to 12).



## 3. Product Analysis
We evaluated product performance across categories and sub-categories:

Top Performing Sub-Categories: A DAX ranking measure was created to identify top-selling sub-categories by region/market:
DAX
Copy code
Sub-Category Sales Rank = 
RANKX(
    ALL('GlobalSuperstore'[Sub-Category]), 
    CALCULATE([Total Sales], ALLEXCEPT('GlobalSuperstore', 'GlobalSuperstore'[Region])),
    , 
    DESC, 
    Dense
)
Product Profitability: We used a scatter plot to visualize the relationship between product discounts and profitability. The plot revealed how discounts impacted product profitability and highlighted high-profit/low-discount products.
## 4. Customer Analysis
We analyzed customer behavior and segmented them based on loyalty and purchases:

New vs Returning Customers: We calculated new customers for 2013 and 2014, and returning customers, using measures:
DAX
Copy code
New Customers 2013 = 
CALCULATE(
    DISTINCTCOUNT('GlobalSuperstore'[Customer Country Key]),
    FILTER(
        'GlobalSuperstore',
        'GlobalSuperstore'[First Purchase Year] = 2013
    )
)

Returning Customers = 
CALCULATE(
    DISTINCTCOUNT('GlobalSuperstore'[Customer Country Key]),
    FILTER(
        'GlobalSuperstore',
        'GlobalSuperstore'[First Purchase Year] < YEAR('GlobalSuperstore'[Order Date])
    )
)
Customer Loyalty Metrics: Metrics such as Repeat Purchase Rate, Customer Lifetime Value (CLV), and Churn Rate were calculated to understand customer retention.
# 5. Visualization & Dashboard Creation
The Power BI dashboard includes the following pages:

### Page 1: Sales and Profit Analysis

Line charts, bar charts, and KPIs to show overall sales, profit trends, and year-over-year growth.
A bar chart displaying sales by region and market, highlighting top-performing regions.

### Page 2: Product Analysis

A scatter plot showing the relationship between discount and profit for each product.
A bar chart displaying top-performing product sub-categories by sales and profit across different regions.

### Page 3: Customer Analysis

A pie chart and bar chart comparing new vs returning customers in 2013 and 2014.
A table showing the top 10 customers by total sales.
Power BI Dashboard
The Power BI dashboard is interactive and allows users to:

Filter data by Year, Region, Market, and Product Category.
Explore detailed insights into sales performance, customer behavior, and product profitability.
View KPIs for key business metrics such as total sales, profit margin, and customer retention.
# How to Access the Dashboard
You can view the live Power BI dashboard by following this link (https://app.powerbi.com/links/3A4flj3jkL?ctid=e8ef11a3-0ad9-413f-97aa-ea65017c2470&pbi_source=linkShare). The dashboard showcases dynamic visuals with the ability to drill down and filter key metrics.

Conclusion
This analysis highlights key business metrics such as top-selling products, customer behavior, profitability trends, and regional performance. The dashboard provides an intuitive way to track business performance over time and make data-driven decisions.

Global_SuperStore_dashboard.pbix
Global_Superstore2.csv: The dataset used for this analysis.
