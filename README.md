# PyBer_Analysis
Analysis of PyBer, a ride-sharing app company valued at $2.3 billion. We were assigned a big project, to analyze all the rideshare data from January to early May of 2019 and create a compelling visualization for the CEO, V. Isualize. After the successful completion of that project we are assigned another project with Omar. To create a multiple-line graph that shows the total weekly fares for each city type.


## Overview of the analysis
**Resources used**

For this project two CSV files were used that had ride data and city data. 
- **Ride Data file:** The ride data CSV file includes 2376 rows and 4 columns, namely:- City, Date, Fare, ride_id. The first 10 rows of this csv file is as follows:

![ride_data_df](https://user-images.githubusercontent.com/111251560/192709610-b64fcdb0-2e8d-48c7-8b69-d0d988ee2821.png)

[ride_data](/Resources/ride_data.csv)

- **City Data file:** The city data CSV file inclused 121 rows and 3 columns, namely:- City, Driver_count and type. the first 10 rows of this csv file is as follows:

![city_data_df](https://user-images.githubusercontent.com/111251560/192710289-c5414575-76cc-4ce3-bde8-4eedc1207ae6.png)

[city_data](/Resources/city_data.csv)

**Technology used** 
Python scripts using Pandas libraries, the Jupyter Notebook, and Matplotlib to create a variety of charts that showcase the relationship between the type of city and the number of drivers and riders, as well as the percentage of total fares, riders, and drivers by type of city.

**Coding language used** 
Python was the main coding language, we used SciPy, a statistical Python package, and NumPy, a fundamental package for scientific computing in Python functions.

### Steps involved in the Analysis:
For this analysis we are using two csv files, so we used following steps to make the computing logical and systematic:
- **Merge both csv file data** As the data is devided in two csv files first thing we did to make analysis easy is combine both the file data into one data frame called "pyber_data_df" by using "city" as the index. To combine the data we used following code:
> pyber_data_df = pd.merge(ride_data_df, city_data_df, how="left", on=["city", "city"])

**Output**

![merge_data](https://user-images.githubusercontent.com/111251560/192822373-a7be02a2-0a2f-46f4-945f-84e735c794ff.png)

- **Calculating total ride and total drivers**

Following is the code used to find the total rides in each city type

> total_rides = pyber_data_df.groupby(["type"]).count()["ride_id"]

Following code is used to find the total number of drivers in each city type

> total_drivers = city_data_df.groupby(["type"]).sum()["driver_count"]

- **Calculating average fare per city type**

The average fare per ride is calculated by dividing Total fare by Total rides. The code is attached as follows:

> average_fare_per_ride = total_fare / total_rides

- **Calculated average fare per driver**

The average fare per driver is calculated by dividing Total fare by Total Drivers. The code is attached as follows:

> average_fare_per_driver = total_fare / total_drivers

- **Data summary**

To summarize that data and to make the conclusion easier we created a dataframe with Total rides, total drivers, total fare and average fare per ride and average fare per driver. We used following code to do so:

> pyber_summary_df = pd.DataFrame({
>                                "Total Rides" : total_rides,
>                                "Total Drivers" : total_drivers,
>                                "Total Fare" : total_fare,
>                                "Average Fare per Ride" : average_fare_per_ride,
>                                "Average Fare per Driver" : average_fare_per_driver
>                                })

- **Summary Formatting**

To make the data more presentable we made some chages to the output by formating it using the following formula:

> pyber_summary_df["Total Rides"] = pyber_summary_df["Total Rides"].map("{:,.0f}".format)

> pyber_summary_df["Total Drivers"] = pyber_summary_df["Total Drivers"].map("{:,.0f}".format)

> pyber_summary_df["Total Fare"] = pyber_summary_df["Total Fare"].map("${:,.2f}".format)

> pyber_summary_df["Average Fare per Ride"] = pyber_summary_df["Average Fare per Ride"].map("${:,.2f}".format)

> pyber_summary_df["Average Fare per Driver"] = pyber_summary_df["Average Fare per Driver"].map("${:,.2f}".format)


## Results
The analysis results are depicted in the jupyter notebook attached below:

[PyBer_Challenge](/PyBer_Challenge.ipynb)

![summary_output](https://user-images.githubusercontent.com/111251560/192925316-73a6e9b6-5004-49cd-9f7e-ab20021d584e.png)

- Total number of rides are most in Urban area with (1625 rides per week).
- Highest number of drivers are available in urban area as compared to rural and subrural area with 2405, 78 and 490 drivers respectively.
- By reviewing the average fare per ride, it could be conclued that the rides in rural area are more profitable as compared to suburban and urban area with $34.62, $30.97 and 24.53 average fare respectively.
- The data of Average Fare per Driver also depict quite the same story, in rural area the average fare per driver is more that 3 times the average fare in urban area.
- The results refect the tolal fare in urban area is more that 9 times the fare in rural area and twice the fare in suburban area. 
- To make the data understandable and to provide visual presentation to the analysis we converted the data frame by resampling and converting the date into a datetime data type the new data frame appeared as the following:

![timedate](https://user-images.githubusercontent.com/111251560/192934770-c9eaae18-e9c2-4e05-97f3-c8a0eaa06d88.png)

![Test_image](/analysis/PyBer_fare_summary.png)

### Observations from line chart
- The Average weekly fare of rural area lies in $0 to $500 range
- Average weekly fare of suburban area lies in $500 to $1200 range
- Average weekly fare of suburban area lies in $1500 to $2500 range

## Summary

From the above analysis we could summarize that in Urban cities the number of drivers is way more that the demand that is the number of rides. So the fare generated from these rides is bare minimun. After this analysis we have come up with come recommendations for the PerBer ride share company that could help the company to be profitable and reach the demand and supply equilibrium. 

### Recommendations for PyBer:

- Systematic distribution of service in all the city types: We need to deep dive in the factors affecting ride choices in all three city types and provide special offers to drivers to shift from Urban area to rural and suburban area as  in Urban rae we are having excessive supply as compared to the demand for service where as in rural area its the opposite. 

- Provide special offers for customers in rural areas to adapt to ride share service: Based on the Analysis it is observed that in rural area the supply of drivers is very less as compare to urban areas as a result the Total fare generated in rural area is drastically ow as compared to urban and suburban areas. Detail market research is required to understand the mindset, choices and spending habits of customers in rural area. We also need to consider coupons and special incentives to customers in rural areas to motivate them to adopt PyBer ride sharing. As the Average Fare per ride is highest in rural areas.

- Review the company structure and hiring process: Based on the analysis it is highly recommended that we need to review the headcount of drivers. as we are having about 1.5 times the drivers as compared to the rides in the urban area which is a huge financial pressure at PyBer. We need to re-struct the headcounts, could consider moving around employees, evaluating there performance and recognizing the key performers.
