# 🧠 LeetCode 180 – Consecutive Numbers

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Logs**

| Column Name | Type |
|------------|------|
| id         | int  |
| num        | int  |

`id` is the primary key for this table and increases sequentially.

---

### 📝 Task

Write a SQL query to find **all numbers that appear at least three times consecutively**.

Return the result table in **any order**.

---

## 🧩 Approach

- Use **self-joins** to compare three consecutive rows.
- Join the table:
  - `T1` → current row
  - `T2` → next row (`id + 1`)
  - `T3` → third row (`id + 2`)
- Ensure:
  - The `num` value is the **same across all three rows**
- Use `DISTINCT` to avoid duplicate results.

---

## 🧪 SQL Solution

```sql
SELECT DISTINCT T3.num AS ConsecutiveNums
FROM Logs T1
JOIN Logs T2
    ON T2.id = T1.id + 1
JOIN Logs T3
    ON T3.id = T2.id + 1
WHERE T1.num = T2.num
  AND T2.num = T3.num;
