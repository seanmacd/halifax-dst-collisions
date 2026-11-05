# How the End of Daylight Saving Time Affects Evening Rush-Hour Collisions in Halifax (2018–2026)

**Author:** Sean MacDougall (A00482538)

---

## 1. Topic Overview

Every year on the first Sunday of November in Nova Scotia, daylight saving time (DST) ends, moving the clocks back one hour. This changes the sunset time from about 6:05 pm to 5:05 pm in Halifax, shifting the evening commute from daylight to darkness. There are debates across Canada regarding seasonal clock changes. If a darker commute measurably increases collisions, then that acts as evidence for ending clock changes.

## 2. Research Question

> Does the seasonal clock change in November, which moves the evening commute into darkness, increase the number of traffic collisions during the evening rush hour (5:00–6:30 pm) in the Halifax Regional Municipality?

## 3. Scope Definition

### Time Period

The collision dataset covers **December 31, 2017 to August 31, 2026**. The DST analysis uses the eight fall-back transitions this data covers:

- November 4, 2018
- November 3, 2019
- November 1, 2020
- November 7, 2021
- November 6, 2022
- November 5, 2023
- November 3, 2024
- November 2, 2025

The analysis compares the **four weeks before** each transition and the **four weeks after**.

### Geographic Boundaries

The collision dataset covers all collisions recorded within the road right-of-way in the Halifax Regional Municipality, as reported by Halifax Regional Police.

### Time-of-Day Boundaries

- **Evening rush hour** *(focus time window)*: **5:00–6:30 pm**, the time period that turns to darkness when the clocks change.
- **Midday** *(control window)*: **11:00 am–2:00 pm**. Light levels do not change with clock changes, so this window is used as a control for weather and seasonal conditions.
- **Morning rush hour** *(secondary focus time window)*: **7:00–8:30 am**, the time period that gets brighter when the clocks change.

## 4. Hypothesis

> In the four weeks after the November fall-back, the average number of daily collisions in HRM during the evening rush hour (5:00–6:30 pm) will be **significantly higher** than in the four weeks before. This increase will be **larger than any change in the midday window** (11:00 am–2:00 pm) over the same period.

A supporting prediction is that morning rush-hour collisions will stay the same or decrease, since those commutes become brighter.

## 5. Required Datasets

### Dataset: HRM Traffic Collisions

- **Source:** <https://data-hrm.hub.arcgis.com/datasets/HRM::traffic-collisions/about>
- **Formats:** CSV (primary), with GeoJSON, Shapefile, and the ArcGIS REST API available through the HRM Open Data Hub.
- **Relevance:** Each record is a police-reported collision, with its date, time, and conditions. The date places each collision before or after a DST transition, and the time places it in the evening rush-hour, midday, or morning rush-hour window. Counting collisions by day and time window gives the daily totals needed to compare the weeks before and after each clock change.

## 6. Proposed Analytics

### Visualizations

1. **Event-centred line chart:** Average daily collisions in each time window, plotted against days relative to the fall-back, averaged across all eight years.
2. **Before/after grouped bar chart:** Mean daily collisions before and after the DST transition for each time window.
3. **Hour-of-day heatmap:** Collisions by hour of day (rows) and week relative to the fall-back (columns), showing whether the increase after the clock change is concentrated in the evening hours.

### Statistical Analyses

1. **Descriptive statistics:** A summary of statistics of the dataset using pandas `.describe()` and frequency counts, including the mean, median, standard deviation, and range of daily collision counts in each time window.
2. **Difference-in-differences regression:** A Poisson regression of daily collision counts, with terms for before and after the transition, time window, and their interaction. The interaction term measures the DST effect that can't be explained by seasonal or weather changes affecting the whole day.
3. **Welch's t-test:** A comparison of mean daily evening rush-hour collisions in the four weeks before vs. the four weeks after the transition, testing whether the difference is statistically significant.

## 7. Anticipated Analytical Story

I expect a clear, immediate rise in evening rush-hour collisions after the clocks fall back, while midday collisions stay roughly the same and morning collisions remain the same or drop. This pattern would show that the loss of evening daylight drives the increase in collisions in November, separate from weather conditions.

I expect the 2020 transition to be an outlier, since pandemic restrictions reduced commuter traffic. The analysis will test whether the results hold with that year removed.

*A known limitation is that the collision data records crashes, not traffic volume. A rise in collisions could partly reflect changes in how many people are driving. Comparing time windows within the same days reduces this concern, but does not remove it.*
