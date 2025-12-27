# 🤝 LeetCode 602 – Friend Requests II: Who Has the Most Friends

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **RequestAccepted**

| Column Name   | Type |
|---------------|------|
| requester_id  | int  |
| accepter_id   | int  |
| accept_date   | date |

This table contains the IDs of users who have accepted friend requests.

---

## 📝 Task

Write a SQL query to find the **user ID** who has the **most friends** and the **number of friends** they have.

> Friendship is **bidirectional**.

---

## 🧩 Approach

- Count how many times a user appears as:
  - `requester_id`
  - `accepter_id`
- Combine both counts using a **FULL OUTER JOIN**
- Use `NVL` to handle missing values
- Sort by total friends in descending order
- Use `ROWNUM = 1` to fetch the top result

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT * FROM
(SELECT NVL(T1.ID, T2.ID) AS ID, NVL(T1.CNT, 0)  + NVL(T2.CNT,0) AS NUM
FROM
(SELECT REQUESTER_ID AS ID, COUNT(ACCEPTER_ID) AS CNT
FROM REQUESTACCEPTED
GROUP BY REQUESTER_ID) T1
FULL OUTER JOIN
(SELECT ACCEPTER_ID AS ID, COUNT(REQUESTER_ID) AS CNT
FROM REQUESTACCEPTED
GROUP BY ACCEPTER_ID) T2
ON T1.ID = T2.ID
ORDER BY NUM DESC
)
WHERE ROWNUM = 1;
