# 🧠 LeetCode 176 – Second Highest Salary

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employee**

| Column Name | Type |
|------------|------|
| id         | int  |
| salary     | int  |

`id` is the primary key for this table.  
Each row of this table contains information about the salary of an employee.

---

### 📝 Task

Write a SQL query to report the **second highest salary** from the `Employee` table.  
If there is no second highest salary, the query should return **NULL**.

---

## 🧩 Approach

- First, find the **maximum salary** in the table.
- Then, find the **maximum salary that is strictly less** than the highest salary.
- This handles duplicate highest salaries correctly.
- If no such salary exists, `MAX()` will return `NULL`.

---

## 🧪 SQL Solution

```sql
SELECT 
    MAX(Salary) AS SecondHighestSalary
FROM Employee
WHERE Salary < (
    SELECT MAX(Salary)
    FROM Employee
);
