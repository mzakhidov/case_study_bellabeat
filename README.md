# Case Study - How Can a Welness Technology Company Play It Smart?

##### This is a capstone project as part of Google Data Analytics course. 

### Introduction
[Bellabeat](https://bellabeat.com) is a high-tech company that manufactures health-focused smart products for women. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.

### Business Task 
Analyze smart device usage data in order to gain insight into how consumers use non-Bellabeat smart devices. Goals are the following:
+ Identify trends in smart device usage
+ Determine how these trends can be applied to Bellabeat customers
+ Use these trends to optimize Bellabeat marketing strategy

### Data Sources: 
FitBit Fintess Tracker Data (Kaggle). For this case study, FitBit Fitness Tracker Data has been utilized. It covers 2 months of data between 03.12.2016-05.12.2016. 
+ [Data Link](https://www.kaggle.com/datasets/arashnic/fitbit) 

### Stakeholders
+ _Urska Srsen_: Bellabeat's cofounder and Chief Creative Officer
+ _Sando Mur_: Mathematician and Bellabeat's cofounder; key member of the Bellabeat executive team
+ Bellabeat marketing analytics team

### Products
+ Bellabeat app
+ Leaf
+ Time
+ Spring
+ Bellabeat membership

### Data Cleaning
+ Date field has been standardized to DD-MM-YY across all the data files 

### Data Limitations
1. Data is old (2001) and isn't up to date
2. Limited window (2 months) which might or might not reflect seasonality
3. Potential of bias due to the limited (30) number of customer data
4. Data is only from FitBit
5. S

It’s worth noting that data only covers two months. Due to its limitation, data insights might not give viewer the full picture. Several years of annual data could be appropriate. Data also comes from a single brand/company for smart devices, FitBit while there are multiple major players in this market. It can’t be taken as the whole industry data due to this limitation. 

### Data Analysis in R
#### Load library and files
```
install.packages('tidyverse')
install.packages('janitor') ???
```
library(tidyverse)  
library(lubridate)
library(ggplot2)


#### Import data sets

First, I uploaded the files directly into R Cloud in order to directly read the file without pasting full file path in the computer. 

```
daily_activity <-read_csv("dailyActivity_merged.csv")
daily_calories <- read.csv("dailyCalories_merged.csv")
daily_intensities <- read.csv("dailyIntensities_merged.csv")
daily_steps <- read.csv("dailySteps_merged.csv")
sleep_day <- read.csv("sleepDay_merged.csv")
weight_log <- read.csv("weightLogInfo_merged.csv")

```

#### Data Visualizations

ggplot(data=daily_activity) + geom_point(mapping=aes(x=TotalSteps, y=Calories, color=Calories))



### Summary of the analysis
+ There's a positive correlation between number of total steps each customer has taken with the calories burned
+ S
+ S
+ S

### Visualizations

All these data visualizations can be found here


### Recommendations
1. S
2. S
3. S
