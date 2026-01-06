# 🧠 LeetCode 1873 – Calculate Special Bonus

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
| salary     | int     |

- `employee_id` is the primary key.
- Each employee has a `name` and `salary`.

---

### 📝 Task

Write a SQL query to calculate a **special bonus** for each employee:

- Bonus = `salary` if:
  - `employee_id` is **odd**
  - `name` **does not start with 'M'**
- Otherwise, Bonus = 0

Return results ordered by `employee_id`.

---

## 🧩 Approach

- Use a `CASE` statement to handle the conditions:
  - `MOD(employee_id, 2) <> 0` for odd IDs
  - `NAME NOT LIKE 'M%'` for names not starting with 'M'
- Use `ORDER BY` to sort results by `employee_id`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
Select Employee_ID,
CASE
WHEN
MOD(Employee_ID,2)<>0
AND NAME NOT LIKE 'M%'
THEN SALARY
ELSE 0
END Bonus
FROM Employees
ORDER BY EMPLOYEE_ID;
