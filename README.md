
# Insights from a Real Airbnb Dataset - Cape Town 🏘️

This project focuses on insights derived from the **listings dataset** for Airbnb properties in **Cape Town**. The analysis includes pricing, popular neighborhoods, and geographical trends.


# Select the data of Cape Town

![image](https://github.com/user-attachments/assets/b609a689-1451-412b-96de-a97252f3750b)

---
## Python Code for Analysis
```python
import pandas as pd
calendar = pd.read_csv('calendar.csv.gz')
```
---
## Questions that you might want to address about the given data 
---
Let`s dive into exciting insights!

## 1 Want to know the number of available and unavailable rooms
---
```python
calendar.available.value_counts()
```
![image](https://github.com/user-attachments/assets/f1a556e2-b0f4-4cd4-990f-5a101725f4fa)

## 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
---
Explanation: value_counts(normalize=True) gives proportions. Multiplying by 100 converts the proportions into percentages
```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
![image](https://github.com/user-attachments/assets/842fe77f-2add-4729-ada4-2c8d9af6be8b)

## 3 Let`s Count the busiest day! 🚩
---
Hint: We will be counting the most unavailable days (given by f)
```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
![image](https://github.com/user-attachments/assets/34d520cc-8bb9-43a3-a7ee-6cb024d094d9)

## 4 Plot a bar graph to show availability percentage
---
```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
![image](https://github.com/user-attachments/assets/f3a57056-07b8-4934-b4ec-ae2093305a4e)

## 5 Plot the busiest day
---
```python
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
![image](https://github.com/user-attachments/assets/dcc1e4b1-094d-4f09-9540-545d50563d81)

## 📄 Download listings dataset of Hawaii from
[listings.csv](https://github.com/user-attachments/files/18569483/listings.csv)
```python
import pandas as pd
listings = pd.read_csv('/content/listings (1).csv')
```

```python
listings.columns
```
## ✅ Room type and price is given seperately
---
Let`s Combine and visualize them
```python
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
![image](https://github.com/user-attachments/assets/94fe7cce-a000-49df-b118-104e4f4808af)

## ✅ Which are the top 10 neighborhoods with the most listings?
---
Let`s Combine and visualize them
```python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
![image](https://github.com/user-attachments/assets/84da4979-5a4d-410b-b7a2-869cb5aa5f0a)

## ✅ Geographical Distribution of Listings (Price Colored)
---
Let`s Combine and visualize them
```python
import matplotlib.pyplot as plt
import seaborn as sns
```
```python
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
![image](https://github.com/user-attachments/assets/aafbe25b-550f-483f-be40-6d9c3c880615)

## Let us see the listings on a real map
* Hotter Areas (Red/Yellow): High Density: The areas that appear in red or yellow (the "hot" colors) indicate higher density or concentration of listings. This means there are more listings in these areas. Popular Locations: These regions might be more popular or in high demand. It could be near tourist attractions, popular neighborhoods, or central areas in Hawaii where people tend to stay more often. Colder Areas (Green/Blue):

* Low Density: Areas with blue or green (the "cold" colors) indicate a lower concentration of listings. These regions have fewer listings available. Less Popular Locations: These areas might be less popular or further from key attractions. If you're looking at pricing or other factors, lower density could imply less competition in these regions, which might indicate more affordable areas or less tourist traffic. Density Patterns:

* Clustered Areas: If you notice clusters of heatmap intensity, they represent hotspots. These might correspond to high-traffic areas like resorts, beaches, or urban centers. Spread-Out Listings: If the heatmap shows a more uniform distribution, it could suggest that listings are more evenly spread across the region, which may reflect a more balanced demand for rentals across different areas of Hawaii.
import folium
from folium.plugins import HeatMap
import pandas as pd


hawaii_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Hawaii
m = folium.Map(location=[20.7967, -156.3319], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in hawaii_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('Cape_Town_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
![image](https://github.com/user-attachments/assets/38eaf543-8682-4f0f-8d20-1f055f209559)

