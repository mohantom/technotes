SQL Server Query
==================
Course: SQL server 2012 querying 1, 2012
Course: SQL server 2012 querying 2, 2012
Adventure Workds 2014 database: https://msftdbprodsamples.codeplex.com/releases/view/125550 


## Introduction to Relational Databases
Database objects
Table
– Store data
– Core component to all databases

Other objects work with table data
`Views` are virtual tables

Simplify structure
`Stored procedures` are commands that can be executed

Make changes
Return data
– Functions are commands that can be executed
Return data

Columns, rows, fields
`Constraints`: Ensure valid values
`Triggers`: Execute code in response to modifications
`Primary Key`: Unique values; Required for each row; Designed to uniquely identify each row

`Foreign Key`: Used to create relationships between tables;
Refers to the column pointing to the primary key column in the other table

## Relationship Concepts
– Divide data into multiple tables
– Faster updates
– More flexible reporting and querying
– Aids in data integrity
    Most queries require data from multiple tables
– Accomplished through joins

### One-to-One
– One row refers to one row
– Used to divide data when details aren’t frequently needed
– Not commonly implemented

### One-to-Many
– One row refers to many rows
– Parent child relationships
One customer can have many orders

### Many-to-Many
– Many rows refer to many rows
 One product can be ordered many times
 One order can have many products
– Implemented through two one-to-many relationships
 Middle table sometimes referred to as a "join" table

Design scenario

    Need to store customer orders
    A customer can place multiple orders
    An order can contain multiple products
    Products can be ordered multiple times

![Design scenario for order-product](../data/table%20design%20orders.png)
 
 

### Table design guide
Don't duplicate column data – How many products can we order?
Don’t duplicate row data – How many orders will a customer have?
Don’t store calculated fields*
– You can always figure out the answer
– Commonly violated for read performance and ease of use
Ensure data will remain consistent if changes occur
– What happens if a product price changes

SQL statements can update sets of rows
– Referred to as a result set
– Bounded by a predicate or filter

SQL can update individual rows
– Done through cursors (try to avoid it)
– Problems 
 Complex logic
 Slower performance

### Variables
Variables store temporary data
Components–Name
All variables start with an @ sign
System variables start with @@–Data type
What type of information will be stored
 –Integer, DteTime, Value
The information being stored
Can be NULL, meaning no value

## Introduction to select statement
Comments: --, /* */; short-cut: ^K
Referencing Objects
•Each object has four parts to its name
–Server: Default to the current server
–Database: Default to current database
–Schema: Defaults to configurable schema or dbo
Best practice is to always specify the name of the schema
–Object name
Keywords and special characters in an object name
– [] (Square brackets)
– "" (Double quotes)
•Must be enabled on server
–Quoted identifiers

Add semicolon at the end of the statement

### Predicate keywords
Between and (inclusive range)
(not) in, all, any, some, (not) exists

`LIKE` allows wild card characters
–% - Zero or more characters
–_ - One character
–[ ] – Used for a range
•[afr] – Will find a, f, or r
•[a-f] – Will find a, b, c, d, e, or f
–[^] – Any character except what is in the range

Escape character to search for special characters
– ProductCode LIKE '\[pc-%\]' ESCAPE '\'
Will search for [pc-%]

Only rows that test "true" are returned
•Any operation involving null evaluates to "unknown"

## Utilizing joins
Join syntax
-- ANSI Standard Joins
SELECT <columns>
FROM Schema.Table1 AS t1 INNER JOIN Schema.Table2 AS t2 ON t1.Column = t2.Column;
-- WHERE line joins
-- SQL will rewrite
-- Not preferred method
SELECT <columns>
FROM Schema.Table1 AS t1
 , Schema.Table2 AS t2
WHERE t1.Column = t2.Column;

