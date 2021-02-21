SQL server performance
=======================
Course: What Every Developer Should Know About SQL Server Performance, 2016

## introduction

http://downloadsqlserverexpress.com/
http://buildingbettersoftware.blogspot.com/2016/02/sample-database-for-what-every.html 

SQL Server clusterd index structure


 

## Analyzing SQL Statements for Performance
Execution plan (^L)
### Case study 1
```shell script
SELECT c.DepartmentCode, c.CourseNumber, c.CourseTitle, c.Credits, cd.Grade
FROM CourseEnrollments cd
INNER JOIN CourseOfferings co
	ON cd.CourseOfferingId = co.CourseOfferingId
INNER JOIN Courses c
	ON co.DepartmentCode = c.DepartmentCode
	AND co.CourseNumber = c.CourseNumber
WHERE cd.StudentId = 29717;
```


SET STATISTICS IO ON
SET STATISTICS TIME ON
Run the sql, then check the "Messages"
	CourseOfferings: Logical reads 83
	CourseEnrollments: logical read 12023 (=> not efficient sql statement)
Each logical read represents 8KB data.

Improve:
```shell script
CREATE NONCLUSTERED INDEX IX_CourseEnrollments_studentId
ON CourseEnrollments (StudentId)
```


### Case study 2
```shell script
SELECT co.*
FROM CourseOfferings co
LEFT OUTER JOIN CourseEnrollments ce
	ON co.CourseOfferingId = ce.CourseOfferingId
WHERE co.TermCode = 'SP2016'
AND ce.CourseOfferingId IS NULL


SELECT co.*
FROM CourseOfferings co
WHERE NOT EXISTS (
	SELECT 1 
	FROM CourseEnrollments ce
	WHERE ce.CourseOfferingId = co.CourseOfferingId
)
AND co.TermCode = 'SP2016'
```


If subquery's a entry exist, jump out

 
Table scan and Hash Match are expensive.

## Building Effective Indexes
- Clustered index: store the data for the table, typically organized by the primary key, only one allowed.
- Non-clustered index: all other indexes, data organized by index key, contains pointers to matching rows. Multiple allowed.
Scan => seek (tree)
Add indexes for where clause criteria
Each index support each use case with different where clause
Most common columns as the first index, 2nd most as the 2nd index.
Index foreign key columns

```shell script
CREATE INDEX IX_Applicants_FirstNameLastName
	ON Applicants (FirstName, LastName, State)

SELECT *
	FROM Applicants
	WHERE LastName = 'Davis'
		AND State = 'CO'
Index scan, Logical reads > 2500, "first name" is not in WHERE
CREATE INDEX IX_Applicants_FirstNameLastName
	ON Applicants (LastName, FirstName, State)
```
Now it's index seek.

## Index selectivity
How many or how few rows correspond to each index key value
Students: 120,000, distinctive names: 107,000 => good ratio to index on (lastName, firstName)
Force use index (not recommended)
`SELECT * FOM Students WITH (Index(IX_Students_State))`
This is better:
CREATE INDEX IX_Students_StateCity ON Students (State, City)

## Selectivity and like
`LIKE '%harri'` // index is not used
`LIKE 'T%'` // this affect the selectivity, if selectivity is low, SQL server will use index scan

## Functions in where clause
If function is on the left of WHERE clause, index is not used
```shell script
SELECT * FROM Applicants
	WHERE substring(email, 0, charindex('@', email, 0)) = 'LouiseJSmith';
```

Solution: add a computed column
ALTER TABLE Applicants ADD EmailLocalPart AS substring(email, 0, charindex('@', email, 0))

## Covering index
```shell script
CREATE INDEX IX_Students_Email ON Students (Email) INCLUDE (lastName, firstName)
	// lastName, firstName is not part of index, but included.

SELECT Email, firstName, lastName 
FROM students
WHERE email = 'PaulDWilliams@gustr.com
```
SQL Server is able to find all the data for the query in the index itself. 
This avoids needing a key lookup operation to find the data row in the table.


Caution: consider a covering index when you only need to add one or two columns as include columns 
to give performance boost to a key query.

DO NOT over index: maintenance cost
DML statement: Insert, update, delete

### Finding unused indexes using DMVs
```shell script
SELECT 
  OBJECT_NAME(s.object_id) AS TableName,
  i.name As IndexName,
  i.type_desc as IndexType,
  user_seeks + user_scans + user_lookups As TotalUsage,
  user_seeks,
  user_scans,
  user_lookups,
  user_updates,
FROM sys.dm_db_index_usage_stats s
RIGHT OUTER JOIN sys.indexes i
  ON s.[object_id] = i.[object_id]
  AND s.index_id = i.index_id
WHERE s.database_id = DB_ID()
  AND i.name IS NOT NULL
  AND OBJECTPROPERTIES(s.[object_id], 'IsMsShipped') = 0
ORDER BY s.object_id, s.index_id 
```

## Finding performance bottleneck
Dynamic management views (DMV)
View server state permission is required to access DMV

Sessions, client, connections
 

Current executing statement

Worst performance statement

Index recommendation

Index analysis
 

## Capturing What Your Application is Doing Inside SQL Server
What statement is running? In what order?
SQL Profiler (2008 & before), SQL SERVER Extended Events (2012 & later)
Production tracing like requires DBA

## Applying Common Performance Practices
Parameterized sql
 
Protects against sql injection attacks
Performs faster: cached statement (similar execution plan)
ORM like hibernate automatically parameterize SQL they generate.

### Stored procedures
Faster? Only than dynamic SQL
Stored procedures are similar to parameterized SQL, due to cached execution plan

### Auto-commit
Default is on.
Execute queries (insertion) in batch
Transaction Commit() the batch: slightly better

### ORM
Increase productivity, abstract
Less control of what's happening
Not good for complex queries

### N+1 selects problem
https://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem-in-orm-object-relational-mapping

Records are being loaded individually because they are being lazy loaded.
Eager loading is better in this case.
Watch for N+1 problem any time you are loading child objects.
Using tracing to understand what's going on.

