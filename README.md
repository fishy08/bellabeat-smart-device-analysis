# Bellabeat Smart Device Analysis

Google Data Analytics Capstone — Case Study 2
Peter Francis Muthukkalai

## Overview

This case study was completed as part of the Google Data Analytics Professional Certificate. I took on the role of a junior data analyst tasked with analysing smart device usage data to uncover how consumers engage with wellness technology — and applying those insights to one Bellabeat product.

The core business question was:

> "How do consumers use non-Bellabeat smart devices, and what does that reveal for Bellabeat's marketing strategy?"

The findings were used to generate three strategic recommendations for the **Bellabeat Leaf** wellness tracker, focused on movement reminders, sleep quality, and personalised user goals.

\---

## Business Context

Bellabeat is a high-growth wellness technology company that designs health-focused smart devices for women. Its product range includes the Leaf tracker, the Time watch, and the Spring smart water bottle — all connected via the Bellabeat app, which provides data on activity, sleep, stress, and reproductive health.

While Bellabeat has established a strong presence in the wellness market, the marketing team identified an opportunity to use smart device usage data to better understand consumer behaviour and refine product positioning. Rather than relying on assumptions, the goal was to let real-world usage patterns drive the strategy.

\---

## Tools Used

|Tool|Purpose|
|-|-|
|BigQuery (SQL)|Data exploration, cleaning, and all analysis queries across Phases 1–3|
|Tableau Public|Interactive dashboards and visualisations|
|Microsoft PowerPoint|14-slide executive presentation deck|
|Microsoft Word|Full analytical report|

\---

## Data Source

* **Provider:** Möbius via Kaggle (CC0 Public Domain licence)
* **Original source:** FitBit Fitness Tracker Data — consented personal tracker data
* **Period:** 31 days (12 April – 12 May 2016)
* **Size:** 33 FitBit users across 5 tables
* **Tables used:** daily\_activity, sleep\_day, hourly\_steps, hourly\_intensities, weight\_log
* **Privacy:** No personally identifiable information included

\---

## Data Cleaning

Before analysis, all five tables were audited in BigQuery. The following issues were identified and resolved:

|Issue|Decision|Reasoning|
|-|-|-|
|3 duplicate rows in sleep\_day|Removed|Identical user ID and date — double-counted entries|
|84 invalid days in daily\_activity|Removed|TotalSteps = 0 AND SedentaryMinutes = 1440 — device not worn|
|Fat column in weight\_log (97% null)|Excluded|Smart scale required — not available to most participants|
|Mixed timestamp formats in hourly tables|Standardised|CASE / PARSE\_TIMESTAMP applied to ensure consistent UTC format|
|Sedentary minutes include sleep|Documented|Fitbit counts all inactivity; comparisons made relatively between segments|

\---

## Analysis \& Key Findings

### 1\. Activity by Day of Week — The Saturday Leisure Peak

!\[Steps by Day of Week](charts/chart1_steps_day.png)

Users average 8,329 daily steps — 17% below the WHO 10,000-step goal. Saturday is the most active day at 8,979 steps, driven by leisure activity rather than habit. Sunday and Friday are the weakest days. Monday records the highest sedentary time (16.4 hours), suggesting a work-week onset effect. This pattern mirrors what Cyclistic found with casual riders: activity is recreational, not routine.

\---

### 2\. Activity by Hour — Three Peaks and a Critical Dip

!\[Steps by Hour of Day](charts/chart2_steps_hour.png)

Three clear activity windows emerge across the day: morning (8–10am), lunch (12–2pm), and evening (5–7pm, peaking at 6pm with 599 avg steps/hour). Crucially, a consistent **3pm dip** drops activity to 406 avg steps — the lowest point of the active day. This is the single most actionable finding in the dataset: it identifies a precise, daily window for a Leaf movement reminder.

\---

### 3\. Sleep Quality — The Sunday Paradox

!\[Sleep Quality by Day](charts/chart3_sleep_day.png)

Users average 7.0 hours of sleep per night — just meeting the minimum recommended threshold — but spend 39 minutes awake in bed nightly, indicating poor sleep quality rather than a duration problem. The Sunday paradox stands out: Sunday has the most time in bed (8.4 hours) yet the worst sleep quality (50.8 minutes awake). Anticipatory work-week stress is the likely driver. This is a clear, underserved use case for a Leaf wind-down programme.

\---

### 4\. User Segments — Who Are These Users?

!\[User Activity Segments](charts/chart4_user_segments.png)

Users were segmented into four tiers by average daily step count. Moderately Active users (33.3%) are the largest group and sit closest to the Active threshold — making them the highest-priority conversion target. With relatively small step increases, this segment could cross into Active behaviour. Sedentary users (21.2%) represent a separate challenge that likely requires different messaging and product features.

\---

### 5\. Sedentary Behaviour Across Segments

!\[Sedentary Hours by Segment](charts/chart5_sedentary_segment.png)

