Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
...SQL
ALTER TABLE public.all_sessions11
    ALTER COLUMN "totaltransactionrevenue" TYPE integer USING ("totaltransactionrevenue"::integer);
UPDATE all_sessions11
SET "totaltransactionrevenue" = "totaltransactionrevenue" / 1000000;
SELECT *FROM all_sessions11

SELECT city, country, SUM("totaltransactionrevenue") as transactionrevenue
FROM public.all_sessions11
WHERE "totaltransactionrevenue" IS NOT NULL
GROUP BY city, country
ORDER BY transactionrevenue DESC;
....



Answer: 21 cities, the highest is united states 4650 but the city was (not available in demo data set) lowest was in Zurich city in Switzerland and transaction revenue is 16  (1000000)million
 BUT when i removed 'not available in demo data_set',in the city using
...SQL
SELECT city, country, SUM("totaltransactionrevenue") as transactionrevenue
FROM public.all_sessions11
WHERE "totaltransactionrevenue" IS NOT NULL AND city<> ('not available in demo dataset')
GROUP BY city, country
ORDER BY transactionrevenue DESC;
...
RESULTS====20 rows  with San Francisco United States 1248  generating  the highest level of transaction revenue


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
...SQL
SELECT a1.city,a1.country,p.name,AVG(p.orderedquantity) as averageordered
FROM products p
JOIN all_sessions11 a1 ON  p.sku=a1.productsku
GROUP BY a1.city,a1.country,p.name,p.orderedquantity
ORDER BY p.orderedquantity DESC
...


Answer:Answer:5984 rows   ,
 highest=city(not set), country(Taiwan) product(kickball), averageordered=15170
Lowest=city-Yokohama, country-Japan, product-men’s short sleeve Hero Tee HEATHER, average=1



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
...SQL
SELECT city, country, v2productcategory, COUNT(*) AS row_count
FROM all_sessions11
GROUP BY city, country, v2productcategory
ORDER BY row_count DESC
...

Answer
RESULT Answer: product category ,(  Home/shop by Brand/Youtube/ )is the highest with 577 count , country is United States, But the  city  = 'not available  in demo dataset,.
=== Parttern: most productcategory   are categories of product ordered  by visitors in United States but ‘not available in demo dataset in the city  is more than the  that of other countries

ALSO where there is a clause of city<>'not available in demo dataset' the result changes.

..SQL
SELECT city, country, v2productcategory, count(v2productcategory) as category
FROM all_sessions11
WHERE city is not NULL and city != 'not available in demo dataset'
AND v2productcategory != '(not set)' and v2productcategory != '${escCatTitle}'
GROUP BY  v2productcategory,city, country
ORDER BY category desc;
...
Result: city=Mountain view, country:united states , productcategory=Home/Nest/Nest-USA-92
1681 rows



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
...SQL
SELECT s.name,MAX(p.orderedquantity) AS top_selling,a1.city,a1.country
FROM all_sessions11 a1
JOIN products P ON p.sku= a1.productsku
JOIN sales_report s ON  p.stocklevel = s.stocklevel
WHERE P.orderedquantity <> 0
GROUP BY  s.name, P.orderedquantity,a1.city,a1.country
ORDER BY P.orderedquantity DESC
....


Answer:Answer: returned 10401
— The product requested most is  kick ball, followed by (22 oz Water Bottle)
-	Most cities bought the same amount of it, 15170 but in total, visitors in the United states  ordered the most as a country.
-	Pattern worthy of nothing is that most city ordered the same amount of  kickball.
-the same pattern operate in most cities and countries buying 22 oz Water Bottle(8942)
-followed by sun glasses and Android women’s short sleeve Hero Tee Black been the least in all cities and countries.


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
...SQL
SELECT city, country,totaltransactionrevenue
FROM all_sessions11
WHERE totaltransactionrevenue > 0
GROUP BY totaltransactionrevenue ,city,country
ORDER BY totaltransactionrevenue DESC
...


ANSWER: In summary, the revenue generated from the United States from sales of  products Is more than any other country and the impact is numerous .  
The  high ecommerce revenue generation  indicates a thriving  online business environment that will affect the economic growth of the country positively.
. It will also generate employment opportunities, stimulate entrepreneurship, and attract investment in the ecommerce sector which in turn will also lead to Increased Tax Revenue: i.e. increased tax collection for the government, This will be used  to fund public services, infrastructure development, and social welfare programs.
Other areas include  job creation,consumer convenience, digital transformation etc
Overall, a high ecommerce revenue generated by the United States, brings economic benefits, technological advancements, job opportunities, and enhances the country's competitiveness in the global market. It shows the successful adoption of digital commerce and its positive impact on various aspects of society and the economy.








