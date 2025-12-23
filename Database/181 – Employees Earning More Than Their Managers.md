# 🧠 LeetCode 181 – Employees Earning More Than Their Managers

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employee**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |
| salary     | int  |
| managerId  | int  |

`id` is the primary key for this table.  
Each row indicates an employee and their manager.

---

### 📝 Task

Write a SQL query to find the **employees who earn more than their managers**.

Return the result table in **any order**.

---

## 🧩 Approach

- Use a **self-join** on the `Employee` table.
- Treat:
  - `E1` as the **manager**
  - `E2` as the **employee**
- Match employees to managers using `managerId`.
- Filter cases where the **employee’s salary is greater** than their manager’s salary.

---

## 🧪 SQL Solution

```sql
SELECT 
    E2.name AS Employee
FROM Employee E1
JOIN Employee E2
    ON E1.id = E2.managerId
WHERE E1.salary < E2.salary;
