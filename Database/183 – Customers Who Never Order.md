# 🧠 LeetCode 183 – Customers Who Never Order

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Customers**

| Column Name | Type |
|------------|------|
| id         | int  |
| name       | varchar |

`id` is the primary key for this table.

---

Table: **Orders**

| Column Name | Type |
|------------|------|
| id         | int  |
| customerId | int  |

`id` is the primary key for this table.  
`customerId` is a foreign key referencing `Customers(id)`.

---

### 📝 Task

Write a SQL query to find **customers who never placed an order**.

Return the result table in **any order**.

---

## 🧩 Approach

- Use a **subquery** to retrieve all `CustomerID` values from the `Orders` table.
- Filter customers whose `ID` does **not exist** in the subquery result.
- This pattern is commonly known as an **anti-join**.

---

## 🧪 SQL Solution

```sql
SELECT NAME AS CUSTOMERS FROM CUSTOMERS WHERE ID NOT IN (SELECT CUSTOMERID FROM ORDERS);