Even the most Active users average 16.2 sedentary hours per day — demonstrating that high step counts do not prevent prolonged inactivity. The Sedentary segment averages 18.2 hours. Paradoxically, Lightly Active users (17.7h) sit above Active users in sedentary time despite a moderate step count, suggesting that activity is concentrated in short bursts. Sedentary behaviour is a universal problem across all segments, not just the least active users.

\---

### 6\. Active Minutes Breakdown — The Real Picture of the Day

!\[Active Minutes Breakdown](charts/chart6_active_minutes.png)

Breaking the day into activity intensity types reveals the full extent of inactivity. Sedentary time accounts for 951.8 minutes per day — 66% of a 24-hour day. Very Active minutes total just 23.2 per day, which is close to the recommended 20–30 minutes of vigorous daily exercise, but users are not consistently reaching it. The gap between intent and habit is where the Leaf can intervene.

\---

## Summary

|Dimension|Finding|Implication|
|-|-|-|
|Avg daily steps|8,329 steps/day|17% below WHO 10,000 goal|
|Peak activity day|Saturday (8,979 steps)|Leisure-driven, not habitual|
|Peak activity hour|6pm (599 avg steps/hr)|Post-work exercise window|
|Critical dip|3pm — lowest daytime activity|Optimal reminder trigger|
|Avg sleep|7.0 hrs/night|At minimum threshold|
|Sleep quality|39 mins awake/night|Poor wind-down routines|
|Sunday paradox|Most time in bed, worst quality|Anticipatory work stress|
|Largest segment|Moderately Active (33.3%)|Highest conversion priority|
|Sedentary time|15.9 hrs/day across ALL segments|Universal — not just inactive users|

**Core insight:** Users are not inactive by choice — they move when reminded (commute, lunch, post-work) but spend the rest of the day sedentary without realising it. The Leaf's opportunity is to close the gap between the activity users already do and the activity they could do with the right nudge at the right time.

\---

## Top 3 Recommendations

### 01 · Smart Movement Reminders at the 3pm Dip *(Highest Priority)*

Deploy a haptic movement reminder via the Leaf at 3pm daily — the most consistent, data-evidenced low-activity point across all users. Supplement with a Monday morning step challenge to counter the work-week sedentary spike. Goals should be personalised per activity segment so the nudge feels relevant, not generic.

**Messaging:** *"You've been still for a while — a 5-minute walk changes everything."*

\---

### 02 · Sunday Wind-Down Programme *(Sleep \& Retention)*

Build a guided Sunday evening wind-down sequence in the Bellabeat app, triggered when the Leaf detects low movement and high restlessness in the pre-sleep window. The programme should include breathing exercises and screen-off reminders, targeting the 50.8-minute average time users spend awake in bed on Sunday nights. Reducing this single data point would deliver a measurable, shareable wellness win for users.

**Messaging:** *"Sunday sorted — wake up Monday ready."*

\---

### 03 · Personalised Goals by Activity Segment *(Conversion \& Engagement)*

Classify users into activity segments at onboarding based on their first two weeks of Leaf data. Moderately Active users — the largest segment at 33.3% — should receive a progressive step-increase programme with weekly micro-goals and in-app coaching. The goal is not to turn them into athletes but to shift them from Moderately Active to Active through small, sustainable increases.

**Messaging:** *"You're closer than you think — let's close the gap together."*

\---

## Next Steps

* **Collect Bellabeat-specific data** — FitBit data is a useful proxy but first-party Leaf usage data would provide more accurate, directly applicable insights across Bellabeat's actual user base
* **A/B test the 3pm reminder** — Aggregate data identifies the dip; personalised testing would confirm whether a fixed 3pm trigger outperforms a user-adaptive reminder window
* **Validate the Sunday hypothesis** — Survey Bellabeat users on Sunday evening habits to confirm whether anticipatory work stress is the driver before building the wind-down programme around it
* **Build segment-aware onboarding** — Classifying users at onboarding and immediately personalising goals and reminders could drive early retention and habit formation
* **Expand the dataset** — 33 users over 31 days in 2016 limits generalisability; a larger, more recent, and more diverse dataset would significantly increase confidence in all findings

\---

## Presentation \& Report

The full deliverables are available in this repository:

📊 `Bellabeat_Analysis_Peter_Francis.pptx` — 14-slide executive presentation  
📝 `Bellabeat_Report_Peter_Francis.docx` — Full analytical report (9 pages)  
📈 `charts/` — All 6 analysis charts

🔗 [View interactive Tableau dashboard](https://public.tableau.com/app/profile/peter.francis.muthukkalai/viz/Bellabeat_Analysis_17749098758380)

\---

## About

**Peter Francis Muthukkalai**  
Google Data Analytics Professional Certificate — Capstone Project 2

This analysis was completed as part of the Google Data Analytics Certificate programme. The dataset is provided by Möbius via Kaggle under CC0 Public Domain licence.

🔗 [Case Study 1: Cyclistic Bike-Share Analysis](https://github.com/fishy08/Cyclistic-bike-share-analysis)

