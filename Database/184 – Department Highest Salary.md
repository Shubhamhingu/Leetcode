# 🧠 LeetCode 184 – Department Highest Salary

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
| salary     | int  |
| departmentId | int |

`id` is the primary key for this table.

---

Table: **Department**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |

`id` is the primary key for this table.

---

### 📝 Task

Write a SQL query to find the **employee(s) who earn the highest salary in each department**.

Return the result table in **any order**.

---

## 🧩 Approach

- First, compute the **maximum salary per department** using `GROUP BY`.
- Join this result back to the `Employee` table to find employees matching that salary.
- Join with the `Department` table to fetch department names.
- This approach correctly handles **multiple employees with the same highest salary**.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT D.NAME AS DEPARTMENT, E.NAME AS EMPLOYEE, T.SALARY AS SALARY
FROM DEPARTMENT D JOIN EMPLOYEE E ON D.ID = E.DEPARTMENTID
JOIN
(SELECT MAX(SALARY) AS SALARY, DEPARTMENTID DID
FROM EMPLOYEE
GROUP BY DEPARTMENTID) T
ON T.DID = E.DEPARTMENTID
WHERE T.SALARY = E.SALARY;
