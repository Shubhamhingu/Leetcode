# 🍽️ LeetCode 1321 – Restaurant Growth

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Customer**

| Column Name | Type |
|------------|------|
| visited_on | date |
| amount     | number |

---

## 📝 Task

For each day, calculate a **7-day sliding window**:

1. `AMOUNT` – sum of total sales over the current day and previous 6 days  
2. `AVERAGE_AMOUNT` – average sales over the current day and previous 6 days (rounded to 2 decimals)  

Return results starting from the **7th day**, since a full 7-day window is required.

---

## 🧩 Approach

1. Aggregate **daily sales** using `SUM(amount)` grouped by `visited_on`  
2. Use a **window function (`SUM() OVER` and `AVG() OVER`)** with `ROWS BETWEEN 6 PRECEDING AND CURRENT ROW`  
   - Computes a 7-day sliding sum and average  
3. Use `ROW_NUMBER()` to filter out days before the first full 7-day window  

---

## 🧪 SQL Solution (PL/SQL)

```sql
WITH daily_sales AS (
    SELECT visited_on, SUM(amount) AS total_amount
    FROM Customer
    GROUP BY visited_on
), TEMPTABLE AS (
    SELECT to_char(visited_on,'YYYY-MM-DD') AS VISITED_ON, 
           SUM(total_amount) OVER (
               ORDER BY VISITED_ON
               ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
           ) AS AMOUNT,
           ROUND(AVG(total_amount) OVER (
               ORDER BY visited_on 
               ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
           ), 2) AS average_amount,
           ROW_NUMBER() OVER (ORDER BY VISITED_ON) AS RN
    FROM daily_sales
)
SELECT VISITED_ON, AMOUNT, AVERAGE_AMOUNT 
FROM TEMPTABLE
WHERE RN >= 7;
