# Case Study - How Can a Wellness Technology Company Play It Smart?

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


### Data Limitations
1. Data is old (2016) which might not match the current trends
2. Potential of bias due to the limited (30) number of customer data. This is the bare minimum needed for data analysis. 
3. Data doesn't feature demographics data while Bellabeat specifically targets womens
4. Limited window (2 months) which might or might not reflect seasonality
6. Data is only from FitBit (single smart device brand while there are other relevant players in the market)
7. S

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

First, I uploaded the files directly into R Cloud in order to directly read the file without pasting full file path in the computer. Then, I pulled the file through read_csv function as part of R tidyverse package. 

```
daily_activity <-read_csv("dailyActivity_merged.csv")
daily_calories <- read.csv("dailyCalories_merged.csv")
daily_intensities <- read.csv("dailyIntensities_merged.csv")
daily_steps <- read.csv("dailySteps_merged.csv")
sleep_day <- read.csv("sleepDay_merged.csv")
weight_log <- read.csv("weightLogInfo_merged.csv") <- This data file won't be used as there are only 8 unique user IDs which is too small of a sample size. 

```

### Data Cleaning
+ Date field has been standardized to DD-MM-YY across all the data files through the function 


Checking the number of unique participants in each imported data file. 
```
n_distinct(daily_activity$Id)
n_distinct(daily_calories$Id)
n_distinct(daily_intensities$Id)
n_distinct(daily_steps$Id)
n_distinct(sleep_day$Id)
n_distinct(weight_log$Id)
```

Checking for and removing duplicate values in each data file.


sum(duplicated(daily_activities))
sum(duplicated(daily_calories))
sum(duplicated(daily_intensities))
sum(duplicated(daily_steps))
sum(duplicated(sleep_day))   - Three (3) duplicates 
sum(duplicated(weight_log))

Removing 3 duplicates in sleep_day data file and renaming the file as daily_sleep. 
daily_sleep <- unique(sleep_day)  
sum(duplicated(daily_sleep))


#### Data Visualizations

ggplot(data=daily_activity) + geom_point(mapping=aes(x=TotalSteps, y=Calories, color=Calories))



### Summary of the analysis
+ There's a positive correlation between number of total steps each customer has taken with the calories burned. This could obviously be used to encourage/notify customers in order to build positive energy/connection between the user and the product
+ S
+ S
+ S

### Visualizations

All these data visualizations can be found here


### Recommendations
1. S
2. S
3. S
