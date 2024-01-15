# captsone_bellabeat
Case Study of Bellabeat: Women's wellness company
# To get started on my project, I will upload the necessary csv files
library(readr)
dailyActivity_merged <- read_csv("dailyActivity_merged.csv")
# To see the table in another tab use the View()
View(dailyActivity_merged)
library(readr)
dailyCalories_merged <- read_csv("dailyCalories_merged.csv")
View(dailyCalories_merged)
library(readr)
dailySteps_merged <- read_csv("dailySteps_merged.csv")
View(dailySteps_merged)

#Install necessary packages for cleaning & organizing the data
install.packages("tidyverse")
install.packages("lubridate")
install.packages("dplyr")
install.packages("ggplot2")
install.packages("tidyr")

# Load libraries needed
library(tidyverse)
library(lubridate)
library(dplyr)
library(ggplot2)
library(tidyr)

# Creating dataframes
daily_activity <- read.csv("dailyActivity_merged.csv")

# Import sleepDay_merged.csv

library(readr)
sleepDay_merged <- read_csv("sleepDay_merged.csv")
View(sleepDay_merged)
sleep_day <- read.csv("sleepDay_merged.csv")
# Preview the daily_activity data
head(daily_activity)

# Idnetify all the columns in the daily_activity data
colnames(daily_activity)

# Take a look at the sleep_day data.
head(sleep_day)

# Identify all the columns in the sleep_day data.
colnames(sleep_day)

# How many unique participants are there in each dataframe? 
# It looks like there may be more participants in the daily activity 
# dataset than the sleep dataset.

n_distinct(daily_activity$Id)
n_distinct(sleep_day$Id)

# How many observations are there in each dataframe?

nrow(daily_activity)
nrow(sleep_day)

# What are some quick summary statistics we'd want to know about each data frame?

# For the daily activity dataframe:
daily_activity %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes) %>%
  summary()

# For the sleep dataframe:
sleep_day %>%  
  select(TotalSleepRecords,
         TotalMinutesAsleep,
         TotalTimeInBed) %>%
  summary()
# What does this tell us about this sample of people's activities?

# What's the relationship between steps taken in a day and sedentary minutes? 
# How could this help inform the customer segments that we can market to? 
# E.g. position this more as a way to get started in walking more? 
# Or to measure steps that you're already taking?

ggplot(data=daily_activity, aes(x=TotalSteps, y=SedentaryMinutes)) + geom_point()

# What's the relationship between minutes asleep and time in bed? 
# You might expect it to be almost completely linear - are there any unexpected trends?
ggplot(data=sleep_day, aes(x=TotalMinutesAsleep, y=TotalTimeInBed)) + geom_point()
# It seems those who stayed in bed the longest got the most sleep, with a few outliers.
#Merge two datasets together
combined_data <- merge(sleep_day, daily_activity, by="Id")

# Take a look at how many participants are in this data set.
n_distinct(combined_data$Id)

# We have 24 particapants
# Note that both datasets have the 'Id' field - 
# this can be used to merge the datasets.

# Note that there were more participant Ids in the daily activity 
# dataset that have been filtered out using merge. Consider using 'outer_join' 
# to keep those in the dataset. 
