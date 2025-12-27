# 🏟️ LeetCode 601 – Human Traffic of Stadium

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Stadium**

| Column Name | Type |
|-------------|------|
| id          | int |
| visit_date  | date |
| people      | int |

`id` is the primary key for this table.  
Each row contains the number of people who visited the stadium on a given day.

---

## 📝 Task

Write a SQL query to display the records with **three or more consecutive days**
where the **number of people is at least 100** on each day.

Return the result ordered by `visit_date`.

---

## 🧩 Approach

- Use **self-joins** to find three consecutive rows based on `id`
- Check that all three days have `people >= 100`
- Use `UNION` to include all rows that are part of a valid 3-day window
- Format dates for consistent output

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT T1.ID, TO_CHAR(T1.VISIT_DATE,'YYYY-MM-DD') AS VISIT_DATE, T1.PEOPLE
FROM STADIUM T1 JOIN STADIUM T2
ON T2.ID = T1.ID + 1
JOIN STADIUM T3
ON T3.ID = T2.ID + 1
WHERE T1.PEOPLE >= 100
AND T2.PEOPLE >= 100
AND T3.PEOPLE >= 100
UNION
SELECT T2.ID, TO_CHAR(T2.VISIT_DATE,'YYYY-MM-DD'), T2.PEOPLE
FROM STADIUM T1 JOIN STADIUM T2
ON T2.ID = T1.ID + 1
JOIN STADIUM T3
ON T3.ID = T2.ID + 1
WHERE T1.PEOPLE >= 100
AND T2.PEOPLE >= 100
AND T3.PEOPLE >= 100
UNION
SELECT T3.ID, TO_CHAR(T3.VISIT_DATE,'YYYY-MM-DD'), T3.PEOPLE
FROM STADIUM T1 JOIN STADIUM T2
ON T2.ID = T1.ID + 1
JOIN STADIUM T3
ON T3.ID = T2.ID + 1
WHERE T1.PEOPLE >= 100
AND T2.PEOPLE >= 100
AND T3.PEOPLE >= 100;
