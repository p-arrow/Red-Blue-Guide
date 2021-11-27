## TABLE OF CONTENTS
1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/SQL.md#basics)
2. [STATEMENTS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/SQL.md#statements)
3. [METHODS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/SQL.md#methods)
4. [SQL EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/C_Coding/SQL.md#sql-examples)

## BASICS

### Technical Terms 
- **ERD** (Entity relationship diagram): Common way to view data in a database
- **SQL** (Structured Query Language): A language that allows us to access data stored in a database
- **Database**: Collection of tables that share connected data stored in a computer
- **Database Normalization**: When creating a database, think about how data will be stored
    - Are the tables storing logically?
    - Can I accesssingle location, rather than many tables for the same information
    - Can I access and manipulate data quickly and efficiently?
- **Primary Key (PK) / Foreign Key (FK)**
    - A primary key is a unique column in a particular table. Normally first column in each tables 
    - A foreign key is when we see a primary key in another table


### Advantages of SQL 
- SQL is easy to understand
- access data directly
- audit and replicate our data
- analyzing multiple tables at once
- analyze more complex questions than dashboard tools like Google Analytics
- SQL isn't case sensitive
- Data integrity is ensured:
    - only the data you want entered is entered
    - only certain users are able to enter data into the database
- Data can be accessed quickly:
    - obtain results very quickly from the data stored in a database
    - Code can be optimized to quickly pull results
- Data is easily shared:
    - multiple individuals can access data stored in a database
- NULL: all cells where data does not exist



### Best Practices 
- Capitalization of orders: FROM, SELECT, ORDER BY etc.
- Avoid Spaces in Table and Variable Names: table_name
- Use White Space in Queries
- SQL isn't case sensitive
- Semicolons:  `SELECT account_id FROM orders;`

<br />

## STATEMENTS

- **CREATE TABLE**: is a statement that creates a new table in a database.
- **DROP TABLE**: is a statement that removes a table in a database.
- **SELECT**: allows you to read data and display it. This is called a query.
- **SELECT DISTINCT**: narrows down the results
- **FROM**: is where you tell the query what table you are querying from. Notice the columns need to exist in this table
- **LIMIT**
    - useful to see just first few rows of a table
    - It will always appear as last statement
    - SQL evaluates the aggregations before the LIMIT clause
    - If you don’t group by any columns, you’ll get a 1-row result—no problem there
    - If you group by column with enough unique values that it exceeds the LIMIT number, the 
     aggregates will be calculated, and then some rows will simply be omitted from the results
- **ORDER BY**
    - allows us to order our table by any row
    - placed always after the SELECT and FROM statements
    - placed before the LIMIT statement
    - The order of columns listed in ORDER BY does make a difference. Ordering from left to right
- **WHERE**
    - we can subset out tables based on conditions that must be met
    - non-numeric: `LIKE, NOT, IN, AND, OR, BETWEEN, IS (NULL)`
    - numerical: `= , < , > , !=`
- **DESC**
    - creates a descending order
- **DROP and CREATE**
    - change the data in the database
    - reserved for database administrators 
- **INNER JOIN**
```
    SELECT accounts.name, orders.occurred_at
    FROM orders
    JOIN accounts
    ON orders.account_id = accounts.id;
```
- **OUTER JOIN** 
    1. Left (Outer) Join = Inner Join + Left Table
    2. Right (Outer) Join = Inner Join + Right Table
    3. Full Outer Join
       - pulls all same rows like INNER JOIN, but also potentially pull some additional rows
       - If no matching information in JOINed table, this type called NULL. You can consider any cell without data as NULL
       - Database executes JOIN/ON query first, then that result is filtered by WHERE

```
SELECT c.countryid, c.countryName, s.stateName
FROM State s                
LEFT JOIN Country c
ON c.countryid = s.countryid;

# The table called via "FROM" is the Left Table
```
- **COUNT** 
   - counts the rows
   - COUNT does not consider rows that have NULL values
- **SUM**
   - sum up all numerical data in a column
   - Unlike COUNT, you can only use SUM on numeric columns
   - SUM will ignore NULL values
- **MIN/MAX**
   - return min or max value of a column
- **AVG**
   - return the average value
- **GROUP BY**
   - aggregate data within subsets of the data
- **HAVING**
   - “clean” way to filter a query that has been aggregated (i/o WHERE)
   - HAVING appears after the GROUP BY clause, but before the ORDER BY clause
- **DATE_TRUNC**
   - truncate your date to a particular part of your date-time column
   - Common trunctions are day, month, and year
- **DATE_PART**
   - can be useful for pulling a specific portion of a date
   - pulling month or day of the week (dow) means, you're no longer keeping years in order (!)
- **CASE**
   - always goes in the SELECT clause
   - CASE must include the following components: WHEN, THEN, and END. ELSE is optional
   - You can include multiple WHEN and ELSE statements
- **WITH**
   - often called a Common Table Expression or CTE
   - serve the exact same purpose as subqueries, but tend to be cleaner to follow the logic
   - When creating multiple tables using WITH, you add comma after every table except the last one
   - The new table_name is always aliased, followed by your query nested between parentheses
- **POSITION**
   - takes a character and a column, and provides the index for each row.
   - The index of the first position is 1 in SQL 
   - it is *case sensitive*: `LEFT(UPPER(name), 1)` or `LEFT(LOWER(name), 1)`
   - `POSITION(',' IN city_state)`
- **STRPOS**
    - provides the same result as POSITION
    - it is *case sensitive*: `LEFT(UPPER(name), 1)` or `LEFT(LOWER(name), 1)`
    - `STRPOS(city_state, ',')`
- **CONCAT**
   - Combine columns together across rows
   - `CONCAT(first_name, ' ', last_name)`
- **CAST**
   - You can change a string to a date using CAST
   - CAST is actually useful to change lots of column types
   - `CAST(date_column AS DATE)`
   - `date_column::DATE`
- **COALESCE**
   - returns the first Null-value passed in each row

<br />

## METHODS

### DERIVED COLUMNS
- Creating a new column that is a combination of existing columns
- Common operators include:
```
    * (Multiplication)
    + (Addition)
    - (Subtraction)
    / (Division)
```
- Adding "AS" in order to create a name for the derived column
```
SELECT MIN(standard_qty) AS standard_min,
       MAX(standard_qty) AS standard_max
FROM orders;
```

### SUBQUERY
- You MUST use an alias for the table you nest within the outer query.
- The subquery goes in the FROM statement of the outer query
- If we return single single value, the SUBQUERY could be nested within a CASE statement
- If we return an entire column, IN wis needed to perform a logical argument
- If we are return an entire table, we must use ALIAS for the table
```
SELECT channel, AVG(event_count) AS avg_event_count
FROM (SELECT DATE_TRUNC('day',occurred_at) AS day,
      channel,
      COUNT(*) AS event_count
      FROM web_events
      GROUP BY 1,2) sub
GROUP BY 1
ORDER BY 2 DESC
```

### WINDOW FUNCTION
- Performs a calculation across a set of table rows that are somehow related to the current row
- This is comparable to the type of calculation that can be done with an aggregate function
- But unlike regular aggregate functions, use of a window function does not cause rows to become grouped into a single output row
- the rows retain their separate identities.
- **You can’t use window functions and standard aggregations in the same query**
- **More specifically, you can’t include window functions in a GROUP BY clause**
- **OVER**
   - The OVER clause determines exactly how the rows of the query are split up for processing by the window function
   - The PARTITION BY list within OVER specifies dividing the rows into groups, or partitions, that share the same values of the PARTITION BY expression(s)
- **ORDER BY**
   - If ORDER BY: frame consists of all rows from the start of the partition up to current row, plus any following rows that are equal to the current row according to the ORDER BY clause
   - If ORDER BY omitted: default frame consists of all rows in the partition
- **PARTITION BY**
   - PARTITION BY within OVER specifies dividing the rows into groups, or partitions
   - If PARTITION BY omitted: just one partition containing all the rows

<br />

## SQL EXAMPLES
```
SELECT accounts_id,
       SUM(poster_qty) AS poster,
       SUM(standard_qty) AS standard,
       SUM(gloss_qty) AS gloss
FROM orders
GROUP BY accounts_id
ORDER BY accounts_id;

# Any column in the SELECT statement that is not within aggregator must be in GROUP BY clause
# The GROUP BY always goes between WHERE and ORDER BY
```

```
SELECT accounts_id
      SUM(total_amt_usd) AS sum 
FROM orders
GROUP BY 1
HAVING SUM(total_amt_usd) >= 250000
+
SELECT a.name, w.channel, COUNT(*)AS counts
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
GROUP BY a.name, w.channel
HAVING w.channel = 'facebook' AND COUNT(*)>6
ORDER BY counts
```

```
SELECT DATE_TRUNC ('day',occurred_at) AS day,
      SUM(standard_qty) AS std_qty
FROM orders 
GROUP BY DATE_TRUNC ('day',occurred_at) // 1
ORDER BY DATE_TRUNC ('day',occurred_at) // 1
```

```
SELECT DATE_PART ('dow',occurred_at) AS day_of_week,
      SUM(total) AS total_qty
FROM orders 
GROUP BY 1
ORDER BY 2
```

```
SELECT standard_qty, COUNT(*)
FROM orders
GROUP BY 1  # "1" refers to standard_qty since it is first column in SELECT
ORDER BY 1  # "1" refers to standard_qty since it is first column in SELECT
```

```
SELECT s.name,
        COUNT(*) AS total_orders,
        SUM(total_amt_usd) AS total_sales,
        CASE WHEN COUNT(*) > 200 OR SUM(total_amt_usd) > 750000 THEN 'top'
             WHEN COUNT(*) > 150 OR SUM(total_amt_usd) > 500000 THEN 'middle'
             ELSE 'low' END AS rank
 FROM orders o
 JOIN accounts a
 ON o.account_id = a.id
 JOIN sales_reps s
 ON s.id = a.sales_rep_id
 GROUP BY 1
 ORDER BY 3 DESC
```

```
SELECT q3.sales_rep, q3.reg_name, q3.total_usd
FROM (SELECT reg_name,MAX(total_usd) AS total_usd
      FROM (SELECT s.name AS sales_rep,r.name AS reg_name, SUM(total_amt_usd)AS total_usd
            FROM orders o
            JOIN accounts a
            ON o.account_id = a.id
            JOIN sales_reps s
            ON s.id = a.sales_rep_id
            JOIN region r
            ON r.id = s.region_id
            GROUP BY 1,2) q1
      GROUP BY 1) q2
JOIN (SELECT s.name AS sales_rep,r.name AS reg_name, SUM(total_amt_usd)AS total_usd
      FROM orders o
      JOIN accounts a
      ON o.account_id = a.id
      JOIN sales_reps s
      ON s.id = a.sales_rep_id
      JOIN region r
      ON r.id = s.region_id
      GROUP BY 1,2
      ORDER BY 3 DESC) q3
ON q2.reg_name = q3.reg_name AND q3.total_usd = q2.total_usd
```

```
WITH table1 AS (
          SELECT *
          FROM web_events),
     table2 AS (
          SELECT *
          FROM accounts)

SELECT *
FROM table1
JOIN table2
ON table1.account_id = table2.id;
```

```
>>Solution #1<<
SELECT category, COUNT(*)
FROM(SELECT CASE WHEN letter IN ('A','E','I','O','U') THEN 'vowel'
            ELSE 'consonant' END AS category
            FROM (SELECT name, LEFT(UPPER(name), 1) AS letter
                 FROM accounts) sub
    )sub2
GROUP BY 1

>>Solution #2<<
SELECT category, COUNT(*)
FROM (SELECT CASE WHEN LEFT(UPPER(name), 1) IN ('A','E','I','O','U') THEN 'vowel'
             ELSE 'consonant' END AS category
             FROM accounts) sub
GROUP BY 1

>>Solution #3<<
SELECT CASE WHEN LEFT(UPPER(name), 1) IN ('A','E','I','O','U') THEN 'vowel'
       ELSE 'consonant' END AS category,
       COUNT(*)
FROM accounts
GROUP BY 1
```

```
COUNT(primary_poc) AS regular_poc
COUNT(COALESCE(primary_poc, 'no POC')) AS modified_poc
FROM accounts

# result is 345 regular, but modified 354 due to COALESCE
```
