# power-outages
Final Project in DSC 80 at UC San Diego<br>
By: Aki Baidya and Dhruv Sehgal


---


## Introduction
We chose to analyze a dataset containing data about major power outages in the continental U.S. We acquired this dataset from the 'Laboratory for Advancing Sustainable Critical Infrastructure' at Purdue University. It records data from January 2000 to July 2016. The Department of Energy defines ‘major’ power outages to be those that affect at least 50,000 customers or cause an unplanned firm load loss of at least 300 MW. Other than just power outage information (such as outage start and end time, outage duration, and cause), it also contains other data such as geographic region, climate of the region, scale of the outage, land-use patterns, and economic characteristics of the region.


Our research question is, “What variables affect the duration of a power outage?” We wish to analyze this so that power companies and urban planning companies can better create infrastructure to prepare better for unexpected events. Since our dataset also contains data such as economic characteristics of a region and land-use patterns, this would also help us understand which populations are more likely to spend large periods of time without power, such as historically underserved and marginalized communities.


There are 1534 rows in our dataset with 55 columns (variables). We plan to focus mainly on these variables:
| Column | Description |
| --- | --- |
| `'U.S._STATE'` | State the outage occurred in |
| `’NERC.REGION’` | The North American Electric Reliability Corporation (NERC) regions involved
in the outage event |
| `’CLIMATE.REGION’` | U.S. Climate regions specified by National Centers for Environmental
Information |
| `'OUTAGE.START.DATE'` | Date of year when the outage started |
| `’OUTAGE.START.TIME’` | Time of day when the outage started |
| `’OUTAGE.RESTORATION.DATE’` | Date of year when power was restored
| `’OUTAGE.RESTORATION.TIME’` | Time of day when power was restored |
| `’CAUSE.CATEGORY’` | Cause of the power outage |
| `’CAUSE.CATEGORY.DETAIL’` | Extra details about the cause if applicable |
| `’OUTAGE.DURATION’` | Duration of the power outage in minutes |
| `’RES.PERCEN’` | Percentage of residential electricity consumption compared to the total
electricity consumption in the state (in %) |
| `’COM.PERCEN’` | Percentage of commercial electricity consumption compared to the total
electricity consumption in the state (in %) |
| `’IND.PERCEN’` | Percentage of industrial electricity consumption compared to the total
electricity consumption in the state (in %) |
| `’PC.REALGSP.REL’` | Relative per capita real GSP as compared to the total per capita real GDP of the U.S. (fraction) |
| `’POPPCT.URBAN’` | Percentage of the total population of the U.S. state represented by the urban
population (in %) |






---




## Data Cleaning and Exploratory Data Analysis




### Data Cleaning


1. We only keep the columns we are interested in (the ones listed above).
2. We convert ‘OUTAGE.START.DATE’ and ‘OUTAGE.RESTORATION.DATE’ to a format that we can convert to a date.
3. We combine ‘OUTAGE.START.DATE’ and ‘OUTAGE.START.TIME’ to a pd.Timestamp and do the same ‘OUTAGE.RESTORATION.DATE’ and ‘OUTAGE.RESTORATION.TIME’. We would most likely mostly work with the .time, but would want to keep .date for power outages than span more than a day.
3. 




### Univariate Analysis




### Bivariate Analysis




### Interesting Aggregates




---




## Assessment of Missingness




---




## Hypothesis Testing




---




## Framing a Prediction Problem




---




## Baseline Model




---




## Final Model




---




## Fairness Analysis




---

