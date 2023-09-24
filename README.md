# Coding-Samurai
Task 1: Exploratory Data Analysis on Airbnb data  

What did we learn from this project?

a). We found that Entre home/apt has the highest number of room types overall and prices are high in Brooklyn and Manhattan for the entire home/apt.

b). From visualization most people love to stay in the entire home/apt and in a private room rather than a shared room.

c). Most of people like to stay at a lower price and their reviews are higher in that area.

d). We have found the busiest host.

e). They are busy because they listed their room type as entire home/apt and private room which is preferred by most people.

f). We found the traffic area based on the minimum nights booked.

g). At last we found a correlation between the variables.

import pandas as pt
import numpy as np
import matplotlib. pyplot as plt  
import seaborn as sb         
%matplotlib inline  

Data = pt.read_csv("AB_NYC_2019.csv")

Data

Data.isnull()
Data.isnull().sum()

Data.drop(['latitude','longitude','last_review','calculated_host_listings_count'],axis=1)

Data.describe()

Aera_wise_room_price = data.groupby(['neighbourhood_group','room_type'])['price'].max().reset_index()
Aera_wise_room_price 

Aera_wise_room_price.sort_values(by='price',ascending=False).head(10)

area_reviews = Data.groupby(['neighbourhood_group'])['number_of_reviews'].max().reset_index()
area_reviews

area = area_reviews['neighbourhood_group']
review = area_reviews['number_of_reviews']
picture = plt.figure(figsize =(8,6))

plt.bar(area ,review , color = 'black', width = 0.5 )
plt.xlabel('Area')
plt.ylabel('Review')
plt.title('Number of review in term of area')

plt.show()

traffic_area = Data.groupby(['neighbourhood_group','room_type'])['minimum_nights'].count().reset_index()
traffic_area

area_traffic = traffic_area['room_type']
room_stayed = traffic_area['minimum_nights']

fig = plt.figure(figsize = (4,6))

plt.bar(area_traffic,room_stayed , color ='black')
plt.xlabel('room type')
plt.ylabel('minimum nights')
plt.title('traffic area based on night booked')
plt.show()

corr = Data.corr(method = 'kendall')
fig = plt.figure(figsize =(8,6))
sb.heatmap(corr,annot = True)
Data.columns
