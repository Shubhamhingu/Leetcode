# 🧠 LeetCode 577 – Employee Bonus

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employee**

| Column Name | Type |
|------------|------|
| empId      | int  |
| name       | varchar |
| supervisor | int |
| salary     | int |

`empId` is the primary key for this table.

---

Table: **Bonus**

| Column Name | Type |
|------------|------|
| empId      | int  |
| bonus      | int |

`empId` is a foreign key referencing `Employee(empId)`.

---

### 📝 Task

Write a SQL query to report the **name and bonus amount** of employees  
whose bonus is **less than 1000**.  
Employees without a bonus should also be included.

Return the result table in **any order**.

---

## 🧩 Approach

- Use a **LEFT JOIN** to include all employees.
- Join the `Bonus` table to retrieve bonus values.
- Filter rows where:
  - Bonus is **less than 1000**, or
  - Bonus is **NULL** (no bonus record exists)

---

## 🧪 SQL Solution

```sql
# Write your MySQL query statement below
SELECT E.NAME as name,B.BONUS as bonus FROM EMPLOYEE E LEFT JOIN BONUS B ON E.EMPID=B.EMPID WHERE B.BONUS<1000 OR B.BONUS IS NULL;
