

**Google Capstone Project: A Case Study of Bellabeat using Excel, SQL & R**


![image](https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/e3e15c4f-2e2a-4415-9265-b63bfec53f12)


This document represents my finalized case study from an elective module within the Google Data Analytics Course called the Capstone Project.

The examination adheres to the six stages of data analysis outlined in the Google Data Analysis course: Ask, Prepare, Process, Analyse, Share and Act.

**Step 1: Ask**

In this phase, I'll explain the problem and what we aim to achieve in this case study. Then, I'll describe the expected result.

**1.0 Background**

Bellabeat is a leading high-tech manufacturer dedicated to delivering sophisticated and practical products designed for women. The company's focus is on creating empowering solutions that enhance women's well-being and align with their lifestyles. Established in 2013, Bellabeat has witnessed substantial growth, establishing itself as a key player in the women's technology sector.

Urška Sršen, the co-founder and Chief Creative Officer of Bellabeat, expresses confidence in the potential for discovering further avenues for growth by examining consumer data beyond Bellabeat, such as analyzing usage data from FitBit fitness trackers.

**1.1 Business Task**

Analyze FitBit data to understand user behavior and collect valuable insights for shaping future Bellabeat products and refining marketing strategies.

**1.2 Business Objectives**

1. What are some trends in smart device usage? 
2. How could these trends apply to Bellabeat customers? 
3. How could these trends help influence Bellabeat marketing strategy?

**1.3 Deliverables**

•	A clear summary of the business task
•	A description of all data sources used
•	Documentation of any cleaning or manipulation of data
•	A summary of my analysis
•	Supporting visualizations and key findings
•	My top high-level content recommendations based on the analysis

**1.4 Key Stakeholders**

•	**Urška Sršen** serves as Bellabeat's co-founder and Chief Creative Officer

•	**Sando Mur**, a mathematician and co-founder, plays a crucial role within the Bellabeat executive team. 

•	**The marketing analytics team** at Bellabeat consists of data analysts who are tasked with gathering, assessing, and presenting data to inform and shape the company's marketing strategy.

**Step 2: Prepare**

To prepare, I assess the data in use and its limitations.

**2.0 Data Source**

•	The data is accessible to the public on Kaggle through this link: https://www.kaggle.com/datasets/arashnic/fitbit. 

•	The data is derived from a survey conducted via Amazon Mechanical Turk between 03.12.2016 and 05.12.2016, with input from 30 participants. 

•	The dataset comprises individual tracker details, encompassing minute-level data related to physical activity, heart rate, and sleep monitoring.

**2.1 Limitations of the Data**

•	**Outdated Information:** The data was collected in 2016, raising the possibility that user activities and habits have evolved since the data gathering.

•	**User Count**: The dataset encompasses information from only 30 users, representing a limited sample size.

•	**Data Collection:** The information was gathered through a survey, prompting concerns about the integrity of the data.

**2.2 Credibility of the Data (ROCCC rule)** 

As per the course teachings, adhering to the ROCCC rule for good data entails considerations in the following areas:

**Reliable** = LOW: The dataset's reliability is compromised by its inclusion of only 30 users.

**Original** = MED: The data is sourced from a reputable third party, Amazon Mechanical Turk.

**Comprehensive** = MED: The dataset exhibits moderate comprehensiveness by covering various fitness-related categories.

**Current** = LOW: The data's currency is low since it was collected in 2016.

**Cited** = LOW: The source of citation for the data remains unidentified.

**2.3 Data selection**

The dataset comprises 18 Excel files. However, I opted to analyze a subset of 5 files, specifically focusing on the :

```sql

dailyActivity_merged.csv

dailyCalories_merged.csv

dailySteps.csv

sleepDay_merged.csv

weightLogInfo.csv

```

**2.4 Tools used** 

Cleaning: Excel

Analysis & Visualisation: SQL & R

**Step 3: Process**

I plan to analyze the information in the section by: Investigating the data, Identifying and handling duplicates and null values, Converting data formats, and Querying the data.

**3.0 Data Preparation (Excel & SQL)**

To initiate my analysis, I initiated the data cleaning process in Excel. I implemented the following procedures:

1.	Checked for duplicates in the data, resulting in the removal of three entries from the 'dailySleep' category.
2.	Sorted and filtered the data to ensure uniformity across datasets.
3.	Converted the date format to MDY using the 'Text to Columns' function.
4.	Formatted numerical data into the number format, and in some cases, restricted variables to two decimal places, particularly for the 'distance' variable.
5.	Employed the 'LEN' function to ensure consistency in customer ID lengths.

The use of Excel for data cleaning provided confidence that each dataset adhered to consistent formats.

Subsequently, I transitioned to SQL to promptly determine the count of unique users in each dataset. I executed the following query and replicated the process for each dataset.

