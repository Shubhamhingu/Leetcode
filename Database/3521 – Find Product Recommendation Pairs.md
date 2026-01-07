# 🛒 LeetCode 3521 – Find Product Recommendation Pairs

**Difficulty:** Medium  
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

- Records which products each user has purchased.

**ProductInfo**

| Column Name | Type    |
|------------|---------|
| product_id | int     |
| category   | varchar |

- Provides the category of each product.

---

### 📝 Task

Find pairs of products `(PRODUCT1_ID, PRODUCT2_ID)` such that:

1. Both products were purchased by the same user.
2. At least **3 users** purchased both products.
3. Report the category of each product and the number of users.

Sort the results by:

- `CUSTOMER_COUNT` descending
- `PRODUCT1_ID` ascending
- `PRODUCT2_ID` ascending

---

## 🧩 Approach

1. Use a **self-join** on `PRODUCTPURCHASES` to find product pairs bought by the same user.  
2. Filter to only consider distinct pairs where `PRODUCT_1 < PRODUCT_2` to avoid duplicates.  
3. Count the number of users who bought each pair.  
4. Only include pairs with at least 3 users.  
5. Join with `PRODUCTINFO` to get product categories.  
6. Order results as specified.  

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
WITH TEMPTABLE AS (
    SELECT DISTINCT PP1.PRODUCT_ID AS PRODUCT_1, PP2.PRODUCT_ID AS PRODUCT_2, PP1.USER_ID
    FROM PRODUCTPURCHASES PP1 JOIN PRODUCTPURCHASES PP2
    ON PP1.PRODUCT_ID != PP2.PRODUCT_ID AND PP1.USER_ID = PP2.USER_ID
    GROUP BY PP1.PRODUCT_ID, PP2.PRODUCT_ID, PP1.USER_ID
    HAVING PP1.PRODUCT_ID < PP2.PRODUCT_ID
    ORDER BY PP1.USER_ID
), FINALTEMP AS (
    SELECT PRODUCT_1, PRODUCT_2, COUNT(USER_ID) AS CUSTOMER_COUNT
    FROM TEMPTABLE
    GROUP BY PRODUCT_1, PRODUCT_2
    HAVING COUNT(USER_ID) >= 3
)
SELECT F.PRODUCT_1 AS PRODUCT1_ID,
    F.PRODUCT_2 AS PRODUCT2_ID,
    P1.CATEGORY AS PRODUCT1_CATEGORY,
    P2.CATEGORY AS PRODUCT2_CATEGORY,
    F.CUSTOMER_COUNT AS CUSTOMER_COUNT
FROM FINALTEMP F JOIN PRODUCTINFO P1 ON F.PRODUCT_1 = P1.PRODUCT_ID
JOIN PRODUCTINFO P2 ON F.PRODUCT_2 = P2.PRODUCT_ID
ORDER BY CUSTOMER_COUNT DESC, PRODUCT1_ID, PRODUCT2_ID;
