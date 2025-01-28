
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
![image](https://github.com/user-attachments/assets/2fe7881e-3141-4ae7-810a-78afd87c37dc)
## 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
---
Explanation: value_counts(normalize=True) gives proportions. Multiplying by 100 converts the proportions into percentages
```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
## 3 Let`s Count the busiest day! 🚩
---
Hint: We will be counting the most unavailable days (given by f)
```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
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
## 5 Plot the busiest day
---
```python
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
