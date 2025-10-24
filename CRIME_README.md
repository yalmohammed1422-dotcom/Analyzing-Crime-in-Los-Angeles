# Los Angeles Crime Analysis

A comprehensive data analysis project exploring crime patterns in Los Angeles, focusing on temporal trends, geographic hotspots, and victim demographics.

## Overview

This project analyzes LA crime data to uncover critical insights about:
1. Peak crime hours throughout the day
2. High-crime areas during night hours (10 PM - 4 AM)
3. Victim age group distributions and vulnerability patterns

## Features

- **Temporal Analysis**: Identifies peak crime hours and time-of-day patterns
- **Night Crime Focus**: Analyzes crimes occurring between 10 PM and 4 AM
- **Geographic Insights**: Determines high-risk areas, especially at night
- **Demographic Analysis**: Examines crime victims by age groups
- **Comprehensive Visualizations**: 7 matplotlib charts revealing crime patterns

## Requirements

```python
pandas
matplotlib
numpy
```

Install dependencies:
```bash
pip install pandas matplotlib numpy
```

## Dataset

The analysis expects a DataFrame named `crimes` with the following columns:
- `TIME OCC`: Time of crime occurrence (format: HHMM as string)
- `AREA NAME`: Geographic area/neighborhood name
- `Vict Age`: Age of the victim (numeric)

## Analysis Breakdown

### Analysis 1: Peak Crime Hour

**Objective**: Identify the hour of day with the highest crime frequency

```python
# Extract hour from TIME OCC
crimes['hour'] = crimes['TIME OCC'].str[0:2]

# Find peak hour
peak_crime_hour_str = crimes["hour"].value_counts().idxmax()
peak_crime_hour = int(peak_crime_hour_str)
```

**Key Insights**:
- Identifies most dangerous time of day
- Helps optimize police patrol schedules
- Reveals daily crime rhythm

**Visualizations**:
- 24-hour crime distribution (bar chart with highlighted peak)
<img width="3182" height="1380" alt="image" src="https://github.com/user-attachments/assets/084d83a6-4ed5-4179-bd26-68cc01cf800e" />

- Time period groupings (Early Morning, Morning, Afternoon, Evening)
<img width="2382" height="1377" alt="image" src="https://github.com/user-attachments/assets/54adfe55-6c89-4755-9efb-3c5246267583" />

- Line plot showing hourly crime trend
<img width="3182" height="1381" alt="image" src="https://github.com/user-attachments/assets/5d9e4ee9-3298-4862-a590-d7d1d6b8e50b" />

---

### Analysis 2: Peak Night Crime Location

**Objective**: Identify the area with most crimes during night hours (10 PM - 4 AM)

```python
# Define night period (after 10 PM or before 4 AM)
crimes['night'] = (crimes['hour'] > '22') | (crimes['hour'] < '4')

# Filter night crimes
crimes_night = crimes[crimes['night'] == True]

# Find peak location
peak_night_crime_location = crimes_night['AREA NAME'].value_counts().idxmax()
```

**Key Insights**:
- Identifies high-risk areas after dark
- Informs targeted night patrol strategies
- Reveals areas needing enhanced lighting/security

**Visualizations**:
- Top 10 night crime locations (horizontal bar chart)
<img width="2781" height="1580" alt="image" src="https://github.com/user-attachments/assets/12a8eb87-e872-4451-a4ee-66c6ce9602d6" />

---

### Analysis 3: Victim Age Groups

**Objective**: Analyze crime victim demographics by age categories

```python
# Define age bins and labels
group_bins = [0, 17, 25, 34, 44, 54, 64, 100]
group_labels = ["0-17", "18-25", "26-34", "35-44", "45-54", "55-64", "65+"]

# Create age groups
crimes['age_group'] = pd.cut(crimes['Vict Age'], bins=group_bins, labels=group_labels)

# Get distribution
victim_ages = crimes['age_group'].value_counts()
```

**Key Insights**:
- Identifies most vulnerable age groups
- Informs targeted crime prevention programs
- Reveals age-specific victimization patterns

**Visualizations**:
- Age group bar chart with counts
<img width="2382" height="1380" alt="image" src="https://github.com/user-attachments/assets/abc86957-85aa-44c3-bc2f-26a5dcee9848" />

- Age group pie chart with percentages
<img width="1892" height="1979" alt="image" src="https://github.com/user-attachments/assets/f53149c5-ceee-4979-8b42-7dd25f0a0a67" />

- Raw age distribution histogram (with mean/median)
<img width="2782" height="1379" alt="image" src="https://github.com/user-attachments/assets/7729dd98-6fa9-4280-a7a3-c30ff9c47000" />

---
*A data-driven approach to understanding and preventing crime in Los Angeles through temporal, geographic, and demographic analysis.*


This analysis is based on reported crime data and may not reflect unreported crimes. Crime patterns can change over time. Always consult official law enforcement sources for current safety information.
