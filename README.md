

```python
import matplotlib.pyplot as plt
import seaborn as sns

import pandas as pd
import numpy as np
```


```python
# Import and read the data
City_data = pd.read_csv('../MatPlotLibHW/city_data.csv')
Ride_data = pd.read_csv('../MatPlotLibHW/Ride_data.csv')

City_data.head(), Ride_data.head()
```




    (             city  driver_count   type
     0      Kelseyland            63  Urban
     1      Nguyenbury             8  Urban
     2    East Douglas            12  Urban
     3   West Dawnfurt            34  Urban
     4  Rodriguezburgh            52  Urban,
               city                 date   fare        ride_id
     0     Sarabury  2016-01-16 13:49:27  38.35  5403689035038
     1    South Roy  2016-01-02 18:42:34  17.49  4036272335942
     2  Wiseborough  2016-01-21 17:35:29  44.18  3645042422587
     3  Spencertown  2016-07-31 14:53:22   6.87  2242596575892
     4   Nguyenbury  2016-07-09 04:42:44   6.28  1543057793673)




```python
#Merging the Data by City

CityRide_df = pd.merge(City_data, Ride_data, on='city', how='outer')

del CityRide_df['ride_id']

CityRide_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Adding Total Rides Count to DF
CityRide_df['ride_count'] = CityRide_df.groupby('city')['city'].transform('count')

CityRide_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Groupby City name


CityGroup = CityRide_df.groupby(['city', 'type']).mean()

CityGroup.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>driver_count</th>
      <th>fare</th>
      <th>ride_count</th>
    </tr>
    <tr>
      <th>city</th>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <th>Urban</th>
      <td>21</td>
      <td>23.928710</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <th>Urban</th>
      <td>67</td>
      <td>20.609615</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <th>Suburban</th>
      <td>16</td>
      <td>37.315556</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <th>Urban</th>
      <td>21</td>
      <td>23.625000</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <th>Urban</th>
      <td>49</td>
      <td>21.981579</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create Bubble Chart with Data

colors = ["Gold", "LightSkyBlue", "LightCoral"]

CityGroup.plot(kind="scatter", x="ride_count", y="fare", s=CityGroup["driver_count"]*10, c=colors, edgecolors="grey", title=" Pyber Ride Sharing Data")
plt.style.use('seaborn-whitegrid')
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.figtext(0.5, 0,"Note: Circle size corresponds with driver count per city", wrap=True,
            horizontalalignment='left', fontsize=8)
plt.legend()
plt.ylim(15,45)
plt.xlim(0,40)

plt.show()

```


![png](output_5_0.png)



```python
#Pie Chart by City TYpe
CityType_df = CityRide_df.groupby(['type']).sum()

CityType_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>driver_count</th>
      <th>fare</th>
      <th>ride_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>727</td>
      <td>4255.09</td>
      <td>1015</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>9730</td>
      <td>20335.69</td>
      <td>13475</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>64501</td>
      <td>40078.34</td>
      <td>41251</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.title("% of Total Fares by City Type")
CityType = ["Rural", "Suburban", "Urban"]
TotalFares = [4255, 20335, 40078]
colors = ["Gold", "LightSkyBlue", "LightCoral"]

plt.pie(TotalFares, labels=CityType, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.axis("equal")
plt.show()
```


![png](output_7_0.png)



```python
plt.title("% of Total Drivers by City Type")
CityType = ["Rural", "Suburban", "Urban"]
TotalDrivers = [727, 9730, 64501]
colors = ["Gold", "LightSkyBlue", "LightCoral"]

plt.pie(TotalDrivers, labels=CityType, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=120)
plt.axis("equal")
plt.show()
```


![png](output_8_0.png)



```python

CityType = ["Rural", "Suburban", "Urban"]
TotalRides = [125, 657, 1625]
colors = ["Gold", "LightSkyBlue", "LightCoral"]

plt.title("% of Total Rides by City Type")
plt.pie(TotalRides, labels=CityType, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=120)
plt.axis("equal")
plt.show()
```


![png](output_9_0.png)



```python
# Three observable trends in Pyber Data:
    # Although the Urban and Suburban environments have the most drivers and rides, the Rural environments provide the greater profits. Therefore the company would be well advised to recruit more drivers in Rural environments.
    # But the number of drivers also tends to bring down the average fare amount, especially in Urban areas
    # Despite having a smaller proportion of drivers, Suburban areas have higher demands for rides.
```