```sql
SELECT COUNT (DISTINCT ID) AS UniqueId

FROM `molten-gantry-383718.fitbit_tracker_data.dailyActivity_merged`
```
```sql
SELECT COUNT (DISTINCT ID) AS UniqueId

FROM `molten-gantry-383718.fitbit_tracker_data.dailyCalories_merged`
```
```sql
SELECT COUNT (DISTINCT ID) AS UniqueId

FROM `molten-gantry-383718.fitbit_tracker_data.dailySteps_merged`
```
```sql
SELECT COUNT (DISTINCT ID) AS UniqueId

FROM `molten-gantry-383718.fitbit_tracker_data.sleepDay_merged`
```
```sql
SELECT COUNT (DISTINCT ID) AS UniqueId

FROM `molten-gantry-383718.fitbit_tracker_data.weightLogInfo_merged`
```

Number of **unique users** per dataset:

· dailyActivity_merged — **33**

· dailySteps_merged — **33**

· dailyCalories_merged — **33**

· sleepDay_merged — **24**

· weightLogInfo_merged — **8**

•	Since the 'weight_log_info' dataset contained only 8 distinct users, I opted not to utilize it for analysis due to insufficient data.

By maintaining data integrity, determining user counts, and establishing uniform formatting across datasets, I transitioned to employing R for further analysis.

**Step 4: Analyse (R)**

I've initiated the loading process for the packages I've chosen.
```r
library(tidyverse)
library(skimr)
library(dplyr)
library(tidyr)
library(janitor)
library(readr)
library(lubridate)
library(ggplot2)
```

Upon completing the package loading, I proceeded to import the datasets that have been preprocessed or cleaned.

```r
activity <- read_csv("~/Desktop/Case_study_bellabeat/Fitabase Data 4.12.16-5.12.16/dailyActivity_merged.csv")
calories <- read_csv("~/Desktop/Case_study_bellabeat/Fitabase Data 4.12.16-5.12.16/dailyCalories_merged.csv")
steps <- read_csv("~/Desktop/Case_study_bellabeat/Fitabase Data 4.12.16-5.12.16/dailySteps_merged.csv")
sleep <- read_csv("~/Desktop/Case_study_bellabeat/Fitabase Data 4.12.16-5.12.16/sleepDay_merged.csv")
```

Subsequently, I aimed to preview each dataset using the head() function, resulting in the generation of the following tabular displays.

<img width="925" alt="Screenshot 2023-12-13 at 2 19 55 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/ebf34d13-3a69-4c5e-b979-24fd85be6edf">


After reviewing the clean datasets in R, I used diverse features to extract essential insights and observations.


•	I grouped together the total steps of users to categorize them based on their levels of activity:

```r
activity <- activity %>%
  mutate(Activeness = case_when(
    TotalSteps < 6000 ~ "Inactive",
    TotalSteps < 8999 ~ "Low Activity",
    TotalSteps < 10000 ~ "Moderate Activity",
    TotalSteps < 13000 ~ "High Activity",
    TRUE ~ "Very High Activity"
  ))
```


•	Subsequently, I used the colnames(activity) function to confirm the inclusion of the column. Once verified, I proceeded to summarize the distribution of activity levels as percentages.


```r
colnames(activity)

activity_summary <- activity %>%
  group_by(Activeness) %>%
  summarise(n = n()) %>%
  mutate(percentage = n / sum(n) * 100)
```


•	After generating the activity_summary dataframe, I aimed to examine this dataset to acquire statistical insights regarding activity levels.

```r
View(activity_summary)

# the following dataframe was viewed
```

<img width="362" alt="Screenshot 2023-12-13 at 2 29 50 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/561864b4-aa40-4f95-b3cd-fd1c918d4a75">


•	The summary indicates that the majority of the recorded data, amounting to 39%, originates from inactive users based on total steps. In contrast, only 33% of the recorded data comes from highly/very highly active users, while users with low/moderate activity levels contributed 29% of the recorded data.

Furthemore, to carry out later visualisations I had to merge both activity and sleep.


```r
# creating the new dataframe

activity_sleep <- merge(activity, sleep, by = 'Id')

# then finding the average amount of sleep each activeness category gets

activity_sleep_avg <- activity_sleep %>%
  group_by(Activeness) %>%
  summarize(avg_minutes_asleep = mean(TotalMinutesAsleep)) %>%
  mutate(Activeness = reorder(Activeness, avg_minutes_asleep)) 

# viewing the data as a tibble to show the averages

View(activity_sleep_avg)
```

<img width="365" alt="Screenshot 2023-12-13 at 2 34 21 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/dcb15456-423e-433e-a950-7012a9ebee95">


Observing the data, users across all category levels appear to obtain a comparable amount of sleep. Notably, individuals categorized as 'Very High Activity' receive an average of 6.5 hours of sleep per night. In contrast, those classified as 'Inactive' enjoy an additional 0.7 hours of sleep (equivalent to 42 minutes), resulting in a total of 7.2 hours per night.

After extracting important insights from a thorough examination of the data, the upcoming section will provide visual representations to reveal further discoveries.


**Step 5: Share**


In this section, we will display multiple visualizations intended to identify corelation between the data and other significant factors that are of interest to Bellabeat.

**5.0 Total Steps vs Calories Burned **

To examine the correlation between the two variables, I chose for a scatterplot to visualize the results.

