# 🧮 LeetCode 3220 – Odd and Even Transactions

**Difficulty:** Medium  
**Category:** SQL / Conditional Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Transactions**

| Column Name        | Type |
|-------------------|------|
| transaction_id    | int  |
| transaction_date  | date |
| amount            | int  |

Each row represents a transaction with a certain `amount` on a given date.

---

### 📝 Task

For each `transaction_date`, calculate:
- The **sum of odd amounts** → `odd_sum`
- The **sum of even amounts** → `even_sum`

Return the result ordered by `transaction_date`.

---

## 🧩 Approach

1. Use a **CTE** to separate amounts into:
   - `EVEN_SUM` → amount if even, else `0`
   - `ODD_SUM` → amount if odd, else `0`
2. Aggregate the results by `transaction_date`.
3. Format the date using `TO_CHAR`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT TRANSACTION_DATE,
           CASE
               WHEN MOD(AMOUNT, 2) = 0 THEN AMOUNT
               ELSE 0
           END AS EVEN_SUM,
           CASE
               WHEN MOD(AMOUNT, 2) != 0 THEN AMOUNT
               ELSE 0
           END AS ODD_SUM
    FROM TRANSACTIONS
)
SELECT TO_CHAR(TRANSACTION_DATE,'YYYY-MM-DD') AS TRANSACTION_DATE,
       SUM(ODD_SUM) AS ODD_SUM,
       SUM(EVEN_SUM) AS EVEN_SUM
FROM TEMPTABLE
GROUP BY TRANSACTION_DATE
ORDER BY TRANSACTION_DATE;
