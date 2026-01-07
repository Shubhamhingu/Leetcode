# 🧪 LeetCode 3586 – Find COVID Recovery Patients

**Difficulty:** Medium  
**Category:** SQL / CTEs / Date Calculations  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:

**Patients**

| Column Name  | Type    |
|-------------|---------|
| patient_id   | int     |
| patient_name | varchar |
| age          | int     |

**COVID_Tests**

| Column Name | Type    |
|------------|---------|
| patient_id  | int     |
| test_date   | date    |
| result      | varchar | (either 'Positive' or 'Negative') |

- Each patient may have multiple COVID tests over time.  
- A patient is considered **recovered** once a negative test occurs **after** a positive test.

---

### 📝 Task

For each patient who had a positive test followed by a negative test:

- Find the **earliest positive test** (`MIN(TEST_DATE)` where `RESULT='Positive'`).  
- Find the **earliest negative test after that positive test**.  
- Calculate **recovery time** as the difference in days between the two tests.  

Return columns:

- `PATIENT_ID`  
- `PATIENT_NAME`  
- `AGE`  
- `RECOVERY_TIME` (days)  

Order by `RECOVERY_TIME` ascending, then `PATIENT_NAME`.

---

## 🧩 Approach

1. Use a CTE `POSTABLE` to get the **first positive test** for each patient.  
2. Use a CTE `NEGTABLE` to get all negative tests.  
3. Join positive and negative tests on `PATIENT_ID` and filter only negative tests **after the positive test**.  
4. Compute `RECOVERY_TIME = MIN(N.TEST_DATE - P.TEST_DATE)` per patient.  
5. Join with `PATIENTS` to get names and ages.  
6. Group and order as required.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH POSTABLE AS (
    SELECT PATIENT_ID, MIN(TEST_DATE) AS TEST_DATE FROM COVID_TESTS
    WHERE RESULT = 'Positive'
    GROUP BY PATIENT_ID;
), NEGTABLE AS (
    SELECT 
        PATIENT_ID, TEST_DATE
    FROM COVID_TESTS
    WHERE RESULT = 'Negative'
)
SELECT P.PATIENT_ID, PA.PATIENT_NAME, PA.AGE, MIN(N.TEST_DATE - P.TEST_DATE) AS RECOVERY_TIME
FROM POSTABLE P JOIN NEGTABLE N
ON P.PATIENT_ID = N.PATIENT_ID
JOIN PATIENTS PA ON PA.PATIENT_ID = P.PATIENT_ID
WHERE N.TEST_DATE > P.TEST_DATE
GROUP BY P.PATIENT_ID, PA.PATIENT_NAME, PA.AGE
ORDER BY RECOVERY_TIME, PATIENT_NAME;
