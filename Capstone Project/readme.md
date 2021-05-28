# Google Analytics Capstone - Case 1 Bike Share

This is my analysis of the provided Bike Share case.
Full case study and procedure is documented on Kaggle [here](https://kaggle.com/purpleultralisk/google-data-analytics-case-1-bike-share)
Data set can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html)

**Goal**
The objective of the study was to identify user trends in user behavior and use this knowledge to help convert casual riders to members.

**Key Observations**
There were some key trends observed from the January 2020 to April 2021 data:

1. Casual riders ride for 20 minutes longer than annual members on average
2. Casual riders ride further than members on average
3. Casual riders ride most often on Sundays and Mondays, while annual members are evenly distributed

**Recommendation**
To incentivize riders to convert to members we can look to:

1. Increase prices on loans with longer duration for casual members
2. Increase prices on loans for Sundays

**Learning**
This case provided a hands-on excercise to convert raw data into actionable insights.
A number of R packages was used:

-   `tidyverse` for general data cleaning
-   `geosphere` for calculating distance between 2 coordinates
-   `ggplot2` for data visualization
