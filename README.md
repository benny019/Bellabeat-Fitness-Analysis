# BELLABEAT FITNESS ANALYSIS
![](bellabeat_intro.png)
## *INTRODUCTION*
This is a capstone case study project as part of my Google Data Analytics Professional Certificate course. The case study assumes me to be a data analyst working with the marketing analyst team at **Bellabeat**, a high-tech company that manufactures health-focused smart products.They offer different smart devices that collect data on activity, sleep, stress, and reproductive health to empower women with knowledge about their own health and habits.

## Key Task
- To analyze smart device fitness data (from FitBit) in order to gain insight into how consumers use non-Bellabeat smart devices.
- Select one Bellabeat product to apply these insights to
- Come up with high-level recommendations for how these trends can inform Bellabeat marketing strategy.

## Concept Demonstrated
To successfully carry out this project, I diligently followed the six steps of data analysis processes as learnt in the course: ask, prepare, process, analyze, share, and act, using three analytical tools: Excel, SQL and Tableau. Stated below are details of tasks carried out in each step. 



## PHASE 1: ASK
In this first stage, I defined the problem to be solved, familarized myself with the business task and engaged in analytical thinking to come up with further questions to unveil deeeper answers. This should also guide me to the kind of data to use for the project, but being a case study, a dataset was already provided. 

The following overall questions will guide the analysis:
1. What are some trends in smart device usage?
2. How can these trends apply to Bellabeat customers?
3. How can these trends help influence Bellabeat marketing strategy?



