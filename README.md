# Dsa210begum
# Analyzing Personal Netflix Viewing Patterns

## Introduction
Netflix is one of the most popular streaming platforms, offering a vast collection of movies, TV shows, and documentaries. Understanding personal viewing habits can provide insights into content preferences, binge-watching behaviors, and the impact of recommendations. This project aims to analyze individual Netflix watch history by scraping the viewing activity from the Netflix website.

## Project Scope
This project will focus on extracting and analyzing Netflix watch history to identify patterns in content consumption. The key objectives include:
- Extracting watch history directly from Netflix through web scraping.
- Analyzing watch time distribution and content preferences.
- Investigating seasonal or time-based trends in viewing behavior.

## Data Acquisition
The primary source of data will be a self-scraped dataset obtained from the Netflix website. This dataset will include:
- Titles watched (movies, TV series, documentaries, etc.).
- Date and time of viewing.
- Duration and frequency of watching.
- Genre categorization (if available).

The data extraction will be performed using automated web scraping techniques, ensuring accurate retrieval of personal viewing history.

## Methodology
### 1. Data Cleaning and Preprocessing
- Removing duplicate entries and errors.
- Formatting timestamps for proper time-based analysis.
- Categorizing content based on type, genre, or other relevant attributes.

### 2. Exploratory Data Analysis (EDA)
- Identifying peak watching hours and preferred genres.
- Detecting binge-watching patterns and content consumption trends.
- Analyzing how frequently different types of content are watched.

### 3. Trend Analysis
- Investigating how viewing habits change over time (e.g., weekdays vs. weekends, seasonal patterns).
- Assessing whether Netflix recommendations influence content choices.

## Goals and Expected Insights
This project aims to provide:
- A structured and clean dataset of Netflix viewing history.
- A visual representation of personal content consumption trends.
- Meaningful insights into how and when Netflix is used.




# What we got?

---

## Table of Contents

1. [Data & Feature Engineering](#data--features)  
2. [Exploratory Data Analysis](#eda)  
3. [Hypothesis Testing](#hypothesis-testing)  
4. [Machine Learning Models](#machine-learning-models)  
5. [Conclusions](#conclusions)  

---

## Data & Feature Engineering

- **Source**: `user_data_tiktok.json` exported from TikTok  
- **Records**: 12 345 watch events  
- **Enrichments**:  
  - `day_of_week` (Monday…Sunday)  
  - `time_bin` (Morning/Afternoon/Evening/Night)  
  - `is_holiday` (weekends + national holidays)  
  - `duration_min` (session durations)  
  - `SeasonBin` (Winter, Spring, Summer, Fall)  

---

## Exploratory Data Analysis

### 1. Watch Count by Day of Week  
![Watch Count by Day of Week](fig1_day_of_week.png)  

### 2. Watch Count by Time of Day  
![Watch Count by Time of Day](fig2_time_of_day.png)  

### 3. Holiday vs Non-Holiday Usage  
![Holiday vs Non-Holiday](fig3_holiday_vs_nonholiday.png)  

### 4. Session Duration Distribution  
![Session Duration](fig4_session_duration.png)  

### 5. Binge Watching Trends  
![Binge Trends](fig5_binge_trends.png)  

### 6. Views by Season  
![Views by Season](fig6_views_by_season.png)  

### 7. Watch Duration by Season  
![Duration by Season](fig7_duration_by_season.png)  

### 8. Correlation Matrix  
![Correlation Matrix](fig8_corr_matrix.png)  

### 9. Rolling 3-Month Moving Average of Daily Views  
![Rolling Trend](fig9_rolling_trend.png)  

*(…plus 6 more plots in the notebook: heatmaps for day×hour, KDE of time-bin distributions, autocorrelation, pair-plots, elbow plot for sessions, etc.)*

---

## Hypothesis Testing

| Test                                        | Statistic    | p-value  | Conclusion                          |
|---------------------------------------------|-------------:|---------:|-------------------------------------|
| Weekend vs Weekday daily views              | t = 1.68     | 0.0943   | No significant difference (α=0.05)  |
| Winter vs Summer binge-day rate (χ²-test)    | χ² = 8.41    | 0.0037   | Significant difference              |
| Weekend vs Weekday total daily duration     | t = 2.05     | 0.0411   | Significant difference              |

---

## Machine Learning Models

### 1. Classify `time_bin`  
- **Features**: hour, day-of-week, weekend flag, month  
- **Model**: RandomForestClassifier (200 trees)  
- **Accuracy**: 72%  
- **Confusion Matrix**:  
  ![CM time_bin](fig10_cm_time_bin.png)  

### 2. Classify `day_of_week`  
- **Features**: hour, weekend flag, month  
- **Model**: RandomForestClassifier (200 trees)  
- **Accuracy**: 58%  
- **Confusion Matrix**:  
  ![CM day_of_week](fig11_cm_day_of_week.png)  

### 3. Regress Daily View Count  
- **Features**: weekday number, weekend flag, month  
- **Model**: RandomForestRegressor (200 trees)  
- **MAE**: 2.3 views/day  
- **R²**: 0.68  
- **Predicted vs True**:  
  ![Pred vs True](fig12_pred_vs_true.png)  

---

## Conclusions

- **Temporal patterns**: peaks in mid-week mornings.  
- **Holiday effects**: mixed—no strong difference in raw counts, but binge behavior varies by season.  
- **Seasonality**: statistically significant shifts in binge rates between Winter and Summer.  
- **Predictive models**: moderate accuracy; time-bin classification is easier (72%) than day-of-week (58%).  
- **Next steps**: integrate video metadata, refine session definitions, and explore time-series forecasting.

---

> _All code, plots, and results are contained in the accompanying Jupyter notebooks._  

