# Capsotne Project - The Battle of Neighborhoods: Travel Edition

### Table of Contents
1. Introduction/Business Problem
2. Data
3. Methodlogy
4. Results
5. Discussion
6. Conclusion

## 1. Introduction
When traveling to a new city, a common problem is determining where to stay. Each city has many, many neighborhoods and making a bad pick can make or break your trip. Because of this, more often than not you need to spend a significant amount of time researching each city for activities, restaurants, entertainment, points of interest, and various other criteria in order to make a determination, which is ultimately a gamble.

With this project, I aim to provide a system that users can trust to make their neighborhood stay determination for them. Using the foursquare api and sample neighborhoods from users, I will be able to make accurate and tailored recommendations for which neighborhoods users can stay in.

## 2. Data
The data necessary for this project is going to be commercial venues which will be sourced from the Foursquare api. This will be used in order to find which commercial spaces exist in the neighborhoods that our user have liked as well as to assess which neighborhoods would be great reccomendations for the user. So I will use the explore endpoint to get the venues nearby both the user input neighborhoods as well as to explore all the neighborhoods in the cities they will visit.

Some of the most important venues to look at will be:
- Restaurants
- Landmarks and venues
- Nightlife
- Activites

Joining this data with the tastes of our user, the goal is to be able to find similar neighborhoods that our user may prefer to stay in.