### Best practice
Always alias table names
–Schema.Table AS t
•Always use two part naming for columns
–t.ColumnName
•Place each join on separate line
–FROM Schema.Table1 AS t1
INNER JOIN Schema.Table2 AS t2 ON t1.Column = t2.Column
•Place tables in logical order

INNER JOIN, FULL JOIN, LEFT JOIN, RIGHT JOIN
Cross join, self join

## Subquery
A query within a query
•Uses
–Breakdown complex logic
–Simplify reading
–"Sneak in" operations otherwise not allowed
•Place an aggregate function on a where clause
> Can often be replaced by a join

–Joins may perform faster
•SQL Server will frequently rewrite subqueries as joins
–Most readable query is frequently best

### SELECT line
•Access information from tables in SELECT line
–Average order amount
–Highest product price
•Query must return a single (scalar) value

### FROM line
•Create a "dynamic" table
•Useful for breaking down queries
•Query must be aliased
 
### WHERE line
Useful for comparing values from other tables
– Find customers who have placed orders
– Find orders containing a particular product category
Example: all customers who have placed an order
 
### IN
– Confirm column value exists in subquery
– Similar to an inner join
`EXISTS`: can be faster than IN
– Returns true if subquery returns values
– Frequently used with correlated queries
•ALL
–Compares column value to all items returned by subquery
–Subquery must return only one column
•ANY or SOME
–Compares column value to any item returned by subquery
–Subquery must return only one column
–ANY and SOME are identical
Correlated subqueries
Pass column from main (outer) query into subquery
•Used to simulate a join
 
## Union
Requirements
1.	Each query must contain the same number of columns
2.	Data types must be compatible
3.	First query sets column names of result set
4.	If using ORDER BY there can only be one at the end
5.	By default UNION queries are DISTINCT
–Use UNION ALL to return all rows with duplicate values
Distinct can be expensive (need to sort and remove)

## Aggregating data
GROUP BY … HAVING …
Used to perform calculations on data
•Examples
– Average sales per region
– Highest priced product per category
– Best performing sales person per department

•NULL values are ignored
•All columns on select line must be in aggregate
–GROUP BY line for all columns not in aggregate

SUM, MAX, MIN, AVG
COUNT(column): does not count null values
COUNT(*): count all rows

•GROUP BY is required for all columns not in aggregate
•Used for "by" or "for each" in user requests

•HAVING filters groups
•Used to find results that meet criteria
–Customers that have spent at least $100,000
–Sales people more than 30% under their quota

### Having vs Where
Where is filtered first, the Having is to filter groups

### Data rollups
ROLLUP
•CUBE
•GROUPING SET
•GROUPING and GROUPING_ID Functions

Provided GROUP BY Category, Subcategory, Product
•Totals provided:
–Category, Subcategory and Product
–Category, Subcategory
–Category

GROUP BY category, subcategory, product
WITH ROLLUP

CUBE
Provides totals for all combinations of columns on GROUP BY
•Provided GROUP BY Category, Subcategory, Product
•Totals provided:
–Category, Subcategory and Product
–Category, Subcategory
–Category, Product
–Subcategory, Product
–Category
–Subcategory
–Product
WITH CUBE
Caution: may get duplicate data or unwanted data

GROUPING SETS
Control totals provided
•Provided GROUP BY Category, Subcategory, Product
•Desired totals
–Category, Subcategory
–Category
–Subcategory
•Syntax: 
GROUP BY GROUPING SETS ((Category, Subcategory) , (Category) , (Subcategory))

GROUPING identifies a column/row being used for a total
–Returns the number 1 whenever that column/row is a total
•GROUPING_ID accepts column parameters
–Uses a bitmap to identify which columns are being used for total
•From the right
–1 for the first column
–2 for the second
–4 for the third
–Etc.
•Provided GROUPING_ID(Category, Subcategory, Product)
1.Product
2.Subcategory
3.Subcategory & Product
4.Category
5.Category & Product
6.Category & Subcategory
7.Category & Subcategory & Product
 

