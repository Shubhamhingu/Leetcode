# 🧠 LeetCode 1965 – Employees With Missing Information

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Employees**

| Column Name  | Type |
|-------------|------|
| employee_id | int  |
| name        | varchar |

---

Table: **Salaries**

| Column Name  | Type |
|-------------|------|
| employee_id | int  |
| salary      | int  |

- `employee_id` is the primary key in both tables.
- Some employees may be missing from one of the tables.

---

### 📝 Task

Write a SQL query to find the **employee IDs that are missing information**, meaning:

- The employee exists in **only one** of the two tables  
- Either missing from `Employees` **or** missing from `Salaries`

Return the result ordered by `employee_id`.

---

## 🧩 Approach

- First, get all employee IDs appearing in **either** table using `UNION`.
- Then, remove employee IDs that appear in **both** tables using an inner join.
- The remaining IDs represent employees with missing information.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT EMPLOYEE_ID FROM
(SELECT EMPLOYEE_ID FROM EMPLOYEES UNION SELECT EMPLOYEE_ID FROM SALARIES)
WHERE EMPLOYEE_ID NOT IN 
(SELECT E.EMPLOYEE_ID
FROM EMPLOYEES E JOIN SALARIES S
ON E.EMPLOYEE_ID = S.EMPLOYEE_ID);
