# 🧠 LeetCode 3716 – Find Churn Risk Customers

**Difficulty:** Medium  
**Category:** SQL / Analytics / CTE  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **SUBSCRIPTION_EVENTS**

| Column Name     | Type    |
|-----------------|---------|
| USER_ID         | int     |
| EVENT_DATE      | date    |
| EVENT_TYPE      | varchar |
| PLAN_NAME       | varchar |
| MONTHLY_AMOUNT  | number  |

A **churn risk customer** is defined as a subscriber who:

1. Has been a subscriber for **at least 60 days**.  
2. Has **downgraded their subscription** at least once.  
3. Currently pays **less than 50% of their historical maximum monthly amount**.

---

### 🧩 Approach

1. Compute **subscription duration** for each user:
   - `DAYS_AS_SUBSCRIBER = MAX(EVENT_DATE) - MIN(EVENT_DATE)`  
   - Filter users with at least 60 days.
2. Identify users who have **downgraded**.
3. Find **maximum historical monthly amount** for each user.
4. Join all these tables to get:
   - `CURRENT_PLAN`, `CURRENT_MONTHLY_AMOUNT`  
   - `MAX_HISTORICAL_AMOUNT`, `DAYS_AS_SUBSCRIBER`
5. Filter users with **current monthly amount < 50% of max historical amount**.  
6. Order by `DAYS_AS_SUBSCRIBER DESC` and `USER_ID`.

---

### 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT USER_ID, MAX(EVENT_DATE) AS MAXDATE, MIN(EVENT_DATE) AS MINDATE, 
    MAX(EVENT_DATE) - MIN(EVENT_DATE) AS DAYS_AS_SUBSCRIBER FROM SUBSCRIPTION_EVENTS
    GROUP BY USER_ID
    HAVING MAX(EVENT_DATE) - MIN(EVENT_DATE) >= 60;
), DOWNGRADETABLE AS (
    SELECT USER_ID FROM SUBSCRIPTION_EVENTS
    WHERE EVENT_TYPE = 'downgrade'
    GROUP BY USER_ID
), MAXAMOUNT AS (
    SELECT USER_ID, MAX(MONTHLY_AMOUNT) AS MAX_HISTORICAL_AMOUNT
    FROM SUBSCRIPTION_EVENTS
    GROUP BY USER_ID
)
SELECT S.USER_ID, S.PLAN_NAME AS CURRENT_PLAN, S.MONTHLY_AMOUNT AS CURRENT_MONTHLY_AMOUNT,
M.MAX_HISTORICAL_AMOUNT AS MAX_HISTORICAL_AMOUNT, T.DAYS_AS_SUBSCRIBER AS DAYS_AS_SUBSCRIBER
FROM SUBSCRIPTION_EVENTS S JOIN TEMPTABLE T
ON S.USER_ID = T.USER_ID AND S.EVENT_DATE = T.MAXDATE
JOIN DOWNGRADETABLE D ON D.USER_ID = S.USER_ID
JOIN MAXAMOUNT M ON M.USER_ID = S.USER_ID
WHERE MONTHLY_AMOUNT > 0
AND S.MONTHLY_AMOUNT < M.MAX_HISTORICAL_AMOUNT * 0.5
ORDER BY DAYS_AS_SUBSCRIBER DESC, USER_ID;
