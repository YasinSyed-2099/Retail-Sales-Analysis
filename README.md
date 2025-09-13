# Retail-Sales-Analysis

## Project Overview
**Project Title**: Retail Sales Analysis
**Database**: `Project1`

This project analyzes a Retail Sales dataset using SQL. The dataset contains information about customer transactions such as date, time, customer demographics, product category, and sales details. The focus is on building SQL skills step by step through  progressively challenging questions covering data cleaning, exploration, and business-focused analysis.

## Objective
1. **Design and structure a retail sales database.**
2. **Perform data cleaning to ensure data quality and consistency.**
3. **Conduct exploratory analysis to understand sales volume, customer demographics, and product categories.**
4. **Solve business questions using SQL queries involving filtering, grouping, aggregations, and ranking.**

## Project Structure

### 1. Database Setup 
 -- **Database Creation**:The project starts by creating a database named `Project1`
 -- **Table Creation**: A table named retail_sales_analysis is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE Project1;

CREATE TABLE retail_sales_analysis
(
transactions_id INT PRIMARY KEY,
sale_date DATE NULL,
sale_time TIME NULL,
customer_id INT NULL,
gender VARCHAR(15) NULL,
age INT NULL,
category VARCHAR(15) NULL,
quantity INT NULL,
price_per_unit FLOAT NULL,
cogs FLOAT NULL,
total_sale FLOAT NULL
);
```

### 2. Data Exploration & Cleaning
-- **Record Count**: Determine the total number of records in the dataset.
-- **Customer Count**: Find out how many unique customers are in the dataset.
-- **Category count**: Identify all unique product categories in the dataset.
-- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
SELECT * FROM retail_sales_analysis;

SELECT COUNT(*) AS Record_count
FROM retail_sales_analysis
;

SELECT COUNT(DISTINCT(customer_id)) AS Total_Customer 
FROM retail_sales_analysis
;

SELECT DISTINCT category 
FROM retail_sales_analysis
;

SELECT * FROM retail_sales_analysis
WHERE transactions_id IS NULL 
OR sale_date IS NULL 
OR sale_time IS NULL
OR customer_id IS NULL
OR gender IS NULL
OR age IS NULL
OR category IS NULL
OR quantity IS NULL
OR price_per_unit IS NULL
OR cogs IS NULL 
OR total_sale IS NULL
;

DELETE FROM retail_sales_analysis
WHERE sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL 
   OR gender IS NULL OR age IS NULL OR category IS NULL 
   OR quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

```

### 3. Data Analysis & Findings
The following SQL queries were developed to answer specific business questions:

1.**Write a SQL query to retrieve all columns for sales made on '2022-11-05'.** :
```sql
SELECT *
FROM retail_sales_analysis
WHERE sale_date = '2022-11-05'
;
```
