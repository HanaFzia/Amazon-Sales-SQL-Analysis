# Amazon-Sales-SQL-Analysis
This project explores Amazon Sales Data between February 2 and April 2 2025, using SQL to extract  meaningful business insights. The goal is to help stakeholders understand customer behavior, product performance, and operational efficiency.

## Objectives
To analyze and summarize key performance indicators (KPIs) from raw sales data using SQL, and provide data-driven answers to common business questions.

## Business Questions Answered
Dataset Source: [Amazon Sales 2025 (Kaggle)](https://www.kaggle.com/datasets/zahidmughal2343/amazon-sales-2025)

#### Order Performance
How many orders were completed?
```
SELECT*
FROM "amazon_sales_data 2025"
WHERE status='Completed';
```
![image](https://github.com/user-attachments/assets/3bc9d113-5a48-4444-83c4-9e5047a07016)

How many orders were cancelled?
```
SELECT*
FROM "amazon_sales_data 2025"
WHERE status='Cancelled';
```
![image](https://github.com/user-attachments/assets/2ba19bb5-9819-42ae-805a-776aff7e2ad2)

#### Revenue and Product Performance
What are the top 5 selling products by *quantity*?
```
SELECT product,
status,
SUM (quantity) AS total_quantity_sold
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY product
ORDER BY total_quantity_sold DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/19834124-a347-4cd0-9cf1-98ede58eeb47)

What are the top 5 selling products by *total sales*?
```
SELECT product,
category,
status,
SUM (total_sales) AS total_sales_sold
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY product
ORDER BY total_sales_sold DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/ed52adb2-fdfc-4c50-b456-b3f3bf7595bd)

What are the top 5 product categories by *quantity*?
```
SELECT category,
status,
SUM (quantity) AS total_quantity_sold
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY category
ORDER BY total_quantity_sold DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/04a31841-56a3-4d6b-91c0-54b025fbe350)

What are the top 5 product categories by *total sales*?
```
SELECT category,
status,
SUM (total_sales) AS total_sales_sold
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY category
ORDER BY total_sales_sold DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/bad4fa46-4db8-4655-bc70-da77253683a3)

What are the top cancelled products?
```
SELECT product,
status,
SUM (quantity) AS total_quantity_cancelled
FROM "amazon_sales_data 2025"
WHERE status = 'Cancelled'
GROUP BY product
ORDER BY total_quantity_cancelled DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/06e16565-4604-48dd-a5d3-4ce46ec1bc3c)

What is the average order value per product?
```
SELECT product,
AVG(total_sales)AS avg_order_value
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY product
ORDER BY avg_order_value DESC;
```
![image](https://github.com/user-attachments/assets/a0874319-fc5b-4c3e-b6e5-ff13096bc9c3)

What is the cancellation rate per category?
```
SELECT category,
status,
SUM (quantity) AS total_quantity_cancelled
FROM "amazon_sales_data 2025"
WHERE status = 'Cancelled'
GROUP BY category
ORDER BY total_quantity_cancelled DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/8df14813-3bba-479a-92a7-2432ba75d2e0)

#### Consumer Insights
Who are the top 5 customers by purchase amount?
```
SELECT customer_name,
SUM(total_sales)AS total_purchase_amount
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY customer_name
ORDER BY total_purchase_amount DESC;
```
![image](https://github.com/user-attachments/assets/cbd3205d-c6ec-4818-a656-0aafc5aad32d)

Which customer locations had the highest purchase volume?
```
SELECT customer_location,
status,
SUM (quantity) AS total_quantity_sold
FROM "amazon_sales_data 2025"
WHERE status = 'Completed'
GROUP BY customer_location
ORDER BY total_quantity_sold DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/f8bfe07e-2473-40aa-b5ba-5f9b7e7076aa)

#### Payment Behavior
What is the most used payment method?
```
SELECT payment_method,
SUM(CASE WHEN status = 'Completed' THEN 1 ELSE 0 END) AS completed,
SUM(CASE WHEN status = 'Cancelled' THEN 1 ELSE 0 END) AS cancelled
FROM "amazon_sales_data 2025"
GROUP BY payment_method;
```
![image](https://github.com/user-attachments/assets/0e93a76e-1f47-4f7a-98c2-7a24424120b4)
