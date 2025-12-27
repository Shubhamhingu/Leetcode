# 🌳 LeetCode 608 – Tree Node

**Difficulty:** Medium  
**Category:** SQL / Database  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Tree**

| Column Name | Type |
|------------|------|
| id         | int  |
| p_id       | int  |

- `id` is the primary key of this table.
- Each row represents a node and its parent.
- Root nodes have `p_id IS NULL`.

---

## 📝 Task

Classify each node in the tree as one of the following:
- **Root**: Node with no parent
- **Inner**: Node with both parent and at least one child
- **Leaf**: Node with a parent but no children

Return the result ordered by `id`.

---

## 🧩 Approach

- Identify **Root** nodes using `p_id IS NULL`
- Identify **Inner** nodes by checking if a node appears as a parent
- Identify **Leaf** nodes by excluding all parent nodes
- Use `UNION` to combine all node types

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT ID, 'Root' AS TYPE FROM TREE WHERE P_ID IS NULL
UNION
SELECT DISTINCT(T1.ID) AS ID, 'Inner' AS TYPE
FROM TREE T1 JOIN TREE T2
ON T1.ID = T2.P_ID
AND T1.ID NOT IN (SELECT ID FROM TREE WHERE P_ID IS NULL);
UNION
SELECT ID, 'Leaf' AS TYPE
FROM TREE
WHERE ID NOT IN (SELECT DISTINCT(T1.ID) AS ID
FROM TREE T1 JOIN TREE T2
ON T1.ID = T2.P_ID)
AND P_ID IS NOT NULL;
