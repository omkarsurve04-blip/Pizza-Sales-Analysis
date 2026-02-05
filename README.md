# Pizza-Sales-Analysis



## Project Overview

**Project Title**: Pizza Sales Analysis  
**Level**: Beginner  
**Database**: `pizza_db`
**Tools**: PostgreSQL + Power BI

This project analyzes a Pizza Sales dataset using PostgreSQL for data querying and Power BI for visualization to uncover business insights and customer behavior patterns.

## Objectives

Instead of just writing queries, II approached this project like a Business/Data Analyst, converting raw transactional data into:

1. KPIs	.
2. Sales trends
3. Product performance metrics.
4. Interactive dashboards


The objective was to help stakeholders answer:

1. How much revenue are we generating?.
2. What do customers order most?
3. Which pizzas perform best and worst?.
4. How do sales change daily and monthly?.



## Project Structure



### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `pizza_db`.
- **Table Creation**: A table named `pizza_db` is created to store the sales data. 

```sql
CREATE DATABASE pizza_db;

CREATE TABLE pizza_db (
    order_id INT,
    order_date DATE,
    order_time TIME,
    pizza_name VARCHAR(100),
    pizza_category VARCHAR(50),
    pizza_size VARCHAR(5),
    quantity INT,
    unit_price DECIMAL(10,2),
    total_price DECIMAL(10,2)
);

COPY pizza_db
FROM 'H:\Data Analyst\SQL\Pizza Sales Project\pizza_db.csv'
DELIMITER ','
CSV HEADER;
```


### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:


### Key Performance Indicators (KPIs)

1. **What is the total revenue generated from all pizza sales**:


```sql
SELECT SUM(total_price) AS total_revenue
FROM pizza_db;
```

2. **What is the average order value**

```sql
SELECT 
    SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value
FROM pizza_db;
```

3. **How many total pizzas were sold**:
```sql
SELECT SUM(quantity) AS total_pizzas_sold
FROM pizza_db;
```

4. **How many total orders were placed**:
```sql
SELECT COUNT(DISTINCT order_id) AS total_orders
FROM pizza_db;
```

5. **What is the average number of pizzas per order.**:
```sql
SELECT 
    SUM(quantity) * 1.0 / COUNT(DISTINCT order_id) AS avg_pizzas_per_order
FROM pizza_db;
```


### Sales Trends


6. **How do total orders vary day-wise (daily trend).**:
```sql
SELECT 
    to_char(order_date,'day') as order_day,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_db
GROUP BY order_day
ORDER BY total_orders desc
```

7. **How do total orders change month-wise (monthly trend).**:
```sql
SSELECT 
    TO_CHAR(order_date, 'Month') AS order_month,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_db
GROUP BY order_month
ORDER BY total_orders desc
```


### Category Insights


8. **What percentage of sales comes from each pizza category.**:
```sql
SELECT 
    pizza_category,
	sum(total_price)*100/
	(select  sum (total_price) from pizza_db) as percentage_sold
FROM pizza_db
GROUP BY pizza_category
    
```

### Product Performance Analysis


9. **What percentage of sales comes from each pizza size?**:
```sql
SELECT 
    pizza_size,
	sum(total_price)*100/
	(select  sum (total_price) from pizza_db) as percentage_sold
FROM pizza_db
GROUP BY pizza_size
```

10. **Which are the top 5 best sellers by revenue**:
```sql
SELECT 
    pizza_name,
    SUM(total_price) AS revenue
FROM pizza_db
GROUP BY pizza_name
ORDER BY revenue DESC
LIMIT 5;
```

11. **Which are the bottom 5 sellers by revenue.**:
```sql
SELECT 
    pizza_name,
    SUM(total_price) AS revenue
FROM pizza_db
GROUP BY pizza_name
ORDER BY revenue ASC
LIMIT 5;
```

12. **Which pizzas have the highest total quantity sold**:
```sql
SELECT 
    pizza_name,
    SUM(quantity) AS total_quantity
FROM pizza_db
GROUP BY pizza_name
ORDER BY total_quantity DESC
LIMIT 5;
```


13. **Which pizzas have the lowest total quantity sold.**:
```sql
SELECT 
    pizza_name,
    SUM(quantity) AS total_quantity
FROM pizza_db
GROUP BY pizza_name
ORDER BY total_quantity ASC
LIMIT 5;
```

14. **Which pizzas receive the highest number of orders**:
```sql
SELECT 
    pizza_name,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_db
GROUP BY pizza_name
ORDER BY total_orders DESC
LIMIT 5;
```


15. **Which pizzas receive the lowest number of orders.**:
```sql
SELECT 
    pizza_name,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_db
GROUP BY pizza_name
ORDER BY total_orders ASC
LIMIT 5;
```

##  Key Insights You Can Derive

- Revenue trends over time
- Customer ordering behavior
- Best & worst performing products
- Category and size preferences
- Sales optimization opportunities
- Classic & Supreme categories generate highest revenue
- Medium size pizzas dominate sales share
- Weekends show higher order volumes
- Few pizzas consistently underperform → candidates for promotion/removal
- Top 20% products drive majority of revenue 

##  Tech Stack

- PostgreSQL
- SQL (Aggregation, Window Functions, Grouping, Filtering)
- CSV Data Import
- Power BI
- DAX

##  Skills Demonstrated

- SQL querying
- Data cleaning
- KPI building
- Data modeling
- ashboard design
- Business storytelling




