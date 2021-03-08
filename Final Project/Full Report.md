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
### 3.1 Determination of the target variable
In order to create a recommendation, a similarity score was used. The inputs to this similarity score is an average of the neareest 100 venues from the geographical center of the neighborhood. The average was chosen to account for neighborhoods which don't have 100 venues within a 500 meter radius from the center.

In order to calculate the similarity score the euclidean distance was used. The euclidean distance was used because it prefers neighborhoods with similar relative frequencies and also was a good measure for neighborhoods with unique venues.

### 3.2 Process
In order to obtain this value, the nearest 100 venues for the input baseline neighborhood was used to determine the frequency of each type of present venue. With this, we then retreived the nearest 100 venues to each neighborhood in the target city. With this, we then iterated through each neighborhood in the target city and calculated the eucledian distance from the baseline. Using the eucledian distance, it was determined that the neighborhood with the smallest euclidean distance was the most similar neighborhood and was selected as the recommended city.

A common case wehn running this analysis was when the target nighborhood had unique entries that didn't exist in the baseline neighborhood or vice-versa. In this case, we removed any of the venues that did not exist within the baseline neighborhood. The rational for this removal was to ensure that venues unique to only the target neighborhoods would not factor negatively in the caluclation of the eucledian distance. This was the case because we are looking for neighborhoods most similar to the baseline neighborhood, regardless of wheither or not the target neighborhood had more unique neighborhoods.

![Screen Shot 2021-03-07 at 9 57 09 PM](https://user-images.githubusercontent.com/38566125/110269125-07a26200-7f91-11eb-82e0-fafa04e7427b.png)

(Figure 1: The similar neighborhoods between the Baseline and target neighborhoods.)

In the initial development, we used Downtown Brooklyn in New York City as the baseline in order to predict the most similar neighborhood in San Francisco. As a New York City resident, it was convenient to use a neighborhood that I am personally familiar with.

As a way to remain grounded throughout the analysis, we looked at the common venues across the target neighborhoods and the baseline neighborhood. In Figure 1 we can see the similar neighobrhoods that were used.

## 4. Results
In using this method, we found that the most similar neighborhood to Downtown Brooklyn was SoMa in San Francisco. Using the aforementioned method, we found that the euclidean distance between Downtown Brooklyn and SoMa is 0.105.

![Screen Shot 2021-03-07 at 9 44 38 PM](https://user-images.githubusercontent.com/38566125/110267756-70d4a600-7f8e-11eb-8c3d-45159d9e8fc7.png)

(Figure 2: The 5 most similar San Francisco Neighborhoods to Downtown Brooklyn.)

Figure 3 below shows the most common venues in the SoMa neighborhood.

![Screen Shot 2021-03-07 at 9 46 39 PM](https://user-images.githubusercontent.com/38566125/110268028-feb09100-7f8e-11eb-989c-42109b4cef92.png)

(Figure 3: The most common venues in SoMa, San Francisco.)

Comparing the results in Figure 2 to those in Figure 3, we can see that two of the venues show up at the same relative frequency.

![Screen Shot 2021-03-07 at 9 51 26 PM](https://user-images.githubusercontent.com/38566125/110268361-85656e00-7f8f-11eb-9a51-214ebb501f9c.png)

(Figure 4: The most common venues in Downtown Brooklyn, NYC.)

## 5. Discussion
While going through this, it was noted that the tyes of restaurants in the area had a significant input into the calculated similarity to each neighborhood. This greatly manifested iteself when looking into the similarity of neighborhoods in vastly different countries. For example, in Tokyo there were many restaurants that were uniqe to Japan as a nation. This caused for a significant amount of venues to be omitted between Downtown Brooklyn and Tokyo. Despite this, we see that many of the similar neighborhoods share a venue as their top most common neighborhood.

A consideration that may improve the accuracy of this analysis is to further group the venue categories. For example, there are many restaruant types and it may be adventageous to use more general restaruant types than the ones provided. For example, rather than using "Burger Joint", "Taco Stand", "Hotdog Cart", etc it may be better to label them all as "Quick Eats" or so. Additionally, it would be more accurate to include more venues than 100, in order to account for local variances in each neighborhood.

## 6. Conclusion
By using the eucledian distance between the relative frequency of venues in neighborhoods we can find a relevant method to find similar neighborhoods. Using this to find similar neighborhoods to Downtown Brooklyn, we found that the SoMa neighborhood in San Francisco is the most similar neighborhood in San Francisco. Despite this similarity, we found that regional differences have caused for omissions between the baseline and target neighborhoods. These may be able to be accounted for by using more general categories and taking more venues into consideration.

