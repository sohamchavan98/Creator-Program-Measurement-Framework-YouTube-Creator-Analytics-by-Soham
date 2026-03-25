![Dashboard Preview](dashboard_preview.png)

# HardScope Creator Program Measurement Workspace

### YouTube Tech Reviewer Analysis

**Stack:** Python · YouTube Data API v3 · Pandas · Power BI

Submission for **HardScope — Lead Analyst, Creator Strategy & ROI Measurement Challenge**

---

# Program Context

This project evaluates the performance of a **technology creator marketing program** using public YouTube performance data.

The partnerships team needs answers to three questions:

1. What did we actually get from this creator program?
2. Which creators and formats are working?
3. Where should we allocate creator budget next quarter?

To answer those questions this workspace builds a lightweight measurement system:

data pipeline → modeled dataset → analytics dashboard → executive recommendations.

---

# Data Source

All data was collected from the **YouTube Data API v3**.

The API returns public performance metrics for creators and videos without requiring channel authorization.

Endpoints used:

| Endpoint      | Data Returned                          |
| ------------- | -------------------------------------- |
| channels.list | subscriber counts and channel metadata |
| search.list   | recent videos per creator              |
| videos.list   | views, likes, comments, duration       |

Dataset summary:

* 8 tech creators
* 220 videos
* 227M total views

Creators analyzed include:

MKBHD
Linus Tech Tips
JerryRigEverything
Unbox Therapy
Dave2D
TechLinked
Arun Maini
MrMobile

---

# Measurement Framework

The measurement system is built around a **three-layer creator marketing funnel**.

## Awareness

Measures reach and audience exposure.

Metrics:

Views
Subscribers
Average views per video

---

## Engagement

Measures audience interaction and attention.

Metrics:

Engagement rate
Like rate
Comment rate

Formula:

```
Engagement Rate = (likes + comments) / views
```

---

## Consideration (Intent Proxy)

Direct purchase signals are not available via the public YouTube API.

Intent is approximated using behavioral proxies.

Metrics:

Views per subscriber
Views per day
Comment rate

These metrics indicate deeper audience interest beyond passive viewing.

---

# Creator Marketing Funnel

Program-level funnel:

Views (Awareness)
227M

Engagements
8M → **3.36% engagement rate**

Comments
~0.22% comment rate

The funnel visual highlights where audience interaction drops across the creator program.

---

# Engineered Analytics Features

The dataset includes engineered metrics derived during data transformation.

| Feature          | Description                   |
| ---------------- | ----------------------------- |
| engagement_rate  | (likes + comments) / views    |
| like_rate        | likes / views                 |
| comment_rate     | comments / views              |
| views_per_sub    | reach efficiency              |
| views_per_day    | recency-adjusted performance  |
| duration_bucket  | video length category         |
| performance_tier | top / mid / bottom performers |

Two analytics tables are produced:

videos (video-level dataset)
channel_summary (creator rollup)

---

# Dashboard Overview

The Power BI dashboard contains four pages designed for marketing stakeholders.

---

## Program Overview

High-level creator program performance.

Includes:

program KPI cards
creator marketing funnel
engagement benchmark comparison
views by creator
video distribution

Purpose: assess overall program health.

---

## Video Performance Deep Dive

Analyzes creator performance and identifies scaling opportunities.

Key visual:

**Creator Performance Matrix**

Axes:

Views (reach)
Engagement rate (quality)

Quadrant interpretation:

High reach + high engagement → scale creator
High reach + low engagement → optimize content
Low reach + high engagement → promote distribution
Low reach + low engagement → reduce investment

---

## Format & Engagement Analysis

Evaluates the impact of video format.

Insights:

Long-form videos (>20 min) generate the highest engagement and highest average views.

Short videos (<5 min) consistently underperform.

Visuals include:

engagement by video length
views by format
performance tier distribution
creator × format heatmap

---

## Recommendations & Creator Scorecard

Final decision layer.

Includes:

creator scorecard table
engagement heatmap
views per day analysis
written strategic recommendations

---

# Key Findings

1. TechLinked shows the strongest engagement efficiency (5.12% ER and 0.24 views per subscriber).

2. Long-form videos consistently outperform shorter formats across both engagement and views.

3. MrMobile produces highly engaging long-form content but requires stronger distribution.

4. MKBHD delivers the largest reach but engagement sits near the benchmark threshold.

5. Short videos underperform across most creators.

---

# Limitations

Public platform data introduces several limitations.

| Limitation                         | Impact                       |
| ---------------------------------- | ---------------------------- |
| No watch-time data                 | cannot measure retention     |
| No click-through data              | conversion layer not visible |
| No branded search signal           | discovery intent unknown     |
| Low video counts for some channels | averages less reliable       |

These limitations are documented transparently rather than hidden.

---

# Architecture Decisions

Python was used for:

data ingestion
feature engineering
dataset modeling

Power BI was used for:

interactive dashboards
creator comparison
decision-oriented reporting

This approach separates data engineering from visualization while keeping the workflow reproducible.

---

# Running the Project

Install dependencies:

```
pip install requests pandas openpyxl python-dotenv
```

Create a `.env` file:

```
YOUTUBE_API_KEY=your_api_key
```

Run pipeline:

```
python 01_fetch_channels.py
python 02_fetch_videos.py
python 03_clean_transform.py
python 04_export.py
```

Open Power BI and load:

```
hardscope_output/yt_tech_reviewers.xlsx
```

---

# Future Improvements

With additional time the project would expand to include:

Google Trends search lift data
cross-platform creator analysis
conversion tracking via GA4
automated weekly reporting pipeline
creator performance monitoring alerts

---

# What This Project Demonstrates

This workspace demonstrates the core skills required for creator program analytics:

data sourcing
measurement framework design
analytics modeling
dashboard reporting
strategic recommendation development

---

Built for **HardScope — Lead Analyst Creator Strategy & ROI Measurement Challenge**
