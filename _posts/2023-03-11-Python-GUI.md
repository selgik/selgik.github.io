---
output:
  always_allow_html: true
  author: Sylvia K
  date: 2023-03-11
  excerpt: pythonprj
  knit: "(function (inputFile, encoding) { rmarkdown::render(inputFile,
    encoding=encoding, output_dir= “\\~/selgik.github.io/\\_posts”)})"
  layout: post
  md_document:
    preserve_yaml: true
    variant: gfm
  tags:
  - jekyll
  - python
  - gui
title: Python-GUI
---
## Overview 
Automate tasks and distribute app to others  

![gui](/assets/images/gui-prj.png)

## Table of Contents
1. Motivation  
2. GUI  
3. Action Flow   
4. Full Codes
5. Converting Scripts Into Executable App For Distribution 
6. Final Deliverable

## 1. Motivation   
### I do not want to do repetitive tasks  
- If you work at operation, there could be sequence of tasks or routine you may need to take everyday.  
- For example, connect to VPN > clock-in (record time in) > open necessary websites > set alarm to clock-out (record time out) etc.   
- This is not only repetitive but also manual. And, I make mistakes too. Sometimes I forget to set the alarm resulting in clocking out late. I want my codes to do these things for me.   

## 2. GUI  
### (1) version 1  
- by opening the app, user will have buttons to use  
![v1](/assets/images/v1.png)  
         
### (2) version 2  
- by opening the app, user will have forms to fill in and buttons to use  
![v2](/assets/images/v2.png)  

## 3. Action Flow   
### (1) version 1  
- Clock Reminder: by clicking this button, timer (preset ex. 9h) will start   
- Lunch Reminder: by clicking this button, timer (preset ex. 1h) will start  
- Web Opener: by clicking this button, pre-set websites will be opened in one window  

### (2) version 2  
- Your Clock Time: user types in their shirt start time (in HH:MM format)  
- Your Lunch Time: user types in the minutes they took for lunch (in MM format)  
- Set Alarm: by clicking this button, user will get alert when to clock-out notification will pop up after shirt start time + lunch time + 8h  
- Open URL: by clicking this button, pre-set websites will be opened in one window  
- Instructions: by clicking this button, user will see another window containing texts with Next button   

## 4. Full Codes   
- For the full codes, check out at [GitHub](https://github.com/selgik/RPA-project/tree/main/button-to-start)   

## 5. Converting Scripts Into Executable App For Distribution  
    python -m PyInstaller --windowed script.py  

## 6. Final Deliverable   
- User can open the app and click buttons to automate tasks
 
*END* 
