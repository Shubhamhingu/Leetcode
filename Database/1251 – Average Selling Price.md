# 💰 LeetCode 1251 – Average Selling Price

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**Prices**

| Column Name | Type |
|------------|------|
| product_id | int  |
| price      | number |
| start_date | date  |
| end_date   | date  |

**UnitsSold**

| Column Name  | Type |
|-------------|------|
| product_id  | int   |
| units       | int   |
| purchase_date | date |

---

## 📝 Task

For each product, compute the **average selling price** based on actual units sold:

\[
\text{AVERAGE_PRICE} = \frac{\sum(\text{price} \times \text{units})}{\sum(\text{units})}
\]

- If no units were sold, return **0**.
- Round the result to **2 decimal places**.

---

## 🧩 Approach

1. **Join** `Prices` and `UnitsSold` on `PRODUCT_ID`  
2. Ensure that the `PURCHASE_DATE` is **within the price validity period** (`START_DATE` to `END_DATE`)  
3. Compute weighted average: `SUM(price * units) / SUM(units)`  
4. Use `NVL(...,0)` for products with no sales  
5. Group by `PRODUCT_ID`

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT P.PRODUCT_ID, 
       NVL(ROUND(SUM(P.PRICE * U.UNITS)/SUM(U.UNITS),2),0) AS AVERAGE_PRICE
FROM PRICES P 
LEFT JOIN UNITSSOLD U
ON P.PRODUCT_ID = U.PRODUCT_ID 
AND U.PURCHASE_DATE BETWEEN P.START_DATE AND P.END_DATE
GROUP BY P.PRODUCT_ID;
