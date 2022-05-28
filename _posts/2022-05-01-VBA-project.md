---
output:
  always_allow_html: true
  author: Sylvia K
  date: 2022-05-01
  excerpt: project note
  knit: "(function (inputFile, encoding) { rmarkdown::render(inputFile,
    encoding=encoding, output_dir= “\\~/selgik.github.io/\\_posts”)})"
  layout: post
  md_document:
    preserve_yaml: true
    variant: gfm
  tags:
  - jekyll
  - vba
title: VBA Project
---
## Overview 
Automate data entry and visualization process with Excel VBA.  
(Use Google Chrome or full screen mode for video)

 {% include video1.html id="/assets/images/video1.mp4" %}  
 
## Table of Contents
1. Motivation  
2. Process Design  
3. Building Schema   
4. Code Chunks
5. Final Deliverable  

## 1. Motivation 
### (1) Task
Let's say, I work at operation. As part of my matrix, I need to hit targetter hour (ex. 5.5 hours) on assigned project. While I can plan my week and allocate time flexibly, it is recommended to meet daily goal of at least 5h.  

### (2) Problem
- I need to manually calculate the time spent on the project to meet daily, weekly and monthly goal. Sometimes I make mistakes in calculation. 
- I work hard but I cannot meet the targetted goal. I do not know how I can better manage my time.

### (3) Motivtaion
- I want to be free from calculating remaining hours. I want the program to tell me how many hours are left to meet the weekly goal.
- I want to analyze my time and find the area for improvement. I want to know where I am spending rest of my time and how I can adjust to meet targeted project hour.  
- I do not want to use multiple platforms. A one-stop platform where I can input data and gain insight, would be easier.  
         
## 2. Process Design 

| Overall workflow: |
| :---   | :- |
| User enters data (project hour) via the form in sheet_1 |
| -> Data is transffered to sheet_2. Everyday new data will be piled up |
| -> Data is re-transffered to sheet_3 undergoing cleaning, calculation and pivoting process |
| -> Cleaned data is represented as visual graphs and bulletin in the sheet_1.   |

### (1) Step 1 - layout design
I will have one-page dashboard:  
- a. 1st component will be the data entry form with a button. User will be updating last working day's project hour.  
- b. 2nd component will be the bulletin where calculated remaining hour for given week is announced.  
- c. 3rd component will be a chart showing progress against the goal for the last working day.  
- d. 4th component will be a chart showing daily progress (time spent on project hour) for a given month.  
- e. 5th component will be a chart analyzing activies on reamining hours.  
- f. 6th component will be a table showing monthly summary.  
         
I will have 3 spreadsheet:  
- g. sheet_1: main dashboard sheet containing form, bulletin, charts and table. User's main go-to page.  
- h. sheet_2: raw data sheet where fed data from the form will be organized.  
- i. sheet_3: calculation sheet where pivot tables and other calculations will be performed.  
         
### (2) Step 2 - enter data (ref: 2(1)a.)
I want:  
- User to feed (select or type) date, day type (full day/half day) and achieved project hour.  
- User to optionally feed activity hour to analyze how remaining hours are spent.  
- Fed data to be organized in table format in a spearate sheet.  

How?  
- Solution: use VBA. Create button which will trigger the data transfer process.  
- Flow: user feeds data to the form in sheet_1 -> clicks button -> data is transffered and organized in the table in sheet_2.  
         
### (3) Step 3 - process data
Create pivot tables:   
- Charts will be created based on the pivot tables. For each type of chart, independent pivot table will be created.  
- All calculations, pivot tables and data validation lists etc. will be organized in this sheet_3.  

Hide the sheet:   
- To avoid user's confusion and breaking the formula, all sheets will be protected except where user is feeding data in the form in sheet_1.  
- Additinoally, sheet_3 will be hidden as users do not need to see raw/transformed data (table, pivot, reference list etc.)  
         
### (4) Step 4 - data visualization    
Decide optimal chart type:  
- 2(1)c: donut chart.  
- 2(1)d: bar or line chart.  
- 2(1)e: donut chart combining with horizontal bar chart showing top ranks in remaining hour section.   
    
### (5) Step 5 - test
Test out various chart types and color to see the overall harmony. Ask questions:  
- Did I put too much information? Sould I reduce charts? Did I select too many chart types?   
- Will the form be placed on the left or right? Which one is more user friendly? Are there too many colors?
        
## 3. Building Schema  
(1) Worksheet:  

