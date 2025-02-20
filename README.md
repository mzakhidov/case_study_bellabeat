# Case Study - How Can a Wellness Technology Company Play It Smart?

#### This is a capstone project as part of the Google Data Analytics course. 

### Introduction
[Bellabeat](https://bellabeat.com) is a high-tech company that manufactures health-focused smart wearable products for women. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart device data could help unlock new growth oppounities for the company.

<img src="https://github.com/mzakhidov/case_study_bellabeat/blob/main/Bellabeat%20logo.png?raw=true" alt="Bellabeat Logo" width="300">

### Business Task 
Analyze smart device usage data in order to gain insight into how consumers use their non-Bellabeat smart devices. Insights should help guide the marketing strategy for the Bellabeat. 

Primary goals are:
+ Identify trends in smart wearable device usage data
+ Determine how these trends can be applied to Bellabeat customers
+ Use these trends to optimize Bellabeat marketing strategy

### Data Source 
FitBit Fintess Tracker Data (CC0: Public Domain, dataset made available through Mobius). This Kaggle data set contains personal tness tracker from thiy tbit users. Thiy eligible Fitbit users consented to the submission of
personal tracker data, including minute-level output for physical activity, hea rate, and sleep monitoring. It includes information about daily activity, steps, and hea rate that can be used to explore users’ habits. It covers a month of data between 04.12.2016-05.12.2016. 
+ [Data Link](https://www.kaggle.com/datasets/arashnic/fitbit) 

### Stakeholders
+ _Urska Srsen_: Bellabeat's cofounder and Chief Creative Officer
+ _Sando Mur_: Mathematician and Bellabeat's cofounder; key member of the Bellabeat executive team
+ Bellabeat marketing analytics team

### Products
+ **Bellabeat app**: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users beer understand their current habits and make healthy decisions. The Bellabeat app connects to their line of sma wellness products.
+ **Leaf**: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
+ **Time**: This wellness watch combines the timeless look of a classic timepiece with sma technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
+ **Spring**: This is a water bole that tracks daily water intake using sma technology to ensure that you are appropriately hydrated throughout the day. The Spring bole connects to the Bellabeat app to track your
hydration levels.
+ **Bellabeat membership**: Bellabeat also oers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and
beauty, and mindfulness based on their lifestyle and goals.

### Data Limitations
1. Data is old (from 2016) which may not match the current trends.
2. Potential of bias due to the limited (30) number of customer data. This is the bare minimum needed for data analysis. 
3. Data doesn't feature demographics data while Bellabeat specifically targets womens
4. Limited window for data (1 month) which might potentially reflect seasonality. People tend to be more active in warmer months. 
5. Data is only from FitBit (single smart device brand while there are other relevant players in the market such as Apple, Samsung, etc.)
6. Data isn't comprehensive as it doesn't contain info on gender, age, etc.
7. Data isn't original as it doesn't directly come from FitBit, rather from 3rd party. 

### Data Preparation and Processing

Based on the initial review of CSV files through Excel, R studio has been chosen to prepare, process, analyze the data. Initially, the R packages of tidyverse and janitor have been installed and the respective libraries have been loaded. 

#### Install packages and load libraries
```
install.packages('tidyverse')
install.packages('janitor') 
```
```
library(tidyverse)  
library(lubridate)
library(ggplot2)
```

#### Import data sets

As "dailyActivity_merged.csv" file contained most of the high level data metrics, it was decided that only daily data files would be imported for analysis. Downloaded csv files have been uploaded into R Cloud in order to directly read the file. Then, the files have been pulled through read_csv function as part of R tidyverse package and renamed accordingly for simplicity. 

```
daily_activity <-read_csv("dailyActivity_merged.csv")
daily_calories <- read.csv("dailyCalories_merged.csv")
daily_intensities <- read.csv("dailyIntensities_merged.csv")
daily_steps <- read.csv("dailySteps_merged.csv")
sleep_day <- read.csv("sleepDay_merged.csv")
weight_log <- read.csv("weightLogInfo_merged.csv") 

```

### Data Cleaning
Date field has been standardized to DD-MM-YY across all the data files through the function.
```
daily_activity <- daily_activity %>% mutate( Weekday = weekdays(as.Date(ActivityDate, "%m/%d/%Y")))
```

Checking the number of unique participants in each imported data file. 
```
n_distinct(daily_activity$Id)
n_distinct(daily_calories$Id)
n_distinct(daily_intensities$Id)
n_distinct(daily_steps$Id)
n_distinct(sleep_day$Id)
n_distinct(weight_log$Id) 
```

The "weight_log" file won't be used as there are only 8 unique user IDs which is too small of a sample size. 

Checking for and removing duplicate values in each data file.

```
sum(duplicated(daily_activities))
sum(duplicated(daily_calories))
sum(duplicated(daily_intensities))
sum(duplicated(daily_steps))
sum(duplicated(sleep_day))   - Three (3) duplicates 
sum(duplicated(weight_log))
```

Removing 3 duplicates in sleep_day data file and renaming the file as daily_sleep.  
```
daily_sleep <- unique(sleep_day)  
sum(duplicated(daily_sleep))  
```

Checking for NA values 
```
sum(is.na(daily_activity))
sum(is.na(daily_calories))
sum(is.na(daily_intentisities))
sum(is.na(daily_steps))
sum(is.na(daily_sleep))
sum(is.na(weight_log)) <- Sixty five (65) NA values

```

Adding a new column for weekdays
```
daily_activity <- daily_activity %>% mutate( Weekday = weekdays(as.Date(ActivityDate, "%m/%d/%Y")))

```

Order the days of the week:
```
daily_activity$Weekday <- ordered(daily_activity$Weekday, levels=c("Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"))

```


Combine data sets

As "daily_activity" file contained metrics on calories, intentisies, steps, it was decided that only "daily_activity" and "daily_sleep" files would be combined and named as "combined_data".

```
combined_data <- merge(daily_activity,daily_sleep,by = c("Id"), all=TRUE)

```


#### Data Analysis and Visualizations

Correlation between total steps and calories: 
```

ggplot(combined_data, aes(x = TotalSteps, y = Calories)) +
  geom_point(color = "darkgreen", alpha = 0.5) +
  geom_smooth(method = "lm", color = "red") + # Add a trend line
  labs(title = "Steps vs. Calories Burned", x = "Total Steps", y = "Calories Burned") +
  theme_bw()

```

![steps vs calories](https://github.com/user-attachments/assets/0303d36b-36e9-471f-942c-38689ac9ab55)


Total steps by the weekday:
```
ggplot(data=daily_activity, aes(x=Weekday, y=TotalSteps)) + 
    geom_bar(stat="identity", fill="blue")+
    labs(title="Steps by Weekday", y="Total Steps") 
```

![steps_weekdays](https://github.com/user-attachments/assets/d9cf24da-94e0-4e15-bf95-0c6d84b7cd00)


Correlation between sleep and calories:
```
ggplot(data=combined_data) + geom_point(mapping=aes(x=TotalMinutesAsleep/60, y=Calories, color=Calories)) + labs(title="Calories vs Time Slept", x="Time Asleep (Hours)", y="Calories")

```
![calories vs time slept](https://github.com/user-attachments/assets/ea7fda76-7baf-454f-a193-3f11699415b4)


### Summary of the analysis
+ There's a positive correlation between number of total steps each customer has taken with the calories burned. This could obviously be used to encourage/notify customers in order to build positive energy/connection between the user and the product
+ Users seem to take the most number of steps in middle of the workweek: Tuesday, Wednesday, Thursday.
+ There's a positive correlation on calories burned and sleep time (between 5-10 hours)


### Recommendations
1. Encourage users by giving them calories burned notifications as a "reward" notification in Bellabeat products
2. Focus on days where users take the least amount of steps. Suggest activities to the user in order to increase their total steps on these days
3. Send reminders to users on getting enough sleep between 6-10 hours
4. Due to data limitations, all the above recommendations might require further validation based on recent data
