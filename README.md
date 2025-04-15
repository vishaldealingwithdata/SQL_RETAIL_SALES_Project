# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner  
**Database**: `p1_retail_db`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `p1_retail_db`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE SQL_SALES_PROJECT1;
USE SQL_SALES_PROJECT1;

-- CREATE TABLE

CREATE TABLE RETAIL_SALES (
transactions_id INT PRIMARY KEY,
sale_date DATE,
sale_time TIME,
customer_id INT,
gender varchar(15),
age INT,
category VARCHAR(15),
quantity INT,
price_per_unit FLOAT,
cogs FLOAT,
total_sale FLOAT
);

SELECT * FROM RETAIL_SALES;
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
SELECT * FROM RETAIL_SALES
WHERE 
TRANSACTIONS_ID IS NULL
OR
SALE_DATE IS NULL
OR
SALE_TIME IS NULL
OR
CUSTOMER_ID IS NULL
OR
GENDER IS NULL
OR
AGE IS NULL
OR
CATEGORY IS NULL
OR
QUANTITY IS NULL
OR
PRICE_PER_UNIT IS NULL
OR
COGS IS NULL
OR
TOTAL_SALE IS NULL;

-- WHAT TOTAL SALES DO WE HAVE?
SELECT COUNT(TRANSACTIONS_ID) AS TOTAL_SALES
FROM RETAIL_SALES;

-- HOW MANY UNIQUE CUSTOMERS DO WE HAVE?
SELECT COUNT(DISTINCT CUSTOMER_ID) AS TOTAL_CUSTOMERS
FROM RETAIL_SALES;
```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

-- WHAT IS THE TOTAL REVENUE GENERATED FROM ALL RETAIL SALES?
SELECT SUM(TOTAL_SALE) AS TOTAL_REVENUE 
FROM 
RETAIL_SALES;

-- WHICH ARE THE TOP 2 PRODUCT CATEGORIES BASED ON TOTAL SALES AMOUNT?
SELECT CATEGORY, SUM(TOTAL_SALE) AS TOTAL_PROFIT FROM RETAIL_SALES
GROUP BY CATEGORY
ORDER BY TOTAL_PROFIT DESC LIMIT 2;

-- HOW DOES THE DAILY SALES TREND LOOK OVER TIME?
SELECT SALE_DATE, SUM(TOTAL_SALE) AS DAILY_SALES
FROM RETAIL_SALES
GROUP BY SALE_DATE
ORDER BY SALE_DATE;

-- WHAT IS THE AVERAGE NUMBER OF ITEMS SOLD PER TRANSACTION (AVERAGE BASKET SIZE)?
SELECT AVG(QUANTITY) AS AVERAGE_BASKET_SIZE
FROM RETAIL_SALES;

-- HOW IS THE CUSTOMER BASE DISTRIBUTED BY GENDER?
SELECT GENDER, COUNT(DISTINCT CUSTOMER_ID) AS TOTAL_CUST
FROM RETAIL_SALES
GROUP BY GENDER;

-- WHICH AGE PERSON SPENDS THE MOST ON AVERAGE PER TRANSACTION?
SELECT AGE, AVG(TOTAL_SALE)
FROM RETAIL_SALES
GROUP BY AGE
ORDER BY AVG(TOTAL_SALE) DESC;

-- LIST THE QUANTITY AND CUSTOMERS MAKING PURCHASES MORE THAN 3 TIMES?
SELECT CUSTOMER_ID, QUANTITY
FROM RETAIL_SALES
GROUP BY CUSTOMER_ID, QUANTITY
HAVING COUNT(*) > 3
ORDER BY QUANTITY DESC;

-- WHICH TIME OF DAY (MORNING, AFTERNOON, EVENING) GENERATES THE HIGHEST SALES?
SELECT 
  CASE
    WHEN SALE_TIME < '12:00:00' THEN 'MORNING'
    WHEN SALE_TIME < '17:00:00' THEN 'AFTERNOON'
    ELSE 'EVENING'
  END AS TIME_OF_DAY,
  SUM(TOTAL_SALE) AS TOTAL_SALES
FROM RETAIL_SALES
GROUP BY TIME_OF_DAY;

-- WHICH PRODUCT CATEGORY HAS THE HIGHEST TOTAL QUANTITY SOLD?
SELECT CATEGORY, SUM(QUANTITY)
FROM RETAIL_SALES
GROUP BY CATEGORY
ORDER BY SUM(QUANTITY) DESC LIMIT 1;

-- WHICH CUSTOMER CAN BE CONSIDERED FOR A LOYALTY PROGRAM BASED ON THEIR TOTAL SPENDING(MAX)?
SELECT DISTINCT CUSTOMER_ID, SUM(TOTAL_SALE)
FROM RETAIL_SALES
GROUP BY CUSTOMER_ID
ORDER BY SUM(TOTAL_SALE)
DESC LIMIT 1;
```

## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.


