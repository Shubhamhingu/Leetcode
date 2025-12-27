# 🧠 LeetCode 185 – Department Top Three Salaries

**Difficulty:** Hard  
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

Write a SQL query to find the **top three salaries in each department**.  
Return the result table in **any order**.

---

## 🧩 Approach

- Use a **CTE (Common Table Expression)** to simplify the logic.
- Apply `DENSE_RANK()` partitioned by `departmentId` to rank salaries **within each department**.
- Use `DENSE_RANK` to:
  - Handle **duplicate salaries**
  - Avoid gaps in ranking
- Filter records where `RANKING <= 3`.
- Join with `Department` to retrieve department names.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS(
SELECT DEPARTMENTID, SALARY, NAME, 
DENSE_RANK() OVER (PARTITION BY DEPARTMENTID ORDER BY SALARY DESC) AS RANKING
FROM EMPLOYEE)
SELECT D.NAME AS DEPARTMENT, T.NAME AS EMPLOYEE, T.SALARY AS SALARY
FROM TEMPTABLE T JOIN DEPARTMENT D
ON D.ID = T.DEPARTMENTID
WHERE RANKING <= 3;
