# 🧠 LeetCode 570 – Managers with at Least 5 Direct Reports

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employee**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |
| managerId  | int  |

`id` is the primary key for this table.  
Each row indicates an employee and their manager.

---

### 📝 Task

Write a SQL query to find the **names of managers** who have **at least 5 direct reports**.

Return the result table in **any order**.

---

## 🧩 Approach

- Use a **self-join** on the `Employee` table to relate managers and their direct reports.
- Group by the manager’s `id`.
- Use `HAVING COUNT(*) >= 5` to filter managers with at least five employees reporting to them.
- Join back to the `Employee` table to retrieve manager names.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT NAME FROM EMPLOYEE E
JOIN 
(SELECT E1.ID AS ID
FROM EMPLOYEE E1 JOIN EMPLOYEE E2
ON E1.ID = E2.MANAGERID
GROUP BY E1.ID
HAVING COUNT(*) >= 5) T
ON T.ID = E.ID;
