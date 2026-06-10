# Table of Contents

- [SQL and DBSQL Commands](#sql-and-dbsql-commands)
- [Fact and Dimension Table](#fact-and-dimension-table)
- [SCD](#scd)
- [CTE](#cte)

-----------------

Of course. This is an excellent and crucial step in your career. Your senior data engineer gave you pure gold advice. "GOD Level SQL" isn't about memorizing every function; it's about deeply understanding *how* data is structured, moved, and transformed, and being able to express complex business logic elegantly and performantly in SQL.

Since you're at Databricks, the context is the Lakehouse architecture, which blends the best of data warehouses and data lakes. This means your SQL skills need to span both traditional warehousing concepts and modern distributed data processing paradigms.

Let's build your roadmap. We'll structure it in phases, from fundamentals to mastery, with a heavy focus on the data engineering context.

### The "God Level" SQL Roadmap for a Data Engineer

---

### Phase 1: Solidifying the Unshakeable Foundation (Weeks 1-2)

You know the basics, but we need to make them second nature. The goal here is to be able to write clean, readable, and correct queries without thinking.

**Core Concepts:**

*   **Relational Model Revisited:** Truly understand Primary Keys, Foreign Keys, Constraints, and Normalization (1NF, 2NF, 3NF). Know *why* they exist.
*   **Mastering `JOIN`s:** `INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, `CROSS JOIN`. Be able to visualize the result of each join instantly. Understand self-joins.
*   **Advanced `GROUP BY` and `HAVING`:** Use them for complex aggregations. Understand the order of execution (`FROM` -> `WHERE` -> `GROUP BY` -> `HAVING` -> `SELECT` -> `ORDER BY`).
*   **Subqueries vs. CTEs (Common Table Expressions):** Know when and why to use the `WITH` clause. Hint: for readability and reusability, CTEs are almost always preferred.

**Resources:**

1.  **Main Resource (Choose One):**
    *   **Course:** **[Mode's SQL Tutorial](https://mode.com/sql-tutorial/)** (Free & Interactive): It's fantastic for going from basic to intermediate. It's practical and well-paced.
    *   **Book:** **"Learning SQL, 3rd Edition" by Alan Beaulieu:** A classic for a reason. It builds a very strong foundation.

2.  **Optional/Supplementary Resources:**
    *   **Practice:** **[SQLZoo](https://sqlzoo.net/)** - Great for hands-on practice with specific concepts.
    *   **Reference:** **[W3Schools SQL Tutorial](https://www.w3schools.com/sql/)** - Excellent for quick syntax lookups.

---

### Phase 2: The Data Engineer's Toolkit - Advanced SQL (Weeks 3-5)

This is where you start separating yourself from a casual SQL user. These tools are the bread and butter of data transformation and analysis.

**Core Concepts:**

*   **Window Functions:** This is **non-negotiable** for a data engineer. They are your superpower.
    *   Ranking: `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `NTILE()`
    *   Offset: `LAG()`, `LEAD()`
    *   Aggregates as Window Functions: `SUM(...) OVER (PARTITION BY ... ORDER BY ...)` for running totals, moving averages, etc.
*   **Advanced Data Manipulation:**
    *   `CASE` statements for conditional logic.
    *   `COALESCE`, `NULLIF` for robust `NULL` handling.
    *   `UNION` vs. `UNION ALL`.
*   **Pivoting Data:** `PIVOT`/`UNPIVOT` (if the dialect supports it) or the manual way using `CASE` statements with aggregations.

**Resources:**

1.  **Main Resource:**
    *   **Book:** **"T-SQL Window Functions" by Itzik Ben-Gan.** Don't be put off by "T-SQL". The concepts are universal and this book is the undisputed bible on the topic. It will fundamentally change how you write SQL.

2.  **Optional/Supplementary Resources:**
    *   **Online Guide:** **[The SQL Window Functions Cheat Sheet](https://www.sqltutorial.org/sql-window-functions/)** - A great, easy-to-read guide.
    *   **Practice:** **LeetCode (Database Problems)** and **HackerRank (SQL Problems)**. Start with Medium difficulty here. They are full of window function problems.

---

### Phase 3: The Architect's Mindset - Data Warehousing & Modeling (Weeks 6-8)

This is where you learn the *why* behind the code you write. You were spot on with SCDs and CDC. This phase is about the patterns that govern how data pipelines are built.

**Core Concepts:**

*   **OLTP vs. OLAP:** Understand the difference between transactional systems and analytical systems.
*   **Dimensional Modeling:**
    *   Facts & Dimensions: What they are, how they relate.
    *   Star Schema vs. Snowflake Schema.
*   **Slowly Changing Dimensions (SCDs):** This is a direct request from your list.
    *   **Type 1:** Overwrite.
    *   **Type 2:** Add a new row (versioning with effective dates and current flags). This is the most common and important one.
    *   **Type 3:** Add a new column.
*   **Change Data Capture (CDC):** How do you identify new or changed records from a source system? (e.g., using timestamps, version numbers, or log-based CDC tools).
*   **The `MERGE` Statement:** The practical implementation of SCDs and CDC logic. It combines `INSERT`, `UPDATE`, and `DELETE` into one atomic statement. **This is critical in Databricks/Delta Lake.**

**Resources:**

1.  **Main Resource:**
    *   **Book:** **"The Data Warehouse Toolkit, 3rd Edition" by Ralph Kimball.** This is the foundational text of dimensional modeling. Reading the first few chapters will give you a vocabulary and framework that will serve you for your entire career.

2.  **Optional/Supplementary Resources:**
    *   **Databricks Docs:** Search for their articles on "Slowly Changing Dimensions Delta Lake". They have excellent, practical examples of implementing SCD Type 2 using `MERGE`.
    *   **YouTube:** Search for "Dimensional Modeling Explained" or "SCD Type 2 Explained" for great visual breakdowns.

---

### Phase 4: Databricks SQL & The Lakehouse Way (Ongoing, but focus in Weeks 9-10)

Now, let's get specific to your environment. SQL in Databricks is SQL, but the underlying engine (Photon) and storage format (Delta Lake) give you unique capabilities.

**Core Concepts:**

*   **Delta Lake:** Understand that you're not querying a traditional database. You're querying versioned Parquet files with a transaction log.
    *   **ACID Transactions:** This is why you can do reliable `MERGE` statements on a data lake.
    *   **Time Travel:** `SELECT * FROM my_table VERSION AS OF 1`. Know this exists and what it's for.
    *   **`OPTIMIZE` and `Z-ORDER`:** How to physically optimize the data layout for query performance.
*   **Databricks SQL (DBSQL):**
    *   Understand the difference between a SQL Warehouse and an All-Purpose Cluster.
    *   Learn to use the query profiler to see where your query is spending time.
*   **Delta Live Tables (DLT):** While not pure SQL, it's a framework for building pipelines using SQL. Understand its declarative nature and the `APPLY CHANGES INTO` syntax, which is Databricks' managed way of doing CDC/SCD.

**Resources:**

1.  **Main Resource:**
    *   **[Official Databricks Documentation](https://docs.databricks.com/) & [Databricks Academy](https://www.databricks.com/learn/academy):** There is no substitute. It is comprehensive, up-to-date, and has tutorials specifically for what you're doing. Focus on the sections for Delta Lake and Databricks SQL.

2.  **Optional/Supplementary Resources:**
    *   **The Databricks Blog:** They frequently post deep dives and best practices.
    *   **Book:** **"Learning Spark, 2nd Edition"**: While not just SQL, reading parts of it will help you understand the distributed engine *underneath* DBSQL, which is crucial for performance tuning.

---

### Phase 5: Performance & Internals (The "God" Tier)

This is what separates the great from the gods. Understanding *how* the database/query engine executes your query.

**Core Concepts:**

*   **Reading an `EXPLAIN` Plan:** Learn to identify full table scans, index seeks/scans, and the cost of different join types (e.g., Broadcast Hash Join vs. Sort Merge Join in the Spark world).
*   **Indexing Theory:** Even though Delta Lake has `Z-ORDERING` instead of traditional indexes, you MUST understand the theory. Know what a B-Tree is conceptually. This knowledge is transferable everywhere.
*   **Transactions & Concurrency:** ACID properties (Atomicity, Consistency, Isolation, Durability). Understand what locking is, even at a high level.

**Resources:**

1.  **Main Resource:**
    *   **Website/Book:** **[Use The Index, Luke!](https://use-the-index-luke.com/)** by Markus Winand (also available as the book "SQL Performance Explained"). This is the single best resource for learning how SQL performance works from the ground up. It's concise, clear, and vendor-neutral.

2.  **Optional/Supplementary Resources:**
    *   **Conference Talks:** Search YouTube for talks from Databricks Data+AI Summit or AWS re:Invent on query optimization and performance.
    *   **ORM Deep Dive:** Since you have an ORM background, learn how to get the raw SQL that your ORM generates. Analyze it. You'll be shocked at how inefficient it can be, and it's a great way to learn what *not* to do.

---

### Summary and Action Plan

| Phase | Focus                                         | Main Resource Recommendation                             | Practice Platform              |
| :---- | :-------------------------------------------- | :------------------------------------------------------- | :----------------------------- |
| **1** | Core SQL Mastery                              | Mode's SQL Tutorial OR "Learning SQL" (Beaulieu)         | SQLZoo, Mode's exercises       |
| **2** | Advanced Analytical SQL                       | "T-SQL Window Functions" (Ben-Gan)                       | LeetCode, HackerRank (Medium+) |
| **3** | Data Warehouse Architecture                   | "The Data Warehouse Toolkit" (Kimball)                   | Apply concepts in project work |
| **4** | Databricks Ecosystem                          | Official Databricks Documentation & Academy              | Your internship project!       |
| **5** | Performance & Internals                       | UseTheIndexLuke.com / "SQL Performance Explained"        | Analyze `EXPLAIN` on your own queries |

**Final Advice:**

1.  **Practice Every Day:** Even 30 minutes on LeetCode or re-writing a query more efficiently makes a huge difference.
2.  **Read Production Code:** Look at the SQL code your senior engineers are writing. Ask them *why* they structured a CTE a certain way or chose a specific join strategy. This is an invaluable learning resource.
3.  **Think in Sets, Not Loops:** This is the biggest mental shift. SQL operates on entire sets of data at once. Avoid thinking row-by-row. Window functions are the ultimate expression of set-based thinking.

You are in the perfect position to learn this, and you have the right attitude. Stick to this plan, be curious, and you'll be the person others come to for SQL help in no time. Good luck


# SQL and DBSQL Commands

Here is a rapid-fire list of 60+ essential SQL and Databricks SQL commands, keywords, and concepts, categorized for easy reference. 

### Delta Lake Specific (The Magic)
1. `MERGE INTO` (Upserts)
2. `OPTIMIZE` (File compaction)
3. `ZORDER BY` (Data skipping/clustering)
4. `VACUUM` (Delete old files)
5. `RETAIN 0 HOURS` (Vacuum parameter)
6. `RESTORE TABLE` (Undo mistakes)
7. `DESCRIBE HISTORY` (View transaction log)
8. `DESCRIBE DETAIL` (View table metadata/size)
9. `VERSION AS OF` (Time travel syntax)
10. `TIMESTAMP AS OF` (Time travel syntax)
11. `DEEP CLONE` (Full data copy)
12. `SHALLOW CLONE` (Metadata-only copy)
13. `FSCK REPAIR TABLE` (Fix broken metadata)
14. `CONVERT TO DELTA` (Upgrade Parquet to Delta)

### Data Definition (DDL - Structure)
15. `CREATE CATALOG`
16. `CREATE SCHEMA` / `CREATE DATABASE`
17. `CREATE TABLE`
18. `CREATE OR REPLACE TABLE` (CRAS)
19. `CREATE TABLE AS SELECT` (CTAS)
20. `CREATE TABLE ... USING DELTA`
21. `CREATE TABLE ... LOCATION` (External/Unmanaged tables)
22. `CREATE TABLE ... PARTITIONED BY` 
23. `CREATE VIEW`
24. `CREATE TEMP VIEW`
25. `CREATE GLOBAL TEMP VIEW`
26. `CREATE MATERIALIZED VIEW` (Databricks SQL)
27. `CREATE STREAMING LIVE TABLE` (Delta Live Tables)
28. `ALTER TABLE ... ADD COLUMNS` (Schema evolution)
29. `ALTER TABLE ... DROP COLUMNS`
30. `ALTER TABLE ... RENAME COLUMN`
31. `ALTER TABLE ... SET TBLPROPERTIES`
32. `DROP TABLE`
33. `TRUNCATE TABLE` (Wipe data, keep schema)

### Data Manipulation (DML - Editing)
34. `INSERT INTO` (Append)
35. `INSERT OVERWRITE` (Replace data, keep schema)
36. `UPDATE ... SET ... WHERE`
37. `DELETE FROM ... WHERE`
38. `COPY INTO` (Incremental Auto Loader via SQL)

### Advanced Querying (DQL - Reading)
39. `WITH` (Common Table Expressions / CTEs)
40. `INNER JOIN` / `LEFT JOIN` / `RIGHT JOIN` / `FULL OUTER JOIN`
41. `CROSS JOIN` (Cartesian product)
42. `LEFT ANTI JOIN` (Find missing records)
43. `LEFT SEMI JOIN` (Fast existence check)
44. `PIVOT` (Rows to Columns)
45. `UNPIVOT` (Columns to Rows)
46. `UNION` / `UNION ALL` 
47. `INTERSECT` (Common records)
48. `EXCEPT` / `MINUS` (Difference)
49. `GROUP BY` / `HAVING`
50. `ROLLUP` / `CUBE` (Multidimensional aggregation)

### Window Functions & Analytics
51. `OVER (PARTITION BY ... ORDER BY ...)`
52. `ROW_NUMBER()` 
53. `RANK()` / `DENSE_RANK()`
54. `LEAD()` (Look at next row)
55. `LAG()` (Look at previous row)

### Complex Data Types (JSON & Arrays)
56. `EXPLODE()` (Flatten arrays to rows)
57. `FROM_JSON()` (Parse string to JSON)
58. `TO_JSON()` (Convert object to JSON string)
59. `COLLECT_LIST()` / `COLLECT_SET()` (Aggregate rows into an array)
60. `FILTER()` (Higher-order array function)
61. `TRANSFORM()` (Higher-order array function)
62. `REDUCE()` (Higher-order array function)

### Unity Catalog & Security (DCL)
63. `GRANT` (Give permissions)
64. `REVOKE` (Remove permissions)
65. `SHOW GRANTS`
66. `CREATE EXTERNAL LOCATION`
67. `CREATE STORAGE CREDENTIAL`
68. `CREATE SHARE` (Delta Sharing)
69. `CREATE RECIPIENT` (Delta Sharing)

### Metadata Exploration
70. `SHOW CATALOGS`
71. `SHOW DATABASES`
72. `SHOW TABLES`
73. `SHOW CREATE TABLE` (See exact SQL used to build table)
74. `DESCRIBE EXTENDED`


# Fact and Dimension Table

To explain Fact and Dimension tables to experienced professionals, you need to go beyond the basic definitions and explain the **architectural "Why."** 

Fact and Dimension tables are the building blocks of **Dimensional Modeling** (pioneered by Ralph Kimball). In the Databricks Medallion Architecture, you build these tables in your **Gold Layer**. 

Here is a comprehensive, detailed breakdown of how they work, their variations, and why they are designed this way.

---

### The Big Picture: Why Dimensional Modeling?
Traditional databases (OLTP/RDBMS) are built using **Third Normal Form (3NF)**. They break data into dozens of tiny tables to avoid duplicating data. This is great for fast `INSERT`s, but terrible for analytics because answering a simple business question requires 15 slow `JOIN`s.

Dimensional Modeling ignores 3NF. It intentionally duplicates data (de-normalization) and organizes it into a **Star Schema** to make `SELECT` queries and aggregations lightning fast. 

---

### 1. Dimension Tables (The "Context")
Dimension tables contain the descriptive attributes of your business. They answer the **Who, What, Where, When, and Why** of a transaction.

*   **Structure:** They are typically **Wide** (many columns) but **Short** (relatively few rows compared to fact tables). 
*   **Data Type:** Highly textual and descriptive. 
*   **Examples:** `Dim_Customer`, `Dim_Product`, `Dim_Store`, `Dim_Date`.

#### Key Architectural Concepts of Dimensions:
*   **Natural Key vs. Surrogate Key:**
    *   *Natural Key:* The ID from the source system (e.g., Salesforce Customer ID `ABC-123`).
    *   *Surrogate Key:* A brand new, auto-incrementing Integer ID created specifically for the Data Warehouse (e.g., `Customer_Key = 1`). **Fact tables only join to Surrogate Keys.** Integers process joins infinitely faster than string-based Natural Keys.
*   **Slowly Changing Dimensions (SCDs):** How do you handle a customer who moves from New York to California?
    *   **SCD Type 1 (Overwrite):** You delete "New York" and replace it with "California". (Fast, but you lose historical tracking).
    *   **SCD Type 2 (Versioning):** You keep the New York row but mark a flag `Is_Active = False`. You insert a brand new row for California with `Is_Active = True`. (This allows you to tie past sales to NY, and future sales to CA).
*   **The Date Dimension (`Dim_Date`):** Every data warehouse has an artificially generated Date table. Instead of doing complex SQL math to group by Quarter, the Date dimension has columns like `Is_Weekend`, `Fiscal_Quarter`, and `Holiday_Name`.

---

### 2. Fact Tables (The "Metrics")
Fact tables contain the measurable, quantitative data about a business event. They answer the **"How Much"** or **"How Many."**

*   **Structure:** They are typically **Narrow** (few columns, mostly just IDs and numbers) but incredibly **Long** (millions or billions of rows).
*   **Data Type:** Highly numeric.
*   **Examples:** `Fact_Sales`, `Fact_Website_Clicks`, `Fact_Inventory`.

#### Key Architectural Concepts of Fact Tables:
*   **The Grain (Crucial Concept):** The grain defines exactly what **one single row** in the fact table represents. For example, is a row "One daily summary of a store's sales," or is it "One single scan of a barcode at a cash register?" *You must define the grain before building the table.*
*   **Foreign Keys:** The only text in a fact table should be the Surrogate Keys that link back to the Dimension tables.
*   **Types of Facts (Metrics):**
    1.  **Additive:** Can be summed across all dimensions. (e.g., `Sales_Amount`. You can add sales by day, by store, or by customer, and the math is always correct).
    2.  **Semi-Additive:** Can be summed across *some* dimensions, but not Time. (e.g., `Bank_Account_Balance`. You can add the balances of all customers today, but you cannot add your Monday balance to your Tuesday balance to get a "Total Balance").
    3.  **Non-Additive:** Cannot be summed at all. (e.g., `Profit_Margin_Percentage` or `Temperature`. You must calculate an average instead).

#### Types of Fact Tables:
1.  **Transaction Fact Table:** One row per event. (e.g., Every time a customer clicks "Buy").
2.  **Periodic Snapshot Fact Table:** Summarized data at regular intervals. (e.g., A daily summary of total sales per store).
3.  **Accumulating Snapshot Fact Table:** Tracks a workflow with a clear start and end. (e.g., Order Placed $\rightarrow$ Order Shipped $\rightarrow$ Order Delivered. The same row is updated as the item moves through the pipeline).

---

### 3. The Star Schema (Bringing them together)
When you place the Fact table in the center and connect the Dimension tables around it via Foreign Keys, it looks like a Star.

*   **Why analysts love it:** If the CEO wants to know *"Total Revenue of Blue Shirts sold in California during Q3,"* the query is incredibly simple. You join `Fact_Sales` to `Dim_Product` (filter 'Blue Shirt'), `Dim_Store` (filter 'California'), and `Dim_Date` (filter 'Q3'). 

---

### 💡 The "Databricks Philosophy" (For your presentation)

If you are presenting this to experienced pros, here is how you tie traditional Fact/Dim theory to modern Databricks Lakehouse engineering:

1.  **Storage is Cheap, Compute is Expensive:** In the 1990s, architects used "Snowflake Schemas" to compress dimension tables and save hard drive space. In Databricks, we don't care about AWS S3 storage costs. We use heavily denormalized **Star Schemas** because Databricks' Photon engine can scan wide tables blisteringly fast.
2.  **Handling SCDs with Delta Lake:** In a traditional Hadoop Data Lake, updating a Dimension table for an SCD Type 2 change was impossible without rewriting the entire file. Databricks **Delta Lake** gives us the `MERGE INTO` SQL command, allowing us to perform upserts on Dimension tables in seconds.
3.  **Z-Ordering the Fact Table:** Because Fact tables have billions of rows, they can be slow to query. In Databricks, we use `OPTIMIZE Fact_Sales ZORDER BY (Customer_Key, Date_Key)`. This physically clusters the data in cloud storage based on those Dimension keys, allowing Spark to skip reading 99% of the files when an analyst runs a dashboard query.


# SCD

To explain **Slowly Changing Dimensions (SCD)** to experienced professionals, you need to show them exactly how the data looks before and after a change. 

In a Data Warehouse, dimension attributes change over time (e.g., a customer moves, a product gets a new category). How you design your database to handle that change is called your SCD strategy.

Here is the comprehensive breakdown of **every standard Kimball SCD type (Types 0, 1, 2, 3, 4, and 6)**. 

To make this crystal clear, we will use **one consistent example** for most of them: 
*   **The Scenario:** Customer "John Doe" (Customer_ID = 99) lives in **New York**. 
*   **The Event:** Today, John moves to **California**.

---

### SCD Type 0: Retain Original (The "Do Nothing" Approach)
*   **The Concept:** Once the data is written, it is never allowed to change. Subsequent updates are completely ignored.
*   **When to use it:** For attributes that represent a permanent fact at the time of creation (e.g., `Original_Signup_Date`, `Birth_Branch`, `SSN`).
*   **The Example:**
    Even if John moves to California, his `Original_Signup_State` will forever remain New York.

---

### SCD Type 1: Overwrite (No History)
*   **The Concept:** You simply `UPDATE` the existing row. The old data is permanently destroyed.
*   **When to use it:** When the business does not care about history, or when fixing a spelling mistake.
*   **The Data Before:**
    | Cust_Key | Cust_ID | Name | State |
    | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | New York |
*   **The Data After (Type 1):**
    | Cust_Key | Cust_ID | Name | State |
    | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | **California** |
*   **The Danger:** If John bought a TV while living in New York, running a historical sales report tomorrow will make it look like he bought that TV in California. You rewrite history.

---

### SCD Type 2: Add a New Row (Row Versioning) - *The Industry Standard*
*   **The Concept:** You keep the old row but mark it as "Inactive." You insert a brand new row with the new data and mark it as "Active." 
*   **Requirements:** You *must* use a Surrogate Key (Cust_Key), and you need tracking columns (`Start_Date`, `End_Date`, `Is_Active`).
*   **When to use it:** When perfect historical accuracy is required (90% of all Enterprise Data Warehouses use Type 2).
*   **The Data Before:**
    | Cust_Key | Cust_ID | Name | State | Start_Date | End_Date | Is_Active |
    | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | New York | 2020-01-01 | 9999-12-31 | **Y** |
*   **The Data After (Type 2):**
    | Cust_Key | Cust_ID | Name | State | Start_Date | End_Date | Is_Active |
    | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | New York | 2020-01-01 | **2023-10-01** | **N** |
    | **102** | 99 | John Doe | **California** | **2023-10-02** | 9999-12-31 | **Y** |
*   **The Benefit:** If John bought a TV in 2021, the `Fact_Sales` table uses `Cust_Key 101`. If he buys a TV today, it uses `Cust_Key 102`. History is perfectly preserved.

---

### SCD Type 3: Add a New Column (Partial History)
*   **The Concept:** You do not add a new row. Instead, you add a column to hold the previous value.
*   **When to use it:** When the business only cares about the "Current" vs. "Previous" state (e.g., comparing current sales territory assignments to last year's assignments).
*   **The Data Before:**
    | Cust_Key | Cust_ID | Name | Current_State | Previous_State |
    | :--- | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | New York | NULL |
*   **The Data After (Type 3):**
    | Cust_Key | Cust_ID | Name | Current_State | Previous_State |
    | :--- | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | **California** | **New York** |
*   **The Danger:** If John moves a third time (to Texas), the "New York" data is permanently overwritten and lost. You only keep one step of history.

---

### SCD Type 4: Use a History Table
*   **The Concept:** You split the dimension into two separate tables. The main `Dim_Customer` table acts exactly like **Type 1** (Overwrites; only shows current data). A second, separate table `Dim_Customer_History` tracks every single change.
*   **When to use it:** When the Dimension is queried heavily for real-time operations, and you want to keep the main table small and fast, relegating the bulky history to a table that analysts only query occasionally.
*   **The Data After (Type 4):**
    *Table 1: `Dim_Customer` (Main Table)*
    | Cust_Key | Cust_ID | Name | State |
    | :--- | :--- | :--- | :--- |
    | 101 | 99 | John Doe | **California** |

    *Table 2: `Dim_Customer_History` (History Table)*
    | Hist_Key | Cust_ID | Name | State | Valid_From | Valid_To |
    | :--- | :--- | :--- | :--- | :--- | :--- |
    | 1 | 99 | John Doe | New York | 2020-01-01 | 2023-10-01 |
    | 2 | 99 | John Doe | California | 2023-10-02 | NULL |

---

### SCD Type 5: Mini-Dimension (For Rapidly Changing Attributes)
*(Note: Not based on the 1-2-3 numbering, this is an architectural pattern).*
*   **The Concept:** What if an attribute changes *every single day*? (e.g., Customer Credit Score, or Age Profile). If you use Type 2, your Customer table will grow to billions of rows instantly. 
*   **The Solution:** You remove the volatile attribute from `Dim_Customer` entirely. You create a "Mini-Dimension" (e.g., `Dim_Demographics`) containing every possible combination of Credit Score and Age. You then link them directly in the Fact table, not the Dimension table.

---

### SCD Type 6: The Hybrid (Types 1 + 2 + 3 combined)
*(Math logic: 1 + 2 + 3 = 6)*
*   **The Concept:** This is the ultimate, most complex SCD. It adds a new row (like Type 2), creates a historical column (like Type 3), and overwrites the "Current" attribute on all past rows (like Type 1).
*   **When to use it:** When the business wants perfect history, but an analyst frequently asks: *"Show me all historical sales for anyone who CURRENTLY lives in California."*
*   **The Data Before:**
    | Cust_Key | Cust_ID | Hist_State | Current_State | Is_Active |
    | :--- | :--- | :--- | :--- | :--- |
    | 101 | 99 | New York | New York | Y |
*   **The Data After (Type 6):**
    | Cust_Key | Cust_ID | Hist_State | Current_State | Is_Active |
    | :--- | :--- | :--- | :--- | :--- |
    | 101 | 99 | New York | **California** *(Overwritten!)* | **N** |
    | **102** | 99 | **California** | **California** | **Y** |
*   **The Benefit:** Row 101 correctly states that historically, John was in NY. But it was overwritten to show he *currently* lives in CA. Now, an analyst can simply run `WHERE Current_State = 'California'` and easily pull all of John's NY sales and CA sales in one query.

---

### 💡 Databricks Context for your Presentation:
When you present this to the experienced pros, you can drop this massive flex:

*"Historically, managing SCD Type 2 in a Data Lake was a nightmare because you couldn't run row-level updates on massive Parquet files to close out the `End_Date` and `Is_Active` columns. In Databricks, we execute SCD Type 1 and Type 2 effortlessly using the **`MERGE INTO`** SQL command on Delta Tables. Furthermore, if we use **Delta Live Tables (DLT)**, Databricks has a built-in function called `APPLY CHANGES INTO` that automatically manages all the SCD Type 1 and Type 2 sequencing, timestamps, and active flags behind the scenes without us having to write the complex update logic!"*

## More on SCD

There are eight widely recognized types of Slowly Changing Dimensions (SCDs), numbered 0 through 7, used in data warehousing to manage how historical data changes over time. Types 1, 2, and 3 are the most commonly implemented standards. [1, 2, 3, 4] 
## The 8 SCD Types

* Type 0 (Fixed Dimension): Original values are retained permanently. No changes or updates are ever allowed. [3, 5] 
* Type 1 (Overwrite): The old data is permanently overwritten with the new value. No historical tracking is retained. [6, 7] 
* Type 2 (Row Versioning): A new row is added for every change made to an attribute. This creates a full audit trail and is the standard for tracking history. [5, 7, 8, 9] 
* Type 3 (Previous Value Column): Instead of a new row, a new column is added to the existing record to store only the previous value (before the most recent change). [6, 7] 
* Type 4 (Separate History Table): The dimension table retains only the current value, while changes are pushed to an append-only, separate history table. [5, 7] 
* Type 5 (Combined 4 + 1): Combines Types 4 and 1. It updates the current attribute in the main dimension table (like Type 1) but utilizes a separate table to track the versioned history. [10] 
* Type 6 (Hybrid / Combined 1 + 2 + 3): Combines the techniques of Types 1, 2, and 3. A single row tracks the current value, while a duplicate row (or older versions) tracks historical states over time. [1, 6, 11] 
* Type 7 (Hybrid Fact/Dimension Link): Uses both surrogate keys and natural keys in the dimension table to seamlessly link fact tables to both the current and historical versions of the dimension. [1, 10] 

To explore deeper explanations, the [Wikipedia Slowly Changing Dimension](https://en.wikipedia.org/wiki/Slowly_changing_dimension) page offers a detailed breakdown of these different methods and their hybrid applications. [1] 
Would you like to know which of these SCD types best fits your specific data needs (such as tracking customer addresses vs. updating product prices), or do you need help with SCD implementation in your data warehouse?

[1] [https://en.wikipedia.org](https://en.wikipedia.org/wiki/Slowly_changing_dimension)
[2] [https://www.cdata.com](https://www.cdata.com/kb/articles/slowly-changing-dimensions.rst)
[3] [https://www.applexus.com](https://www.applexus.com/blogs/slowly-changing-dimension-types-using-data-services)
[4] [https://www.youtube.com](https://www.youtube.com/watch?v=sZFCYpojP4I&t=34)
[5] [https://www.thoughtspot.com](https://www.thoughtspot.com/data-trends/data-modeling/slowly-changing-dimensions-in-data-warehouse)
[6] [https://www.expressanalytics.com](https://www.expressanalytics.com/blog/what-is-a-slowly-changing-dimension-and-the-logic-in-implementation)
[7] [https://weld.app](https://weld.app/blog/what-is-slowly-changing-dimensions)
[8] [https://www.thoughtspot.com](https://www.thoughtspot.com/data-trends/data-modeling/slowly-changing-dimensions-in-data-warehouse)
[9] [https://oneuptime.com](https://oneuptime.com/blog/post/2026-01-30-data-warehouse-type2-scd/view)
[10] [https://radacad.com](https://radacad.com/scd-slowly-changing-dimension-an-ultimate-guide/)
[11] [https://www.iri.com](https://www.iri.com/blog/data-transformation2/scd-type-6/)


# CTE

To explain **Common Table Expressions (CTEs)** to experienced professionals, you should frame them not just as a SQL syntax, but as a **code-organization and readability tool**. 

In the modern data engineering world (especially when using tools like **dbt** inside Databricks), CTEs are the absolute gold standard for writing SQL.

Here is the comprehensive guide to CTEs, covering every possible use case and variation.

---

### What is a CTE?
A CTE (defined by the `WITH` keyword) is a **temporary, named result set**. 
Think of it like creating a temporary table or View that exists *only for the exact millisecond* that your query is running, and then it instantly vanishes.

**Why use them instead of Subqueries?**
Subqueries are nested *inside* the main query, forcing you to read SQL inside-out. 
CTEs allow you to write SQL **top-to-bottom**, breaking massive, 1,000-line analytical queries into small, readable, logical stepping stones.

---

### Type 1: The Basic CTE (Replacing a Subquery)
*   **The Scenario:** You want to find all employees who make more than the company's average salary.
*   **How it works:** You calculate the average in the CTE, and then use that result in your main query.

```sql
WITH Company_Average AS (
    SELECT AVG(Salary) AS Avg_Salary 
    FROM employees
)
SELECT 
    e.Employee_Name, 
    e.Salary 
FROM employees e
CROSS JOIN Company_Average ca
WHERE e.Salary > ca.Avg_Salary;
```

---

### Type 2: Chained (Multiple) CTEs (The "Data Pipeline")
*   **The Scenario:** You need to do a complex transformation: First, filter active users. Second, calculate their total spend. Third, find the top 10.
*   **How it works:** You can define multiple CTEs separated by a comma. **CTE #2 can SELECT from CTE #1.** This is how modern pipelines are written.

```sql
WITH Active_Users AS (
    SELECT User_ID, Name 
    FROM users 
    WHERE Status = 'Active'
),
User_Spend AS (
    SELECT User_ID, SUM(Order_Total) AS Total_Spent
    FROM orders
    GROUP BY User_ID
)
-- The Main Query brings the CTEs together
SELECT 
    au.Name, 
    us.Total_Spent
FROM Active_Users au
JOIN User_Spend us ON au.User_ID = us.User_ID
ORDER BY us.Total_Spent DESC
LIMIT 10;
```

---

### Type 3: The Reusable CTE (Self-Joins)
*   **The Scenario:** You need to calculate Year-over-Year (YoY) Sales growth. You need to compare 2023 data to 2022 data.
*   **How it works:** Instead of writing the complex aggregation logic twice, you write it *once* in a CTE, and then `JOIN` the CTE to itself!

```sql
WITH Yearly_Sales AS (
    SELECT 
        Year(Order_Date) AS Sales_Year, 
        SUM(Amount) AS Total_Revenue
    FROM sales
    GROUP BY Year(Order_Date)
)
SELECT 
    Current_Year.Sales_Year,
    Current_Year.Total_Revenue AS Revenue_This_Year,
    Previous_Year.Total_Revenue AS Revenue_Last_Year,
    (Current_Year.Total_Revenue - Previous_Year.Total_Revenue) AS YoY_Growth
FROM Yearly_Sales Current_Year
LEFT JOIN Yearly_Sales Previous_Year 
    ON Current_Year.Sales_Year = Previous_Year.Sales_Year + 1;
```

---

### Type 4: CTEs with DML (Insert / Merge / Update)
*   **The Scenario:** You need to clean data before inserting it into your Silver Delta Table.
*   **How it works:** CTEs are not just for `SELECT` statements. You can use a CTE to prepare data exactly how you want it, and then instantly `INSERT` or `MERGE` it into a target table.

```sql
WITH Cleaned_API_Data AS (
    SELECT 
        CAST(Customer_ID AS INT),
        UPPER(TRIM(Customer_Name)) AS Clean_Name,
        COALESCE(State, 'Unknown') AS State
    FROM raw_bronze_api_table
    WHERE Customer_ID IS NOT NULL
)
INSERT INTO silver_customers (ID, Name, State)
SELECT * FROM Cleaned_API_Data;
```

---

### Type 5: The Recursive CTE (The Boss Level)
*   **The Scenario:** You have hierarchical data. For example, an Organizational Chart where an employee has a `Manager_ID`, and that Manager also has a `Manager_ID`, going all the way up to the CEO. You want to print the entire org chart showing who reports to whom at every level.
*   **How it works:** You use the keyword `WITH RECURSIVE`. The CTE actually **references itself** in a loop until it reaches the end of the hierarchy.
*   *Note: Databricks added support for Recursive CTEs in Databricks SQL / Spark 3.4.*

**The Anatomy of a Recursive CTE:**
1.  **Anchor Member:** The starting point (e.g., The CEO, who has no manager).
2.  `UNION ALL`
3.  **Recursive Member:** The query that joins back to the CTE itself to find the next level down.

```sql
WITH RECURSIVE Org_Chart AS (
    
    -- 1. ANCHOR MEMBER: Find the CEO (Manager_ID is NULL)
    SELECT 
        Employee_ID, 
        Name, 
        Manager_ID, 
        1 AS Hierarchy_Level
    FROM employees
    WHERE Manager_ID IS NULL
    
    UNION ALL
    
    -- 2. RECURSIVE MEMBER: Find the people who report to the people above
    SELECT 
        e.Employee_ID, 
        e.Name, 
        e.Manager_ID, 
        oc.Hierarchy_Level + 1 AS Hierarchy_Level
    FROM employees e
    JOIN Org_Chart oc ON e.Manager_ID = oc.Employee_ID
    -- This loops automatically until no more employees are found!
)
SELECT * FROM Org_Chart ORDER BY Hierarchy_Level;
```

---

### 💡 The "Databricks Philosophy" (For your presentation)

If you are explaining this in your reverse-KT session, make this highly relevant point to the senior engineers:

*"In modern Databricks development, especially if your company uses **dbt (Data Build Tool)**, CTEs are the fundamental building blocks of the entire architecture. dbt compiles hundreds of modular SQL files into massive chained CTEs before executing them on the Databricks Photon engine. Writing subqueries is considered an anti-pattern today; top-to-bottom CTEs are the modern standard for debugging and readability."*

## More on CTEs

In SQL, there are two primary types of Common Table Expressions (CTEs), with advanced variations depending on how they are nested or processed by the database engine: [1, 2, 3, 4, 5] 
## The 2 Primary Types of CTEs

   1. Non-Recursive CTE: The most common type. It retrieves a result set once and acts as a temporary, named table within the execution scope of your query. [2, 5] 
   2. Recursive CTE: References itself repeatedly until a specific stopping condition (termination condition) is met. It is primarily used to query hierarchical data like organizational charts, category trees, or network paths. [2, 5, 6] 

## Advanced Categorizations & Variations
Depending on your database platform (e.g., SQL Server, PostgreSQL), CTEs can also be categorized by how they are written or evaluated: [7] 

* Nested CTEs: These are layered CTEs where the definition of one CTE references another CTE within the same query. [8, 9] 
* Sequential CTEs: A query that contains multiple, independent CTEs declared one after the other, separated by a comma, which can reference earlier CTEs in the sequence. [8, 10, 11, 12] 
* Inline vs. Materialized CTEs (Performance-based):
* Inline: The database treats them dynamically as subqueries.
   * Materialized: The database physically stores the results of the CTE in memory/temp tables to prevent redundant calculations, which is highly useful in platforms like PostgreSQL. [2, 13] 
* Data-Modifying CTE: Allows you to use INSERT, UPDATE, or DELETE statements inside the CTE and return the results to your main query. [14, 15, 16, 17] 

If you want to dive deeper, tell me which database platform you are using (e.g., PostgreSQL, SQL Server, MySQL) and what data you are trying to query. I can help you write the perfect CTE for your specific situation.

[1] [https://www.c-sharpcorner.com](https://www.c-sharpcorner.com/article/common-table-expression-cte-in-sql-server/)
[2] [https://www.sigmacomputing.com](https://www.sigmacomputing.com/blog/common-table-expressions)
[3] [https://www.sqlservercentral.com](https://www.sqlservercentral.com/articles/what-exactly-is-a-cte-in-t-sql-a-comprehensive-guide-with-7-examples)
[4] [https://www.linkedin.com](https://www.linkedin.com/pulse/sql-deep-dive-subqueries-vs-ctes-sulara-perera-j0gfc)
[5] [https://www.scribd.com](https://www.scribd.com/document/871140874/Week-11-CTE)
[6] [https://www.stratascratch.com](https://www.stratascratch.com/blog/sql-ctes-usage-advantages-and-drawbacks)
[7] [https://www.owox.com](https://www.owox.com/glossary/common-table-expression-cte)
[8] [https://learn.microsoft.com](https://learn.microsoft.com/en-us/sql/t-sql/queries/nested-common-table-expression?view=sql-server-ver17)
[9] [https://www.blog.datawithbaraa.com](https://www.blog.datawithbaraa.com/p/sql-ctes-a-comprehensive-guide)
[10] [https://www.databasestar.com](https://www.databasestar.com/sql-cte-with/)
[11] [https://campus.datacamp.com](https://campus.datacamp.com/courses/data-manipulation-in-sql/correlated-queries-nested-queries-and-common-table-expressions?ex=7)
[12] [https://www.scribd.com](https://www.scribd.com/document/807055858/cte-in-sql)
[13] [https://www.reddit.com](https://www.reddit.com/r/SQL/comments/1etr8xq/do_you_use_ctes/)
[14] [https://www.cockroachlabs.com](https://www.cockroachlabs.com/docs/stable/common-table-expressions)
[15] [https://www.tigerdata.com](https://www.tigerdata.com/learn/how-to-use-common-table-expression-sql)
[16] [https://mimo.org](https://mimo.org/glossary/sql/common-table-expression)
[17] [https://oneuptime.com](https://oneuptime.com/blog/post/2026-01-24-mysql-cte/view)
