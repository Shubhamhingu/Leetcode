# 📈 LeetCode 3421 – Find Students Who Improved

**Difficulty:** Medium  
**Category:** SQL / Window Functions  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Scores**

| Column Name | Type |
|------------|------|
| student_id | int  |
| subject    | varchar |
| score      | int  |
| exam_date  | date |

Each student can take multiple exams per subject on different dates.

---

### 📝 Task

For each **student–subject** pair:
- Compare the **latest exam score** with the **earliest exam score**
- Return only those students whose **latest score is higher than their first score**

Output columns:
- `student_id`
- `subject`
- `first_score`
- `latest_score`

---

## 🧩 Approach

1. **Rank exams by date**
   - Use `DENSE_RANK()` partitioned by `student_id` and `subject`
   - Order by `exam_date DESC`
   - Latest exam gets rank `1`

2. **Identify earliest and latest exams**
   - Minimum rank → latest exam
   - Maximum rank → first exam

3. **Join rankings back to scores**
   - Extract first and latest scores
   - Filter only cases where `latest_score > first_score`

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */

WITH RANKEDSCORES AS (
    SELECT STUDENT_ID,
           SUBJECT,
           SCORE,
           EXAM_DATE,
           DENSE_RANK() OVER (
               PARTITION BY STUDENT_ID, SUBJECT
               ORDER BY EXAM_DATE DESC
           ) AS RANKINGS
    FROM SCORES
),
MINMAXRANKINGS AS (
    SELECT STUDENT_ID,
           SUBJECT,
           MIN(RANKINGS) AS MINRANKINGS,
           MAX(RANKINGS) AS MAXRANKINGS
    FROM RANKEDSCORES
    GROUP BY STUDENT_ID, SUBJECT
)
SELECT R1.STUDENT_ID,
       R1.SUBJECT,
       R2.SCORE AS FIRST_SCORE,
       R1.SCORE AS LATEST_SCORE
FROM MINMAXRANKINGS M
JOIN RANKEDSCORES R1
  ON R1.STUDENT_ID = M.STUDENT_ID
 AND R1.SUBJECT = M.SUBJECT
 AND R1.RANKINGS = M.MINRANKINGS
JOIN RANKEDSCORES R2
  ON R2.STUDENT_ID = M.STUDENT_ID
 AND R2.SUBJECT = M.SUBJECT
 AND R2.RANKINGS = M.MAXRANKINGS
WHERE R1.SCORE > R2.SCORE;
