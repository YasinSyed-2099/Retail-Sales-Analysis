# Retail-Sales-Analysis

## Project Overview
- **Project Title**: Retail Sales Analysis
- **Database**: `Project1`

This project analyzes a Retail Sales dataset using SQL. The dataset contains information about customer transactions such as date, time, customer demographics, product category, and sales details. The focus is on building SQL skills step by step through  progressively challenging questions covering data cleaning, exploration, and business-focused analysis.

## Objective
1. **Design and structure a retail sales database.**
2. **Perform data cleaning to ensure data quality and consistency.**
3. **Conduct exploratory analysis to understand sales volume, customer demographics, and product categories.**
4. **Solve business questions using SQL queries involving filtering, grouping, aggregations, and ranking.**

## Project Structure

### 1. Database Setup 
 - **Database Creation**: The project starts by creating a database named `Project1`
 - **Table Creation**: A table named retail_sales_analysis is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

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
- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

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

1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05'** :
```sql
SELECT *
FROM retail_sales_analysis
WHERE sale_date = '2022-11-05'
;
```
2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022** :
```sql
SELECT * 
FROM retail_sales_analysis
WHERE 
	category = 'clothing'
	AND DATE_FORMAT(sale_date,'%Y-%m') = '2022-11'
 AND quantity >= 4
;
```
3. **Write a SQL query to calculate the total sales (total_sale) for each category and total orders** :
```sql
SELECT 
	category,
    SUM(total_sale) AS Sales_amount,
    COUNT(*) AS Total_orders
FROM retail_sales_analysis
GROUP BY 1
;
```

4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category** :
```sql
SELECT 
 category,
 ROUND(AVG(age), 2) AS Average_age
 FROM retail_sales_analysis
WHERE category = 'Beauty'
;
```
5. **Write a SQL query to find all transactions where the total_sale is greater than 1000** :
```sql
SELECT * 
FROM retail_sales_analysis
WHERE 
	total_sale > 1000
;
```

6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category** :
```sql
SELECT 
	category,
    gender,
    COUNT(transactions_id) AS no_transaction
FROM retail_sales_analysis
GROUP BY 1, 2
ORDER BY 1 
;
```
7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year** :
```sql
SELECT 
	Year,
    Month,
    ROUND(avg_total_sales , 2) AS total_avg_sales
FROM
(
SELECT 
	YEAR(sale_date) AS Year,
    MONTH(sale_date) AS Month,
    AVG(total_sale) AS avg_total_sales,
    RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC ) AS rnk
FROM retail_sales_analysis
GROUP BY 1,2
) AS Table1
WHERE rnk = 1
;
```

8. **Write a SQL query to find the top 5 customers based on the highest total sales** :
```sql
SELECT 
	customer_id,
    SUM(total_sale) AS Total_sales
FROM retail_sales_analysis
GROUP BY customer_id
ORDER BY Total_sales DESC
LIMIT 5 
;
```

9. **Write a SQL query to find the number of unique customers who purchased items from each category** :
```sql
SELECT 
	category,
    COUNT(DISTINCT(customer_id)) AS unique_customers
FROM retail_sales_analysis
GROUP BY 1
;

```

10. **Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)** :
```sql
SELECT 
    CASE
		WHEN HOUR(sale_time)<= 12 THEN 'Morning'
        WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'evening'
        END AS time_of_day,
        COUNT(*) no_of_orders
FROM retail_sales_analysis
GROUP BY 1
;

```


## Findings

## Reports

## Conclusion








