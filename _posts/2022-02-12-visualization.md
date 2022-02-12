# 시각화

- row data를 활용하는 것 보다 분석에 도움을 준다
- outlier를 찾을 때 도움을 준다
- reporting에 도움을 준다
- 선그래프, 막대그래프, 파이그래프 등 여러가지 그래프들이 있다.

## 선그래프

- 변화를 보여주기에 적합한 그래프
- 데이터가 숫자로 이루어져있어야 활용이 가능한 그래프


```python
%matplotlib inline

import pandas as pd
```


```python
df = pd.read_csv('data/broadcast.csv', index_col = 0)
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
      <th>KBS</th>
      <th>MBC</th>
      <th>SBS</th>
      <th>TV CHOSUN</th>
      <th>JTBC</th>
      <th>Channel A</th>
      <th>MBN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2011</th>
      <td>35.951</td>
      <td>18.374</td>
      <td>11.173</td>
      <td>9.102</td>
      <td>7.380</td>
      <td>3.771</td>
      <td>2.809</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>36.163</td>
      <td>16.022</td>
      <td>11.408</td>
      <td>8.785</td>
      <td>7.878</td>
      <td>5.874</td>
      <td>3.310</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>31.989</td>
      <td>16.778</td>
      <td>9.673</td>
      <td>9.026</td>
      <td>7.810</td>
      <td>5.350</td>
      <td>3.825</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>31.210</td>
      <td>15.663</td>
      <td>9.108</td>
      <td>9.440</td>
      <td>7.490</td>
      <td>5.776</td>
      <td>4.572</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>27.777</td>
      <td>16.573</td>
      <td>9.099</td>
      <td>9.940</td>
      <td>7.267</td>
      <td>6.678</td>
      <td>5.520</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>27.583</td>
      <td>14.982</td>
      <td>8.669</td>
      <td>9.829</td>
      <td>7.727</td>
      <td>6.624</td>
      <td>5.477</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>26.890</td>
      <td>12.465</td>
      <td>8.661</td>
      <td>8.886</td>
      <td>9.453</td>
      <td>6.056</td>
      <td>5.215</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.plot(kind = 'line')
```




    <AxesSubplot:>




![output_4_1](/assets/images/output_4_1.png)


선그래프를 활용하면 데이터의 추이를 확인하는데 편리하다


```python
df.plot(y = 'KBS')
```




    <AxesSubplot:>




![output_6_1](/assets/images/output_6_1.png)



```python
df.plot(y = ["KBS", 'JTBC'])
```




    <AxesSubplot:>




![output_7_1](/assets/images/output_7_1.png)



```python
df[['KBS', 'JTBC']]
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
      <th>KBS</th>
      <th>JTBC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2011</th>
      <td>35.951</td>
      <td>7.380</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>36.163</td>
      <td>7.878</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>31.989</td>
      <td>7.810</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>31.210</td>
      <td>7.490</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>27.777</td>
      <td>7.267</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>27.583</td>
      <td>7.727</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>26.890</td>
      <td>9.453</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[['KBS', 'JTBC']].plot()
```




    <AxesSubplot:>




![output_9_1](/assets/images/output_9_1.png)



```python
df['KBS'].plot()
```




    <AxesSubplot:>




![output_10_1](/assets/images/output_10_1.png)


pandas DataFrame의 plot()의 default 값은 선그래프이다.

## 막대그래프

- 다양한 카테고리를 특정 기준으로 비교하기위해 사용하는 그래프


```python
%matplotlib inline

import pandas as pd
df = pd.read_csv('data/sports.csv', index_col = 0)
```


```python
df.plot(kind='bar')
```




    <AxesSubplot:>




![output_14_1](/assets/images/output_14_1.png)



```python
df.plot(kind = 'bar', stacked = True)
```




    <AxesSubplot:>




![output_15_1](/assets/images/output_15_1.png)


stacked 기능을 활용해서 데이터가 쌓이는 형태의 그래프를 그릴수도 있다

### 막대그래프 실습

- 실리콘밸리에서 일하는 남자 관리자에 대한 인종 분포를 그리는 실습


```python
# 데이터 읽어들이기
df = pd.read_csv('data/silicon_valley_summary.csv')

# 문제의 조건에 맞게 데이터 자르기
df = df[(df['job_category'] == 'Managers') & (df['gender'] == 'Male') & (df['race_ethnicity'] != 'All')]

# 데이터 인덱싱 및 인종 정보를 데이터프레임의 인덱스로 설정
df = df[['race_ethnicity', 'count']]
df.set_index('race_ethnicity', inplace = True)

# 그래프 그리기
df.plot(y = 'count', kind = 'bar')
```




    <AxesSubplot:xlabel='race_ethnicity'>




![output_18_1](/assets/images/output_18_1.png)

