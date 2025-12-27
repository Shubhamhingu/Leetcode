# 🧑‍💼 LeetCode 607 – Sales Person

**Difficulty:** Easy  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables involved: **SalesPerson**, **Company**, **Orders**

### SalesPerson
| Column Name | Type |
|------------|------|
| sales_id   | int |
| name       | varchar |
| salary     | int |
| commission_rate | int |
| hire_date  | date |

### Company
| Column Name | Type |
|------------|------|
| com_id     | int |
| name       | varchar |
| city       | varchar |

### Orders
| Column Name | Type |
|------------|------|
| order_id   | int |
| order_date | date |
| com_id     | int |
| sales_id   | int |
| amount     | int |

---

## 📝 Task

Write a SQL query to find the **names of all salespersons** who **did not have any orders related to the company named `'RED'`**.

---

## 🧩 Approach

- Identify all `sales_id` values that appear in orders associated with company `'RED'`
- Exclude those `sales_id` values using `NOT IN`
- Return remaining salesperson names

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT NAME FROM SALESPERSON WHERE SALES_ID NOT IN
(SELECT O.SALES_ID T_SALES_ID FROM COMPANY C JOIN ORDERS O ON C.COM_ID = O.COM_ID WHERE C.NAME = 'RED');
