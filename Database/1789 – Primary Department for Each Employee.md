# 🧠 LeetCode 1789 – Primary Department for Each Employee

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employee**

| Column Name    | Type    |
|---------------|---------|
| employee_id   | int     |
| department_id | int     |
| primary_flag  | char(1) |

- `employee_id` is the primary key.
- `primary_flag` indicates whether this department is the employee's primary department (`'Y'` or `'N'`).
- An employee can belong to **one or more departments**.

---

### 📝 Task

Write a SQL query to return **the primary department for each employee**:

- If `PRIMARY_FLAG = 'Y'`, select that department.
- If an employee belongs to **only one department**, select that department.
- Return unique `(employee_id, department_id)` pairs.

---

## 🧩 Approach

- First, select all records where `PRIMARY_FLAG = 'Y'`.
- Then, handle employees with only **one department**.
- Combine results using `UNION` to remove duplicates.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT EMPLOYEE_ID,DEPARTMENT_ID
FROM EMPLOYEE
WHERE PRIMARY_FLAG = 'Y'
UNION
SELECT E.EMPLOYEE_ID, E.DEPARTMENT_ID
FROM EMPLOYEE E JOIN 
(SELECT EMPLOYEE_ID,COUNT(EMPLOYEE_ID) AS CNT
FROM EMPLOYEE
GROUP BY EMPLOYEE_ID HAVING COUNT(EMPLOYEE_ID) = 1) T
ON E.EMPLOYEE_ID = T.EMPLOYEE_ID;
