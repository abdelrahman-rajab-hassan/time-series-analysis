
# Chicago Crime Analysis Dashboard (2020–2022)

An interactive Tableau dashboard exploring reported crime in Chicago from 2020 to 2022. The data was unioned from the yearly Chicago crime datasets and filtered to a clean three-year window for performance.

**Author:** Abdelrahman Rajab Hassan
**Tool:** Tableau Public

---

## Overview

The project consists of two connected dashboards:

- **Main dashboard** — crime volume by type, a geographic crime map, and arrest outcomes, all linked by an interactive action filter.
- **Secondary dashboard** — a monthly crime trend over the full three-year period.

Clicking a crime type on the main dashboard filters the map and arrest chart. The trend view is intentionally left unaffected so it always shows the complete picture.

---

## Dashboards

### Main Dashboard

Crimes by type, a homicide location map, and arrest rate — with a navigation button to the trend view.

<img width="1362" height="747" alt="main-dashboard" src="https://github.com/user-attachments/assets/cc6408db-85c5-48bc-b837-2f74db7572d3" />


### Crime Trend (Secondary Dashboard)

Monthly reported crime from December 2019 to December 2022. The two sharp dips align with COVID-19 lockdown periods, followed by a steady climb through 2022.

<img width="1427" height="765" alt="crime-trend" src="https://github.com/user-attachments/assets/e5afb060-aef6-48fb-a872-7b43dfd98acd" />


### Crimes by Type

Theft, battery, and criminal damage are the three most common categories by a wide margin.

<img width="1418" height="766" alt="crimes-by-type" src="https://github.com/user-attachments/assets/6fb2d26d-3336-43c1-9d8d-c01ca0e39cd6" />


---

## Features

- Union of the 2020–2022 Chicago crime data
- At least three visualizations on the main dashboard plus a trend view
- Navigation buttons linking the two dashboards
- A custom (non-default) color palette and coordinated styling
- An action filter that links the type chart to the map and arrest views, while excluding the trend chart

---

## Data

Source: Chicago crime records (yearly files, 2000–2022), unioned and filtered to 2020–2022 for this analysis.

Key fields used: `Date`, `Primary Type`, `Arrest`, `Domestic`, `District`, `Latitude`, `Longitude`.
