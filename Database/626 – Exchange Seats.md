# 💺 LeetCode 626 – Exchange Seats

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Seat**

| Column Name | Type |
|------------|------|
| id         | int |
| student    | varchar |

`id` is the primary key.  

---

## 📝 Task

Write a SQL query to **swap students in adjacent seats**:  
- Even-numbered seats swap with the previous odd-numbered seat  
- Odd-numbered seats swap with the next even-numbered seat  

Return the updated seating arrangement.

---

## 🧩 Approach

- Use **self-joins** to pair adjacent seats
- Swap students where `MOD(ID,2) = 0`
- Use a **CTE (WITH TEMPTABLE)** to store swapped pairs
- Include any remaining seats that were not swapped

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS
(SELECT S1.ID, S2.STUDENT
FROM SEAT S1 JOIN SEAT S2
ON S1.ID = S2.ID + 1
WHERE MOD(S1.ID,2) = 0
UNION
SELECT S1.ID, S2.STUDENT
FROM SEAT S1 JOIN SEAT S2
ON S2.ID = S1.ID + 1
WHERE MOD(S2.ID,2) = 0)
SELECT ID, STUDENT FROM TEMPTABLE
UNION
SELECT ID, STUDENT FROM SEAT
WHERE ID NOT IN (
    SELECT S1.ID
    FROM SEAT S1 JOIN SEAT S2
    ON S1.ID = S2.ID + 1
    WHERE MOD(S1.ID,2) = 0
    UNION
    SELECT S1.ID
    FROM SEAT S1 JOIN SEAT S2
    ON S2.ID = S1.ID + 1
    WHERE MOD(S2.ID,2) = 0
);
