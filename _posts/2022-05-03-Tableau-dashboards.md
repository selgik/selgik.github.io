---
output:
  always_allow_html: true
  author: Sylvia K
  date: 2022-05-03
  excerpt: test
  knit: "(function (inputFile, encoding) { rmarkdown::render(inputFile,
    encoding=encoding, output_dir= “\\~/selgik.github.io/\\_posts”)})"
  layout: post
  md_document:
    preserve_yaml: true
    variant: gfm
  tags:
  - jekyll
title: Tableau Dashboards
---

## Overview
Tableau dashboards are great. They empower users to see what they want. Instead of creating graphs everytime you need, link data and build filters so that Lilly from Sales or James from Finance can get insights from them. 

- Type1: One page dashboard for easier navigation  
(Use Google Chrome or full screen mode)
  {% include video2.html id="/assets/images/video2.mp4" %}  
   
- Type2: Multiple pages dashboard segregated per topic  
(Use Google Chrome or full screen mode)
  {% include video3.html id="/assets/images/video3.mp4" %}  
  
In this page, I have prepared two types of documents. Scope of Work for <a href="#type1">Type1</a> and Report for <a href="#type2">Type2</a>. 
Click relevant documents or [here](https://public.tableau.com/app/profile/sylvia.kim) to test dashboards out.

<a name="type1">  
# Type1: Scope of Work  
##  
## Type1: Scope of Work  
###  
Data Visualization Project   
Date: Nov 12, 2021                                                                                        
Data Analyst: Sylvia K.  
Client/Sponsor: N/A  

### 1. Purpose: 
The goal of this project is to visualize key COVID-19 data enabling easeir search and comparison overview.  
    
The project will organize daily and historical COVID-19 data using country, time and region filters. After applying filters, the project will illustrate daily and total number of confirmed cases/deaths/ vaccinations and trend over time, including fatality rate change and case fluctuation over the last 14 days, as of the last update date of the dashboard. The project will also provide an overview on global/continental COVID-19 ranking summary on the map.  
  
The final deliverable will streamline search process by producing comprehensive report on COVID-19 status.

### 2. Scope / Major Project Activities:
  
| **Activity**        | **Description**                                                                      |  
|---------------------|--------------------------------------------------------------------------------------|  
|Data collection      | Collect COVID-19 data from Our World in Data (https://ourworldindata.org/coronavirus)|
|Decide story point   | Decide on key figures to include in the dashboard.                                   |
|Identify relationship| Study whether there is relationship between key figures.                             |
|Design report        | Compare chart types and arrange information.                                         |
|Deliver dashboard    | Deliver final dashboard with optimal type of filters.                                |

### 3. This project does not include:
Other than country-level data (dashboard will not provide either continental or city-level summary).

### 4. Deliverables:
Interactive dashboard: A data visualization user can search and view summarized COVID-19 data.

### 5. Schedule Overview / Major Milestones:
  
| **Milestone**       | **Date**             | **Description**                                                                                |
|---------------------|----------------------|------------------------------------------------------------------------------------------------|  
|Upload dashboard     | Oct 15, 2021         | Upload dashbaord to Tableau Public to enable user to interact with data.                       |
|Datasource update    | Every 2 days         | In order to accurately capture daily updates, data-source update is scheduled for every 2 days.|

 *Update has been stopped as of Nov 7, 2021.* 
  
<a name="type2">
## Type2: Report

## Table of Contents
1. Motivation  
2. Project Workflow
3. Part 1: Clean Data with SQL
4. Part 2: Visualize Findings with Tableau
5. Final Deliverable
6. Data Source  

## 1. Movitation
### Problem
- Raw data is too big and it is impossible to read the insights. Data is not cleaned up either.
- Data is too big for Excel to handle. I need other program to clean, transform and visualize data.
 
### Motivation
- I want to quickly clean up and calculate data.
- I want to find out trend, insights and interesting figures and share with users.
- I also want to give end-user a freedom to navigate and to find out their own insight.

## 2. Project Workflow
* What is this data telling me? Ask questions (or assumption) and find answers.  
* Part 1: Clean data with SQL 
* Part 2: Visualize findings with Tableau


## 3. Part 1: Clean Data With SQL.   
### Understand the Dataset 
By asking questions:
- How many requests are being reported to each agencies? 
- What kind of complaints are received the most? 
- When is the peak season for each agencies?
- What can I suggest for each agencies to deal with seaonsal fluctuation?


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
-> Finding: There are 2,283 cases where status is "Closed" but no closed_date is provided.


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
-> Finding: No null value found under status column.


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
-> Finding: Results between Tableau and BigQuery are similar except for HPD. (Why huge difference for HPD? Need further investigation)


## 4. Part 2: Visualize Findings with Tableau
### Choosing dashboard type
- Question: Why did I chose to build multiple pages dashboards for this project?
- Answer: Unlike the COVID-19 project where I had to deal with only 1 unified theme (COVID-19), this project had mulitple themes (requests number, duration time, season or agencies etc). Adding all analysis in one page could be overwhelming to users as it would contain too much information. 

### Designing dashboards
- Divide dashboards into three section: service requests summary per (1) season (2) agency (3) type.
- Enable data source filters for year/month
- Add key insights for each section. 

### Track Tableau issues

#### 1. Situation
I want to analyze top 10 complaints type out of 431.  
  
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

## 5. Final Deliverable
### Dashboard Demos
- Click this [link](https://public.tableau.com/app/profile/sylvia.kim) to test out.

## 6. Information About Data Source
- Data source: [NYC 311 Dataset](https://console.cloud.google.com/marketplace/product/city-of-new-york/nyc-311?project=capable-blend-330013)  
- Description: This data includes all New York City 311 service requests from 2010 to the present, and is updated daily. 311 is a non-emergency number that provides access to non-emergency municipal services.
  
*END*
