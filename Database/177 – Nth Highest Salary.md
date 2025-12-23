# 🧠 LeetCode 177 – Nth Highest Salary

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

---

### 📝 Task

Write a SQL function `getNthHighestSalary(N)` that returns the **Nth highest distinct salary** from the `Employee` table.  
If there is no Nth highest salary, return **NULL**.

---

## 🧩 Approach

- Use a **window function (`DENSE_RANK`)** to rank salaries in descending order.
- `DENSE_RANK` ensures:
  - Duplicate salaries receive the **same rank**
  - No rank gaps occur
- Filter the result where `RANKING = N`.
- Use `SELECT INTO` inside a **PL/SQL function** to return the value.

---

## 🧪 SQL Solution (PL/SQL)

```sql
CREATE FUNCTION getNthHighestSalary(N IN NUMBER)
RETURN NUMBER IS
    result NUMBER;
BEGIN
    WITH TempTable AS (
        SELECT 
            DENSE_RANK() OVER (ORDER BY salary DESC) AS ranking,
            salary
        FROM Employee
    )
    SELECT DISTINCT salary
    INTO result
    FROM TempTable
    WHERE ranking = N;

    RETURN result;
END;
