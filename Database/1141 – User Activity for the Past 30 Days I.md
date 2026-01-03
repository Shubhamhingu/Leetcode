# 📅 LeetCode 1141 – User Activity for the Past 30 Days I

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Activity**

| Column Name   | Type |
|--------------|------|
| user_id      | int  |
| session_id   | int  |
| activity_date| date |
| activity_type| enum |

---

## 📝 Task

Find the **daily active user count** for the **past 30 days ending on 2019-07-27** (inclusive).

- A user is considered active if they performed **any activity** on a given day.
- Return results ordered by date.

---

## 🧩 Approach

- Filter records within the **last 30 days** from `2019-07-27`
- Group data by `activity_date`
- Count **distinct users per day**
- Format the date as `YYYY-MM-DD`

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT 
    TO_CHAR(ACTIVITY_DATE, 'YYYY-MM-DD') AS DAY,
    COUNT(DISTINCT USER_ID) AS ACTIVE_USERS
FROM ACTIVITY
WHERE ACTIVITY_DATE <= TO_DATE('2019-07-27')
  AND ACTIVITY_DATE > TO_DATE('2019-07-27') - 30
GROUP BY ACTIVITY_DATE
ORDER BY DAY;
