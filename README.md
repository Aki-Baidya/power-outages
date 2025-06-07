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
| `’NERC.REGION’` | The North American Electric Reliability Corporation (NERC) regions involved in the outage event |
| `’CLIMATE.REGION’` | U.S. Climate regions specified by National Centers for Environmental Information |
| `'OUTAGE.START.DATE'` | Date of year when the outage started |
| `’OUTAGE.START.TIME’` | Time of day when the outage started |
| `’OUTAGE.RESTORATION.DATE’` | Date of year when power was restored
| `’OUTAGE.RESTORATION.TIME’` | Time of day when power was restored |
| `’CAUSE.CATEGORY’` | Cause of the power outage |
| `’CAUSE.CATEGORY.DETAIL’` | Extra details about the cause if applicable |
| `’OUTAGE.DURATION’` | Duration of the power outage in minutes |
| `’RES.PERCEN’` | Percentage of residential electricity consumption compared to the total electricity consumption in the state (in %) |
| `’COM.PERCEN’` | Percentage of commercial electricity consumption compared to the total electricity consumption in the state (in %) |
| `’IND.PERCEN’` | Percentage of industrial electricity consumption compared to the total electricity consumption in the state (in %) |
| `’PC.REALGSP.REL’` | Relative per capita real GSP as compared to the total per capita real GDP of the U.S. (fraction) |
| `’POPPCT.URBAN’` | Percentage of the total population of the U.S. state represented by the urban population (in %) |


---


## Data Cleaning and Exploratory Data Analysis


### Data Cleaning


1. We only keep the columns we are interested in (the ones listed above).
2. Since an `'OUTAGE.DURATION'` of zero means nothing, we replace all zeroes with `NaN` values.
3. We then filter out the rows that are not null for `'OUTAGE.DURATION'`.
4. We combine `‘OUTAGE.START.DATE’` and `‘OUTAGE.START.TIME’` to one column as a pd.Timestamp and do the same `‘OUTAGE.RESTORATION.DATE’` and `‘OUTAGE.RESTORATION.TIME’`. We would most likely mostly work with the .time, but would want to keep .date for power outages than span more than a day.
5. Finally, we mean imputed `'RES.PERCEN'`, `'COM.PERCEN'`, and `'IND.PERCEN'`.
These are the first few rows of our cleaned DataFrame:


|  | U.S._STATE | NERC.REGION | CLIMATE.REGION   | CAUSE.CATEGORY     | OUTAGE.DURATION | RES.PERCEN | COM.PERCEN | IND.PERCEN | PC.REALGSP.REL | POPPCT_URBAN | OUTAGE.START           | OUTAGE.RESTORATION     |
|---|------------|-------------|------------------|--------------------|----------------:|-----------:|-----------:|-----------:|----------------:|-------------:|------------------------|------------------------|
| **1** | Minnesota  | MRO         | East North Central | severe weather     | 3060.0          | 35.55      | 32.23      | 32.20      | 1.08           | 73.27         | 2011-07-01 17:00:00    | 2011-07-03 20:00:00    |
| **2** | Minnesota  | MRO         | East North Central | intentional attack |    1.0          | 30.03      | 34.21      | 35.73      | 1.09           | 73.27         | 2014-05-11 18:38:00    | 2014-05-11 18:39:00    |
| **3** | Minnesota  | MRO         | East North Central | severe weather     | 3000.0          | 28.10      | 34.50      | 37.37      | 1.07           | 73.27         | 2010-10-26 20:00:00    | 2010-10-28 22:00:00    |
| **4** | Minnesota  | MRO         | East North Central | severe weather     | 2550.0          | 31.99      | 33.54      | 34.44      | 1.07           | 73.27         | 2012-06-19 04:30:00    | 2012-06-20 23:00:00    |
| **5** | Minnesota  | MRO         | East North Central | severe weather     | 1740.0          | 33.98      | 36.21      | 29.78      | 1.09           | 73.27         | 2015-07-18 02:00:00    | 2015-07-19 07:00:00    |



### Univariate Analysis

First, we wanted to see the most common causes of power outages. Using a pie chart, we were able to see the relative frequencies of each `'CAUSE.CATEGORY'`. 'severe weather' is the most common one by far, accounting for more than half of the power outages. 'fuel supply emergency' is the least common one, accounting for barely 3% of power outages.

<iframe
  src="assets/pie-chart.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Next, we looked at the number of power outages in each state. California has the most number of power outages by far with a whopping count of 197, followed by Texas then Michigan.

<iframe
  src="assets/num_outages.html"
  width="1200"
  height="600"
  frameborder="0"
></iframe>



### Bivariate Analysis

Since our project is centered around predicting the duration of a power outage, we next looked at the mean `'OUTAGE.DURATION'` of all 9 `'CLIMATE.REGION'`s.

<iframe
    src="assets/avg_dur_fig.html"
    width="800"
    height="600"
    frameborder="0"
></iframe>

We then looked at the number of power outages by `'CLIMATE.REGION'`. While 'West North Central' has the minimum count and outage duration, other climate regions (other than ) have different orders in the two analyses.

<iframe
  src="assets/outages_per_region_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Interesting Aggregates

