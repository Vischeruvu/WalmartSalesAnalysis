# Walmart Sales Data Analysis

## Overview

This project is designed to explore Walmart sales data to gain insights into the performance of different branches and products, sales trends, and customer behavior. The ultimate goal is to improve and optimize sales strategies. The dataset was sourced from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting).

The competition involved analyzing historical sales data from 45 Walmart stores located across various regions. Each store has multiple departments, and participants are tasked with forecasting sales for each department in each store. The challenge is further compounded by the inclusion of holiday markdown events, which are known to influence sales but are difficult to predict in terms of their impact on different departments.

## Objectives

The primary aim of this project is to analyze Walmart’s sales data to understand the factors influencing sales across different branches and to identify areas for improvement.

## Data Description

The dataset, obtained from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting), includes sales transactions from three Walmart branches located in Mandalay, Yangon, and Naypyitaw. The data comprises 17 columns and 1000 rows:

| Column                  | Description                             | Data Type      |
| :---------------------- | :-------------------------------------- | :------------- |
| invoice_id              | Invoice of the sales made               | VARCHAR(30)    |
| branch                  | Branch where the sales were made        | VARCHAR(5)     |
| city                    | Location of the branch                  | VARCHAR(30)    |
| customer_type           | Type of the customer                    | VARCHAR(30)    |
| gender                  | Gender of the customer making purchase  | VARCHAR(10)    |
| product_line            | Product line of the product sold        | VARCHAR(100)   |
| unit_price              | Price of each product                   | DECIMAL(10, 2) |
| quantity                | Amount of the product sold              | INT            |
| VAT                     | Amount of tax on the purchase           | FLOAT(6, 4)    |
| total                   | Total cost of the purchase              | DECIMAL(10, 2) |
| date                    | Date of the purchase                    | DATE           |
| time                    | Time of the purchase                    | TIMESTAMP      |
| payment_method          | Payment method used                     | VARCHAR(15)    |
| cogs                    | Cost of Goods Sold                      | DECIMAL(10, 2) |
| gross_margin_percentage | Gross margin percentage                 | FLOAT(11, 9)   |
| gross_income            | Gross Income                            | DECIMAL(10, 2) |
| rating                  | Rating                                  | FLOAT(2, 1)    |

## Analysis Areas

1. **Product Analysis**
   - Understand different product lines, identify top performers, and determine areas needing improvement.

2. **Sales Analysis**
   - Analyze sales trends of various products to assess the effectiveness of sales strategies and identify necessary adjustments.

3. **Customer Analysis**
   - Discover customer segments, purchase patterns, and profitability of each customer segment.

## Approach

1. **Data Wrangling**
   - Inspect the data to handle missing values and ensure data quality.

2. **Feature Engineering**
   - Create new columns to enhance analysis:
     - `time_of_day`: Categorize sales into Morning, Afternoon, and Evening.
     - `day_name`: Extract day of the week from the transaction date.
     - `month_name`: Extract month from the transaction date.

3. **Exploratory Data Analysis (EDA)**
   - Perform exploratory analysis to answer key business questions and derive insights.

4. **Conclusion**
   - Summarize findings and provide recommendations based on the analysis.

## Business Questions

### Generic

1. How many unique cities are represented in the data?
2. In which city is each branch located?

### Product

1. How many unique product lines are there?
2. What is the most common payment method?
3. What is the top-selling product line?
4. What is the total revenue by month?
5. Which month had the highest COGS?
6. Which product line generated the most revenue?
7. Which city has the highest revenue?
8. Which product line had the largest VAT?
9. For each product line, categorize as "Good" or "Bad" based on average sales.
10. Which branch sold more products than the average?
11. What is the most common product line by gender?
12. What is the average rating for each product line?

### Sales

1. Number of sales made during each time of day, by weekday.
2. Which customer type generates the most revenue?
3. Which city has the highest VAT percentage?
4. Which customer type incurs the highest VAT?

### Customer

1. How many unique customer types are there?
2. How many unique payment methods are there?
3. What is the most common customer type?
4. Which customer type makes the most purchases?
5. What is the predominant gender of customers?
6. What is the gender distribution per branch?
7. During which time of day do customers give the most ratings?
8. Which time of day sees the most ratings per branch?
9. Which day of the week has the highest average ratings?
10. Which day of the week has the highest average ratings per branch?

## Revenue and Profit Calculations

- **COGS**: `unit_price * quantity`
- **VAT**: `5% * COGS`
- **Total (Gross Sales)**: `VAT + COGS`
- **Gross Profit (Gross Income)**: `Total - COGS`
- **Gross Margin**: `gross_income / total_revenue`

**Example Calculation:**

Given:
- `Unit Price = 45.79`
- `Quantity = 7`

Calculate:
- **COGS**: `45.79 * 7 = 320.53`
- **VAT**: `5% * 320.53 = 16.0265`
- **Total**: `320.53 + 16.0265 = 336.5565`
- **Gross Margin Percentage**: `16.0265 / 336.5565 ≈ 4.76%`

## SQL Code

For detailed SQL queries, refer to the [SQL_queries.sql](https://github.com/Princekrampah/WalmartSalesAnalysis/blob/master/SQL_queries.sql) file.

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS walmartSales;

-- Create table
CREATE TABLE IF NOT EXISTS sales(
    invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12, 4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12, 4),
    rating FLOAT(2, 1)
);
