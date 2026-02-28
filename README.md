#🛒 Retail Sales Analysis
January 25, 2026
📌 Project Overview
Database Name: p1_retail_db

This project is created to showcase practical SQL skills that are commonly used by Data Analysts in real-world scenarios. The main goal is to analyze retail sales data, clean it, explore patterns, and answer important business questions using SQL.

This project is especially suitable for beginners who want to build a strong SQL foundation and add a hands-on project to their data analytics portfolio.

This project includes:
Database creation

Data cleaning techniques

Exploratory Data Analysis (EDA)

Business-focused SQL queries

Insight generation for decision-making

🎯 Project Objectives
Create and set up a retail sales database

Identify and remove missing or null data

Perform exploratory data analysis (EDA)

Solve real business problems using SQL queries

Generate meaningful insights from sales data

🗂️ Project Structure
1️⃣ Database Setup
🔹 Database Creation
CREATE DATABASE p1_retail_db;
🔹 Table Creation
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
🔹 Total Number of Records
SELECT COUNT(*) FROM retail_sales;
🔹 Unique Customer Count
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
🔹 Unique Product Categories
SELECT DISTINCT category FROM retail_sales;
🔹 Checking for Null Values
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
🔹 Removing Records with Missing Values
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
🔹 Total Sales by Product Category
SELECT
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
🔹 Average Age of Customers Buying Beauty Products
SELECT
    ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
🔹 High-Value Transactions (Sales > ₹1000)
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
🔹 Transactions by Gender and Category
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
🔹 Top 5 Customers Based on Total Sales
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
🔹 Orders by Sales Shift (Morning, Afternoon, Evening)
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
Customers belong to multiple age groups and purchase products across different categories such as Clothing and Beauty.

💰 High-Value Transactions
Several transactions exceed ₹1000, indicating the presence of premium customers and high-value purchases.

📈 Sales Trends
Monthly analysis helps identify the best-performing months in each year, which is useful for seasonal planning.

🧠 Customer Insights
The analysis highlights top-spending customers and identifies popular product categories.

📑 Reports Generated
Sales Summary Report

Category-wise Performance Analysis

Monthly and Shift-Based Sales Trends

Top Customers and Customer Distribution

✅ Conclusion
This Retail Sales Analysis project highlights the practical use of SQL in real-world data analysis. From database creation and data cleaning to exploratory analysis and business reporting, the project demonstrates essential analytical skills. It effectively converts raw sales data into actionable insights, making it a strong beginner-level, self-developed portfolio project for aspiring data analysts
