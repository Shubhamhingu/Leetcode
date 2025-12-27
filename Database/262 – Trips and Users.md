# 🧠 LeetCode 262 – Trips and Users

**Difficulty:** Hard  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Trips**

| Column Name | Type |
|------------|------|
| id         | int  |
| client_id  | int  |
| driver_id  | int  |
| city_id    | int  |
| status     | varchar |
| request_at | date |

---

Table: **Users**

| Column Name | Type |
|------------|------|
| users_id   | int  |
| banned     | varchar |
| role       | varchar |

---

### 📝 Task

Write a SQL query to find the **daily cancellation rate** of trips  
between **2013-10-01** and **2013-10-03**.

Rules:
- Exclude trips where **either the client or the driver is banned**
- Cancellation rate =  
  **(number of cancelled trips) / (total trips)**  
- Round the result to **2 decimal places**

---

## 🧩 Approach

- Join `Trips` with `Users` to validate trip participants.
- Exclude trips involving **banned users** (both clients and drivers).
- Use a `CASE` expression to:
  - Count cancelled trips
  - Ignore completed trips
- Aggregate by `request_at` to compute **daily cancellation rates**.
- Use `ROUND()` to format the result.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT DAY, STATUS AS "CANCELLATION RATE" FROM
(SELECT T1.REQUEST_AT AS DAY,
ROUND(SUM(CASE
    WHEN T1.STATUS LIKE '%completed%' THEN 0
    ELSE 1
END)/COUNT(*),2) AS STATUS
FROM TRIPS T1 JOIN USERS U 
ON U.USERS_ID = T1.CLIENT_ID 
WHERE T1.ID NOT IN (SELECT ID
FROM TRIPS JOIN USERS
ON CLIENT_ID = USERS_ID
AND BANNED = 'Yes'
UNION
SELECT ID
FROM TRIPS JOIN USERS
ON DRIVER_ID = USERS_ID
AND BANNED = 'Yes')
AND T1.REQUEST_AT BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY T1.REQUEST_AT);
