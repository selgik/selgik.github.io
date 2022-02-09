---
output:
  always_allow_html: true
  author: Sylvia K
  date: 2022-02-09
  excerpt: project note
  knit: "(function (inputFile, encoding) { rmarkdown::render(inputFile,
    encoding=encoding, output_dir= “\\~/selgik.github.io/\\_posts”)})"
  layout: post
  md_document:
    preserve_yaml: true
    variant: gfm
  tags:
  - jekyll
  - r-markdown
title: P1/ Project Note
---
## Overview 
* This is the part 1 of project note.  
* See the final deliverable in this [post](https://selgik.github.io/data-viz/) (Project#1). 

## Table of Contents
1. Motivation  
2. Process Design  
3. Building Schema   
4. Final Deliverable  

## 1. Motivation 
### (1) Task
I need to spend certain amount of time or hit targetted hour (for example: at least 5.5h) on assigned project every day. Although I can work flexibly, as working on project 8h one day and 2h on another day, it is recommended to meet average daily goal of mentioned 5.5h.  

### (2) Problem
a. I need to manually calculate the project time to meet daily, weekly and monthly goal.  
b. I work hard everyday but I cannot meet the assigned goal. I do not know how can I improve and where am I spending my time.

### (3) Motivtaion
a. I want to be free from calculating remaining hours to meet average goal.  
b. I want analyze my time and find the area of improvement. I want to know where am I spending rest of my time and how can I adjust to meet targeted project hour.  
c. I do not use multiple platform. A dashboard solving both problem a and b, would be helpful.  
         
## 2. Process Design 
    Overall workflow: 
      User enters data (tracks time) via the form in sheet_1 -> 
        Data is transffered to sheet_2. Everyday new data will be piled up -> 
         Data is re-transffered to sheet_3 undergoing cleaning, calculation, pivoting process -> 
          Cleaned data is represented as visual graphs and bulletin in the sheet_1.                      

### (1) Step 1 - layout design
I will have one-page dashboard:  
a. 1st component will be the form, user will be updating last working day's project hour.  
b. 2nd component will be the bulletin where calculated remaining hour for given week is announced.  
c. 3rd component will be a chart showing progress against the goal for the last working day.  
d. 4th component will be a chart showing daily progress (time spent on project hour) for a given month.
e. 5th component will be a chart analyzing activies on reamining hours.  
f. 6th component will be a table showing monthly summary.  
         
I will have 3 spreadsheet:  
g. sheet_1: main dashboard sheet containing form, bulletin, charts and table. User's main page.
h. sheet_2: raw data sheet where fed data from the form will be organized.  
i. sheet_3: calculation sheet where pivot tables and other calculations will be performed.  
         
### (2) Step 2 - enter data (ref: 2(1)a)
a. What do I want to do? I want:
. User to feed (select or type) date, day type (full day/half day) and project hour.  
. User to optionally feed activity hour to analyze how remaining hours are used.  
. Fed data to be organized in table format in a spearate sheet.  

b. How?  
. Solution: use VBA. Create button which will trigger the data transfer process.  
. Flow: user feeds data to the form in sheet_1 -> button -> data is transffered and organized in the table in sheet_2.  
         
### (3) Step 3 - process data
a. Create pivot tables   
. Charts will be created based on the pivot tables. For each type of chart, independent pivot table will be created.  
. All calculations, pivot tables and data validation lists etc. will be organized in this sheet_3.  

b. Hide the sheet   
. To avoid confusion and breaking the format, all sheets will be protected except where user is feeding data in the form.  
. Additinoally, this sheet_3 will be hidden as users do not need to see background data (table, pivot, reference list etc.)  
         
### (4) Step 4 - data visualization    
a. Decide optimal chart type  
. 2(1)c: donut chart.  
. 2(1)d: bar or line chart.  
. 2(1)e: donut chart combining with horizontal bar chart showing top ranks in remaining hour section.   
    
### (5) Step 5 - test
a. Test out various chart types and color to see the overall harmony.  
b. Ask questions  
. Did I put too much information? Sould I reduce charts? Did I select too many chart types?   
. Will the form be placed on the left or right? Which one is more user friendly?  
         
         
## 3. Building Schema  
(1) Worksheet:  

| Worksheet Name | Description |
| :---   | :- |
| a. sheet_1  | main dashboard sheet containing form, bulletin, charts and table.  |
| b. sheet_2  | raw data sheet where fed data from the form will be organized.  |
| c. sheet_3  | calculation sheet where pivot tables and other calculations will be performed.  |

(2) Table (sheet_1):

| Field Name | Description |
| :---   | :- |
| a. Working hour | Add data validation. Select from the list: full or half day. |
| b. Date | Add data validation. Select from the list: list of last "n" date. |
| c. Project hour | User can type in the form of hour or minute. |
| d. Other activity(s) | User can type in the form of hour or minute. |
| e. Comment | User can type strings. |
| + Button | User clicks. Linked VBA code transffers entered data from sheet_1 to sheet_2.|


## 4. Final Deliverable
- User has one-stop page where they can feed the data and review the status/progress/analysis with visual aids in real time.   
- This dashboard can be utilized by those who needs to track or hit the tageted hour.  
Ex. operation center such as call center where each individual has targeted hour to hit.

*END* 
