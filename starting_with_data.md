Question 1: 
Find out the visitors from United states that  made organic searching.
on the sites


SQL Queries:
...SQL
SELECT fullvisitorid,country,channelgrouping
FROM all_sessions11
WHERE channelgrouping IN('Organic Search')
AND country IN ('United States')
...

Answer: 3771 visitors from United States ma an Organic searching in  the sites.



Question 2:  Find out how many visitors  made an order with their fullvisitorid.

SQL Queries:
...SQL
SELECT COUNT(ss.total_ordered) AS total_ordered, a1.fullvisitorid
FROM all_sessions11 a1 
INNER JOIN sales_report ss On ss.productsku = a1.productsku
WHERE total_ordered = 0
GROUP BY a1.fullvisitorid
.....

Answer: 2151  visitors did not make any order.



Question 3: 
How many people from New York city  made a  direct serch on the sites

SQL Queries:
...SQL
SELECT fullvisitorid,country,channelgrouping,city
FROM all_sessions11
WHERE channelgrouping IN('Direct')
AND country IN ('United States')
AND city IN ('New York')
...

Answer: 126  visitors from New York made a direct searching on the site.



Question 4:  No os transactions entered by the visitors.

SQL Queries:

...SQL
SELECT SUM(transactions) AS totaltransactions
FROM all_sessions11
...

Answer: 72 transactions was made by visitors on the sites.



Question 5: 

SQL Queries:

Answer:
