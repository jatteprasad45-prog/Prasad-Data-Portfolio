#🛒 Retail Sales Analysis
<br>
January 25, 2026
<br>


📌 Project Overview
<br>

Database Name: p1_retail_db <br>


This project is created to showcase practical SQL skills that are commonly used by Data Analysts in real-world scenarios. The main goal is to analyze retail sales data, clean it, explore patterns, and answer important business questions using SQL.
<br>

This project is especially suitable for beginners who want to build a strong SQL foundation and add a hands-on project to their data analytics portfolio.
<br>

This project includes:
<br>

Database creation
<br>

Data cleaning techniques
<br>

Exploratory Data Analysis (EDA)
<br>

Business-focused SQL queries
<br>

Insight generation for decision-making
<br>

🎯 Project Objectives
<br>

Create and set up a retail sales database
<br>

Identify and remove missing or null data
<br>

Perform exploratory data analysis (EDA)
<br>

Solve real business problems using SQL queries
<br>

Generate meaningful insights from sales data
<br>

🗂️ Project Structure
<br>

1️⃣ Database Setup
<br>

🔹 Database Creation
<br>

CREATE DATABASE
p1_retail_db;
<br>

🔹 Table Creation
<br>

CREATE TABLE retail_sales (

    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
<br>

2️⃣ Data Exploration & Cleaning
<br>

🔹 Total Number of Records
<br>

SELECT COUNT(*) FROM retail_sales;
<br>

🔹 Unique Customer Count
<br>

SELECT 
COUNT(

DISTINCT customer_id
)
FROM retail_sales;
<br>
 
🔹 Unique Product Categories
<br>

SELECT DISTINCT category FROM retail_sales;
<br>

🔹 Checking for Null Values
<br>

SELECT *
FROM retail_sales
WHERE sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL;
<br>

🔹 Removing Records with Missing Values
<br>

DELETE FROM retail_sales
WHERE sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL;
📊 Data Analysis & Business Queries
🔹 Sales on a Specific Date
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
<br>

🔹 Clothing Sales (Quantity ≥ 4) in November 2022
<br>

SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity >= 4;
<br>

🔹 Total Sales by Product Category
<br>

SELECT
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
<br>

🔹 Average Age of Customers Buying Beauty Products
<br>

SELECT
    ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
<br>

🔹 High-Value Transactions (Sales > ₹1000)
<br>

SELECT *
FROM retail_sales
WHERE total_sale > 1000;
<br>

🔹 Transactions by Gender and Category
<br>

SELECT🛒 Retail Sales Analysis (SQL Project)

📅 January 25, 2026

📌 Project Overview

Database Name: p1_retail_db

This project demonstrates practical SQL skills commonly used by Data Analysts in real-world business scenarios. The objective is to analyze retail sales data, clean it, explore trends, and answer important business questions using SQL.

It is designed as a beginner-friendly portfolio project to build a strong SQL foundation.

🛠 Tools & Concepts Used

SQL (PostgreSQL/MySQL compatible)

Database Creation

Data Cleaning

Aggregations & Grouping

Window Functions (RANK)

CTE (Common Table Expressions)

Business-Oriented Query Writing

🎯 Project Objectives

Create and set up a retail sales database

Identify and remove missing/null data

Perform Exploratory Data Analysis (EDA)

Solve real business problems using SQL

Generate meaningful insights for decision-making

🗂️ Project Structure
1️⃣ Database Setup
🔹 Create Database
CREATE DATABASE p1_retail_db;
🔹 Create Table
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
2️⃣ Data Exploration & Cleaning
🔹 Total Records
SELECT COUNT(*) FROM retail_sales;
🔹 Unique Customers
SELECT COUNT(DISTINCT customer_id)
FROM retail_sales;
🔹 Unique Product Categories
SELECT DISTINCT category
FROM retail_sales;
🔹 Checking for Missing Values
SELECT *
FROM retail_sales
WHERE sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL;
🔹 Removing Missing Records
DELETE FROM retail_sales
WHERE sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL;
📊 Data Analysis & Business Queries
🔹 Sales on a Specific Date
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
🔹 Clothing Sales (Quantity ≥ 4) in November 2022
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity >= 4;
🔹 Total Sales by Category
SELECT
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
🔹 Average Age of Beauty Customers
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
🔹 High-Value Transactions (Sales > ₹1000)
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
🔹 Transactions by Gender & Category
SELECT
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
🔹 Best Selling Month in Each Year
SELECT year, month, avg_sale
FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY year, month
) t
WHERE rank = 1;
🔹 Top 5 Customers by Total Sales
SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
🔹 Unique Customers per Category
SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
🔹 Orders by Sales Shift
WITH hourly_sales AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT
    shift,
    COUNT(*) AS total_orders
FROM hourly_sales
GROUP BY shift;
🔍 Key Findings
👥 Customer Demographics

Customers belong to multiple age groups and purchase across different product categories such as Clothing and Beauty.

💰 High-Value Transactions

Several transactions exceed ₹1000, indicating premium customers and high-value purchases.

📈 Sales Trends

Monthly analysis identifies best-performing months in each year, useful for seasonal planning.

🧠 Customer Insights

The analysis highlights top-spending customers and identifies popular product categories.

📑 Reports Generated

Sales Summary Report

Category-wise Performance Analysis

Monthly & Shift-Based Sales Trends

Top Customers Analysis

✅ Conclusion

This project demonstrates practical SQL skills including database creation, data cleaning, aggregation, window functions, and business-driven analysis. It converts raw retail transaction data into meaningful business insights, making it a strong beginner-level portfolio project for aspiring data analysts.
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
<br>

🔹 Best Selling Month in Each Year
<br>

SELECT year, month, avg_sale
FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY year, month
) t
WHERE rank = 1;
<br>

🔹 Top 5 Customers Based on Total Sales
<br>

SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
<br>

🔹 Unique Customers per Category
<br>

SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
<br>

🔹 Orders by Sales Shift (Morning, Afternoon, Evening)
<br>

WITH hourly_sales AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT
    shift,
    COUNT(*) AS total_orders
FROM hourly_sales
GROUP BY shift;
<br>

🔍 Key Findings
<br>

👥 Customer Demographics
<br>

Customers belong to multiple age groups and purchase products across different categories such as Clothing and Beauty.
<br>

💰 High-Value Transactions
<br>

Several transactions exceed ₹1000, indicating the presence of premium customers and high-value purchases.
<br>

📈 Sales Trends
<br>

Monthly analysis helps identify the best-performing months in each year, which is useful for seasonal planning.
<br>

🧠 Customer Insights
<br>

The analysis highlights top-spending customers and identifies popular product categories.
<br>

📑 Reports Generated
<br>

Sales Summary Report
<br>

Category-wise Performance Analysis
<br>

Monthly and Shift-Based Sales Trends
<br>

Top Customers and Customer Distribution
<br>


✅ Conclusion
This Retail Sales Analysis project highlights the practical use of SQL in real-world data analysis. From database creation and data cleaning to exploratory analysis and business reporting, the project demonstrates essential analytical skills. It effectively converts raw sales data into actionable insights, making it a strong beginner-level, self-developed portfolio project for aspiring data analysts
