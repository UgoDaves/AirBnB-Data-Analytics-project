![airbnb-hult-research-2](https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/c590446f-4803-47fb-b5bd-da4b7bc89609)
# AirBnB-Data-Analytics-project
I have been invited to join a real estate company as a data analyst, where our focus is on entering the Airbnb market by listing houses in the Dallas, Texas area. My role involves conducting a thorough analysis to leverage data to make informed decisions and enhance the company's success in this new venture.

## Ask Phase
1. How do we make accurate decisions on the best approach to take in order to create successful AirBnB listings? 
My strategy includes:
-  Make a list of the top ten most successful hosts, and analyze their overal revenue.
-  Analyzing areas with the higest turn out.
-  Identify the most popular accomodation category.
-  Analyze the average number of bedrooms, beds and baths.

## Prepare Phase
1. Description of all datasources used:
The dataset used for this project can be found [here](http://insideairbnb.com/get-the-data/), a website called 'Inside Airbnb' a third-party public data-source. It consists of 18 columns ranging from the listing ID to license. Since it does not include the demograpic details of hosts, it is hard to determine if it consists of any bias. The dataset policy can be accessed [here](http://insideairbnb.com/data-policies)



## Process Phase
Documentation of any cleaning or manipulation of Data: I used PowerQuery, Postgresql and Microsoft Power BI for visualization.
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
#### Imported results from SQL queries into Power Bi
- Established data model by creating relationships for proper visual analysis
<img width="737" alt="datamodel" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/894b17d5-f3d8-47b4-8c52-bd6f7ff3bb81">


## Analyze Phase
A summary of my analysis
```sql
-- In this dataset, we have a total of 4,255 hosts
SELECT COUNT(host_id) AS total_hosts
FROM airbnb;

-- The number of distinct hosts that made a listings is 1,965
SELECT COUNT(DISTINCT(host_id))
FROM airbnb;

SELECT COUNT(DISTINCT(host_name))
FROM airbnb;

--Number of Districts(1-14)
SELECT DISTINCT district
from airbnb
ORDER BY 1

-- The top ten listings with the potential highest revenue are 
SELECT COUNT(host_id) AS num_of_listings,
host_id, 
host_name,
SUM(price*min_nights) AS rev_per_booking
FROM airbnb
GROUP BY 2,3
ORDER BY rev_per_booking DESC
LIMIT 10;

/* Listing type, accomodation type, bedroom, beds, baths, 
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
- In the absence of revenue information within the dataset, I derived an estimate by calculating the product of the minimum stay duration and the corresponding price. This method allowed me to approximate the potential revenue associated with each listing. This is the list of the top ten highest earners by revenue.
<img width="438" alt="revbyhost" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/1169507d-0592-459d-8d5d-6ead78580c31">


- I analyzed the average number of bedrooms, beds and baths of the top ten highest earners.
<img width="481" alt="avg_bed_baths" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/77226d07-679d-453d-bc30-699a33c2b5f2">


- This is a breakdown of the accomdation and listing type.
<img width="945" alt="listing type" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/28b88a8e-2b83-49b2-8781-50343bb923d0">

This is a map containing listings of all ten hosts.

<img width="520" alt="map" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/4811bfae-fd2c-4cbe-ad68-d0093a139398">


### Findings:
- The available listing types include Condos, Homes, Rental units, Serviced apartments, and Townhouses. Rental units emerge as the most prevalent, totaling 270 listings, with Dalls being the originator of 138 of these listings.

<img width="523" alt="listing_type" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/e5f1b54e-548d-404d-8b2e-d388663998f1"> 
<img width="519" alt="dalls_listingtype" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/971c05b2-7943-4859-be40-ae15c86455de">

- The analysis indicates a potential correlation between success and the number of rental units listed. However, an interesting observation is that Libby, with only three listings, achieved success, suggesting that the number of listings alone may not be the sole factor influencing performance.

<img width="464" alt="corellation" src="https://github.com/UgoDaves/AirBnB-Data-Analytics-project/assets/152723434/d9b9bce9-1196-45c1-b326-0beb49a9d4bd">


