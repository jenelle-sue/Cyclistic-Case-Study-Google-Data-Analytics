# Cyclistic-Case-Study-Google-Data-Analytics
Capstone project for Google Data Analytics Course

## Introduction
The Google Data Analytics course on Coursera culminates with a Capstone project designed to utilize the new skills obtained over the previous 7 courses.  I choose the Cyclistic bike-share analysis case study for my capstone project. Information regarding my data cleaning, analysis and proposed next steps is outlined below.

## Quick Links
Data Source: [Divvy_Trips](https://divvy-tripdata.s3.amazonaws.com/index.html)  
Data visualizations: [Tableau](https://public.tableau.com/shared/6SR2DHY7P?:display_count=n&:origin=viz_share_link)  
SQL Queries:  
	1. [Table Combination](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/table_combination)  
 	2. [Data Exploration](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/data_exploration)  
  	3. [Data Cleanup](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/data_cleanup)   
   	4. [Data Analysis](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/data_analysis)  
	


## Background
Cyclistic is a bike-share program located in Chicago that was launched in 2016. The company has grown to a fleet of more than 5,800 bicycles that are geotracked and locked into a network of over 600 docking stations across the city.  The bikes can be picked up at one station and returned to any other stations within the network.  The company has flexible pricing plans which appeals to broad consumer segments. Customers can choose from single ride passes, full-day passes or annual memberships. Casual riders are those customers who purchase single ride or full-day passes. Members are those customers purchasing annual passes. 

## Scenario
In this project I am working as a junior-data analyst on the marketing analyst team at Cyclistic.  Finance analysts with the company have concluded that annual members are more profitable and the director of marketing believes maximizing the number of annual members will be key to future growth. The overall goal for my group is to develop a new marketing strategy to convert casual riders into annual members. 

These three questions will guide the future marketing program:  
		1.  How do annual members and casual riders use Cyclistic bikes differently?  
		2.  Why would casual riders buy Cyclistic annual memberships?  
		3.  How can Cyclistic use digital media to influence casual riders to become members?  

I have been assigned the first question; _how do annual members and casual riders differ in their use of the Cyclistic bikes?_ In addition, I was asked to provide my top three recommendations to maximize the number of annual members.

## Data Sourcing and Preparation
The Cyclistic historical data was provided by Motivate Internation Inc. under this [license](https://divvybikes.com/data-license-agreement). This data was provided Google Analytics for the course and does not contain any rider's personal identifiable information.  I chose to work with the most recent full year of data: January 2024 through December 2024. 
The data for each month was available in a separate csv file and all twelve files were stored in a dedicated Google Cloud Storage bucket due to the large file size.

## Data Processing and Cleaning
I completed the data cleaning and processing in multiple steps.  The first step was to upload each month of data onto the SQL platform and explore the attributes to ensure the table setups were the same.  Each individual month dataset contained 13 columns that were identical for field names and types of data. I was able to combine all the monthly datasets into one annual file for 2024 using this [SQL code](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/table_combination) After combination of the monthly tables I  reviewed the annual dataset to verify that it retained the same 13 columns and the number of rows added up to the expected total of 5,860,568.

### Inital Observations
- There were numerous NULL entries for the following columns, **start_station_name, start_station_id, end_station_name, end_station_id, end_lng,** and **end_lat**
- There was a difference with the format of the **started_at** and **ended_at** columns. Some of the data contained extra significant figures for the milliseconds. 
 	For example: 2024-02-07 14:03:19 UTC or 2024-11-05 13:55:42.650000 UTC

### Data Exploration
All code used for this data exploration can be found [here](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/data_exploration)
- confirmed that the **member_casual** column only had two distinct entry types  
- counted the number of rides per member type to make sure the dataset had a reasonable amount of data to compare  
- confirmed there were only three distinct types of bikes available  
- confirmed the **ride_ids** were all 16 characters in length 
- checked that there were rides that lasted less than 1 minute or longer than 24 hours
- checked for duplicate ride ids -> identified 211 identical ride ids

### Data Cleanup
All code used for this data cleanup can be found [here](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/data_cleanup)    
- removed all rows with NULL values for the columns identified previously
- truncated all **started_at** and **ended_at column** values to remove the extra significant figures for the milliseconds  
- created a column for **month** (1 = January and 12 = December)  
- created a column for **day_of_week** (1 = Sunday and 7 =  Saturday)  
- created a column for **ride_length**  
- deleted rows where **ride_length** total time was less than 1 minute or greater than 24 hours  
- identified 121 duplicate ride_ids and deleted  

### Data Analysis
All code used for these calculations can be found [here](https://github.com/jenelle-sue/Cyclistic-Case-Study-Google-Data-Analytics/blob/main/data_analysis)
- average and max **ride_lengths**
- average and max **ride)lengths** by **member_casual**
- max number of rides by **day_of_week**
- max number of rides by **month**
- top 5 **start_station_name** for casual riders
- top 5 **start_station_names** for members
  
## Findings
I took the cleaned 2024 annual data set and uploaded it to [Tableau](https://public.tableau.com/shared/6SR2DHY7P?:display_count=n&:origin=viz_share_link) in order to create the data visualizations to provide a summary of how members and casual riders use the bikes differently 

Here are my top findings: 
Annual riders make up 64% of the rides while casual riders make up 36% of all rides
![image](https://github.com/jenelle-sue/images/blob/main/Membership%20Overview.png)

Annual riders take shorter rides, 12.6 minutes on average. Whereas casual riders rides are twice as long on average at 24.2 minutes. 
Both groups ride longer on the weekend, Saturday and Sunday, compared to weekdays.
![image](https://github.com/jenelle-sue/images/blob/main/Ride%20Time.png)

Casual members ride more on Saturday and Sunday whereas the annual riders have higher number of rides during the week, Monday through Friday. 
![image](https://github.com/jenelle-sue/images/blob/main/Rides%20by%20Day%20of%20Week.png)

All types of riders show increased activity in the summer/fall months (May - Oct)
![image](https://github.com/jenelle-sue/images/blob/main/Rides%20by%20Month-2.png)

Top 5 start locations for casual riders are near tourist attractions including various museums, Millenium station, and Navy Pier. Whereas the top 5 start locations for annual riders are near transportation hubs, train stations or larger apartment complexes.
![image](https://github.com/jenelle-sue/images/blob/main/Maps-2.png)


## Conclusion/Next Steps
Top three recommendations to convert casual riders to annual members.  
- Offer additional membership subscription periods such as 3 or 6 months. This would attract casual riders that ride more frequently during the nicer weather months. Focus advertisements near train stations and transportation hubs in the city to target commuters.
- Offer discounted ride prices to members on rides > 20 minutes which may result in more casual riders signing up for memberships if they frequently take longer rides.
- Target tourists for memberships by partnering with popular local attractions. Include package deals of rental membership with tickets for popular locations if possible. Focus advertisments near museums, Millenium station, and Navy Pier.
