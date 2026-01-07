# 📊 LeetCode 3564 – Seasonal Sales Analysis

**Difficulty:** Hard  
**Category:** SQL / Aggregation / Window Functions  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**Sales**

| Column Name | Type    |
|------------|---------|
| sale_id    | int     |
| product_id | int     |
| quantity   | int     |
| price      | decimal |
| sale_date  | date    |

**Products**

| Column Name | Type    |
|------------|---------|
| product_id | int     |
| category   | varchar |

- Each sale corresponds to a product, quantity, price, and sale date.  
- Each product belongs to a category.

---

### 📝 Task

For **each season** (Spring: Mar–May, Summer: Jun–Aug, Fall: Sep–Nov, Winter: Dec–Feb):

1. Compute **total quantity sold** and **total revenue** per category.  
2. Identify the **top category** per season based on:
   - Highest total quantity,  
   - Break ties using total revenue.  
3. Return:

- `SEASON` (Spring, Summer, Fall, Winter)  
- `CATEGORY`  
- `TOTAL_QUANTITY`  
- `TOTAL_REVENUE`  

---

## 🧩 Approach

1. **Separate the sales into seasonal tables** using `EXTRACT(MONTH FROM SALE_DATE)`.  
2. Compute **total quantity** and **total revenue** per category in each season.  
3. Use `RANK()` to rank categories per season by total quantity and total revenue.  
4. Filter for `RANKING = 1` to get the top category in each season.  

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH FALLTABLE AS (
    SELECT P.CATEGORY, P.PRODUCT_ID, S.PRICE, SUM(S.QUANTITY) AS TOT_QUANTITY,
    S.PRICE * SUM(S.QUANTITY) AS TOTAL_REVENUE
    FROM SALES S JOIN PRODUCTS P ON P.PRODUCT_ID = S.PRODUCT_ID
    WHERE EXTRACT(MONTH FROM SALE_DATE) IN (9,10,11)
    GROUP BY P.CATEGORY, P.PRODUCT_ID, S.PRICE
), SPRINGTABLE AS (
    SELECT P.CATEGORY, P.PRODUCT_ID, S.PRICE, SUM(S.QUANTITY) AS TOT_QUANTITY,
    S.PRICE * SUM(S.QUANTITY) AS TOTAL_REVENUE
    FROM SALES S JOIN PRODUCTS P ON P.PRODUCT_ID = S.PRODUCT_ID
    WHERE EXTRACT(MONTH FROM SALE_DATE) IN (3,4,5)
    GROUP BY P.CATEGORY, P.PRODUCT_ID, S.PRICE
), SUMMERTABLE AS (
    SELECT P.CATEGORY, P.PRODUCT_ID, S.PRICE, SUM(S.QUANTITY) AS TOT_QUANTITY,
    S.PRICE * SUM(S.QUANTITY) AS TOTAL_REVENUE
    FROM SALES S JOIN PRODUCTS P ON P.PRODUCT_ID = S.PRODUCT_ID
    WHERE EXTRACT(MONTH FROM SALE_DATE) IN (6,7,8)
    GROUP BY P.CATEGORY, P.PRODUCT_ID, S.PRICE
), WINTERTABLE AS (
    SELECT P.CATEGORY, P.PRODUCT_ID, S.PRICE, SUM(S.QUANTITY) AS TOT_QUANTITY,
    S.PRICE * SUM(S.QUANTITY) AS TOTAL_REVENUE
    FROM SALES S JOIN PRODUCTS P ON P.PRODUCT_ID = S.PRODUCT_ID
    WHERE EXTRACT(MONTH FROM SALE_DATE) IN (12,1,2)
    GROUP BY P.CATEGORY, P.PRODUCT_ID, S.PRICE
), FINTABLE AS (
    SELECT RANK() OVER (ORDER BY SUM(F.TOT_QUANTITY) DESC, SUM(F.TOTAL_REVENUE) DESC) AS RANKING,
    'Fall' AS SEASON, F.CATEGORY, SUM(F.TOT_QUANTITY) AS TOTAL_QUANTITY, SUM(F.TOTAL_REVENUE) AS TOTAL_REVENUE
    FROM FALLTABLE F
    GROUP BY F.CATEGORY
    UNION
    SELECT RANK() OVER (ORDER BY SUM(SP.TOT_QUANTITY) DESC, SUM(SP.TOTAL_REVENUE) DESC) AS RANKING,
    'Spring' AS SEASON, SP.CATEGORY, SUM(SP.TOT_QUANTITY) AS TOTAL_QUANTITY, SUM(SP.TOTAL_REVENUE) AS TOTAL_REVENUE
    FROM SPRINGTABLE SP
    GROUP BY SP.CATEGORY
    UNION
    SELECT RANK() OVER (ORDER BY SUM(S.TOT_QUANTITY) DESC, SUM(S.TOTAL_REVENUE) DESC) AS RANKING,
    'Summer' AS SEASON, S.CATEGORY, SUM(S.TOT_QUANTITY) AS TOTAL_QUANTITY, SUM(S.TOTAL_REVENUE) AS TOTAL_REVENUE
    FROM SUMMERTABLE S
    GROUP BY S.CATEGORY
    UNION
    SELECT RANK() OVER (ORDER BY SUM(W.TOT_QUANTITY) DESC, SUM(W.TOTAL_REVENUE) DESC) AS RANKING,
    'Winter' AS SEASON, W.CATEGORY, SUM(W.TOT_QUANTITY) AS TOTAL_QUANTITY, SUM(W.TOTAL_REVENUE) AS TOTAL_REVENUE
    FROM WINTERTABLE W
    GROUP BY W.CATEGORY
)
SELECT SEASON, CATEGORY, TOTAL_QUANTITY, TOTAL_REVENUE
FROM FINTABLE
WHERE RANKING = 1;
