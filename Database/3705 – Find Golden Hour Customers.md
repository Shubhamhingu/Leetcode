# 🧠 LeetCode 3705 – Find Golden Hour Customers

**Difficulty:** Medium  
**Category:** SQL / Analytics / CTE  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **RESTAURANT_ORDERS**

| Column Name       | Type    |
|------------------|---------|
| ORDER_ID          | int     |
| CUSTOMER_ID       | int     |
| ORDER_TIMESTAMP   | datetime|
| ORDER_AMOUNT      | number  |
| ORDER_RATING      | number (nullable) |

A **golden hour customer** is defined as a customer who:

1. Places orders primarily during **peak hours**:
   - 11:00–13:00  
   - 14:00 exactly at 14:00  
   - 18:00–20:00  
   - 21:00 exactly at 21:00
2. Has **at least 3 total orders**.  
3. Has **more than 50% of orders rated**.  
4. Has an **average rating of at least 4.0**.  
5. Orders during peak hours for **at least 60% of their orders**.

---

### 🧩 Approach

1. **Mark each order** as `PEAK_HOUR` (1 if in peak hour, else 0) and `ORDER_RATED` (1 if order has rating, else 0).  
2. Aggregate by `CUSTOMER_ID` to calculate:
   - `TOTAL_ORDERS`
   - `PEAK_HOUR_PERCENTAGE` = #peak orders ÷ total orders
   - `AVERAGE_RATING`
   - `RATING_PERCENTAGE` = #rated orders ÷ total orders
3. Filter customers meeting all golden hour criteria:
   - `TOTAL_ORDERS >= 3`  
   - `PEAK_HOUR_PERCENTAGE >= 0.6`  
   - `RATING_PERCENTAGE >= 0.5`  
   - `AVERAGE_RATING >= 4.0`  

---

### 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT ORDER_ID, CUSTOMER_ID, ORDER_TIMESTAMP, ORDER_AMOUNT, ORDER_RATING,
    CASE WHEN (TO_CHAR(ORDER_TIMESTAMP, 'HH24') >= '11' AND (TO_CHAR(ORDER_TIMESTAMP, 'HH24') <= '13') 
        OR (TO_CHAR(ORDER_TIMESTAMP, 'HH24') = '14' AND TO_CHAR(ORDER_TIMESTAMP, 'MI') = '00') 
        OR (TO_CHAR(ORDER_TIMESTAMP, 'HH24') >= '18' AND TO_CHAR(ORDER_TIMESTAMP, 'HH24') <= '20') 
        OR (TO_CHAR(ORDER_TIMESTAMP, 'HH24') = '21' AND TO_CHAR(ORDER_TIMESTAMP, 'MI') = '00'))
    THEN 1
    ELSE 0
    END AS PEAK_HOUR,
    CASE WHEN ORDER_RATING IS NULL THEN 0
    ELSE 1
    END AS ORDER_RATED
    FROM RESTAURANT_ORDERS
), FINALTEMP AS (
    SELECT CUSTOMER_ID, COUNT(*) AS TOTAL_ORDERS, SUM(PEAK_HOUR)/COUNT(*) AS PEAK_HOUR_PERCENTAGE,
    ROUND(AVG(ORDER_RATING),2) AS AVERAGE_RATING, SUM(ORDER_RATED)/COUNT(*) AS RATING_PERCENTAGE
    FROM TEMPTABLE
    GROUP BY CUSTOMER_ID
)
SELECT CUSTOMER_ID, TOTAL_ORDERS, ROUND(PEAK_HOUR_PERCENTAGE * 100) AS PEAK_HOUR_PERCENTAGE,
AVERAGE_RATING
FROM FINALTEMP
WHERE TOTAL_ORDERS >= 3
AND PEAK_HOUR_PERCENTAGE >= 0.6
AND RATING_PERCENTAGE >= 0.5
AND AVERAGE_RATING >= 4.0
ORDER BY AVERAGE_RATING DESC, CUSTOMER_ID DESC;
