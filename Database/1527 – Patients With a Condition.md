# 🧠 LeetCode 1527 – Patients With a Condition

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Patients**

| Column Name | Type    |
|------------|---------|
| patient_id | int     |
| patient_name | varchar |
| conditions | varchar |

`patient_id` is the primary key for this table.

---

### 📝 Task

Write a SQL query to report all patients who have **Type I Diabetes**, which is represented by the condition code **DIAB1**.

- The condition may appear at the **start** of the `conditions` string.
- Or it may appear **after a space** if there are multiple conditions listed.

---

## 🧩 Approach

- Use the `LIKE` operator to match:
  - `DIAB1` at the beginning of the string.
  - `DIAB1` appearing after a space.
- This ensures accurate detection without matching partial words.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT * FROM PATIENTS WHERE CONDITIONS LIKE 'DIAB1%' OR CONDITIONS LIKE '% DIAB1%';