| Worksheet Name | Description |
| :---   | :- |
| a. sheet_1  | main dashboard worksheet containing form, bulletin, charts.  |
| b. sheet_2  | raw data worksheet where fed data from the user form will be organized.  |
| c. sheet_3  | calculation worksheet where pivot tables and other calculations will be performed.  |

(2) Table (sheet_1):

| Field Name | Description |
| :---   | :- |
| a. Working hour | Add data validation. Select from the list: full or half day. |
| b. Date | Add data validation. Select from the list: list of last "n" date. |
| c. Project hour | User can type in the form of hour or minute. |
| d. Other activity(s) | User can type in the form of hour or minute. |
| e. Comment | User can type strings. |
| + Button | User clicks. Linked VBA code transffers entered data from sheet_1 to sheet_2.|


## 4. Code Chucks

    Sub Update_Prd()
    
    'Step0: Declare variable
    
    Dim a As Integer
    a = Worksheets("sheet_2").Cells(1, 11).Value
    
    'Question: What is in Cells(1,11)? 
    'Answer: There is formula =counta(D1:D500)+3 in Cells(1, 11).
    '        Once data is transfferd via Step1, Cells(1,11) value will increase due to counta function. 
    '        As a result, newly transffered data will be sotred in the next row number.
    '        Without it, newly transffered data will be stored in the smae row where previously transffered data sit. 
    '        It will make impossible to store historical data as new data will erase old data.
    

    'Step1: If cell C6 is NOT empty, transfer data from Main_Dashboard to sheet_2
    'C6 is where user inputs date
    
    If IsEmpty(Worksheets("Main_Dashbaord").Range("C6")) = False Then

    Worksheets("sheet_2").Cells(a, 2) = Worksheets("Main_Dashbaord").Cells(5, 3)
    Worksheets("sheet_2").Cells(a, 3) = Worksheets("Main_Dashbaord").Cells(6, 3)
    Worksheets("sheet_2").Cells(a, 4) = Worksheets("Main_Dashbaord").Cells(7, 3)
    Worksheets("sheet_2").Cells(a, 5) = Worksheets("Main_Dashbaord").Cells(8, 3)
    Worksheets("sheet_2").Cells(a, 6) = Worksheets("Main_Dashbaord").Cells(9, 3)
    Worksheets("sheet_2").Cells(a, 7) = Worksheets("Main_Dashbaord").Cells(10, 3)
    Worksheets("sheet_2").Cells(a, 8) = Worksheets("Main_Dashbaord").Cells(11, 3)
    Worksheets("sheet_2").Cells(a, 9) = Worksheets("Main_Dashbaord").Cells(12, 3)
    Worksheets("sheet_2").Cells(a, 10) = Worksheets("Main_Dashbaord").Cells(13, 3)
    Worksheets("sheet_2").Cells(a, 11) = Worksheets("Main_Dashbaord").Cells(14, 3)
    Worksheets("sheet_2").Cells(a, 12) = Worksheets("Main_Dashbaord").Cells(15, 3)

    'Next, clear the contents for below range.     
    Worksheets("Main_Dashbaord").Range("C5:C15").ClearContents

    'Otherwise (if C6 is empty) alert user to fill in the date.
    Else
       MsgBox "Date is missing"
    End If


    'Step2: Mark the day as default "full day" instead of "half day" so that user does not have to select everyday.
    Range("C5").Select
    ActiveCell.FormulaR1C1 = "Full"
    Range("C6").Select


    'Step3: Refresh pivot so that related graphs on dashboard can be auto-updated upon clicking button.
    ActiveWorkbook.RefreshAll
    
    'Step 4: Sort horizontal bar chart analyzing activities in remaining hour, in ASC order. (recorded via macro)
        ActiveWorkbook.Worksheets("sheet_3").AutoFilter.Sort.SortFields.Clear
        ActiveWorkbook.Worksheets("sheet_3").AutoFilter.Sort.SortFields.Add2 Key:= _
            Range("AG2:AG9"), SortOn:=xlSortOnValues, Order:=xlAscending, DataOption _
           :=xlSortNormal
          With ActiveWorkbook.Worksheets("sheet_3").AutoFilter.Sort
            .Header = xlYes
            .MatchCase = False
            .Orientation = xlTopToBottom
           .SortMethod = xlPinYin
           .Apply
          End With

    End Sub


## 5. Final Deliverable
- User has one-stop page where they can feed the data and review the status/progress/analysis with visual aids in real time.   
- This dashboard can be utilized by those who needs to track or hit the tageted hour. (Ex. operation center such as call center where each individual has targeted hour to hit.)    

 
*END* 
