# 📊 LeetCode 1070 – Product Sales Analysis III

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Sales**

| Column Name | Type |
|------------|------|
| sale_id    | int  |
| product_id | int  |
| year       | int  |
| quantity   | int  |
| price      | int  |

Each row represents the sale of a product in a given year.

---

## 📝 Task

Write a SQL query to find, for each product, the **first year it was sold**, along with the **quantity** and **price** in that year.

---

## 🧩 Approach

- Determine the **minimum year** for each product
- Join this result back to the `Sales` table
- Retrieve the corresponding quantity and price for that first year

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT T.PRODUCT_ID, T.YEAR_MIN AS FIRST_YEAR, S.QUANTITY, S.PRICE
FROM SALES S JOIN 
(SELECT PRODUCT_ID,MIN(YEAR) YEAR_MIN FROM SALES
GROUP BY PRODUCT_ID) T
ON T.PRODUCT_ID = S.PRODUCT_ID
AND T.YEAR_MIN = S.YEAR;
