# 🧠 LeetCode 196 – Delete Duplicate Emails

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Person**

| Column Name | Type |
|------------|------|
| id         | int  |
| email      | varchar |

`id` is the primary key for this table.  
Each row contains an email address. Emails will not be `NULL`.

---

### 📝 Task

Write a SQL query to **delete all duplicate email entries**, keeping **only one record** per email.  
The record with the **smallest `id`** should be retained.

---

## 🧩 Approach

- Group records by `EMAIL`.
- Use `MIN(ID)` to identify the **record to keep** for each email.
- Delete all records whose `ID` is **not** in the retained set.
- This ensures:
  - Exactly one row per email remains
  - Data integrity is preserved

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
DELETE FROM PERSON WHERE ID NOT IN (
    SELECT MIN(ID)
    FROM PERSON
    GROUP BY EMAIL);
