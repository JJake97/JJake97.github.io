---
layout: signle
title: 'Python_DataFrame #1'
categories: Python_DataFrame
tag: Python
toc: true
author_profile: false
sidebar:
  nav: 'docs'
---



# DataFrame


```python
import pandas as pd
import numpy as np
```


```python
df = pd.read_csv('./world_cities.csv')
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>City / Urban area</th>
      <th>Country</th>
      <th>Population</th>
      <th>Land area (in sqKm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Buenos Aires</td>
      <td>Argentina</td>
      <td>11200000</td>
      <td>2266</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Melbourne</td>
      <td>Australia</td>
      <td>3162000</td>
      <td>2080</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Sydney</td>
      <td>Australia</td>
      <td>3502000</td>
      <td>1687</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Brisbane</td>
      <td>Australia</td>
      <td>1508000</td>
      <td>1603</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Perth</td>
      <td>Australia</td>
      <td>1177000</td>
      <td>964</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>City / Urban area</th>
      <th>Country</th>
      <th>Population</th>
      <th>Land area (in sqKm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>244</th>
      <td>245</td>
      <td>Canton</td>
      <td>USA</td>
      <td>267000</td>
      <td>372</td>
    </tr>
    <tr>
      <th>245</th>
      <td>246</td>
      <td>Spokane</td>
      <td>USA</td>
      <td>335000</td>
      <td>371</td>
    </tr>
    <tr>
      <th>246</th>
      <td>247</td>
      <td>Tashkent</td>
      <td>Uzbekistan</td>
      <td>2200000</td>
      <td>531</td>
    </tr>
    <tr>
      <th>247</th>
      <td>248</td>
      <td>Ho Chi Minh City</td>
      <td>Vietnam</td>
      <td>4900000</td>
      <td>518</td>
    </tr>
    <tr>
      <th>248</th>
      <td>249</td>
      <td>Harare</td>
      <td>Zimbabwe</td>
      <td>1750000</td>
      <td>712</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape
```




    (249, 5)




```python
df.columns
```




    Index(['Unnamed: 0', 'City / Urban area', 'Country', 'Population',
           'Land area (in sqKm)'],
          dtype='object')




