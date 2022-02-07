---
output:
  always_allow_html: true
  author: Sylvia K
  date: 2022-02-07
  excerpt: test
  knit: "(function (inputFile, encoding) { rmarkdown::render(inputFile,
    encoding=encoding, output_dir= “\\~/selgik.github.io/\\_posts”)})"
  layout: post
  md_document:
    preserve_yaml: true
    variant: gfm
  tags:
  - jekyll
title: SQL/Tableau Code Note
---

## Overview
### Information about data source
* Data source: [NYC 311 Dataset](https://console.cloud.google.com/marketplace/product/city-of-new-york/nyc-311?project=capable-blend-330013)  
* Description: This data includes all New York City 311 service requests from 2010 to the present, and is updated daily.311 is a non-emergency number that provides access to non-emergency municipal services.

### Project Workflow
* Clean and review data in SQL -> visualize findings in Tableau

## Part 1: SQL Code Review 
### Understand the Dataset 


#### Question 1: Get summary of data
~~~sql
SELECT 
    unique_key, 
    created_date,
    closed_date,
    agency,
    agency_name,
    complaint_type,
    location_type,
    incident_address,
    address_type,
    city,
    status,
    resolution_description
FROM bigquery-public-data.new_york_311.311_service_requests
LIMIT 10 
~~~


#### Question 2: Check completeness of data
~~~sql
SELECT closed_date, status
FROM bigquery-public-data.new_york_311.311_service_requests
WHERE status = "Closed" 
  AND closed_date IS NULL
~~~
-> Finding: There are 2283 cases where status is "Closed" but no closed_date is provided.


#### Question 3: How many status type are there? 
~~~sql
SELECT DISTINCT status
FROM bigquery-public-data.new_york_311.311_service_requests
~~~
-> Finding: There are 13 types. Status types to be considered when visualiziaing dataset are: Cancel/Cancelled, Closed, Rest.


#### Question 4: What is the percentage of each status?
~~~sql
WITH temp AS (
    SELECT 
        status, 
        COUNT(status) AS counts,
        (SELECT COUNT(*) FROM bigquery-public-data.new_york_311.311_service_requests) AS total_counts
    FROM 
        bigquery-public-data.new_york_311.311_service_requests
    GROUP BY
        status
    )

SELECT 
    status,
    ROUND ((counts/total_counts)*100,2) AS percentage_total
FROM
    temp
ORDER BY 
    percentage_total DESC
~~~
-> Finding: Around 96% of cases are closed. 


#### Question 5: Ensure that all cases are assigned with its status
~~~sql
SELECT status 
FROM bigquery-public-data.new_york_311.311_service_requests
WHERE status IS NULL
~~~
-> Finding: no null value found under status column.


#### Question 6: What are the top complaints? 
~~~sql
SELECT complaint_type, COUNT(complaint_type) AS counts
FROM bigquery-public-data.new_york_311.311_service_requests
GROUP BY complaint_type
ORDER BY counts DESC
~~~
-> Finding: Noise-residential > heat/hot water > illegal parking


#### Question 7: Who are the top agency handling the requests?
~~~sql
SELECT agency_name, COUNT(agency_name) AS counts
FROM bigquery-public-data.new_york_311.311_service_requests
GROUP BY agency_name
ORDER BY counts DESC
~~~
-> Finding: New York City Police Department > Department of Housing Preservation and Development > Department of Transportation


#### Question 8: Which year did the requests hit the most number?
~~~sql
SELECT 
    EXTRACT(year FROM created_date) AS year,
    COUNT(*) AS counts
FROM bigquery-public-data.new_york_311.311_service_requests
GROUP BY year
ORDER BY counts desc
~~~
-> Finding: 2018 > 2020 > 2017


#### Question 9: Calculate average time required for request to be closed. Verify results.
(1) Calculated field from Tableau:
```
DATEDIFF('day',[Created Date],[Closed Date])
```

(2) Verification in BigQuery:
~~~sql
WITH temp AS (
    SELECT 
        timestamp_diff(closed_date,created_date,day) AS tiemdiff
    FROM 
        `capable-blend-330013.new_york_311.5years` 
    WHERE agency="HPD" 
      AND closed_date IS NOT NULL
    GROUP BY closed_date, created_date
    )

 SELECT 
    SUM(tiemdiff)/
    (SELECT COUNT(*) FROM capable-blend-330013.new_york_311.5years WHERE agency="HPD" AND closed_date IS NOT NULL)
    FROM temp
~~~
-> Finding: Results between Tableau and BigQuery are similar except for HPD. (Why huge difference for HPD?)


## Part 2: Tableau Note
### Track Issues and solutions

#### 1. Situation
I want to analyze top 10 complaints type out of 431. Instead of having 10 charts for each rank, I want to use filter so that I can see one rank chart each time.
  
#### 2. Problem
I try to use Top N item as filter, but filter card shows me the whole list of complaint type.
  - Problem A. I cannot use Top N filter, as filter card will show the entire list. 
  - Problem B. I cannot use grouped list for filter either. 
  - Problem C. Creating custom list takes time as I need to search and add manaully.

#### 3. Solution
Use parameter and apply [parameter] = [dimension] in filter.
  - Step 1. Group Top 10 complaint type vs rest types. This will speed up Step 2.
  - Step 2. Create parameter using string and adding values from Step 1's Group. 
  - Step 3. Add [complaint type] dimension as filter and edit fiter by going to condition > by formula > [parameter] = [complaint type]
  - Step 4. Show parameter control panel. 
  
#### 4. Tip
When I used parameter control, one of chart showed blank result.
  - Reason: I used copied worksheet where one of product name was alised previously. 
  - Solution: I edited Group from 3. Solution - Step 1 by removing inner-group of complaint type name. 
  
#### 5. Credit
  - Filtering with parameters by Ross Perez:
    https://www.tableau.com/about/blog/2012/7/filtering-parameters-18326

*END*
