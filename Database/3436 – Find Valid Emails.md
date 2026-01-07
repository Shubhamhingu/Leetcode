# 📧 LeetCode 3436 – Find Valid Emails

**Difficulty:** Easy  
**Category:** SQL / Regular Expressions  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Users**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| email      | varchar |

---

### 📝 Task

Find all users whose **email addresses are valid** based on the following rules:

- Username contains **only letters and digits**
- Domain contains **only letters**
- Email must end with **`.com`**
- Format: `username@domain.com`

Return:
- `user_id`
- `email`

---

## 🧩 Approach

- Use `REGEXP_LIKE` to validate the email format
- Apply a regular expression that strictly enforces:
  - Alphanumeric username
  - Alphabet-only domain
  - `.com` suffix

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT USER_ID, EMAIL
FROM USERS
WHERE REGEXP_LIKE(EMAIL, '^[A-Za-z0-9]+@[A-Za-z]+\.com$');
