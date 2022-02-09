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
title: P3/ Tableau Note
---

## Overview
This is the part 2 of project note. See the final deliverable in this [post](https://selgik.github.io/data-viz/) (Project#3). 

### Project Workflow
* Clean and review data in SQL -> **visualize findings in Tableau**

### Information about data source
* Data source: [NYC 311 Dataset](https://console.cloud.google.com/marketplace/product/city-of-new-york/nyc-311?project=capable-blend-330013)  
* Description: This data includes all New York City 311 service requests from 2010 to the present, and is updated daily. 311 is a non-emergency number that provides access to non-emergency municipal services.

### Tool Used
* Tableau Desktop

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

#### Review Tableau Dashboard in Action
Go to the post [Data Visualization](https://selgik.github.io/data-viz/) and review Project 3.  
*END*
