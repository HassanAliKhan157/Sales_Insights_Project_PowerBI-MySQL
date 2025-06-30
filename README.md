# AtliQ Hardware - Sales Insights Dashboard Project

This project presents sales insights for **AtliQ Hardware**, an India-based company that supplies computer hardware and peripherals to clients such as Surge Stores and Nomad Stores across the country.

## Problem Statement

AtliQ Hardware has its head office in Delhi and multiple regional offices throughout India. The Sales Director has been facing several challenges:

**•** The market is growing dynamically.  
**•** Overall sales are declining.  
**•** Regional managers provide only verbal updates without supporting data.  
**•** There is no central dashboard to monitor performance region-wise or product-wise.  

Without factual data, the Sales Director cannot make effective, informed decisions. This project aims to build a centralized **Power BI dashboard** that enables real-time, data-driven decision-making to support business growth.

## Project Goals (AIMS Grid)

| **Component**     | **Description** |
|------------------|-----------------|
| **Purpose**       | Unlock hidden sales insights and automate reporting to reduce manual work. |
| **Stakeholders**  | Sales Director, Marketing Team, Customer Service Team, Data and Analytics Team, IT Department. |
| **End Result**    | An automated dashboard providing timely and clear sales insights for better decisions. |
| **Success Criteria** | **•** Dashboard reveals new insights<br>**•** Enables smarter, faster decisions<br>**•** Saves 10% of sales cost<br>**•** Saves 20% of business time spent on manual data gathering |

## Data Discovery and Analysis

The sales data was provided in a MySQL database and analyzed using SQL.

### Issues Identified

**•** Invalid market names in the `market` table  
**•** Negative and zero sales amounts in the `transactions` table  
**•** Transactions in USD despite operations being limited to India (should be INR)

### Sample SQL Queries

```sql
-- Total number of customers
SELECT COUNT(*) FROM sales.customers;

-- Transactions for Chennai (market_code = 'Mark001')
SELECT * FROM sales.transactions WHERE market_code = 'Mark001';

-- Total revenue in 2020
SELECT SUM(sales.transactions.sales_amount)
FROM sales.transactions
INNER JOIN sales.date
ON sales.transactions.order_date = sales.date.date
WHERE sales.date.year = 2020
  AND (sales.transactions.currency = 'INR' OR sales.transactions.currency = 'USD');
```

Similar queries were used to extract sales by city, year, month, and currency.

## Data Cleaning and ETL Process

Data was cleaned and transformed using **Power Query** in **Power BI Desktop**. Key steps:

**•** Connected MySQL database to Power BI  
**•** Removed null and blank rows from the `market` table  
**•** Filtered out negative and zero values from the `transactions` table  
**•** Converted all USD transactions to INR using a fixed exchange rate (`1 USD = 75 INR`)  
**•** Handled inconsistencies in currency formatting (`USD` vs `USD\r`)  

### Conversion Formula Used

```m
= Table.AddColumn(
    #"Filtered Rows",
    "norm_sales_amount",
    each if [currency] = "USD" then [sales_amount] * 75 else [sales_amount]
)
```

## Dashboard Toolkit

**•** Power BI Desktop – For building the main dashboard  
**•** Power Query – For transforming and cleaning the raw data  
**•** DAX (Data Analysis Expressions) – For calculated measures and logic  
**•** Data Modeling – To create relationships and star schema design  

## Dashboard Features

**•** Region-wise and city-wise sales performance  
**•** Year-on-year and month-wise revenue comparisons  
**•** Product-level insights and sales trends  
**•** Currency normalization to INR for consistency  
**•** Real-time filtering and cross-analysis capabilities  

## Impact and Benefits

**•** The Sales Director now has instant access to accurate and reliable sales insights  
**•** Helps identify underperforming regions and products  
**•** Saves time and reduces dependency on manual reporting  
**•** Enables fact-based strategic planning and forecasting  

## Dashboard Screenshot

![Dashboard Screenshot]()
