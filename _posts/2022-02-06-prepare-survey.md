---
output:
  always_allow_html: true
  author: Sylvia K
  date: 2022-02-06
  excerpt: test
  knit: "(function (inputFile, encoding) { rmarkdown::render(inputFile,
    encoding=encoding, output_dir= “\\~/selgik.github.io/\\_posts”)})"
  layout: post
  md_document:
    preserve_yaml: true
    variant: gfm
  tags:
  - jekyll
  - r-markdown
title: test
---

## TABLE OF CONTENTS:
* MOTIVATION
* KEY CONCEPTS
* APPLYING KEY CONCEPTS
* REMAKRS

***

## MOTIVATION
1. TASK
       Recently I led training for 1,000 staffs. I want to know whether staffs were satisfied with the training contents.
       Depending on the survey results, I may have to restructure or continue with the current program.
       I prepare survey questions and ask other colleauges to review to ensure questions are unbiased and fair. 
       
2. PROBLEM
       a. How many should I survey? 
          I cannot survey 1,000 staffs as it will cost a lot. 
          I cannot survey 10 staffs either and assume the result would truly represent the whole staffs's opinion.
       b. How should I interpret the results? 
          60% responded A and 40% reponded B. What else is hidden behind those numbers?
       
3. MOTIVATION
       I want to determine optimal sample size and understand how to interpret the survey results.
       
***       
## KEY CONCEPTS
1. POPULATION VS SAMPLE
       I cannot survey all 1,000 staffs. I want to survey the portion that can represent the 1,000 staffs.
       I plan to survey only 50. Can I expect that sample size will give an accurate insight?  
   
       a. Population is 1,000. Sample size is 50.
       b. Tip: It is advised to use minimum 30 as sample size*, for an average result of a sample starts to represent the average result of a population.
       
2. MARGIN OF ERROR
       Surveying all 1,000 staffs will give 70% of satisfaction rate. 
       But if I select 50 staffs based on the high attendance, engagement and test results of the training, I may get 90% satisfaction rate.
       On the other hand, if I select 50 staffs from the low performing group, the satisfaction rate may drop down. 

       a. Margin of error is the difference between samples' results (ex. 90%) and entire population's result (ex. 70%), 20% in this case.
       b. Tip: The smaller the margin of error, the closer samples' results are to actual population's result. 
  
3. CONFIDENCE LEVEL
       If I would run the same survey 100 times, I want to obtain the same result at least 90 times, 
       so that I can feel confident that survey was prepared and executed accurately and the results are meaningful.
 
       a. Confidence level here is 90% (90 times out of 100 times). 
       b. Tip: The most commonly used confidence level is 95%. 90% can work in some cases. 
   
4. STATISTICAL SIGNIFICANCE
       Could my survey result be due to a coincidence or accurate measurement? I surely want the latter option.
   
       a. Statistical significance is the determination of whether the result could be due to random chance or not.
       b. Tip: The greater the significance, the less due to chance.
       
5. STATISTICAL POWER
       The probability of getting meaningful results is statistical power.
   
       a. Statistical power is the probability of getting meaningful results (statistically significant) results. 
       b. Tip: Typically, having at least 80% of statistical power is considered for results to be satistically significant.

***
## APPLYING KEY CONCEPTS
1. INTERPRET RESULTS
       Let's assume I ran the survey with randomly chosen 50 staffs and the result said 30 of them (60%) gave positive rating on training,
       while the rest 20 staffs (40%) gave negative rating. Provided that the confidence level is 90%, I can calculate margin of error as ~11%.
       That means, there are 90% chance that the 1,000 staffs' positive response would fall between 49% - 71%.  
       
       So what does that mean? Did staffs enjoyed training or not? 
       With margin of error fall in between ~50%, this could mean the survey results are inconclusive. 
       So I might consider increasing sample size and re-do the survey. Increasing sample size will drop the margin of error.
       
2. DETERMINE SAMPLE SIZE
       In order to calculate the sample size**, I need population size, confidence level (%) and margin of error (%).
       Let's assume I want to obtain accurate results from survey with 99% confidence level and 5% margin of error.
       For 1,000 staffs then I would at least survey 400 staffs. 
   
3. CALCULATE MARGIN OF ERROR
       If I have population size, sample size and confidence level (%) I could calculate margin of error***.
       Let's assume I target 95% confidence level for surveying 100 staffs out of 1,000 population.
       Margin of error would be at ~9%. 

***

## REMAKRS
1. DOES IT ALWAYS MATTER TO HAVE STATISTICAL SIGNIFICANT SAMPLE SIZE?
       The answer is yes and no. It will depend on the types, circumtances or industries etc.
       Let's say the department's head wants to restructure training program depending on the satisfaction rate from the survey.
       For this case, running survey with statistically significant sample size will matter.
       
       However, if I am casually seeking feedback and want to know about general satisfaction rate, 
       whether we have statistically significant sample size or not, will not matter that much. 
       What will matter more is, feedback, improvement ideas and suggestsions that will be submitted by the staffs.

2. REMARKS
    *  30 as sample size under 2.(1) 
       As sample size increases, the results more closely resemble the normal (bell-shaped) distribution. 
       A sample of 30 is the smallest sample size for which the Central limit theorem (CLT) is still valid.

    ** Calculate sample size under 3.(2)
       I used sample size calculator. Ex: https://www.surveymonkey.com/mp/sample-size-calculator/
       
    ***Calculate margin of error under 3.(3)
       I used margin of error calculator. Ex: https://www.surveymonkey.com/mp/margin-of-error-calculator/

