# 🧠 LeetCode 1693 – Daily Leads and Partners

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **DailySales**

| Column Name | Type    |
|------------|---------|
| date_id    | date    |
| make_name  | varchar |
| lead_id    | int     |
| partner_id | int     |

Each row represents a sales record for a specific **date** and **car make**.

---

### 📝 Task

Write a SQL query to report for each **date** and **make**:

- Number of **unique leads**
- Number of **unique partners**

Format the `date_id` as `YYYY-MM-DD`.

---

## 🧩 Approach

- Group records by `date_id` and `make_name`.
- Use `COUNT(DISTINCT ...)` to calculate unique leads and partners.
- Format the date using `TO_CHAR`.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT TO_CHAR(DATE_ID,'YYYY-MM-DD') AS DATE_ID, 
MAKE_NAME, 
COUNT(DISTINCT(LEAD_ID)) AS UNIQUE_LEADS,
COUNT(DISTINCT(PARTNER_ID)) AS UNIQUE_PARTNERS
FROM DAILYSALES
GROUP BY DATE_ID,MAKE_NAME;
