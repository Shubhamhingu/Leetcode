# 🚌 LeetCode 1204 – Last Person to Fit in the Bus

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Queue**

| Column Name | Type |
|------------|------|
| person_name | varchar |
| weight      | int   |
| turn        | int   |

- People board a bus **in order of `turn`**
- The bus can hold a total weight of **1000**
- Find the **last person who can fit** in the bus without exceeding the limit

---

## 📝 Task

Return the **person_name** of the last person whose inclusion keeps the total weight ≤ 1000.

---

## 🧩 Approach

1. Use a **window function (`SUM() OVER`)** to calculate **cumulative weight** as people board  
2. Filter to include only rows where **cumulative weight ≤ 1000**  
3. Select the person with the **largest cumulative weight** (last to fit)  
4. Use `ROWNUM = 1` to pick the last person

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS(
    SELECT PERSON_NAME, WEIGHT, SUM(WEIGHT) OVER (ORDER BY TURN) AS TOT_WEIGHTS
    FROM QUEUE
), TEMPTABLE2 AS
(SELECT PERSON_NAME, WEIGHT, TOT_WEIGHTS 
 FROM TEMPTABLE
 WHERE TOT_WEIGHTS <= 1000 
 ORDER BY TOT_WEIGHTS DESC)
SELECT PERSON_NAME 
FROM TEMPTABLE2
WHERE ROWNUM = 1;
