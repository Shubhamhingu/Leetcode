# ✍️ LeetCode 3374 – First Letter Capitalization II

**Difficulty:** Easy  
**Category:** SQL / String Functions  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **User_Content**

| Column Name    | Type |
|---------------|------|
| content_id    | int  |
| content_text  | varchar |

Each row contains a piece of user-generated text.

---

### 📝 Task

For each row, return:
- `content_id`
- the original text as `original_text`
- the text with the **first letter of each word capitalized** as `converted_text`

---

## 🧩 Approach

- Use Oracle’s built-in `INITCAP()` function.
- `INITCAP()` converts the first letter of each word to uppercase and the remaining letters to lowercase.
- No additional logic or joins are required.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT CONTENT_ID,
       CONTENT_TEXT AS ORIGINAL_TEXT,
       INITCAP(CONTENT_TEXT) AS CONVERTED_TEXT
FROM USER_CONTENT;
