# 🧠 LeetCode 175 – Combine Two Tables

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Person**

| Column Name | Type    |
|------------|---------|
| personId   | int     |
| lastName   | varchar |
| firstName  | varchar |

personId is the primary key for this table.

---

Table: **Address**

| Column Name | Type    |
|------------|---------|
| addressId  | int     |
| personId   | int     |
| city       | varchar |
| state      | varchar |

addressId is the primary key for this table.

---

### 📝 Task

Write a SQL query to report the **first name, last name, city, and state** of each person in the `Person` table.  
If the address of a person does not exist, return **NULL** values.

---

## 🧩 Approach

- Use a **LEFT JOIN** to keep all records from the `Person` table.
- Match records using `personId`.

---

## 🧪 SQL Solution

```sql
SELECT 
    p.firstName,
    p.lastName,
    a.city,
    a.state
FROM Person p
LEFT JOIN Address a
ON p.personId = a.personId;
