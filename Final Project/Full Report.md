# Capsotne Project - The Battle of Neighborhoods: Travel Edition

### Table of Contents
1. Introduction/Business Problem
2. Data
3. Methodlogy
4. Results
5. Discussion
6. Conclusion

## 1. Introduction
### 1.1 Background
When traveling to a new city, a difficult problem to solve is determining where to stay. Each city has many, many neighborhoods and making a bad pick can make or break your trip. Because of this, more often than not you need to spend a significant amount of time researching each city for activities, restaurants, entertainment, points of interest, and various other criteria in order to make a determination, which is ultimately a gamble.

In order to keep the scope managable, we will begin by only using this script for select available cities..

### 1.2 Problem
Data that typically contirubtes to how well a neighborhood is received by a traveler is the neighborhoods' similarity. This project aims to use features about each neighborhood to provide the optimial neighborhood for a user to travel to.

### 1.3 Interest
Any travel or transportation business would be interested in providing this sort of insight to their customers in order to be able to provide their customers with a more tailored experience. This can also be used in order to better target partnerships for the business providing the service and those providing other services.

## 2. Data
### 2.1 Data Sources
In order to be able to run this analysis, we will need to be able to have two sets of data:
1. Neighborhoods in a city
2. Venues in a city

A list of neighborhoods that exist will come from scraping the [Airbnb Website](https://www.airbnb.com/locations) that ouline which neighborhoods exist in every city. With this, we will then use [GeoPy](https://geopy.readthedocs.io/en/stable/) in order to compliment the neighborhood names with the latitude and longitiude values.

The commercial venues data  will be sourced from the Foursquare api. This will be used in order to find which venues exist in the neighborhoods that our user have liked as well as to assess which neighborhoods would be great reccomendations for the user. So I will use the explore endpoint to get the venues nearby both the user input neighborhoods as well as to explore all the neighborhoods in the cities they will visit.

Some of the most important venues to look at will be:
- Restaurants
- Landmarks and venues
- Nightlife
- Activites

Joining this data with the tastes of our user, the goal is to be able to find similar neighborhoods that our user may prefer to stay in.

### 2.2 Data Preparation
Neighborhood data was downloaded using the [Airbnb Website](https://www.airbnb.com/locations) as an HTML file and then was scraped in order to retreive each city and each neighborhood in the city. Then geopy was used to obtain the latitude and longitude of each of these neighborhoods. Gaps were found mostly for invalid entries for geopy and these gaps were ignored. Once enhanced, the neighborhood data was turned into a dataframe.

We then ask the user to input their liked neighborhood and their travel city. Once input, we use Foursquare's api to download the venue information for the liked neighborhood and each of the neighborhoods in the target city.

## 3. Methodology
### 3.1 
