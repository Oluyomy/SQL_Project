What are your risk areas? Identify and describe them.
1:Data integrity and reliability is one of my risk areas because of the validity of the ecommerce database. This is due to high levels of inconsistency, missing rows,duplicate and invalid data present in the database.
2. Reliability of this ecommerce database: During this analysis, lack of proper backup and recovery mechanisms experienced when converting some data_types lead to the  loss of some code which I was working on .
Also when deleting, updating in the course of execution, pdAdmin shuts down causing  lost codes that are not saved in the process.
3: Inconsistent error during execution of codes, including inadequate error handling are  risk areas. I had numerous syntax errors but later rectified them.

QA Process:
Describe your QA process and include the SQL queries used to execute it.

Data validation is for integrity and reliability
When validating, we make sure that our data is
●	complete (i.e. no blank or null values)
●	unique (i.e. no duplicate values)
●	consistent with what we expect (eg. a decimal between a certain range).
-To prepare my ecommerce database by creating a new all_sessions11 table  entirely eliminating irrelivant columns. 
-I created ERD to establish relationship between all the tables ,other steps taken include.  

STEP1:
Data Assertion ; I looked for  problems in a dataset,identify missing values and duplicates.
  Code used for assertion :

...SQL
SELECT  fullvisitorid, channelgrouping
FROM all_sessions11
WHERE fullvisitorid is null
 If it returns 0 passed, if >=1 assertion failed
...

STEP2:Checking rows: missing and null values.

...SQL
SELECT fullvisitorid
FROM all_sessions11
WHERE  city IS NULL
OR NOT country IN (‘Japan’, ‘United States’)
...

STEP3:Checking for unique fields

...SQL
SELECT
    visitid    SUM(1) AS count
FROM analytics
GROUP BY 1
HAVING count > 1
...

STEP4: 
QA.md was prepared as documentation.
