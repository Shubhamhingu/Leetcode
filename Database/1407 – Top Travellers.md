# 🧳 LeetCode 1407 – Top Travellers

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |

Table: **Rides**

| Column Name | Type |
|------------|------|
| id         | int  |
| user_id    | int  |
| distance   | int  |

---

## 📝 Task

For each user, calculate the **total distance traveled**:

- If a user has no rides, their traveled distance should be `0`
- Sort results by:
  1. `travelled_distance` **descending**
  2. `name` **ascending**

Return:

- `NAME`
- `TRAVELLED_DISTANCE`

---

## 🧩 Approach

1. Perform a **LEFT JOIN** from `Users` to `Rides` so users with no rides are included
2. Use `SUM(distance)` to calculate total travel per user
3. Use `NVL` to convert `NULL` sums into `0`
4. Apply required sorting

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT US.NAME,
       NVL(SUM(RI.DISTANCE), 0) AS TRAVELLED_DISTANCE
FROM USERS US
LEFT JOIN RIDES RI
ON US.ID = RI.USER_ID
GROUP BY US.ID, US.NAME
ORDER BY TRAVELLED_DISTANCE DESC, US.NAME ASC;
