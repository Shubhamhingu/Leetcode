# 🛒 LeetCode 1045 – Customers Who Bought All Products

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables: **Customer**, **Product**

### Customer
| Column Name  | Type |
|-------------|------|
| customer_id | int  |
| product_key | int  |

Each row represents a customer purchasing a product.

### Product
| Column Name  | Type |
|-------------|------|
| product_key | int  |

---

## 📝 Task

Write a SQL query to find the `customer_id` of customers who have **bought all products** in the `Product` table.

---

## 🧩 Approach

- Count the **distinct products** bought by each customer
- Compare it with the **total number of products** in the Product table
- Return customers where these counts match

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT CUSTOMER_ID
FROM 
(SELECT CUSTOMER_ID, COUNT(DISTINCT(PRODUCT_KEY)) AS CNT
FROM CUSTOMER
GROUP BY CUSTOMER_ID)
WHERE CNT = (SELECT COUNT(*) FROM PRODUCT);
