# 🧠 LeetCode 550 – Game Play Analysis IV

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Activity**

| Column Name | Type |
|------------|------|
| player_id  | int  |
| device_id  | int  |
| event_date | date |
| games_played | int |

There is no primary key for this table.

---

### 📝 Task

Write a SQL query to report the **fraction of players** who logged in again on the **day after their first login**.

- Round the result to **2 decimal places**.

---

## 🧩 Approach

- Identify each player’s **first login date**.
- Count how many players logged in **exactly one day after** their first login (numerator).
- Count the **total number of distinct players** (denominator).
- Divide numerator by denominator to get the fraction.
- Use **CTEs** to break the logic into readable steps.

---

## 🧪 SQL Solution

```sql
WITH FIRSTLOGIN AS (
    SELECT PLAYER_ID, MIN(EVENT_DATE) AS EVENT_DATE
    FROM ACTIVITY
    GROUP BY PLAYER_ID
), NUMERATOR AS (
    SELECT COUNT(A.PLAYER_ID) NUM
    FROM ACTIVITY A JOIN FIRSTLOGIN F
    ON A.EVENT_DATE = F.EVENT_DATE + 1
    AND A.PLAYER_ID = F.PLAYER_ID
), DENOMINATOR AS (
    SELECT COUNT(DISTINCT(PLAYER_ID)) AS DEN FROM ACTIVITY
)
SELECT ROUND(NUM/DEN,2) AS FRACTION FROM NUMERATOR,DENOMINATOR;
