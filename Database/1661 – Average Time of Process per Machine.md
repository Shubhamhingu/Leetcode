# 🧠 LeetCode 1661 – Average Time of Process per Machine

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Activity**

| Column Name    | Type    |
|---------------|---------|
| machine_id    | int     |
| process_id    | int     |
| activity_type | varchar |
| timestamp     | float   |

The table records the **start** and **end** time of each process on a machine.

- Each process has exactly one `start` and one `end`.
- The same machine can run multiple processes.

---

### 📝 Task

Write a SQL query to find the **average processing time per machine**.

- Processing time for a process = `end.timestamp - start.timestamp`
- Average should be **rounded to 3 decimal places**
- Return results ordered by `machine_id`

---

## 🧩 Approach

- Self-join the `Activity` table to pair `start` and `end` records for the same machine and process.
- Calculate processing time for each process.
- Aggregate by `machine_id` to compute the average processing time.
- Round the result to 3 decimal places.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT MACHINE_ID, ROUND(SUM(PROCESSING_TIME)/COUNT(*),3) AS PROCESSING_TIME
FROM
(SELECT T1.MACHINE_ID,T1.PROCESS_ID, T2.TIMESTAMP - T1.TIMESTAMP AS PROCESSING_TIME
FROM ACTIVITY T1 JOIN ACTIVITY T2
ON T1.MACHINE_ID = T2.MACHINE_ID
AND T1.PROCESS_ID = T2.PROCESS_ID
AND T1.ACTIVITY_TYPE = 'start'
AND T2.ACTIVITY_TYPE = 'end')
GROUP BY MACHINE_ID
ORDER BY MACHINE_ID;
