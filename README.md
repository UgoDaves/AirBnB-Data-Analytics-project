![airbnb-hult-research-2](https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/c590446f-4803-47fb-b5bd-da4b7bc89609)
# AirBnB-Data-Analytics-project
As part of a strategic initiative, a valued client within the real estate sector has entrusted me with the task of conducting a thorough analysis of Airbnb listings in the vibrant Dallas, Texas area. The objective is to provide insights that will empower our client to make successful investment decisions within the Airbnb ecosystem.
In this project, I would be analyzing AirBnB listing dataset specifically in Dallas, Texas area to gain date driven insight, on basically the factors that may contribute to having a successful AirBnB listing.

## Ask Phase
1. How do we make accurate decisions on the best approach to take in order to create successful AirBnB listings? 
My strategy includes:
-  Make a list of the top ten most successful hosts, and analyze their overal revenue.
-  Analyzing Districts and areas with the higest turn out.
-  Identify the most popular accomodation category.

## Prepare Phase
1. Discription of all datasources used:
The dataset used for this project can be found [here](http://insideairbnb.com/get-the-data/), a website called 'Inside Airbnb' a third-party public data-source. It consists of 18 columns ranging from the listing ID to license. Since it does not include the demograpic details of hosts, it is hard to determine if it consists of any bias. The dataset policy can be accessed [here](http://insideairbnb.com/data-policies)



## Process Phase
Documentation of any cleaning or manipulation of Data.
#### Import Data into Power Query:
Utilized Power Query to import the raw dataset, providing a structured environment for subsequent data cleaning.

#### Remove Unnecessary Columns:
- Identified and deleted the "neighbourhood" "id" and "license" columns, as they were deemed irrelevant for the analysis.
  
#### Separate Combined Columns:
- Addressed data quality by breaking down information that was originally combined in a single column. Specifically, separated the "rating," "number of beds," "bedrooms," and "baths" into distinct columns for improved clarity and analysis.
  
#### Remove Empty Columns:
- Identified and removed any empty or redundant columns to streamline the dataset.
  
#### Text Reduction for SQL Analysis:
- Recognizing the importance of efficient SQL analysis, reduced the length of text within the dataset to enhance readability and simplify queries.

#### Imported data into Postgresql
``` sql
CREATE TABLE airbnb (
id BIGINT,
host_id BIGINT,
host_name VARCHAR (40),
accomodation_type TEXT,
listing_type TEXT,
bedrooms SMALLINT,
beds SMALLINT,
baths NUMERIC (2,1),
rating NUMERIC (3,2),
district SMALLINT,
latitude NUMERIC (12,10),
longitude NUMERIC (12,10),
price INT,
min_nights INT,
num_of_reviews INT,
last_review DATE,
reviews_per_month NUMERIC (3,2),
host_listings_count INT,
availability_365 INT,
num_of_reviews_lmt INT
);

ALTER TABLE airbnb
DROP COLUMN id;
```
## Analyze Phase
A summary of my analysis
```sql
--1) In this dataset, we have a total of 4,255 hosts
SELECT COUNT(host_id) AS total_hosts
FROM airbnb;

--2) The number of distinct hosts that made a listings is 1,965
SELECT COUNT(DISTINCT(host_id))
FROM airbnb;

SELECT COUNT(DISTINCT(host_name))
FROM airbnb;

--3) The top ten listings with the potential highest revenue are 
SELECT COUNT(host_id) AS num_of_listings,
host_id, 
host_name,
SUM(price*min_nights) AS rev_per_booking
FROM airbnb
GROUP BY 2,3
ORDER BY rev_per_booking DESC
LIMIT 10;

/*4) Listing type, accomodation type, bedroom, beds, baths, 
District and locations of where the listings are located, of top 10. */
SELECT host_id,
host_name,
accomodation_type,
listing_type,
bedrooms,
beds,
baths,
district,
latitude,
longitude
FROM airbnb
WHERE host_id IN (108514926,112593570,104309976,211225279,329464978,471536148,305350123,
67281738,9124824,308850424,23916014,47763153,62395523,378270433,156543716,
462299527,24921413,314010499,65241900,35999704);
```

