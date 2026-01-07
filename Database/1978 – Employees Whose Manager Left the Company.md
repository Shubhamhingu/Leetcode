# 🧠 LeetCode 1978 – Employees Whose Manager Left the Company

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
| manager_id  | int  |
| salary      | int  |

- `employee_id` is the primary key.
- `manager_id` refers to another employee’s `employee_id`.
- Some managers may no longer exist in the table.

---

### 📝 Task

Write a SQL query to find the **employee IDs** of employees who:

- Have a **salary less than 30000**
- Whose **manager has left the company** (i.e., `manager_id` does not exist in the Employees table)

Return the result ordered by `employee_id`.

---

## 🧩 Approach

- Filter employees with `salary < 30000`.
- Use a subquery to check managers who are **not present** in the Employees table.
- Order the final result by `employee_id`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT EMPLOYEE_ID
FROM EMPLOYEES
WHERE SALARY < 30000
AND MANAGER_ID NOT IN (SELECT EMPLOYEE_ID FROM EMPLOYEES)
ORDER BY EMPLOYEE_ID;
