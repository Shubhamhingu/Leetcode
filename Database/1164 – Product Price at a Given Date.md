# 🏷️ LeetCode 1164 – Product Price at a Given Date

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Products**

| Column Name  | Type |
|-------------|------|
| product_id  | int  |
| new_price   | int  |
| change_date | date |

Each row represents a product price change on a specific date.

---

## 📝 Task

Find the price of each product on **2019-08-16**.

Rules:
- If the product has a price change **on or before** `2019-08-16`, use the **latest price before or on that date**
- If the product has **no price change before that date**, return the default price **10**

---

## 🧩 Approach

This solution handles **two cases** using `UNION`:

### 1️⃣ Products with **no price change before the given date**
- These products get the default price `10`

### 2️⃣ Products with price changes
- Find the **latest change date ≤ given date**
- Fetch the corresponding price

Key techniques used:
- `NOT IN` for missing historical records
- `MAX(CHANGE_DATE)` to get the latest valid price
- `COALESCE` for safety fallback

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT PRODUCT_ID, 10 AS PRICE
FROM PRODUCTS
WHERE PRODUCT_ID NOT IN (
    SELECT PRODUCT_ID
    FROM PRODUCTS
    WHERE CHANGE_DATE <= TO_DATE('2019-08-16','YYYY-MM-DD')
    GROUP BY PRODUCT_ID
)
UNION
SELECT P.PRODUCT_ID AS PRODUCT_ID, COALESCE(P.NEW_PRICE,10)
FROM PRODUCTS P JOIN
(SELECT PRODUCT_ID, MAX(CHANGE_DATE) NEW_DATE
FROM PRODUCTS
WHERE CHANGE_DATE <= TO_DATE('2019-08-16','YYYY-MM-DD')
GROUP BY PRODUCT_ID) T
ON T.PRODUCT_ID = P.PRODUCT_ID AND T.NEW_DATE = P.CHANGE_DATE;
