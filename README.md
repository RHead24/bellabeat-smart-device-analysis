# bellabeat-smart-device-analysis
a data analytics case study tracking smart device health data to find growth opportunities for Bellabeat
**Google Data Analytics Capstone Project**

## Project Overview
This repository contains a data analysis case study on Bellabeat, a high-tech manufacturer of health-focused smart products for women. The goal is to analyze smart device fitness data to unlock new growth opportunities for the company.

## Data Preparation & Staging
* **Data Source:** Fitbit Fitness Tracker Data (Kaggle public dataset).
* **Storage & Environment:** Data uploaded and staged inside **Google BigQuery**.
* **Ingestion Notes:** Resolved raw CSV timestamp formatting conflicts by configuring BigQuery's advanced ingestion settings (allowing an error threshold to bypass trailing file glitches while preserving core data integrity).
## Processing/Cleaning 
* Rows showing 0 total steps paired with 1440 sedentary minutes were flagged as 'device non-wear days' and excluded from behavioral trend calculations to avoid skewing the true active baseline.
* The sleep_day and hourly_steps tables stored tracking IDs as text strings, which conflicted with the 64-bit integers (INT64) in daily_activity. Data cleaning was executed via runtime SQL CAST functions to homogenize schemas without altering the structural raw data.
* FitBit string timestamps included trailing 12:00:00 AM markers across all dates in the sleep logs. SPLIT() and SAFE.PARSE_DATE regular expressions were deployed to isolate clean, indexable dates (YYYY-MM-DD) for standard table joins.
## Analysis & Queries
* Ran a query to determine number of rows and unique users.
* Results of first query: 1	daily_activity	940 total rows	33 unique users.
2	sleep_day  	413 total rows	24 unique users.
3	hourly_steps	22099 total rows.	33 unique users. 
4	weight_log 	67 total rows	8 unique users.
* Ran second query to find user overlap between activity and sleep records.
* Results of second query: Proved 33 activity users vs 24 sleep users. 413 overlapping records.
* Ran third query to determine average time spent in various tiers of activity in correlation to sleep data.
* Results of third query: 1. Highly Sedentary (>12 hrs)	204	total logged days 367.8 average minutes asleep	6.1 average hours asleep	31.5 average minutes awake in bed.
2. Moderately Sedentary (8-12 hrs) 182 total logged days 	466.5 average minutes asleep	7.8 average hours asleep	47.1 average minutes awake in bed.
3. Active / Low Sedentary (<8 hrs)	27 total logged days	493.0 average minutes asleep	8.2 average hours asleep    43.4 average minutes awake in bed.
* Ran fourth query to show daily activity such as average daily steps and time spent at different activity tiers.
* Results of fourth query (and relation to Global Daily Activity Baselines):
-- Average Daily Steps: 7,638 steps (Below 10k target)
-- Average Sedentary Minutes: 991.2 mins (~16.5 hours of inactivity)
-- Average Very Active Minutes: 21.2 mins
-- Average Fairly Active Minutes: 13.6 mins
-- Average Lightly Active Minutes: 192.8 mins
* Ran fifth query to see how many users manually or automatically logged entries for weight.
* Results for fifth query: -- Total Participation: 8 out of 33 users (75%+ drop-off in tracking compliance).
-- Split: 5 users manually logged 41 entries. 3 users automatically synced 26 entries.
Initial commit: Add project overview and staging notes.
Additional commits: Add sections for processing and analysis.
