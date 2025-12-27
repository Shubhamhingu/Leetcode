# 🧠 LeetCode 511 – Game Play Analysis I

**Difficulty:** Easy  
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
Each row shows the activity of a player on a specific day.

---

### 📝 Task

Write a SQL query to report the **first login date** for each player.

Return the result table in **any order**.

---

## 🧩 Approach

- Group records by `PLAYER_ID`.
- Use `MIN(EVENT_DATE)` to find the **earliest login date**.
- Format the date using `TO_CHAR` to match the required output format.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT PLAYER_ID, TO_CHAR(MIN(EVENT_DATE),'YYYY-MM-DD') AS FIRST_LOGIN FROM ACTIVITY GROUP BY PLAYER_ID;
