# 🧠 LeetCode 2356 – Number of Unique Subjects Taught by Each Teacher

**Difficulty:** Easy  
**Category:** SQL / Aggregation  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Teacher**

| Column Name | Type |
|------------|------|
| teacher_id | int  |
| subject_id | int  |
| dept_id    | int  |

- The table may contain duplicate rows.
- Each row indicates that a teacher teaches a subject in a department.

---

### 📝 Task

Write a SQL query to report the **number of unique subjects** each teacher teaches.

Return the result table with:
- `teacher_id`
- Count of **distinct** `subject_id` as `cnt`

---

## 🧩 Approach

- Group records by `teacher_id`.
- Use `COUNT(DISTINCT subject_id)` to ensure duplicate subjects are counted only once per teacher.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT TEACHER_ID,
       COUNT(DISTINCT SUBJECT_ID) AS CNT
FROM TEACHER
GROUP BY TEACHER_ID;
