# 🧠 LeetCode 1517 – Find Users With Valid E-Mails

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type    |
|------------|---------|
| user_id    | int     |
| name       | varchar |
| mail       | varchar |

`user_id` is the primary key for this table.

---

### 📝 Task

Write a SQL query to find all users who have **valid email addresses**.  

A valid email must:
- Start with a **letter**
- Contain only **letters, digits, underscores, dots, or dashes** before `@`
- End with **@leetcode.com**

---

## 🧩 Approach

- Use `REGEXP_LIKE` to validate the email format.
- Apply a regular expression that strictly matches the required pattern.
- Filter only rows with valid emails.

---

## 🧪 SQL Solution

```sql
/* Write your PL/SQL query statement below */
SELECT USER_ID, NAME, MAIL
FROM USERS
WHERE REGEXP_LIKE(MAIL, '^[A-Za-z][A-Za-z0-9._-]*@leetcode\.com$');
