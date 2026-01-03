# 📰 LeetCode 1148 – Article Views I

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Views**

| Column Name | Type |
|------------|------|
| article_id | int  |
| author_id  | int  |
| viewer_id  | int  |
| view_date  | date |

---

## 📝 Task

Find all **authors who viewed at least one of their own articles**.

- An author views their own article when `author_id = viewer_id`
- Return the result ordered by author id

---

## 🧩 Approach

- Filter rows where `AUTHOR_ID = VIEWER_ID`
- Use `DISTINCT` to avoid duplicates
- Sort the output by `AUTHOR_ID`

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT DISTINCT AUTHOR_ID AS ID
FROM VIEWS
WHERE AUTHOR_ID = VIEWER_ID
ORDER BY AUTHOR_ID;
