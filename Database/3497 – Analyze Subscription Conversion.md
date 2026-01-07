# 📊 LeetCode 3497 – Analyze Subscription Conversion

**Difficulty:** Medium  
**Category:** SQL / Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **UserActivity**

| Column Name       | Type    |
|------------------|---------|
| user_id           | int     |
| activity_type     | varchar |
| activity_duration | number  |

- `activity_type` can be `"free_trial"` or `"paid"`.
- `activity_duration` records the duration of each activity in minutes.

---

### 📝 Task

For each user who has **both free trial and paid activities**, report:

1. `TRIAL_AVG_DURATION` – the average duration of free trial activities.  
2. `PAID_AVG_DURATION` – the average duration of paid activities.

---

## 🧩 Approach

- Use two **CTEs** to calculate the average duration per user for each activity type (`free_trial` and `paid`).  
- Join the two CTEs on `USER_ID` to get a consolidated view of trial vs paid activity per user.  
- Use `ROUND` to format averages to 2 decimal places.  

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TRTAB AS (
    SELECT USER_ID, ROUND(AVG(ACTIVITY_DURATION),2) AS TRIAL_AVG_DURATION
    FROM USERACTIVITY
    WHERE ACTIVITY_TYPE = 'free_trial'
    GROUP BY USER_ID
),
PATAB AS (
    SELECT USER_ID, ROUND(AVG(ACTIVITY_DURATION),2) AS PAID_AVG_DURATION
    FROM USERACTIVITY
    WHERE ACTIVITY_TYPE = 'paid'
    GROUP BY USER_ID
)
SELECT P.USER_ID, T.TRIAL_AVG_DURATION, P.PAID_AVG_DURATION
FROM PATAB P JOIN TRTAB T
ON P.USER_ID = T.USER_ID
ORDER BY USER_ID;