We wanted to see whether the time at which a power outage occurs has any correlation with the climate region and the cause. We noticed power outages because of 'fuel supply emergency' started earlier in the day, while power outages due to 'islanding' started later in the day. Across climate regions, the times look about the same, although 'Northeast' seems to have the latest `'OUTAGE.START'` times.

| CAUSE.CATEGORY               | Central        | East North Central   | Northeast         | Northwest         | South             | Southeast         | Southwest         | West              | West North Central |
|-----------------------------|----------------|-----------------------|-------------------|-------------------|-------------------|-------------------|-------------------|-------------------|---------------------|
| equipment failure           | 13:00:48       | 08:35:00              | 11:15:45          | 16:47:00          | 10:46:00          | 16:50:15          | 15:39:36          | 12:00:20          | 09:46:00            |
| fuel supply emergency       | 08:36:15       | 07:50:15              | 12:04:08         | 01:48:00          | 09:52:30          | NaN               | 09:14:00          | 13:17:18          | NaN                 |
| intentional attack          | 11:23:35       | 12:19:22              | 10:26:53           | 12:21:12          | 10:55:33         | 12:05:40          | 11:15:06          | 10:32:22          | 12:51:00            |
| islanding                   | 18:19:00       | 12:01:00              | 22:44:00          | 16:03:20          | 18:13:30          | NaN               | 09:22:00          | 12:26:42         | 14:50:12            |
| public appeal               | 14:00:00       | 14:07:00              | 13:00:00          | 14:02:00          | 13:36:15            | 15:00:00          | 10:00:00          | 14:08:06      | 08:10:30            |
| severe weather              | 13:11:27       | 13:32:09               | 13:30:53          | 09:33:52         | 12:26:10           | 13:36:49          | 09:15:06          | 11:46:49      | 17:20:00            |
| system operability disruption| 15:16:30       | 11:54:20              | 15:21:38           | 15:28:00          | 13:27:18         | 12:11:44          | 14:02:45          | 12:54:09        | NaN                 |


---



## Assessment of Missingness

### NMAR Analysis

In our cleaned dataset, the only column with missing values is `'CLIMATE.REGION'`. Since the only rows for which values are missing are for `'U.S._STATE' == Hawaii`, this missingness depends on the `'U.S._STATE'` column, making it MAR. Before imputing missing values in `'RES.PERCEN'`, `'COM.PERCEN'`, and `'IND.PERCEN'`, the missing values did not seem to depend on themselves, and hence we cannot be sure if the missingness mechanism is NMAR.

### Missingness Dependency

We first checked for columns that missingness of `'CLIMATE.REGION'` does not depend on. We test `'PC.REALGSP.REL'`. We can say the null is there is no relation, and the alternate is that there is a relation. We used a permutation test, and used the absolute difference of means of `'CLIMATE.REGION'` for non-missing and missing values as the test-statistic. We agreed on a p-value of 0.05, since our dataset contains ~1500 rows and we are only using a 1000 repetitions. We got a p-value of 0.91, which is much more than the p-value and hence we can safely conclude that there is no relation between `'CLIMATE.REGION'` missingnessa nd `'PC.REALGSP.REL'`

<iframe
  src="assets/cli_mi.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


We then checked for a column that the missingness of `'CLIMATE.REGION'` did depend on. Looking at our columns, the one that seemed the closest was `'NERC.REGION'`. We used the same null and alternate as above. Using a permutation test over 1000 repetitions, we got a p-value of 0.00, which is much lower than our agreed p-value of 0.05. Hence, we reject the null and conclude the possibility that there is a relation between missingness of `'CLIMATE.REGION'` and `'NERC.REGION'`.

<iframe
  src="assets/sim_chi.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

---




## Hypothesis Testing

**Null Hypothesis**: Outage Durations are equal in length regardless of whether the majority of electricity consumption in the state is residential or industrial

**Alternate Hypothesis**: Outage Durations are longer when the majority of electricity consumption in the state is residential, as compared to industrial

I define the majority to be more than 50%. Hence, we would be comparing `'OUTAGE.DURATION'` across rows with `'RES.PERCEN' > 50.0` and `'IND.PERCEN' > 50.0`.

Our text statistic would be subtracting the mean `'OUTAGE.DURATION'` of industrially dominated states from the mean `'OUTAGE.DURATION'` of residentially dominated states. This would be a permutation test.

Since we only have ~1500 rows, we chose a p-value of 0.05.

Doing a permutation test of a 1000 repetitions, we got a p-value of 0.025, which is lower than our agreed p-value. Hence, we reject the null.

<iframe
  src="assets/hypo_test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


---




## Framing a Prediction Problem

We want to predict the `'OUTAGE.DURATION'` using mainly `'U.S._STATE'`, `'CLIMATE.REGION'`, and `'CAUSE.CATEGORY'`. Since these all are categorical columns, we would want to use one-hot encoding for this problem. Since our prediction is a number, this would be a regression model. We chose to predict this variable so that people could know if their neighborhood or industrial buildings might need to brace for longer durations of no power. We can use the F-1 score to check our model.


---




## Baseline Model




---




## Final Model




---




## Fairness Analysis




---

