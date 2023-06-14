# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
To transform and analyze the ecommerce database  enabling businesses to gain insights into sales trends, visitors behavior, and other key performance indicators for informed decision-making and strategic planning. 
●	To Extracting the data to database 
●	To Cleaning and transforming the data
●	To developing insights into the trends  and patterns of the database

## Process
.Download the csv data files.
. Create ecommerce database.
.Import the data into pgAdmin.
.Explore and examine the columns,data_types,pattern and consistencies,looking for how to clean and transform the data for meaningful use.
    1.For each of the 5 tables, I clean the data .
    2.by removing duplicates in some columns,
    3.Changed  some data_types into standard formats (eg timeonsite from integer to timestamp).
    4.corrected inconsistent errors in the data.
    5.Added a new table called  adjunitcost by  dividing unitcost /1000000.
     6.Removed some null columns and did a general cleaning for data integrity and reliability.
.Create an ERD to establish the relationship between all the tables indicating the primary and foreign keys. 
.Retrieved specific data sets for the queries given  for proper querying execution.
. QA process


## Results
1.San Francisco in United States generated the highest level of transaction revenue. 1248
2. Taiwan have the highest average number  of product ordered.(men’s short sleeve Hero Tee HEATHER), while Yokohama city in Japan has the lowest
3.The product category (  Home/shop by Brand/Youtube/) is the highest   ordered with 577 count by visitors from country United States but the  city is 'not available  in demo dataset'.
 
4.The product requested most is  kick ball, followed by (22 oz Water Bottle) and most cities bought the same amount of it, 15170 but in total, visitors from the United states ordered the most as a country.
-	Pattern worthy of nothing is that most city ordered the same number of kickball.

5.The revenue generated from the United States from sales of products is more than any other country and the impact is numerous .  
The  high ecommerce revenue generation  indicates a thriving  online business environment that will affect the economic growth of the country positively,generate employment opportunities, stimulate entrepreneurship, and attract investment in the ecommerce sector which in turn will also lead to Increased Tax Revenue: i.e. increased tax collection for the government, This will be used  to fund public services, infrastructure development, and social welfare programs.

## Challenges 
.Most columns  contain null values and need to be cleaned. Eg ‘productrefund amount’.
.Cleaning is time consuming.
.Ambiguity in data in some columns eg(fullvisitorid) 18 numbers each.
.Unmatching columns having the same name but different data_type found in all_sessions and analysis(timeonsite).
.Some columns seem irrelevant to the ecommerce data. 
.Most rows are unfixed in Unitprice column in analytics table are ‘0’.


## Future Goals
.I will clean up the data extensively.
.Take out time to do more analysis  for more informed decision on ecommerce .