## PHASE 2: PREPARE
This stage focuses on preparing the data. I downloaded the required CSV file from the provided source and stored it on my computer. The dataset used for the project  is the [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit) stored in Kaggle and made available through [Mobius](https://www.kaggle.com/arashnic). 

### Dataset Information
The dataset was generated through a survey distributed via Amazon Mechanical Turk between 12th March, 2016 and 12th May, 2016. The Kaggle data set contains personal fitness tracker data from thirty-five fitbit users who consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. It includes information about daily activity, steps, and heart rate that can be used to explore users’ habits. 

### Data Collection
The data explorer tab on Kaggle has two sepaprate folders:

*mturkfitbit_export_3.12.16-4.11.16* with 11 csv files for the date between 03/12/2016 and 04/11/2016.

*mturkfitbit_export_4.12.16-5.12.16* with 18 csv files for the date between 04/12/2016 and 05/12/2016.

I downloaded both datasets to ensure complete data coverage for the survey period. However, out of the multiple files in each folder, I only used the **daily_activities** and **sleep** files, as they contained most of the relevant information found in the other files. To proceed with the analysis, I would need to merge these datasets.

### Data Credibility & Integrity
I used Excel to quickly explore the data, gaining an understanding of their structure and organization. Afterward, I reassessed their relevance to the business task and evaluated data quality using the ROCCC framework (Reliable, Original, Comprehensive, Current, and Cited).

#### Outcome of Exploration (Limitation): 
After thorough examination of the dataset, it appeared there were some issues with the data
1. Given the small sample size (35 users) and the absence of demographic information, there is a potential for sampling bias, making it unclear whether the sample accurately represents the broader population. 
2. Additionally, the dataset is somewhat outdated, and the survey duration was limited to two months. 
3. There is no detailed information about the data set (metadata), making it hard to understand. 
4. The sleep data is incomplete as there are only details about 24 users out of 35. 



## PHASE 3: PROCESS
In this phase, I focused on ensuring data integrity through thorough cleaning, validation, and verification. I reviewed and corrected data types, ensured consistency, checked constraints, and validated data ranges based on the details provided in the source. With the cleaned data, I proceeded to organize and manipulate it for analysis, aligning each step with the business objectives.

**Data Merging:** The _activity_data_ and _sleep_data_ were stored in separate files for each of the two months, resulting in four datasets that needed to be merged for analysis. I accomplished this using SQL, applying **JOIN** and **UNION** functions.

First, I used a **LEFT JOIN** to merge the _daily_activity_ and _sleep_ data for each month (March 12 – April 11 and April 12 – May 12), using user_id and date as the primary keys. Then, I applied the UNION function to combine both merged datasets into a single dataset covering the full survey period.

After merging, I performed another round of data cleaning and validation using SQL to ensure the dataset was accurate and ready for analysis. 

#### Below are the manipulations made to the data during cleaning process:

* Change of Datatype: Formatted the Date Column in sleepDay_merged and Daily_activity sheet as Date (mm/dd/yyyy) to ensure uniformity. 
* Removed Duplicate
* Cleared all records with the date 2024-04-12 in the daily activity data table of 3.12.16 – 4.11.16
* Removed unnecessary records
* Splitted ActivityDate Column to Date and Time Columns
* Calculated the total minutes asleep per day by each ID
* Checked the result for necessary cleaning process
* Removed dates outside consideration
* Joined the daily activity data column with the sleep data of the second dataset (using left full join function)
* Removed unnecessary records such as logged activity distance
* Rename the columns headers to be easily understandable and ensure consistency and successful merging
* Merged the two datasets together to have all details in a place using Union Function.

*Note: The csv file for the merged dataset is available in the input tab (/kaggle/input/merged-data/full daily data.csv).*


## PHASE 4: ANALYZE

### Approach
With all the daily data consolidated, I could now focus on identifying trends and key insights. My analysis aimed to examine users activities, study habits such as calorie burn and sleep behavior, and then check out for possible relationship. 

I would start by examining based on users' average activity levels to gain an initial **overview**. Then, I would conduct a more in-depth investigation by grouping users based on their activity levels to uncover patterns in their behavior.

### Computation of mean data and total active minutes
Considering the stated approach, there is need to compute the daily mean value for each of the users' activity to know how they perform averagely on daily basis. From the mean data I would also compute the total active minutes for each user to be able to distribute them based on their activity intensity level.

It is worthy of note that I stuck with the WHO Physical Activity Recommendation for Adults in this computation. [check here for source](https://iris.who.int/bitstream/handle/10665/336656/9789240015128-eng.pdf?sequence=1). This ensures that the analysis remains aligned with recognized health guidelines considering that Bellabeat manufactures health-focused products. 

To calculate period of activeness, WHO considers vigorous activity more intense than moderate activity, so it counts for more in terms of time. Specifically, the WHO says "minute of vigorous-intensity activity is approximately equivalent to 2 minutes of moderate-intensity activity in terms of health benefits." Applying this to my dataset:
#### **total active mins = 2(very_active_mins) + fairly_active_mins.**

### Overview: Examining user Average Behaviour
After the computations, I unploaded the dataset into **Tableau** and began my investigation. I used majorly scatter plots to visualize how calory burn and sleep duration corelate differently with daily steps, active minutes and all activity intensity levels for each user. I also checked the calories burnt and sleeping habit by days.

### In-Depth Analysis: Examining each group of users
The idea here is to carry out a thorough analysis on the users after they have been classified into usertypes based on their activites and also classified by sleep behaviour. This will help in properly investigating the patterns and relationship between users' activities and habits. 

#### Classification into usertypes
For the classification by activities, I could not conveniently pick an activity to use between the users' daily steps and their activity intensity level, especially after seeing from the overview that both activities have significant and similar impact on the users' habits. Also with the realization that human physical activity is not only determined by steps, I decided to classify the users both based by their daily steps and activity intensity level. 

##### Steps-Based Classification
For this classification, I followed the guidelines provided by MedicineNet since WHO does not provide information on distribution by steps [source](https://www.medicinenet.com/how_many_steps_a_day_is_considered_active/article.htm)

* Sedentary: Less than 5,000 steps daily
* Low active: About 5,000 to 7,499 steps daily
* Somewhat active: About 7,500 to 9,999 steps daily
* Very active: More than 10,000 steps daily


##### Intensity-Based Classification
For this classification, I used the computed total active minutes and followed the guidelines provided by WHO. [*source*](https://iris.who.int/bitstream/handle/10665/336656/9789240015128-eng.pdf?sequence=1)

* Low Intensity: Less than 30 minutes of total active minutes per day.
* Moderately Intensity: 30-60 minutes of total active minutes per day.
* High Intensity: More than 60 minutes of total active minutes per day.


#### Classification by Sleep Behaviour
* less than 7 hours of daily sleep = bad sleepers
* 7 - 9 hours of daily sleep = normal sleepers
* more than 9 hours of daily sleep = over sleepers


After these classifications, I was then able to easily visualize patterns in user types, check their relationship with various habits and uncover any surprises in the data. 



## PHASE 5: SHARE 

### Insights From Examining Users' Average Behaviour (Overview)

1. **Investigation on Calory Burn:** Generally, the influence of users' activities on the amount of calory burn reduce by level of intensity, in fact, sedentary periods have a negative correlation.  Specifically, users' daily steps and active mins both correlates positively with amount of calory burn, though, active mins has a stronger correlation. This infer that the amount of calory burn is expected to rise as daily steps or active mins increases. (Note: active mins = 2(very active mins) + fairly active mins)
2. **Investigation on Sleep Behaviour:** The users' daily steps and active minutes both have very weak negative (or almost no) correlation with their sleep duration. Also their activities, regardless of the intensity level have barely no influence on their sleep behaviour, except for sedentary minutes which have moderately negative correlation.


### Insights from Step-Based In-depth Analysis

1. **Usertype Distribution:** The number of users in each group reduces orderly. While sedentary users claim the highest population (11), we have 9 lightly active users, 8  fairly active users and 7 very active users. Making a total of 35. 
2. **Sleep Behaviour:** There are 12 bad sleepers, 11 normal sleepers and just 1 over sleeper. It appears that sleep information is only available for 24 out of all 35 users.
3. **Activities and Habits:** The fairly active users appear to have the highest amount of calory burn and not the very active users who were associated with most daily steps and active minutes. This was no longer a surprise as the fairly active users were seen to have the least sedentary periods and best sleep habit.
4. **Sleep Habits' Underlying Effect on Users:** It turned out that most fairly active users (6 out of 8) were normal sleepers while most very active users (4 out 0f 5) were bad sleepers. A reason the very active users didn't burn most calories could most like be because of their higher sedentary periods, further traced to bad sleep habit.

### Insights From Intensity Based In-depth Analysis

1. **Usertype Distribution:** There are 15 low intensity users, 8 moderate intensity and 12 high intensity users. The sleep distribution remains the same as above.
2. **Activities and Habits:** The high intensity users have the highest amount of calory burn. This was not a surprise as they clearly have the most intensive activities, highest average daily steps, least sedentary period and as well quality sleep habits. We could see that most of the high intensity users (5 out of 9) are normal sleepers, as opposed to the other usertypes.
3. **Consistency in Intensity-based Distribution:** The trends in the intensity based analysis consistently appeared in order of distribution. This could be because the method accounted for all kinds of activities exhibited by the users as opposeed to the former where they were grouped just by their daily steps.

### Visualization

For a better interaction, click [here](https://public.tableau.com/views/BellabeatFitnessTracker_17292563592600/DashboardOverview?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link) for the visuals in Tableau Public, where you can hover between each dasboards using the navigation buttons. 



## PHASE 6: ACT

### Application to Bellabeat Company and Recommendations
1. **Portability and Choice of Product:** The lack of sleep information about some of the users is most likely due to inconvenience from using the products while sleeping.  Bellabeat should prioritize the design of highly portable devices usable at all times. Currently, I would apply my findings to the Bellabeat's Leaf product, being the most portable.
2. **Product Optimization and Health Goal:** Multiple activities contribute to certain health goals. The Leaf should be enhanced to track a wider range of health-related activities. It should also be personalized to calculate daily portion needs, monitor user commitment, and provide progress alerts and reminders. This will help users better achieve their health goals.
3. **Optimize Calorie Burn:** To optimize calorie burn, it's crucial to track both active and sedentary periods. Even highly active individuals with prolonged sedentary periods may not achieve their desired calorie burn goals.
4. **Increase User activity:** From the distributions, sedentary users claimed the highest number. Bellabeat should prioritize strategies to reduce sedentary behavior. This could involve personalized monitoring, product improvements, regular reminders, reward systems, and community-driven initiatives to inspire users to be more active.
5. **Prioritize Sleep:** Adequate sleep remains crucial for overall health and well-being. The Leaf product should be designed to effectively monitor sleep duration and provide alerts when sleep falls below the recommended 7-9 hours.
