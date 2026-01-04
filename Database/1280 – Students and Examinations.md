# 🎓 LeetCode 1280 – Students and Examinations

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**Students**

| Column Name   | Type |
|---------------|------|
| student_id    | int  |
| student_name  | varchar |

**Subjects**

| Column Name   | Type |
|---------------|------|
| subject_name  | varchar |

**Examinations**

| Column Name   | Type |
|---------------|------|
| student_id    | int  |
| subject_name  | varchar |

---

## 📝 Task

For **each student** and **each subject**, report:

- `student_id`  
- `student_name`  
- `subject_name`  
- `attended_exams`: number of times the student attended that subject's exam (0 if none)  

Order results by `student_id` and `subject_name`.

---

## 🧩 Approach

1. **CROSS JOIN** Students × Subjects to generate all possible student-subject combinations  
2. **LEFT JOIN** Examinations to count attended exams  
3. Use `NVL(...,0)` for subjects with no attended exams  
4. Group by student and subject for aggregation

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */ 
SELECT ST.STUDENT_ID, ST.STUDENT_NAME, SU.SUBJECT_NAME, NVL(COUNT(EX.SUBJECT_NAME),0) AS ATTENDED_EXAMS
FROM STUDENTS ST CROSS JOIN SUBJECTS SU
LEFT JOIN EXAMINATIONS EX
ON ST.STUDENT_ID = EX.STUDENT_ID
AND SU.SUBJECT_NAME = EX.SUBJECT_NAME
GROUP BY ST.STUDENT_ID, ST.STUDENT_NAME, SU.SUBJECT_NAME
ORDER BY ST.STUDENT_ID, SU.SUBJECT_NAME;
