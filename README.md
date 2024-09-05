# Online Sales Data Analysis Project using Power BI and mySQL

## Dashboard
![Dashboard PDF_page-0001](https://github.com/yashag1/EDA-project-revenue/assets/137886065/6f8e9eb0-11ea-4faa-9391-4ea375577d4b)


## Data Used
Dataset Link - [Online Sales Dataset](https://www.kaggle.com/datasets/shreyanshverma27/online-sales-dataset-popular-marketplace-data)

Data Cleaning & Analysis - MySQL Workbench, MySQL Command Line Client

Data Visualization - PowerBI


## Questions
1. What is the net revenue generated over the whole period?
2. What is the distribution of revenue by payment methods in different regions?
3. What is the distribution of revenue over different product categories?
4. What is the revenue trend with the months of operation?
5. Which are the top 3 selling products across different regions?


## SQL Queries
Question 1:
```sql
SELECT ROUND(SUM(total_revenue), 2) AS sales_till_date FROM sales;
```

Question 2:
```sql
SELECT region, payment_method, ROUND(SUM(total_revenue), 2) AS revenue FROM sales GROUP BY region, payment_method ORDER BY region;
```

Question 3:
```sql
SELECT category, ROUND(SUM(total_revenue), 2) AS revenue_by_category FROM sales GROUP BY category;
```

Question 4:
```sql
SELECT DATE_FORMAT(date, '%b') AS month, ROUND(SUM(total_revenue), 2) AS revenue_by_month FROM sales GROUP BY month;
```

Question 5:
```sql
WITH
ProductRevenue AS (
    SELECT region, product_name, SUM(total_revenue) AS revenue FROM sales GROUP BY region, product_name),
RankedProducts AS (
    SELECT region, product_name, revenue, ROW_NUMBER() OVER(PARTITION BY region ORDER BY revenue DESC) AS ranked FROM ProductRevenue)
SELECT region, product_name, revenue FROM RankedProducts WHERE ranked <= 3 ORDER BY region, ranked;
```

