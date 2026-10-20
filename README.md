# How Severe Weather and Public Events Disrupt MBTA Green Line B Travel Times

**BA 780 – Team Project (Team A08)** · Boston University, Questrom School of Business

**Team members:** Susan Huang, Ingrid Felix, Ruining Shan, Tia Theseira, Kaiser Lu

## Overview
The MBTA Green Line B Branch runs through the BU campus. Between Boston College and Kenmore it runs above ground, sharing Commonwealth Avenue with car traffic, and from Kenmore to Government Center it runs underground. We measured how precipitation, temperature, and public events affect the line's travel time and reliability, and which parts of the line are hit hardest. To capture two very different seasonal profiles, we compared **September 2025** (start of the semester and fall events) with **December 2025** (cold weather and holiday crowds).

## Data
| Dataset | Source | Time range |
|---|---|---|
| MBTA Rapid Transit Travel Times 2025 | [MBTA Open Data Portal](https://mbta-massdot.opendata.arcgis.com/datasets/5f71a5c035fc4a4dad1b7fa73ba27ef8/about) | Sept & Dec 2025 |
| Local Climatological Data (LCD) v2, Boston Logan | [NOAA NCEI](https://www.ncei.noaa.gov/access/search/datasets/local-climatological-data-v2/) | Jan–Dec 2025 |
| Special Event License Applications | [Analyze Boston](https://data.boston.gov/dataset/special-event-license-applications/resource/fb05bfda-a57e-4d97-948b-4f1949ba3c8a) | Events in 2025 |

We filtered the MBTA data to the B Branch (1.77M trip records in September and 1.12M in December), aggregated it by date, hour, direction, and stop pair, and merged it with hourly weather and daily event counts. The final dataset has **539,798 rows**.

## Methods
- Cleaned and merged three datasets with different time granularity (hourly travel times and weather, daily events)
- Handled messy weather fields, such as trace precipitation recorded as "T", mixed data types, and missing values
- Built a baseline from end-to-end trips (Boston College ↔ Government Center) and from "normal" days with no rain and no events
- Answered 15 hypothesis-driven questions in four groups: baseline performance, weather, public events, and weather + events combined
- Compared above-ground and underground segments, peak and off-peak hours, and September and December
- Used descriptive statistics, correlations, and visualizations (line charts, box plots, histograms, scatter plots with trend lines) built with pandas, matplotlib, and seaborn

## Key Findings
1. **Above-ground segments drive unpredictability.** Even on normal days, travel-time variability above ground is roughly three times that of underground segments (average standard deviation of 192.9 s vs. 66.7 s).
2. **Rush hour is slower but more predictable.** Peak hours add about 1.5 minutes to the median end-to-end trip (47.8 vs. 46.3 min), but their spread is tighter (standard deviation of 5.6 vs. 6.6 min).
3. **September is slower than December.** On normal days, the median end-to-end trip was 47.8 minutes in September and 43.1 minutes in December, likely because of the back-to-school rush.
4. **Rain alone barely matters.** Median travel time on precipitation days was about the same as on dry days, and daily rainfall was only weakly correlated with travel time (r = 0.09).
5. **Events matter more than weather.** Extreme trips (at or above the 90th percentile) made up 11.2% of event-day records vs. 6.9% on non-event days, with the largest slowdowns at Government Center inbound (+39%). Days with both rain and an event were the slowest overall (47.8 vs. 46.1 min).

## Recommendations
- **MBTA:** Prioritize transit signal priority on Commonwealth Avenue, add capacity during the September move-in period, and combine weather forecasts with the city's event permits to plan for high-risk days.
- **Riders:** Leave extra buffer time during off-peak hours and in September.

## Limitations
Some comparison groups were small or uneven. For example, there were only 9 "normal" days, and the data had more event-day records than non-event-day records. Weather, time of day, and events also overlap, so these findings are associations, not causal effects.

## Repository Contents
| File | Description |
|------|-------------|
| `A08-Green-Line-B-Weather-and-Event-Disruptions.ipynb` | Final team project report: analysis code, charts, and written findings |
| `README.md` | Project overview (this file) |

## How to Run
1. Open the notebook in Jupyter Notebook or Google Colab.
2. The raw data was loaded from the team's Google Cloud Storage bucket (gs://teama08/...).
3. To re-run the analysis, download the three datasets from the links above and update the file paths in Section 3.1.
4. Run the cells from top to bottom.
