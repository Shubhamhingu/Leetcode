# 🛒 LeetCode 3554 – Find Category Recommendation Pairs

**Difficulty:** Hard  
**Category:** SQL / Aggregation / Joins  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Tables:  

**ProductPurchases**

| Column Name | Type |
|------------|------|
| user_id    | int  |
| product_id | int  |

**ProductInfo**

| Column Name | Type    |
|------------|---------|
| product_id | int     |
| category   | varchar |

- `ProductPurchases` tracks which products each user bought.  
- `ProductInfo` provides the category for each product.

---

### 📝 Task

Find **category pairs** `(CATEGORY1, CATEGORY2)` such that:

1. Both categories were purchased by the same user.  
2. At least **3 users** purchased both categories.  
3. Ensure `CATEGORY1 < CATEGORY2` to avoid duplicates.  
4. Report the number of users for each category pair as `CUSTOMER_COUNT`.  

Sort the results by:

- `CUSTOMER_COUNT` descending
- `CATEGORY1` ascending
- `CATEGORY2` ascending

---

## 🧩 Approach

1. **Join `ProductPurchases` with `ProductInfo`** to get the category for each purchase.  
2. Use a **self-join** to form all category pairs per user.  
3. Filter distinct pairs where `CATEGORY1 < CATEGORY2`.  
4. Count the number of users per category pair.  
5. Include only pairs with at least 3 users.  
6. Order results according to the requirements.  

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH NEWINPUT AS (
    SELECT PP.USER_ID, PP.PRODUCT_ID, PI.CATEGORY AS CATEGORY
    FROM PRODUCTPURCHASES PP JOIN PRODUCTINFO PI
    ON PP.PRODUCT_ID = PI.PRODUCT_ID;
), NEWTEMP AS (
    SELECT DISTINCT PP1.CATEGORY AS CATEGORY_1, PP2.CATEGORY AS CATEGORY_2, PP1.USER_ID
    FROM NEWINPUT PP1 JOIN NEWINPUT PP2
    ON PP1.CATEGORY != PP2.CATEGORY AND PP1.USER_ID = PP2.USER_ID
    GROUP BY PP1.CATEGORY, PP2.CATEGORY, PP1.USER_ID
    HAVING PP1.CATEGORY < PP2.CATEGORY
)
SELECT N.CATEGORY_1 AS CATEGORY1, N.CATEGORY_2 AS CATEGORY2, COUNT(N.USER_ID) AS CUSTOMER_COUNT
FROM NEWTEMP N
GROUP BY N.CATEGORY_1, N.CATEGORY_2
HAVING COUNT(N.USER_ID) >= 3
ORDER BY CUSTOMER_COUNT DESC, CATEGORY_1, CATEGORY_2;
