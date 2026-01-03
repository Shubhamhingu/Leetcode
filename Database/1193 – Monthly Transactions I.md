# 📅 LeetCode 1193 – Monthly Transactions I

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Transactions**

| Column Name | Type |
|------------|------|
| trans_id   | int  |
| trans_date | date |
| country    | varchar |
| state      | varchar |
| amount     | number |

---

## 📝 Task

For each **month** and **country**, report:

- `TRANS_COUNT`: total number of transactions  
- `APPROVED_COUNT`: number of transactions with `state = 'approved'`  
- `TRANS_TOTAL_AMOUNT`: total amount of all transactions  
- `APPROVED_TOTAL_AMOUNT`: total amount of approved transactions  

Format the month as `'YYYY-MM'`.

---

## 🧩 Approach

1. Transform `state` and `amount` into **numeric flags** in a CTE:
   - `STATE = 1` if approved, else 0  
   - `APP_TRANS = amount` if approved, else 0  
2. Group by **month** and **country**
3. Aggregate:
   - `COUNT(*)` → total transactions  
   - `SUM(STATE)` → approved count  
   - `SUM(AMOUNT)` → total amount  
   - `SUM(APP_TRANS)` → approved amount

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */ 
WITH TEMP_TABLE AS (
    SELECT TO_CHAR(TRANS_DATE,'YYYY-MM') AS MONTH, COUNTRY, 
    CASE
        WHEN STATE = 'approved' THEN 1
        ELSE 0
    END AS STATE,
    AMOUNT,
    CASE 
        WHEN STATE = 'approved' THEN AMOUNT
        ELSE 0
    END AS APP_TRANS
    FROM TRANSACTIONS
)
SELECT MONTH, COUNTRY, COUNT(*) AS TRANS_COUNT, 
       SUM(STATE) AS APPROVED_COUNT, 
       SUM(AMOUNT) AS TRANS_TOTAL_AMOUNT,
       SUM(APP_TRANS) AS APPROVED_TOTAL_AMOUNT 
FROM TEMP_TABLE
GROUP BY COUNTRY, MONTH;
