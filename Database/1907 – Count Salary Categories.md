# 🧠 LeetCode 1907 – Count Salary Categories

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Accounts**

| Column Name | Type    |
|------------|---------|
| account_id | int     |
| income     | int     |

- `account_id` is the primary key.
- `income` is the salary of the account holder.

---

### 📝 Task

Write a SQL query to **count the number of accounts** in each salary category:

- **Low Salary:** income < 20000  
- **Average Salary:** 20000 ≤ income ≤ 50000  
- **High Salary:** income > 50000  

Include categories with zero accounts in the result.

---

## 🧩 Approach

- Create a fixed list of categories using a `UNION ALL` subquery.  
- Classify each account into a category using a `CASE` statement.  
- Aggregate counts per category and join with the fixed list to ensure all categories appear.  
- Use `COALESCE` to handle categories with no accounts.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT C.CATEGORY, COALESCE(A.ACCOUNTS_COUNT,0) AS ACCOUNTS_COUNT FROM 
(
    SELECT 'Low Salary' AS CATEGORY FROM DUAL
    UNION ALL
    SELECT 'Average Salary' FROM DUAL
    UNION ALL
    SELECT 'High Salary' FROM DUAL
) C LEFT JOIN (
SELECT CATEGORY, COUNT(*) AS ACCOUNTS_COUNT FROM
(
SELECT ACCOUNT_ID,
CASE WHEN INCOME < 20000 THEN 'Low Salary'
WHEN INCOME >= 20000 AND INCOME <= 50000 THEN 'Average Salary'
WHEN INCOME > 50000 THEN 'High Salary'
END AS CATEGORY
FROM ACCOUNTS
)
GROUP BY CATEGORY) A
ON A.CATEGORY = C.CATEGORY;
