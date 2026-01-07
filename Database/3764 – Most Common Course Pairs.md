# 🧠 LeetCode 3764 – Most Common Course Pairs

**Difficulty:** Medium  
**Category:** SQL / Analytics / Window Functions  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **COURSE_COMPLETIONS**

| Column Name     | Type    |
|-----------------|---------|
| USER_ID         | int     |
| COURSE_NAME     | varchar |
| COMPLETION_DATE | date    |
| COURSE_RATING   | number  |

You are asked to find the **most common consecutive course pairs** taken by users.  
Only consider users who have:

1. Completed **at least 5 courses**.  
2. Have an **average course rating ≥ 4**.

---

### 🧩 Approach

1. Identify **qualified users** using a `QUALIFIER` CTE:
   - Users with ≥5 courses and average rating ≥4.
2. For each qualified user, create a **consecutive course pair**:
   - Use `LEAD()` over `USER_ID` and `COMPLETION_DATE` to get the next course.
3. Filter out rows where the second course is `NULL` (no consecutive pair).
4. Group by `(FIRST_COURSE, SECOND_COURSE)` to get **transition counts**.
5. Order results by:
   - `TRANSITION_COUNT DESC`  
   - Alphabetically by `FIRST_COURSE` and `SECOND_COURSE` in case of ties.

---

### 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH QUALIFIER AS (
    SELECT USER_ID, COUNT(*) AS CNT, AVG(COURSE_RATING) AS CR
    FROM COURSE_COMPLETIONS
    GROUP BY USER_ID
    HAVING COUNT(*) >= 5 AND AVG(COURSE_RATING) >= 4
), TEMPTABLE AS (
    SELECT COURSE_NAME AS FIRST_COURSE, 
           LEAD(COURSE_NAME) OVER (PARTITION BY USER_ID ORDER BY USER_ID, COMPLETION_DATE) AS SECOND_COURSE 
    FROM COURSE_COMPLETIONS 
    WHERE USER_ID IN (SELECT USER_ID FROM QUALIFIER)
    ORDER BY USER_ID, COMPLETION_DATE
)
SELECT FIRST_COURSE, SECOND_COURSE, COUNT(*) AS TRANSITION_COUNT 
FROM TEMPTABLE
WHERE SECOND_COURSE IS NOT NULL
GROUP BY FIRST_COURSE, SECOND_COURSE
ORDER BY TRANSITION_COUNT DESC, LOWER(FIRST_COURSE), LOWER(SECOND_COURSE);
