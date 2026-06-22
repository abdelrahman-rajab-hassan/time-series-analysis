# Chicago Crime Time Series Analysis
 
A time series analysis of crime data from the city of Chicago, exploring patterns across **police districts, years, and months**. The project uses the publicly available *Crimes 2001 to Present* dataset from the Chicago Data Portal.
 
## Overview
 
This project answers a set of stakeholder questions about Chicago crime by preparing the data with a datetime index and using resampling, grouping, and normalization to surface trends and outliers.
 
## Dataset
 
- **Source:** [Chicago Data Portal — Crimes 2001 to Present](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2)
- **Format:** Split into one CSV per year (`Data/Chicago-Crime_YYYY.csv`) to stay repo-friendly.
- **Key columns:** `Date`, `Primary Type`, `District`, `Arrest`, `Domestic`, `Latitude`, `Longitude`.
## Tools
 
`pandas` · `numpy` · `matplotlib` · `seaborn`
 
## Analysis & Findings
 
### Topic 1 — Comparing Police Districts (2022)
- **Most crime:** District 8.0, with over 15,000 cases.
- **Least crime:** District 31.0, far below all other districts.
### Topic 2 — Crimes Across the Years
- **Overall trend:** Total crime **declined steadily**, from nearly 490,000 in 2001 to around 240,000 in 2022 (~50% drop). It plateaued around 2015–2018, fell sharply in 2020 (likely COVID-related), then rebounded slightly in 2022.
- **Counter-trend crimes (rose while overall fell):** Concealed Carry License Violation, Criminal Sexual Assault, Deceptive Practice, Homicide, Interference with Public Officer, Obscenity, Stalking, and Weapons Violation.
  > *Note:* Some categories started after 2001, so their large multiples partly reflect small early counts rather than pure growth.
### Topic 4 — Comparing Months
- **Most crime:** July and August (summer), ~710,000+ each.
- **Least crime:** February and December (winter), ~530,000.
- **Outliers (peak outside summer):**
  - **Fall (Oct):** Motor Vehicle Theft, Robbery, Intimidation, Obscenity
  - **Spring (May):** Assault, Kidnapping, Weapons Violation
  - **Winter (Jan):** Deceptive Practice, Prostitution, Offense Involving Children
## How to Run
 
1. Clone the repository.
2. Place the yearly CSV files in the `Data/` folder.
3. Open and run `chicago-crime-timeseries-analysis.ipynb`.
```bash
pip install pandas numpy matplotlib seaborn
```
 
