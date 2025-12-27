# 🔢 LeetCode 619 – Biggest Single Number

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **MyNumbers**

| Column Name | Type |
|------------|------|
| num        | int |

---

## 📝 Task

Find the **largest number** that appears **exactly once** in the table.  
If no such number exists, return `NULL`.

---

## 🧩 Approach

- Group numbers and count their occurrences
- Filter numbers appearing **exactly once**
- Order numbers in descending order
- Use `ROWNUM = 1` to select the largest
- `COALESCE` ensures `NULL` is returned if no number satisfies the condition

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT COALESCE ((SELECT NUM FROM (SELECT NUM,COUNT(NUM) CN FROM MYNUMBERS GROUP BY NUM ORDER BY NUM DESC)
WHERE CN=1 AND ROWNUM<=1),NULL) AS NUM FROM DUAL;