```python
df.info()  ## 각 column의 정보
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 249 entries, 0 to 248
    Data columns (total 5 columns):
     #   Column               Non-Null Count  Dtype 
    ---  ------               --------------  ----- 
     0   Unnamed: 0           249 non-null    int64 
     1   City / Urban area    249 non-null    object
     2   Country              249 non-null    object
     3   Population           249 non-null    int64 
     4   Land area (in sqKm)  249 non-null    int64 
    dtypes: int64(3), object(2)
    memory usage: 9.9+ KB



```python
df.describe() ## 각 column의 통계값
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Population</th>
      <th>Land area (in sqKm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>249.000000</td>
      <td>2.490000e+02</td>
      <td>249.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>124.273092</td>
      <td>3.006538e+06</td>
      <td>1035.212851</td>
    </tr>
    <tr>
      <th>std</th>
      <td>72.369388</td>
      <td>4.136435e+06</td>
      <td>1033.487331</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>1.810000e+05</td>
      <td>365.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>62.000000</td>
      <td>5.980000e+05</td>
      <td>511.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>124.000000</td>
      <td>1.500000e+06</td>
      <td>684.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>187.000000</td>
      <td>3.502000e+06</td>
      <td>1116.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>249.000000</td>
      <td>3.320000e+07</td>
      <td>8683.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sort_values(by = 'Population', ascending = False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>City / Urban area</th>
      <th>Country</th>
      <th>Population</th>
      <th>Land area (in sqKm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>86</th>
      <td>86</td>
      <td>Tokyo/Yokohama</td>
      <td>Japan</td>
      <td>33200000</td>
      <td>6993</td>
    </tr>
    <tr>
      <th>141</th>
      <td>141</td>
      <td>New York Metro</td>
      <td>USA</td>
      <td>17800000</td>
      <td>8683</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Sao Paulo</td>
      <td>Brazil</td>
      <td>17700000</td>
      <td>1968</td>
    </tr>
    <tr>
      <th>123</th>
      <td>123</td>
      <td>Seoul/Incheon</td>
      <td>South Korea</td>
      <td>17500000</td>
      <td>1049</td>
    </tr>
    <tr>
      <th>94</th>
      <td>94</td>
      <td>Mexico City</td>
      <td>Mexico</td>
      <td>17400000</td>
      <td>2072</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>223</th>
      <td>224</td>
      <td>Asheville</td>
      <td>USA</td>
      <td>222000</td>
      <td>536</td>
    </tr>
    <tr>
      <th>243</th>
      <td>244</td>
      <td>Bonita Springs / Naples</td>
      <td>USA</td>
      <td>221000</td>
      <td>389</td>
    </tr>
    <tr>
      <th>238</th>
      <td>239</td>
      <td>Huntsville</td>
      <td>USA</td>
      <td>213000</td>
      <td>407</td>
    </tr>
    <tr>
      <th>220</th>
      <td>221</td>
      <td>Hickory</td>
      <td>USA</td>
      <td>188000</td>
      <td>546</td>
    </tr>
    <tr>
      <th>57</th>
      <td>57</td>
      <td>Pau</td>
      <td>France</td>
      <td>181000</td>
      <td>450</td>
    </tr>
  </tbody>
</table>
<p>249 rows × 5 columns</p>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>City / Urban area</th>
      <th>Country</th>
      <th>Population</th>
      <th>Land area (in sqKm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Buenos Aires</td>
      <td>Argentina</td>
      <td>11200000</td>
      <td>2266</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Melbourne</td>
      <td>Australia</td>
      <td>3162000</td>
      <td>2080</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Sydney</td>
      <td>Australia</td>
      <td>3502000</td>
      <td>1687</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Brisbane</td>
      <td>Australia</td>
      <td>1508000</td>
      <td>1603</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Perth</td>
      <td>Australia</td>
      <td>1177000</td>
      <td>964</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>244</th>
      <td>245</td>
      <td>Canton</td>
      <td>USA</td>
      <td>267000</td>
      <td>372</td>
    </tr>
    <tr>
      <th>245</th>
      <td>246</td>
      <td>Spokane</td>
      <td>USA</td>
      <td>335000</td>
      <td>371</td>
    </tr>
    <tr>
      <th>246</th>
      <td>247</td>
      <td>Tashkent</td>
      <td>Uzbekistan</td>
      <td>2200000</td>
      <td>531</td>
    </tr>
    <tr>
      <th>247</th>
      <td>248</td>
      <td>Ho Chi Minh City</td>
      <td>Vietnam</td>
      <td>4900000</td>
      <td>518</td>
    </tr>
    <tr>
      <th>248</th>
      <td>249</td>
      <td>Harare</td>
      <td>Zimbabwe</td>
      <td>1750000</td>
      <td>712</td>
    </tr>
  </tbody>
</table>
<p>249 rows × 5 columns</p>
</div>




```python
df['Country']
```




    0       Argentina
    1       Australia
    2       Australia
    3       Australia
    4       Australia
              ...    
    244           USA
    245           USA
    246    Uzbekistan
    247       Vietnam
    248      Zimbabwe
    Name: Country, Length: 249, dtype: object




```python
df['City / Urban area'].unique()
```




    array(['Buenos Aires', 'Melbourne', 'Sydney', 'Brisbane', 'Perth',
           'Adelaide', 'Gold Coast', 'Vienna', 'Baku/Sumqayit', 'Brussels',
           'Antwerp', 'Sao Paulo', 'Rio de Janeiro', 'Belo Horizonte',
           'Curitiba', 'Brasilia', 'Fortaleza', 'Porto Alegre', 'Campinas',
           'Goiania', 'Recife', 'Phnom Penh', 'Montreal.', 'Toronto',
           'Vancouver', 'Edmonton', 'Calgary', 'Quebec', 'Ottawa/Hull',
           'Winnipeg', 'St. Catharines', 'Santiago', 'Beijing', 'Shanghai',
           'Shenzhen', 'Shenyang', 'Tianjin', 'Dalian', 'Bogota', 'Kinshasa',
           'Lumumbashi', 'Copenhagen', 'Quito', 'Cairo', 'Helsinki', 'Paris',
           'Marseille', 'Bordeaux', 'Lyon', 'Toulouse', 'Nice', 'Toulon',
           'Avignon', 'Valenciennes', 'Douai/Lens', 'Nantes', 'Lille', 'Pau',
           'Tours', 'Bethune', 'Essen/Düsseldorf', 'Berlin', 'Frankfurt',
           'Hamburg', 'Cologne/Bonn', 'Munich', 'Stuttgart', 'Aachen',
           'Accra', 'Athens', 'Budapest', 'Delhi', 'Hyderabad', 'Bangalore',
           'Kolkata', 'Mumbai', 'Chennai', 'Jakarta', 'Tehran', 'Baghdad',
           'Dublin', 'Tel Aviv', 'Milan', 'Rome', 'Naples', 'Turin',
           'Tokyo/Yokohama', 'Nagoya', 'Osaka/Kobe/Kyoto', 'Fukuoka',
           'Sapporo', 'Kuwait', 'Beirut', 'Kuala Lumpur', 'Mexico City',
           'Guadalajara', 'Monterey', 'Rotterdam', 'Auckland', 'Lagos',
           'Lahore', 'Karachi', 'Lima', 'Manila', 'Katowice', 'Warsaw',
           'Lisbon', 'Porto', 'San Juan', 'Aguadilla', 'Moscow',
           'St Petersburg', 'Nizhni Novgorod', 'Arabia', 'Riyadh', 'Jeddah',
           'Singapore', 'Johannesburg/East Rand', 'Durban', 'Cape Town',
           'Pretoria', 'Vereeniging', 'Port Elizabeth', 'Seoul/Incheon',
           'Madrid', 'Barcelona', 'Khartoum', 'Stockholm', 'Taichung',
           'Taipei', 'Bangkok', 'Istanbul', 'Ankara', 'Abu Dhabi', 'Dubai',
           'London', 'Birmingham', 'Manchester', 'Leeds/Bradford', 'Glasgow',
           'Donetsk', 'New York Metro', 'Chicago', 'Atlanta', 'Philadelphia',
           'Boston', 'Los Angeles', 'Dallas/Fort Worth', 'Houston', 'Detroit',
           'Washington', 'Miami', 'Seattle', 'Minneapolis/St. Paul',
           'Pittsburgh', 'St. Louis', 'Tampa//St. Petersburg', 'Phoenix/Mesa',
           'San Diego', 'Baltimore', 'Cincinnati', 'Cleveland', 'Kansas City',
           'Indianapolis', 'San Francisco//Oakland', 'Virginia Beach',
           'Providence', 'Denver', 'Milwaukee', 'Portland', 'Hartford',
           'Bridgeport//Stamford', 'Orlando', 'Riverside/San Bernardino',
           'Richmond', 'Charlotte', 'Nashville', 'Jacksonville',
           'San Antonio', 'Memphis', 'Columbus', 'Louisville', 'Sacramento',
           'Buffalo', 'Knoxville', 'Dayton', 'Oklahoma City', 'Raleigh',
           'Austin', 'McAllen', 'Springfield', 'Akron', 'Rochester', 'Tucson',
           'Chattanooga', 'Allentown/Bethlehem', 'Barnstable Town',
           'Las Vegas', 'New Haven', 'Albany', 'Baton Rouge',
           'Sarasota//Bradenton', 'Columbia', 'Poughkeepsie', 'Tulsa',
           'San Jose', 'Grand Rapids', 'Winston/Salem', 'Worcester',
           'Augusta', 'Flint', 'Charleston', 'Salt Lake City', 'Youngstown',
           'Greenville', 'Omaha', 'Albuquerque', 'Palm Bay', 'El Paso',
           'Pensacola', 'Hickory', 'Mobile', 'Harrisburg', 'Asheville',
           'Little Rock', 'Toledo', 'Lancaster', 'New Orleans',
           'Colorado Springs', 'Cape Coral', 'Ogden', 'Syracuse', 'Wichita',
           'Concord', 'Port St Lucie', 'Fayetteville', 'Jackson', 'Scranton',
           'Huntsville', 'Durham', 'South Bend', 'Shreveport', 'Honolulu',
           'Bonita Springs / Naples', 'Canton', 'Spokane', 'Tashkent',
           'Ho Chi Minh City', 'Harare'], dtype=object)




```python
df['City / Urban area'].value_counts()
```




    Buenos Aires            1
    Bridgeport//Stamford    1
    San Diego               1
    Baltimore               1
    Cincinnati              1
                           ..
    Osaka/Kobe/Kyoto        1
    Fukuoka                 1
    Sapporo                 1
    Kuwait                  1
    Harare                  1
    Name: City / Urban area, Length: 249, dtype: int64




```python
df['City / Urban area'].describe()
```




    count              249
    unique             249
    top       Buenos Aires
    freq                 1
    Name: City / Urban area, dtype: object




```python
df['Country'].value_counts()
```




    USA            105
    France          15
    Brazil          10
    Canada           9
    Germany          8
                  ... 
    Israel           1
    Kuwait           1
    Malaysia         1
    Netherlands      1
    Zimbabwe         1
    Name: Country, Length: 61, dtype: int64




```python
df['Country'].describe()
```




    count     249
    unique     61
    top       USA
    freq      105
    Name: Country, dtype: object




```python
pop_dens = df['Population'] / df['Land area (in sqKm)']
```


```python
df['pop_dens'] = pop_dens
```


```python
df_high_density = df[df['pop_dens'] > 10000]
```


```python
df_high_density.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 19 entries, 32 to 129
    Data columns (total 6 columns):
     #   Column               Non-Null Count  Dtype  
    ---  ------               --------------  -----  
     0   Unnamed: 0           19 non-null     int64  
     1   City / Urban area    19 non-null     object 
     2   Country              19 non-null     object 
     3   Population           19 non-null     int64  
     4   Land area (in sqKm)  19 non-null     int64  
     5   pop_dens             19 non-null     float64
    dtypes: float64(1), int64(3), object(2)
    memory usage: 1.0+ KB



```python
df.sort_values(by = 'pop_dens', ascending = False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>City / Urban area</th>
      <th>Country</th>
      <th>Population</th>
      <th>Land area (in sqKm)</th>
      <th>pop_dens</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>75</th>
      <td>75</td>
      <td>Mumbai</td>
      <td>India</td>
      <td>14350000</td>
      <td>484</td>
      <td>29648.760331</td>
    </tr>
    <tr>
      <th>74</th>
      <td>74</td>
      <td>Kolkata</td>
      <td>India</td>
      <td>12700000</td>
      <td>531</td>
      <td>23917.137476</td>
    </tr>
    <tr>
      <th>101</th>
      <td>101</td>
      <td>Karachi</td>
      <td>Pakistan</td>
      <td>9800000</td>
      <td>518</td>
      <td>18918.918919</td>
    </tr>
    <tr>
      <th>99</th>
      <td>99</td>
      <td>Lagos</td>
      <td>Nigeria</td>
      <td>13400000</td>
      <td>738</td>
      <td>18157.181572</td>
    </tr>
    <tr>
      <th>34</th>
      <td>34</td>
      <td>Shenzhen</td>
      <td>China</td>
      <td>8000000</td>
      <td>466</td>
      <td>17167.381974</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>194</th>
      <td>195</td>
      <td>Chattanooga</td>
      <td>USA</td>
      <td>344000</td>
      <td>751</td>
      <td>458.055925</td>
    </tr>
    <tr>
      <th>223</th>
      <td>224</td>
      <td>Asheville</td>
      <td>USA</td>
      <td>222000</td>
      <td>536</td>
      <td>414.179104</td>
    </tr>
    <tr>
      <th>57</th>
      <td>57</td>
      <td>Pau</td>
      <td>France</td>
      <td>181000</td>
      <td>450</td>
      <td>402.222222</td>
    </tr>
    <tr>
      <th>220</th>
      <td>221</td>
      <td>Hickory</td>
      <td>USA</td>
      <td>188000</td>
      <td>546</td>
      <td>344.322344</td>
    </tr>
    <tr>
      <th>196</th>
      <td>197</td>
      <td>Barnstable Town</td>
      <td>USA</td>
      <td>244000</td>
      <td>741</td>
      <td>329.284750</td>
    </tr>
  </tbody>
</table>
<p>249 rows × 6 columns</p>
</div>




```python
cnts = df['Country'].value_counts()
```


```python
cnts[cnts == 4]
```




    Italy    4
    Name: Country, dtype: int64



## 정리

1. read_csv(): csv 확장자 파일을 읽어들이는 기능
2. head(): 맨 앞의 5개 row를 보여주는 기능
3. tail(): 맨 뒤의 5개 row를 보여주는 기능
4. shape: 데이터가 몇행 몇열로 이루어져 있는지 보여주는 기능
5. columns: Data 행의 헤더를 보여주는 기능
6. info(): 데이터프레임 각 column의 정보를 보여주는 기능
7. describe(): 각 column의 통계값을 보여주는 기능
8. unique(): 데이터 중복값을 제거해서 보여주는 기능
9. value_counts(): 각 데이터들의 개수를 파악해주는 기능
10. sort_values(): 특정 행을 기준으로 정렬해주는 기능


```python

```
