# 🧠 LeetCode 1731 – The Number of Employees Which Report to Each Employee

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employees**

| Column Name | Type    |
|------------|---------|
| employee_id| int     |
| name       | varchar |
| age        | int     |
| reports_to | int     |

- `employee_id` is the primary key.
- Each employee may report to another employee via `reports_to`.

---

### 📝 Task

Write a SQL query to report for each employee:

- Number of **direct reports**
- **Average age** of their direct reports (rounded to the nearest integer)

Return results ordered by `employee_id`.

---

## 🧩 Approach

- Aggregate the `Employees` table by `reports_to` to:
  - Count direct reports
  - Calculate average age
- Join the aggregated result back to the `Employees` table to get employee names.
- Order the final output by `employee_id`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT E.EMPLOYEE_ID, E.NAME, T.REPORTS_COUNT, T.AVERAGE_AGE
FROM EMPLOYEES E JOIN 
(SELECT REPORTS_TO, COUNT(*) AS REPORTS_COUNT, ROUND(AVG(AGE)) AS AVERAGE_AGE
FROM EMPLOYEES
GROUP BY REPORTS_TO) T
ON T.REPORTS_TO = E.EMPLOYEE_ID
ORDER BY E.EMPLOYEE_ID;
