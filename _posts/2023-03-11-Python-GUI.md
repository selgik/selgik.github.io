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
Distribute executable app automating repetitive tasks so that others can use without installing python  

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
### (1) Version 1: user will have buttons to use  
![v1](/assets/images/v1.png)  
         
### (2) Version 2: user will have forms to fill in and buttons to use  
![v2](/assets/images/v2.png)  

## 3. Action Flow
### (1) Version 1
- Clock Reminder: click the button and timer (pre-set ex. 9h) will start   
- Lunch Reminder: click the button and timer (pre-set ex. 1h) will start  
- Web Opener: click the button and pre-set websites will be opened in one window  

### (2) Version 2  
- Your Clock Time: type in shift start time (in HH:MM format)  
- Your Lunch Time: type in the minutes taken for lunch (in MM format)  
- Set Alarm: click the button and notification will show up when the current time hits calculated clock-out time (which is the sum of shift start time + lunch time + 8h)  
- Open URL: click the button and pre-set websites will be opened in one window  
- Instructions: click the button and another window containing texts messages (instructions) will pop up with 'Next' button   

## 4. Full Codes
- To review the full codes, check out at [GitHub](https://github.com/selgik/RPA-project/tree/main/button-to-start)   

## 5. Converting Scripts Into App
- Convert scripts to executable app for distribution. End-user would not need to install python but just launch the app.
- PyInstaller module was used to convert python script into an app:   
> python -m PyInstaller --windowed script.py  

## 6. Final Deliverable   
- User can open the app and click buttons to automate tasks.
 
*END* 
