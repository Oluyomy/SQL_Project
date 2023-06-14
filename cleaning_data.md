What issues will you address by cleaning the data?
Issues adressed include the following
●	There are duplicate data in the primary keys of the all_sessions, analytics and product tables.
●	Null values in the all_sessions and analytics table.
●	Data_type is inconsistent in all_sessions, analytics tables
●	Incorrect formats  foun in all_sessions table.


Queries:
Below, provide the SQL queries you used to clean your data.
STEP1: To make assertions, i checked for validity of all_sessions table.

...SQL
SELECT DISTINCT(fullvisitorid),visitid,productquantity,date,type,timeonsite
FROM all_sessions
...

... SQL
SELECT fullvisitorid,visitid,productquantity,date,type,timeonsite
FROM all_sessions
....
Returned 15134 rows
====Total row returned =794  are duplicates out of 15134

 SOLUTION

STEP2:I created a new table and named it as all_sessions11 to eliminate null columns

...SQL
CREATE TABLE all_sessions11 AS
	SELECT fullvisitorid,channelgrouping,time,country,city,transactions,
	timeonsite,pageviews,date,visitid,type,productquantity,productprice,productsku,	v2productname,v2productcategory,pagetitle,pagepathlevel1,ecommerceaction_type,ecommerceaction_step,ecommerceaction_option
FROM all_sessions
...

2:To check for validity  in table, I usedthis code.
...SQL
SELECT DISTINCT(fullvisitorid),visitid,productquantity,date,type,timeonsite
FROM all_sessions11
...
==returned=14569 rows

...SQL
SELECT fullvisitorid,visitid,productquantity,date,type,timeonsite
FROM all_sessions11
....
Returned15134
====Total row returned shows794  are duplicates out of 15134

  SOLUTION : code to remove duplicates

...SQL
DELETE FROM all_sessions11
WHERE fullvisitorid NOT IN (
    SELECT MIN(fullvisitorid)
    FROM all_sessions11
    GROUP BY fullvisitorid,channelgrouping,time,country,city,totaltransactionrevenue,transactions,
	timeonsite,pageviews,date,visitid,type,productquantity,productprice,productsku,	v2productname,v2productcategory,pagetitle,pagepathlevel1,ecommerceaction_type,ecommerceaction_step,ecommerceaction_option
);
....
To delete rows with no primary key

...SQL
DELETE FROM all_sessions11
WHERE fullvisitorid IN (
    SELECT fullvisitorid
    FROM all_sessions11
    GROUP BY fullvisitorid
    HAVING COUNT(*) > 1
	);
    .....
====13429 rows



STEP3= To check for duplicates in analytics.

for analytics duplicates

...SQL
SELECT visitid,date,userid,timeonsite
FROM analytics
...
 returned 4301122 rows
...SQL
SELECT DISTINCT(visitid),date,userid,timeonsite
FROM analytics
.....
==IT RETURENED 150403 meaning there is duplicates

To remove duplicates from analytics
...SQL
DELETE FROM analytics
WHERE fullvisitorid NOT IN (
    SELECT MIN(fullvisitorid)
    FROM analytics
    GROUP BY visitnumber,visitid,visitstarttime,
	date,fullvisitorid,userid,channelgrouping,socialengagementtype,
	units_sold,pageviews,timeonsite,bounces,pageviews,revenue,unitprice
);
...

To remove duplicate from products table, i used
...SQL
SELECT sku,name,orderedquantity
FROM products
...
====outcome=1092
...SQL
SELECT DISTINCT(sku),name,orderedquantity
FROM products
...
===outcome=1092 meaning no duplicates

Thre are no  duplicate  sales_by_sku table
No duplicates

Toremove duplicates from sales_reports
...SQL
DELETE FROM sales_report
WHERE productsku NOT IN (
    SELECT MIN(productsku)
    FROM sales_report
    GROUP BY productsku,total_ordered,name,stocklevel,restockingleadtime,sentimentscore,sentimentmagnitude,ratio
);
...

STEP4: IDENTIFYING MISSING AND EXTREME VALUES
 
 For country 
 ...SQL
SELECT fullvisitorid,visitid,country,city
FROM all_sessions11
WHERE country like '(not set)'
...
====Returned 21 rows
For country and city  that is ‘(not set)’
...SQL
SELECT fullvisitorid,visitid,country,city
FROM all_sessions11
WHERE country like '(not set)'
AND city LIKE ‘(not set)’
...
 ===returned 20 rows

For city not available in demo dataset
...SQL
SELECT fullvisitorid,visitid,country,city
FROM all_sessions11
WHERE city like 'not available in demo dataset'
...
=== returned 7449 rows

For product price
...SQL
SELECT fullvisitorid,productprice, productquantity
FROM all_sessions11
WHERE productprice='0'
ORDER BY productquantity
...
===It returned 347 rows

To change datatype to correct form eg
 timeonsite to timestamp
 ...SQL  
ALTER TABLE all_sessions11
ALTER COLUMN timeonsite TYPE timestamp USING to_timestamp(timeonsite);
/ //for analytics visitstarttime
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE timestamp USING to_timestamp(visitstarttime);
...

To change time  to hours HH:MM:SS I used
...SQL
ALTER TABLE all_sessions11
ALTER COLUMN time
TYPE VARCHAR
USING LPAD(time::VARCHAR, 6, '0');
UPDATE public.all_sessions11
SET time = SUBSTR(time, 1, 2)||':'||SUBSTR(time, 3, 2)||':'||SUBSTR(time, 5, 2);
UPDATE public.all_sessions11
SET time = TIME '00:00:00' + 
           INTERVAL '1 hour' * CAST(SUBSTR(time, 1, 2) AS INTEGER) +
           INTERVAL '1 minute' * CAST(SUBSTR(time, 4, 2) AS INTEGER) +
           INTERVAL '1 second' * CAST(SUBSTR(time, 7, 2) AS INTEGER);
ALTER TABLE public.all_sessions11
ALTER COLUMN time TYPE TIME USING time::TIME;
...


To change unitprice to unit cost/ 100000
...SQL
SELECT CAST(unitprice/1000000.0 AS DECIMAL(10, 2)) AS unitprice, unitprice
FROM analytics;
...
====returned a numeric data not integer with 2decimal places not rounded up
Rows returned 1444

For productprice , cast to numeric
...SQL
SELECT CAST(productprice/1000000.0 AS DECIMAL(10, 2)) AS productprice, productprice
FROM all_sessions11;
...