## Adavnce data aggregation
### CTE
Inline view or temporary table
•Uses:
–Breakdown complex queries
–Avoid subqueries
–Simplify certain syntax
 

### Pivot and unpivot
Convert row data into columns
```shell script
SELECT <NonPivot>
, <FirstPivotedColumn>
, ...
FROM <Table containing data>
PIVOT (FUNCTION(<data column>)
FOR <List of pivoted columns>)
AS <alias>

```

```shell script
SELECT *
    FROM SalesData
      PIVOT (SUM(Totalsold)
        FOR OrderYear IN ([2001], [2002], [2003], [2004])) AS pvt;
```
 

Unpivot is not a true reverse of pivot (not used so often)
```shell script
SELECT <Columns>
FROM <PivotedTable>
	UNPIVOT (<AggregatedColumn>
FOR <NewColumn>
	IN (<ColumnList>)) AS UPVT

```


### Except and intercept
Behaves like a UNION statement
–Same number of columns
–Data types must be compatible
•INTERSECT returns rows from top query that match bottom query
•EXCEPT returns rows from top query that don’t match bottom query
 

### Sorting data
ORDER BY controls which columns will be used to sort output
– If no ORDER BY is provided, no order is guaranteed
•Can sort by multiple columns
– Uses columns in order
•For example: FirstName and then LastName
•ORDER BY executes last in a SELECT statement
– Can use column aliases
– Can also use column number (Never use this syntax)

### TOP
Used to limit number of rows returned
•Can specify a number of rows or percent
•TOP is typically used with ORDER BY

### Ranking functions
ROW_NUMBER
–Returns the row number
•RANK
–Returns ranking based on ORDER BY statement
–Ties skip to the next number
•DENSE_RANK
–Returns ranking based on ORDER BY statement
–Ties don’t advance the rank number
•NTILE(x)
–Breaks rows into equal sections
–x is the number of sections

 

### Paging
Used to retrieve portions of data
•FETCH and OFFSET
–FETCH indicates the number of rows to retrieve
–OFFSET indicates the number of rows to skip
•Restrictions
–ORDER BY is required
–TOP is not allowed
SELECT <columns>
FROM <tables>
ORDER BY <columns>
OFFSET x
FETCH NEXT 5 ROWS ONLY;


### Distinct
Removes duplicate values
•The entire row must be a duplicate
•Will cause a sort of the data
–Impacts performance


## Built-in functions

Performance issues
–SQL may need to process each row individually
•"Hidden cursor"
–Avoid passing columns into functions in SELECT statements
•Basically never do this on the WHERE line

### ISNULL
–Two parameters
•Returns the first parameter if it is not null
•Returns the second parameter if the first parameter is null
•COALESCE
–Multiple parameters
•Returns the first parameter SQL Server finds that is not null
–More flexible and easier to read

### GETDATE()
–Returns the current server date
•GETUTCDATE()
–Returns the server date normalized to UTC
•DATEPART()
–Returns a part of a date
–Related to DAY(), MONTH(), and YEAR()

### DATEDIFF()
–Difference between two dates
•DATEADD()
–Add time to a date
•ISDATE()
–Determines if value is a date

### DATEFROMPARTS()
–Builds a day from a provided year, day, month
•TIMEFROMPARTS()
–Builds a time from provided hour, minute, second
•EOMONTH()
–Provides the last day of the month for the provided date
•PARSE()
–Converts string to a date
CHARINDEX()
–Searches for one string inside another
•PATINDEX()
–Supports pattern searches inside of a string, ‘%speaker%’
•LEFT() and RIGHT()
–Returns characters from the left or right side of a string
•LTRIM() and RTRIM()
–Removes strings whitespace from a string
•LEN()
–Returns the length of a string
CONCAT()
–Concatenates strings
•FORMAT()
–Converts value to a string using .NET formatting


CONVERT(type, value, format)
–Accepts a formatting option
•CAST(value AS type)

