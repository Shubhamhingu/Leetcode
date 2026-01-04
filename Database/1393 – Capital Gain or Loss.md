# 📈 LeetCode 1393 – Capital Gain/Loss

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Stocks**

| Column Name     | Type    |
|-----------------|---------|
| stock_name      | varchar |
| operation       | varchar | — "Buy" or "Sell"  
| price           | number  |
| operation_day   | date    |

---

## 📝 Task

For each stock, calculate the **capital gain or loss**:

- Buying a stock reduces capital (subtract `PRICE`)  
- Selling a stock increases capital (add `PRICE`)  
- Sum over all transactions per stock  

Return:

- `STOCK_NAME`  
- `CAPITAL_GAIN_LOSS`  

---

## 🧩 Approach

1. Use a `CASE` statement to assign **negative value for "Buy"** and positive for "Sell"  
2. Use a **CTE (`WITH`)** to create a temporary table with adjusted prices  
3. Aggregate with `SUM(NEW_PRICE)` grouped by `STOCK_NAME`  

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT STOCK_NAME,
           CASE
               WHEN OPERATION = 'Buy' THEN -1 * PRICE
               ELSE PRICE
           END AS NEW_PRICE
    FROM STOCKS
    ORDER BY OPERATION_DAY
)
SELECT STOCK_NAME, SUM(NEW_PRICE) AS CAPITAL_GAIN_LOSS
FROM TEMPTABLE
GROUP BY STOCK_NAME;