```r
ggplot(data = activity) +
  geom_smooth(mapping = aes(x = TotalSteps, y = Calories)) +
  geom_point(mapping = aes(x = TotalSteps, y = Calories, color = Calories)) +
  labs(title = "Total Steps vs Calories Burned", x = "Steps") +
  scale_color_gradient(low = "yellow", high = "red")
```

<img width="929" alt="Screenshot 2023-12-13 at 2 42 21 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/9e2b1b33-9932-4ab7-9f71-f496737c48ba">


The scatterplot illustrates a positive correlation between total steps and calories burned. The visual representation suggests that individuals who consume more calories tend to take a higher number of steps per day.


**5.1 Visualization of activity levels by category.**

I concluded that creating visualizations for the previously defined activity categories would offer a crucial insight into the users' activity levels based on their daily step counts:

```r
ggplot(activity_summary, aes(x="", y=percentage, fill=Activeness)) +
  geom_bar(stat="identity", width=1, color="white") +
  coord_polar("y", start=0) +
  labs(title="Activity Category Distribution", fill="Activity Category")
```


<img width="863" alt="Screenshot 2023-12-13 at 2 46 25 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/0dab178c-b2a5-48b1-b14a-32e70c0c9bdb">


The representation of the most active users in red and purple indicates that inactive users still constitute the majority, holding the largest percentage of users within that category. Additionally, the low to moderate users also encompass a larger portion of users compared to the most active ones.


**5.2 Comparison between Total Distance and Calories Burned.**

If we think about it, it might seem obvious that people who travel longer distances might burn more calories. However, this doesn't tell us whether it's the distance itself that causes more calories to be burned or if it's the level of activity that matters more.

```r
ggplot(data = activity, mapping=aes(x = Calories, y = TotalDistance, color = Calories)) +
+     geom_point() +
+     geom_smooth(method = "loess", span = 0.5, se = FALSE) +
+     labs(title = "Total Distance Travelled vs Calories Burnt", x = "Calories Burnt") +
+     scale_color_gradient(low = "green", high = "red")
```


<img width="928" alt="Screenshot 2023-12-13 at 2 49 35 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/f9f7f6ce-e457-4b36-a700-b15cad281cd1">


I wanted to show how the total distance a person travels is connected to the calories they burn. So, I used a smoother line that highlights the trend. When you go further, you burn more calories. Using the geom_smooth(method = "loess") helped me make this relationship clear.

Thus, we can connect the earlier activity categories to this correlation. Those who burn more calories tend to walk longer distances each day, placing them in the high or very high activity categories.


**5.4 Sleep and Activity Levels Analysed.**

Finally, I aimed to investigate whether there was a connection between the assigned activity levels of users and the duration of their sleep. To achieve this, I had to generate a new dataset that combines information on both sleep and activity levels.

```r
activity_sleep <- merge(activity, sleep, by = 'Id')
```

This enabled me to determine the average duration of sleep (in minutes) for users in each level of activity. I reordered the data to follow a logical sequence, ranging from inactive to very high:

```r
activity_sleep_avg <- activity_sleep %>%
  group_by(Activeness) %>%
  summarize(avg_minutes_asleep = mean(TotalMinutesAsleep)) %>%
  mutate(Activeness = reorder(Activeness, avg_minutes_asleep))
```

Now, to represent the findings graphically, I will create a bar chart:

```r
ggplot(activity_sleep_avg, aes(x = Activeness, y = avg_minutes_asleep, fill = Activeness)) +
  geom_bar(stat = "identity") +
  scale_fill_manual(values = c("green", "blue", "purple", "orange", "red")) +
  labs(title = "Average Sleep Time by Activity Group", x = "Activity Group", y = "Average Sleep Time (minutes)") +
  theme_bw()
```

<img width="921" alt="Screenshot 2023-12-13 at 2 56 11 AM" src="https://github.com/aqibparvez13/Bellabeat-Case-Study/assets/153671648/ed8acce2-731f-410c-8950-429c3e96ab09">


According to the bar chart, there isn't a significant distinction in the time allocated to each activity group. As previously noted, **individuals with lower activity levels tend to have longer sleep durations, whereas those with higher activity levels have shorter sleep durations.**

**Step 6: Act**

In this phase, I generated various recommendations for Bellabeat, outlining ways in which they can apply the insights obtained from the study to make concrete improvements.

**Key Findings:**

•	A higher percentage of users (38%) are characterized as relatively inactive compared to those who engage in frequent exercise (32%).

•	Users covering greater distances in their walks tend to burn more calories and exhibit a higher likelihood of being active compared to those who take fewer steps.

•	Individuals with the least physical activity tend to have longer sleep durations, whereas those with the highest exercise levels tend to sleep the least.

•	There is a positive correlation observed between calories burned and the number of steps taken, indicating that as users complete more steps per day, they also burn more calories.

**Actionable suggestions for improvement**

•	Implement push notifications to encourage users to achieve their daily step targets, enhancing user interaction with the technology and promoting better health through increased physical activity.

•	Provide incentives for users engaged in extensive exercise to prioritize and achieve the necessary amount of rest essential for body repair.

•	Introduce a daily calorie burn goal for users aiming to lose weight, motivating them to cultivate healthier habits, such as walking more.









































