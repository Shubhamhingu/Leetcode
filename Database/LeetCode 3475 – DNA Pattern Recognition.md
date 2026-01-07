# 🧬 LeetCode 3475 – DNA Pattern Recognition

**Difficulty:** Medium  
**Category:** SQL / String Matching  
**Platform:** LeetCode  

---

## 📘 Problem Statement

Table: **Samples**

| Column Name  | Type    |
|--------------|---------|
| sample_id    | int     |
| dna_sequence | varchar |
| species      | varchar |

Each sample contains a DNA sequence represented as a string of nucleotides (`A`, `T`, `G`, `C`).

---

### 📝 Task

For each sample, report the following:

1. `HAS_START` – 1 if the DNA sequence starts with `"ATG"`, else 0.  
2. `HAS_STOP` – 1 if the DNA sequence ends with any of `"TAA"`, `"TAG"`, `"TGA"`, else 0.  
3. `HAS_ATAT` – 1 if the DNA sequence contains the substring `"ATAT"`, else 0.  
4. `HAS_GGG` – 1 if the DNA sequence contains the substring `"GGG"`, else 0.

---

## 🧩 Approach

- Use `LIKE` for string pattern matching.  
- `ATG%` detects sequences starting with `"ATG"`.  
- `%TAA`, `%TAG`, `%TGA` detect sequences ending with stop codons.  
- `%ATAT%` and `%GGG%` detect presence of specific motifs anywhere in the sequence.  
- Use `CASE` statements to map pattern presence to 1/0 flags.

---

## 🧪 SQL Solution (PL/SQL)

```sql
/* Write your PL/SQL query statement below */
SELECT SAMPLE_ID, DNA_SEQUENCE, SPECIES,
CASE
    WHEN DNA_SEQUENCE LIKE 'ATG%' THEN 1
    ELSE 0
END AS HAS_START,
CASE
    WHEN DNA_SEQUENCE LIKE '%TAA' THEN 1
    WHEN DNA_SEQUENCE LIKE '%TAG' THEN 1
    WHEN DNA_SEQUENCE LIKE '%TGA' THEN 1
    ELSE 0
END AS HAS_STOP,
CASE
    WHEN DNA_SEQUENCE LIKE '%ATAT%' THEN 1
    ELSE 0
END AS HAS_ATAT,
CASE
    WHEN DNA_SEQUENCE LIKE '%GGG%' THEN 1
    ELSE 0
END AS HAS_GGG
FROM SAMPLES;
