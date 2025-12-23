# 🧠 LeetCode 178 – Rank Scores

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Scores**

| Column Name | Type |
|------------|------|
| id         | int  |
| score      | decimal |

`id` is the primary key for this table.

---

### 📝 Task

Write a SQL query to **rank the scores** in descending order.  
The ranking should:
- Be **dense**
- Not have gaps between ranks
- Assign the same rank to **duplicate scores**

---

## 🧩 Approach

- Use the **`DENSE_RANK()` window function**.
- Order scores in **descending order** so higher scores get better ranks.
- `DENSE_RANK` ensures:
  - Equal scores share the same rank
  - No rank numbers are skipped

---

## 🧪 SQL Solution

```sql
SELECT 
    score,
    DENSE_RANK() OVER (ORDER BY score DESC) AS rank
FROM Scores;