•http://msdn.microsoft.com/en-us/library/ms187928.aspx

•TRY_PARSE()
–More flexible when converting strings to data types
–Returns NULL if parse fails
•TRY_CONVERT()
–Same as CONVERT(), only returns NULL if conversion fails

•CHOOSE()
–Returns a list item based on its location
–First parameter is index
–Next parameters are the list
•IIF()
–Instant if
–Three parameters:
•Boolean expression
•Return value if true
•Return value if false


## Query optimization
### Index
Clustered index
– Order in which the data in the table is stored
– Page number in a book

•Nonclustered index
– Copy of data sorted for queries
– Index in the back of a book
•Contains a pointer back to the original content

### Query optimizer
Execution plan

Scan
–Examines every row in the table or index
–Imagine searching for all people named Christopher in the phonebook
•Seek
–Able to follow path directly to the desired data
–Imagine searching for all people with a last name of Harrison in the phonebook


Merge Join
–Data is presorted
–Most efficient join
•Loop Join (Nested Loops)
–One table is much smaller than the other
–Smaller table is searched for values that match larger table
•Hash Join
–Large tables and unsorted data
–Slowest type of join


### Query hint
Control how SQL Server will execute a query
– Which index to use
– How to lock data
•Typically avoided


### Dynamic Management Objects
•Used to see what's going on behind the scenes
– Find out how SQL Server is using resources
– Identify problem queries
•Views are treated like tables
•Functions accept parameters
–Parameters are often other database objects

sys.dm_db_index_usage_stats
–Determine which indexes are (or aren’t) being used
•sys.dm_db_mising_index_details
–Determine what indexes SQL Server thinks should be added
•sys.dm_db_index_physical_stats
–Determine how an index is using disk space
sys.dm_tran_database_transactions
–Something
•sys.dm_tran_session_transactions
–Something
•sys.dm_tran_locks
–Something else

### Dynamic SQL
Allows for the creation of SQL on the fly
–Can enable a more flexible application
•Concerns
–Performance
•Something
–Security
•SQL Injection Attacks
–Allows an attacker to inject their on SQL statements
–Use parameters

Always validate parameters
 


## Modifying Data
INSERT, UPDATE, DELETE
Be careful!
Tips to avoid disasters
– Always start with a SELECT statement
•SELECT will never modify data
– Always add a WHERE statement
•Not a bad idea to start with it
– Comment code that modifies the database
•Avoids "accidental F5"

Use DEFAULT and NULL for default and null values


-- Only deletes contacts that
-- exist in BadContacts
```shell script
DELETE FROM Contacts
FROM Contacts c
INNER JOIN BadContacts bc
ON c.ContactID = bc.ContactID
```


### TRUNCATE
Deletes all rows from table
•Does not "log" operation
•Not available for tables serving as a parent for child tables
–Could not truncate Customers table if Orders had a foreign key relationship for Customers
•TRUNCATE <table>

Advanced Data Modification

OUTPUT concepts
•"Localized Trigger"
•Useful for logging or returning modified data

Retrieving modified data
•Special tables
–Identical to target table
•INSERTED
–INSERT Statement
•New rows
–UPDATE Statement
•New values
•DELETED
–DELETE Statement
•Deleted rows
–UPDATE Statement
•Original values
 

### Merge concepts
Combine data from two tables
•Determine how to handle conflicts
– Update existing data
– Insert missing data

•MERGE <TARGET>
–Where to place the data
•USING <SOURCE>
–Where to get the data from
•ON
–The join to determine matches
WHEN MATCHED THEN
–Operation for existing data
WHEN NOT MATCHED [BY TARGET] THEN
–Operation for missing data
–Can have optional parameter applied to filter target rows
•WHEN NOT MATCHED [BY SOURCE] THEN
–Operation for missing data
–Can have optional parameter applied to filter source rows
OUTPUT
–Retrieve modified data
–$action provides the action taken
•Insert
•Delete
 

