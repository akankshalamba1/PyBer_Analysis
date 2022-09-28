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
> total_rides = pyber_data_df.groupby(["type"]).count()["ride_id"]
> total_drivers = city_data_df.groupby(["type"]).sum()["driver_count"]

- **Calculating average fare per city type**
> average_fare_per_ride = total_fare / total_rides

- **Calculated average fare per driver**
> average_fare_per_driver = total_fare / total_drivers

- **Data summary**
> pyber_summary_df = pd.DataFrame({
                                "Total Rides" : total_rides,
                                "Total Drivers" : total_drivers,
                                "Total Fare" : total_fare,
                                "Average Fare per Ride" : average_fare_per_ride,
                                "Average Fare per Driver" : average_fare_per_driver
                                })

- **Summary Formatting**
> pyber_summary_df["Total Rides"] = pyber_summary_df["Total Rides"].map("{:,.0f}".format)

pyber_summary_df["Total Drivers"] = pyber_summary_df["Total Drivers"].map("{:,.0f}".format)

pyber_summary_df["Total Fare"] = pyber_summary_df["Total Fare"].map("${:,.2f}".format)

pyber_summary_df["Average Fare per Ride"] = pyber_summary_df["Average Fare per Ride"].map("${:,.2f}".format)

pyber_summary_df["Average Fare per Driver"] = pyber_summary_df["Average Fare per Driver"].map("${:,.2f}".format)
## Results

## Summary
