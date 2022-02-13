## 파이그래프

- 비율을 나타내는 그래프
- 절대적인 수치보다 비율을 표현할 때 유리한 그래프


```python
%matplotlib inline
import pandas as pd
```

### 파이그래프 실습


```python
df = pd.read_csv('data/silicon_valley_details.csv')
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
      <th>company</th>
      <th>year</th>
      <th>race</th>
      <th>gender</th>
      <th>job_category</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>23andMe</td>
      <td>2016</td>
      <td>Hispanic_or_Latino</td>
      <td>male</td>
      <td>Executives</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>23andMe</td>
      <td>2016</td>
      <td>Hispanic_or_Latino</td>
      <td>male</td>
      <td>Managers</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>23andMe</td>
      <td>2016</td>
      <td>Hispanic_or_Latino</td>
      <td>male</td>
      <td>Professionals</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23andMe</td>
      <td>2016</td>
      <td>Hispanic_or_Latino</td>
      <td>male</td>
      <td>Technicians</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23andMe</td>
      <td>2016</td>
      <td>Hispanic_or_Latino</td>
      <td>male</td>
      <td>Sales workers</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.drop(df[df['count'] == 0].index, inplace = True)
```


```python
pie_graph = df[df['company'] == 'Adobe']
```


```python
filter = pie_graph['race'] == 'Overall_totals'
del_totals = (pie_graph['job_category'] != 'Totals') & (pie_graph['job_category'] != 'Previous_totals')
result = pie_graph[filter & del_totals]
result.set_index('job_category', inplace = True)
```


```python
result.plot(y = 'count', kind = 'pie')
```




    <AxesSubplot:ylabel='count'>




    
![png](output_8_1.png)
    


## 히스토그램

- 데이터를 범위로 묶어서 시각화하는 형태의 그래프


```python
df = pd.read_csv('data/body.csv', index_col = 0)
```


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
      <th>Height</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>Number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>176.0</td>
      <td>85.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>175.3</td>
      <td>67.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>168.6</td>
      <td>75.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>168.1</td>
      <td>67.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>175.3</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>996</th>
      <td>171.8</td>
      <td>68.2</td>
    </tr>
    <tr>
      <th>997</th>
      <td>171.5</td>
      <td>75.6</td>
    </tr>
    <tr>
      <th>998</th>
      <td>177.9</td>
      <td>66.5</td>
    </tr>
    <tr>
      <th>999</th>
      <td>174.4</td>
      <td>72.0</td>
    </tr>
    <tr>
      <th>1000</th>
      <td>173.5</td>
      <td>77.4</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 2 columns</p>
</div>




```python
df.plot(kind = 'hist', y = 'Height')
```




    <AxesSubplot:ylabel='Frequency'>




    
![png](output_12_1.png)
    



```python
df.plot(kind = 'hist', y = 'Height', bins = 15)
```




    <AxesSubplot:ylabel='Frequency'>




    
![png](output_13_1.png)
    


히스토그램의 구간을 나누는 파라미터는 'bins'이며 숫자가 클수록 더 잘게 쪼갠다


```python
df.plot(kind = 'hist', y = 'Height', bins = 200)
```




    <AxesSubplot:ylabel='Frequency'>




    
![png](output_15_1.png)
    


'bins'를 너무 크게할 경우 오히려 분석에 불리해진다.

## Box Plot

- 데이터셋의 통계정보를 시각적으로 보여주기위해 사용된다
- 최댓값, 최솟값, 중앙값, Q1, Q3, IQR


```python
df = pd.read_csv('data/exam.csv', index_col = 0)

df.plot(y = ['math score', 'reading score', 'writing score'], kind = 'box')
```




    <AxesSubplot:>




    
![png](output_18_1.png)
    


### Box Plot Insight

- 데이터의 분산된 정도를 파악할 수 있다(Box의 길이)
- 대량의 데이터셋의 통계값도 어느정도 파악할 수 있다

## 산점도

- 상관관계를 보여주기에 적합한 그래프


```python
df = pd.read_csv('data/exam.csv', index_col = 0)
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
      <th>race/ethnicity</th>
      <th>parental level of education</th>
      <th>lunch</th>
      <th>test preparation course</th>
      <th>math score</th>
      <th>reading score</th>
      <th>writing score</th>
    </tr>
    <tr>
      <th>gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>group B</td>
      <td>bachelor's degree</td>
      <td>standard</td>
      <td>none</td>
      <td>72</td>
      <td>72</td>
      <td>74</td>
    </tr>
    <tr>
      <th>female</th>
      <td>group C</td>
      <td>some college</td>
      <td>standard</td>
      <td>completed</td>
      <td>69</td>
      <td>90</td>
      <td>88</td>
    </tr>
    <tr>
      <th>female</th>
      <td>group B</td>
      <td>master's degree</td>
      <td>standard</td>
      <td>none</td>
      <td>90</td>
      <td>95</td>
      <td>93</td>
    </tr>
    <tr>
      <th>male</th>
      <td>group A</td>
      <td>associate's degree</td>
      <td>free/reduced</td>
      <td>none</td>
      <td>47</td>
      <td>57</td>
      <td>44</td>
    </tr>
    <tr>
      <th>male</th>
      <td>group C</td>
      <td>some college</td>
      <td>standard</td>
      <td>none</td>
      <td>76</td>
      <td>78</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.plot(kind = 'scatter', x = 'math score', y = 'reading score')
```




    <AxesSubplot:xlabel='math score', ylabel='reading score'>




    
![png](output_22_1.png)
    



```python
df.plot(kind = 'scatter', x = 'reading score', y = 'writing score')
```




    <AxesSubplot:xlabel='reading score', ylabel='writing score'>




    
![png](output_23_1.png)
    


산점도를 그려 비교해보았을 때 수학과 읽기 성적보다 읽기와 쓰기 성적의 상관관계가 더 높다


```python
df.corr()
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
      <th>math score</th>
      <th>reading score</th>
      <th>writing score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>math score</th>
      <td>1.000000</td>
      <td>0.817580</td>
      <td>0.802642</td>
    </tr>
    <tr>
      <th>reading score</th>
      <td>0.817580</td>
      <td>1.000000</td>
      <td>0.954598</td>
    </tr>
    <tr>
      <th>writing score</th>
      <td>0.802642</td>
      <td>0.954598</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



상관계수를 비교해보면 수치적으로 더욱 명확하게 관계를 파악할 수 있다


```python

```
