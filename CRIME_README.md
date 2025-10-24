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
- **Comprehensive Visualizations**: 11 matplotlib charts revealing crime patterns

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
- Time period groupings (Early Morning, Morning, Afternoon, Evening)
- Line plot showing hourly crime trend

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
- Day vs Night crime pie chart
- Comparison of all crimes vs night crimes by area
- Night crime distribution by hour

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
- Age group pie chart with percentages
- Raw age distribution histogram (with mean/median)

---

## Visualizations Summary

The project includes **11 comprehensive matplotlib visualizations**:

### Temporal Analysis
1. **24-Hour Crime Distribution** - Bar chart showing crimes per hour (peak highlighted)
2. **Time Period Groupings** - Bar chart of Early Morning, Morning, Afternoon, Evening
3. **Crime Trend Line** - Smooth line plot showing daily crime pattern

### Night Crime Analysis
4. **Top 10 Night Crime Areas** - Horizontal bar chart (peak area highlighted)
5. **Day vs Night Pie Chart** - Proportion comparison
6. **Area Comparison** - All crimes vs night crimes for top 10 areas
7. **Night Hour Distribution** - Crime pattern within night hours

### Victim Demographics
8. **Age Group Bar Chart** - Victims by age category with counts
9. **Age Group Pie Chart** - Percentage distribution
10. **Age Histogram** - Raw age distribution with mean/median lines

### Overview
11. **Comprehensive Dashboard** - 4-panel view combining all key metrics

---

## Usage

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Load your data
crimes = pd.read_csv('la_crime_data.csv')

# Run the analysis script
# [Execute analysis code]
```

## Sample Output

```
Peak crime hour: 12:00 (12-hour format: 12 PM)

Crime distribution by hour (top 10):
12    15234
18    14567
15    14123
...

Number of night crimes (10 PM - 4 AM): 125,432
Peak night crime location: Central

Top 10 night crime locations:
Central        12,543
77th Street    11,234
...

Victim distribution by age group:
26-34    95,432
35-44    87,654
18-25    76,543
45-54    65,432
55-64    43,210
0-17     32,109
65+      28,876

Most victimized age group: 26-34
Least victimized age group: 65+

==================================================
Analysis Complete!
==================================================
```

## Key Findings Template

Based on the analysis, you can report:

### Temporal Patterns
- **Peak Hour**: Most crimes occur at [X]:00 
- **Dangerous Period**: [Time period] has highest crime concentration
- **Night Crime Rate**: [X]% of crimes occur between 10 PM and 4 AM

### Geographic Patterns
- **Highest Crime Area**: [Area Name] has most overall crimes
- **Night Hotspot**: [Area Name] is most dangerous after dark
- **Top 3 Risk Areas**: [List areas]

### Victim Demographics
- **Most Affected**: [Age group] is most frequently victimized
- **Youth Crime**: [X]% of victims are under 18
- **Senior Crime**: [X]% of victims are 65+
- **Prime Age**: Ages [X-Y] account for [Z]% of all victims

## Insights & Interpretations

### Why These Patterns Matter

**Temporal Insights**:
- Midday peaks often relate to property crimes in commercial areas
- Late evening spikes may indicate assault/robbery patterns
- Early morning crimes often involve burglary of businesses

**Night Crime Analysis**:
- Night crimes tend to be more violent
- Areas with entertainment districts show higher night crime
- Residential areas may see more burglaries at night

**Age Demographics**:
- Young adults (18-34) are most frequently victimized
- May reflect higher exposure through nightlife/work
- Elderly populations face different crime types (fraud, theft)

## Practical Applications

### For Law Enforcement
- **Resource Allocation**: Deploy more officers during peak hours
- **Night Patrols**: Focus on identified high-risk areas after dark
- **Targeted Programs**: Age-specific crime prevention initiatives

### For City Planning
- **Street Lighting**: Improve illumination in night crime hotspots
- **CCTV Placement**: Install cameras at peak crime locations
- **Community Centers**: Provide safe spaces for vulnerable age groups

### For Residents
- **Awareness**: Know dangerous hours and areas to avoid
- **Safety Planning**: Plan routes avoiding high-crime zones
- **Community Watch**: Organize neighborhood watch in hotspots

## Code Improvements Implemented

- ✅ **11 professional visualizations** using matplotlib only
- ✅ **Color-coded highlights** for peak values and key areas
- ✅ **Comprehensive labels** with formatted numbers (commas)
- ✅ **Multiple perspectives** on same data (bars, pies, lines)
- ✅ **Time period analysis** with logical groupings
- ✅ **Dashboard view** for holistic understanding
- ✅ **Statistical markers** (mean, median) on distributions
- ✅ **Print statements** for all key findings

## Potential Further Analysis

### Additional Analyses
- Crime type breakdown by hour/area
- Seasonal crime patterns (by month/season)
- Victim gender analysis
- Crime clearance rates by area
- Repeat victimization patterns
- Correlation with socioeconomic factors

### Advanced Visualizations
- Heatmaps of crime by hour and day of week
- Geographic maps with crime density
- Time series forecasting
- Network analysis of crime patterns
- Interactive dashboards with filters

### Statistical Tests
- Chi-square tests for independence
- Time series decomposition
- Clustering analysis for crime patterns
- Correlation analysis between variables

## Alternative Implementation

### More Efficient Night Filter
```python
# Convert hour to integer once
crimes['hour_int'] = crimes['hour'].astype(int)

# Boolean indexing
crimes['night'] = (crimes['hour_int'] >= 22) | (crimes['hour_int'] < 4)
```

### Vectorized Age Grouping
```python
# Using cut is already efficient, but you can add labels inline
crimes['age_group'] = pd.cut(
    crimes['Vict Age'],
    bins=[0, 17, 25, 34, 44, 54, 64, 100],
    labels=["0-17", "18-25", "26-34", "35-44", "45-54", "55-64", "65+"]
)
```

## File Structure

```
project/
│
├── la_crime_analysis_matplotlib.py    # Main analysis script
├── README.md                          # This file
└── la_crime_data.csv                  # Your dataset (not included)
```

## Data Sources

LA crime data can be obtained from:
- LA City Data Portal: https://data.lacity.org/
- LA Police Department Open Data
- Kaggle datasets

## Data Privacy & Ethics

**Important Considerations**:
- This analysis uses aggregate data for public safety insights
- Individual victim information should remain confidential
- Findings should inform policy, not stigmatize communities
- Consider socioeconomic context when interpreting results

## Contributing

Contributions welcome! Areas for enhancement:
- Additional crime type analysis
- Machine learning predictions
- Real-time data integration
- Interactive web dashboard
- Mobile alert system

## License

This project is open source and available under the MIT License.

## Author

Los Angeles Crime Analysis Project

---

*A data-driven approach to understanding and preventing crime in Los Angeles through temporal, geographic, and demographic analysis.*

## Acknowledgments

Data courtesy of the Los Angeles Police Department and LA City Open Data Portal. This analysis is for educational and public safety purposes.

## Disclaimer

This analysis is based on reported crime data and may not reflect unreported crimes. Crime patterns can change over time. Always consult official law enforcement sources for current safety information.
