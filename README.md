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

CREATE DATABASE p1_retail_db;
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

SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
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

SELECT
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
