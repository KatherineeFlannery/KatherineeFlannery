# Cyclistic Bikes

## Business Question
How do casual riders and annual members use Cyclistic bikes differently, and how can these differences be leveraged to convert casual riders into annual members?

## Data Sources Used
For this case study, I used data from [Cyclistic’s historical data] (https://divvy-tripdata.s3.amazonaws.com/index.html) for the previous 12 months from May 2021 - April 2022 . The data is a public data set from Motivate International Inc. and was used under this [license.](https://divvybikes.com/data-license-agreement) The data is organized in excel spreadsheets by month. 

## Column Titles
ride_id
rideable_type
started_at
ended_at
start_station_name
start_station_id
end_station_name
end_station_id 
start_lat
start_lng
end_lat
end_lng
member_casual

The data does not have information about the customers to determine how much an individual uses the service nor any billing or credit card information to determine if customers live in the area. This will also mean that we cannot determine how many times a specific customer is using the service or if casual users convert to members. 

## Data Preparation
Combined monthly datasets into a single table using SQL
Validated data integrity (missing values, duplicates, category consistency)
Standardized bike type labels for consistency
Filtered out implausible ride durations (<60 seconds, >24 hours)
Engineered new features including ride length and day of week

## Key Findings
Classic bikes are favored by both members and casual users, making up 60% of rides in each group.
Ride Duration:  Casual users average double the ride length of members with casual users averaging 26 minute rides and members averaging 13 minute rides.
Usage Timing: Members ride more frequently on weekdays, consistent with commuting patterns; casual riders peak on weekends
Seasonality: Usage increases in summer months for both groups, with casual riders surpassing members during peak tourist season
Location Patterns: The most popular stations for casual users were concentrated near tourist attractions such as the beach, children’s museum, millennium park, theater and aquarium. Member stations were further from the coast and near more offices, likely being used to commute for work.
Bike Preference: Classic bikes account for approximately 60% of rides for both user types

## Recommendations
- Introduce pricing incentives that make annual memberships more cost-effective for frequent, long-duration casual riders
- Offer tiered memberships tailored to tourists versus local riders
- Target high-traffic tourist stations with membership promotions and limited-time incentives


