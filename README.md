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
1. Documentation of any cleaning or manipulation of Data.
### Import Data into Power Query:
Utilized Power Query to import the raw dataset, providing a structured environment for subsequent data cleaning.

### Remove Unnecessary Columns:
- Identified and deleted the "neighbourhood" "id" and "license" columns, as they were deemed irrelevant for the analysis.
  
### Separate Combined Columns:
- Addressed data quality by breaking down information that was originally combined in a single column. Specifically, separated the "rating," "number of beds," "bedrooms," and "baths" into distinct columns for improved clarity and analysis.
  
### Remove Empty Columns:
- Identified and removed any empty or redundant columns to streamline the dataset.
  
### Text Reduction for SQL Analysis:
- Recognizing the importance of efficient SQL analysis, reduced the length of text within the dataset to enhance readability and simplify queries.

```CREATE TABLE airbnb (
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
)
```
